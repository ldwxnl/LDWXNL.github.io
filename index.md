---
layout: default
title: 首页
---

<!-- 引入字体图标（用于GitHub和邮箱图标） -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<!-- 1. 设置蓝粉渐变背景 -->
<style>
  body {
    margin: 0;
    padding: 0;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 50%, #f093fb 100%);
    background-attachment: fixed; /* 让背景固定，滚动时更顺滑 */
    min-height: 100vh;
    font-family: "Segoe UI", "Microsoft YaHei", sans-serif;
    color: #333;
  }

  /* 主内容容器：增加一点毛玻璃质感 */
  .page-container {
    max-width: 900px;
    margin: 0 auto;
    padding: 2rem;
  }

  /* 顶部背景区域：现在和body融为一体，或者你可以保留一个独立的header */
  .hero-section {
    text-align: center;
    padding: 4rem 1rem;
    color: white;
    margin-bottom: 2rem;
  }

  .hero-section h1 {
    font-size: 3rem;
    margin: 0;
    font-weight: 700;
    letter-spacing: 2px;
    text-shadow: 0 2px 10px rgba(0,0,0,0.2);
  }

  .hero-section p {
    font-size: 1.2rem;
    opacity: 0.9;
    margin-top: 0.5rem;
  }

  /* 卡片通用样式：增强立体感 */
  .card {
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    padding: 2.5rem;
    margin-bottom: 2rem;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 50px rgba(0, 0, 0, 0.15);
  }

  /* 头像：强制居中 + 精致边框 */
  .avatar {
    display: block;
    margin: 0 auto 1.5rem; /* 上下间距，左右自动居中 */
    width: 140px;
    height: 140px;
    border-radius: 50%;
    object-fit: cover;
    border: 5px solid rgba(255, 255, 255, 0.8);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s;
  }

  .avatar:hover {
    transform: scale(1.05);
  }

  /* 个人介绍文字居中 */
  .profile-text {
    text-align: center;
  }

  .profile-text h3 {
    margin-top: 0;
    color: #2c3e50;
    font-size: 1.8rem;
    font-weight: 600;
  }

  .profile-text p {
    line-height: 1.8;
    color: #555;
    margin-bottom: 0.5rem;
    font-size: 1.05rem;
  }

  .contact-info {
    margin-top: 1.5rem;
    color: #666;
    font-size: 0.95rem;
  }

  .contact-info a {
    color: #667eea;
    text-decoration: none;
    font-weight: 600;
    margin: 0 0.5rem;
  }

  .contact-info a:hover {
    text-decoration: underline;
    color: #764ba2;
  }

  /* 按钮区域 */
  .actions-section {
    text-align: center;
    margin: 3rem 0;
  }

  .actions-section h4 {
    color: white; /* 按钮区的标题用白色，因为在渐变背景上 */
    margin-bottom: 1.5rem;
    font-size: 1.3rem;
    text-shadow: 0 1px 3px rgba(0,0,0,0.2);
  }

  .button-group {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
  }

  .btn {
    padding: 1rem 2.5rem;
    color: #333;
    text-decoration: none;
    border: 2px solid #333;
    border-radius: 50px; /* 更圆润的按钮 */
    font-weight: 600;
    background: rgba(255, 255, 255, 0.9);
    transition: all 0.3s ease;
    text-align: center;
    min-width: 180px;
    display: inline-block;
    box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  }

  .btn:hover {
    background: #333;
    color: white;
    transform: translateY(-3px);
    box-shadow: 0 8px 25px rgba(0,0,0,0.2);
  }

  /* 留言板样式微调 */
  .giscus-box {
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    padding: 2rem;
    margin-top: 2rem;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.1);
  }

  .giscus-box h2 {
    margin-top: 0;
    color: #2c3e50;
    font-size: 1.8rem;
    text-align: center;
  }

  .giscus-box p {
    color: #666;
    line-height: 1.6;
    margin-bottom: 1.5rem;
    text-align: center;
  }

  .tip-box {
    background: #e8f4f8;
    border-left: 4px solid #3498db;
    padding: 1rem 1.5rem;
    margin-bottom: 2rem;
    border-radius: 0 10px 10px 0;
  }

  .tip-box p {
    margin: 0;
    color: #555;
    font-size: 0.95rem;
    text-align: left;
  }

  /* 响应式调整 */
  @media (max-width: 768px) {
    .button-group {
      flex-direction: column;
      align-items: center;
    }
    .btn {
      width: 80%;
    }
  }
</style>

<!-- 页面结构 -->

  <!-- 顶部 Hero 区域：蓝粉渐变 -->
  <div class="hero-section">
    <h1>首页</h1>
    我的个人网站和博客
  </div>

  <!-- 主内容区 -->
  <div class="page-container">

    <!-- 头像和自我介绍卡片 -->
    <div class="card">
      <img src="/assets/images/avatar.jpg" alt="我的头像" class="avatar">
      <div class="profile-text">
        <h3>关于我</h3>
        <p style="font-size: 1.1rem; max-width: 600px; margin: 0 auto 1rem;">
          你好！我是 LDWXNL，热爱技术、分享与交流。这个网站是我记录学习、项目和生活的空间。你问我是谁，别问，问就是ldwxnl
        
        <p class="contact-info">
          <i class="fas fa-envelope"></i> 联系我: to@hrn.cc.cd | 
          <a href="https://github.com/ldwxnl" target="_blank"><i class="fab fa-github"></i> GitHub</a>
        
      </div>
    </div>

    <!-- 网站核心功能按钮区域 -->
    <div class="actions-section">
      <h4>🎯 探索更多</h4>
      <div class="button-group">
        <a href="/posts" class="btn">📖 查看我的博客</a>
        <a href="/games" class="btn">🎮 游戏中心</a>
      </div>
    </div>

    <hr style="margin: 3rem 0; border: none; border-top: 2px solid rgba(255,255,255,0.3);">

    <!-- 留言板区域 -->
    <div class="giscus-box">
      <h2>💬 玩家留言板</h2>
      <p style="color: #666;">
        欢迎大家在下方留言交流游戏心得、反馈问题或分享进服体验！
      
      <div class="tip-box">
        <p style="margin: 0; color: #555; font-size: 0.95rem;">
          <strong>📌 提示：</strong> 评论需要 GitHub 账号，数据会保存在仓库的 Discussions 中。
          闲聊、反馈、求带都可以，但请注意网络礼仪。
        
      </div>
      
      <!-- Giscus 评论区 -->
      <div class="giscus"></div>
    </div>

  </div>

  <!-- Giscus 脚本 -->
  <script src="https://giscus.app/client.js"
          data-repo="LDWXNL/LDWXNL.github.io"
          data-repo-id="R_kgDOR96W3Q"
          data-category="Announcements"
          data-category-id="DIC_kwDOR96W3c4C8t89"
          data-mapping="pathname"
          data-strict="0"
          data-reactions-enabled="1"
          data-emit-metadata="0"
          data-input-position="top"
          data-theme="preferred_color_scheme"
          data-lang="zh-CN"
          crossorigin="anonymous"
          async>
  </script>

  <!-- 优化 Giscus 样式 -->
  <style>
    .giscus, .giscus-frame {
      width: 100%;
      border: none;
      min-height: 300px;
      background: transparent;
    }
    .giscus .giscus-header,
    .giscus .giscus-footer {
      display: none;
    }
  </style>
