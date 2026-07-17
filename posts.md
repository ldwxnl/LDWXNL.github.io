---
layout: default
title: 我的博客
---

<!-- 内联样式，建议后续移到 assets/css/blog.css -->
<style>
  /* ===== 全局重置 ===== */
  .blog-container {
    max-width: 960px;
    margin: 0 auto;
    padding: 2rem 1.5rem;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  }

  .blog-header {
    margin-bottom: 3rem;
    text-align: center;
  }
  .blog-header h1 {
    font-size: 2.8rem;
    font-weight: 700;
    letter-spacing: -1px;
    color: #1a1a2e;
    margin-bottom: 0.3rem;
  }
  .blog-header p {
    font-size: 1.1rem;
    color: #6c757d;
    border-top: 2px solid #e9ecef;
    padding-top: 0.8rem;
    display: inline-block;
  }

  /* ===== 文章列表（卡片网格） ===== */
  .post-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.8rem;
  }

  .post-card {
    background: #ffffff;
    border-radius: 16px;
    box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
    padding: 1.5rem 1.2rem;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    border: 1px solid #f1f3f5;
    display: flex;
    flex-direction: column;
  }
  .post-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 32px rgba(0, 0, 0, 0.08);
  }

  .post-card .post-title {
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.4;
    margin: 0 0 0.3rem 0;
  }
  .post-card .post-title a {
    color: #1a1a2e;
    text-decoration: none;
    transition: color 0.15s;
  }
  .post-card .post-title a:hover {
    color: #4c6ef5;
  }

  .post-card .post-meta {
    font-size: 0.85rem;
    color: #868e96;
    display: flex;
    align-items: center;
    gap: 0.6rem;
    flex-wrap: wrap;
    margin-top: 0.2rem;
  }
  .post-card .post-meta .date {
    background: #f1f3f5;
    padding: 0.1rem 0.7rem;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: 500;
  }
  .post-card .post-meta .category {
    background: #e7edff;
    color: #4c6ef5;
    padding: 0.1rem 0.7rem;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: 500;
  }

  .post-card .post-excerpt {
    font-size: 0.95rem;
    color: #495057;
    line-height: 1.6;
    margin: 0.6rem 0 0.8rem 0;
    flex: 1;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  .post-card .read-more {
    font-size: 0.9rem;
    font-weight: 500;
    color: #4c6ef5;
    text-decoration: none;
    align-self: flex-start;
    border-bottom: 2px solid transparent;
    transition: border-color 0.2s;
  }
  .post-card .read-more:hover {
    border-bottom-color: #4c6ef5;
  }

  /* ===== 空状态 ===== */
  .no-posts {
    text-align: center;
    padding: 4rem 0;
    color: #868e96;
    font-size: 1.1rem;
  }

  /* ===== 响应式 ===== */
  @media (max-width: 640px) {
    .blog-header h1 {
      font-size: 2rem;
    }
    .post-grid {
      grid-template-columns: 1fr;
      gap: 1.2rem;
    }
    .post-card {
      padding: 1rem;
    }
  }
</style>

<div class="blog-container">

  <!-- 页眉 -->
  <header class="blog-header">
    <h1>📝 我的博客</h1>
    <p>记录技术、思考与生活</p>
  </header>

  <!-- 文章列表 -->
  {% if site.posts.size > 0 %}
    <div class="post-grid">
      {% for post in site.posts %}
        <article class="post-card">
          <h2 class="post-title">
            <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          </h2>

          <div class="post-meta">
            <span class="date">{{ post.date | date: "%Y年%m月%d日" }}</span>
            {% if post.categories %}
              <span class="category">{{ post.categories | first }}</span>
            {% endif %}
            {% if post.tags %}
              <span style="font-size:0.75rem;color:#adb5bd;">#{{ post.tags | first }}</span>
            {% endif %}
          </div>

          {% if post.excerpt %}
            <div class="post-excerpt">
              {{ post.excerpt | strip_html | truncatewords: 20 }}
            </div>
          {% endif %}

          <a href="{{ post.url | relative_url }}" class="read-more">阅读全文 →</a>
        </article>
      {% endfor %}
    </div>
  {% else %}
    <div class="no-posts">
      <p>还没有文章，请耐心等待 🚀</p>
    </div>
  {% endif %}

</div>
