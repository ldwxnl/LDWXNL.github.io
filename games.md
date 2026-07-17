---
layout: default
title: 🎮 游戏中心
permalink: /games/
---

<!-- 内联样式，建议后续移至 assets/css/games.css -->
<style>
  /* ===== 全局容器 ===== */
  .games-container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 2rem 1.5rem;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  }

  .games-header {
    text-align: center;
    margin-bottom: 3rem;
  }
  .games-header h1 {
    font-size: 2.8rem;
    font-weight: 700;
    color: #1a1a2e;
    letter-spacing: -0.5px;
    margin-bottom: 0.3rem;
  }
  .games-header p {
    font-size: 1.1rem;
    color: #6c757d;
    border-top: 2px solid #e9ecef;
    padding-top: 0.8rem;
    display: inline-block;
  }

  /* ===== 游戏卡片网格 ===== */
  .game-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 1.8rem;
    margin-bottom: 3rem;
  }

  .game-card {
    background: #ffffff;
    border-radius: 16px;
    box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
    padding: 1.5rem 1.2rem;
    border: 1px solid #f1f3f5;
    transition: transform 0.25s ease, box-shadow 0.25s ease;
    display: flex;
    flex-direction: column;
  }
  .game-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 32px rgba(0, 0, 0, 0.08);
  }

  .game-card .game-icon {
    font-size: 2.8rem;
    margin-bottom: 0.2rem;
  }
  .game-card .game-title {
    font-size: 1.3rem;
    font-weight: 600;
    margin: 0 0 0.2rem 0;
  }
  .game-card .game-title a {
    color: #1a1a2e;
    text-decoration: none;
    transition: color 0.15s;
  }
  .game-card .game-title a:hover {
    color: #4c6ef5;
  }

  .game-card .game-desc {
    font-size: 0.95rem;
    color: #495057;
    line-height: 1.6;
    margin: 0.4rem 0 1rem 0;
    flex: 1;
  }
  .game-card .game-tag {
    font-size: 0.75rem;
    background: #e7edff;
    color: #4c6ef5;
    padding: 0.1rem 0.7rem;
    border-radius: 20px;
    display: inline-block;
    align-self: flex-start;
    font-weight: 500;
  }

  /* ===== 服务器信息卡片（重点突出） ===== */
  .server-card {
    background: linear-gradient(135deg, #1a1a2e 0%, #2d2d44 100%);
    border-radius: 20px;
    padding: 2rem 2rem;
    margin: 2rem 0 2.5rem 0;
    color: #e9ecef;
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
    border: 1px solid rgba(255, 255, 255, 0.06);
  }
  .server-card .server-title {
    font-size: 1.8rem;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 0.8rem;
    margin-bottom: 0.8rem;
  }
  .server-card .server-title .status-badge {
    background: #22c55e;
    padding: 0.2rem 0.8rem;
    border-radius: 30px;
    font-size: 0.8rem;
    font-weight: 600;
    color: #fff;
    letter-spacing: 0.3px;
  }
  .server-card .server-detail {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 0.8rem 1.5rem;
    margin-top: 0.5rem;
  }
  .server-card .server-detail .item {
    display: flex;
    flex-direction: column;
  }
  .server-card .server-detail .item .label {
    font-size: 0.75rem;
    text-transform: uppercase;
    opacity: 0.6;
    letter-spacing: 0.5px;
  }
  .server-card .server-detail .item .value {
    font-size: 1rem;
    font-weight: 500;
    color: #f8f9fa;
    word-break: break-all;
  }
  .server-card .server-detail .item .value a {
    color: #748ffc;
    text-decoration: none;
  }
  .server-card .server-detail .item .value a:hover {
    text-decoration: underline;
  }
  .server-card .server-note {
    margin-top: 1rem;
    font-size: 0.92rem;
    border-top: 1px solid rgba(255, 255, 255, 0.08);
    padding-top: 1rem;
    opacity: 0.8;
  }

  /* ===== 版权声明 ===== */
  .copyright {
    margin-top: 3rem;
    padding-top: 1.5rem;
    border-top: 2px solid #e9ecef;
    font-size: 0.9rem;
    color: #868e96;
    line-height: 1.8;
  }
  .copyright a {
    color: #4c6ef5;
    text-decoration: none;
  }
  .copyright a:hover {
    text-decoration: underline;
  }

  /* ===== 响应式 ===== */
  @media (max-width: 640px) {
    .games-header h1 {
      font-size: 2rem;
    }
    .game-grid {
      grid-template-columns: 1fr;
      gap: 1.2rem;
    }
    .server-card {
      padding: 1.2rem 1.2rem;
    }
    .server-card .server-title {
      font-size: 1.4rem;
      flex-wrap: wrap;
    }
    .server-card .server-detail {
      grid-template-columns: 1fr;
      gap: 0.4rem;
    }
  }
</style>

<div class="games-container">

  <!-- 页眉 -->
  <header class="games-header">
    <h1>🎮 游戏中心</h1>
    <p>一些经典的网页小游戏，点击卡片跳转体验</p>
  </header>

  <!-- 游戏卡片网格 -->
  <div class="game-grid">

    <!-- 1. 2048 -->
    <div class="game-card">
      <div class="game-icon">🧩</div>
      <h2 class="game-title"><a href="https://play2048.co/" target="_blank">经典 2048</a></h2>
      <p class="game-desc">合并数字，挑战 2048！经典的益智游戏，适合消磨时间。</p>
      <span class="game-tag">益智</span>
    </div>

    <!-- 2. 贪吃蛇（自制） -->
    <div class="game-card">
      <div class="game-icon">🐍</div>
      <h2 class="game-title"><a href="snake/" target="_blank">贪吃蛇（自制）</a></h2>
      <p class="game-desc">经典贪吃蛇游戏，用方向键控制蛇的移动，看看你能吃多长。</p>
      <span class="game-tag">街机</span>
    </div>

    <!-- 3. Minecraft 网页版 -->
    <div class="game-card">
      <div class="game-icon">⛏️</div>
      <h2 class="game-title"><a href="https://www.mcjs.cc/" target="_blank">Minecraft 网页版</a></h2>
      <p class="game-desc">在浏览器中体验我的世界风格，无需安装客户端。</p>
      <span class="game-tag">沙盒</span>
    </div>

    <!-- 4. 更多推荐（组合两个小游戏） -->
    <div class="game-card">
      <div class="game-icon">🎯</div>
      <h2 class="game-title">更多推荐</h2>
      <p class="game-desc">
        <a href="https://flappybird.io/" target="_blank">🐦 飞翔的鸟</a><br>
        <a href="chrome://dino" target="_blank">🦕 Chrome 小恐龙</a>（需离线时访问）
      </p>
      <span class="game-tag">休闲</span>
    </div>

  </div>

  <!-- ===== 服务器信息卡片 ===== -->
  <div class="server-card">
    <div class="server-title">
      🌐 我的 Minecraft 服务器
      <span class="status-badge">🟢 在线</span>
    </div>

    <div class="server-detail">
      <div class="item">
        <span class="label">连接地址</span>
        <span class="value">
          网页版：<a href="http://hrsi.cc.cd" target="_blank">hrsi.cc.cd</a><br>
          Java版：<code>java.hrsi.cc.cd</code><br>
          基岩版：<code>jy.hrsi.cc.cd</code> 端口 <code>11188</code>
        </span>
      </div>
      <div class="item">
        <span class="label">版本 & 模式</span>
        <span class="value">1.8.8 (Java) · 生存模式</span>
        <span style="font-size:0.85rem;opacity:0.7;">网页与 Java 端口：25565</span>
      </div>
      <div class="item">
        <span class="label">互通性</span>
        <span class="value">Java版、网页版、基岩版互通</span>
        <span style="font-size:0.85rem;opacity:0.7;">基岩版适配可能不佳，请见谅</span>
      </div>
    </div>

    <div class="server-note">
      📜 纯属同好交流，非商业服 · 随电脑开机运行
    </div>
  </div>

  <!-- ===== 版权声明 ===== -->
  <div class="copyright">
    <strong>版权声明：</strong><br>
    本页面所列游戏均为个人兴趣推荐，著作权归各原作者所有。<br>
    游戏名称与商标属于其各自所有者，此处仅作介绍。<br>
    若涉及任何版权问题，请联系我进行修改。📧 <a href="mailto:to@hrsi.cc.cd">to@hrsi.cc.cd</a>
  </div>

</div>
