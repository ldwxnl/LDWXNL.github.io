---
layout: default
title: 首页
---
<style>
  /* Steam 风格全局样式 */
  :root {
    --steam-bg: #1b2838;
    --steam-card: #2a475e;
    --steam-accent: #66c0f4;
    --steam-text: #c7d5e0;
    --steam-border: #3d5a80;
  }
  
  body {
    background: linear-gradient(135deg, #0c141c 0%, var(--steam-bg) 50%, #0f1b2b 100%);
    color: var(--steam-text);
    font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
    line-height: 1.6;
    min-height: 100vh;
    padding: 1rem;
  }
  
  .steam-container {
    max-width: 1200px;
    margin: 0 auto;
  }
  
  /* 毛玻璃卡片 */
  .steam-card {
    background: rgba(42, 71, 94, 0.85);
    backdrop-filter: blur(10px);
    border-radius: 12px;
    border: 1px solid var(--steam-border);
    padding: 2rem;
    margin-bottom: 2rem;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s, box-shadow 0.3s;
  }
  
  .steam-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.4);
  }
  
  /* 头像区域 */
  .profile-header {
    display: flex;
    align-items: center;
    gap: 2rem;
    flex-wrap: wrap;
  }
  
  .profile-avatar {
    width: 140px;
    height: 140px;
    border-radius: 50%;
    border: 4px solid var(--steam-accent);
    object-fit: cover;
    box-shadow: 0 0 20px rgba(102, 192, 244, 0.3);
  }
  
  .profile-info h1 {
    color: white;
    font-size: 2.5rem;
    margin: 0 0 0.5rem 0;
    font-weight: 300;
  }
  
  .profile-info .subtitle {
    color: var(--steam-accent);
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }
  
  .contact-links {
    display: flex;
    gap: 1.5rem;
    margin-top: 1rem;
  }
  
  .contact-link {
    color: var(--steam-text);
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem 1rem;
    background: rgba(29, 45, 60, 0.7);
    border-radius: 6px;
    transition: all 0.3s;
  }
  
  .contact-link:hover {
    background: var(--steam-accent);
    color: white;
  }
  
  /* 功能按钮 */
  .action-buttons {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
    margin-top: 2rem;
  }
  
  .action-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
    padding: 1.5rem;
    background: linear-gradient(135deg, rgba(29, 45, 60, 0.9) 0%, rgba(42, 71, 94, 0.9) 100%);
    border: 2px solid var(--steam-border);
    border-radius: 10px;
    color: white;
    text-decoration: none;
    font-size: 1.2rem;
    font-weight: 500;
    transition: all 0.3s;
  }
  
  .action-btn:hover {
    background: linear-gradient(135deg, var(--steam-accent) 0%, #4a9bda 100%);
    border-color: var(--steam-accent);
    transform: translateY(-3px);
  }
  
  .action-btn-icon {
    font-size: 1.8rem;
  }
  
  /* 留言板 */
  .comments-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1.5rem;
  }
  
  .comments-header h2 {
    color: white;
    font-size: 1.8rem;
    margin: 0;
  }
  
  .comments-info {
    background: rgba(102, 192, 244, 0.1);
    border-left: 4px solid var(--steam-accent);
    padding: 1rem;
    border-radius: 0 6px 6px 0;
    margin-bottom: 1.5rem;
  }
  
  /* 响应式 */
  @media (max-width: 768px) {
    .profile-header {
      flex-direction: column;
      text-align: center;
    }
    
    .contact-links {
      justify-content: center;
    }
    
    .action-buttons {
      grid-template-columns: 1fr;
    }
  }
</style>

<div class="steam-container">
  <!-- 头像和介绍卡片 -->
  <div class="steam-card">
    <div class="profile-header">
      <img src="/assets/images/avatar.jpg" alt="我的头像" class="profile-avatar">
      <div class="profile-info">
        <h1>LDWXNL</h1>
        <div class="subtitle">玩家 • 开发者 • 探索者</div>
        <p style="max-width: 600px; margin: 1rem 0; opacity: 0.9;">
          你好！我是 LDWXNL，热爱技术、游戏与分享。这是我的数字角落，记录学习、项目和奇思妙想。你问我是谁？问就是打游戏的。
        </p>
        <div class="contact-links">
          <a href="mailto:qwrrdfrrfgr@qq.com" class="contact-link">
            <span>📧</span> 联系我
          </a>
          <a href="https://github.com/ldwxnl" target="_blank" class="contact-link">
            <span>🔗</span> GitHub
          </a>
        </div>
      </div>
    </div>
  </div>
  
  <!-- 功能按钮卡片 -->
  <div class="steam-card">
    <h2 style="color: white; margin-top: 0; font-size: 1.8rem; margin-bottom: 1.5rem;">🚀 核心功能</h2>
    <div class="action-buttons">
      <a href="/posts" class="action-btn">
        <span class="action-btn-icon">📖</span>
        <span>技术博客</span>
      </a>
      <a href="/games" class="action-btn">
        <span class="action-btn-icon">🎮</span>
        <span>游戏中心</span>
      </a>
    </div>
  </div>
  
  <!-- 留言板卡片 -->
  <div class="steam-card">
    <div class="comments-header">
      <h2>💬 玩家留言板</h2>
    </div>
    
    <div class="comments-info">
      <p style="margin: 0; color: var(--steam-text);">
        <strong>欢迎交流！</strong> 在这里分享游戏心得、反馈问题或单纯聊聊天。支持匿名评论，无需登录。
      </p>
    </div>
    
    <!-- Cusdis 评论区 -->
    <div id="cusdis_thread"
         data-host="https://cusdis.com"
         data-app-id="你的 APP ID" <!-- 记得替换！ -->
         data-page-id="{{ page.url }}"
         data-page-url="{{ page.url | absolute_url }}"
         data-page-title="{{ page.title }}"
         data-theme="dark"  <!-- 深色主题匹配 Steam 风格 -->
         style="min-height: 300px; border-radius: 8px; overflow: hidden;">
    </div>
  </div>
</div>

<!-- 引入 Cusdis JS -->
<script defer src="https://cusdis.com/js/cusdis.es.js"></script>
