---
layout: default
title: 🐍 贪吃蛇游戏
permalink: games/snake-game/
---

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>🐍 贪吃蛇游戏 - 智能AI版</title>
    <style>
        /* 全局重置 */
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
            background: #1a1a1a;
            color: #fff;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
        }

        /* 游戏容器 */
        .game-container {
            width: 100%;
            height: 100vh;
            display: flex;
            flex-direction: column;
            padding: 0.5rem;
        }

        /* 头部 */
        .game-header {
            text-align: center;
            padding: 0.5rem 0;
            margin-bottom: 0.5rem;
        }

        .game-title {
            font-size: 1.8rem;
            color: #4CAF50;
            margin-bottom: 0.3rem;
        }

        .game-subtitle {
            font-size: 0.9rem;
            color: #888;
        }

        /* 控制面板 */
        .control-panel {
            display: flex;
            justify-content: center;
            gap: 0.5rem;
            margin-bottom: 0.5rem;
            flex-wrap: wrap;
        }

        .control-btn {
            padding: 0.5rem 1rem;
            border: 1px solid #444;
            border-radius: 6px;
            background: #333;
            color: #fff;
            font-size: 0.9rem;
            cursor: pointer;
        }

        .control-btn.active {
            background: #4CAF50;
            border-color: #4CAF50;
        }

        /* 分数面板 */
        .score-panel {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            margin-bottom: 0.8rem;
            background: rgba(0, 0, 0, 0.3);
            padding: 0.8rem;
            border-radius: 8px;
        }

        .score-item {
            text-align: center;
        }

        .score-label {
            font-size: 0.8rem;
            color: #aaa;
            margin-bottom: 0.2rem;
        }

        .score-value {
            font-size: 1.4rem;
            font-weight: bold;
        }

        /* 游戏区域 */
        .game-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .canvas-container {
            position: relative;
            width: 100%;
            max-width: 600px;  /* 电脑端更大的画布 */
            aspect-ratio: 1/1;
            border-radius: 10px;
            overflow: hidden;
            background: #000;
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.6);
        }

        #gameCanvas {
            width: 100%;
            height: 100%;
            display: block;
        }

        /* 控制按钮 */
        .action-buttons {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin: 1rem 0;
        }

        .action-btn {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 8px;
            background: #333;
            color: #fff;
            font-size: 1rem;
            cursor: pointer;
            min-width: 120px;
        }

        .action-btn.primary {
            background: #4CAF50;
        }

        /* AI设置面板 */
        .ai-settings {
            display: none;
            background: rgba(0, 0, 0, 0.8);
            padding: 1rem;
            border-radius: 8px;
            margin: 0.5rem auto;
            max-width: 400px;
        }

        .ai-settings.active {
            display: block;
        }

        .setting-group {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.8rem;
        }

        .setting-label {
            font-size: 0.9rem;
        }

        .slider {
            width: 150px;
            height: 6px;
            border-radius: 3px;
            background: #333;
            outline: none;
        }

        /* 虚拟按键 - 只在移动端显示 */
        .virtual-controls {
            display: none; /* 默认隐藏 */
            position: fixed;
            bottom: 20px;
            left: 0;
            right: 0;
            flex-direction: column;
            align-items: center;
            z-index: 100;
        }

        .dpad-container {
            display: grid;
            grid-template-areas: 
                ". up ."
                "left . right"
                ". down .";
            gap: 12px;
            margin-bottom: 10px;
        }

        .dpad-btn {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: rgba(76, 175, 80, 0.9);
            border: 2px solid #fff;
            color: #fff;
            font-size: 1.8rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            touch-action: manipulation;
        }

        .dpad-btn:active {
            background: rgba(255, 255, 255, 0.9);
            color: #000;
        }

        .dpad-btn.up { grid-area: up; }
        .dpad-btn.down { grid-area: down; }
        .dpad-btn.left { grid-area: left; }
        .dpad-btn.right { grid-area: right; }

        /* 电脑端优化 */
        @media (min-width: 768px) {
            .canvas-container {
                max-width: 500px;
            }
            
            .game-title {
                font-size: 2.2rem;
            }
            
            .score-value {
                font-size: 1.8rem;
            }
        }

        /* 手机端优化 */
        @media (max-width: 480px) {
            .canvas-container {
                max-width: 95vw;
            }
            
            .virtual-controls {
                display: flex; /* 在手机上显示虚拟按键 */
            }
            
            .dpad-btn {
                width: 60px;
                height: 60px;
                font-size: 1.5rem;
            }
            
            .action-btn {
                min-width: 100px;
                padding: 0.7rem 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <!-- 头部 -->
        <header class="game-header">
            <h1 class="game-title">🐍 贪吃蛇AI对战</h1>
            <p class="game-subtitle">挑战智能AI，体验极致操作</p>
        </header>

        <!-- 控制面板 -->
        <div class="control-panel">
            <button class="control-btn active" data-mode="single">单人模式</button>
            <button class="control-btn" data-mode="ai">AI对战</button>
        </div>

        <!-- 分数面板 -->
        <div class="score-panel">
            <div class="score-item">
                <div class="score-label">你的分数</div>
                <div class="score-value" id="playerScore">0</div>
            </div>
            <div class="score-item">
                <div class="score-label">你的长度</div>
                <div class="score-value" id="playerLength">1</div>
            </div>
            <div class="score-item">
                <div class="score-label">最高分</div>
                <div class="score-value" id="highScore">0</div>
            </div>
        </div>

        <!-- AI设置 -->
        <div class="ai-settings" id="aiSettings">
            <div class="setting-group">
                <span class="setting-label">AI数量</span>
                <input type="range" min="1" max="5" value="3" class="slider" id="aiCount">
                <span id="aiCountValue">3</span>
            </div>
            <div class="setting-group">
                <span class="setting-label">AI难度</span>
                <input type="range" min="1" max="5" value="3" class="slider" id="aiDifficulty">
                <span id="aiDifficultyValue">中等</span>
            </div>
        </div>

        <!-- 游戏区域 -->
        <div class="game-area">
            <div class="canvas-container">
                <canvas id="gameCanvas"></canvas>
            </div>
            
            <div class="action-buttons">
                <button class="action-btn primary" id="startBtn">开始游戏</button>
                <button class="action-btn" id="pauseBtn">暂停</button>
                <button class="action-btn" id="restartBtn">重新开始</button>
            </div>
        </div>

        <!-- 虚拟按键（只在移动端显示） -->
        <div class="virtual-controls" id="virtualControls">
            <div class="dpad-container">
                <button class="dpad-btn up">↑</button>
                <button class="dpad-btn down">↓</button>
                <button class="dpad-btn left">←</button>
                <button class="dpad-btn right">→</button>
            </div>
        </div>
    </div>

    <script>
    // ==================== 游戏配置 ====================
    const CONFIG = {
        GRID_SIZE: 20,
        INITIAL_SPEED: 150,
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
            snakes: [],
            difficulty: 3,
            count: 3,
            colors: ['#FF5252', '#2196F3', '#FF9800', '#9C27B0', '#00BCD4']
        },
        
        // 游戏状态
        food: { x: 0, y: 0 },
        highScore: localStorage.getItem('snakeHighScore') || 0,
        isPaused: true,
        isGameOver: true,
        gameMode: 'single',
        gameLoop: null,
        startTime: 0,
        elapsedTime: 0,
        foodCount: 0
    };

    // ==================== 初始化游戏 ====================
    function initGame() {
        console.log('🎮 初始化游戏...');
        
        // 获取DOM元素
        getDOMElements();
        
        // 初始化Canvas
        initCanvas();
        
        // 显示最高分
        GameState.elements.highScore.textContent = GameState.highScore;
        
        // 检测设备类型，控制虚拟按键显示
        detectDevice();
        
        // 绑定事件
        setupEventListeners();
        
        // 初始化游戏状态
        resetGame();
        
        // 初始绘制
        draw();
        
        console.log('🎮 游戏初始化完成！');
    }

    // 检测设备类型
    function detectDevice() {
        const isTouchDevice = 'ontouchstart' in window || 
                             navigator.maxTouchPoints > 0 ||
                             navigator.msMaxTouchPoints > 0;
        const isMobile = window.innerWidth < 768;
        
        // 只在触摸设备且屏幕较小时显示虚拟按键
        if (isTouchDevice && isMobile) {
            document.getElementById('virtualControls').style.display = 'flex';
        }
    }

    // 获取DOM元素
    function getDOMElements() {
        GameState.elements = {
            // Canvas
            canvas: document.getElementById('gameCanvas'),
            
            // 分数显示
            playerScore: document.getElementById('playerScore'),
            playerLength: document.getElementById('playerLength'),
            highScore: document.getElementById('highScore'),
            
            // 按钮
            startBtn: document.getElementById('startBtn'),
            pauseBtn: document.getElementById('pauseBtn'),
            restartBtn: document.getElementById('restartBtn'),
            
            // 模式选择
            modeButtons: document.querySelectorAll('.control-btn'),
            aiSettings: document.getElementById('aiSettings'),
            
            // AI设置
            aiCount: document.getElementById('aiCount'),
            aiCountValue: document.getElementById('aiCountValue'),
            aiDifficulty: document.getElementById('aiDifficulty'),
            aiDifficultyValue: document.getElementById('aiDifficultyValue'),
            
            // 虚拟按键
            virtualControls: document.getElementById('virtualControls'),
            dpadButtons: document.querySelectorAll('.dpad-btn')
        };
        
        // 获取Canvas上下文
        GameState.ctx = GameState.elements.canvas.getContext('2d');
    }

    // 初始化Canvas
    function initCanvas() {
        const canvas = GameState.elements.canvas;
        const container = canvas.parentElement;
        
        // 根据屏幕大小设置画布尺寸
        const maxSize = Math.min(window.innerWidth, window.innerHeight) * 0.85;
        const size = Math.min(600, maxSize);
        
        canvas.width = size;
        canvas.height = size;
        
        // 设置焦点
        canvas.setAttribute('tabindex', '0');
        canvas.focus();
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
                GameState.elements.modeButtons.forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                GameState.gameMode = this.dataset.mode;
                
                // 显示/隐藏AI设置
                if (this.dataset.mode === 'ai') {
                    GameState.elements.aiSettings.classList.add('active');
                } else {
                    GameState.elements.aiSettings.classList.remove('active');
                }
                
                resetGame();
            });
        });
        
        // AI设置
        GameState.elements.aiCount.addEventListener('input', function() {
            const value = parseInt(this.value);
            GameState.elements.aiCountValue.textContent = value;
            GameState.ai.count = value;
            if (GameState.gameMode === 'ai') {
                initAISnakes();
                draw();
            }
        });
        
        GameState.elements.aiDifficulty.addEventListener('input', function() {
            const value = parseInt(this.value);
            const difficulties = ['极简', '简单', '中等', '困难', '专家'];
            GameState.elements.aiDifficultyValue.textContent = difficulties[value - 1];
            GameState.ai.difficulty = value;
        });
        
        // 虚拟按键
        GameState.elements.dpadButtons.forEach(btn => {
            btn.addEventListener('touchstart', function(e) {
                e.preventDefault();
                handleDPad(this.textContent);
                this.style.background = '#fff';
                this.style.color = '#000';
            });
            
            btn.addEventListener('touchend', function(e) {
                e.preventDefault();
                this.style.background = '';
                this.style.color = '';
            });
        });
        
        // Canvas点击获取焦点
        GameState.elements.canvas.addEventListener('click', function() {
            this.focus();
        });
        
        // 窗口大小变化时重新调整
        window.addEventListener('resize', function() {
            initCanvas();
            draw();
        });
    }

    // 处理虚拟按键
    function handleDPad(direction) {
        if (GameState.isPaused && !GameState.isGameOver) return;
        
        switch(direction) {
            case '↑':
                if (GameState.player.direction.dy !== 1) {
                    GameState.player.direction = { dx: 0, dy: -1 };
                }
                break;
            case '↓':
                if (GameState.player.direction.dy !== -1) {
                    GameState.player.direction = { dx: 0, dy: 1 };
                }
                break;
            case '←':
                if (GameState.player.direction.dx !== 1) {
                    GameState.player.direction = { dx: -1, dy: 0 };
                }
                break;
            case '→':
                if (GameState.player.direction.dx !== -1) {
                    GameState.player.direction = { dx: 1, dy: 0 };
                }
                break;
        }
    }

    // 键盘控制
    function handleKeyDown(e) {
        if (GameState.isPaused && !GameState.isGameOver) return;
        
        switch(e.key.toLowerCase()) {
            case 'arrowup':
            case 'w':
                if (GameState.player.direction.dy !== 1) {
                    GameState.player.direction = { dx: 0, dy: -1 };
                }
                break;
            case 'arrowdown':
            case 's':
                if (GameState.player.direction.dy !== -1) {
                    GameState.player.direction = { dx: 0, dy: 1 };
                }
                break;
            case 'arrowleft':
            case 'a':
                if (GameState.player.direction.dx !== 1) {
                    GameState.player.direction = { dx: -1, dy: 0 };
                }
                break;
            case 'arrowright':
            case 'd':
                if (GameState.player.direction.dx !== -1) {
                    GameState.player.direction = { dx: 1, dy: 0 };
                }
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
            GameState.startTime = Date.now();
            GameState.gameLoop = setInterval(gameUpdate, CONFIG.INITIAL_SPEED);
            
            GameState.elements.startBtn.textContent = '游戏中...';
            GameState.elements.canvas.focus();
            
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
            GameState.elements.startBtn.textContent = '继续游戏';
        } else {
            GameState.gameLoop = setInterval(gameUpdate, CONFIG.INITIAL_SPEED);
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
        
        GameState.elements.startBtn.textContent = '开始游戏';
    }

    // ==================== 游戏逻辑 ====================
    function gameUpdate() {
        if (GameState.isPaused || GameState.isGameOver) return;
        
        // 移动玩家
        moveSnake(GameState.player.snake, GameState.player.direction, true);
        
        // 更新AI
        if (GameState.gameMode === 'ai') {
            updateAISnakes();
        }
        
        // 检查碰撞
        if (checkCollision(GameState.player.snake)) {
            gameOver();
            return;
        }
        
        // 检查AI碰撞
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
        
        // 撞自己
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
        
        GameState.elements.startBtn.textContent = '重新开始';
    }

    // ==================== AI系统 ====================
    function initAISnakes() {
        GameState.ai.snakes = [];
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        
        for (let i = 0; i < GameState.ai.count; i++) {
            const aiSnake = {
                snake: [],
                direction: { dx: 1, dy: 0 },
                color: GameState.ai.colors[i % GameState.ai.colors.length],
                lastMove: 0,
                moveDelay: Math.max(100, 300 - (GameState.ai.difficulty * 50)),
                strategy: Math.floor(Math.random() * 3) // 0=食物,1=玩家,2=随机
            };
            
            // 找到安全位置
            let pos = findSafePosition();
            if (pos) {
                aiSnake.snake = [{ x: pos.x, y: pos.y }];
                GameState.ai.snakes.push(aiSnake);
            }
        }
    }

    function findSafePosition() {
        const gridCount = Math.floor(GameState.elements.canvas.width / CONFIG.GRID_SIZE);
        const maxAttempts = 100;
        
        for (let attempt = 0; attempt < maxAttempts; attempt++) {
            const x = Math.floor(Math.random() * (gridCount - 4)) + 2;
            const y = Math.floor(Math.random() * (gridCount - 4)) + 2;
            
            let safe = true;
            
            // 检查玩家蛇
            for (const segment of GameState.player.snake) {
                if (segment.x === x && segment.y === y) {
                    safe = false;
                    break;
                }
            }
            
            // 检查其他AI蛇
            for (const aiSnake of GameState.ai.snakes) {
                for (const segment of aiSnake.snake) {
                    if (segment.x === x && segment.y === y) {
                        safe = false;
                        break;
                    }
                }
                if (!safe) break;
            }
            
            if (safe) return { x, y };
        }
        
        return null;
    }

    function updateAISnakes() {
        const now = Date.now();
        
        for (let i = GameState.ai.snakes.length - 1; i >= 0; i--) {
            const aiSnake = GameState.ai.snakes[i];
            
            if (now - aiSnake.lastMove >= aiSnake.moveDelay) {
                // 智能AI决策
                makeAIDecision(aiSnake, i);
                moveSnake(aiSnake.snake, aiSnake.direction, false);
                aiSnake.lastMove = now;
                
                // 检查AI蛇是否碰撞
                if (checkCollision(aiSnake.snake)) {
                    GameState.player.score += CONFIG.AI_KILL_SCORE;
                    GameState.ai.snakes.splice(i, 1);
                }
            }
        }
    }

    function makeAIDecision(aiSnake, aiIndex) {
        const head = aiSnake.snake[0];
        const directions = [
            { dx: 1, dy: 0 },
            { dx: -1, dy: 0 },
            { dx: 0, dy: 1 },
            { dx: 0, dy: -1 }
        ];
        
        // 避免掉头
        const validDirections = directions.filter(dir => 
            !(dir.dx === -aiSnake.direction.dx && dir.dy === -aiSnake.direction.dy)
        );
        
        // 根据难度和策略选择方向
        let chosenDirection = null;
        
        if (aiSnake.strategy === 0 || GameState.ai.difficulty >= 4) {
            // 追踪食物策略
            chosenDirection = moveTowards(head, GameState.food, validDirections);
        } else if (aiSnake.strategy === 1 && GameState.ai.difficulty >= 3) {
            // 追踪玩家策略
            if (GameState.player.snake.length > 0) {
                chosenDirection = moveTowards(head, GameState.player.snake[0], validDirections);
            }
        }
        
        // 如果还没有选择方向，随机选择
        if (!chosenDirection && validDirections.length > 0) {
            chosenDirection = validDirections[Math.floor(Math.random() * validDirections.length)];
        }
        
        if (chosenDirection) {
            aiSnake.direction = chosenDirection;
        }
    }

    function moveTowards(from, to, validDirections) {
        const dx = to.x - from.x;
        const dy = to.y - from.y;
        
        let bestDirection = null;
        let bestDistance = Infinity;
        
        for (const dir of validDirections) {
            const newX = from.x + dir.dx;
            const newY = from.y + dir.dy;
            const distance = Math.abs(to.x - newX) + Math.abs(to.y - newY);
            
            if (distance < bestDistance) {
                bestDistance = distance;
                bestDirection = dir;
            }
        }
        
        return bestDirection;
    }

    function checkAICollisions() {
        for (let i = GameState.ai.snakes.length - 1; i >= 0; i--) {
            const aiSnake = GameState.ai.snakes[i];
            const head = aiSnake.snake[0];
            
            // 检查是否撞到玩家
            for (const segment of GameState.player.snake) {
                if (head.x === segment.x && head.y === segment.y) {
                    GameState.player.score += CONFIG.AI_KILL_SCORE;
                    GameState.ai.snakes.splice(i, 1);
                    break;
                }
            }
        }
    }

    // ==================== 渲染系统 ====================
    function draw() {
        const cellSize = CONFIG.GRID_SIZE;
        const ctx = GameState.ctx;
        const canvas = GameState.elements.canvas;
        
        // 清空画布
        ctx.fillStyle = '#111';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        
        // 绘制玩家蛇
        drawSnake(GameState.player.snake, '#4CAF50', true);
        
        // 绘制AI蛇
        for (let i = 0; i < GameState.ai.snakes.length; i++) {
            const aiSnake = GameState.ai.snakes[i];
            drawSnake(aiSnake.snake, aiSnake.color, false);
        }
        
        // 绘制食物
        drawFood();
    }

    function drawSnake(snake, color, isPlayer) {
        const cellSize = CONFIG.GRID_SIZE;
        const ctx = GameState.ctx;
        
        snake.forEach((segment, index) => {
            ctx.fillStyle = color;
            ctx.fillRect(
                segment.x * cellSize + 1,
                segment.y * cellSize + 1,
                cellSize - 2,
                cellSize - 2
            );
            
            // 蛇头特殊标记
            if (index === 0) {
                ctx.fillStyle = isPlayer ? '#000' : '#fff';
                ctx.beginPath();
                ctx.arc(
                    segment.x * cellSize + cellSize / 2,
                    segment.y * cellSize + cellSize / 2,
                    cellSize / 4,
                    0,
                    Math.PI * 2
                );
                ctx.fill();
            }
        });
    }

    function drawFood() {
        const cellSize = CONFIG.GRID_SIZE;
        const ctx = GameState.ctx;
        
        // 食物主体
        ctx.fillStyle = '#FF5252';
        ctx.beginPath();
        ctx.arc(
            GameState.food.x * cellSize + cellSize / 2,
            GameState.food.y * cellSize + cellSize / 2,
            cellSize / 2 - 2,
            0,
            Math.PI * 2
        );
        ctx.fill();
        
        // 发光效果
        ctx.shadowColor = '#FF5252';
        ctx.shadowBlur = 10;
        ctx.fill();
        ctx.shadowBlur = 0;
    }

    // ==================== UI更新 ====================
    function updateDisplay() {
        GameState.elements.playerScore.textContent = GameState.player.score;
        GameState.elements.playerLength.textContent = GameState.player.length;
    }

    // ==================== 启动游戏 ====================
    document.addEventListener('DOMContentLoaded', function() {
        console.log('📄 DOM加载完成，初始化游戏');
        setTimeout(initGame, 100);
    });
    </script>
</body>
</html>
