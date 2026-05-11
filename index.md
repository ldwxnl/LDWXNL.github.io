---
layout: default
title: 首页
---
<style>
  /* --- 基础设置：深色模式 --- */
  body {
    background: #0f0f14; /* 深邃的暗紫色背景 */
    color: #e0e0e0;
    font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
    margin: 0;
    padding: 0;
    min-height: 100vh;
  }

  /* --- 主容器：居中布局 --- */
  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 40px 20px;
  }

  /* --- 核心卡片样式：毛玻璃效果 (Glassmorphism) --- */
  .card {
    background: rgba(255, 255, 255, 0.05); /* 半透明白色背景 */
    border: 1px solid rgba(255, 255, 255, 0.1); /* 细微的边框 */
    border-radius: 16px; /* 大圆角 */
    backdrop-filter: blur(10px); /* 关键：毛玻璃模糊效果 */
    -webkit-backdrop-filter: blur(10px); /* 兼容 Safari */
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3); /* 深沉的阴影 */
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
    box-shadow: 0 0 20px rgba(102, 192, 244, 0.3); /* 头像发光效果 */
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
    background: linear-gradient(90deg, #6A11CB 0%, #2575FC 100%); /* 渐变背景 */
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
    border-left: 4px solid #66c0f4; /* 左侧高亮边框 */
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

  /* --- Cusdis 评论区适配 --- */
  #cusdis_thread {
    margin-top: 40px;
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

  <!-- 5. 留言板 (Cusdis) -->
  <div class="card" id="cusdis_thread">
    <h2 style="text-align: center; color: #fff; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 15px; margin-bottom: 20px;">💬 玩家留言板</h2>
    <p style="text-align: center; color: #aaa; margin-bottom: 20px;">
      欢迎大家在下方留言交流游戏心得、反馈问题或分享进服体验！
    
    <!-- 这里插入 Cusdis 代码 -->
    <script async src="https://cusdis.com/client.js"
      data-app-id="你的APP_ID"
      data-host="https://cusdis.com"
      data-page-id="{{ page.url }}"
      data-page-title="{{ page.title }}"
      data-theme="dark">
    </script>
  </div>

</div>

<script>
  // 简单的实时时间脚本
  function updateTime() {
    const now = new Date();
    const timeString = now.toLocaleTimeString('zh-CN', { hour12: false });
    document.getElementById('current-time').innerText = timeString;
  }
  setInterval(updateTime, 1000);
  updateTime();
</script>
