---
layout: default
title: 首页
---

<!-- 引入字体图标（术立口音乐所需） -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

<!-- 主容器：统一的毛玻璃背景 -->
<div class="page-container">
  
  <!-- 头像和自我介绍区域 -->
  <div class="profile-section">
    <img src="/assets/images/avatar.jpg" alt="我的头像" class="avatar">
    <div class="profile-text">
      <h3>关于我</h3>
      <p>你好！我是 LDWXNL，热爱技术、分享与交流。这个网站是我记录学习、项目和生活的空间。你问我是谁，别问，问就是ldwxnl</p>
      <p class="contact-info">
        <i class="fas fa-envelope"></i> 联系我: to@hrn.cc.cd | 
        <a href="https://github.com/LDWXNL" target="_blank"><i class="fab fa-github"></i> GitHub</a>
      </p>
    </div>
  </div>

  <!-- 网站核心功能按钮区域 -->
  <div class="actions-section">
    <h4><i class="fas fa-crosshairs"></i> 探索更多</h4>
    <div class="button-group">
      <a href="/posts" class="action-btn">
        <i class="fas fa-book"></i> 查看我的博客
      </a>
      <a href="/games" class="action-btn">
        <i class="fas fa-gamepad"></i> 游戏中心
      </a>
    </div>
  </div>

  <hr class="divider">

  <!-- 留言板区域 -->
  <div class="comments-section">
    <h2><i class="fas fa-comments"></i> 玩家留言板</h2>
    <p>欢迎大家在下方留言交流游戏心得、反馈问题或分享进服体验！</p>
    
    <!-- 提示框 -->
    <div class="tip-box">
      <p><strong>📌 提示：</strong> 评论需要 GitHub 账号，数据会保存在仓库的 Discussions 中。闲聊、反馈、求带都可以，但请注意网络礼仪。</p>
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

<style>
/* ===== 全局样式重置 ===== */
.page-container * {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* ===== 主容器（毛玻璃效果） ===== */
.page-container {
  background: rgba(249, 249, 249, 0.8); /* 半透明背景 */
  backdrop-filter: blur(10px); /* 关键：毛玻璃模糊效果 */
  -webkit-backdrop-filter: blur(10px);
  padding: 3rem 2rem;
  border-radius: 20px; /* 更大的圆角 */
  margin: 2rem 0;
  border: 1px solid rgba(255, 255, 255, 0.5); /* 白色边框增强玻璃感 */
  box-shadow: 
    0 8px 32px rgba(0, 0, 0, 0.1), /* 外阴影 */
    inset 0 1px 0 rgba(255, 255, 255, 0.6); /* 内发光 */
}

/* ===== 头像区域 ===== */
.profile-section {
  display: flex;
  align-items: center;
  gap: 2rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
}

.avatar {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid white;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15); /* 更强的阴影 */
  transition: transform 0.3s ease; /* 悬停动画 */
}
.avatar:hover {
  transform: scale(1.05); /* 悬停放大 */
}

.profile-text h3 {
  margin-top: 0;
  color: #2d3748; /* 更深的灰色 */
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}

.profile-text p {
  line-height: 1.7;
  color: #4a5568;
  margin-bottom: 0.8rem;
}

.contact-info {
  color: #718096;
  font-size: 0.95rem;
}
.contact-info a {
  color: #4299e1;
  text-decoration: none;
  border-bottom: 1px dashed #4299e1;
  margin-left: 4px;
}
.contact-info i {
  margin-right: 4px;
}

/* ===== 功能按钮区域 ===== */
.actions-section {
  text-align: center;
  margin-bottom: 2rem;
}

.actions-section h4 {
  color: #4a5568;
  margin-bottom: 1.5rem;
  font-size: 1.3rem;
}

.button-group {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.action-btn {
  padding: 1rem 2.5rem;
  color: #2d3748;
  text-decoration: none;
  border: 2px solid #2d3748;
  border-radius: 12px; /* 更大的圆角 */
  font-weight: 600;
  background: transparent;
  transition: all 0.3s ease;
  text-align: center;
  min-width: 180px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px; /* 图标和文字间距 */
}
.action-btn:hover {
  background: #2d3748;
  color: white;
  transform: translateY(-3px); /* 悬停上浮 */
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.15);
}

/* ===== 分割线 ===== */
.divider {
  margin: 3rem 0;
  border: none;
  border-top: 2px solid #e2e8f0;
}

/* ===== 留言板区域 ===== */
.comments-section {
  max-width: 800px;
  margin: 0 auto;
  padding: 2.5rem;
  background: white;
  border-radius: 16px;
  box-shadow: 0 6px 24px rgba(0, 0, 0, 0.08);
}

.comments-section h2 {
  margin-top: 0;
  color: #2d3748;
  font-size: 1.8rem;
  text-align: center;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.comments-section > p {
  color: #718096;
  line-height: 1.6;
  margin-bottom: 1.5rem;
  text-align: center;
}

.tip-box {
  background: #f0fff4; /* 浅绿色背景 */
  border-left: 4px solid #48bb78; /* 绿色边框 */
  padding: 1rem 1.5rem;
  margin-bottom: 2rem;
  border-radius: 0 8px 8px 0;
}
.tip-box p {
  margin: 0;
  color: #2d3748;
  font-size: 0.95rem;
}

/* ===== Giscus 样式优化 ===== */
.giscus, .giscus-frame {
  width: 100%;
  border: none;
  min-height: 300px;
  border-radius: 12px;
}

/* ===== 响应式设计（移动端适配） ===== */
@media (max-width: 768px) {
  .page-container {
    padding: 2rem 1rem;
    margin: 1rem 0;
  }
  
  .profile-section {
    flex-direction: column;
    text-align: center;
    gap: 1.5rem;
  }
  
  .button-group {
    flex-direction: column;
    gap: 1rem;
  }
  
  .comments-section {
    padding: 1.5rem;
  }
}
</style>
