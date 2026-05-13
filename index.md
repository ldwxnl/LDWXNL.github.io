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

<!-- 音乐播放器区域 -->
<div style="
  max-width: 800px;
  margin: 2rem auto;
  padding: 2rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.05);
">
  <h2 style="margin-top: 0; color: #333; font-size: 1.8rem; text-align: center; margin-bottom: 1.5rem;">🎵 音乐播放器</h2>
  <!-- APlayer 播放器 -->
  <meting-js
    server="netease"
    type="playlist"
    id="8653606632"
    fixed="false"
    loop="all"
    order="list"
    list-folded="false"
    list-max-height="300px"
    theme="#ff4081">
  </meting-js>
</div>

<hr style="margin: 3rem 0; border: none; border-top: 2px solid #eee;">

<!-- 留言板完整区域 -->
<div style="
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.05);
">
  <h2 style="margin-top: 0; color: #333; font-size: 1.8rem; text-align: center;">💬 玩家留言板</h2>
  
  <p style="color: #666; line-height: 1.6; margin-bottom: 1.5rem; text-align: center;">
    欢迎大家在下方留言交流游戏心得、反馈问题或分享进服体验！
  </p>
  
  <div style="
    background: #f8f9fa;
    border-left: 4px solid #4CAF50;
    padding: 1rem 1.5rem;
    margin-bottom: 2rem;
    border-radius: 0 6px 6px 0;
  ">
    <p style="margin: 0; color: #555; font-size: 0.95rem;">
      <strong>📌 提示：</strong> 评论需要 GitHub 账号，数据会保存在仓库的 Discussions 中。
      闲聊、反馈、求带都可以，但请注意网络礼仪。
    </p>
  </div>
  
  <!-- Giscus 评论区 -->
  <div class="giscus"></div>
</div>

<!-- 引入 APlayer 和 MetingJS 资源 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/meting@2.0.1/dist/Meting.min.js"></script>

<!-- 引入 Giscus 评论系统 -->
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

<!-- 优化样式 -->
<style>
  /* 确保Giscus框架填满容器 */
  .giscus, .giscus-frame {
    width: 100%;
    border: none;
    min-height: 300px;
  }
  
  /* 隐藏默认的giscus页眉页脚（可选） */
  .giscus .giscus-header,
  .giscus .giscus-footer {
    display: none;
  }
  
  /* APlayer 播放器响应式适配 */
  .aplayer {
    margin: 0 auto;
  }
</style>
