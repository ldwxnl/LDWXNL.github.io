---
layout: default
title: 🐍 贪吃蛇游戏
permalink: games/snake-game/
---

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <title>🐍 贪吃蛇游戏 - AI对战增强版</title>
    <style>
        /* 基础样式 */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            -webkit-tap-highlight-color: transparent;
            -webkit-user-select: none;
            user-select: none;
        }

        html, body {
            width: 100%;
            min-height: 100vh;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: #1a1a1a;
            color: #e0e0e0;
            overflow-x: hidden;
        }

        /* 游戏容器 - 允许垂直滚动 */
        .game-app {
            max-width: 1200px;
            margin: 0 auto;
            padding: 1rem;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* 头部 */
        .game-header {
            text-align: center;
            padding: 1rem 0;
            margin-bottom: 1rem;
        }

        .game-title {
            font-size: 2rem;
            color: #4CAF50;
            margin-bottom: 0.5rem;
        }

        .game-subtitle {
            color: #aaa;
            font-size: 1rem;
        }

        /* 主游戏区域 */
        .game-main {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            flex: 1;
        }

        /* 控制面板区域 */
        .control-panels {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .control-panel {
            flex: 1;
            min-width: 300px;
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1.2rem;
        }

        .panel-title {
            color: #4CAF50;
            font-size: 1.1rem;
            margin-bottom: 1rem;
            border-left: 3px solid #4CAF50;
            padding-left: 0.8rem;
        }

        /* 游戏模式选择 */
        .mode-selector {
            display: flex;
            flex-direction: column;
            gap: 0.6rem;
        }

        .mode-btn {
            padding: 0.7rem 1rem;
            background: #333;
            border: 2px solid transparent;
            border-radius: 8px;
            color: #fff;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            text-align: left;
        }

        .mode-btn.active {
            background: rgba(76, 175, 80, 0.1);
            border-color: #4CAF50;
        }

        .mode-btn:hover:not(.active) {
            background: #3a3a3a;
        }

        /* AI设置 */
        .ai-settings {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 0.8rem;
        }

        .ai-setting-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .ai-setting-item input[type="range"] {
            flex: 1;
        }

        .ai-setting-item span {
            font-size: 0.9rem;
            color: #4CAF50;
            min-width: 40px;
        }

        /* 皮肤选择器 */
        .skin-selector {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.8rem;
        }

        .skin-btn {
            background: #333;
            border: 2px solid transparent;
            border-radius: 8px;
            padding: 0.6rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .skin-btn.active {
            border-color: #4CAF50;
            background: rgba(76, 175, 80, 0.1);
        }

        .skin-preview {
            width: 30px;
            height: 30px;
            border-radius: 6px;
            margin-bottom: 0.3rem;
        }

        .classic-skin { background: linear-gradient(45deg, #4CAF50, #8BC34A); }
        .neon-skin { background: linear-gradient(45deg, #00bcd4, #e040fb); box-shadow: 0 0 8px #00bcd4; }
        .pixel-skin { background: linear-gradient(45deg, #ff9800, #ff5722); }
        .nature-skin { background: linear-gradient(45deg, #795548, #4caf50); }

        /* 游戏区域 */
        .game-area {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1rem;
        }

        .canvas-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            aspect-ratio: 1/1;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 8px 30px rgba(0,0,0,0.4);
            touch-action: none; /* 禁止游戏区域滚动 */
        }

        #gameCanvas {
            width: 100%;
            height: 100%;
            display: block;
            background: #111;
        }

        /* 游戏覆盖层 */
        .game-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 10;
        }

        .overlay-title {
            font-size: 2rem;
            color: #4CAF50;
            margin-bottom: 1rem;
            text-align: center;
        }

        .overlay-text {
            font-size: 1.1rem;
            color: #ccc;
            margin-bottom: 1.5rem;
            text-align: center;
            line-height: 1.5;
        }

        /* 按钮样式 */
        .btn {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary {
            background: linear-gradient(135deg, #4CAF50, #2E7D32);
            color: white;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(76, 175, 80, 0.3);
        }

        /* 分数面板 */
        .score-panel {
            display: flex;
            justify-content: center;
            gap: 1.5rem;
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1rem 2rem;
            flex-wrap: wrap;
        }

        .score-item {
            text-align: center;
            min-width: 80px;
        }

        .score-label {
            color: #aaa;
            font-size: 0.8rem;
            margin-bottom: 0.3rem;
        }

        .score-value {
            color: #fff;
            font-size: 1.8rem;
            font-weight: bold;
        }

        /* 控制按钮组 */
        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .action-btn {
            padding: 0.7rem 1.5rem;
            background: #333;
            border: 1px solid #444;
            border-radius: 6px;
            color: #fff;
            font-weight: 500;
            cursor: pointer;
            min-width: 120px;
        }

        .action-btn:hover {
            background: #3a3a3a;
            border-color: #4CAF50;
        }

        /* 游戏统计 */
        .game-stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1rem;
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1rem;
        }

        .stat-item {
            text-align: center;
        }

        .stat-label {
            color: #aaa;
            font-size: 0.8rem;
            margin-bottom: 0.3rem;
        }

        .stat-value {
            color: #fff;
            font-size: 1.2rem;
            font-weight: bold;
        }

        /* 手机虚拟控制 - 增强版 */
        .mobile-controls {
            display: none;
            margin-top: 1rem;
            width: 100%;
            max-width: 500px;
        }

        .control-section {
            margin-bottom: 1rem;
        }

        .control-section-title {
            color: #4CAF50;
            font-size: 1rem;
            margin-bottom: 0.5rem;
            text-align: center;
        }

        .virtual-dpad {
            display: grid;
            grid-template-areas: 
                ". up ."
                "left . right"
                ". down .";
            gap: 15px;
            justify-content: center;
            margin: 0 auto;
        }

        .dpad-btn {
            width: 70px;
            height: 70px;
            border: none;
            border-radius: 50%;
            background: #333;
            color: white;
            font-size: 28px;
            cursor: pointer;
            touch-action: manipulation;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 8px rgba(0,0,0,0.3);
            transition: all 0.1s;
        }

        .dpad-btn.up { grid-area: up; }
        .dpad-btn.down { grid-area: down; }
        .dpad-btn.left { grid-area: left; }
        .dpad-btn.right { grid-area: right; }

        .dpad-btn:active {
            background: #4CAF50;
            transform: scale(0.95);
        }

        /* 功能按钮区域 */
        .function-buttons {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-top: 1rem;
        }

        .func-btn {
            padding: 0.8rem;
            background: #333;
            border: 1px solid #444;
            border-radius: 8px;
            color: #fff;
            font-size: 0.9rem;
            cursor: pointer;
            text-align: center;
        }

        .func-btn:active {
            background: #4CAF50;
        }

        /* 操作说明 */
        .instructions {
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1rem;
            margin-top: 1rem;
            font-size: 0.9rem;
            line-height: 1.5;
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .game-app {
                padding: 0.5rem;
            }
            
            .control-panels {
                flex-direction: column;
            }
            
            .control-panel {
                min-width: auto;
            }
            
            .canvas-container {
                max-width: 95vw;
            }
            
            .score-panel {
                padding: 0.8rem 1rem;
                gap: 1rem;
            }
            
            .score-item {
                min-width: 70px;
            }
            
            .score-value {
                font-size: 1.5rem;
            }
            
            .mobile-controls {
                display: block;
            }
            
            .skin-selector {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .game-stats {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .dpad-btn {
                width: 60px;
                height: 60px;
                font-size: 24px;
            }
        }

        @media (max-width: 480px) {
            .game-title {
                font-size: 1.6rem;
            }
            
            .panel-title {
                font-size: 1rem;
            }
            
            .btn {
                padding: 0.7rem 1.2rem;
                font-size: 0.9rem;
            }
            
            .action-btn {
                min-width: 100px;
                padding: 0.6rem 1rem;
            }
            
            .dpad-btn {
                width: 50px;
                height: 50px;
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="game-app">
        <!-- 头部 -->
        <header class="game-header">
            <h1 class="game-title">🐍 贪吃蛇游戏 - AI对战</h1>
            <p class="game-subtitle">挑战多个AI对手，体验激烈对战！</p>
        </header>

        <!-- 主游戏区域 -->
        <main class="game-main">
            <!-- 控制面板 -->
            <div class="control-panels">
                <!-- 左面板：游戏设置 -->
                <div class="control-panel">
                    <h3 class="panel-title">🎮 游戏设置</h3>
                    <div class="mode-selector">
                        <button class="mode-btn active" data-mode="single">单人模式</button>
                        <button class="mode-btn" data-mode="ai">AI对战模式</button>
                    </div>
                    
                    <!-- AI设置（仅AI模式显示） -->
                    <div id="ai-settings" style="display: none; margin-top: 1rem;">
                        <div class="panel-title">🤖 AI设置</div>
                        <div class="ai-settings">
                            <div class="ai-setting-item">
                                <label>AI数量:</label>
                                <input type="range" id="ai-count" min="1" max="3" value="1">
                                <span id="ai-count-value">1</span>
                            </div>
                            <div class="ai-setting-item">
                                <label>AI难度:</label>
                                <input type="range" id="ai-difficulty" min="1" max="3" value="2">
                                <span id="ai-difficulty-value">中等</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 右面板：皮肤选择 -->
                <div class="control-panel">
                    <h3 class="panel-title">🎨 皮肤选择</h3>
                    <div class="skin-selector">
                        <button class="skin-btn active" data-skin="classic">
                            <div class="skin-preview classic-skin"></div>
                            <span>经典</span>
                        </button>
                        <button class="skin-btn" data-skin="neon">
                            <div class="skin-preview neon-skin"></div>
                            <span>霓虹</span>
                        </button>
                        <button class="skin-btn" data-skin="pixel">
                            <div class="skin-preview pixel-skin"></div>
                            <span>像素</span>
                        </button>
                        <button class="skin-btn" data-skin="nature">
                            <div class="skin-preview nature-skin"></div>
                            <span>自然</span>
                        </button>
                    </div>
                </div>
            </div>

            <!-- 游戏区域 -->
            <div class="game-area">
                <!-- 游戏画布 -->
                <div class="canvas-container">
                    <canvas id="gameCanvas"></canvas>
                    
                    <!-- 游戏状态覆盖层 -->
                    <div id="gameOverlay" class="game-overlay">
                        <h2 id="overlayTitle" class="overlay-title">贪吃蛇AI对战</h2>
                        <p id="overlayText" class="overlay-text">选择AI对战模式，挑战多个AI对手！</p>
                        <button id="startBtn" class="btn btn-primary">开始游戏</button>
                    </div>
                </div>

                <!-- 分数面板 -->
                <div class="score-panel">
                    <div class="score-item">
                        <div class="score-label">你的分数</div>
                        <div id="playerScore" class="score-value">0</div>
                    </div>
                    <div class="score-item">
                        <div class="score-label">你的长度</div>
                        <div id="playerLength" class="score-value">1</div>
                    </div>
                    <div class="score-item">
                        <div class="score-label">最高分</div>
                        <div id="highScore" class="score-value">0</div>
                    </div>
                </div>

                <!-- 控制按钮 -->
                <div class="action-buttons">
                    <button id="pauseBtn" class="action-btn">暂停游戏</button>
                    <button id="restartBtn" class="action-btn">重新开始</button>
                </div>

                <!-- 游戏统计 -->
                <div class="game-stats">
                    <div class="stat-item">
                        <div class="stat-label">游戏时间</div>
                        <div id="gameTime" class="stat-value">00:00</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">食物数量</div>
                        <div id="foodCount" class="stat-value">0</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-label">存活AI</div>
                        <div id="aliveAI" class="stat-value">0</div>
                    </div>
                </div>

                <!-- 手机虚拟控制 -->
                <div class="mobile-controls">
                    <div class="control-section">
                        <div class="control-section-title">虚拟方向键</div>
                        <div class="virtual-dpad">
                            <button class="dpad-btn up">↑</button>
                            <button class="dpad-btn down">↓</button>
                            <button class="dpad-btn left">←</button>
                            <button class="dpad-btn right">→</button>
                        </div>
                    </div>
                    
                    <div class="control-section">
                        <div class="control-section-title">功能按键</div>
                        <div class="function-buttons">
                            <button class="func-btn" id="mobilePause">暂停</button>
                            <button class="func-btn" id="mobileStart">开始</button>
                            <button class="func-btn" id="mobileRestart">重来</button>
                        </div>
                    </div>
                </div>

                <!-- 操作说明 -->
                <div class="instructions">
                    <p><strong>操作说明：</strong></p>
                    <p>• 电脑：方向键 或 WASD 控制移动，空格键暂停</p>
                    <p>• 手机：滑动屏幕 或 使用虚拟按键控制</p>
                    <p>• AI模式：击败AI蛇获得额外分数，AI会主动攻击你</p>
                </div>
            </div>
        </main>
    </div>

    <script>
    // ==================== 游戏配置 ====================
    const CONFIG = {
        GRID_SIZE: 20,
        PLAYER_SPEED: 150,
        AI_SPEEDS: [300, 200, 100], // 简单、中等、困难
        FOOD_SCORE: 10,
        AI_KILL_SCORE: 50
    };

    // ==================== 游戏状态 ====================
    const GameState = {
        // DOM元素
        elements: {},
        
        // 游戏对象
        canvas: null,
        ctx: null,
        
        // 玩家
        player: {
            snake: [],
            direction: { dx: 0, dy: 0 },
            score: 0,
            length: 1
        },
        
        // AI系统
        ai: {
            snakes: [], // 数组，支持多个AI
            difficulty: 2, // 1-简单, 2-中等, 3-困难
            count: 1,     // AI数量
            colors: ['#9C27B0', '#2196F3', '#FF9800'] // AI颜色
        },
        
        // 游戏状态
        food: { x: 0, y: 0 },
        highScore: localStorage.getItem('snakeHighScore') || 0,
        isPaused: true,
        isGameOver: true,
        gameMode: 'single',
        
        // 游戏循环
        gameLoop: null,
        startTime: 0,
        elapsedTime: 0,
        foodCount: 0,
        
        // 皮肤系统
        currentSkin: 'classic',
        skins: {
            classic: { snake: '#4CAF50', food: '#FF5252', bg: '#111' },
            neon: { snake: '#00bcd4', food: '#ffeb3b', bg: '#0a0a1a' },
            pixel: { snake: '#ff9800', food: '#2196f3', bg: '#1a1a1a' },
            nature: { snake: '#795548', food: '#ff7043', bg: '#0f2a1f' }
        },
        
        // 触摸控制
        touchStartX: 0,
        touchStartY: 0
    };

    // ==================== 初始化游戏 ====================
    function initGame() {
        console.log('🎮 初始化贪吃蛇AI对战游戏...');
        
        // 获取DOM元素
        getDOMElements();
        
        // 初始化Canvas
        initCanvas();
        
        // 显示最高分
        GameState.elements.highScore.textContent = GameState.highScore;
        
        // 绑定事件监听器
        setupEventListeners();
        
        // 初始化游戏状态
        resetGame();
        
        // 初始绘制
        draw();
        
        console.log('🎮 游戏初始化完成！');
    }

    // 获取DOM元素
    function getDOMElements() {
        GameState.elements = {
            // Canvas相关
            canvas: document.getElementById('gameCanvas'),
            gameOverlay: document.getElementById('gameOverlay'),
            overlayTitle: document.getElementById('overlayTitle'),
            overlayText: document.getElementById('overlayText'),
            
            // 分数显示
            playerScore: document.getElementById('playerScore'),
            playerLength: document.getElementById('playerLength'),
            highScore: document.getElementById('highScore'),
            
            // 统计信息
            gameTime: document.getElementById('gameTime'),
            foodCount: document.getElementById('foodCount'),
            aliveAI: document.getElementById('aliveAI'),
            
            // 按钮
            startBtn: document.getElementById('startBtn'),
            pauseBtn: document.getElementById('pauseBtn'),
            restartBtn: document.getElementById('restartBtn'),
            
            // 模式选择
            modeButtons: document.querySelectorAll('.mode-btn'),
            aiSettings: document.getElementById('ai-settings'),
            
            // AI设置
            aiCount: document.getElementById('ai-count'),
            aiCountValue: document.getElementById('ai-count-value'),
            aiDifficulty: document.getElementById('ai-difficulty'),
            aiDifficultyValue: document.getElementById('ai-difficulty-value'),
            
            // 皮肤选择
            skinButtons: document.querySelectorAll('.skin-btn'),
            
            // 虚拟控制
            dpadButtons: document.querySelectorAll('.dpad-btn'),
            mobilePause: document.getElementById('mobilePause'),
            mobileStart: document.getElementById('mobileStart'),
            mobileRestart: document.getElementById('mobileRestart')
        };
        
        // 获取Canvas上下文
        GameState.ctx = GameState.elements.canvas.getContext('2d');
    }

    // 初始化Canvas
    function initCanvas() {
        const canvas = GameState.elements.canvas;
        
        // 设置Canvas焦点
        canvas.setAttribute('tabindex', '0');
        canvas.style.outline = 'none';
        canvas.focus();
        
        // 设置Canvas尺寸
        const container = canvas.parentElement;
        const size = Math.min(container.clientWidth, container.clientHeight);
        canvas.width = size;
        canvas.height = size;
    }

    // ==================== 事件监听器 ====================
    function setupEventListeners() {
        console.log('🎮 设置事件监听器...');
        
        // 键盘控制
        document.addEventListener('keydown', handleKeyDown);
        
        // 游戏按钮
        GameState.elements.startBtn.addEventListener('click', startGame);
        GameState.elements.pauseBtn.addEventListener('click', togglePause);
        GameState.elements.restartBtn.addEventListener('click', resetGame);
        
        // 模式选择
        GameState.elements.modeButtons.forEach(btn => {
            btn.addEventListener('click', function() {
                // 移除所有active
                GameState.elements.modeButtons.forEach(b => b.classList.remove('active'));
                // 设置当前active
                this.classList.add('active');
                // 更新游戏模式
                GameState.gameMode = this.dataset.mode;
                
                // 显示/隐藏AI设置
                if (this.dataset.mode === 'ai') {
                    GameState.elements.aiSettings.style.display = 'block';
                } else {
                    GameState.elements.aiSettings.style.display = 'none';
                }
                
                // 重置游戏
                resetGame();
            });
        });
        
        // AI数量设置
        GameState.elements.aiCount.addEventListener('input', function() {
            const value = parseInt(this.value);
            GameState.elements.aiCountValue.textContent = value;
            GameState.ai.count = value;
            if (GameState.gameMode === 'ai') {
                initAISnakes();
                draw();
            }
        });
        
        // AI难度设置
        GameState.elements.aiDifficulty.addEventListener('input', function() {
            const value = parseInt(this.value);
            const difficulties = ['简单', '中等', '困难'];
            GameState.elements.aiDifficultyValue.textContent = difficulties[value - 1];
            GameState.ai.difficulty = value;
        });
        
        // 皮肤选择
        GameState.elements.skinButtons.forEach(btn => {
            btn.addEventListener('click', function() {
                // 移除所有active
                GameState.elements.skinButtons.forEach(b => b.classList.remove('active'));
                // 设置当前active
                this.classList.add('active');
                // 更新皮肤
                GameState.currentSkin = this.dataset.skin;
                // 重新绘制
                draw();
            });
        });
        
        // 虚拟方向键
        GameState.elements.dpadButtons.forEach(btn => {
            btn.addEventListener('touchstart', function(e) {
                e.preventDefault();
                const direction = this.textContent;
                handleDirection(direction);
                this.style.background = '#4CAF50';
            });
            
            btn.addEventListener('touchend', function(e) {
                e.preventDefault();
                this.style.background = '#333';
            });
            
            btn.addEventListener('mousedown', function() {
                const direction = this.textContent;
                handleDirection(direction);
                this.style.background = '#4CAF50';
            });
            
            btn.addEventListener('mouseup', function() {
                this.style.background = '#333';
            });
        });
        
        // 手机功能按钮
        GameState.elements.mobilePause.addEventListener('click', togglePause);
        GameState.elements.mobileStart.addEventListener('click', startGame);
        GameState.elements.mobileRestart.addEventListener('click', resetGame);
        
        // 触摸控制
        setupTouchControls();
        
        // Canvas点击获取焦点
        GameState.elements.canvas.addEventListener('click', function() {
            this.focus();
        });
        
        console.log('🎮 事件监听器设置完成');
    }

    // 设置触摸控制
    function setupTouchControls() {
        const canvas = GameState.elements.canvas;
        const minSwipeDistance = 20;
        
        // 触摸开始
        canvas.addEventListener('touchstart', function(e) {
            if (e.touches.length !== 1) return;
            const touch = e.touches[0];
            GameState.touchStartX = touch.clientX;
            GameState.touchStartY = touch.clientY;
            e.preventDefault();
        }, { passive: false });
        
        // 触摸结束
        canvas.addEventListener('touchend', function(e) {
            if (!GameState.touchStartX || GameState.isPaused || GameState.isGameOver) return;
            if (e.changedTouches.length !== 1) return;
            
            const touch = e.changedTouches[0];
            const deltaX = touch.clientX - GameState.touchStartX;
            const deltaY = touch.clientY - GameState.touchStartY;
            
            // 防误触
            if (Math.abs(deltaX) < minSwipeDistance && Math.abs(deltaY) < minSwipeDistance) {
                GameState.touchStartX = 0;
                return;
            }
            
            // 判断滑动方向
            if (Math.abs(deltaX) > Math.abs(deltaY)) {
                if (deltaX > 0) handleDirection('→');
                else handleDirection('←');
            } else {
                if (deltaY > 0) handleDirection('↓');
                else handleDirection('↑');
            }
            
            GameState.touchStartX = 0;
            e.preventDefault();
        }, { passive: false });
        
        // 阻止游戏区域滚动
        canvas.addEventListener('touchmove', function(e) {
            e.preventDefault();
        }, { passive: false });
    }

    // 处理方向输入
    function handleDirection(direction) {
        if (GameState.isPaused && !GameState.isGameOver) return;
        
        switch(direction) {
            case '↑':
            case 'ArrowUp':
                if (GameState.player.direction.dy !== 1) {
                    GameState.player.direction = { dx: 0, dy: -1 };
                }
                break;
            case '↓':
            case 'ArrowDown':
                if (GameState.player.direction.dy !== -1) {
                    GameState.player.direction = { dx: 0, dy: 1 };
                }
                break;
            case '←':
            case 'ArrowLeft':
                if (GameState.player.direction.dx !== 1) {
                    GameState.player.direction = { dx: -1, dy: 0 };
                }
                break;
            case '→':
            case 'ArrowRight':
                if (GameState.player.direction.dx !== -1) {
                    GameState.player.direction = { dx: 1, dy: 0 };
                }
                break;
        }
    }

    // 键盘控制
    function handleKeyDown(e) {
        switch(e.key) {
            case 'ArrowUp':
            case 'w':
            case 'W':
                handleDirection('↑');
                break;
            case 'ArrowDown':
            case 's':
            case 'S':
                handleDirection('↓');
                break;
            case 'ArrowLeft':
            case 'a':
            case 'A':
                handleDirection('←');
                break;
            case 'ArrowRight':
            case 'd':
            case 'D':
                handleDirection('→');
                break;
            case ' ': // 空格键暂停
                e.preventDefault();
                togglePause();
                break;
        }
    }

    // ==================== 游戏控制 ====================
    function startGame() {
        console.log('🎮 开始游戏，模式:', GameState.gameMode, 'AI数量:', GameState.ai.count);
        
        if (GameState.isGameOver) {
            resetGame();
            GameState.isGameOver = false;
        }
        
        if (GameState.isPaused) {
            GameState.isPaused = false;
            GameState.startTime = Date.now() - GameState.elapsedTime;
            GameState.gameLoop = setInterval(gameUpdate, CONFIG.PLAYER_SPEED);
            
            // 更新UI
            GameState.elements.gameOverlay.style.display = 'none';
            GameState.elements.startBtn.textContent = '游戏中...';
            GameState.elements.canvas.focus();
            
            // AI模式初始化AI蛇
            if (GameState.gameMode === 'ai') {
                initAISnakes();
            }
        }
    }

    function togglePause() {
        if (GameState.isGameOver) return;
        
        GameState.isPaused = !GameState.isPaused;
        if (GameState.isPaused) {
            clearInterval(GameState.gameLoop);
            showOverlay('游戏暂停', '点击继续游戏');
            GameState.elements.startBtn.textContent = '继续游戏';
        } else {
            GameState.gameLoop = setInterval(gameUpdate, CONFIG.PLAYER_SPEED);
            GameState.elements.gameOverlay.style.display = 'none';
            GameState.elements.startBtn.textContent = '游戏中...';
        }
    }

    function resetGame() {
        console.log('🎮 重置游戏');
        
        clearInterval(GameState.gameLoop);
        GameState.isPaused = true;
        GameState.isGameOver = true;
        
        // 重置玩家
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        const center = Math.floor(gridCount / 2);
        GameState.player = {
            snake: [{ x: center, y: center }],
            direction: { dx: 0, dy: 0 },
            score: 0,
            length: 1
        };
        
        // 重置AI
        GameState.ai.snakes = [];
        
        // 生成食物
        generateFood();
        
        // 重置状态
        GameState.foodCount = 0;
        GameState.elapsedTime = 0;
        
        // 更新显示
        updateDisplay();
        draw();
        
        // 显示开始界面
        if (GameState.gameMode === 'ai') {
            showOverlay('AI对战模式', `挑战 ${GameState.ai.count} 个AI对手！`);
        } else {
            showOverlay('贪吃蛇游戏', '点击开始游戏');
        }
        GameState.elements.startBtn.textContent = '开始游戏';
        GameState.elements.gameTime.textContent = '00:00';
    }

    // ==================== 游戏逻辑 ====================
    function gameUpdate() {
        if (GameState.isPaused || GameState.isGameOver) return;
        
        // 更新游戏时间
        GameState.elapsedTime = Date.now() - GameState.startTime;
        updateGameTime();
        
        // 移动玩家蛇
        moveSnake(GameState.player.snake, GameState.player.direction, true);
        
        // AI模式：移动所有AI蛇
        if (GameState.gameMode === 'ai') {
            updateAllAISnakes();
        }
        
        // 检查玩家碰撞
        if (checkCollision(GameState.player.snake)) {
            gameOver();
            return;
        }
        
        // 检查AI蛇碰撞
        if (GameState.gameMode === 'ai') {
            checkAICollisions();
        }
        
        // 更新显示
        updateDisplay();
        draw();
    }

    // 移动蛇
    function moveSnake(snake, direction, isPlayer = false) {
        if (direction.dx === 0 && direction.dy === 0) return;
        
        const head = { 
            x: snake[0].x + direction.dx, 
            y: snake[0].y + direction.dy 
        };
        snake.unshift(head);
        
        // 检查是否吃到食物
        if (head.x === GameState.food.x && head.y === GameState.food.y) {
            if (isPlayer) {
                GameState.player.score += CONFIG.FOOD_SCORE;
                GameState.player.length = snake.length;
                GameState.foodCount++;
            }
            generateFood();
        } else {
            snake.pop();
        }
    }

    // 生成食物
    function generateFood() {
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        let newFood;
        let onSnake;
        
        do {
            onSnake = false;
            newFood = {
                x: Math.floor(Math.random() * gridCount),
                y: Math.floor(Math.random() * gridCount)
            };
            
            // 检查是否在玩家蛇身上
            for (const segment of GameState.player.snake) {
                if (segment.x === newFood.x && segment.y === newFood.y) {
                    onSnake = true;
                    break;
                }
            }
            
            // 检查是否在AI蛇身上
            for (const aiSnake of GameState.ai.snakes) {
                for (const segment of aiSnake.snake) {
                    if (segment.x === newFood.x && segment.y === newFood.y) {
                        onSnake = true;
                        break;
                    }
                }
                if (onSnake) break;
            }
        } while (onSnake);
        
        GameState.food = newFood;
    }

    // 检查碰撞
    function checkCollision(snake) {
        const head = snake[0];
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        
        // 撞墙
        if (head.x < 0 || head.x >= gridCount || head.y < 0 || head.y >= gridCount) {
            return true;
        }
        
        // 撞自己（从第2节开始检查）
        for (let i = 1; i < snake.length; i++) {
            if (head.x === snake[i].x && head.y === snake[i].y) {
                return true;
            }
        }
        
        return false;
    }

    // 游戏结束
    function gameOver() {
        console.log('🎮 游戏结束，得分:', GameState.player.score);
        
        clearInterval(GameState.gameLoop);
        GameState.isGameOver = true;
        GameState.isPaused = true;
        
        // 更新最高分
        if (GameState.player.score > GameState.highScore) {
            GameState.highScore = GameState.player.score;
            localStorage.setItem('snakeHighScore', GameState.highScore);
            GameState.elements.highScore.textContent = GameState.highScore;
        }
        
        showOverlay('游戏结束', `得分: ${GameState.player.score}<br>长度: ${GameState.player.length}<br>时间: ${formatTime(GameState.elapsedTime)}`);
        GameState.elements.startBtn.textContent = '重新开始';
    }

    // ==================== AI对战系统 ====================
    function initAISnakes() {
        GameState.ai.snakes = [];
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        
        for (let i = 0; i < GameState.ai.count; i++) {
            // 将AI蛇放在不同的起始位置
            let startX, startY;
            do {
                startX = Math.floor(Math.random() * (gridCount - 4)) + 2;
                startY = Math.floor(Math.random() * (gridCount - 4)) + 2;
            } while (isPositionOccupied(startX, startY));
            
            GameState.ai.snakes.push({
                snake: [{ x: startX, y: startY }],
                direction: { dx: 1, dy: 0 },
                color: GameState.ai.colors[i % GameState.ai.colors.length],
                lastMoveTime: Date.now(),
                moveDelay: CONFIG.AI_SPEEDS[GameState.ai.difficulty - 1]
            });
        }
        
        updateAliveAICount();
    }

    function isPositionOccupied(x, y) {
        // 检查是否在玩家蛇身上
        for (const segment of GameState.player.snake) {
            if (segment.x === x && segment.y === y) return true;
        }
        
        // 检查是否在其他AI蛇身上
        for (const aiSnake of GameState.ai.snakes) {
            for (const segment of aiSnake.snake) {
                if (segment.x === x && segment.y === y) return true;
            }
        }
        
        return false;
    }

    function updateAllAISnakes() {
        const now = Date.now();
        
        for (let i = GameState.ai.snakes.length - 1; i >= 0; i--) {
            const aiSnake = GameState.ai.snakes[i];
            
            // 控制AI移动速度
            if (now - aiSnake.lastMoveTime >= aiSnake.moveDelay) {
                // 更新AI移动方向
                updateAIDirection(aiSnake, i);
                
                // 移动AI蛇
                moveSnake(aiSnake.snake, aiSnake.direction, false);
                
                aiSnake.lastMoveTime = now;
                
                // 检查AI蛇是否碰撞
                if (checkCollision(aiSnake.snake)) {
                    // AI蛇死亡，玩家得分
                    GameState.player.score += CONFIG.AI_KILL_SCORE;
                    GameState.ai.snakes.splice(i, 1);
                    updateAliveAICount();
                }
            }
        }
    }

    function updateAIDirection(aiSnake, aiIndex) {
        const head = aiSnake.snake[0];
        const directions = [
            { dx: 1, dy: 0 },
            { dx: -1, dy: 0 },
            { dx: 0, dy: 1 },
            { dx: 0, dy: -1 }
        ];
        
        // 避免直接掉头
        const validDirections = directions.filter(dir => 
            !(dir.dx === -aiSnake.direction.dx && dir.dy === -aiSnake.direction.dy)
        );
        
        // 根据难度调整AI智能
        let chosenDirection;
        if (GameState.ai.difficulty === 3) { // 困难
            // 30%概率朝食物移动，20%概率朝玩家移动，50%随机
            const rand = Math.random();
            if (rand < 0.3) {
                chosenDirection = moveTowards(head, GameState.food, validDirections);
            } else if (rand < 0.5) {
                chosenDirection = moveTowards(head, GameState.player.snake[0], validDirections);
            } else {
                chosenDirection = validDirections[Math.floor(Math.random() * validDirections.length)];
            }
        } else if (GameState.ai.difficulty === 2) { // 中等
            // 20%概率朝食物移动，80%随机
            if (Math.random() < 0.2) {
                chosenDirection = moveTowards(head, GameState.food, validDirections);
            } else {
                chosenDirection = validDirections[Math.floor(Math.random() * validDirections.length)];
            }
        } else { // 简单
            chosenDirection = validDirections[Math.floor(Math.random() * validDirections.length)];
        }
        
        if (chosenDirection) {
            aiSnake.direction = chosenDirection;
        }
    }

    function moveTowards(from, to, validDirections) {
        const dx = to.x - from.x;
        const dy = to.y - from.y;
        
        // 优先选择减少距离的方向
        let bestDirection = null;
        let bestScore = -Infinity;
        
        for (const dir of validDirections) {
            const newX = from.x + dir.dx;
            const newY = from.y + dir.dy;
            const distX = Math.abs(to.x - newX);
            const distY = Math.abs(to.y - newY);
            const score = -(distX + distY); // 负距离，越小越好
            
            if (score > bestScore) {
                bestScore = score;
                bestDirection = dir;
            }
        }
        
        return bestDirection || validDirections[0];
    }

    function checkAICollisions() {
        for (let i = GameState.ai.snakes.length - 1; i >= 0; i--) {
            const aiSnake = GameState.ai.snakes[i];
            const head = aiSnake.snake[0];
            
            // 检查是否撞到玩家
            for (const segment of GameState.player.snake) {
                if (head.x === segment.x && head.y === segment.y) {
                    // AI撞到玩家，AI死亡
                    GameState.player.score += CONFIG.AI_KILL_SCORE;
                    GameState.ai.snakes.splice(i, 1);
                    updateAliveAICount();
                    break;
                }
            }
        }
    }

    function updateAliveAICount() {
        GameState.elements.aliveAI.textContent = GameState.ai.snakes.length;
    }

    // ==================== 渲染系统 ====================
    function draw() {
        const skin = GameState.skins[GameState.currentSkin];
        const cellSize = CONFIG.GRID_SIZE;
        const ctx = GameState.ctx;
        const canvas = GameState.elements.canvas;
        
        // 清空画布
        ctx.fillStyle = skin.bg;
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        
        // 绘制玩家蛇
        drawSnake(GameState.player.snake, skin.snake, true);
        
        // 绘制AI蛇
        for (let i = 0; i < GameState.ai.snakes.length; i++) {
            const aiSnake = GameState.ai.snakes[i];
            drawSnake(aiSnake.snake, aiSnake.color, false);
        }
        
        // 绘制食物
        ctx.fillStyle = skin.food;
        ctx.beginPath();
        const centerX = GameState.food.x * cellSize + cellSize / 2;
        const centerY = GameState.food.y * cellSize + cellSize / 2;
        ctx.arc(centerX, centerY, cellSize / 2 - 2, 0, Math.PI * 2);
        ctx.fill();
        
        // 食物发光效果
        ctx.shadowColor = skin.food + '80';
        ctx.shadowBlur = 10;
        ctx.fill();
        ctx.shadowBlur = 0;
    }

    // 绘制蛇
    function drawSnake(snake, color, isPlayer) {
        const cellSize = CONFIG.GRID_SIZE;
        const ctx = GameState.ctx;
        
        snake.forEach((segment, index) => {
            if (index === 0) {
                // 蛇头
                ctx.fillStyle = isPlayer ? color : '#FFFFFF';
                ctx.fillRect(
                    segment.x * cellSize + 1,
                    segment.y * cellSize + 1,
                    cellSize - 2,
                    cellSize - 2
                );
                
                // 蛇头标记
                ctx.fillStyle = isPlayer ? '#FFFFFF' : color;
                ctx.fillRect(
                    segment.x * cellSize + 5,
                    segment.y * cellSize + 5,
                    cellSize - 10,
                    cellSize - 10
                );
            } else {
                // 蛇身
                ctx.fillStyle = color;
                ctx.fillRect(
                    segment.x * cellSize + 1,
                    segment.y * cellSize + 1,
                    cellSize - 2,
                    cellSize - 2
                );
            }
        });
    }

    // ==================== UI更新 ====================
    function updateDisplay() {
        GameState.elements.playerScore.textContent = GameState.player.score;
        GameState.elements.playerLength.textContent = GameState.player.length;
        GameState.elements.foodCount.textContent = GameState.foodCount;
    }

    function updateGameTime() {
        GameState.elements.gameTime.textContent = formatTime(GameState.elapsedTime);
    }

    function showOverlay(title, text) {
        GameState.elements.overlayTitle.innerHTML = title;
        GameState.elements.overlayText.innerHTML = text;
        GameState.elements.gameOverlay.style.display = 'flex';
    }

    // ==================== 工具函数 ====================
    function formatTime(ms) {
        const totalSeconds = Math.floor(ms / 1000);
        const minutes = Math.floor(totalSeconds / 60);
        const seconds = totalSeconds % 60;
        return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    }

    // ==================== 启动游戏 ====================
    document.addEventListener('DOMContentLoaded', function() {
        console.log('📄 DOM加载完成，初始化游戏...');
        setTimeout(initGame, 100);
    });

    // 窗口大小变化时重新调整Canvas
    window.addEventListener('resize', function() {
        initCanvas();
        draw();
    });
    </script>
</body>
</html>
