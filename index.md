---
layout: default
title: 首页
---
<!--
  完整修复版：
  1. 音乐播放器：渲染播放列表，自动跳过无法播放的音源，支持URL/网易云ID添加
  2. HRSI 助手：接入硅基流动 API，保留三重人格人设，带对话记忆
  3. 聊天室：localStorage 同步，用户头像首字母+颜色
  4. Giscus 留言板
-->

<style>
  /* ===== 全局重置与变量 ===== */
  :root {
    --primary: #4c6ef5;
    --primary-light: #748ffc;
    --primary-dark: #3b5bdb;
    --bg-body: #f0f2f5;
    --bg-card: #ffffff;
    --text-primary: #1a1a2e;
    --text-secondary: #4a4a6a;
    --text-muted: #8888aa;
    --shadow-sm: 0 2px 12px rgba(0, 0, 0, 0.06);
    --shadow-md: 0 8px 30px rgba(0, 0, 0, 0.08);
    --shadow-lg: 0 16px 48px rgba(0, 0, 0, 0.12);
    --radius: 16px;
    --radius-sm: 10px;
    --transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  }

  /* ===== 页面主容器 ===== */
  .page-wrapper {
    max-width: 1100px;
    margin: 0 auto;
    padding: 2rem 1.5rem 4rem;
  }

  /* ===== 个人卡片 ===== */
  .profile-card {
    background: var(--bg-card);
    border-radius: var(--radius);
    box-shadow: var(--shadow-md);
    padding: 2rem 2.5rem;
    margin-bottom: 2rem;
    display: flex;
    align-items: center;
    gap: 2.5rem;
    flex-wrap: wrap;
    transition: var(--transition);
  }
  .profile-card:hover {
    box-shadow: var(--shadow-lg);
  }
  .profile-avatar {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    object-fit: cover;
    border: 4px solid var(--primary);
    box-shadow: 0 4px 16px rgba(76, 110, 245, 0.25);
    flex-shrink: 0;
    transition: var(--transition);
    background: var(--primary-light);
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
    font-weight: 600;
  }
  .profile-avatar:hover {
    transform: scale(1.03);
  }
  .profile-info {
    flex: 1;
    min-width: 220px;
  }
  .profile-info h1 {
    font-size: 2rem;
    font-weight: 700;
    color: var(--text-primary);
    margin: 0 0 0.3rem 0;
    letter-spacing: -0.5px;
  }
  .profile-info .tagline {
    font-size: 1.05rem;
    color: var(--text-secondary);
    line-height: 1.7;
    margin: 0.2rem 0 0.6rem 0;
  }
  .profile-info .tagline strong {
    color: var(--primary);
    font-weight: 600;
  }
  .profile-links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.8rem 1.5rem;
    margin-top: 0.5rem;
  }
  .profile-links a {
    color: var(--text-secondary);
    text-decoration: none;
    font-size: 0.92rem;
    border-bottom: 2px solid transparent;
    transition: var(--transition);
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
  }
  .profile-links a:hover {
    color: var(--primary);
    border-bottom-color: var(--primary);
  }

  /* ===== 功能卡片通用 ===== */
  .section-card {
    background: var(--bg-card);
    border-radius: var(--radius);
    box-shadow: var(--shadow-sm);
    padding: 1.8rem 2rem;
    margin-bottom: 2rem;
    transition: var(--transition);
  }
  .section-card:hover {
    box-shadow: var(--shadow-md);
  }
  .section-card .card-title {
    font-size: 1.3rem;
    font-weight: 600;
    color: var(--text-primary);
    margin: 0 0 0.3rem 0;
    display: flex;
    align-items: center;
    gap: 0.6rem;
  }
  .section-card .card-sub {
    color: var(--text-muted);
    font-size: 0.92rem;
    margin: 0 0 1.2rem 0;
  }

  /* ===== 探索按钮 ===== */
  .explore-row {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    flex-wrap: wrap;
    margin: 0.5rem 0 0.5rem 0;
  }
  .explore-btn {
    padding: 0.8rem 2.4rem;
    border: 2px solid var(--text-primary);
    border-radius: var(--radius-sm);
    font-weight: 600;
    font-size: 1rem;
    color: var(--text-primary);
    background: transparent;
    text-decoration: none;
    transition: var(--transition);
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
  }
  .explore-btn:hover {
    background: var(--text-primary);
    color: #fff;
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
  }
  .explore-btn.primary {
    background: var(--primary);
    border-color: var(--primary);
    color: #fff;
  }
  .explore-btn.primary:hover {
    background: var(--primary-dark);
    border-color: var(--primary-dark);
  }

  /* ===== 音乐播放器 ===== */
  .player-wrap {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .player-main {
    display: flex;
    align-items: center;
    gap: 1.5rem;
    flex-wrap: wrap;
  }
  .player-cover {
    width: 90px;
    height: 90px;
    border-radius: var(--radius-sm);
    background: linear-gradient(135deg, #4c6ef5, #a855f7);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2.4rem;
    color: #fff;
    flex-shrink: 0;
    box-shadow: 0 4px 16px rgba(76, 110, 245, 0.25);
    transition: var(--transition);
  }
  .player-cover.loading {
    animation: pulse-cover 1.2s ease-in-out infinite;
  }
  @keyframes pulse-cover {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.6; }
  }
  .player-info {
    flex: 1;
    min-width: 160px;
  }
  .player-info .song-title {
    font-weight: 600;
    font-size: 1.05rem;
    color: var(--text-primary);
    margin: 0 0 0.1rem 0;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .player-info .song-artist {
    font-size: 0.88rem;
    color: var(--text-muted);
    margin: 0;
  }
  .player-controls {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    flex-wrap: wrap;
    margin-top: 0.3rem;
  }
  .player-controls button {
    background: none;
    border: none;
    font-size: 1.4rem;
    cursor: pointer;
    color: var(--text-secondary);
    padding: 0.2rem 0.4rem;
    border-radius: 8px;
    transition: var(--transition);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 38px;
    height: 38px;
  }
  .player-controls button:hover {
    background: #f0f2ff;
    color: var(--primary);
  }
  .player-controls button.play-btn {
    background: var(--primary);
    color: #fff;
    width: 44px;
    height: 44px;
    border-radius: 50%;
    font-size: 1.2rem;
  }
  .player-controls button.play-btn:hover {
    background: var(--primary-dark);
    transform: scale(1.05);
  }
  .player-progress {
    flex: 1;
    min-width: 120px;
    display: flex;
    align-items: center;
    gap: 0.6rem;
  }
  .player-progress input[type="range"] {
    -webkit-appearance: none;
    appearance: none;
    width: 100%;
    height: 4px;
    border-radius: 2px;
    background: #ddd;
    outline: none;
    transition: var(--transition);
  }
  .player-progress input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: var(--primary);
    cursor: pointer;
    box-shadow: 0 2px 8px rgba(76, 110, 245, 0.3);
  }
  .player-progress input[type="range"]::-moz-range-thumb {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    background: var(--primary);
    cursor: pointer;
    border: none;
  }
  .player-time {
    font-size: 0.78rem;
    color: var(--text-muted);
    font-variant-numeric: tabular-nums;
    min-width: 70px;
    text-align: center;
  }
  .player-volume {
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
  .player-volume input[type="range"] {
    -webkit-appearance: none;
    appearance: none;
    width: 60px;
    height: 3px;
    border-radius: 2px;
    background: #ddd;
    outline: none;
  }
  .player-volume input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: var(--primary);
    cursor: pointer;
  }
  .player-volume input[type="range"]::-moz-range-thumb {
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: var(--primary);
    cursor: pointer;
    border: none;
  }

  /* 播放列表 */
  .playlist-wrap {
    border-top: 1px solid #eee;
    padding-top: 1rem;
    margin-top: 0.2rem;
  }
  .playlist-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 0.5rem;
  }
  .playlist-header span {
    font-weight: 500;
    font-size: 0.9rem;
    color: var(--text-secondary);
  }
  .playlist-header .btn-group {
    display: flex;
    gap: 0.4rem;
    flex-wrap: wrap;
  }
  .playlist-header .add-btn {
    background: none;
    border: 1px dashed #ccc;
    padding: 0.2rem 0.8rem;
    border-radius: 20px;
    font-size: 0.8rem;
    color: var(--text-muted);
    cursor: pointer;
    transition: var(--transition);
    white-space: nowrap;
  }
  .playlist-header .add-btn:hover {
    border-color: var(--primary);
    color: var(--primary);
    background: #f8f9ff;
  }
  .playlist-items {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
    max-height: 180px;
    overflow-y: auto;
    padding-right: 4px;
  }
  .playlist-items::-webkit-scrollbar {
    width: 4px;
  }
  .playlist-items::-webkit-scrollbar-thumb {
    background: #ccc;
    border-radius: 4px;
  }
  .playlist-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0.4rem 0.6rem;
    border-radius: 8px;
    font-size: 0.82rem;
    color: var(--text-secondary);
    cursor: pointer;
    transition: var(--transition);
  }
  .playlist-item:hover {
    background: #f5f7ff;
  }
  .playlist-item.active {
    background: #eef1ff;
    color: var(--primary);
    font-weight: 500;
  }
  .playlist-item .del-btn {
    background: none;
    border: none;
    color: #ccc;
    cursor: pointer;
    font-size: 0.75rem;
    padding: 0 0.2rem;
    transition: var(--transition);
  }
  .playlist-item .del-btn:hover {
    color: #e74c3c;
  }
  .playlist-empty {
    color: var(--text-muted);
    font-size: 0.85rem;
    text-align: center;
    padding: 0.8rem 0;
  }

  /* ===== 聊天室 ===== */
  .chat-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin-top: 0.5rem;
  }
  @media (max-width: 720px) {
    .chat-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }
  }
  .chat-room {
    border: 1px solid #eee;
    border-radius: var(--radius-sm);
    overflow: hidden;
    display: flex;
    flex-direction: column;
    height: 420px;
  }
  .chat-room .chat-header {
    background: #f8f9ff;
    padding: 0.6rem 1rem;
    font-weight: 600;
    font-size: 0.95rem;
    color: var(--text-primary);
    border-bottom: 1px solid #eee;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-shrink: 0;
  }
  .chat-room .chat-header .badge {
    font-size: 0.7rem;
    background: #4c6ef5;
    color: #fff;
    padding: 0.1rem 0.6rem;
    border-radius: 12px;
    font-weight: 500;
  }
  .chat-messages {
    flex: 1;
    overflow-y: auto;
    padding: 0.8rem 1rem;
    background: #fafbff;
    display: flex;
    flex-direction: column;
    gap: 0.4rem;
  }
  .chat-messages .msg {
    max-width: 80%;
    padding: 0.4rem 0.8rem;
    border-radius: 12px;
    font-size: 0.86rem;
    line-height: 1.5;
    word-break: break-word;
    animation: fade-in 0.25s ease;
    display: flex;
    align-items: flex-start;
    gap: 0.5rem;
  }
  .chat-messages .msg .avatar {
    width: 26px;
    height: 26px;
    border-radius: 50%;
    background: #4c6ef5;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.68rem;
    font-weight: 600;
    flex-shrink: 0;
    text-transform: uppercase;
  }
  .chat-messages .msg .content {
    flex: 1;
  }
  .chat-messages .msg .name {
    font-weight: 600;
    font-size: 0.77rem;
    display: block;
  }
  .chat-messages .msg .time {
    font-size: 0.62rem;
    opacity: 0.6;
    margin-left: 0.4rem;
  }
  .chat-messages .msg.self {
    align-self: flex-end;
    background: var(--primary);
    color: #fff;
    border-bottom-right-radius: 4px;
  }
  .chat-messages .msg.self .avatar {
    order: 1;
  }
  .chat-messages .msg.self .name {
    color: rgba(255,255,255,0.8);
  }
  .chat-messages .msg.other {
    align-self: flex-start;
    background: #fff;
    color: var(--text-primary);
    border: 1px solid #e8ecff;
    border-bottom-left-radius: 4px;
  }
  .chat-messages .msg.other .name {
    color: var(--primary);
  }
  .chat-messages .empty-chat {
    color: var(--text-muted);
    font-size: 0.83rem;
    text-align: center;
    padding: 2rem 0;
  }
  @keyframes fade-in {
    from { opacity: 0; transform: translateY(6px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .chat-input-row {
    display: flex;
    gap: 0.5rem;
    padding: 0.5rem 0.8rem;
    border-top: 1px solid #eee;
    background: #fff;
    flex-shrink: 0;
  }
  .chat-input-row input {
    flex: 1;
    border: 1px solid #e0e4f0;
    border-radius: 20px;
    padding: 0.4rem 1rem;
    font-size: 0.87rem;
    outline: none;
    transition: var(--transition);
    background: #fafbff;
  }
  .chat-input-row input:focus {
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(76, 110, 245, 0.12);
  }
  .chat-input-row button {
    background: var(--primary);
    color: #fff;
    border: none;
    border-radius: 20px;
    padding: 0.4rem 1.2rem;
    font-weight: 500;
    font-size: 0.84rem;
    cursor: pointer;
    transition: var(--transition);
  }
  .chat-input-row button:hover {
    background: var(--primary-dark);
    transform: scale(1.02);
  }

  /* ===== Giscus 留言板 ===== */
  .giscus-wrap {
    margin-top: 0.5rem;
  }
  .giscus-wrap .giscus {
    width: 100%;
    border: none;
    min-height: 310px;
  }

  /* ===== HRSI 聊天按钮 ===== */
  .hrsi-toggle {
    position: fixed;
    bottom: 24px;
    right: 24px;
    z-index: 9998;
    background: var(--primary);
    color: #fff;
    border: none;
    border-radius: 50%;
    width: 54px;
    height: 54px;
    font-size: 24px;
    cursor: pointer;
    box-shadow: 0 4px 18px rgba(76, 110, 245, 0.34);
    transition: var(--transition);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .hrsi-toggle:hover {
    transform: scale(1.07);
    box-shadow: 0 6px 26px rgba(76, 110, 245, 0.43);
  }
  .hrsi-toggle .badge-dot {
    position: absolute;
    top: 4px;
    right: 4px;
    width: 11px;
    height: 11px;
    border-radius: 50%;
    background: #22c55e;
    border: 2px solid #fff;
  }

  /* ===== HRSI 聊天框 ===== */
  .hrsi-box {
    position: fixed;
    bottom: 88px;
    right: 24px;
    width: 370px;
    max-width: calc(100vw - 46px);
    height: 480px;
    max-height: calc(100vh - 140px);
    background: #1a1a2e;
    border-radius: var(--radius);
    box-shadow: var(--shadow-lg);
    display: none;
    flex-direction: column;
    z-index: 9999;
    color: #eee;
    font-family: 'Segoe UI', system-ui, sans-serif;
    overflow: hidden;
    border: 1px solid rgba(255, 255, 255, 0.06);
    animation: slide-up 0.33s ease;
  }
  .hrsi-box.open {
    display: flex;
  }
  @keyframes slide-up {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  .hrsi-box .hrsi-header {
    background: var(--primary);
    padding: 0.65rem 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-shrink: 0;
  }
  .hrsi-box .hrsi-header span {
    font-weight: 650;
    font-size: 0.94rem;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
  .hrsi-box .hrsi-header .close-btn {
    background: none;
    border: none;
    color: #fff;
    font-size: 1.2rem;
    cursor: pointer;
    opacity: 0.73;
    transition: var(--transition);
    padding: 0 0.2rem;
  }
  .hrsi-box .hrsi-header .close-btn:hover {
    opacity: 1;
    transform: rotate(90deg);
  }
  .hrsi-box .hrsi-msgs {
    flex: 1;
    overflow-y: auto;
    padding: 0.8rem 1rem;
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    background: #16213e;
  }
  .hrsi-box .hrsi-msgs .msg {
    max-width: 88%;
    padding: 0.47rem 0.85rem;
    border-radius: 12px;
    font-size: 0.86rem;
    line-height: 1.51;
    animation: fade-in 0.23s ease;
  }
  .hrsi-box .hrsi-msgs .msg.user {
    align-self: flex-end;
    background: var(--primary);
    color: #fff;
    border-bottom-right-radius: 4px;
  }
  .hrsi-box .hrsi-msgs .msg.bot {
    align-self: flex-start;
    background: #2a3a5e;
    color: #dde;
    border-bottom-left-radius: 4px;
  }
  .hrsi-box .hrsi-msgs .msg.bot .label {
    font-size: 0.63rem;
    opacity: 0.67;
    display: block;
    margin-bottom: 0.1rem;
  }
  .hrsi-box .hrsi-msgs .empty-hrsi {
    color: rgba(255,255,255,0.36);
    font-size: 0.84rem;
    text-align: center;
    padding: 2rem 0;
  }
  .hrsi-box .hrsi-input-row {
    display: flex;
    gap: 0.5rem;
    padding: 0.5rem 0.8rem;
    border-top: 1px solid rgba(255,255,255,0.055);
    background: #1a1a2e;
    flex-shrink: 0;
  }
  .hrsi-box .hrsi-input-row input {
    flex: 1;
    border: 1px solid rgba(255,255,255,0.085);
    border-radius: 20px;
    padding: 0.375rem 1rem;
    font-size: 0.835rem;
    outline: none;
    background: #0f0f1f;
    color: #eee;
    transition: var(--transition);
  }
  .hrsi-box .hrsi-input-row input:focus {
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(76, 110, 245, 0.145);
  }
  .hrsi-box .hrsi-input-row input::placeholder {
    color: #565656;
  }
  .hrsi-box .hrsi-input-row button {
    background: var(--primary);
    color: #fff;
    border: none;
    border-radius: 20px;
    padding: 0.395rem 1rem;
    font-weight: 570;
    font-size: 0.785rem;
    cursor: pointer;
    transition: var(--transition);
  }
  .hrsi-box .hrsi-input-row button:hover {
    background: var(--primary-dark);
  }
  .hrsi-box .hrsi-input-row button:disabled {
    opacity: 0.415;
    cursor: not-allowed;
  }

  /* ===== 响应式微调 ===== */
  @media (max-width: 680px) {
    .page-wrapper {
      padding: 1rem 0.7rem 3rem;
    }
    .profile-card {
      padding: 1.1rem 1.1rem;
      gap: 1.1rem;
    }
    .profile-avatar {
      width: 78px;
      height: 78px;
      font-size: 1.9rem;
    }
    .profile-info h1 {
      font-size: 1.38rem;
    }
    .section-card {
      padding: 1.1rem 0.9rem;
    }
    .player-main {
      gap: 0.7rem;
    }
    .player-cover {
      width: 62px;
      height: 62px;
      font-size: 1.5rem;
    }
    .player-controls button {
      width: 29px;
      height: 29px;
      font-size: 1rem;
    }
    .player-controls button.play-btn {
      width: 36px;
      height: 36px;
      font-size: 0.99rem;
    }
    .player-volume input[type="range"] {
      width: 36px;
    }
    .hrsi-box {
      width: calc(100vw - 30px);
      right: 15px;
      bottom: 78px;
      height: 410px;
    }
    .explore-btn {
      padding: 0.49rem 1.2rem;
      font-size: 0.865rem;
    }
    .playlist-header .btn-group {
      gap: 0.225rem;
    }
    .playlist-header .add-btn {
      font-size: 0.675rem;
      padding: 0.095rem 0.475rem;
    }
    .chat-messages .msg .avatar {
      width: 19px;
      height: 19px;
      font-size: 0.595rem;
    }
  }

  /* ===== 自定义滚动条 ===== */
  .chat-messages::-webkit-scrollbar,
  .hrsi-msgs::-webkit-scrollbar,
  .playlist-items::-webkit-scrollbar {
    width: 4px;
  }
  .chat-messages::-webkit-scrollbar-thumb,
  .hrsi-msgs::-webkit-scrollbar-thumb,
  .playlist-items::-webkit-scrollbar-thumb {
    background: #bbb;
    border-radius: 4px;
  }
  .chat-messages::-webkit-scrollbar-track,
  .hrsi-msgs::-webkit-scrollbar-track {
    background: transparent;
  }

  /* ===== 分割线 ===== */
  .divider {
    border: none;
    border-top: 2px solid #edf0f5;
    margin: 2rem 0 1.8rem 0;
  }
</style>

<!-- ============================================================ -->
<!-- 页面主体 -->
<!-- ============================================================ -->
<div class="page-wrapper">

  <!-- ====== 1. 个人卡片 ====== -->
  <div class="profile-card">
    <img src="/assets/images/avatar.jpg"
         alt="我的头像"
         class="profile-avatar"
         onerror="this.style.display='none'; this.parentNode.querySelector('.fallback-avatar').style.display='flex';">
    <div class="fallback-avatar profile-avatar" style="display:none;">L</div>
    <div class="profile-info">
      <h1>LDWXNL</h1>
      <p class="tagline">
        你好！我是 <strong>LDWXNL</strong>，热爱技术、分享与交流。<br>
        这个网站是我记录学习、项目和生活的空间。<br>
        你问我是谁？别问，问就是 <strong>hrsi</strong> 🚀
      </p>
      <div class="profile-links">
        <a href="mailto:to@hrn.cc.cd">📧 to@hrn.cc.cd</a>
        <a href="https://github.com/ldwxnl" target="_blank">🐙 GitHub</a>
      </div>
    </div>
  </div>

  <!-- ====== 2. 音乐播放器 ====== -->
  <div class="section-card">
    <div class="card-title">🎵 音乐播放器 · 纯音乐</div>
    <div class="card-sub">内置多个免费音源，自动跳过无法播放的链接。您也可以添加自己的URL或网易云ID。</div>

    <div class="player-wrap">
      <div class="player-main">
        <div class="player-cover" id="playerCover">🎶</div>
        <div class="player-info">
          <div class="song-title" id="songTitle">未播放</div>
          <div class="song-artist" id="songArtist">—</div>
          <div class="player-controls">
            <button onclick="prevSong()" title="上一首">⏮</button>
            <button class="play-btn" id="playBtn" onclick="togglePlay()">▶</button>
            <button onclick="nextSong()" title="下一首">⏭</button>
            <div class="player-progress">
              <span class="player-time" id="currentTime">0:00</span>
              <input type="range" id="progressBar" value="0" step="0.01" oninput="seekProgress(this.value)">
              <span class="player-time" id="totalTime">0:00</span>
            </div>
            <div class="player-volume">
              <span>🔊</span>
              <input type="range" id="volumeBar" min="0" max="1" step="0.01" value="0.71" oninput="setVolume(this.value)">
            </div>
          </div>
        </div>
      </div>

      <div class="playlist-wrap">
        <div class="playlist-header">
          <span>📋 播放列表 (<span id="playlistCount">0</span>)</span>
          <div class="btn-group">
            <button class="add-btn" onclick="addSongByURL()">🔗 添加URL</button>
            <button class="add-btn" onclick="addNeteaseSong()" style="border-color:var(--primary);color:var(--primary);">🎵 网易云ID</button>
          </div>
        </div>
        <div class="playlist-items" id="playlistContainer">
          <div class="playlist-empty">暂无歌曲，点击添加</div>
        </div>
      </div>
    </div>
  </div>

  <!-- ====== 3. 探索按钮 ====== -->
  <div style="margin: 0.5rem 0 1.8rem 0;">
    <div class="explore-row">
      <a href="/posts" class="explore-btn">📖 查看我的博客</a>
      <a href="/games" class="explore-btn primary">🎮 游戏中心</a>
    </div>
  </div>

  <hr class="divider">

  <!-- ====== 4. 聊天室 + 留言板 ====== -->
  <div class="section-card" style="padding-bottom: 0.5rem;">
    <div class="card-title">💬 交流社区</div>
    <div class="card-sub">在聊天室实时畅聊，或在留言板留下你的想法</div>

    <div class="chat-grid">
      <div class="chat-room">
        <div class="chat-header">
          <span>💬 即时聊天室</span>
          <span class="badge">🟢 在线</span>
        </div>
        <div class="chat-messages" id="chatMessages">
          <div class="empty-chat">还没有消息，来说点什么吧 👋</div>
        </div>
        <div class="chat-input-row">
          <input type="text" id="chatInput" placeholder="输入消息…" onkeydown="if(event.key==='Enter') sendChat()">
          <button onclick="sendChat()">发送</button>
        </div>
      </div>

      <div style="display:flex;flex-direction:column;gap:0.3rem;">
        <div style="font-weight:500;font-size:0.955rem;color:var(--text-secondary);">📝 留言板</div>
        <div style="flex:1;min-height:280px;border-radius:var(--radius-sm);overflow:hidden;background:#fafbff;padding:0.175rem;">
          <div class="giscus"></div>
        </div>
        <div style="font-size:0.775rem;color:var(--text-muted);margin-top:0.125rem;">
          💡 使用 GitHub 账号登录后即可留言
        </div>
      </div>
    </div>
  </div>

</div>

<!-- ============================================================ -->
<!-- HRSI 聊天按钮 & 聊天框 -->
<!-- ============================================================ -->
<button class="hrsi-toggle" id="hrsiToggle" onclick="toggleHRSI()" title="HRSI AI 助手">
  🤖
  <span class="badge-dot"></span>
</button>

<div class="hrsi-box" id="hrsiBox">
  <div class="hrsi-header">
    <span>🔥 HRSI AI 助手</span>
    <button class="close-btn" onclick="toggleHRSI()">✕</button>
  </div>
  <div class="hrsi-msgs" id="hrsiMsgs">
    <div class="empty-hrsi">👋 你好！我是 HRSI，有什么可以帮你？</div>
  </div>
  <div class="hrsi-input-row">
    <input type="text" id="hrsiInput" placeholder="问 HRSI 点什么…" onkeydown="if(event.key==='Enter') sendHRSI()">
    <button id="hrsiSendBtn" onclick="sendHRSI()">发送</button>
  </div>
</div>

<!-- ============================================================ -->
<!-- 脚本区 -->
<!-- ============================================================ -->

<!-- Giscus 评论系统 -->
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

<!-- ===== 音乐播放器脚本（渲染播放列表 + 修复版） ===== -->
<script>
(function() {
    'use strict';

    const defaultSongs = [
        { title: 'SoundHelix 1', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3' },
        { title: 'SoundHelix 2', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3' },
        { title: 'SoundHelix 3', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3' },
        { title: 'SoundHelix 4', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3' },
        { title: 'Piano', artist: 'FMA', url: 'https://files.freemusicarchive.org/storage-freemusicarchive-org/music/no_curator/Tours/Enthusiast/Tours_-_01_-_Enthusiast.mp3' },
        { title: 'Ambient', artist: 'FMA', url: 'https://files.freemusicarchive.org/storage-freemusicarchive-org/music/Creative_Commons/Ketsa/Raising_Frequencies/Ketsa_-_01_-_Raising_Frequencies.mp3' }
    ];

    let playlist = [];
    let currentIndex = 0;
    let isPlaying = false;
    let isDragging = false;
    let failCount = 0;

    const audio = new Audio();
    const playBtn = document.getElementById('playBtn');
    const progressBar = document.getElementById('progressBar');
    const volumeBar = document.getElementById('volumeBar');
    const currentTimeEl = document.getElementById('currentTime');
    const totalTimeEl = document.getElementById('totalTime');
    const songTitle = document.getElementById('songTitle');
    const songArtist = document.getElementById('songArtist');
    const playlistContainer = document.getElementById('playlistContainer');
    const playlistCount = document.getElementById('playlistCount');
    const playerCover = document.getElementById('playerCover');

    function formatTime(sec) {
        if (!sec || isNaN(sec)) return '0:00';
        const m = Math.floor(sec / 60);
        const s = Math.floor(sec % 60);
        return m + ':' + (s < 10 ? '0' : '') + s;
    }

    function loadPlaylist() {
        try {
            const saved = localStorage.getItem('music_playlist');
            if (saved) {
                const parsed = JSON.parse(saved);
                if (Array.isArray(parsed) && parsed.length > 0) {
                    playlist = parsed;
                    return;
                }
            }
        } catch (_) {}
        playlist = JSON.parse(JSON.stringify(defaultSongs));
        savePlaylist();
    }

    function savePlaylist() {
        try {
            localStorage.setItem('music_playlist', JSON.stringify(playlist));
        } catch (_) {}
    }

    function renderPlaylist() {
        playlistContainer.innerHTML = '';
        if (!playlist.length) {
            playlistContainer.innerHTML = '<div class="playlist-empty">暂无歌曲，点击上方按钮添加</div>';
            playlistCount.textContent = '0';
            return;
        }
        playlistCount.textContent = playlist.length;
        playlist.forEach((song, idx) => {
            const item = document.createElement('div');
            item.className = 'playlist-item' + (idx === currentIndex ? ' active' : '');
            const infoSpan = document.createElement('span');
            infoSpan.textContent = (song.title || '未命名') + ' — ' + (song.artist || '未知');
            const delBtn = document.createElement('button');
            delBtn.className = 'del-btn';
            delBtn.textContent = '✕';
            delBtn.addEventListener('click', function(e) {
                e.stopPropagation();
                removeSong(idx);
            });
            item.appendChild(infoSpan);
            item.appendChild(delBtn);
            item.addEventListener('click', function() {
                playSong(idx);
            });
            playlistContainer.appendChild(item);
        });
    }

    function playSong(index) {
        if (index < 0 || index >= playlist.length) return;
        currentIndex = index;
        const song = playlist[index];
        if (!song || !song.url) return;
        if (window.retryTimer) {
            clearTimeout(window.retryTimer);
            window.retryTimer = null;
        }
        audio.src = song.url;
        audio.load();
        audio.volume = parseFloat(volumeBar.value) || 0.71;
        songTitle.textContent = song.title || '未命名';
        songArtist.textContent = song.artist || '未知';
        playerCover.textContent = '🎵';
        playerCover.classList.remove('loading');
        failCount = 0;
        audio.play().then(() => {
            isPlaying = true;
            playBtn.textContent = '⏸';
            renderPlaylist();
        }).catch(() => {
            failCount++;
            if (failCount < playlist.length) {
                playerCover.textContent = '⚠️';
                playerCover.classList.add('loading');
                window.retryTimer = setTimeout(() => nextSong(), 2000);
            } else {
                playerCover.textContent = '❌';
                songTitle.textContent = '所有歌曲都无法播放';
                songArtist.textContent = '请检查网络或添加新歌曲';
                playBtn.textContent = '▶';
                isPlaying = false;
            }
        });
    }

    function togglePlay() {
        if (!playlist.length) {
            alert('播放列表为空，请先添加歌曲');
            return;
        }
        if (audio.paused) {
            if (!audio.src) {
                playSong(currentIndex);
                return;
            }
            audio.play().then(() => {
                isPlaying = true;
                playBtn.textContent = '⏸';
            }).catch(() => {});
        } else {
            audio.pause();
            isPlaying = false;
            playBtn.textContent = '▶';
        }
    }

    function nextSong() {
        if (!playlist.length) return;
        const next = (currentIndex + 1) % playlist.length;
        playSong(next);
    }

    function prevSong() {
        if (!playlist.length) return;
        const prev = (currentIndex - 1 + playlist.length) % playlist.length;
        playSong(prev);
    }

    function removeSong(index) {
        if (index < 0 || index >= playlist.length) return;
        if (playlist.length <= 1) {
            alert('至少保留一首歌曲');
            return;
        }
        playlist.splice(index, 1);
        savePlaylist();
        if (index === currentIndex) {
            if (index >= playlist.length) currentIndex = playlist.length - 1;
            playSong(currentIndex);
        } else if (index < currentIndex) {
            currentIndex--;
        }
        renderPlaylist();
    }

    function addSongByURL() {
        const url = prompt('请输入音乐文件的 URL（mp3 / ogg / wav）：');
        if (!url) return;
        const title = prompt('请输入歌曲名称：') || '未命名';
        const artist = prompt('请输入艺术家名称：') || '未知';
        playlist.push({ title, artist, url });
        savePlaylist();
        renderPlaylist();
        if (playlist.length === 1) playSong(0);
    }

    function addNeteaseSong() {
        const id = prompt('请输入网易云歌曲 ID（例如 186016）：');
        if (!id) return;
        const cleanId = id.trim();
        if (!/^\d+$/.test(cleanId)) {
            alert('请输入数字ID');
            return;
        }
        const url = 'https://music.163.com/song/media/outer/url?id=' + cleanId + '.mp3';
        const title = prompt('请输入歌曲名称（可选）：') || ('网易云歌曲 ' + cleanId);
        const artist = prompt('请输入艺术家名称（可选）：') || '未知';
        playlist.push({ title, artist, url });
        savePlaylist();
        renderPlaylist();
        if (playlist.length === 1) playSong(0);
    }

    function seekProgress(val) {
        if (!audio.duration || isNaN(audio.duration)) return;
        audio.currentTime = (val / 100) * audio.duration;
        currentTimeEl.textContent = formatTime(audio.currentTime);
    }

    function setVolume(val) {
        audio.volume = parseFloat(val);
    }

    audio.addEventListener('timeupdate', function() {
        if (!isDragging && audio.duration) {
            progressBar.value = (audio.currentTime / audio.duration) * 100;
            currentTimeEl.textContent = formatTime(audio.currentTime);
        }
    });
    audio.addEventListener('loadedmetadata', function() {
        totalTimeEl.textContent = formatTime(audio.duration);
        progressBar.value = 0;
    });
    audio.addEventListener('ended', function() { nextSong(); });
    audio.addEventListener('error', function() {
        if (failCount < playlist.length) {
            failCount++;
            playerCover.textContent = '⚠️';
            playerCover.classList.add('loading');
            window.retryTimer = setTimeout(() => nextSong(), 2000);
        }
    });
    audio.addEventListener('canplay', function() {
        playerCover.classList.remove('loading');
        playerCover.textContent = '🎵';
    });
    progressBar.addEventListener('mousedown', function() { isDragging = true; });
    progressBar.addEventListener('mouseup', function() { isDragging = false; });
    progressBar.addEventListener('touchstart', function() { isDragging = true; });
    progressBar.addEventListener('touchend', function() { isDragging = false; });

    window.playSong = playSong;
    window.togglePlay = togglePlay;
    window.nextSong = nextSong;
    window.prevSong = prevSong;
    window.removeSong = removeSong;
    window.addSongByURL = addSongByURL;
    window.addNeteaseSong = addNeteaseSong;
    window.seekProgress = seekProgress;
    window.setVolume = setVolume;

    loadPlaylist();
    renderPlaylist();
    if (playlist.length > 0) playSong(0);
    console.log('播放器已加载，歌单数量:', playlist.length);
})();
</script>
