---
layout:     post
title:      PowerDesigner物理模型设置约束条件(主码、外码、check约束、非空约束、默认值)（转载）
subtitle:   
date:       2020-05-01
author:     Mehaei
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - python
---
主键：<br>
双击实体进入，属性界面点击keys选项卡，选中主键，右击点击properties（属性）<br>
<img src="https://img-blog.csdnimg.cn/20200501193209888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

红圈内自定义主键名称<br>
<img src="https://img-blog.csdnimg.cn/20200501193221602.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

2．外码<br>
双击reference，选择integrity（完整性）选项卡，自定义外键名称<br>
<img src="https://img-blog.csdnimg.cn/20200501193232115.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

3.CHECK约束<br>
方法一（列约束）：双击实体进入，属性界面点击column选项卡，选中要添加约束的字段名，右击点击properties（属性）

<img src="https://img-blog.csdnimg.cn/20200501193254238.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

点击additional checks，自定义约束名同时编写约束代码

<img src="https://img-blog.csdnimg.cn/202005011933047.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

方法二（表约束）：双击实体进入，属性界面点击rules选项卡，点击create an object 选项，选中新建的object，右击点击属性<br>
<img src="https://img-blog.csdnimg.cn/20200501193311377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

在常规选项卡中自定义约束名称，并把type改为constraint

<img src="https://img-blog.csdnimg.cn/2020050119331799.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

然后选择expression选项卡，编写约束代码。

<img src="https://img-blog.csdnimg.cn/20200501193323290.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

4.非空约束：<br>
双击实体进入，属性界面点击column选项卡，选中要添加约束的字段名，右击点击properties（属性）点击勾选mandatory即可

<img src="https://img-blog.csdnimg.cn/20200501193331400.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

5.默认值约束：<br>
双击实体进入，属性界面点击column选项卡，选中要添加约束的字段名，右击点击properties（属性），点击基本检查选项卡，设置默认值。<br>
<img src="https://img-blog.csdnimg.cn/20200501193338770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNjYxNTU4,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
