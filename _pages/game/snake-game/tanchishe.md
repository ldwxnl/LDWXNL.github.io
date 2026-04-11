---
layout: default
title: 🐍 贪吃蛇游戏
permalink: games/snake-game/
---

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <title>🐍 贪吃蛇游戏 - 完美移动端版</title>
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

        /* 游戏容器 */
        .game-app {
            max-width: 100%;
            margin: 0 auto;
            padding: 0.5rem;
            display: flex;
            flex-direction: column;
            height: 100vh;
        }

        /* 游戏标题和模式选择 */
        .game-header {
            text-align: center;
            padding: 0.5rem 0;
            flex-shrink: 0;
        }

        .game-title {
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
            color: #4CAF50;
        }

        .mode-selector {
            display: flex;
            justify-content: center;
            gap: 0.5rem;
            margin-bottom: 0.5rem;
            flex-wrap: wrap;
        }

        .mode-btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 20px;
            background: #333;
            color: #fff;
            font-size: 0.9rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        .mode-btn.active {
            background: #4CAF50;
            color: #000;
        }

        /* 游戏信息面板 */
        .info-panel {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 0.5rem;
            margin-bottom: 0.5rem;
            background: rgba(0, 0, 0, 0.3);
            padding: 0.75rem;
            border-radius: 10px;
            flex-shrink: 0;
        }

        .info-item {
            text-align: center;
            padding: 0.5rem;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 8px;
        }

        .info-label {
            font-size: 0.8rem;
            opacity: 0.8;
            margin-bottom: 0.25rem;
        }

        .info-value {
            font-size: 1.2rem;
            font-weight: bold;
        }

        /* 游戏画布容器 */
        .canvas-container {
            position: relative;
            width: 100%;
            flex-grow: 1;
            min-height: 200px;
            background: #000;
            border-radius: 10px;
            overflow: hidden;
            touch-action: none; /* 防止页面滚动 */
        }

        #gameCanvas {
            width: 100%;
            height: 100%;
            display: block;
        }

        /* 虚拟按键容器 */
        .virtual-controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 1rem 0;
            margin-top: auto; /* 固定在底部 */
            flex-shrink: 0;
        }

        .control-row {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin: 0.5rem 0;
        }

        .control-btn {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: rgba(76, 175, 80, 0.3);
            border: 2px solid #4CAF50;
            color: white;
            font-size: 1.5rem;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.1s;
            -webkit-tap-highlight-color: transparent;
        }

        .control-btn:active {
            background: rgba(76, 175, 80, 0.7);
            transform: scale(0.95);
        }

        /* AI设置面板 */
        .ai-settings {
            margin-top: 1rem;
            padding: 1rem;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 10px;
            display: none;
        }

        .ai-settings.active {
            display: block;
        }

        .setting-group {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.75rem;
        }

        .setting-label {
            font-size: 0.9rem;
        }

        .slider {
            -webkit-appearance: none;
            width: 60%;
            height: 6px;
            border-radius: 3px;
            background: #333;
            outline: none;
        }

        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: #4CAF50;
            cursor: pointer;
        }

        /* 响应式调整 */
        @media (max-width: 480px) {
            .info-panel {
                grid-template-columns: repeat(3, 1fr);
                padding: 0.5rem;
            }
            
            .info-item {
                padding: 0.4rem;
            }
            
            .info-label {
                font-size: 0.7rem;
            }
            
            .info-value {
                font-size: 1rem;
            }
            
            .control-btn {
                width: 50px;
                height: 50px;
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="game-app">
        <!-- 游戏标题和模式选择 -->
        <div class="game-header">
            <h1 class="game-title">🐍 贪吃蛇游戏</h1>
            <div class="mode-selector">
                <button class="mode-btn active" data-mode="single">单人模式</button>
                <button class="mode-btn" data-mode="ai">AI对战</button>
                <button class="mode-btn" data-mode="multi">多人模式</button>
            </div>
        </div>

        <!-- 游戏信息面板 -->
        <div class="info-panel">
            <div class="info-item">
                <div class="info-label">你的分数</div>
                <div class="info-value" id="playerScore">0</div>
            </div>
            <div class="info-item">
                <div class="info-label">你的长度</div>
                <div class="info-value" id="playerLength">1</div>
            </div>
            <div class="info-item">
                <div class="info-label">最高分</div>
                <div class="info-value" id="highScore">0</div>
            </div>
            <div class="info-item">
                <div class="info-label">游戏时间</div>
                <div class="info-value" id="gameTime">00:00</div>
            </div>
            <div class="info-item">
                <div class="info-label">食物数量</div>
                <div class="info-value" id="foodCount">0</div>
            </div>
            <div class="info-item">
                <div class="info-label">存活AI</div>
                <div class="info-value" id="aiAlive">0</div>
            </div>
        </div>

        <!-- 游戏画布容器 -->
        <div class="canvas-container">
            <canvas id="gameCanvas"></canvas>
        </div>

        <!-- 虚拟按键 -->
        <div class="virtual-controls">
            <div class="control-row">
                <div class="control-btn" id="upBtn">↑</div>
            </div>
            <div class="control-row">
                <div class="control-btn" id="leftBtn">←</div>
                <div class="control-btn" id="downBtn">↓</div>
                <div class="control-btn" id="rightBtn">→</div>
            </div>
        </div>

        <!-- AI设置面板 -->
        <div class="ai-settings" id="aiSettings">
            <div class="setting-group">
                <span class="setting-label">AI数量:</span>
                <input type="range" min="1" max="5" value="3" class="slider" id="aiCountSlider">
                <span id="aiCountValue">3</span>
            </div>
            <div class="setting-group">
                <span class="setting-label">AI难度:</span>
                <input type="range" min="1" max="5" value="3" class="slider" id="aiDifficultySlider">
                <span id="aiDifficultyValue">3</span>
            </div>
        </div>
    </div>

    <script>
        // 游戏核心变量
        let canvas, ctx;
        let gameState = {
            mode: 'single', // single, ai, multi
            isRunning: false,
            isPaused: false,
            score: 0,
            highScore: localStorage.getItem('snakeHighScore') || 0,
            gameTime: 0,
            foodCount: 0,
            aiSnakes: [],
            playerSnake: null
        };

        // 初始化游戏
        function initGame() {
            canvas = document.getElementById('gameCanvas');
            ctx = canvas.getContext('2d');
            
            // 设置画布尺寸
            resizeCanvas();
            window.addEventListener('resize', resizeCanvas);
            
            // 初始化玩家蛇
            gameState.playerSnake = createSnake('player', 1);
            
            // 初始化AI蛇（如果是AI模式）
            if (gameState.mode === 'ai') {
                initAISnakes();
            }
            
            // 初始化食物
            spawnFood();
            
            // 绑定事件
            bindEvents();
            
            // 更新UI
            updateUI();
            
            // 开始游戏循环
            gameLoop();
        }

        // 调整画布尺寸
        function resizeCanvas() {
            const container = document.querySelector('.canvas-container');
            canvas.width = container.clientWidth;
            canvas.height = container.clientHeight;
        }

        // 创建蛇
        function createSnake(type, length) {
            const gridSize = Math.min(canvas.width, canvas.height) / 20;
            const startX = Math.floor(Math.random() * (canvas.width / gridSize)) * gridSize;
            const startY = Math.floor(Math.random() * (canvas.height / gridSize)) * gridSize;
            
            return {
                type: type,
                body: [],
                direction: 'right',
                nextDirection: 'right',
                length: length,
                speed: 100,
                color: type === 'player' ? '#4CAF50' : `hsl(${Math.random() * 360}, 70%, 50%)`,
                score: 0,
                alive: true
            };
        }

        // 初始化AI蛇
        function initAISnakes() {
            const aiCount = parseInt(document.getElementById('aiCountSlider').value);
            gameState.aiSnakes = [];
            
            for (let i = 0; i < aiCount; i++) {
                const aiSnake = createSnake('ai', 1);
                // 确保AI蛇不会与玩家蛇重叠
                let validPosition = false;
                while (!validPosition) {
                    validPosition = true;
                    for (let segment of gameState.playerSnake.body) {
                        if (segment.x === aiSnake.body[0].x && segment.y === aiSnake.body[0].y) {
                            validPosition = false;
                            break;
                        }
                    }
                    if (!validPosition) {
                        aiSnake.body[0].x = Math.floor(Math.random() * (canvas.width / gridSize)) * gridSize;
                        aiSnake.body[0].y = Math.floor(Math.random() * (canvas.height / gridSize)) * gridSize;
                    }
                }
                gameState.aiSnakes.push(aiSnake);
            }
        }

        // 生成食物
        function spawnFood() {
            const gridSize = Math.min(canvas.width, canvas.height) / 20;
            const food = {
                x: Math.floor(Math.random() * (canvas.width / gridSize)) * gridSize,
                y: Math.floor(Math.random() * (canvas.height / gridSize)) * gridSize,
                value: 10
            };
            
            // 确保食物不会出现在蛇身上
            let validPosition = false;
            while (!validPosition) {
                validPosition = true;
                for (let segment of gameState.playerSnake.body) {
                    if (segment.x === food.x && segment.y === food.y) {
                        validPosition = false;
                        break;
                    }
                }
                for (let aiSnake of gameState.aiSnakes) {
                    for (let segment of aiSnake.body) {
                        if (segment.x === food.x && segment.y === food.y) {
                            validPosition = false;
                            break;
                        }
                    }
                    if (!validPosition) break;
                }
                if (!validPosition) {
                    food.x = Math.floor(Math.random() * (canvas.width / gridSize)) * gridSize;
                    food.y = Math.floor(Math.random() * (canvas.height / gridSize)) * gridSize;
                }
            }
            
            gameState.food = food;
            gameState.foodCount++;
        }

        // 绑定事件
        function bindEvents() {
            // 模式切换
            document.querySelectorAll('.mode-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    document.querySelectorAll('.mode-btn').forEach(b => b.classList.remove('active'));
                    btn.classList.add('active');
                    gameState.mode = btn.dataset.mode;
                    
                    // 重置游戏
                    resetGame();
                    
                    // 显示/隐藏AI设置
                    const aiSettings = document.getElementById('aiSettings');
                    if (gameState.mode === 'ai') {
                        aiSettings.classList.add('active');
                        initAISnakes();
                    } else {
                        aiSettings.classList.remove('active');
                        gameState.aiSnakes = [];
                    }
                });
            });
            
            // 虚拟按键
            document.getElementById('upBtn').addEventListener('click', () => changeDirection('up'));
            document.getElementById('downBtn').addEventListener('click', () => changeDirection('down'));
            document.getElementById('leftBtn').addEventListener('click', () => changeDirection('left'));
            document.getElementById('rightBtn').addEventListener('click', () => changeDirection('right'));
            
            // AI设置滑块
            document.getElementById('aiCountSlider').addEventListener('input', function() {
                document.getElementById('aiCountValue').textContent = this.value;
                if (gameState.mode === 'ai') {
                    initAISnakes();
                }
            });
            
            document.getElementById('aiDifficultySlider').addEventListener('input', function() {
                document.getElementById('aiDifficultyValue').textContent = this.value;
            });
        }

        // 改变方向
        function changeDirection(direction) {
            if (!gameState.isRunning || gameState.isPaused) return;
            
            const currentDir = gameState.playerSnake.direction;
            const oppositeDir = {
                'up': 'down',
                'down': 'up',
                'left': 'right',
                'right': 'left'
            };
            
            // 防止反向移动
            if (direction !== oppositeDir[currentDir]) {
                gameState.playerSnake.nextDirection = direction;
            }
        }

        // 游戏主循环
        function gameLoop() {
            if (!gameState.isRunning) return;
            
            if (!gameState.isPaused) {
                update();
                render();
                
                // 更新游戏时间
                gameState.gameTime++;
                if (gameState.gameTime % 60 === 0) {
                    updateUI();
                }
            }
            
            requestAnimationFrame(gameLoop);
        }

        // 更新游戏状态
        function update() {
            // 更新玩家蛇方向
            gameState.playerSnake.direction = gameState.playerSnake.nextDirection;
            
            // 移动玩家蛇
            moveSnake(gameState.playerSnake);
            
            // 移动AI蛇
            if (gameState.mode === 'ai') {
                for (let aiSnake of gameState.aiSnakes) {
                    if (aiSnake.alive) {
                        aiMove(aiSnake);
                        moveSnake(aiSnake);
                    }
                }
            }
            
            // 检查碰撞
            checkCollisions();
            
            // 检查食物
            checkFood();
        }

        // 移动蛇
        function moveSnake(snake) {
            const gridSize = Math.min(canvas.width, canvas.height) / 20;
            const head = { ...snake.body[0] };
            
            // 根据方向移动头部
            switch (snake.direction) {
                case 'up': head.y -= gridSize; break;
                case 'down': head.y += gridSize; break;
                case 'left': head.x -= gridSize; break;
                case 'right': head.x += gridSize; break;
            }
            
            // 添加新头部
            snake.body.unshift(head);
            
            // 如果蛇的长度超过设定值，移除尾部
            if (snake.body.length > snake.length) {
                snake.body.pop();
            }
        }

        // AI移动逻辑
        function aiMove(aiSnake) {
            const gridSize = Math.min(canvas.width, canvas.height) / 20;
            const difficulty = parseInt(document.getElementById('aiDifficultySlider').value);
            
            // 获取蛇头位置
            const head = aiSnake.body[0];
            const food = gameState.food;
            
            // 计算食物方向
            const dx = food.x - head.x;
            const dy = food.y - head.y;
            
            // 根据难度调整AI智能程度
            let possibleDirections = [];
            
            // 优先考虑朝向食物的方向
            if (dx > 0 && aiSnake.direction !== 'left') possibleDirections.push('right');
            if (dx < 0 && aiSnake.direction !== 'right') possibleDirections.push('left');
            if (dy > 0 && aiSnake.direction !== 'up') possibleDirections.push('down');
            if (dy < 0 && aiSnake.direction !== 'down') possibleDirections.push('up');
            
            // 随机选择一个方向（根据难度调整随机性）
            let newDirection;
            if (possibleDirections.length > 0) {
                // 难度越高，越倾向于选择朝向食物的方向
                const randomFactor = (5 - difficulty) / 5;
                if (Math.random() < randomFactor) {
                    newDirection = possibleDirections[Math.floor(Math.random() * possibleDirections.length)];
                } else {
                    // 随机选择所有可行方向
                    const allDirections = ['up', 'down', 'left', 'right'];
                    const safeDirections = allDirections.filter(dir => dir !== aiSnake.direction);
                    newDirection = safeDirections[Math.floor(Math.random() * safeDirections.length)];
                }
            } else {
                // 如果没有可行方向，随机选择
                const allDirections = ['up', 'down', 'left', 'right'];
                const safeDirections = allDirections.filter(dir => dir !== aiSnake.direction);
                newDirection = safeDirections[Math.floor(Math.random() * safeDirections.length)];
            }
            
            aiSnake.nextDirection = newDirection;
        }

        // 检查碰撞
        function checkCollisions() {
            const gridSize = Math.min(canvas.width, canvas.height) / 20;
            const playerHead = gameState.playerSnake.body[0];
            
            // 检查是否撞墙
            if (playerHead.x < 0 || playerHead.x >= canvas.width || 
                playerHead.y < 0 || playerHead.y >= canvas.height) {
                gameOver();
                return;
            }
            
            // 检查是否撞到自己
            for (let i = 1; i < gameState.playerSnake.body.length; i++) {
                if (playerHead.x === gameState.playerSnake.body[i].x && 
                    playerHead.y === gameState.playerSnake.body[i].y) {
                    gameOver();
                    return;
                }
            }
            
            // 检查是否撞到AI蛇
            for (let aiSnake of gameState.aiSnakes) {
                if (!aiSnake.alive) continue;
                
                for (let i = 0; i < aiSnake.body.length; i++) {
                    if (playerHead.x === aiSnake.body[i].x && 
                        playerHead.y === aiSnake.body[i].y) {
                        gameOver();
                        return;
                    }
                }
                
                // 检查AI蛇是否撞到玩家蛇
                const aiHead = aiSnake.body[0];
                for (let i = 0; i < gameState.playerSnake.body.length; i++) {
                    if (aiHead.x === gameState.playerSnake.body[i].x && 
                        aiHead.y === gameState.playerSnake.body[i].y) {
                        aiSnake.alive = false;
                    }
                }
            }
            
            // 检查AI蛇之间的碰撞
            for (let i = 0; i < gameState.aiSnakes.length; i++) {
               r (let j = i +  fo1; j < gameState.aiSnakes.length; j++) {
                    const snake1 = gameState.aiSnakes[i];
                    const snake2 = gameState.aiSnakes[j];
                    
                    if (!snake1.alive || !snake2.alive) continue;
                    
                    for (let k = 0; k < snake1.body.length; k++) {
                        if (snake1.body[k].x === snake2.body[0].x && 
                            snake1.body[k].y === snake2.body[0].y) {
                            snake2.alive = false;
                        }
                    }
                    
                    for (let k = 0; k < snake2.body.length; k++) {
                        if (s
