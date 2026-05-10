---
layout: default
title: 首页
---
<!-- 统一的灰色背景容器，包裹整个主内容区域 -->
<div style="background: #f9f9f9; padding: 3rem 2rem; border-radius: 12px; margin: 2rem 0;">

  <!-- 头像和自我介绍区域 -->
  <div style="display: flex; align-items: center; gap: 2rem; margin-bottom: 3rem; flex-wrap: wrap;">
    <!-- 头像 -->
    <img src="/assets/images/avatar.jpg"
         alt="我的头像"
         style="width: 120px; height: 120px; border-radius: 50%; object-fit: cover; border: 4px solid white; box-shadow: 0 4px 12px rgba(0,0,0,0.1);">
    <!-- 文字 -->
    <div style="flex: 1; min-width: 250px;">
      <h3 style="margin-top: 0; color: #333; font-size: 1.8rem;">关于我</h3>
      <p style="line-height: 1.8; color: #555; margin-bottom: 0.8rem;">
        你好！我是 LDWXNL，热爱技术、分享与交流。这个网站是我记录学习、项目和生活的空间。你问我是谁，别问，问就是ldwxnl
      </p>
      <p style="color: #888; font-size: 0.95rem;">
        📧 联系我: qwrrdfrrfgr@qq.com | 🔗
        <a href="https://github.com/ldwxnl" style="color: #0366d6; text-decoration: none; border-bottom: 1px dashed #0366d6;">GitHub</a>
      </p>
    </div>
  </div>

  <!-- 网站核心功能按钮区域 -->
  <div style="text-align: center;">
    <h4 style="color: #666; margin-bottom: 1.5rem;">🎯 探索更多</h4>
    <div style="display: flex; justify-content: center; align-items: center; gap: 2rem; flex-wrap: wrap;">
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
      ">📖 查看我的博客</a>

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
    </div>
  </div>

</div>

<!-- 独立的留言板说明区域 -->
<div style="
  max-width: 800px;
  margin: 3rem auto;
  padding: 2.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 16px;
  color: white;
  text-align: center;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
">

  <h2 style="margin-top: 0; color: white; font-size: 2rem; margin-bottom: 1rem;">💬 玩家留言板</h2>

  <p style="font-size: 1.1rem; line-height: 1.7; margin-bottom: 1.5rem; opacity: 0.95;">
    欢迎在此交流游戏心得、反馈问题或分享进服体验！<br>
    <strong>请注意：</strong> 本页面暂未开通实时评论功能。如需联系，请通过上方邮箱或 GitHub 与我交流。
  </p>

  <div style="
    background: rgba(255, 255, 255, 0.15);
    padding: 1.2rem;
    border-radius: 10px;
    border-left: 5px solid #ffdd40;
    margin-top: 1.5rem;
  ">
    <p style="margin: 0; font-size: 0.95rem; line-height: 1.6;">
      <strong>💡 说明：</strong> 此“留言板”为静态说明页面。<br>
      所有关于游戏服务器、博客内容的讨论，欢迎通过其他渠道进行。
    </p>
  </div>

</div>

<!-- 悬停效果（保留） -->
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
