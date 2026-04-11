---
layout: default
title: 🐍 贪吃蛇游戏
permalink: /snake-game/
---

<style>
/* 基础样式 */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  -webkit-tap-highlight-color: transparent;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #1a1a1a;
  color: #e0e0e0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1rem;
}

.game-container {
  max-width: 800px;
  width: 100%;
  text-align: center;
}

/* 标题 */
.game-title {
  font-size: 2.5rem;
  color: #4CAF50;
  margin-bottom: 0.5rem;
  text-shadow: 0 2px 4px rgba(0,0,0,0.3);
}

.game-subtitle {
  color: #aaa;
  margin-bottom: 2rem;
  font-size: 1.1rem;
}

/* 画布 */
.canvas-wrapper {
  margin: 0 auto 2rem;
  max-width: 600px;
  position: relative;
}

#gameCanvas {
  width: 100%;
  max-width: 400px;
  height: 400px;
  border: 3px solid #333;
  border-radius: 8px;
  background: #111;
  display: block;
  margin: 0 auto;
  touch-action: none;
}

/* 覆盖层 */
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
  border-radius: 8px;
}

.overlay-title {
  font-size: 2rem;
  color: #4CAF50;
  margin-bottom: 1rem;
}

.overlay-text {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  color: #ccc;
}

/* 按钮 */
.btn {
  padding: 0.8rem 1.8rem;
  border: none;
  border-radius: 6px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  margin: 0.5rem;
  min-width: 140px;
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

/* 控制区域 */
.controls {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 2rem;
}

/* 分数面板 */
.score-panel {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.score-item {
  background: #2a2a2a;
  padding: 1rem 1.5rem;
  border-radius: 8px;
  min-width: 120px;
}

.score-label {
  color: #aaa;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}

.score-value {
  color: #fff;
  font-size: 2rem;
  font-weight: bold;
}

/* 响应式 */
@media (max-width: 768px) {
  .game-title {
    font-size: 2rem;
  }
  
  #gameCanvas {
    max-width: 90vw;
    height: 90vw;
  }
  
  .controls {
    flex-direction: column;
    align-items: center;
  }
  
  .btn {
    width: 90%;
    max-width: 300px;
  }
  
  .score-panel {
    gap: 1rem;
  }
  
  .score-item {
    min-width: 100px;
    padding: 0.8rem 1rem;
  }
}
</style>

<div class="game-container">
  <h1 class="game-title">🐍 贪吃蛇游戏</h1>
  <p class="game-subtitle">用键盘或触摸控制蛇的移动，吃到食物变长</p>
  
  <!-- 游戏画布 -->
  <div class="canvas-wrapper">
    <canvas id="gameCanvas" width="400" height="400"></canvas>
    
    <!-- 游戏状态覆盖层 -->
    <div id="gameOverlay" class="game-overlay">
      <h2 id="overlayTitle" class="overlay-title">贪吃蛇游戏</h2>
      <p id="overlayText" class="overlay-text">点击开始游戏</p>
      <button id="startButton" class="btn btn-primary">开始游戏</button>
    </div>
  </div>
  
  <!-- 分数显示 -->
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
  
  <!-- 控制按钮 -->
  <div class="controls">
    <button id="pauseButton" class="btn btn-secondary">暂停游戏</button>
    <button id="restartButton" class="btn btn-secondary">重新开始</button>
  </div>
  
  <!-- 操作说明 -->
  <div style="background: #2a2a2a; padding: 1.5rem; border-radius: 8px; max-width: 600px; margin: 0 auto;">
    <h3 style="color: #4CAF50; margin-bottom: 1rem;">操作说明</h3>
    <p style="margin-bottom: 0.5rem;">电脑：方向键 或 WASD 控制移动</p>
    <p style="margin-bottom: 0.5rem;">手机：在屏幕上滑动控制方向</p>
    <p>每吃一个食物：+10 分，蛇长度 +1</p>
  </div>
</div>

<script>
// ==================== 游戏配置 ====================
const CONFIG = {
  GRID_SIZE: 20,
  INITIAL_SPEED: 150,
  FOOD_SCORE: 10
};

// ==================== 游戏状态 ====================
let game = {
  // 游戏元素
  canvas: null,
  ctx: null,
  
  // 游戏对象
  snake: [],
  food: { x: 0, y: 0 },
  
  // 控制状态
  dx: 0,
  dy: 0,
  
  // 游戏状态
  score: 0,
  highScore: localStorage.getItem('snakeHighScore') || 0,
  length: 1,
  isPaused: true,
  isGameOver: true,
  gameLoop: null,
  
  // 触摸控制
  touchStartX: 0,
  touchStartY: 0
};

// ==================== DOM 元素 ====================
const elements = {};

// ==================== 初始化游戏 ====================
function initGame() {
  console.log('🎮 开始初始化游戏...');
  
  // 获取DOM元素
  elements.canvas = document.getElementById('gameCanvas');
  elements.ctx = elements.canvas.getContext('2d');
  elements.scoreDisplay = document.getElementById('scoreDisplay');
  elements.lengthDisplay = document.getElementById('lengthDisplay');
  elements.highScoreDisplay = document.getElementById('highScoreDisplay');
  elements.startButton = document.getElementById('startButton');
  elements.pauseButton = document.getElementById('pauseButton');
  elements.restartButton = document.getElementById('restartButton');
  elements.gameOverlay = document.getElementById('gameOverlay');
  elements.overlayTitle = document.getElementById('overlayTitle');
  elements.overlayText = document.getElementById('overlayText');
  
  // 检查元素是否找到
  console.log('✅ Canvas元素:', elements.canvas);
  console.log('✅ 开始按钮:', elements.startButton);
  console.log('✅ 暂停按钮:', elements.pauseButton);
  console.log('✅ 重新开始按钮:', elements.restartButton);
  
  // 设置Canvas焦点
  elements.canvas.setAttribute('tabindex', '0');
  elements.canvas.style.outline = 'none';
  elements.canvas.focus();
  
  // 显示最高分
  elements.highScoreDisplay.textContent = game.highScore;
  
  // 初始化游戏状态
  resetGame();
  draw();
  
  // 绑定事件监听器
  setupEventListeners();
  
  console.log('🎮 游戏初始化完成！');
}

// ==================== 事件监听器 ====================
function setupEventListeners() {
  console.log('🎮 设置事件监听器...');
  
  // 键盘控制
  document.addEventListener('keydown', handleKeyDown);
  console.log('✅ 键盘事件监听器已绑定');
  
  // 按钮事件
  elements.startButton.addEventListener('click', function(e) {
    console.log('🎯 开始按钮被点击', e);
    startGame();
  });
  console.log('✅ 开始按钮监听器已绑定');
  
  elements.pauseButton.addEventListener('click', function(e) {
    console.log('🎯 暂停按钮被点击', e);
    togglePause();
  });
  console.log('✅ 暂停按钮监听器已绑定');
  
  elements.restartButton.addEventListener('click', function(e) {
    console.log('🎯 重新开始按钮被点击', e);
    resetGame();
  });
  console.log('✅ 重新开始按钮监听器已绑定');
  
  // Canvas点击获取焦点
  elements.canvas.addEventListener('click', function() {
    console.log('🎯 Canvas被点击，获取焦点');
    elements.canvas.focus();
  });
  
  // 触摸控制
  setupTouchControls();
  
  console.log('🎮 所有事件监听器设置完成');
}

// 触摸控制
function setupTouchControls() {
  elements.canvas.addEventListener('touchstart', function(e) {
    if (e.touches.length !== 1) return;
    const touch = e.touches[0];
    game.touchStartX = touch.clientX;
    game.touchStartY = touch.clientY;
    e.preventDefault();
  }, { passive: false });
  
  elements.canvas.addEventListener('touchend', function(e) {
    if (!game.touchStartX || game.isPaused || game.isGameOver) return;
    if (e.changedTouches.length !== 1) return;
    
    const touch = e.changedTouches[0];
    const deltaX = touch.clientX - game.touchStartX;
    const deltaY = touch.clientY - game.touchStartY;
    const minSwipe = 15;
    
    if (Math.abs(deltaX) < minSwipe && Math.abs(deltaY) < minSwipe) {
      game.touchStartX = 0;
      return;
    }
    
    if (Math.abs(deltaX) > Math.abs(deltaY)) {
      if (deltaX > 0 && game.dx !== -1) { game.dx = 1; game.dy = 0; }
      else if (deltaX < 0 && game.dx !== 1) { game.dx = -1; game.dy = 0; }
    } else {
      if (deltaY > 0 && game.dy !== -1) { game.dx = 0; game.dy = 1; }
      else if (deltaY < 0 && game.dy !== 1) { game.dx = 0; game.dy = -1; }
    }
    
    game.touchStartX = 0;
    e.preventDefault();
  }, { passive: false });
}

// ==================== 游戏控制 ====================
function startGame() {
  console.log('🎮 开始游戏');
  
  if (game.isGameOver) {
    resetGame();
    game.isGameOver = false;
  }
  
  if (game.isPaused) {
    game.isPaused = false;
    game.gameLoop = setInterval(gameUpdate, CONFIG.INITIAL_SPEED);
    elements.gameOverlay.style.display = 'none';
    elements.startButton.textContent = '游戏中...';
    elements.canvas.focus();
  }
}

function togglePause() {
  console.log('🎮 切换暂停状态，当前:', game.isPaused);
  
  if (game.isGameOver) return;
  
  game.isPaused = !game.isPaused;
  if (game.isPaused) {
    clearInterval(game.gameLoop);
    showOverlay('游戏暂停', '点击继续游戏');
    elements.startButton.textContent = '继续游戏';
  } else {
    game.gameLoop = setInterval(gameUpdate, CONFIG.INITIAL_SPEED);
    elements.gameOverlay.style.display = 'none';
    elements.startButton.textContent = '游戏中...';
  }
}

function resetGame() {
  console.log('🎮 重置游戏');
  
  clearInterval(game.gameLoop);
  game.isPaused = true;
  game.isGameOver = true;
  
  // 重置蛇
  const gridCount = Math.floor(elements.canvas.width / CONFIG.GRID_SIZE);
  const center = Math.floor(gridCount / 2);
  game.snake = [{ x: center, y: center }];
  
  // 生成食物
  generateFood();
  
  // 重置状态
  game.dx = 0;
  game.dy = 0;
  game.score = 0;
  game.length = 1;
  
  // 更新显示
  updateDisplay();
  draw();
  
  // 显示开始界面
  showOverlay('贪吃蛇游戏', '点击开始游戏');
  elements.startButton.textContent = '开始游戏';
}

// ==================== 游戏逻辑 ====================
function gameUpdate() {
  if (game.isPaused || game.isGameOver) return;
  
  // 移动蛇
  moveSnake();
  
  // 检查碰撞
  if (checkCollision()) {
    gameOver();
    return;
  }
  
  // 更新显示
  updateDisplay();
  draw();
}

function moveSnake() {
  if (game.dx === 0 && game.dy === 0) return;
  
  const head = { 
    x: game.snake[0].x + game.dx, 
    y: game.snake[0].y + game.dy 
  };
  game.snake.unshift(head);
  
  // 检查是否吃到食物
  if (head.x === game.food.x && head.y === game.food.y) {
    game.score += CONFIG.FOOD_SCORE;
    game.length++;
    generateFood();
  } else {
    game.snake.pop();
  }
}

function generateFood() {
  const gridCount = Math.floor(elements.canvas.width / CONFIG.GRID_SIZE);
  let newFood;
  let onSnake;
  
  do {
    onSnake = false;
    newFood = {
      x: Math.floor(Math.random() * gridCount),
      y: Math.floor(Math.random() * gridCount)
    };
    
    for (const segment of game.snake) {
      if (segment.x === newFood.x && segment.y === newFood.y) {
        onSnake = true;
        break;
      }
    }
  } while (onSnake);
  
  game.food = newFood;
}

function checkCollision() {
  const head = game.snake[0];
  const gridCount = Math.floor(elements.canvas.width / CONFIG.GRID_SIZE);
  
  // 撞墙
  if (head.x < 0 || head.x >= gridCount || head.y < 0 || head.y >= gridCount) {
    return true;
  }
  
  // 撞自己
  for (let i = 1; i < game.snake.length; i++) {
    if (head.x === game.snake[i].x && head.y === game.snake[i].y) {
      return true;
    }
  }
  
  return false;
}

function gameOver() {
  console.log('🎮 游戏结束，得分:', game.score);
  
  clearInterval(game.gameLoop);
  game.isGameOver = true;
  game.isPaused = true;
  
  // 更新最高分
  if (game.score > game.highScore) {
    game.highScore = game.score;
    localStorage.setItem('snakeHighScore', game.highScore);
    elements.highScoreDisplay.textContent = game.highScore;
  }
  
  showOverlay('游戏结束', `得分: ${game.score}<br>长度: ${game.length}`);
  elements.startButton.textContent = '重新开始';
}

// ==================== 渲染 ====================
function draw() {
  const cellSize = CONFIG.GRID_SIZE;
  
  // 清空画布
  elements.ctx.fillStyle = '#111';
  elements.ctx.fillRect(0, 0, elements.canvas.width, elements.canvas.height);
  
  // 绘制蛇
  game.snake.forEach((segment, index) => {
    if (index === 0) {
      elements.ctx.fillStyle = '#4CAF50'; // 蛇头
    } else {
      elements.ctx.fillStyle = '#8BC34A'; // 蛇身
    }
    
    elements.ctx.fillRect(
      segment.x * cellSize + 1,
      segment.y * cellSize + 1,
      cellSize - 2,
      cellSize - 2
    );
  });
  
  // 绘制食物
  elements.ctx.fillStyle = '#FF5252';
  elements.ctx.beginPath();
  const centerX = game.food.x * cellSize + cellSize / 2;
  const centerY = game.food.y * cellSize + cellSize / 2;
  elements.ctx.arc(centerX, centerY, cellSize / 2 - 2, 0, Math.PI * 2);
  elements.ctx.fill();
}

// ==================== UI 更新 ====================
function updateDisplay() {
  elements.scoreDisplay.textContent = game.score;
  elements.lengthDisplay.textContent = game.length;
}

function showOverlay(title, text) {
  elements.overlayTitle.innerHTML = title;
  elements.overlayText.innerHTML = text;
  elements.gameOverlay.style.display = 'flex';
}

// ==================== 输入处理 ====================
function handleKeyDown(e) {
  console.log('⌨️ 按键:', e.key, 'code:', e.code);
  
  if (game.isPaused && !game.isGameOver) return;
  
  switch(e.key.toLowerCase()) {
    case 'arrowup': case 'w':
      if (game.dy !== 1) { 
        game.dx = 0; 
        game.dy = -1; 
        console.log('⬆️ 向上移动');
      }
      break;
    case 'arrowdown': case 's':
      if (game.dy !== -1) { 
        game.dx = 0; 
        game.dy = 1; 
        console.log('⬇️ 向下移动');
      }
      break;
    case 'arrowleft': case 'a':
      if (game.dx !== 1) { 
        game.dx = -1; 
        game.dy = 0; 
        console.log('⬅️ 向左移动');
      }
      break;
    case 'arrowright': case 'd':
      if (game.dx !== -1) { 
        game.dx = 1; 
        game.dy = 0; 
        console.log('➡️ 向右移动');
      }
      break;
    case ' ': // 空格键暂停
      e.preventDefault();
      togglePause();
      break;
  }
}

// ==================== 启动游戏 ====================
// 确保DOM完全加载后再执行
document.addEventListener('DOMContentLoaded', function() {
  console.log('📄 DOM 完全加载，开始初始化游戏');
  setTimeout(initGame, 100); // 稍微延迟确保所有元素就绪
});

// 调试：检查当前焦点
setInterval(function() {
  if (document.activeElement === elements.canvas) {
    console.log('🎯 Canvas 当前获得焦点');
  }
}, 5000);
</script>
