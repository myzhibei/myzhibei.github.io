---
show_in_list: true
layout: post
title: "Diffusion Model Serving: Why It Matters for Systems"
date: 2025-07-15
author: Yanying Lin
description: "Exploring why diffusion models matter for AI infrastructure, their fundamental differences from LLMs, and insights from production serving systems. A deep dive into computational patterns, memory subsystems, and the future of diffusion-based LLMs."
tags: [Diffusion Models, AI Infrastructure]
categories: [Research, Systems]
---


In today's production AI clusters, two workloads dominate the inference landscape: Stable Diffusion (SD) serving and Large Language Model (LLM) serving. While LLMs have captured significant attention in both research and industry, diffusion models represent an equally critical and fundamentally different class of workloads that demand specialized system design. Understanding why diffusion models matter—and how they differ from LLMs at the system level—is essential for building efficient, scalable AI infrastructure.

## Why Stable Diffusion Serving?

Stable Diffusion and LLM serving are the two dominant inference workloads in production clusters, with both reaching 10,000+ QPS at peak. However, they exhibit dramatically different characteristics. SD generation takes tens of seconds per image, while LLM generation operates at token-level latency (milliseconds per token). SD operates through multi-stage pipelines with base models (1-20 GB), LoRA adapters (100 MB - 1 GB), and ControlNet modules (0.5-10 GB). Over 1.6 million possible pipeline combinations exist in production environments, creating unprecedented system complexity.

The diffusion pipeline consists of three main stages:

1. Text encoding: CLIP text model performs a single forward pass to encode prompts into embeddings
2. Iterative denoising: UNet executes in a loop (typically 20-50 steps), where each step depends on the previous output
3. Image decoding: VAE decoder performs a single forward pass to convert latent features into pixel images

This multi-stage, iterative architecture fundamentally differs from the autoregressive nature of LLMs, leading to distinct system requirements and optimization opportunities.

## SD vs. LLM: Core Differences

From a systems perspective, Stable Diffusion and Large Language Models represent two fundamentally different computational paradigms.

### Computational Patterns

Stable Diffusion is a hybrid, multi-stage inference pipeline centered on iterative denoising through a diffusion model. Its computation is primarily convolution-based, with extreme demands on memory bandwidth and capacity, and exhibits clear stage transitions.

Large Language Models are autoregressive, single-stage inference engines centered on attention mechanisms. Their computation is dominated by matrix multiplication (GEMM), with sensitivity to compute throughput and latency, and strict sequential dependencies.

The forward diffusion process can be mathematically described as:

$$q(x_t | x_{t-1}) = \mathcal{N}(x_t; \sqrt{1-\beta_t}x_{t-1}, \beta_t I)$$

where $\beta_t$ is the noise schedule at step $t$. The reverse denoising process learns to approximate:

$$p_\theta(x_{t-1} | x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t, t), \Sigma_\theta(x_t, t))$$

This iterative nature means that each denoising step requires the full UNet forward pass, making activation memory the primary bottleneck rather than model weights.

### Memory Subsystem

| Dimension | Stable Diffusion | Large Language Models |
|:---|:---|:---|
| Model Weights | Relatively small (SD 1.5: ~2.5 GB total) | Extremely large (7B: ~14 GB, 70B: ~140 GB) |
| Activation Memory | Peak activation is extremely high—each denoising step requires storing all UNet intermediate activations | Depends on sequence length; KV Cache grows linearly with batch and sequence length |
| Primary Bottleneck | Activation memory capacity limits image resolution and batch size | Model weights and KV Cache memory bandwidth |

For SD, the activation memory bottleneck becomes more severe at higher resolutions. A 1024×1024 image requires significantly more activation memory than a 512×512 image, even with the same model weights.

### Execution Flow

Stable Diffusion uses a multi-stage, conditional pipeline. Text encoding performs a single forward pass. Iterative denoising executes UNet in a loop (20-50 steps), where each step depends on previous output. Image decoding performs a single forward pass.

Large Language Models use an autoregressive, single-stage loop. The encoding phase performs one complete forward pass to generate initial KV Cache. The decoding phase executes in a loop, generating one token per iteration and updating KV Cache.

The key difference: SD's parallelism is limited by the sequential nature of denoising steps, while LLM's parallelism is limited by the sequential nature of token generation.

### System Optimization Focus

For SD, the focus is on reducing activation memory, optimizing convolutions, and managing multi-stage pipelines. For LLMs, the focus is on maximizing GEMM efficiency, managing KV Cache, and achieving low-latency distributed inference.

In summary, SD is a memory-capacity/bandwidth-sensitive image processing pipeline, while LLM is a compute-throughput/communication-sensitive sequence generation engine.

## Key Insights from Production

Our analysis of production clusters reveals several critical insights that challenge conventional wisdom about serving diffusion models.

### Insight 1: Request Skew Causes Performance Inversion

Model popularity exhibits extreme inequality with a Gini coefficient of 0.876. The top 5% of models handle 78% of all requests. However, we observe a paradox: hot models complete in 29 seconds on average, while cold models complete in 25.8 seconds.

The Gini coefficient, which measures inequality, is calculated as:

$$G = \frac{2 \sum_{i=1}^{n} i \cdot x_i}{n \sum_{i=1}^{n} x_i} - \frac{n+1}{n}$$

where $x_i$ represents the request count for model $i$ sorted in ascending order. A value of 0.876 indicates extreme concentration.

Why the paradox? Resource contention offsets cache warmth benefits. When many requests target the same popular models, they compete for GPU memory, compute resources, and I/O bandwidth, negating the advantage of having models pre-loaded in cache.

This has several implications. Head models need persistent multi-replica placement with GPU reservation. Tail models should rely on host/SSD tiers with prefetch triggers. Schedulers must route by popularity bands to separate hot and cold pools.

### Insight 2: Resource Utilization Paradox

98.4% of pods operate below 20% GPU utilization, yet users experience high latency. Computation consumes only 15-30% of end-to-end latency, with 70-85% of time lost to orchestration overhead.

This reveals that SD serving is memory-bandwidth bound, not compute-bound. Traditional GPU utilization metrics (which measure SM compute activity) are misleading for diffusion workloads. Memory bandwidth, not SM compute, caps throughput. Scheduler decisions must be memory-aware, not compute-centric. Utilization metrics must expose memory bandwidth saturation.

### Insight 3: Cache Replacement Overhead

Base model refreshes cost 22.6 seconds (5× LoRA updates). During replacement bursts, network traffic increases by 345%, while disk I/O only increases by 26%, indicating that intermediate SSD cache layers are underutilized.

This has several implications. Cost-aware eviction policies must weight load cost, reuse probability, and size. Replacement must coordinate with scaling to avoid cache thrashing. Simple LRU fails for heterogeneous component characteristics.

## Looking Forward: Diffusion-based LLMs

As we look to the future, an exciting development is emerging: Diffusion-based Large Language Models. These models combine the iterative denoising process of diffusion models with the sequence generation capabilities of LLMs, creating a fundamentally new computational paradigm.

This convergence will have profound implications for inference systems. The hybrid nature of diffusion-based LLMs will require rethinking how we allocate GPU memory, compute, and bandwidth. The iterative denoising process combined with attention mechanisms creates unique resource demands that differ from both pure diffusion models and traditional LLMs. Current kernels are optimized for either convolution-heavy (diffusion) or GEMM-heavy (LLM) workloads. Diffusion-based LLMs will require novel kernel designs that efficiently handle both computational patterns within a single forward pass. The memory access patterns will fundamentally change. We'll need to manage both the activation memory from iterative denoising steps and the KV Cache from attention mechanisms, with complex interactions between these two memory systems. The entire inference stack—from scheduling and caching to memory management and kernel optimization—will need to be redesigned to handle this new workload class efficiently.

This represents a fascinating and important research direction that will reshape the foundations of AI inference systems. Understanding how to serve diffusion models effectively today provides crucial insights for building the next generation of AI infrastructure that can handle these emerging hybrid models.

---
Diffusion model serving presents unique challenges that cannot be addressed by simply adapting LLM serving techniques. The multi-stage, memory-bandwidth-bound nature of diffusion pipelines requires specialized system design. As diffusion-based LLMs emerge, the lessons learned from production diffusion serving will become even more critical, as these hybrid models will require us to rethink resource usage, CUDA kernels, and data access patterns at a fundamental level.

The future of AI inference systems will be shaped by our ability to efficiently serve these diverse and evolving workloads. Understanding diffusion models is not just about today's image generation—it's about preparing for the next generation of AI systems.

