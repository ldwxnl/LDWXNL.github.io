<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个性化音乐空间</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <!-- 动态背景 -->
    <div id="particles-js"></div>
    
    <div class="container">
        <!-- 左侧：个人资料区域 -->
        <section class="profile-section">
            <div class="avatar-container">
                <img src="https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=500&q=80" 
                     alt="用户头像" class="avatar" id="user-avatar">
                <div class="avatar-upload">
                    <label for="avatar-input" class="upload-btn">
                        <i class="fas fa-camera"></i>
                    </label>
                    <input type="file" id="avatar-input" accept="image/*" style="display: none;">
                </div>
            </div>
            
            <div class="profile-info">
                <h1 class="name" id="user-name">元宝</h1>
                <p class="title" id="user-title">音乐爱好者 & 前端开发者</p>
                <p class="bio" id="user-bio">热爱音乐、编程和创造美好的数字体验。这个网站是我个人音乐空间，分享我喜爱的音乐和心情。希望通过音乐连接每一个有趣的灵魂。</p>
                
                <div class="stats">
                    <div class="stat-item">
                        <span class="stat-number" id="total-plays">128</span>
                        <span class="stat-label">播放次数</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number" id="total-songs">24</span>
                        <span class="stat-label">收藏歌曲</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-number" id="total-time">36</span>
                        <span class="stat-label">收听小时</span>
                    </div>
                </div>
                
                <div class="social-links">
                    <a href="#" class="social-icon">
                        <i class="fab fa-github"></i>
                    </a>
                    <a href="#" class="social-icon">
                        <i class="fab fa-weixin"></i>
                    </a>
                    <a href="#" class="social-icon">
                        <i class="fab fa-qq"></i>
                    </a>
                    <a href="#" class="social-icon">
                        <i class="fab fa-spotify"></i>
                    </a>
                </div>
            </div>
        </section>
        
        <!-- 右侧：音乐播放器区域 -->
        <section class="music-section">
            <div class="player-container">
                <h2 class="player-title">我的音乐空间</h2>
                
                <div class="album-art">
                    <img src="https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80" 
                         alt="专辑封面" class="album-cover" id="album-cover">
                    <div class="vinyl-effect"></div>
                </div>
                
                <div class="song-info">
                    <h3 class="song-title" id="song-title">夜空中最亮的星</h3>
                    <p class="artist" id="song-artist">逃跑计划</p>
                </div>
                
                <div class="progress-area">
                    <div class="progress-bar" id="progress-bar">
                        <div class="progress" id="progress"></div>
                    </div>
                    <div class="timer">
                        <span class="current-time" id="current-time">0:00</span>
                        <span class="duration" id="duration">0:00</span>
                    </div>
                </div>
                
                <div class="controls">
                    <button class="control-btn" id="shuffle-btn" title="随机播放">
                        <i class="fas fa-random"></i>
                    </button>
                    <button class="control-btn" id="prev-btn" title="上一首">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    <button class="control-btn play-pause" id="play-pause-btn" title="播放/暂停">
                        <i class="fas fa-play"></i>
                    </button>
                    <button class="control-btn" id="next-btn" title="下一首">
                        <i class="fas fa-step-forward"></i>
                    </button>
                    <button class="control-btn" id="repeat-btn" title="单曲循环">
                        <i class="fas fa-redo"></i>
                    </button>
                </div>
                
                <div class="volume-control">
                    <i class="fas fa-volume-down volume-icon"></i>
                    <input type="range" min="0" max="100" value="80" class="volume-slider" id="volume-slider">
                    <i class="fas fa-volume-up volume-icon"></i>
                </div>
                
                <div class="playlist">
                    <div class="playlist-header">
                        <h4 class="playlist-title">播放列表</h4>
                        <span class="playlist-count" id="playlist-count">4 首歌曲</span>
                    </div>
                    <div class="playlist-items" id="playlist-items">
                        <!-- 播放列表将通过JavaScript动态生成 -->
                    </div>
                </div>
            </div>
        </section>
    </div>
    
    <!-- 引入粒子背景库 -->
    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    <!-- 引入自定义脚本 -->
    <script src="script.js"></script>
</body>
</html>
