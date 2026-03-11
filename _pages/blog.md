---
layout: page
permalink: /blog/
title: Blog
nav: false
nav_order: 4
---

<style>
  .blog-filter {
    margin-bottom: 2rem;
    text-align: center;
  }
  
  .filter-btn {
    display: inline-block;
    padding: 0.5rem 1.25rem;
    margin: 0.25rem;
    border: 1px solid var(--global-text-color);
    background-color: var(--global-bg-color);
    color: var(--global-text-color);
    border-radius: 20px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 0.9rem;
  }
  
  .filter-btn:hover,
  .filter-btn.active {
    background-color: var(--global-theme-color);
    color: var(--global-card-bg-color);
    border-color: var(--global-theme-color);
  }
  
  .blog-posts {
    display: grid;
    gap: 1.5rem;
  }
  
  .blog-post-card {
    padding: 1.5rem;
    border: 1px solid var(--global-divider-color);
    border-radius: 8px;
    background-color: var(--global-bg-color);
    transition: all 0.3s ease;
    opacity: 1;
    transform: scale(1);
  }
  
  .blog-post-card.hidden {
    display: none;
  }
  
  .blog-post-card:hover {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    transform: translateY(-2px);
    border-color: var(--global-theme-color);
  }
  
  .blog-post-date {
    color: var(--global-text-color-light);
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
  }
  
  .blog-post-title {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 0.75rem;
    color: var(--global-text-color);
  }
  
  .blog-post-title a {
    color: inherit;
    text-decoration: none;
  }
  
  .blog-post-title a:hover {
    color: var(--global-theme-color);
  }
  
  .blog-post-tags {
    margin-top: 0.75rem;
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
  }
  
  .blog-tag {
    display: inline-block;
    padding: 0.25rem 0.75rem;
    background-color: var(--global-code-bg-color);
    color: var(--global-text-color);
    border-radius: 12px;
    font-size: 0.85rem;
    cursor: pointer;
    transition: all 0.2s ease;
  }
  
  .blog-tag:hover {
    background-color: var(--global-theme-color);
    color: var(--global-card-bg-color);
  }
  
  .blog-post-category {
    display: inline-block;
    padding: 0.25rem 0.75rem;
    background-color: rgba(0, 118, 223, 0.1);
    color: #0076df;
    border-radius: 12px;
    font-size: 0.85rem;
    margin-right: 0.5rem;
  }
</style>

<div class="blog-container">
  {% assign visible_posts = "" | split: "" %}
  {% for post in site.posts %}
    {% assign post_year = post.date | date: '%Y' | plus: 0 %}
    {% if post.show_in_list != false and post_year >= 2025 %}
      {% assign visible_posts = visible_posts | push: post %}
    {% endif %}
  {% endfor %}

  <!-- Filter Buttons -->
  <div class="blog-filter">
    <button class="filter-btn active" data-filter="all">All</button>
    {% assign all_tags = visible_posts | map: 'tags' | flatten | uniq | sort %}
    {% assign all_categories = visible_posts | map: 'categories' | flatten | uniq | sort %}
    {% for tag in all_tags %}
      {% if tag != '' %}
        <button class="filter-btn" data-filter="tag-{{ tag | slugify }}">{{ tag }}</button>
      {% endif %}
    {% endfor %}
    {% for category in all_categories %}
      {% if category != '' %}
        <button class="filter-btn" data-filter="category-{{ category | slugify }}">{{ category }}</button>
      {% endif %}
    {% endfor %}
  </div>

  <!-- Blog Posts -->
  <div class="blog-posts">
    {% assign posts_size = visible_posts | size %}
    {% if posts_size > 0 %}
      {% for post in visible_posts %}
        <div class="blog-post-card" 
             data-tags="{% for tag in post.tags %}tag-{{ tag | slugify }} {% endfor %}"
             data-categories="{% for category in post.categories %}category-{{ category | slugify }} {% endfor %}">
          <div class="blog-post-date">
            <i class="fa-solid fa-calendar fa-sm"></i> {{ post.date | date: '%B %d, %Y' }}
          </div>
          <div class="blog-post-title">
            {% if post.redirect == blank %}
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            {% elsif post.redirect contains '://' %}
              <a href="{{ post.redirect }}" target="_blank">{{ post.title }}</a>
              <svg width="1rem" height="1rem" viewBox="0 0 40 40" xmlns="http://www.w3.org/2000/svg" style="display: inline-block; margin-left: 0.5rem; vertical-align: middle;">
                <path
                  d="M17 13.5v6H5v-12h6m3-3h6v6m0-6-9 9"
                  class="icon_svg-stroke"
                  stroke="#999"
                  stroke-width="1.5"
                  fill="none"
                  fill-rule="evenodd"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                ></path>
              </svg>
            {% else %}
              <a href="{{ post.redirect | relative_url }}">{{ post.title }}</a>
            {% endif %}
          </div>
          {% if post.categories.size > 0 %}
            <div>
              {% for category in post.categories %}
                <span class="blog-post-category">{{ category }}</span>
              {% endfor %}
            </div>
          {% endif %}
          {% if post.tags.size > 0 %}
            <div class="blog-post-tags">
              {% for tag in post.tags %}
                <span class="blog-tag" data-filter="tag-{{ tag | slugify }}">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </div>
      {% endfor %}
    {% else %}
      <p>No posts so far...</p>
    {% endif %}
  </div>
</div>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    const filterButtons = document.querySelectorAll('.filter-btn');
    const postCards = document.querySelectorAll('.blog-post-card');
    const tagSpans = document.querySelectorAll('.blog-tag');
    
    // Filter button click handler
    filterButtons.forEach(button => {
      button.addEventListener('click', function() {
        // Update active state
        filterButtons.forEach(btn => btn.classList.remove('active'));
        this.classList.add('active');
        
        const filter = this.getAttribute('data-filter');
        
        // Filter posts
        postCards.forEach(card => {
          if (filter === 'all') {
            card.classList.remove('hidden');
          } else {
            const tags = card.getAttribute('data-tags') || '';
            const categories = card.getAttribute('data-categories') || '';
            if (tags.includes(filter) || categories.includes(filter)) {
              card.classList.remove('hidden');
            } else {
              card.classList.add('hidden');
            }
          }
        });
      });
    });
    
    // Tag click handler
    tagSpans.forEach(tag => {
      tag.addEventListener('click', function() {
        const filter = this.getAttribute('data-filter');
        const button = document.querySelector(`.filter-btn[data-filter="${filter}"]`);
        if (button) {
          button.click();
        }
      });
    });
  });
</script>

