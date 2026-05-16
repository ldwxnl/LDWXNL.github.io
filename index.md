<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hi I'm LELEO</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Microsoft YaHei', sans-serif;
            background-color: #000;
            color: #fff;
            overflow-x: hidden;
            position: relative;
        }
        
        /* 背景图层 */
        .background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: linear-gradient(135deg, #1e5799 0%,#2989d8 50%,#207cca 51%,#7db9e8 100%);
            overflow: hidden;
        }
        
        .water-effect {
            position: absolute;
            width: 100%;
            height: 100%;
            background: url('https://images.unsplash.com/photo-1505506874110-6a7a69069a08?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80') no-repeat center center;
            background-size: cover;
            opacity: 0.7;
            filter: blur(1px);
        }
        
        .bubbles {
            position: absolute;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }
        
        .bubble {
            position: absolute;
            border-radius: 50%;
            background-color: rgba(255, 255, 255, 0.5);
            animation: float 5s ease-in-out infinite;
        }
        
        @keyframes float {
            0% { transform: translateY(0) translateX(0); opacity: 0; }
            50% { opacity: 1; }
            100% { transform: translateY(-100vh) translateX(20px); opacity: 0; }
        }
        
        /* 主容器 */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }
        
        /* 头部区域 */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            padding: 20px 0;
            position: relative;
        }
        
        .avatar-container {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            overflow: hidden;
            border: 3px solid rgba(255, 255, 255, 0.5);
            box-shadow: 0 0 15px rgba(255, 255, 255, 0.3);
            position: relative;
        }
        
        .avatar {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .title {
            position: absolute;
            left: 50%;
            top: 20px;
            transform: translateX(-50%);
            font-size: 48px;
            font-weight: bold;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.8);
            font-family: 'Arial Black', sans-serif;
            letter-spacing: 2px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1, #ffbe0b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: gradient 10s ease infinite;
            background-size: 400% 400%;
        }
        
        @keyframes gradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        
        /* 时间和日期 */
        .time-date {
            position: absolute;
            right: 20px;
            top: 20px;
            background: rgba(0, 0, 0, 0.5);
            padding: 10px 15px;
            border-radius: 10px;
            text-align: right;
            backdrop-filter: blur(5px);
        }
        
        .time {
            font-size: 24px;
            font-weight: bold;
        }
        
        .date {
            font-size: 14px;
            opacity: 0.8;
        }
        
        /* 中间内容 */
        .content {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            gap: 20px;
            margin-top: 80px;
        }
        
        /* 左侧标签 */
        .tags-section {
            flex: 1;
            min-width: 250px;
            background: rgba(0, 0, 0, 0.4);
            padding: 20px;
            border-radius: 15px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .tags-title {
            font-size: 18px;
            margin-bottom: 15px;
            color: #fff;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            padding-bottom: 5px;
        }
        
        .tags-list {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }
        
        .tag {
            background: rgba(255, 255, 255, 0.1);
            padding: 5px 10px;
            border-radius: 15px;
            font-size: 12px;
            transition: all 0.3s ease;
        }
        
        .tag:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-2px);
        }
        
        /* 彩色饼图 */
        .color-wheel {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            background: conic-gradient(
                #ff6b6b 0deg 45deg,
                #ffbe0b 45deg 90deg,
                #45b7d1 90deg 135deg,
                #4ecdc4 135deg 180deg,
                #6a67ce 180deg 225deg,
                #c06c84 225deg 270deg,
                #6c5ce7 270deg 315deg,
                #00cec9 315deg 360deg
            );
            margin: 20px auto;
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.3);
        }
        
        /* 音乐播放器 */
        .music-player {
            flex: 1;
            min-width: 250px;
            background: rgba(0, 0, 0, 0.4);
            padding: 20px;
            border-radius: 15px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .music-title {
            font-size: 18px;
            margin-bottom: 15px;
            color: #fff;
            border-bottom: 1px solid rgba(255, 255, 255, 0.2);
            padding-bottom: 5px;
        }
        
        .player-controls {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-top: 15px;
        }
        
        .play-btn {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .play-btn:hover {
            background: rgba(255, 255, 255, 0.4);
        }
        
        .progress-container {
            flex: 1;
            height: 5px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 5px;
            position: relative;
            margin: 0 10px;
        }
        
        .progress {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #ff6b6b, #4ecdc4);
            border-radius: 5px;
            transition: width 0.1s linear;
        }
        
        /* 中间大图 */
        .main-image {
            flex: 2;
            min-width: 300px;
            position: relative;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.5);
        }
        
        .main-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        
        .quote {
            position: absolute;
            bottom: 20px;
            left: 20px;
            right: 20px;
            background: rgba(0, 0, 0, 0.6);
            padding: 10px 15px;
            border-radius: 10px;
            font-size: 16px;
            text-align: center;
            backdrop-filter: blur(5px);
        }
        
        /* 右侧功能区 */
        .right-section {
            flex: 1;
            min-width: 250px;
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .time-display {
            background: rgba(0, 0, 0, 0.4);
            padding: 20px;
            border-radius: 15px;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            text-align: center;
        }
        
        .time-circle {
            width: 150px;
            height: 150px;
            margin: 10px auto;
            position: relative;
        }
        
        .circle-bg {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 3px solid rgba(255, 255, 255, 0.1);
        }
        
        .circle-progress {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            border: 3px solid transparent;
            border-top: 3px solid #4ecdc4;
            border-right: 3px solid #4ecdc4;
            animation: spin 10s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        .circle-center {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 60%;
            height: 60%;
            background: rgba(0, 0, 0, 0.5);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 18px;
            font-weight: bold;
        }
        
        /* 底部卡片 */
        .cards {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            gap: 20px;
            margin-top: 20px;
        }
        
        .card {
            flex: 1;
            min-width: 200px;
            background: rgba(0, 0, 0, 00.4);
            border-radius: 15px;
            overflow: hidden;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: transform 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card img {
            width: 100%;
            height: 150px;
            object-fit: cover;
        }
        
        .card-content {
            padding: 15px;
        }
        
        .card-title {
            font-size: 16px;
            margin-bottom: 5px;
        }
        
        .card-desc {
            font-size: 12px;
            opacity: 0.8;
        }
        
        .card-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 10px;
        }
        
        .card-link {
            color: #4ecdc4;
            text-decoration: none;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .card-link:hover {
            text-decoration: underline;
        }
        
        /* 响应式设计 */
        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                align-items: center;
                text-align: center;
            }
            
            .title {
                position: static;
                transform: none;
                margin: 20px 0;
            }
            
            .time-date {
                position: static;
                margin-top: 20px;
            }
            
            .content {
                flex-direction: column;
            }
            
            .cards {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <!-- 背景 -->
    <div class="background">
        <div class="water-effect"></div>
        <div class="bubbles">
            <!-- 气泡将通过JS生成 -->
        </div>
    </div>
    
    <!-- 主容器 -->
    <div class="container">
        <!-- 头部区域 -->
        <div class="header">
            <div class="avatar-container">
                <img src="https://i.pravatar.cc/150?img=1" alt="Avatar" class="avatar">
            </div>
            
            <h1 class="title">HI, I'M LELEO</h1>
            
            <div class="time-date">
                <div class="time">16:21:59</div>
                <div class="date">2025年02月17日 星期一</div>
            </div>
        </div>
        
        <!-- 主要内容区 -->
        <div class="content">
            <!-- 左侧标签 -->
            <div class="tags-section">
                <h2 class="tags-title">Tags</h2>
                <div class="tags-list">
                    <div class="tag">乐观开朗</div>
                    <div class="tag">温柔体贴</div>
                    <div class="tag">酷酷亲切</div>
                    <div class="tag">冷静沉着</div>
                    <div class="tag">才是硬控</div>
                    <div class="tag">风趣幽默</div>
                    <div class="tag">端正不斜</div>
                    <div class="tag">善良人妻</div>
                </div>
                
                <!-- 彩色饼图 -->
                <div class="color-wheel"></div>
            </div>
            
            <!-- 音乐播放器 -->
            <div class="music-player">
                <h2 class="music-title">音乐</h2>
                <div class="player-controls">
                    <div class="play-btn">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="white">
                            <path d="M8 5v14l11-7z"/>
                        </svg>
                    </div>
                    <div class="progress-container">
                        <div class="progress"></div>
                    </div>
                    <div class="volume-icon">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="white">
                            <path d="M3 9v6h4l5 5V4L7 9H3zm13.5 3c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02zM14 3.23v2.06c2.89.86 5 3.54 5 6.71s-2.11 5.85-5 6.71v2.06c4.01-.91 7-4.49 7-8.77s-2.99-7.86-7-8.77z"/>
                        </svg>
                    </div>
                </div>
            </div>
            
            <!-- 中间大图 -->
            <div class="main-image">
                <img src="https://images.unsplash.com/photo-1505506874110-6a7a69069a08?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80" alt="Main Image">
                <div class="quote">"如果你看到了这行字，"</div>
            </div>
            
            <!-- 右侧功能区 -->
            <div class="right-section">
                <div class="time-display">
                    <div class="time">16:21:59</div>
                    <div class="date">2025年02月17日 星期一</div>
                    <div class="time-circle">
                        <div class="circle-bg"></div>
                        <div class="circle-progress"></div>
                        <div class="circle-center">00</div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- 底部卡片 -->
        <div class="cards">
            <div class="card">
                <img src="https://images.unsplash.com/photo-1505506874110-6a7a69069a08?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80" alt="Blog">
                <div class="card-content">
                    <h3 class="card-title">博客</h3>
                    <p class="card-desc">写不了一点
                    <div class="card-footer">
                        <a href="#" class="card-link">前往</a>
                    </div>
                </div>
            </div>
            
            <div class="card">
                <img src="https://images.unsplash.com/photo-1505506874110-6a7a69069a08?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80" alt="网盘">
                <div class="card-content">
                    <h3 class="card-title">网盘</h3>
                    <p class="card-desc">云端的百宝箱，数据的避风港
                    <div class="card-footer">
                        <a href="#" class="card-link">前往</a>
                    </div>
                </div>
            </div>
            
            <div class="card">
                <img src="https://images.unsplash.com/photo-1505506874110-6a7a69069a08?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80" alt="二级域名">
                <div class="card-content">
                    <h3 class="card-title">二级域名</h3>
                    <p class="card-desc">免费、稳定、放心
                    <div class="card-footer">
                        <a href="#" class="card-link">前往</a>
                    </div>
                </div>
            </div>
            
            <div class="card">
                <img src="https://images.unsplash.com/photo-1505506874110-6a7a69069a08?ixlib=rb-1.2.1&auto=format&fit=crop&w=1920&q=80" alt="套博要饭">
                <div class="card-content">
                    <h3 class="card-title">套博要饭</h3>
                    <p class="card-desc">博爱世界，打赏链接，一手不亦乐乎
                    <div class="card-footer">
                        <a href="#" class="card-link">前往</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- 音乐播放器脚本 -->
    <script>
        // 创建气泡
        function createBubbles() {
            const bubblesContainer = document.querySelector('.bubbles');
            for (let i = 0; i < 20; i++) {
                const bubble = document.createElement('div');
                bubble.classList.add('bubble');
                const size = Math.random() * 20 + 5;
                bubble.style.width = `${size}px`;
                bubble.style.height = `${size}px`;
                bubble.style.left = `${Math.random() * 100}%`;
                bubble.style.top = `${Math.random() * 100}%`;
                bubble.style.animationDelay = `${Math.random() * 5}s`;
                bubble.style.animationDuration = `${Math.random() * 5 + 5}s`;
                bubblesContainer.appendChild(bubble);
            }
        }
        
        // 音乐播放器功能
        function setupMusicPlayer() {
            const playBtn = document.querySelector('.play-btn');
            const progress = document.querySelector('.progress');
            let isPlaying = false;
            let progressInterval;
            
            playBtn.addEventListener('click', () => {
                isPlaying = !isPlaying;
                if (isPlaying) {
                    playBtn.innerHTML = '<svg width="20" height="20" viewBox="0 0 24 24" fill="white"><path d="M6 19h4V5H6v14zm8-14v14h4V5h-4z"/></svg>';
                    // 模拟进度条前进
                    let width = 0;
                    progressInterval = setInterval(() => {
                        if (width >= 100) {
                            clearInterval(progressInterval);
                            isPlaying = false;
                            playBtn.innerHTML = '<svg width="20" height="20" viewBox="0 0 24 24" fill="white"><path d="M8 5v14l11-7z"/></svg>';
                            progress.style.width = '0%';
                        } else {
                            width += 0.5;
                            progress.style.width = `${width}%`;
                        }
                    }, 100);
                } else {
                    playBtn.innerHTML = '<svg width="20" height="20" viewBox="0 0 24 24" fill="white"><path d="M8 5v14l11-7z"/></svg>';
                    clearInterval(progressInterval);
                }
            });
        }
        
        // 更新时间
        function updateTime() {
            const now = new Date();
            const timeElement = document.querySelector('.time');
            const dateElement = document.querySelector('.date');
            
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            
            const year = now.getFullYear();
            const month = String(now.getMonth() + 1).padStart(2, '0');
            const day = String(now.getDate()).padStart(2, '0');
            const weekdays = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
            const weekday = weekdays[now.getDay()];
            
            timeElement.textContent = `${hours}:${minutes}:${seconds}`;
            dateElement.textContent = `${year}年${month}月${day}日 ${weekday}`;
        }
        
        // 初始化
        document.addEventListener('DOMContentLoaded', () => {
            createBubbles();
            setupMusicPlayer();
            updateTime();
            setInterval(updateTime, 1000);
        });
    </script>
</body>
</html>
