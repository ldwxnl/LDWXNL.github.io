---
layout: default
title: 首页
---
<!--
  修复内容：
  1. 头像路径恢复为 /assets/images/avatar.jpg，若缺失则显示首字母占位。
  2. 音乐播放器使用 SoundHelix 免费测试曲（无版权，稳定可播），移除所有流行歌曲。
  3. 聊天室消息添加用户头像（首字母 + 随机颜色）。
  4. HRSI 助手对话框修复样式，增强错误处理。
  5. 优化响应式布局，修复若干小bug。
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
  .profile-links .sponsor {
    background: #f8f9ff;
    padding: 0.2rem 0.8rem;
    border-radius: 20px;
    border: 1px solid #e8ecff;
    font-size: 0.85rem;
    color: var(--text-muted);
  }
  .profile-links .sponsor:hover {
    background: #eef1ff;
    border-color: var(--primary-light);
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
    max-height: 160px;
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
    font-size: 0.88rem;
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
    font-size: 0.8rem;
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
    height: 340px;
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
    font-size: 0.88rem;
    line-height: 1.5;
    word-break: break-word;
    animation: fade-in 0.25s ease;
    display: flex;
    align-items: flex-start;
    gap: 0.5rem;
  }
  .chat-messages .msg .avatar {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    background: #4c6ef5;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.7rem;
    font-weight: 600;
    flex-shrink: 0;
    text-transform: uppercase;
  }
  .chat-messages .msg .content {
    flex: 1;
  }
  .chat-messages .msg .name {
    font-weight: 600;
    font-size: 0.78rem;
    display: block;
  }
  .chat-messages .msg .time {
    font-size: 0.6rem;
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
    font-size: 0.85rem;
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
    font-size: 0.88rem;
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
    font-size: 0.85rem;
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
    min-height: 320px;
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
    width: 56px;
    height: 56px;
    font-size: 26px;
    cursor: pointer;
    box-shadow: 0 4px 20px rgba(76, 110, 245, 0.35);
    transition: var(--transition);
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .hrsi-toggle:hover {
    transform: scale(1.08);
    box-shadow: 0 6px 28px rgba(76, 110, 245, 0.45);
  }
  .hrsi-toggle .badge-dot {
    position: absolute;
    top: 4px;
    right: 4px;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: #22c55e;
    border: 2px solid #fff;
  }

  /* ===== HRSI 聊天框 ===== */
  .hrsi-box {
    position: fixed;
    bottom: 92px;
    right: 24px;
    width: 360px;
    max-width: calc(100vw - 48px);
    height: 440px;
    max-height: calc(100vh - 120px);
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
    animation: slide-up 0.3s ease;
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
    padding: 0.7rem 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-shrink: 0;
  }
  .hrsi-box .hrsi-header span {
    font-weight: 600;
    font-size: 0.95rem;
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
    opacity: 0.7;
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
    gap: 0.4rem;
    background: #16213e;
  }
  .hrsi-box .hrsi-msgs .msg {
    max-width: 85%;
    padding: 0.4rem 0.8rem;
    border-radius: 12px;
    font-size: 0.88rem;
    line-height: 1.5;
    animation: fade-in 0.25s ease;
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
    font-size: 0.65rem;
    opacity: 0.6;
    display: block;
    margin-bottom: 0.1rem;
  }
  .hrsi-box .hrsi-msgs .empty-hrsi {
    color: rgba(255,255,255,0.3);
    font-size: 0.85rem;
    text-align: center;
    padding: 2rem 0;
  }
  .hrsi-box .hrsi-input-row {
    display: flex;
    gap: 0.5rem;
    padding: 0.5rem 0.8rem;
    border-top: 1px solid rgba(255,255,255,0.06);
    background: #1a1a2e;
    flex-shrink: 0;
  }
  .hrsi-box .hrsi-input-row input {
    flex: 1;
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 20px;
    padding: 0.4rem 1rem;
    font-size: 0.85rem;
    outline: none;
    background: #0f0f1f;
    color: #eee;
    transition: var(--transition);
  }
  .hrsi-box .hrsi-input-row input:focus {
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(76, 110, 245, 0.15);
  }
  .hrsi-box .hrsi-input-row input::placeholder {
    color: #666;
  }
  .hrsi-box .hrsi-input-row button {
    background: var(--primary);
    color: #fff;
    border: none;
    border-radius: 20px;
    padding: 0.4rem 1rem;
    font-weight: 500;
    font-size: 0.8rem;
    cursor: pointer;
    transition: var(--transition);
  }
  .hrsi-box .hrsi-input-row button:hover {
    background: var(--primary-dark);
  }
  .hrsi-box .hrsi-input-row button:disabled {
    opacity: 0.4;
    cursor: not-allowed;
  }

  /* ===== 响应式微调 ===== */
  @media (max-width: 640px) {
    .page-wrapper {
      padding: 1rem 0.8rem 3rem;
    }
    .profile-card {
      padding: 1.2rem 1.2rem;
      gap: 1.2rem;
    }
    .profile-avatar {
      width: 80px;
      height: 80px;
      font-size: 2rem;
    }
    .profile-info h1 {
      font-size: 1.4rem;
    }
    .section-card {
      padding: 1.2rem 1rem;
    }
    .player-main {
      gap: 0.8rem;
    }
    .player-cover {
      width: 64px;
      height: 64px;
      font-size: 1.6rem;
    }
    .player-controls button {
      width: 32px;
      height: 32px;
      font-size: 1.1rem;
    }
    .player-controls button.play-btn {
      width: 38px;
      height: 38px;
      font-size: 1rem;
    }
    .player-volume input[type="range"] {
      width: 40px;
    }
    .hrsi-box {
      width: calc(100vw - 32px);
      right: 16px;
      bottom: 80px;
      height: 400px;
    }
    .explore-btn {
      padding: 0.6rem 1.4rem;
      font-size: 0.9rem;
    }
    .playlist-header .btn-group {
      gap: 0.3rem;
    }
    .playlist-header .add-btn {
      font-size: 0.7rem;
      padding: 0.1rem 0.6rem;
    }
    .chat-messages .msg .avatar {
      width: 22px;
      height: 22px;
      font-size: 0.6rem;
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
    background: #ccc;
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

  <!-- ====== 1. 个人卡片（头像修复） ====== -->
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

  <!-- ====== 2. 音乐播放器（纯音乐，免版权） ====== -->
  <div class="section-card">
    <div class="card-title">🎵 音乐播放器 · 纯音乐</div>
    <div class="card-sub">内置无版权背景音乐，稳定可播。您也可以添加自己的网易云ID或URL</div>

    <div class="player-wrap">
      <!-- 主控制区 -->
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
              <input type="range" id="volumeBar" min="0" max="1" step="0.01" value="0.8" oninput="setVolume(this.value)">
            </div>
          </div>
        </div>
      </div>

      <!-- 播放列表 -->
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
      <!-- 聊天室 -->
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

      <!-- 留言板 (Giscus) -->
      <div style="display:flex;flex-direction:column;gap:0.3rem;">
        <div style="font-weight:500;font-size:0.95rem;color:var(--text-secondary);">📝 留言板</div>
        <div style="flex:1;min-height:280px;border-radius:var(--radius-sm);overflow:hidden;background:#fafbff;padding:0.2rem;">
          <div class="giscus"></div>
        </div>
        <div style="font-size:0.78rem;color:var(--text-muted);margin-top:0.2rem;">
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

<!-- ===== 音乐播放器脚本（修复稳定播放） ===== -->
<script>
  (function() {
    'use strict';

    // ---------- 默认歌单（SoundHelix 免费测试曲，无版权） ----------
    const defaultSongs = [
      { title: 'SoundHelix Song 1', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3' },
      { title: 'SoundHelix Song 2', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3' },
      { title: 'SoundHelix Song 3', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3' },
      { title: 'SoundHelix Song 4', artist: 'SoundHelix', url: 'https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3' },
    ];

    let playlist = [];
    let currentIndex = 0;
    let isPlaying = false;
    let isDragging = false;

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

    // ---------- 工具函数 ----------
    function formatTime(sec) {
      if (!sec || isNaN(sec)) return '0:00';
      const m = Math.floor(sec / 60);
      const s = Math.floor(sec % 60);
      return m + ':' + (s < 10 ? '0' : '') + s;
    }

    // ---------- 加载播放列表 ----------
    function loadPlaylist() {
      try {
        const saved = localStorage.getItem('hrsi_playlist');
        if (saved) {
          const parsed = JSON.parse(saved);
          if (Array.isArray(parsed) && parsed.length) {
            playlist = parsed;
            return;
          }
        }
      } catch (_) { /* ignore */ }
      playlist = JSON.parse(JSON.stringify(defaultSongs));
      savePlaylist();
    }

    function savePlaylist() {
      try {
        localStorage.setItem('hrsi_playlist', JSON.stringify(playlist));
      } catch (_) { /* ignore */ }
    }

    // ---------- 渲染播放列表 ----------
    function renderPlaylist() {
      playlistContainer.innerHTML = '';
      if (!playlist.length) {
        playlistContainer.innerHTML = '<div class="playlist-empty">暂无歌曲，点击添加</div>';
        playlistCount.textContent = '0';
        return;
      }
      playlistCount.textContent = playlist.length;
      playlist.forEach((song, idx) => {
        const div = document.createElement('div');
        div.className = 'playlist-item' + (idx === currentIndex ? ' active' : '');
        div.innerHTML = `
          <span>${song.title || '未命名'} — ${song.artist || '未知'}</span>
          <button class="del-btn" onclick="removeSong(${idx})" title="移除">✕</button>
        `;
        div.addEventListener('click', () => playSong(idx));
        playlistContainer.appendChild(div);
      });
    }

    // ---------- 播放控制 ----------
    function playSong(index) {
      if (index < 0 || index >= playlist.length) return;
      currentIndex = index;
      const song = playlist[index];
      if (!song || !song.url) return;
      audio.src = song.url;
      audio.load();
      audio.volume = parseFloat(volumeBar.value) || 0.8;
      songTitle.textContent = song.title || '未命名';
      songArtist.textContent = song.artist || '未知';
      playerCover.textContent = '🎵';
      playerCover.classList.remove('loading');
      audio.play().then(() => {
        isPlaying = true;
        playBtn.textContent = '⏸';
        renderPlaylist();
      }).catch(() => {
        console.warn('播放失败，尝试下一首');
        playerCover.textContent = '⚠️';
        playerCover.classList.add('loading');
        setTimeout(() => nextSong(), 1500);
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
        if (index >= playlist.length) {
          currentIndex = playlist.length - 1;
        }
        playSong(currentIndex);
      } else if (index < currentIndex) {
        currentIndex--;
      }
      renderPlaylist();
    }

    // ---------- 添加歌曲（URL） ----------
    function addSongByURL() {
      const url = prompt('请输入音乐文件的 URL（mp3 / ogg / wav）：');
      if (!url) return;
      const title = prompt('请输入歌曲名称：') || '未命名';
      const artist = prompt('请输入艺术家名称：') || '未知';
      playlist.push({ title, artist, url });
      savePlaylist();
      renderPlaylist();
      if (playlist.length === 1) {
        playSong(0);
      } else {
        const idx = playlist.length - 1;
        const items = playlistContainer.querySelectorAll('.playlist-item');
        if (items[idx]) items[idx].classList.add('active');
      }
    }

    // ---------- 添加网易云歌曲（通过ID） ----------
    function addNeteaseSong() {
      const id = prompt('请输入网易云歌曲 ID（例如 186016 对应《晴天》）：');
      if (!id) return;
      const cleanId = id.trim();
      if (!/^\d+$/.test(cleanId)) {
        alert('请输入数字ID');
        return;
      }
      const url = `https://music.163.com/song/media/outer/url?id=${cleanId}.mp3`;
      const title = prompt('请输入歌曲名称（可选）：') || `网易云歌曲 ${cleanId}`;
      const artist = prompt('请输入艺术家名称（可选）：') || '未知';
      playlist.push({ title, artist, url });
      savePlaylist();
      renderPlaylist();
      if (playlist.length === 1) {
        playSong(0);
      } else {
        const idx = playlist.length - 1;
        const items = playlistContainer.querySelectorAll('.playlist-item');
        if (items[idx]) items[idx].classList.add('active');
      }
    }

    // ---------- 进度 & 音量 ----------
    function seekProgress(val) {
      if (!audio.duration || isNaN(audio.duration)) return;
      const time = (val / 100) * audio.duration;
      audio.currentTime = time;
      currentTimeEl.textContent = formatTime(time);
    }

    function setVolume(val) {
      audio.volume = parseFloat(val);
    }

    // ---------- 事件绑定 ----------
    audio.addEventListener('timeupdate', () => {
      if (!isDragging && audio.duration) {
        const pct = (audio.currentTime / audio.duration) * 100;
        progressBar.value = pct;
        currentTimeEl.textContent = formatTime(audio.currentTime);
      }
    });

    audio.addEventListener('loadedmetadata', () => {
      totalTimeEl.textContent = formatTime(audio.duration);
      progressBar.value = 0;
    });

    audio.addEventListener('ended', () => {
      nextSong();
    });

    audio.addEventListener('error', () => {
      console.warn('音频加载错误，尝试下一首');
      playerCover.textContent = '⚠️';
      playerCover.classList.add('loading');
      setTimeout(() => nextSong(), 1200);
    });

    audio.addEventListener('canplay', () => {
      playerCover.classList.remove('loading');
      playerCover.textContent = '🎵';
    });

    progressBar.addEventListener('mousedown', () => { isDragging = true; });
    progressBar.addEventListener('mouseup', () => { isDragging = false; });
    progressBar.addEventListener('touchstart', () => { isDragging = true; });
    progressBar.addEventListener('touchend', () => { isDragging = false; });

    // ---------- 暴露全局 ----------
    window.playSong = playSong;
    window.togglePlay = togglePlay;
    window.nextSong = nextSong;
    window.prevSong = prevSong;
    window.removeSong = removeSong;
    window.addSongByURL = addSongByURL;
    window.addNeteaseSong = addNeteaseSong;
    window.seekProgress = seekProgress;
    window.setVolume = setVolume;

    // ---------- 初始化 ----------
    loadPlaylist();
    renderPlaylist();
    if (playlist.length) {
      playSong(0);
    } else {
      playlist = JSON.parse(JSON.stringify(defaultSongs));
      savePlaylist();
      renderPlaylist();
      if (playlist.length) playSong(0);
    }

    console.log('🎵 播放器已加载，歌单数量:', playlist.length);
  })();
</script>

<!-- ===== 聊天室脚本 (localStorage 同步 + 头像) ===== -->
<script>
  (function() {
    'use strict';

    const STORAGE_KEY = 'hrsi_chat_messages';
    const NAME_KEY = 'hrsi_chat_username';
    const MAX_MSGS = 100;

    let username = localStorage.getItem(NAME_KEY) || '访客_' + Math.floor(Math.random() * 1000);
    let messages = [];

    const chatMessages = document.getElementById('chatMessages');
    const chatInput = document.getElementById('chatInput');

    // ---------- 加载消息 ----------
    function loadMessages() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        if (raw) {
          const parsed = JSON.parse(raw);
          if (Array.isArray(parsed)) {
            messages = parsed.slice(-MAX_MSGS);
            return;
          }
        }
      } catch (_) { /* ignore */ }
      messages = [];
    }

    function saveMessages() {
      try {
        localStorage.setItem(STORAGE_KEY, JSON.stringify(messages.slice(-MAX_MSGS)));
      } catch (_) { /* ignore */ }
    }

    // ---------- 获取用户首字母和颜色 ----------
    function getUserAvatar(name) {
      const initial = name.charAt(0).toUpperCase() || '?';
      const colors = ['#4c6ef5', '#f59f00', '#e67700', '#d6336c', '#20c997', '#6f42c1', '#0d6efd', '#fd7e14'];
      const index = name.length % colors.length;
      return { initial, color: colors[index] };
    }

    // ---------- 渲染 ----------
    function renderChat() {
      chatMessages.innerHTML = '';
      if (!messages.length) {
        chatMessages.innerHTML = '<div class="empty-chat">还没有消息，来说点什么吧 👋</div>';
        return;
      }
      messages.forEach(msg => {
        const div = document.createElement('div');
        div.className = 'msg ' + (msg.name === username ? 'self' : 'other');
        const avatarInfo = getUserAvatar(msg.name);
        const timeStr = msg.time ? new Date(msg.time).toLocaleTimeString('zh-CN', { hour: '2-digit', minute: '2-digit' }) : '';
        div.innerHTML = `
          <div class="avatar" style="background:${avatarInfo.color}">${avatarInfo.initial}</div>
          <div class="content">
            <span class="name">${msg.name || '匿名'}</span>
            ${msg.text}
            <span class="time">${timeStr}</span>
          </div>
        `;
        chatMessages.appendChild(div);
      });
      chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    // ---------- 发送消息 ----------
    function sendChat() {
      const text = chatInput.value.trim();
      if (!text) return;
      const msg = {
        name: username,
        text: text,
        time: Date.now(),
      };
      messages.push(msg);
      saveMessages();
      renderChat();
      chatInput.value = '';
      try {
        localStorage.setItem(STORAGE_KEY + '_trigger', Date.now().toString());
      } catch (_) { /* ignore */ }
    }

    // ---------- 监听其他标签页 ----------
    window.addEventListener('storage', (e) => {
      if (e.key === STORAGE_KEY || e.key === STORAGE_KEY + '_trigger') {
        const oldLen = messages.length;
        loadMessages();
        if (messages.length !== oldLen) {
          renderChat();
        }
      }
    });

    // ---------- 初始化 ----------
    loadMessages();
    renderChat();

    if (!localStorage.getItem(NAME_KEY)) {
      const name = prompt('👋 欢迎来到聊天室！请输入你的昵称：', username);
      if (name && name.trim()) {
        username = name.trim();
        localStorage.setItem(NAME_KEY, username);
      }
    } else {
      username = localStorage.getItem(NAME_KEY);
    }

    window.sendChat = sendChat;
    window.chatInput = chatInput;

    console.log('💬 聊天室已加载，当前用户:', username);
  })();
</script>

<!-- ===== HRSI 聊天脚本 ===== -->
<script>
  (function() {
    'use strict';

    const box = document.getElementById('hrsiBox');
    const msgs = document.getElementById('hrsiMsgs');
    const input = document.getElementById('hrsiInput');
    const sendBtn = document.getElementById('hrsiSendBtn');
    let isOpen = false;

    window.toggleHRSI = function() {
      isOpen = !isOpen;
      box.classList.toggle('open', isOpen);
      if (isOpen) {
        input.focus();
      }
    };

    window.sendHRSI = async function() {
      const text = input.value.trim();
      if (!text) return;
      input.value = '';
      sendBtn.disabled = true;
      sendBtn.textContent = '⏳';

      addMsg(text, 'user');

      try {
        const res = await fetch('https://hrsi-api.hrsi.cc.cd/api/generate', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({
            model: 'hrsi-model',
            prompt: `用户问："${text}"\n\n用 HRSI 的身份（12岁技术建造者，中二自信，好燃 So Intense！）简短回答：`,
            stream: false
          })
        });
        if (!res.ok) throw new Error('API 响应错误');
        const data = await res.json();
        const reply = data.response || '🤖 收到！但我暂时想不出更好的回答～';
        addMsg(reply, 'bot');
      } catch (e) {
        console.warn('HRSI API 错误:', e);
        addMsg('😅 HRSI 不在线，稍后再试！或者发邮件给站长/检查网络～', 'bot');
      }

      sendBtn.disabled = false;
      sendBtn.textContent = '发送';
    };

    function addMsg(text, type) {
      const empty = msgs.querySelector('.empty-hrsi');
      if (empty) empty.remove();

      const div = document.createElement('div');
      div.className = 'msg ' + (type === 'user' ? 'user' : 'bot');
      if (type === 'bot') {
        div.innerHTML = `<span class="label">🤖 HRSI</span>${text}`;
      } else {
        div.textContent = text;
      }
      msgs.appendChild(div);
      msgs.scrollTop = msgs.scrollHeight;
    }

    input.addEventListener('keydown', (e) => {
      if (e.key === 'Enter') {
        e.preventDefault();
        window.sendHRSI();
      }
    });

    console.log('🤖 HRSI 助手已加载');
  })();
</script>

<!-- ===== 头像占位增强 ===== -->
<script>
  document.addEventListener('DOMContentLoaded', function() {
    const img = document.querySelector('.profile-avatar');
    const fallback = document.querySelector('.fallback-avatar');
    if (img && img.complete && img.naturalWidth === 0) {
      img.style.display = 'none';
      fallback.style.display = 'flex';
    }
  });
</script>
