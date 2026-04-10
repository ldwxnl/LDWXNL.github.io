---
layout: default
title: 🐍 贪吃蛇游戏
permalink: /snake-game/
---

<!-- 游戏容器 -->
<div id="game-app">
  <!-- 顶部标题 -->
  <div class="game-header">
    <h1>🐍 贪吃蛇游戏</h1>
    <p class="subtitle">滑动屏幕或使用键盘控制，吃到食物变长</p>
  </div>
  
  <!-- 游戏主界面 -->
  <div class="game-main">
    <!-- 左侧控制面板 -->
    <div class="control-panel">
      <!-- 皮肤选择 -->
      <div class="panel-section">
        <h3>🐍 皮肤选择</h3>
        <div class="skin-selector">
          <div class="skin-option active" data-skin="classic">
            <div class="skin-preview classic"></div>
            <span>经典</span>
          </div>
          <div class="skin-option" data-skin="neon">
            <div class="skin-preview neon"></div>
            <span>霓虹</span>
          </div>
          <div class="skin-option" data-skin="pixel">
            <div class="skin-preview pixel"></div>
            <span>像素</span>
          </div>
          <div class="skin-option" data-skin="nature">
            <div class="skin-preview nature"></div>
            <span>自然</span>
          </div>
        </div>
      </div>
      
      <!-- 游戏设置 -->
      <div class="panel-section">
        <h3>⚙️ 游戏设置</h3>
        <div class="setting-item">
          <label>游戏速度</label>
          <select id="speed-select">
            <option value="200">慢速</option>
            <option value="150" selected>正常</option>
            <option value="100">快速</option>
            <option value="70">极速</option>
          </select>
        </div>
        <div class="setting-item">
          <label>网格大小</label>
          <select id="grid-select">
            <option value="15">大网格</option>
            <option value="20" selected>正常</option>
            <option value="25">小网格</option>
          </select>
        </div>
      </div>
      
      <!-- 控制说明 -->
      <div class="panel-section">
        <h3>🎮 控制方式</h3>
        <div class="control-hint">
          <p><strong>电脑</strong>：方向键 或 WASD</p>
          <p><strong>手机</strong>：在屏幕上滑动</p>
        </div>
      </div>
    </div>
    
    <!-- 中间游戏区域 -->
    <div class="game-area">
      <!-- 游戏画布容器 -->
      <div class="canvas-container">
        <canvas id="gameCanvas"></canvas>
        <!-- 游戏状态覆盖层 -->
        <div id="game-overlay" class="game-overlay">
          <h2 id="overlay-title">贪吃蛇游戏</h2>
          <p id="overlay-text">点击开始游戏</p>
          <button id="start-btn" class="btn-primary">开始游戏</button>
        </div>
      </div>
      
      <!-- 分数面板 -->
      <div class="score-panel">
        <div class="score-item">
          <div class="score-label">分数</div>
          <div id="score" class="score-value">0</div>
        </div>
        <div class="score-item">
          <div class="score-label">长度</div>
          <div id="length" class="score-value">1</div>
        </div>
        <div class="score-item">
          <div class="score-label">最高分</div>
          <div id="high-score" class="score-value">0</div>
        </div>
      </div>
    </div>
    
    <!-- 右侧信息面板 -->
    <div class="info-panel">
      <!-- 控制按钮 -->
      <div class="panel-section">
        <h3>🎯 游戏控制</h3>
        <div class="button-group">
          <button id="pause-btn" class="btn-control">暂停游戏</button>
          <button id="restart-btn" class="btn-control">重新开始</button>
        </div>
      </div>
      
      <!-- 游戏统计 -->
      <div class="panel-section">
        <h3>📊 游戏统计</h3>
        <div class="stats">
          <div class="stat-item">
            <span>游戏时间</span>
            <span id="game-time">00:00</span>
          </div>
          <div class="stat-item">
            <span>食物数量</span>
            <span id="food-count">0</span>
          </div>
          <div class="stat-item">
            <span>当前速度</span>
            <span id="current-speed">正常</span>
          </div>
        </div>
      </div>
      
      <!-- 手机提示 -->
      <div class="mobile-hint">
        <p>📱 手机用户：在游戏区域滑动控制方向</p>
      </div>
    </div>
  </div>
</div>

<!-- 游戏CSS -->
<style>
/* 基础重置 */
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
  overflow-x: hidden;
  background: #1a1a1a;
  color: #e0e0e0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  line-height: 1.6;
}

#game-app {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1rem;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* 头部样式 */
.game-header {
  text-align: center;
  padding: 1rem 0 2rem;
  border-bottom: 2px solid #333;
  margin-bottom: 1.5rem;
}

.game-header h1 {
  font-size: 2.5rem;
  color: #4CAF50;
  margin-bottom: 0.5rem;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.subtitle {
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

/* 控制面板 */
.control-panel, .info-panel {
  width: 250px;
  background: #2a2a2a;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 4px 20px rgba(0,0,0,0.2);
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.panel-section h3 {
  color: #4CAF50;
  margin-bottom: 1rem;
  font-size: 1.2rem;
  border-left: 3px solid #4CAF50;
  padding-left: 0.8rem;
}

/* 皮肤选择器 */
.skin-selector {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.8rem;
}

.skin-option {
  background: #333;
  border: 2px solid transparent;
  border-radius: 8px;
  padding: 0.8rem;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s;
}

.skin-option.active {
  border-color: #4CAF50;
  background: rgba(76, 175, 80, 0.1);
}

.skin-option:hover {
  transform: translateY(-2px);
  background: #3a3a3a;
}

.skin-preview {
  width: 40px;
  height: 40px;
  margin: 0 auto 0.5rem;
  border-radius: 6px;
}

/* 皮肤预览样式 */
.skin-preview.classic {
  background: linear-gradient(45deg, #4CAF50, #8BC34A);
}
.skin-preview.neon {
  background: linear-gradient(45deg, #00bcd4, #e040fb);
  box-shadow: 0 0 10px #00bcd4;
}
.skin-preview.pixel {
  background: linear-gradient(45deg, #ff9800, #ff5722);
}
.skin-preview.nature {
  background: linear-gradient(45deg, #795548, #4caf50);
}

/* 设置项 */
.setting-item {
  margin-bottom: 1rem;
}

.setting-item label {
  display: block;
  margin-bottom: 0.5rem;
  color: #bbb;
}

.setting-item select {
  width: 100%;
  padding: 0.6rem;
  background: #333;
  border: 1px solid #444;
  border-radius: 6px;
  color: #fff;
  font-size: 1rem;
}

/* 游戏区域 */
.game-area {
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
  background: #111;
}

#gameCanvas {
  width: 100%;
  height: 100%;
  display: block;
}

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
  text-align: center;
  padding: 2rem;
}

#overlay-title {
  font-size: 2.5rem;
  color: #4CAF50;
  margin-bottom: 1rem;
}

#overlay-text {
  font-size: 1.2rem;
  color: #ccc;
  margin-bottom: 2rem;
  max-width: 400px;
}

/* 按钮样式 */
.btn-primary, .btn-control {
  padding: 0.9rem 2rem;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.btn-primary {
  background: linear-gradient(135deg, #4CAF50, #2E7D32);
  color: white;
  box-shadow: 0 4px 15px rgba(76, 175, 80, 0.3);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(76, 175, 80, 0.4);
}

.btn-control {
  width: 100%;
  background: #333;
  color: #fff;
  border: 1px solid #444;
  margin-bottom: 0.8rem;
}

.btn-control:hover {
  background: #3a3a3a;
  border-color: #4CAF50;
}

.button-group {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

/* 分数面板 */
.score-panel {
  display: flex;
  gap: 2rem;
  background: #2a2a2a;
  border-radius: 12px;
  padding: 1.5rem 3rem;
  box-shadow: 0 4px 20px rgba(0,0,0,0.2);
}

.score-item {
  text-align: center;
  min-width: 100px;
}

.score-label {
  color: #aaa;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.score-value {
  color: #fff;
  font-size: 2.5rem;
  font-weight: bold;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

/* 统计信息 */
.stats {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.stat-item {
  display: flex;
  justify-content: space-between;
  padding: 0.6rem 0;
  border-bottom: 1px solid #333;
}

.stat-item:last-child {
  border-bottom: none;
}

/* 手机提示 */
.mobile-hint {
  display: none;
  text-align: center;
  padding: 1rem;
  background: rgba(76, 175, 80, 0.1);
  border-radius: 8px;
  border: 1px solid rgba(76, 175, 80, 0.3);
  color: #4CAF50;
}

/* 响应式设计 */
@media (max-width: 1200px) {
  .game-main {
    flex-direction: column;
  }
  
  .control-panel, .info-panel {
    width: 100%;
  }
  
  .control-panel {
    order: 3;
  }
  
  .game-area {
    order: 1;
  }
  
  .info-panel {
    order: 2;
  }
  
  .skin-selector {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (max-width: 768px) {
  .game-header h1 {
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
  
  .mobile-hint {
    display: block;
  }
  
  .skin-selector {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .game-header h1 {
    font-size: 1.8rem;
  }
  
  .subtitle {
    font-size: 1rem;
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

<!-- 游戏JavaScript -->
<script>
// ==================== 游戏配置 ====================
const GameConfig = {
  INITIAL_SPEED: 150,
  GRID_SIZE: 20,
  SKINS: {
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
  }
};

// ==================== 游戏状态 ====================
let canvas, ctx;
let gameState = {
  snake: [],
  food: { x: 0, y: 0 },
  dx: 0,
  dy: 0,
  score: 0,
  highScore: localStorage.getItem('snakeHighScore') || 0,
  length: 1,
  speed: GameConfig.INITIAL_SPEED,
  gridSize: GameConfig.GRID_SIZE,
  isPaused: true,
  isGameOver: true,
  gameLoop: null,
  startTime: 0,
  elapsedTime: 0,
  foodCount: 0,
  currentSkin: 'classic',
  touchStartX: 0,
  touchStartY: 0
};

// ==================== DOM 元素 ====================
const dom = {
  canvas: null,
  score: null,
  length: null,
  highScore: null,
  startBtn: null,
  pauseBtn: null,
  restartBtn: null,
  overlay: null,
  overlayTitle: null,
  overlayText: null,
  gameTime: null,
  foodCount: null,
  speedSelect: null,
  gridSelect: null,
  currentSpeed: null
};

// ==================== 初始化 ====================
function initGame() {
  // 获取DOM元素
  dom.canvas = document.getElementById('gameCanvas');
  dom.score = document.getElementById('score');
  dom.length = document.getElementById('length');
  dom.highScore = document.getElementById('high-score');
  dom.startBtn = document.getElementById('start-btn');
  dom.pauseBtn = document.getElementById('pause-btn');
  dom.restartBtn = document.getElementById('restart-btn');
  dom.overlay = document.getElementById('game-overlay');
  dom.overlayTitle = document.getElementById('overlay-title');
  dom.overlayText = document.getElementById('overlay-text');
  dom.gameTime = document.getElementById('game-time');
  dom.foodCount = document.getElementById('food-count');
  dom.speedSelect = document.getElementById('speed-select');
  dom.gridSelect = document.getElementById('grid-select');
  dom.currentSpeed = document.getElementById('current-speed');
  
  // 获取上下文
  ctx = dom.canvas.getContext('2d');
  
  // 初始化画布大小
  resizeCanvas();
  window.addEventListener('resize', resizeCanvas);
  
  // 显示最高分
  dom.highScore.textContent = gameState.highScore;
  
  // 初始化游戏
  resetGame();
  draw();
  
  // 事件监听
  setupEventListeners();
  
  // 初始化皮肤选择
  initSkinSelection();
  
  // 开始游戏循环
  requestAnimationFrame(gameLoop);
}

// 调整画布大小
function resizeCanvas() {
  const container = dom.canvas.parentElement;
  const size = Math.min(container.clientWidth, container.clientHeight);
  dom.canvas.width = size;
  dom.canvas.height = size;
  gameState.gridSize = parseInt(dom.gridSelect.value);
  draw(); // 重新绘制
}

// 设置事件监听
function setupEventListeners() {
  // 键盘控制
  document.addEventListener('keydown', handleKeyDown);
  
  // 按钮事件
  dom.startBtn.addEventListener('click', startGame);
  dom.pauseBtn.addEventListener('click', togglePause);
  dom.restartBtn.addEventListener('click', resetGame);
  
  // 设置更改
  dom.speedSelect.addEventListener('change', (e) => {
    gameState.speed = parseInt(e.target.value);
    updateSpeedDisplay();
    if (!gameState.isPaused && !gameState.isGameOver) {
      clearInterval(gameState.gameLoop);
      gameState.gameLoop = setInterval(gameUpdate, gameState.speed);
    }
  });
  
  dom.gridSelect.addEventListener('change', (e) => {
    gameState.gridSize = parseInt(e.target.value);
    resizeCanvas();
  });
  
  // 触摸控制
  setupTouchControls();
}

// 初始化皮肤选择
function initSkinSelection() {
  const skinOptions = document.querySelectorAll('.skin-option');
  skinOptions.forEach(option => {
    option.addEventListener('click', () => {
      // 移除所有active
      skinOptions.forEach(opt => opt.classList.remove('active'));
      // 添加active到当前
      option.classList.add('active');
      // 更新皮肤
      gameState.currentSkin = option.dataset.skin;
      draw();
    });
  });
}

// 设置触摸控制
function setupTouchControls() {
  dom.canvas.addEventListener('touchstart', (e) => {
    if (e.touches.length !== 1) return;
    const touch = e.touches[0];
    gameState.touchStartX = touch.clientX;
    gameState.touchStartY = touch.clientY;
    e.preventDefault();
  }, { passive: false });
  
  dom.canvas.addEventListener('touchend', (e) => {
    if (!gameState.touchStartX || gameState.isPaused || gameState.isGameOver) return;
    if (e.changedTouches.length !== 1) return;
    
    const touch = e.changedTouches[0];
    const deltaX = touch.clientX - gameState.touchStartX;
    const deltaY = touch.clientY - gameState.touchStartY;
    const minSwipe = 15;
    
    if (Math.abs(deltaX) < minSwipe && Math.abs(deltaY) < minSwipe) {
      gameState.touchStartX = 0;
      return;
    }
    
    if (Math.abs(deltaX) > Math.abs(deltaY)) {
      if (deltaX > 0 && gameState.dx !== -1) { gameState.dx = 1; gameState.dy = 0; }
      else if (deltaX < 0 && gameState.dx !== 1) { gameState.dx = -1; gameState.dy = 0; }
    } else {
      if (deltaY > 0 && gameState.dy !== -1) { gameState.dx = 0; gameState.dy = 1; }
      else if (deltaY < 0 && gameState.dy !== 1) { gameState.dx = 0; gameState.dy = -1; }
    }
    
    gameState.touchStartX = 0;
    e.preventDefault();
  }, { passive: false });
}

// ==================== 游戏控制 ====================
function startGame() {
  if (gameState.isGameOver) {
    resetGame();
    gameState.isGameOver = false;
  }
  
  if (gameState.isPaused) {
    gameState.isPaused = false;
    gameState.startTime = Date.now() - gameState.elapsedTime;
    gameState.gameLoop = setInterval(gameUpdate, gameState.speed);
    dom.overlay.style.display = 'none';
    dom.startBtn.textContent = '游戏中...';
  }
}

function togglePause() {
  if (gameState.isGameOver) return;
  
  gameState.isPaused = !gameState.isPaused;
  if (gameState.isPaused) {
    clearInterval(gameState.gameLoop);
    showOverlay('游戏暂停', '点击继续游戏');
    dom.startBtn.textContent = '继续游戏';
  } else {
    gameState.gameLoop = setInterval(gameUpdate, gameState.speed);
    dom.overlay.style.display = 'none';
    dom.startBtn.textContent = '游戏中...';
  }
}

function resetGame() {
  clearInterval(gameState.gameLoop);
  gameState.isPaused = true;
  gameState.isGameOver = true;
  
  // 重置蛇
  const gridCount = Math.floor(dom.canvas.width / gameState.gridSize);
  const center = Math.floor(gridCount / 2);
  gameState.snake = [{ x: center, y: center }];
  
  // 生成食物
  generateFood();
  
  // 重置状态
  gameState.dx = 0;
  gameState.dy = 0;
  gameState.score = 0;
  gameState.length = 1;
  gameState.foodCount = 0;
  gameState.elapsedTime = 0;
  gameState.speed = parseInt(dom.speedSelect.value);
  
  // 更新显示
  updateUI();
  draw();
  
  // 显示开始界面
  showOverlay('贪吃蛇游戏', '选择皮肤和设置，然后开始游戏');
  dom.startBtn.textContent = '开始游戏';
  updateSpeedDisplay();
}

// ==================== 游戏逻辑 ====================
function gameUpdate() {
  if (gameState.isPaused || gameState.isGameOver) return;
  
  // 移动蛇
  moveSnake();
  
  // 检查碰撞
  if (checkCollision()) {
    gameOver();
    return;
  }
  
  // 更新UI
  updateUI();
  
  // 绘制
  draw();
}

function moveSnake() {
  if (gameState.dx === 0 && gameState.dy === 0) return;
  
  const head = { 
    x: gameState.snake[0].x + gameState.dx, 
    y: gameState.snake[0].y + gameState.dy 
  };
  gameState.snake.unshift(head);
  
  // 检查是否吃到食物
  if (head.x === gameState.food.x && head.y === gameState.food.y) {
    gameState.score += 10;
    gameState.length++;
    gameState.foodCount++;
    generateFood();
    
    // 每吃5个食物加速
    if (gameState.foodCount % 5 === 0) {
      gameState.speed = Math.max(50, gameState.speed - 10);
      clearInterval(gameState.gameLoop);
      gameState.gameLoop = setInterval(gameUpdate, gameState.speed);
      updateSpeedDisplay();
    }
  } else {
    gameState.snake.pop();
  }
}

function generateFood() {
  const gridCount = Math.floor(dom.canvas.width / gameState.gridSize);
  let newFood;
  let onSnake;
  
  do {
    onSnake = false;
    newFood = {
      x: Math.floor(Math.random() * gridCount),
      y: Math.floor(Math.random() * gridCount)
    };
    
    for (const segment of gameState.snake) {
      if (segment.x === newFood.x && segment.y === newFood.y) {
        onSnake = true;
        break;
      }
    }
  } while (onSnake);
  
  gameState.food = newFood;
}

function checkCollision() {
  const head = gameState.snake[0];
  const gridCount = Math.floor(dom.canvas.width / gameState.gridSize);
  
  // 撞墙
  if (head.x < 0 || head.x >= gridCount || head.y < 0 || head.y >= gridCount) {
    return true;
  }
  
  // 撞自己
  for (let i = 1; i < gameState.snake.length; i++) {
    if (head.x === gameState.snake[i].x && head.y === gameState.snake[i].y) {
      return true;
    }
  }
  
  return false;
}

function gameOver() {
  clearInterval(gameState.gameLoop);
  gameState.isGameOver = true;
  gameState.isPaused = true;
  
  // 更新最高分
  if (gameState.score > gameState.highScore) {
    gameState.highScore = gameState.score;
    localStorage.setItem('snakeHighScore', gameState.highScore);
    dom.highScore.textContent = gameState.highScore;
  }
  
  showOverlay('游戏结束', `得分: ${gameState.score}<br>长度: ${gameState.length}<br>时间: ${formatTime(gameState.elapsedTime)}`);
  dom.startBtn.textContent = '重新开始';
}

// ==================== 渲染 ====================
function draw() {
  const skin = GameConfig.SKINS[gameState.currentSkin];
  const cellSize = gameState.gridSize;
  
  // 清空画布
  ctx.fillStyle = skin.bg;
  ctx.fillRect(0, 0, dom.canvas.width, dom.canvas.height);
  
  // 绘制网格（可选）
  if (false) { // 设置为true显示网格
    ctx.strokeStyle = 'rgba(255, 255, 255, 0.05)';
    ctx.lineWidth = 0.5;
    for (let x = 0; x <= dom.canvas.width; x += cellSize) {
      ctx.beginPath();
      ctx.moveTo(x, 0);
      ctx.lineTo(x, dom.canvas.height);
      ctx.stroke();
    }
    for (let y = 0; y <= dom.canvas.height; y += cellSize) {
      ctx.beginPath();
      ctx.moveTo(0, y);
      ctx.lineTo(dom.canvas.width, y);
      ctx.stroke();
    }
  }
  
  // 绘制蛇
  gameState.snake.forEach((segment, index) => {
    if (index === 0) {
      // 蛇头
      ctx.fillStyle = skin.snakeHead;
    } else if (index === gameState.snake.length - 1) {
      // 蛇尾
      ctx.fillStyle = skin.snakeTail;
    } else {
      // 蛇身
      ctx.fillStyle = skin.snakeBody;
    }
    
    ctx.fillRect(
      segment.x * cellSize + 1,
      segment.y * cellSize + 1,
      cellSize - 2,
      cellSize - 2
    );
    
    // 蛇头眼睛
    if (index === 0) {
      const eyeSize = cellSize / 5;
      const offset = cellSize / 3;
      ctx.fillStyle = '#000';
      
      // 根据方向确定眼睛位置
      if (gameState.dx === 1) { // 向右
        ctx.fillRect(segment.x * cellSize + cellSize - offset, segment.y * cellSize + offset, eyeSize, eyeSize);
        ctx.fillRect(segment.x * cellSize + cellSize - offset, segment.y * cellSize + cellSize - offset - eyeSize, eyeSize, eyeSize);
      } else if (gameState.dx === -1) { // 向左
        ctx.fillRect(segment.x * cellSize + offset - eyeSize, segment.y * cellSize + offset, eyeSize, eyeSize);
        ctx.fillRect(segment.x * cellSize + offset - eyeSize, segment.y * cellSize + cellSize - offset - eyeSize, eyeSize, eyeSize);
      } else if (gameState.dy === 1) { // 向下
        ctx.fillRect(segment.x * cellSize + offset, segment.y * cellSize + cellSize - offset, eyeSize, eyeSize);
        ctx.fillRect(segment.x * cellSize + cellSize - offset - eyeSize, segment.y * cellSize + cellSize - offset, eyeSize, eyeSize);
      } else if (gameState.dy === -1) { // 向上
        ctx.fillRect(segment.x * cellSize + offset, segment.y * cellSize + offset - eyeSize, eyeSize, eyeSize);
        ctx.fillRect(segment.x * cellSize + cellSize - offset - eyeSize, segment.y * cellSize + offset - eyeSize, eyeSize, eyeSize);
      } else { // 初始状态
        ctx.fillRect(segment.x * cellSize + offset, segment.y * cellSize + offset, eyeSize, eyeSize);
        ctx.fillRect(segment.x * cellSize + cellSize - offset - eyeSize, segment.y * cellSize + offset, eyeSize, eyeSize);
      }
    }
  });
  
  // 绘制食物
  ctx.fillStyle = skin.food;
  ctx.beginPath();
  const centerX = gameState.food.x * cellSize + cellSize / 2;
  const centerY = gameState.food.y * cellSize + cellSize / 2;
  const radius = cellSize / 2 - 2;
  ctx.arc(centerX, centerY, radius, 0, Math.PI * 2);
  ctx.fill();
  
  // 食物发光效果
  ctx.shadowColor = skin.foodGlow;
  ctx.shadowBlur = 10;
  ctx.fill();
  ctx.shadowBlur = 0;
}

// ==================== UI 更新 ====================
function updateUI() {
  // 更新分数
  dom.score.textContent = gameState.score;
  dom.length.textContent = gameState.length;
  dom.foodCount.textContent = gameState.foodCount;
  
  // 更新游戏时间
  if (!gameState.isPaused && !gameState.isGameOver) {
    gameState.elapsedTime = Date.now() - gameState.startTime;
  }
  dom.gameTime.textContent = formatTime(gameState.elapsedTime);
}

function updateSpeedDisplay() {
  const speedMap = {
    '200': '慢速',
    '150': '正常',
    '100': '快速',
    '70': '极速',
    '50': '极限'
  };
  dom.currentSpeed.textContent = speedMap[gameState.speed] || '自定义';
}

function showOverlay(title, text) {
  dom.overlayTitle.innerHTML = title;
  dom.overlayText.innerHTML = text;
  dom.overlay.style.display = 'flex';
}

// ==================== 工具函数 ====================
function handleKeyDown(e) {
  if (gameState.isPaused && !gameState.isGameOver) return;
  
  switch(e.key) {
    case 'ArrowUp': case 'w': case 'W':
      if (gameState.dy !== 1) { gameState.dx = 0; gameState.dy = -1; } break;
    case 'ArrowDown': case 's': case 'S':
      if (gameState.dy !== -1) { gameState.dx = 0; gameState.dy = 1; } break;
    case 'ArrowLeft': case 'a': case 'A':
      if (gameState.dx !== 1) { gameState.dx = -1; gameState.dy = 0; } break;
    case 'ArrowRight': case 'd': case 'D':
      if (gameState.dx !== -1) { gameState.dx = 1; gameState.dy = 0; } break;
    case ' ': // 空格键暂停
      e.preventDefault();
      togglePause();
      break;
  }
}

function formatTime(ms) {
  const totalSeconds = Math.floor(ms / 1000);
const 分钟 =常量(totalSeconds / 60)；
常量
返回“$ {minutes.toString返回)。padStart (2, ' 0 ')}: $ {seconds.toString()。padStart (2, ' 0 ')} ';
}

// 游戏主循环
函数 () { gameLoop() {
  requestAnimationFrame(gameLoop);
}

// ==================== 启动游戏 ====================
如果
“DOMContentLoaded”内
} 其他 {
  initGame();
}
< / script>

---

## 🎯 第二阶段和第三阶段的实现计划

### 第二阶段：AI 对战模式
- **实现方式**：A* 路径寻找算法
- **AI难度**：简单/中等/困难
- **功能**：与AI蛇对战，AI会自动寻找食物并避开障碍
- **预计时间**：2-3天开发

### 第三阶段：多人广域网对战
- **实现方式**：WebSocket + Node.- **实现方式**：WebSocket   Node.js 后端 后端
- **托管需求**：需要单独的服务器（不能只用 GitHub Pages）
- **功能**：创建房间、加入房间、实时对战
- **预计时间**：1-2周开发

---

## 📱 当前版本特性总结

你现在拥有的这个版本已经包含：

✅ **完整的单人游戏体验**  
✅ **4种可切换皮肤**（经典、霓虹、像素、自然）  
✅ **完美手机适配**（触摸控制 + 响应式布局）  
✅ **游戏设置**（速度、网格大小可调）  
✅ **统计系统**（时间、食物计数、最高分）  
✅ **专业UI设计**（现代化深色主题）

---

## 🔧 部署步骤

1. 在你的 GitHub Pages 仓库中创建文件夹：“贪吃蛇游戏/”
2. 在该文件夹中创建 `index.md` 文件
3. 复制上面的完整代码到 `index.md`
4. 保存并推送到 GitHub
5. 等待 1-2 分钟部署
6. 访问：`https://你的域名/snake-game/`

---

这个版本已经是一个**专业级的贪吃蛇游戏**，比之前的基础版强大了很多。先部署这个版本，测试手机适配效果。如果满意，我们再继续开发AI对战功能。
