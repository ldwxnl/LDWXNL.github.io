<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个性化音乐空间</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background-color: #0f0f1a;
            color: #f0f0f0;
            min-height: 100vh;
            overflow-x: hidden;
        }
        
        #particles-js {
            position: fixed;
            width: 100%;
            height: 100%;
            z-index: -1;
        }
        
        .container {
            display: flex;
            flex-wrap: wrap;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            min-height: 100vh;
        }
        
        /* 左侧个人资料区域 */
        .profile-section {
            flex: 1;
            min-width: 300px;
            padding: 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }
        
        .avatar-container {
            position: relative;
            width: 220px;
            height: 220px;
            margin-bottom: 30px;
        }
        
        .avatar {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
            border: 5px solid transparent;
            background: linear-gradient(45deg, #ff0080, #00ccff, #ff0080) border-box;
            box-shadow: 0 0 20px rgba(0, 204, 255, 0.5);
            animation: avatar-glow 4s infinite alternate;
        }
        
        @keyframes avatar-glow {
            0% { box-shadow: 0 0 20px rgba(0, 204, 255, 0.5); }
            100% { box-shadow: 0 0 30px rgba(255, 0, 128, 0.5), 0 0 40px rgba(0, 204, 255, 0.3); }
        }
        
        .profile-info {
            text-align: center;
            max-width: 400px;
        }
        
        .name {
            font-size: 2.2rem;
            margin-bottom: 10px;
            background: linear-gradient(to right, #ff0080, #00ccff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .title {
            font-size: 1.1rem;
            color: #aaa;
            margin-bottom: 20px;
        }
        
        .bio {
            line-height: 1.6;
            margin-bottom: 30px;
            color: #ccc;
        }
        
        .social-links {
            display: flex;
            gap: 15px;
        }
        
        .social-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            color: #00ccff;
            text-decoration: none;
            transition: all 0.3s ease;
        }
        
        .social-icon:hover {
            background: #00ccff;
            color: #0f0f1a;
            transform: translateY(-5px);
        }
        
        /* 右侧音乐播放器区域 */
        .music-section {
            flex: 1;
            min-width: 300px;
            padding: 30px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        
        .player-container {
            background: rgba(20, 20, 40, 0.7);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .player-title {
            font-size: 1.8rem;
            margin-bottom: 25px;
            text-align: center;
            color: #00ccff;
        }
        
        .album-art {
            width: 200px;
            height: 200px;
            border-radius: 10px;
            margin: 0 auto 25px;
            overflow: hidden;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
        }
        
        .album-cover {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .song-info {
            text-align: center;
            margin-bottom: 25px;
        }
        
        .song-title {
            font-size: 1.4rem;
            margin-bottom: 5px;
        }
        
        .artist {
            color: #aaa;
            font-size: 1rem;
        }
        
        .progress-area {
            margin-bottom: 25px;
        }
        
        .progress-bar {
            height: 6px;
            width: 100%;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            margin-bottom: 5px;
            cursor: pointer;
        }
        
        .progress {
            height: 100%;
            width: 0%;
            background: linear-gradient(to right, #ff0080, #00ccff);
            border-radius: 10px;
            position: relative;
        }
        
        .progress::after {
            content: '';
            position: absolute;
            height: 12px;
            width: 12px;
            border-radius: 50%;
            background: #fff;
            right: -5px;
            top: 50%;
            transform: translateY(-50%);
        }
        
        .timer {
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
            color: #aaa;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .control-btn {
            background: none;
            border: none;
            color: #f0f0f0;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .play-pause {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: linear-gradient(45deg, #ff0080, #00ccff);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.4rem;
        }
        
        .control-btn:hover {
            color: #00ccff;
            transform: scale(1.1);
        }
        
        .playlist {
            margin-top: 20px;
            max-height: 200px;
            overflow-y: auto;
        }
        
        .playlist-title {
            font-size: 1.2rem;
            margin-bottom: 10px;
            color: #aaa;
        }
        
        .playlist-item {
            padding: 10px;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .playlist-item:hover {
            background: rgba(255, 255, 255, 0.1);
        }
        
        .playlist-item.active {
            background: rgba(0, 204, 255, 0.2);
            color: #00ccff;
        }
        
        .playlist-item i {
            font-size: 0.9rem;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            
            .profile-section, .music-section {
                padding: 20px;
            }
            
            .avatar-container {
                width: 180px;
                height: 180px;
            }
            
            .name {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- 动态背景 -->
    <div id="particles-js"></div>
    
    <div class="container">
        <!-- 左侧：个人资料区域 -->
        <section class="profile-section">
            <div class="avatar-container">
                <img src="https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=500&q=80" alt="用户头像" class="avatar">
            </div>
            
            <div class="profile-info">
                <h1 class="name">元宝</h1>
                <p class="title">音乐爱好者 & 前端开发者</p>
                <p class="bio">热爱音乐、编程和创造美好的数字体验。这个网站是我个人音乐空间，分享我喜爱的音乐和心情。希望通过音乐连接每一个有趣的灵魂。</p>
                
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
                    <img src="https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=500&q=80" alt="专辑封面" class="album-cover">
                </div>
                
                <div class="song-info">
                    <h3 class="song-title">夜空中最亮的星</h3>
                    <p class="artist">逃跑计划</p>
                </div>
                
                <div class="progress-area">
                    <div class="progress-bar">
                        <div class="progress" id="progress"></div>
                    </div>
                    <div class="timer">
                        <span class="current-time" id="current-time">0:00</span>
                        <span class="duration" id="duration">0:00</span>
                    </div>
                </div>
                
                <div class="controls">
                    <button class="control-btn" id="prev-btn">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    <button class="control-btn" id="play-pause-btn">
                        <i class="fas fa-play"></i>
                    </button>
                    <button class="control-btn" id="next-btn">
                        <i class="fas fa-step-forward"></i>
                    </button>
                </div>
                
                <div class="playlist">
                    <h4 class="playlist-title">播放列表</h4>
                    <div class="playlist-item active" data-index="0">
                        <i class="fas fa-music"></i>
                        <span>夜空中最亮的星 - 逃跑计划</span>
                    </div>
                    <div class="playlist-item" data-index="1">
                        <i class="fas fa-music"></i>
                        <span>起风了 - 买辣椒也用券</span>
                    </div>
                    <div class="playlist-item" data-index="2">
                        <i class="fas fa-music"></i>
                        <span>光年之外 - G.E.M. 邓紫棋</span>
                    </div>
                    <div class="playlist-item" data-index="3">
                        <i class="fas fa-music"></i>
                        <span>平凡之路 - 朴树</span>
                    </div>
                </div>
            </div>
        </section>
    </div>
    
    <!-- 引入粒子背景库 -->
    <script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
    
    <script>
        // 初始化动态粒子背景
        document.addEventListener('DOMContentLoaded', function() {
            particlesJS("particles-js", {
                particles: {
                    number: { value: 80, density: { enable: true, value_area: 800 } },
                    color: { value: "#00ccff" },
                    shape: { type: "circle" },
                    opacity: { value: 0.5, random: true },
                    size: { value: 3, random: true },
                    line_linked: {
                        enable: true,
                        distance: 150,
                        color: "#ff0080",
                        opacity: 0.2,
                        width: 1
                    },
                    move: { enable: true, speed: 2 }
                },
                interactivity: {
                    detect_on: "canvas",
                    events: {
                        onhover: { enable: true, mode: "repulse" },
                        onclick: { enable: true, mode: "push" }
                    }
                }
            });
        });
        
        // 音乐播放器功能
        document.addEventListener('DOMContentLoaded', function() {
            const audioPlayer = new Audio();
            const playPauseBtn = document.getElementById('play-pause-btn');
            const prevBtn = document.getElementById('prev-btn');
            const nextBtn = document.getElementById('next-btn');
            const progressBar = document.getElementById('progress');
            const currentTimeEl = document.getElementById('current-time');
            const durationEl = document.getElementById('duration');
            const playlistItems = document.querySelectorAll('.playlist-item');
            const songTitle = document.querySelector('.song-title');
            const artist = document.querySelector('.artist');
            const albumCover = document.querySelector('.album-cover');
            
            // 音乐列表
            const musicList = [
                {
                    title: "夜空中最亮的星",
                    artist: "逃跑计划",
                    src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3",
                    cover: "https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80"
                },
                {
                    title: "起风了",
                    artist: "买辣椒也用券",
                    src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3",
                    cover: "https://images.unsplash.com/photo-1511379938547-c1f69419868d?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80"
                },
                {
                    title: "光年之外",
                    artist: "G.E.M. 邓紫棋",
                    src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3",
                    cover: "https://images.unsplash.com/photo-1518609878373-06d740f60d8b?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80"
                },
                {
                    title: "平凡之路",
                    artist: "朴树",
                    src: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3",
                    cover: "https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?ixlib=rb-4.0.3&auto=format&fit=crop&w=500&q=80"
                }
            ];
            
            let currentTrackIndex = 0;
            
            // 加载音乐
            function loadTrack(index) {
                const track = musicList[index];
                audioPlayer.src = track.src;
                songTitle.textContent = track.title;
                artist.textContent = track.artist;
                albumCover.src = track.cover;
                
                // 更新播放列表高亮
                playlistItems.forEach(item => item.classList.remove('active'));
                playlistItems[index].classList.add('active');
                
                // 如果音乐正在播放，继续播放
                if (!audioPlayer.paused) {
                    audioPlayer.play();
                }
            }
            
            // 播放/暂停音乐
            function togglePlayPause() {
                if (audioPlayer.paused) {
                    audioPlayer.play();
                    playPauseBtn.innerHTML = '<i class="fas fa-pause"></i>';
                } else {
                    audioPlayer.pause();
                    playPauseBtn.innerHTML = '<i class="fas fa-play"></i>';
                }
            }
            
            // 更新进度条
            function updateProgress(e) {
                const { currentTime, duration } = e.srcElement;
                const progressPercent = (currentTime / duration) * 100;
                progressBar.style.width = `${progressPercent}%`;
                
                // 更新时间显示
                const formatTime = (time) => {
                    const minutes = Math.floor(time / 60);
                    const seconds = Math.floor(time % 60);
                    return `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
                };
                
                currentTimeEl.textContent = formatTime(currentTime);
                
                if (!isNaN(duration)) {
                    durationEl.textContent = formatTime(duration);
                }
            }
            
            // 设置进度
            function setProgress(e) {
                const width = this.clientWidth;
                const clickX = e.offsetX;
                const duration = audioPlayer.duration;
                
                audioPlayer.currentTime = (clickX / width) * duration;
            }
            
            // 下一首
            function nextTrack() {
                currentTrackIndex = (currentTrackIndex + 1) % musicList.length;
                loadTrack(currentTrackIndex);
                playPauseBtn.innerHTML = '<i class="fas fa-pause"></i>';
                audioPlayer.play();
            }
            
            // 上一首
            function prevTrack() {
                currentTrackIndex = (currentTrackIndex - 1 + musicList.length) % musicList.length;
                loadTrack(currentTrackIndex);
                playPauseBtn.innerHTML = '<i class="fas fa-pause"></i>';
                audioPlayer.play();
            }
            
            // 事件监听
            playPauseBtn.addEventListener('click', togglePlayPause);
            prevBtn.addEventListener('click', prevTrack);
            nextBtn.addEventListener('click', nextTrack);
            audioPlayer.addEventListener('timeupdate', updateProgress);
            audioPlayer.addEventListener('ended', nextTrack);
            
            // 进度条点击事件
            const progressContainer = document.querySelector('.progress-bar');
            progressContainer.addEventListener('click', setProgress);
            
            // 播放列表点击事件
            playlistItems.forEach(item => {
                item.addEventListener('click', function() {
                    const index = parseInt(this.getAttribute('data-index'));
                    currentTrackIndex = index;
                    loadTrack(index);
                    playPauseBtn.innerHTML = '<i class="fas fa-pause"></i>';
                    audioPlayer.play();
                });
            });
            
            // 初始化加载第一首音乐
            loadTrack(0);
        });
    </script>
</body>
</html>
