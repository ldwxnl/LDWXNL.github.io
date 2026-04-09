---
layout: default
title: 首页
---
<div style="display: flex; align-items: center; gap: 2rem; background: #f9f9f9; padding: 2rem; border-radius: 12px; margin: 2rem 0;">
  <!-- 头像 -->
  <img src="/assets/images/avatar.jpg" 
       alt="我的头像" 
       style="width: 120px; height: 120px; border-radius: 50%; object-fit: cover; border: 4px solid white; box-shadow: 0 4px 12px rgba(0,0,0,0.1);">
  
  <!-- 文字 -->
  <div>
    <h3 style="margin-top: 0; color: #333;">关于我</h3>
    <p style="line-height: 1.8; color: #555; margin-bottom: 0.5rem;">
      你好！我是 LDWXNL，热爱技术、分享与交流。这个网站是我记录学习、项目和生活的空间。你问我是谁，别问，问就是ldwxnl
    </p>
    <p style="color: #888; font-size: 0.9rem;">
      📧 联系我: qwrrdfrrfgr@qq.com | 🔗 <a href="https://github.com/ldwxnl" style="color: #0366d6;">GitHub</a>

<!-- 按钮容器 - 用 flex 布局保证完美居中 -->
<div style="
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  margin: 3rem 0;
  flex-wrap: wrap;
">

  <!-- 博客按钮 -->
  <a href="/posts" style="
    padding: 1rem 2.5rem;
    color: #222;
    text-decoration: none;
    border: 2px solid #222;
    border-radius: 8px;
    font-weight: 600;
    background: transparent;
    transition: all 0.3s;
    text-align: center;
    min-width: 180px;
  ">查看我的博客</a>

  <!-- 游戏中心按钮 -->
  <a href="/games" style="
    padding: 1rem 2.5rem;
    color: #222;
    text-decoration: none;
    border: 2px solid #222;
    border-radius: 8px;
    font-weight: 600;
    background: transparent;
    transition: all 0.3s;
    text-align: center;
    min-width: 180px;
  ">🎮 游戏中心</a>
<a href="/tanchishe.html">游戏中心</a>
</div>

<!-- 悬停效果（必须放在这个位置） -->
<style>
  a:hover {
    background: #222;
    color: white;
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(0,0,0,0.1);
  }
  
  /* 手机端优化 */
  @media (max-width: 768px) {
    div[style*="display: flex"] {
      flex-direction: column;
      gap: 1.5rem;
    }
    a[style*="min-width"] {
      width: 90%;
      max-width: 300px;
    }
  }
</style>
