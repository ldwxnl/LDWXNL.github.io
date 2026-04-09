---
layout: default  # 使用主题的默认布局
title: 我的博客   # 页面标题
---

# 我的博客文章
{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) ({{ post.date | date: "%Y-%m-%d" }})
{% endfor %}
