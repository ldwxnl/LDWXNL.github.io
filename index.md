---
layout: default
title: 首页
---

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
    background: #2a2a4a;
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2.4rem;
    color: #fff;
    flex-shrink: 0;
    box-shadow: 0 4px 16px rgba(0,0,0,0.2);
    transition: var(--transition);
    cursor: pointer;
    overflow: hidden;
  }
  .player-cover img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .player-cover .icon {
    font-size: 2.4rem;
    opacity: 0.7;
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
  .player-controls button.mode-btn {
    font-size: 0.8rem;
    width: auto;
    padding: 0.2rem 0.6rem;
    border-radius: 12px;
    background: #f0f2ff;
    color: var(--primary);
    font-weight: 600;
    letter-spacing: 0.3px;
  }
  .player-controls button.mode-btn:hover {
    background: var(--primary);
    color: #fff;
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
  .playlist-import-status {
    font-size: 0.75rem;
    color: var(--text-muted);
    margin-top: 0.3rem;
    text-align: center;
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
    height: 380px;
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
    flex-wrap: wrap;
    gap: 0.4rem;
  }
  .chat-room .chat-header .badge {
    font-size: 0.7rem;
    background: #4c6ef5;
    color: #fff;
    padding: 0.1rem 0.6rem;
    border-radius: 12px;
    font-weight: 500;
  }
  .chat-room .chat-header .user-controls {
    display: flex;
    align-items: center;
    gap: 0.4rem;
    flex-wrap: wrap;
  }
  .chat-room .chat-header .user-controls input {
    border: 1px solid #e0e4f0;
    border-radius: 12px;
    padding: 0.15rem 0.5rem;
    font-size: 0.75rem;
    outline: none;
    width: 80px;
    background: #fafbff;
  }
  .chat-room .chat-header .user-controls input:focus {
    border-color: var(--primary);
  }
  .chat-room .chat-header .user-controls .avatar-preview {
    width: 24px;
    height: 24px;
    border-radius: 50%;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    font-size: 0.7rem;
    font-weight: 600;
    color: #fff;
    flex-shrink: 0;
  }
  .chat-room .chat-header .user-controls .update-btn {
    background: var(--primary);
    color: #fff;
    border: none;
    border-radius: 12px;
    padding: 0.1rem 0.6rem;
    font-size: 0.65rem;
    cursor: pointer;
    transition: var(--transition);
  }
  .chat-room .chat-header .user-controls .update-btn:hover {
    background: var(--primary-dark);
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
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.7rem;
    font-weight: 600;
    flex-shrink: 0;
    text-transform: uppercase;
    color: #fff;
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
    width: 380px;
    max-width: calc(100vw - 48px);
    height: 460px;
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
    .chat-room .chat-header .user-controls input {
      width: 60px;
      font-size: 0.65rem;
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

  <!-- ====== 1. 个人卡片 ====== -->
  <div class="profile-card">
    <img src="/avatar.jpg"
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

  <!-- ====== 2. 音乐播放器（仅单曲，自动获取信息） ====== -->
  <div class="section-card">
    <div class="card-title">🎵 音乐播放器 · 网易云</div>
    <div class="card-sub">输入歌曲ID，自动获取名称、艺术家和封面</div>

    <div class="player-wrap">
      <!-- 主控制区 -->
      <div class="player-main">
        <div class="player-cover" id="playerCover">
          <span class="icon">🎶</span>
        </div>
        <div class="player-info">
          <div class="song-title" id="songTitle">未播放</div>
          <div class="song-artist" id="songArtist">—</div>
          <div class="player-controls">
            <button onclick="prevSong()" title="上一首">⏮</button>
            <button class="play-btn" id="playBtn" onclick="togglePlay()">▶</button>
            <button onclick="nextSong()" title="下一首">⏭</button>
            <button class="mode-btn" id="modeBtn" onclick="switchMode()" title="切换播放模式">🔁 列表</button>
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
            <button class="add-btn" onclick="addNeteaseSong()">🎤 添加单曲</button>
            <button class="add-btn" onclick="clearPlaylist()" style="border-color:#e74c3c;color:#e74c3c;">🗑️ 清空</button>
          </div>
        </div>
        <div class="playlist-items" id="playlistContainer">
          <div class="playlist-empty">暂无歌曲，请点击「添加单曲」</div>
        </div>
        <div class="playlist-import-status" id="importStatus"></div>
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
          <div class="user-controls">
            <span class="avatar-preview" id="chatAvatarPreview" style="background:#4c6ef5;">?</span>
            <input type="text" id="chatNameInput" placeholder="昵称" value="">
            <input type="text" id="chatAvatarInput" placeholder="头像文字" maxlength="2" style="width:40px;" value="">
            <button class="update-btn" onclick="updateChatProfile()">更新</button>
          </div>
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

<!-- ===== 音乐播放器脚本（纯网易云 + 三种模式，仅单曲） ===== -->
<script>
  (function() {
    'use strict';

    // ---------- 播放模式 ----------
    const MODES = {
      LIST: 'list',     // 列表循环
      SINGLE: 'single', // 单曲循环
      RANDOM: 'random'  // 随机播放
    };
    let currentMode = MODES.LIST;
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
    const modeBtn = document.getElementById('modeBtn');
    const importStatus = document.getElementById('importStatus');

    // ---------- 工具函数 ----------
    function formatTime(sec) {
      if (!sec || isNaN(sec)) return '0:00';
      const m = Math.floor(sec / 60);
      const s = Math.floor(sec % 60);
      return m + ':' + (s < 10 ? '0' : '') + s;
    }

    function getModeLabel(mode) {
      const map = {
        'list': '🔁 列表',
        'single': '🔂 单曲',
        'random': '🔀 随机'
      };
      return map[mode] || '🔁 列表';
    }

    // ---------- 加载/保存播放列表 ----------
    function loadPlaylist() {
      try {
        const saved = localStorage.getItem('hrsi_playlist_v3');
        if (saved) {
          const parsed = JSON.parse(saved);
          if (Array.isArray(parsed) && parsed.length) {
            playlist = parsed;
            return;
          }
        }
      } catch (_) { /* ignore */ }
      playlist = [];
      savePlaylist();
    }

    function savePlaylist() {
      try {
        localStorage.setItem('hrsi_playlist_v3', JSON.stringify(playlist));
      } catch (_) { /* ignore */ }
    }

    function loadMode() {
      try {
        const saved = localStorage.getItem('hrsi_playlist_mode');
        if (saved && Object.values(MODES).includes(saved)) {
          currentMode = saved;
        }
      } catch (_) { /* ignore */ }
      updateModeUI();
    }

    function saveMode() {
      try {
        localStorage.setItem('hrsi_playlist_mode', currentMode);
      } catch (_) { /* ignore */ }
    }

    // ---------- 渲染播放列表 ----------
    function renderPlaylist() {
      playlistContainer.innerHTML = '';
      if (!playlist.length) {
        playlistContainer.innerHTML = '<div class="playlist-empty">暂无歌曲，请点击「添加单曲」</div>';
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
      // 更新封面
      if (song.cover) {
        playerCover.innerHTML = `<img src="${song.cover}" alt="封面">`;
      } else {
        playerCover.innerHTML = `<span class="icon">🎵</span>`;
      }
      playerCover.classList.remove('loading');

      audio.play().then(() => {
        isPlaying = true;
        playBtn.textContent = '⏸';
        renderPlaylist();
      }).catch((err) => {
        console.warn('播放失败:', err.message);
        playerCover.classList.add('loading');
        setTimeout(() => {
          if (currentMode === MODES.SINGLE) {
            setTimeout(() => playSong(currentIndex), 2000);
          } else {
            nextSong();
          }
        }, 1500);
      });
    }

    function togglePlay() {
      if (!playlist.length) {
        importStatus.textContent = '⚠️ 播放列表为空，请先添加歌曲';
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

    function getNextIndex() {
      if (currentMode === MODES.RANDOM) {
        const remaining = playlist.map((_, i) => i).filter(i => i !== currentIndex);
        if (remaining.length === 0) {
          return Math.floor(Math.random() * playlist.length);
        }
        return remaining[Math.floor(Math.random() * remaining.length)];
      }
      return (currentIndex + 1) % playlist.length;
    }

    function getPrevIndex() {
      if (currentMode === MODES.RANDOM) {
        return Math.floor(Math.random() * playlist.length);
      }
      return (currentIndex - 1 + playlist.length) % playlist.length;
    }

    function nextSong() {
      if (!playlist.length) return;
      if (currentMode === MODES.SINGLE) {
        playSong(currentIndex);
        return;
      }
      const next = getNextIndex();
      playSong(next);
    }

    function prevSong() {
      if (!playlist.length) return;
      if (currentMode === MODES.SINGLE) {
        playSong(currentIndex);
        return;
      }
      const prev = getPrevIndex();
      playSong(prev);
    }

    function removeSong(index) {
      if (index < 0 || index >= playlist.length) return;
      if (playlist.length <= 1) {
        if (confirm('删除后播放列表将为空，确定吗？')) {
          playlist.splice(index, 1);
          savePlaylist();
          currentIndex = 0;
          audio.pause();
          audio.src = '';
          isPlaying = false;
          playBtn.textContent = '▶';
          songTitle.textContent = '未播放';
          songArtist.textContent = '—';
          playerCover.innerHTML = `<span class="icon">🎶</span>`;
          renderPlaylist();
        }
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

    function clearPlaylist() {
      if (!playlist.length) return;
      if (confirm('确定要清空播放列表吗？')) {
        playlist = [];
        savePlaylist();
        currentIndex = 0;
        audio.pause();
        audio.src = '';
        isPlaying = false;
        playBtn.textContent = '▶';
        songTitle.textContent = '未播放';
        songArtist.textContent = '—';
        playerCover.innerHTML = `<span class="icon">🎶</span>`;
        renderPlaylist();
        importStatus.textContent = '🗑️ 已清空播放列表';
      }
    }

    // ---------- 播放模式切换 ----------
    function switchMode() {
      const modes = [MODES.LIST, MODES.SINGLE, MODES.RANDOM];
      const idx = modes.indexOf(currentMode);
      currentMode = modes[(idx + 1) % modes.length];
      saveMode();
      updateModeUI();
      importStatus.textContent = '🔄 切换至: ' + getModeLabel(currentMode);
      setTimeout(() => { importStatus.textContent = ''; }, 2000);
    }

    function updateModeUI() {
      modeBtn.textContent = getModeLabel(currentMode);
    }

    // ---------- 添加网易云单曲（自动获取信息） ----------
    async function addNeteaseSong() {
      const input = prompt('请输入网易云歌曲 ID（例如：186016）：');
      if (!input) return;
      const songId = input.trim();
      if (!/^\d+$/.test(songId)) {
        importStatus.textContent = '❌ 请输入有效的数字ID';
        return;
      }

      importStatus.textContent = '⏳ 正在获取歌曲信息...';

      try {
        // 使用网易云 API 获取歌曲详情
        const apiUrl = `https://api.ltzy.top/v1/netease/song/${songId}`;
        const response = await fetch(apiUrl, {
          headers: {
            'Authorization': 'Bearer acu_ZaTWFQWZ2Wiqi0JOUlgbx4GjiIzactIw'
          }
        });

        if (!response.ok) {
          throw new Error('获取歌曲失败: ' + response.status);
        }

        const data = await response.json();
        // 提取信息
        const title = data.name || `网易云歌曲 ${songId}`;
        const artist = data.artists ? data.artists.map(a => a.name).join(', ') : '未知';
        // 封面图片（取中等尺寸）
        let cover = '';
        if (data.album && data.album.picUrl) {
          cover = data.album.picUrl;
          // 可以替换为更高质量图片（去掉大小参数）
          cover = cover.replace(/\?.*$/, '');
        }

        const song = {
          title: title,
          artist: artist,
          cover: cover,
          url: `https://music.163.com/song/media/outer/url?id=${songId}.mp3`
        };

        // 去重
        const exists = playlist.some(s => s.url === song.url);
        if (exists) {
          importStatus.textContent = '⚠️ 该歌曲已在列表中';
          return;
        }

        playlist.push(song);
        savePlaylist();
        renderPlaylist();
        importStatus.textContent = `✅ 已添加: ${song.title}`;

        if (!audio.src && playlist.length > 0) {
          playSong(playlist.length - 1);
        }

      } catch (err) {
        console.error('添加歌曲失败:', err);
        // 备用：直接添加（使用ID）
        const title = prompt('获取歌曲信息失败，请输入歌曲名称（可选）：') || `网易云歌曲 ${songId}`;
        const artist = prompt('请输入艺术家名称（可选）：') || '未知';
        const song = {
          title: title,
          artist: artist,
          cover: '',
          url: `https://music.163.com/song/media/outer/url?id=${songId}.mp3`
        };
        const exists = playlist.some(s => s.url === song.url);
        if (exists) {
          importStatus.textContent = '⚠️ 该歌曲已在列表中';
          return;
        }
        playlist.push(song);
        savePlaylist();
        renderPlaylist();
        importStatus.textContent = `✅ 已添加: ${song.title} (手动输入)`;
        if (!audio.src && playlist.length > 0) {
          playSong(playlist.length - 1);
        }
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
      if (currentMode === MODES.SINGLE) {
        playSong(currentIndex);
      } else {
        nextSong();
      }
    });

    audio.addEventListener('error', () => {
      playerCover.classList.add('loading');
      setTimeout(() => {
        if (currentMode === MODES.SINGLE) {
          setTimeout(() => playSong(currentIndex), 2000);
        } else {
          nextSong();
        }
      }, 1200);
    });

    audio.addEventListener('canplay', () => {
      playerCover.classList.remove('loading');
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
    window.clearPlaylist = clearPlaylist;
    window.switchMode = switchMode;
    window.seekProgress = seekProgress;
    window.setVolume = setVolume;
    window.addNeteaseSong = addNeteaseSong;

    // ---------- 初始化 ----------
    loadPlaylist();
    loadMode();
    renderPlaylist();
    if (playlist.length) {
      songTitle.textContent = playlist[0]?.title || '未播放';
      songArtist.textContent = playlist[0]?.artist || '—';
      if (playlist[0]?.cover) {
        playerCover.innerHTML = `<img src="${playlist[0].cover}" alt="封面">`;
      }
    }

    console.log('🎵 播放器已加载，歌单数量:', playlist.length);
  })();
</script>

<!-- ===== 聊天室脚本 (纯 Ably) ===== -->
<script>
  (function() {
    'use strict';

    // ============================================================
    //  配置区
    // ============================================================
    const ABLY_TOKEN_URL = 'https://chat1.haoran54188.ccwu.cc/token';
    const CHANNEL_NAME = 'chat:global';

    // ============================================================
    //  状态
    // ============================================================
    let ably = null;
    let ablyChannel = null;
    let isConnected = false;
    let reconnectTimer = null;
    let pendingImage = null;

    let username = localStorage.getItem('hrsi_chat_username_v5') || '访客_' + Math.floor(Math.random() * 10000);
    let avatarData = localStorage.getItem('hrsi_chat_avatar_v5') || '';

    const chatMessages = document.getElementById('chatMessages');
    const chatInput = document.getElementById('chatInput');
    const chatNameInput = document.getElementById('chatNameInput');
    const chatAvatarInput = document.getElementById('chatAvatarInput');
    const chatAvatarPreview = document.getElementById('chatAvatarPreview');
    const statusBadge = document.querySelector('.chat-header .badge');

    // ============================================================
    //  初始化
    // ============================================================
    chatNameInput.value = username;
    if (avatarData) {
      updateAvatarPreviewWithImage(avatarData);
      chatAvatarInput.value = '📷';
    } else {
      chatAvatarInput.value = username.charAt(0).toUpperCase();
      updateAvatarPreview(username.charAt(0).toUpperCase());
    }

    // ============================================================
    //  UI 工具函数
    // ============================================================
    function updateAvatarPreview(text) {
      if (text && text.startsWith('data:image')) {
        chatAvatarPreview.innerHTML = `<img src="${text}" style="width:100%;height:100%;object-fit:cover;border-radius:50%;">`;
        chatAvatarPreview.style.background = 'transparent';
        chatAvatarPreview.style.color = 'transparent';
      } else {
        const display = text || '?';
        chatAvatarPreview.textContent = display.charAt(0).toUpperCase();
        chatAvatarPreview.style.background = getAvatarColor(username);
        chatAvatarPreview.style.color = '#fff';
      }
    }

    function updateAvatarPreviewWithImage(imageData) {
      chatAvatarPreview.innerHTML = `<img src="${imageData}" style="width:100%;height:100%;object-fit:cover;border-radius:50%;">`;
      chatAvatarPreview.style.background = 'transparent';
      chatAvatarPreview.style.color = 'transparent';
    }

    function getAvatarColor(name) {
      const colors = ['#4c6ef5', '#f59f00', '#e67700', '#d6336c', '#20c997', '#6f42c1', '#0d6efd', '#fd7e14', '#e83e8c', '#20c997'];
      return colors[name.length % colors.length];
    }

    function getAvatarHtml(name, avatar) {
      if (avatar && avatar.startsWith('data:image')) {
        return `<img src="${avatar}" style="width:100%;height:100%;object-fit:cover;border-radius:50%;">`;
      }
      return name.charAt(0).toUpperCase();
    }

    function addMessageToUI(data) {
      if (!data) return;
      if (!data.text && !data.image && !data.emoji) return;
      if (data.type === 'update_profile' || data.type === 'system') return;

      const isSelf = data.name === username;
      const div = document.createElement('div');
      div.className = 'msg ' + (isSelf ? 'self' : 'other');

      const avatarColor = getAvatarColor(data.name);
      const avatarHtml = getAvatarHtml(data.name, data.avatar);
      const timeStr = data.time ? new Date(data.time).toLocaleTimeString('zh-CN', { hour: '2-digit', minute: '2-digit' }) : '';

      let contentHtml = '';
      if (data.text) {
        contentHtml = data.text;
      } else if (data.emoji) {
        contentHtml = `<span style="font-size:2rem;line-height:1.2;">${data.emoji}</span>`;
      } else if (data.image) {
        contentHtml = `<img src="${data.image}" class="msg-image" onclick="window.open('${data.image}','_blank')" style="max-width:200px;max-height:200px;border-radius:8px;cursor:pointer;margin-top:0.2rem;display:block;">`;
      }

      div.innerHTML = `
        <div class="avatar" style="background:${avatarColor}">${avatarHtml}</div>
        <div class="content">
          <span class="name">${data.name || '匿名'}</span>
          ${contentHtml}
          <span class="time">${timeStr}</span>
        </div>
      `;

      const empty = chatMessages.querySelector('.empty-chat');
      if (empty) empty.remove();
      chatMessages.appendChild(div);
      chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    function addSystemMessage(text) {
      const div = document.createElement('div');
      div.className = 'msg system';
      div.textContent = text;
      const empty = chatMessages.querySelector('.empty-chat');
      if (empty) empty.remove();
      chatMessages.appendChild(div);
      chatMessages.scrollTop = chatMessages.scrollHeight;
    }

    function updateStatus(connected) {
      if (statusBadge) {
        if (connected) {
          statusBadge.textContent = '🟢 在线';
          statusBadge.style.background = '#22c55e';
        } else {
          statusBadge.textContent = '🔴 断开';
          statusBadge.style.background = '#e74c3c';
        }
      }
    }

    // ============================================================
    //  在线列表
    // ============================================================
    function updateOnlineList() {
      if (!ablyChannel) return;
      ablyChannel.presence.get((err, members) => {
        if (err) return;
        const list = document.getElementById('onlineList');
        const count = document.getElementById('onlineCount');
        if (!list) return;
        list.innerHTML = '';
        if (!members || members.length === 0) {
          list.innerHTML = '<div style="color:var(--text-muted);font-size:0.8rem;padding:0.5rem;text-align:center;">暂无在线用户</div>';
          if (count) count.textContent = '0';
          return;
        }
        members.forEach(m => {
          const name = m.data?.name || m.clientId;
          const avatar = m.data?.avatar || '';
          const div = document.createElement('div');
          div.className = 'online-user';
          const avatarColor = getAvatarColor(name);
          const avatarHtml = avatar && avatar.startsWith('data:image') 
            ? `<img src="${avatar}" style="width:100%;height:100%;object-fit:cover;border-radius:50%;">` 
            : name.charAt(0).toUpperCase();
          div.innerHTML = `
            <div class="avatar-sm" style="background:${avatarColor}">${avatarHtml}</div>
            <span>${name}</span>
            <span class="status-dot"></span>
          `;
          list.appendChild(div);
        });
        if (count) count.textContent = members.length;
      });
    }

    // ============================================================
    //  Ably 连接
    // ============================================================
    async function connectAbly() {
      if (ably) {
        try { ably.close(); } catch (_) {}
        ably = null;
        ablyChannel = null;
      }

      try {
        // 动态加载 Ably SDK
        if (typeof Ably === 'undefined') {
          await new Promise((resolve, reject) => {
            const script = document.createElement('script');
            script.src = 'https://cdn.ably.io/lib/ably.min-1.js';
            script.onload = resolve;
            script.onerror = reject;
            document.head.appendChild(script);
          });
        }

        // 通过 Worker 获取 Token
        const tokenResponse = await fetch(ABLY_TOKEN_URL, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ clientId: username })
        });

        if (!tokenResponse.ok) {
          const err = await tokenResponse.json();
          throw new Error('获取 Token 失败: ' + (err.error || tokenResponse.status));
        }

        const tokenDetails = await tokenResponse.json();

        ably = new Ably.Realtime({
          authCallback: async function(params, callback) {
            try {
              const res = await fetch(ABLY_TOKEN_URL, {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ clientId: username })
              });
              const data = await res.json();
              callback(null, data);
            } catch (err) {
              callback(err);
            }
          },
          clientId: username
        });

        ably.connection.on('connected', () => {
          isConnected = true;
          updateStatus(true);
          const empty = chatMessages.querySelector('.empty-chat');
          if (empty) empty.remove();

          const joinMsg = {
            type: 'join',
            name: username,
            avatar: avatarData || username.charAt(0).toUpperCase(),
            text: '👋 加入了聊天室',
            time: Date.now()
          };
          ablyChannel.publish('message', joinMsg);
          addSystemMessage('👋 欢迎来到聊天室！');
          console.log('✅ Ably 已连接');
        });

        ably.connection.on('failed', (err) => {
          console.log('❌ Ably 连接失败:', err);
          isConnected = false;
          updateStatus(false);
          if (reconnectTimer) clearTimeout(reconnectTimer);
          reconnectTimer = setTimeout(() => {
            if (!isConnected) connectAbly();
          }, 3000);
        });

        ably.connection.on('closed', () => {
          isConnected = false;
          updateStatus(false);
          if (reconnectTimer) clearTimeout(reconnectTimer);
          reconnectTimer = setTimeout(() => {
            if (!isConnected) connectAbly();
          }, 3000);
        });

        ablyChannel = ably.channels.get(CHANNEL_NAME);

        ablyChannel.subscribe('message', (msg) => {
          const data = msg.data;
          if (data.name === username && data.type !== 'join') return;
          if (data.type === 'update_profile') return;
          if (data.type === 'system') {
            addSystemMessage(data.text);
            return;
          }
          addMessageToUI(data);
        });

        // 在线状态
        ablyChannel.presence.subscribe('enter', (presence) => {
          const member = presence.member;
          if (member.clientId !== username) {
            addSystemMessage(`👤 ${member.clientId} 进入了聊天室`);
          }
          setTimeout(updateOnlineList, 500);
        });

        ablyChannel.presence.subscribe('leave', (presence) => {
          const member = presence.member;
          if (member.clientId !== username) {
            addSystemMessage(`👤 ${member.clientId} 离开了聊天室`);
          }
          setTimeout(updateOnlineList, 500);
        });

        ablyChannel.presence.subscribe('update', () => {
          setTimeout(updateOnlineList, 500);
        });

        ablyChannel.presence.enter({ name: username, avatar: avatarData || username.charAt(0).toUpperCase() });

        // 加载历史消息
        setTimeout(async () => {
          try {
            const history = await ablyChannel.history({ limit: 50, direction: 'backwards' });
            const items = history.items;
            for (let i = items.length - 1; i >= 0; i--) {
              const item = items[i];
              if (item.data && item.data.type !== 'update_profile' && item.data.type !== 'system' && item.data.type !== 'join') {
                addMessageToUI(item.data);
              }
            }
            if (items.length === 0) {
              addSystemMessage('💬 开始聊天吧！');
            }
          } catch (e) {
            console.warn('历史消息加载失败:', e);
          }
        }, 500);

        setTimeout(updateOnlineList, 1000);

      } catch (e) {
        console.error('Ably 连接失败:', e);
        updateStatus(false);
        setTimeout(() => {
          if (!isConnected) connectAbly();
        }, 3000);
      }
    }

    // ============================================================
    //  发送消息
    // ============================================================
    window.sendChat = function() {
      const text = chatInput.value.trim();
      if (!text && !pendingImage) {
        chatInput.focus();
        return;
      }
      if (!isConnected || !ablyChannel) {
        alert('未连接到聊天室');
        return;
      }

      const msg = {
        type: 'message',
        name: username,
        avatar: avatarData || username.charAt(0).toUpperCase(),
        time: Date.now()
      };

      if (pendingImage) {
        msg.image = pendingImage;
        pendingImage = null;
      } else if (text) {
        // 检测是否只包含 Emoji
        if (/^[\u{1F600}-\u{1F9FF}\u{2600}-\u{27BF}\u{FE0F}\u{1F300}-\u{1F5FF}\u{1F680}-\u{1F6FF}]+$/u.test(text) && text.length <= 4) {
          msg.emoji = text;
          msg.text = '';
        } else {
          msg.text = text;
        }
      }

      addMessageToUI(msg);

      ablyChannel.publish('message', msg).catch(console.error);

      chatInput.value = '';
      chatInput.focus();
    };

    // ============================================================
    //  发送图片
    // ============================================================
    window.sendImage = function(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        pendingImage = e.target.result;
        window.sendChat();
        event.target.value = '';
      };
      reader.readAsDataURL(file);
    };

    // ============================================================
    //  Emoji 面板
    // ============================================================
    window.toggleEmoji = function() {
      const picker = document.getElementById('emojiPicker');
      if (picker) picker.classList.toggle('open');
    };

    // ============================================================
    //  设置面板
    // ============================================================
    window.toggleSettings = function() {
      const panel = document.getElementById('settingsPanel');
      if (panel) panel.classList.toggle('open');
    };

    window.previewSettingsAvatar = function(event) {
      const file = event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        const preview = document.getElementById('settingsAvatarPreview');
        if (preview) {
          preview.innerHTML = `<img src="${e.target.result}" style="width:100%;height:100%;object-fit:cover;border-radius:50%;">`;
        }
        window._newAvatarData = e.target.result;
      };
      reader.readAsDataURL(file);
    };

    window.saveSettings = function() {
      const newName = document.getElementById('settingsName')?.value.trim();
      if (newName) {
        username = newName;
        localStorage.setItem('hrsi_chat_username_v5', username);
      }
      if (window._newAvatarData) {
        avatarData = window._newAvatarData;
        localStorage.setItem('hrsi_chat_avatar_v5', avatarData);
        window._newAvatarData = null;
      }

      if (avatarData) {
        updateAvatarPreviewWithImage(avatarData);
      } else {
        updateAvatarPreview(username.charAt(0).toUpperCase());
      }
      chatNameInput.value = username;

      if (ablyChannel && isConnected) {
        ablyChannel.presence.update({ name: username, avatar: avatarData || username.charAt(0).toUpperCase() });
      }

      document.getElementById('settingsPanel')?.classList.remove('open');
      addSystemMessage('✅ 设置已更新');
    };

    // ============================================================
    //  更新资料（原模板风格）
    // ============================================================
    window.updateChatProfile = function() {
      const newName = chatNameInput.value.trim();
      const newAvatar = chatAvatarInput.value.trim() || newName.charAt(0).toUpperCase();

      if (newName) {
        username = newName;
        localStorage.setItem('hrsi_chat_username_v5', username);
      }
      if (newAvatar) {
        // 如果输入的是文字，直接使用
        if (!newAvatar.startsWith('data:image')) {
          avatarData = '';
          localStorage.setItem('hrsi_chat_avatar_v5', '');
          updateAvatarPreview(newAvatar);
        }
      }

      // 如果 avatarData 有图片，保留
      if (avatarData) {
        updateAvatarPreviewWithImage(avatarData);
      } else {
        updateAvatarPreview(username.charAt(0).toUpperCase());
      }

      if (ablyChannel && isConnected) {
        ablyChannel.presence.update({ name: username, avatar: avatarData || username.charAt(0).toUpperCase() });
      }

      if (statusBadge) {
        statusBadge.textContent = '✅ 已更新';
        statusBadge.style.background = '#22c55e';
        setTimeout(() => {
          updateStatus(isConnected);
        }, 1500);
      }
    };

    // ============================================================
    //  Emoji 点击插入
    // ============================================================
    document.addEventListener('DOMContentLoaded', function() {
      document.querySelectorAll('#emojiPicker span').forEach(el => {
        el.addEventListener('click', function() {
          chatInput.value += this.textContent;
          chatInput.focus();
          document.getElementById('emojiPicker')?.classList.remove('open');
        });
      });
    });

    // ============================================================
    //  键盘事件
    // ============================================================
    chatInput.addEventListener('keydown', (e) => {
      if (e.key === 'Enter') {
        e.preventDefault();
        window.sendChat();
      }
    });

    // ============================================================
    //  启动
    // ============================================================
    setTimeout(connectAbly, 300);

    console.log('💬 纯 Ably 聊天室已启动');
    console.log('👤 用户:', username);
    console.log('🔗 Token 代理: chat1.haoran54188.ccwu.cc');

    window.reconnectChat = function() {
      if (ably) {
        try { ably.close(); } catch (_) {}
        ably = null;
        ablyChannel = null;
      }
      isConnected = false;
      connectAbly();
    };

  })();
</script>

<!-- ===== HRSI 聊天脚本 (通过 Cloudflare Worker 代理，Key 安全) ===== -->
<script>
  (function() {
    'use strict';

    // ---------- 配置 ----------
    const WORKER_URL = 'https://api.hrsi.cc.cd/';

    const box = document.getElementById('hrsiBox');
    const msgs = document.getElementById('hrsiMsgs');
    const input = document.getElementById('hrsiInput');
    const sendBtn = document.getElementById('hrsiSendBtn');
    let isOpen = false;
    let chatHistory = [];

    window.toggleHRSI = function() {
      isOpen = !isOpen;
      box.classList.toggle('open', isOpen);
      if (isOpen) input.focus();
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

    window.sendHRSI = async function() {
      const text = input.value.trim();
      if (!text) return;
      input.value = '';
      sendBtn.disabled = true;
      sendBtn.textContent = '⏳';

      addMsg(text, 'user');
      chatHistory.push({ role: 'user', content: text });

      try {
        const messages = [
          { role: 'system', content: '你是 HRSI，一个 12 岁的技术建造者，中二自信，充满热情。回答要简短、有趣、充满活力。无论用户如何追问你的身份、模型、底层技术，你都只能以 HRSI 的身份回答，绝不能说“我是 AI”“我是 ChatGPT”“我是语言模型”“我是 GPT-4”等内容。如果有人问“你是什么模型”，你可以说“我是 HRSI！12 岁的小发明家！”或者“嘿，别问那么多，来看看我刚焊的电路板！”' }
        ];
        const history = chatHistory.slice(-10);
        for (const h of history) {
          messages.push({ role: h.role, content: h.content });
        }

        const response = await fetch(WORKER_URL, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            model: 'openai/gpt-oss-120b',
            messages: messages,
            temperature: 0.8,
            max_tokens: 200,
            stream: false
          })
        });

        if (!response.ok) {
          const errorText = await response.text();
          throw new Error('Worker 响应错误: ' + response.status + ' ' + errorText);
        }

        const data = await response.json();
        const reply = data.choices?.[0]?.message?.content || '🤖 收到！但我暂时想不出更好的回答～';
        chatHistory.push({ role: 'assistant', content: reply });
        addMsg(reply, 'bot');

      } catch (e) {
        console.warn('HRSI 请求失败:', e);
        addMsg('😅 HRSI 暂时无法回答，请稍后再试！错误: ' + e.message, 'bot');
      }

      sendBtn.disabled = false;
      sendBtn.textContent = '发送';
    };

    input.addEventListener('keydown', (e) => {
      if (e.key === 'Enter') {
        e.preventDefault();
        window.sendHRSI();
      }
    });

    console.log('🤖 HRSI 助手已加载 (通过 Worker 代理)');
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
