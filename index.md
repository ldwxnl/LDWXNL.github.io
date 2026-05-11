---
layout: default
title: 首页
---
<style>
  /* --- 基础设置：深色模式 --- */
  body {
    background: #0f0f14;
    color: #e0e0e0;
    font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
    margin: 0;
    padding: 0;
    min-height: 100vh;
  }

  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 40px 20px;
  }

  /* --- 核心卡片样式：毛玻璃效果 --- */
  .card {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
    padding: 25px;
    margin-bottom: 25px;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.4);
  }

  /* --- 头部区域：头像与简介 --- */
  .header {
    display: flex;
    align-items: center;
    gap: 25px;
    margin-bottom: 30px;
  }

  .avatar {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: 3px solid rgba(255, 255, 255, 0.2);
    object-fit: cover;
    box-shadow: 0 0 20px rgba(102, 192, 244, 0.3);
  }

  .intro h1 {
    margin: 0 0 10px 0;
    font-size: 28px;
    color: #ffffff;
    font-weight: 600;
  }

  .intro p {
    margin: 0;
    color: #b0b0b0;
    font-size: 15px;
    max-width: 500px;
    line-height: 1.6;
  }

  /* --- 按钮组：科技感按钮 --- */
  .button-group {
    display: flex;
    gap: 20px;
    margin-bottom: 30px;
    flex-wrap: wrap;
  }

  .btn {
    flex: 1;
    min-width: 200px;
    padding: 14px 20px;
    background: linear-gradient(90deg, #6A11CB 0%, #2575FC 100%);
    border: none;
    border-radius: 8px;
    color: white;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    transition: all 0.3s;
    box-shadow: 0 4px 15px rgba(37, 117, 252, 0.3);
  }

  .btn:hover {
    opacity: 0.9;
    transform: scale(1.02);
  }

  /* --- 音乐条模拟区域 --- */
  .music-bar {
    display: flex;
    align-items: center;
    gap: 15px;
    background: rgba(0, 0, 0, 0.2);
    padding: 10px 20px;
    border-radius: 50px;
    margin-bottom: 30px;
  }
  
  .music-cover {
    width: 50px; height: 50px; border-radius: 8px; background: #333; }
  
  .music-info { flex: 1; }
  .music-title { font-weight: bold; margin: 0; color: #fff; }
  .music-artist { margin: 0; font-size: 12px; color: #aaa; }

  /* --- 网格布局：中间内容区 --- */
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
  }

  .grid-item {
    background: rgba(0, 0, 0, 0.2);
    border-radius: 12px;
    padding: 20px;
    border-left: 4px solid #66c0f4;
  }

  .grid-item h3 { margin-top: 0; color: #66c0f4; }
  .grid-item p { font-size: 14px; color: #ccc; margin-bottom: 0; }

  /* --- 底部时间轴 --- */
  .footer-time {
    text-align: center;
    font-size: 18px;
    color: #fff;
    background: rgba(255, 255, 255, 0.05);
    padding: 15px;
    border-radius: 8px;
    font-family: 'Consolas', monospace;
    letter-spacing: 1px;
  }

  /* --- Giscus 评论区样式 --- */
  .giscus-section {
    margin-top: 40px;
  }
  
  .giscus-title {
    text-align: center;
    color: #fff;
    border-bottom: 1px solid rgba(255,255,255,0.1);
    padding-bottom: 15px;
    margin-bottom: 20px;
    font-size: 1.8rem;
  }
  
  .giscus-info {
    background: rgba(102, 192, 244, 0.1);
    border-left: 4px solid #66c0f4;
    padding: 1rem 1.5rem;
    margin-bottom: 2rem;
    border-radius: 0 6px 6px 0;
  }
  
  .giscus-info p {
    margin: 0;
    color: #b0d7f5;
    font-size: 0.95rem;
  }
</style>

<div class="container">

  <!-- 1. 顶部个人信息卡片 -->
  <div class="card">
    <div class="header">
      <img src="/assets/images/avatar.jpg" alt="头像" class="avatar">
      <div class="intro">
        <h1>LDWXNL</h1>
        热爱技术、分享与交流。这个网站是我记录学习、项目和生活的空间。你问我是谁，别问，问就是ldwxnl。
      </div>
    </div>

    <div class="button-group">
      <a href="/posts" class="btn">📖 查看我的博客</a>
      <a href="/games" class="btn">🎮 游戏中心</a>
    </div>
  </div>

  <!-- 2. 模拟音乐播放器条 (装饰性) -->
  <div class="card music-bar">
    <div class="music-cover"></div>
    <div class="music-info">
      <p class="music-title">Neural Network
      <p class="music-artist">XingHuiSama
    </div>
    <div style="color: #aaa;">▶️ 正在播放...</div>
  </div>

  <!-- 3. 中间网格内容 -->
  <div class="grid">
    <div class="grid-item card">
      <h3>💻 最新动态</h3>
      刚刚更新了个人主页的美化方案，引入了毛玻璃效果和暗色主题，看起来更酷了！
    </div>
    <div class="grid-item card">
      <h3>⭐ 推荐项目</h3>
      正在研究如何接入 Cusdis 评论系统，虽然中间遇到了点小麻烦，但最终搞定了。
    </div>
    <div class="grid-item card">
      <h3>📚 学习笔记</h3>
      最近在学习 Docker 部署，感觉比传统的虚拟主机方便很多，特别是配合 GitHub Actions。
    </div>
  </div>

  <!-- 4. 底部时间 -->
  <div class="card footer-time">
    <span id="current-time">15:32:34</span>
  </div>

  <!-- 5. Giscus 留言板 -->
  <div class="card giscus-section">
    <h2 class="giscus-title">💬 玩家留言板</h2>
    
    <div class="giscus-info">
      <p><strong>📌 提示：</strong> 评论需要 GitHub 账号，数据会保存在仓库的 Discussions 中。闲聊、反馈、求带都可以，但请注意网络礼仪。</p>
    </div>
    
    <!-- Giscus 评论区容器 -->
    <div class="giscus"></div>
  </div>

</div>

<!-- 实时时间脚本 -->
<script>
  function updateTime() {
    const now = new Date();
    const timeString = now.toLocaleTimeString('zh-CN', { hour12: false });
    document.getElementById('current-time').innerText = timeString;
  }
  setInterval(updateTime, 1000);
  updateTime();
</script>

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
        data-input-position="bottom"
        data-theme="dark"
        data-lang="zh-CN"
        crossorigin="anonymous"
        async>
</script>

<!-- Giscus 样式优化 -->
<style>
  .giscus, .giscus-frame {
    width: 100%;
    border: none;
  }
  .giscus-frame {
    border-radius: 8px;
  }
</style>
