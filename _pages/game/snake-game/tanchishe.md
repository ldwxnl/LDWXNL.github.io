---
layout: default
title: 🐍 贪吃蛇（自制）
permalink: /snake-game/
---
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>🐍 贪吃蛇游戏 - 完整版</title>
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
            height: 100%;
            overflow: hidden;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: #1a1a1a;
            color: #e0e0e0;
        }

        /* 游戏容器 */
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
            padding: 1rem 0 2rem;
            border-bottom: 2px solid #333;
            margin-bottom: 1.5rem;
        }

        .game-title {
            font-size: 2.5rem;
            color: #4CAF50;
            margin-bottom: 0.5rem;
        }

        .game-subtitle {
            color: #aaa;
            font-size: 1.1rem;
        }

        /* 主游戏区域 */
        .game-main {
            display: flex;
            gap: 1.5rem;
            flex: 1;
            margin-bottom: 2rem;
        }

        /* 左侧面板 - 游戏模式选择 */
        .left-panel {
            width: 250px;
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1.5rem;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .panel-section {
            margin-bottom: 1.5rem;
        }

        .panel-title {
            color: #4CAF50;
            font-size: 1.2rem;
            margin-bottom: 1rem;
            border-left: 3px solid #4CAF50;
            padding-left: 0.8rem;
        }

        /* 游戏模式选择 */
        .mode-selector {
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
        }

        .mode-btn {
            padding: 0.8rem 1rem;
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

        /* 皮肤选择器 */
        .skin-selector {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 0.8rem;
        }

        .skin-btn {
            background: #333;
            border: 2px solid transparent;
            border-radius: 8px;
            padding: 0.8rem;
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
            width: 40px;
            height: 40px;
            border-radius: 6px;
            margin-bottom: 0.5rem;
        }

        .classic-skin { background: linear-gradient(45deg, #4CAF50, #8BC34A); }
        .neon-skin { background: linear-gradient(45deg, #00bcd4, #e040fb); box-shadow: 0 0 10px #00bcd4; }
        .pixel-skin { background: linear-gradient(45deg, #ff9800, #ff5722); }
        .nature-skin { background: linear-gradient(45deg, #795548, #4caf50); }

        /* 中间游戏区域 */
        .game-center {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1.5rem;
        }

        .canvas-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            aspect-ratio: 1/1;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 8px 30px rgba(0,0,0,0.4);
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
            background: rgba(0, 0, 0, 0.85);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 10;
        }

        .overlay-title {
            font-size: 2.5rem;
            color: #4CAF50;
            margin-bottom: 1rem;
        }

        .overlay-text {
            font-size: 1.2rem;
            color: #ccc;
            margin-bottom: 2rem;
            text-align: center;
        }

        /* 按钮样式 */
        .btn {
            padding: 0.9rem 2rem;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
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

        .btn-secondary {
            background: #333;
            color: #fff;
            border: 1px solid #444;
        }

        .btn-secondary:hover {
            background: #3a3a3a;
            border-color: #4CAF50;
        }

        /* 分数面板 */
        .score-panel {
            display: flex;
            gap: 2rem;
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1.5rem 3rem;
        }

        .score-item {
            text-align: center;
            min-width: 100px;
        }

        .score-label {
            color: #aaa;
            font-size: 0.9rem;
            margin-bottom: 0.5rem;
        }

        .score-value {
            color: #fff;
            font-size: 2.5rem;
            font-weight: bold;
        }

        /* 右侧面板 - 控制面板 */
        .right-panel {
            width: 250px;
            background: #2a2a2a;
            border-radius: 12px;
            padding: 1.5rem;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        /* 控制按钮组 */
        .control-buttons {
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
        }

        .control-btn {
            padding: 0.8rem;
            background: #333;
            border: 1px solid #444;
            border-radius: 6px;
            color: #fff;
            font-weight: 500;
            cursor: pointer;
        }

        .control-btn:hover {
            background: #3a3a3a;
            border-color: #4CAF50;
        }

        /* 游戏统计 */
        .game-stats {
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
        }

        .stat-item {
            display: flex;
            justify-content: space-between;
            padding: 0.5rem 0;
            border-bottom: 1px solid #333;
        }

        .stat-item:last-child {
            border-bottom: none;
        }

        /* 手机虚拟控制 */
        .mobile-controls {
            display: none;
            margin-top: 1rem;
        }

        .virtual-dpad {
            display: grid;
            grid-template-areas: 
                ". up ."
                "left . right"
                ". down .";
            gap: 10px;
            justify-content: center;
        }

        .dpad-btn {
            width: 60px;
            height: 60px;
            border: none;
            border-radius: 50%;
            background: #333;
            color: white;
            font-size: 24px;
            cursor: pointer;
            touch-action: manipulation;
        }

        .dpad-btn.up { grid-area: up; }
        .dpad-btn.down { grid-area: down; }
        .dpad-btn.left { grid-area: left; }
        .dpad-btn.right { grid-area: right; }

        .dpad-btn:active {
            background: #4CAF50;
        }

        /* 响应式设计 */
        @media (max-width: 1024px) {
            .game-main {
                flex-direction: column;
            }
            
            .left-panel, .right-panel {
                width: 100%;
            }
            
            .score-panel {
                padding: 1rem 2rem;
            }
            
            .skin-selector {
                grid-template-columns: repeat(4, 1fr);
            }
        }

        @media (max-width: 768px) {
            .game-title {
                font-size: 2rem;
            }
            
            .canvas-container {
                max-width: 95vw;
            }
            
            .score-panel {
                padding: 1rem 1.5rem;
                gap: 1.5rem;
            }
            
            .score-item {
                min-width: 80px;
            }
            
            .score-value {
                font-size: 2rem;
            }
            
            .mobile-controls {
                display: block;
            }
            
            .skin-selector {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        @media (max-width: 480px) {
            .game-app {
                padding: 0.5rem;
            }
            
            .game-title {
                font-size: 1.8rem;
            }
            
            .score-panel {
                flex-direction: column;
                gap: 1rem;
                padding: 1rem;
            }
            
            .score-item {
                min-width: auto;
            }
        }
    </style>
</head>
<body>
    <div class="game-app">
        <!-- 头部 -->
        <header class="game-header">
            <h1 class="game-title">🐍 贪吃蛇游戏</h1>
            <p class="game-subtitle">经典玩法 + AI对战 + 皮肤系统 + 手机优化</p>
        </header>

        <!-- 主游戏区域 -->
        <main class="game-main">
            <!-- 左侧面板：游戏模式选择 -->
            <div class="left-panel">
                <!-- 游戏模式选择 -->
                <div class="panel-section">
                    <h3 class="panel-title">🎮 游戏模式</h3>
                    <div class="mode-selector">
                        <button class="mode-btn active" data-mode="single">单人模式</button>
                        <button class="mode-btn" data-mode="ai">AI对战模式</button>
                        <button class="mode-btn" data-mode="multiplayer">多人模式（开发中）</button>
                    </div>
                </div>

                <!-- 皮肤选择 -->
                <div class="panel-section">
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

                <!-- AI难度选择（仅AI模式显示） -->
                <div class="panel-section" id="ai-difficulty-section" style="display: none;">
                    <h3 class="panel-title">🤖 AI难度</h3>
                    <div class="mode-selector">
                        <button class="mode-btn" data-difficulty="easy">简单</button>
                        <button class="mode-btn" data-difficulty="medium">中等</button>
                        <button class="mode-btn" data-difficulty="hard">困难</button>
                    </div>
                </div>
            </div>

            <!-- 中间游戏区域 -->
            <div class="game-center">
                <!-- 游戏画布 -->
                <div class="canvas-container">
                    <canvas id="gameCanvas"></canvas>
                    
                    <!-- 游戏状态覆盖层 -->
                    <div id="gameOverlay" class="game-overlay">
                        <h2 id="overlayTitle" class="overlay-title">贪吃蛇游戏</h2>
                        <p id="overlayText" class="overlay-text">选择模式后点击开始游戏</p>
                        <button id="startBtn" class="btn btn-primary">开始游戏</button>
                    </div>
                </div>

                <!-- 分数面板 -->
                <div class="score-panel">
                    <div class="score-item">
                        <div class="score-label">分数</div>
                        <div id="scoreDisplay" class="score-value">0</div>
                    </div>
                    <div class="score-item">
                        <div class="score-label">长度</div>
                        <div id="lengthDisplay" class="score-value">1</div>
                    </div>
                    <div class="score-item">
                        <div class="score-label">最高分</div>
                        <div id="highScoreDisplay" class="score-value">0</div>
                    </div>
                </div>

                <!-- 手机虚拟控制 -->
                <div class="mobile-controls">
                    <div class="virtual-dpad">
                        <button class="dpad-btn up">↑</button>
                        <button class="dpad-btn down">↓</button>
                        <button class="dpad-btn left">←</button>
                        <button class="dpad-btn right">→</button>
                    </div>
                </div>
            </div>

            <!-- 右侧面板：控制面板 -->
            <div class="right-panel">
                <!-- 控制按钮 -->
                <div class="panel-section">
                    <h3 class="panel-title">🎯 游戏控制</h3>
                    <div class="control-buttons">
                        <button id="pauseBtn" class="control-btn">暂停游戏</button>
                        <button id="restartBtn" class="control-btn">重新开始</button>
                        <button id="settingsBtn" class="control-btn">游戏设置</button>
                    </div>
                </div>

                <!-- 游戏统计 -->
                <div class="panel-section">
                    <h3 class="panel-title">📊 游戏统计</h3>
                    <div class="game-stats">
                        <div class="stat-item">
                            <span>游戏时间</span>
                            <span id="gameTime">00:00</span>
                        </div>
                        <div class="stat-item">
                            <span>食物数量</span>
                            <span id="foodCount">0</span>
                        </div>
                        <div class="stat-item">
                            <span>当前模式</span>
                            <span id="currentMode">单人</span>
                        </div>
                    </div>
                </div>

                <!-- 操作说明 -->
                <div class="panel-section">
                    <h3 class="panel-title">📱 操作说明</h3>
                    <p style="font-size: 0.9rem; line-height: 1.5;">
                        电脑：方向键 或 WASD<br>
                        手机：滑动屏幕 或 使用虚拟按键
                    </p>
                </div>
            </div>
        </main>
    </div>

    <script>
    // ==================== 游戏配置 ====================
    const CONFIG = {
        GRID_SIZE: 20,
        INITIAL_SPEED: 150,
        FOOD_SCORE: 10,
        AI_SPEEDS: {
            easy: 300,
            medium: 200,
            hard: 100
        }
    };

    // ==================== 游戏状态 ====================
    const GameState = {
        // DOM元素
        elements: {},
        
        // 游戏对象
        canvas: null,
        ctx: null,
        
        // 玩家蛇
        playerSnake: [],
        playerDirection: { dx: 0, dy: 0 },
        
        // AI蛇（AI模式）
        aiSnake: [],
        aiDirection: { dx: 0, dy: 0 },
        aiDifficulty: 'medium',
        
        // 游戏状态
        food: { x: 0, y: 0 },
        score: 0,
        highScore: localStorage.getItem('snakeHighScore') || 0,
        length: 1,
        isPaused: true,
        isGameOver: true,
        gameMode: 'single', // 'single', 'ai', 'multiplayer'
        
        // 游戏循环
        gameLoop: null,
        startTime: 0,
        elapsedTime: 0,
        foodCount: 0,
        
        // 皮肤系统
        currentSkin: 'classic',
        skins: {
            classic: {
                snakeHead: '#4CAF50',
                snakeBody: '#8BC34A',
                snakeTail: '#2E7D32',
                food: '#FF5252',
                foodGlow: 'rgba(255, 82, 82, 0.5)',
                bg: '#111111'
            },
            neon: {
                snakeHead: '#00bcd4',
                snakeBody: '#e040fb',
                snakeTail: '#7b1fa2',
                food: '#ffeb3b',
                foodGlow: 'rgba(255, 235, 59, 0.5)',
                bg: '#0a0a1a'
            },
            pixel: {
                snakeHead: '#ff9800',
                snakeBody: '#ff5722',
                snakeTail: '#d84315',
                food: '#2196f3',
                foodGlow: 'rgba(33, 150, 243, 0.5)',
                bg: '#1a1a1a'
            },
            nature: {
                snakeHead: '#795548',
                snakeBody: '#4caf50',
                snakeTail: '#2e7d32',
                food: '#ff7043',
                foodGlow: 'rgba(255, 112, 67, 0.5)',
                bg: '#0f2a1f'
            }
        },
        
        // 触摸控制
        touchStartX: 0,
        touchStartY: 0
    };

    // ==================== 初始化游戏 ====================
    function initGame() {
        console.log('🎮 初始化贪吃蛇游戏...');
        
        // 获取DOM元素
        getDOMElements();
        
        // 初始化Canvas
        initCanvas();
        
        // 显示最高分
        GameState.elements.highScoreDisplay.textContent = GameState.highScore;
        
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
            scoreDisplay: document.getElementById('scoreDisplay'),
            lengthDisplay: document.getElementById('lengthDisplay'),
            highScoreDisplay: document.getElementById('highScoreDisplay'),
            
            // 按钮
            startBtn: document.getElementById('startBtn'),
            pauseBtn: document.getElementById('pauseBtn'),
            restartBtn: document.getElementById('restartBtn'),
            
            // 统计信息
            gameTime: document.getElementById('gameTime'),
            foodCount: document.getElementById('foodCount'),
            currentMode: document.getElementById('currentMode'),
            
            // 模式选择
            modeButtons: document.querySelectorAll('.mode-btn'),
            aiDifficultySection: document.getElementById('ai-difficulty-section'),
            difficultyButtons: document.querySelectorAll('[data-difficulty]'),
            
            // 皮肤选择
            skinButtons: document.querySelectorAll('.skin-btn'),
            
            // 虚拟控制
            dpadButtons: document.querySelectorAll('.dpad-btn')
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
                GameState.elements.currentMode.textContent = 
                    this.dataset.mode === 'single' ? '单人' : 
                    this.dataset.mode === 'ai' ? 'AI对战' : '多人';
                
                // 显示/隐藏AI难度选择
                if (this.dataset.mode === 'ai') {
                    GameState.elements.aiDifficultySection.style.display = 'block';
                } else {
                    GameState.elements.aiDifficultySection.style.display = 'none';
                }
                
                // 重置游戏
                resetGame();
            });
        });
        
        // AI难度选择
        GameState.elements.difficultyButtons.forEach(btn => {
            btn.addEventListener('click', function() {
                // 移除所有active
                GameState.elements.difficultyButtons.forEach(b => b.classList.remove('active'));
                // 设置当前active
                this.classList.add('active');
                // 更新AI难度
                GameState.aiDifficulty = this.dataset.difficulty;
            });
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
                this.style.background = '';
            });
            
            btn.addEventListener('mousedown', function() {
                const direction = this.textContent;
                handleDirection(direction);
                this.style.background = '#4CAF50';
            });
            
            btn.addEventListener('mouseup', function() {
                this.style.background = '';
            });
        });
        
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
                // 横向滑动
                if (deltaX > 0) handleDirection('→');
                else handleDirection('←');
            } else {
                // 纵向滑动
                if (deltaY > 0) handleDirection('↓');
                else handleDirection('↑');
            }
            
            GameState.touchStartX = 0;
            e.preventDefault();
        }, { passive: false });
        
        // 阻止触摸滚动
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
                if (GameState.playerDirection.dy !== 1) {
                    GameState.playerDirection = { dx: 0, dy: -1 };
                }
                break;
            case '↓':
            case 'ArrowDown':
                if (GameState.playerDirection.dy !== -1) {
                    GameState.playerDirection = { dx: 0, dy: 1 };
                }
                break;
            case '←':
            case 'ArrowLeft':
                if (GameState.playerDirection.dx !== 1) {
                    GameState.playerDirection = { dx: -1, dy: 0 };
                }
                break;
            case '→':
            case 'ArrowRight':
                if (GameState.playerDirection.dx !== -1) {
                    GameState.playerDirection = { dx: 1, dy: 0 };
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
        console.log('🎮 开始游戏，模式:', GameState.gameMode);
        
        if (GameState.isGameOver) {
            resetGame();
            GameState.isGameOver = false;
        }
        
        if (GameState.isPaused) {
            GameState.isPaused = false;
            GameState.startTime = Date.now() - GameState.elapsedTime;
            GameState.gameLoop = setInterval(gameUpdate, CONFIG.INITIAL_SPEED);
            
            // 更新UI
            GameState.elements.gameOverlay.style.display = 'none';
            GameState.elements.startBtn.textContent = '游戏中...';
            GameState.elements.canvas.focus();
            
            // AI模式初始化AI蛇
            if (GameState.gameMode === 'ai') {
                initAISnake();
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
            GameState.gameLoop = setInterval(gameUpdate, CONFIG.INITIAL_SPEED);
            GameState.elements.gameOverlay.style.display = 'none';
            GameState.elements.startBtn.textContent = '游戏中...';
        }
    }

    function resetGame() {
        console.log('🎮 重置游戏');
        
        clearInterval(GameState.gameLoop);
        GameState.isPaused = true;
        GameState.isGameOver = true;
        
        // 重置玩家蛇
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        const center = Math.floor(gridCount / 2);
        GameState.playerSnake = [{ x: center, y: center }];
        GameState.playerDirection = { dx: 0, dy: 0 };
        
        // 重置AI蛇
        GameState.aiSnake = [];
        GameState.aiDirection = { dx: 0, dy: 0 };
        
        // 生成食物
        generateFood();
        
        // 重置状态
        GameState.score = 0;
        GameState.length = 1;
        GameState.foodCount = 0;
        GameState.elapsedTime = 0;
        
        // 更新显示
        updateDisplay();
        draw();
        
        // 显示开始界面
        showOverlay('贪吃蛇游戏', '选择模式后点击开始游戏');
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
        moveSnake(GameState.playerSnake, GameState.playerDirection);
        
        // AI模式：移动AI蛇
        if (GameState.gameMode === 'ai') {
            updateAISnake();
        }
        
        // 检查碰撞
        if (checkCollision(GameState.playerSnake)) {
            gameOver();
            return;
        }
        
        // AI模式：检查AI蛇碰撞
        if (GameState.gameMode === 'ai' && checkCollision(GameState.aiSnake)) {
            // AI蛇死亡，玩家得分
            GameState.score += 50;
            initAISnake();
        }
        
        // 更新显示
        updateDisplay();
        draw();
    }

    // 移动蛇
    function moveSnake(snake, direction) {
        if (direction.dx === 0 && direction.dy === 0) return;
        
        const head = { 
            x: snake[0].x + direction.dx, 
            y: snake[0].y + direction.dy 
        };
        snake.unshift(head);
        
        // 检查是否吃到食物
        if (head.x === GameState.food.x && head.y === GameState.food.y) {
            GameState.score += CONFIG.FOOD_SCORE;
            GameState.length = snake.length;
            GameState.foodCount++;
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
            for (const segment of GameState.playerSnake) {
                if (segment.x === newFood.x && segment.y === newFood.y) {
                    onSnake = true;
                    break;
                }
            }
            
            // 检查是否在AI蛇身上
            if (GameState.gameMode === 'ai') {
                for (const segment of GameState.aiSnake) {
                    if (segment.x === newFood.x && segment.y === newFood.y) {
                        onSnake = true;
                        break;
                    }
                }
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
        console.log('🎮 游戏结束，得分:', GameState.score);
        
        clearInterval(GameState.gameLoop);
        GameState.isGameOver = true;
        GameState.isPaused = true;
        
        // 更新最高分
        if (GameState.score > GameState.highScore) {
            GameState.highScore = GameState.score;
            localStorage.setItem('snakeHighScore', GameState.highScore);
            GameState.elements.highScoreDisplay.textContent = GameState.highScore;
        }
        
        showOverlay('游戏结束', `得分: ${GameState.score}<br>长度: ${GameState.length}<br>时间: ${formatTime(GameState.elapsedTime)}`);
        GameState.elements.startBtn.textContent = '重新开始';
    }

    // ==================== AI对战系统 ====================
    function initAISnake() {
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        const center = Math.floor(gridCount / 2);
        
        // 将AI蛇放在与玩家对称的位置
        GameState.aiSnake = [
            { x: center + 5, y: center + 5 }
        ];
        GameState.aiDirection = { dx: 1, dy: 0 };
    }

    function updateAISnake() {
        // 简单的AI逻辑：随机移动，有一定概率朝食物移动
        if (GameState.aiSnake.length === 0) return;
        
        const aiHead = GameState.aiSnake[0];
        
        // 30%概率朝食物移动，70%概率随机移动
        if (Math.random() < 0.3) {
            // 朝食物移动
            if (aiHead.x < GameState.food.x && GameState.aiDirection.dx !== -1) {
                GameState.aiDirection = { dx: 1, dy: 0 };
            } else if (aiHead.x > GameState.food.x && GameState.aiDirection.dx !== 1) {
                GameState.aiDirection = { dx: -1, dy: 0 };
            } else if (aiHead.y < GameState.food.y && GameState.aiDirection.dy !== -1) {
                GameState.aiDirection = { dx: 0, dy: 1 };
            } else if (aiHead.y > GameState.food.y && GameState.aiDirection.dy !== 1) {
                GameState.aiDirection = { dx: 0, dy: -1 };
            }
        } else {
            // 随机移动
            const directions = [
                { dx: 1, dy: 0 },
                { dx: -1, dy: 0 },
                { dx: 0, dy: 1 },
                { dx: 0, dy: -1 }
            ];
            
            // 避免直接掉头
            const validDirections = directions.filter(dir => 
                !(dir.dx === -GameState.aiDirection.dx && dir.dy === -GameState.aiDirection.dy)
            );
            
            GameState.aiDirection = validDirections[Math.floor(Math.random() * validDirections.length)];
        }
        
        // 根据难度调整AI速度
        const aiSpeed = CONFIG.AI_SPEEDS[GameState.aiDifficulty] || CONFIG.AI_SPEEDS.medium;
        
        // 控制AI移动速度
        if (Date.now() % aiSpeed < CONFIG.INITIAL_SPEED) {
            moveSnake(GameState.aiSnake, GameState.aiDirection);
        }
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
        drawSnake(GameState.playerSnake, skin.snakeHead, skin.snakeBody, skin.snakeTail);
        
        // 绘制AI蛇（AI模式）
        if (GameState.gameMode === 'ai' && GameState.aiSnake.length > 0) {
            drawSnake(GameState.aiSnake, '#9C27B0', '#7B1FA2', '#4A148C');
        }
        
        // 绘制食物
        ctx.fillStyle = skin.food;
        ctx.beginPath();
        const centerX = GameState.food.x * cellSize + cellSize / 2;
        const centerY = GameState.food.y * cellSize + cellSize / 2;
        ctx.arc(centerX, centerY, cellSize / 2 - 2, 0, Math.PI * 2);
        ctx.fill();
        
        // 食物发光效果
        ctx.shadowColor = skin.foodGlow;
        ctx.shadowBlur = 10;
        ctx.fill();
        ctx.shadowBlur = 0;
    }

    // 绘制蛇
    function drawSnake(snake, headColor, bodyColor, tailColor) {
        const cellSize = CONFIG.GRID_SIZE;
        const ctx = GameState.ctx;
        
        snake.forEach((segment, index) => {
            if (index === 0) {
                // 蛇头
                ctx.fillStyle = headColor;
            } else if (index === snake.length - 1) {
                // 蛇尾
                ctx.fillStyle = tailColor;
            } else {
                // 蛇身
                ctx.fillStyle = bodyColor;
            }
            
            ctx.fillRect(
                segment.x * cellSize + 1,
                segment.y * cellSize + 1,
                cellSize - 2,
                cellSize - 2
            );
        });
    }

    // ==================== UI更新 ====================
    function updateDisplay() {
        GameState.elements.scoreDisplay.textContent = GameState.score;
        GameState.elements.lengthDisplay.textContent = GameState.length;
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
