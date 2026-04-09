---
layout: default
title: 🎮 游戏中心
---

<style>
  /* 游戏容器样式 */
  .game-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem 1rem;
  }
  
  /* 画布响应式 */
  #gameCanvas {
    border: 3px solid #222;
    background: #111;
    display: block;
    max-width: 100%;
    height: auto;
    margin: 0 auto;
    border-radius: 8px;
  }
  
  /* 分数面板 */
  .stats-panel {
    display: flex;
    justify-content: center;
    gap: 3rem;
    margin: 2rem 0;
    flex-wrap: wrap;
  }
  
  .stat-item {
    text-align: center;
    min-width: 120px;
  }
  
  .stat-label {
    font-size: 0.9rem;
    color: #666;
    margin-bottom: 0.5rem;
  }
  
  .stat-value {
    font-size: 2.5rem;
    font-weight: bold;
    color: #222;
  }
  
  /* 按钮样式 */
  .control-buttons {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin: 2rem 0;
    flex-wrap: wrap;
  }
  
  .game-btn {
    padding: 0.9rem 2.2rem;
    color: #222;
    border: 2px solid #222;
    border-radius: 6px;
    background: transparent;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s;
    font-size: 1rem;
  }
  
  .game-btn:hover {
    background: #222;
    color: white;
  }
  
  /* 操作说明 */
  .instructions {
    background: #f9f9f9;
    border-radius: 8px;
    padding: 1.5rem;
    margin-top: 2rem;
    border-left: 4px solid #222;
  }
  
  /* 手机触摸提示 */
  .mobile-hint {
    text-align: center;
    color: #666;
    font-size: 0.9rem;
    margin-top: 1rem;
    display: none;
  }
  
  /* 媒体查询：手机优化 */
  @media (max-width: 768px) {
    .game-container {
      padding: 1rem 0.5rem;
    }
    
    .stats-panel {
      gap: 1.5rem;
    }
    
    .stat-item {
      min-width: 100px;
    }
    
    .control-buttons {
      flex-direction: column;
      align-items: center;
    }
    
    .game-btn {
      width: 90%;
      max-width: 300px;
    }
    
    .mobile-hint {
      display: block;
    }
  }
  
  @media (max-width: 480px) {
    #gameCanvas {
      max-width: 95vw;
    }
  }
</style>

<div class="game-container">
  <h1 style="text-align: center; margin-bottom: 0.5rem;">🐍 贪吃蛇游戏</h1>
  <p style="text-align: center; color: #666; margin-bottom: 2rem;">
    用键盘或触摸控制蛇的移动，吃到食物变长，避免撞墙或撞到自己
  </p>
  
  <!-- 游戏画布 -->
  <div style="text-align: center;">
    <canvas id="gameCanvas" width="400" height="400"></canvas>
  </div>
  
  <p class="mobile-hint">📱 在手机上滑动屏幕控制方向</p>
  
  <!-- 分数面板 -->
  <div class="stats-panel">
    <div class="stat-item">
      <div class="stat-label">分数</div>
      <div id="score" class="stat-value">0</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">最高分</div>
      <div id="highScore" class="stat-value">0</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">长度</div>
      <div id="length" class="stat-value">1</div>
    </div>
  </div>
  
  <!-- 控制按钮 -->
  <div class="control-buttons">
    <button id="startBtn" class="game-btn">开始游戏</button>
    <button id="pauseBtn" class="game-btn">暂停/继续</button>
    <button id="resetBtn" class="game-btn">重新开始</button>
  </div>
  
  <!-- 操作说明 -->
  <div class="instructions">
    <h3 style="margin-top: 0;">游戏说明</h3>
    <ul style="margin-bottom: 0; line-height: 1.6;">
      <li><strong>控制方式</strong>：
        <ul>
          <li>电脑：<kbd>↑↓←→</kbd> 方向键 或 <kbd>W</kbd><kbd>A</kbd><kbd>S</kbd><kbd>D</kbd></li>
          <li>手机：在屏幕上<strong>左右上下滑动</strong>控制方向</li>
        </ul>
      </li>
      <li><strong>游戏规则</strong>：
        <ul>
          <li>每吃一个红色食物：+10 分，蛇长度 +1</li>
          <li>撞墙或撞到自己身体：游戏结束</li>
          <li>最高分会自动保存在浏览器中</li>
        </ul>
      </li>
    </ul>
  </div>
</div>

<script>
// ==================== 游戏配置 ====================
const config = {
  gridSize: 20,       // 网格大小
  initialSpeed: 150,  // 初始速度（毫秒）
  speedIncrease: 2,   // 每吃5个食物加速多少
  foodScore: 10       // 每个食物得分
};

// ==================== 游戏状态 ====================
let canvas, ctx;
let snake = [];
let food = {};
let dx = 0, dy = 0;
let score = 0;
let highScore = localStorage.getItem('snakeHighScore') || 0;
let gameInterval;
let isPaused = true;
let isGameOver = true;
let foodEaten = 0;    // 已吃食物计数（用于加速）

// ==================== DOM 元素 ====================
const scoreElement = document.getElementById('score');
const highScoreElement = document.getElementById('highScore');
const lengthElement = document.getElementById('length');
const startBtn = document.getElementById('startBtn');
const pauseBtn = document.getElementById('pauseBtn');
const resetBtn = document.getElementById('resetBtn');

// ==================== 初始化 ====================
function init() {
  canvas = document.getElementById('gameCanvas');
  ctx = canvas.getContext('2d');
  
  // 显示最高分
  highScoreElement.textContent = highScore;
  
  // 初始化游戏
  resetGame();
  draw();
  
  // 事件监听
  document.addEventListener('keydown', handleKeyPress);
  startBtn.addEventListener('click', startGame);
  pauseBtn.addEventListener('click', togglePause);
  resetBtn.addEventListener('click', resetGame);
  
  // 初始化触摸控制
  initTouchControls();
  
  // 按钮悬停效果
  const buttons = document.querySelectorAll('.game-btn');
  buttons.forEach(btn => {
    btn.addEventListener('mouseenter', () => {
      btn.style.background = '#222';
      btn.style.color = 'white';
    });
    btn.addEventListener('mouseleave', () => {
      btn.style.background = 'transparent';
      btn.style.color = '#222';
    });
  });
}

// ==================== 触摸控制 ====================
function initTouchControls() {
  let touchStartX = 0;
  let touchStartY = 0;
  const minSwipeDistance = 30;

  // 触摸开始
  document.addEventListener('touchstart', (e) => {
    if (isGameOver || isPaused) return;
    const touch = e.touches[0];
    touchStartX = touch.clientX;
    touchStartY = touch.clientY;
  }, { passive: true });

  // 触摸结束（判断方向）
  document.addEventListener('touchend', (e) => {
    if (isGameOver || isPaused || !touchStartX) return;

    const touch = e.changedTouches[0];
    const deltaX = touch.clientX - touchStartX;
    const deltaY = touch.clientY - touchStartY;

    // 防误触
    if (Math.abs(deltaX) < minSwipeDistance && Math.abs(deltaY) < minSwipeDistance) return;

    // 判断主滑动方向
    if (Math.abs(deltaX) > Math.abs(deltaY)) {
      // 横向滑动
      if (deltaX > 0 && dx !== -1) { dx = 1; dy = 0; }  // 右滑
      else if (deltaX < 0 && dx !== 1) { dx = -1; dy = 0; } // 左滑
    } else {
      // 纵向滑动
      if (deltaY > 0 && dy !== -1) { dx = 0; dy = 1; }  // 下滑
      else if (deltaY < 0 && dy !== 1) { dx = 0; dy = -1; } // 上滑
    }

    touchStartX = 0;
  }, { passive: true });
}

// ==================== 游戏控制 ====================
function startGame() {
  if (isGameOver) {
    resetGame();
    isGameOver = false;
  }
  
  if (isPaused) {
    isPaused = false;
    gameInterval = setInterval(gameLoop, getCurrentSpeed());
    startBtn.textContent = '游戏中...';
  }
}

function togglePause() {
  if (isGameOver) return;
  
  isPaused = !isPaused;
  if (isPaused) {
    clearInterval(gameInterval);
    startBtn.textContent = '继续游戏';
  } else {
    gameInterval = setInterval(gameLoop, getCurrentSpeed());
    startBtn.textContent = '游戏中...';
  }
}

function resetGame() {
  clearInterval(gameInterval);
  isPaused = true;
  isGameOver = true;
  
  // 重置蛇
  snake = [{x: 10, y: 10}];
  
  // 重置食物
  generateFood();
  
  // 重置状态
  dx = 0;
  dy = 0;
  score = 0;
  foodEaten = 0;
  
  // 更新显示
  updateScore();
  draw();
  
  startBtn.textContent = '开始游戏';
}

// ==================== 游戏逻辑 ====================
function gameLoop() {
  moveSnake();
  checkCollision();
  draw();
}

function moveSnake() {
  if (dx === 0 && dy === 0) return;
  
  const head = {x: snake[0].x + dx, y: snake[0].y + dy};
  snake.unshift(head);
  
  // 吃到食物
  if (head.x === food.x && head.y === food.y) {
    score += config.foodScore;
    foodEaten++;
    updateScore();
    generateFood();
    
    // 每吃5个食物加速
    if (foodEaten % 5 === 0) {
      clearInterval(gameInterval);
      gameInterval = setInterval(gameLoop, getCurrentSpeed());
    }
  } else {
    snake.pop();
  }
}

function generateFood() {
  let newFood;
  let onSnake;
  
  do {
    onSnake = false;
    newFood = {
      x: Math.floor(Math.random() * (canvas.width / config.gridSize)),
      y: Math.floor(Math.random() * (canvas.height / config.gridSize))
    };
    
    // 确保食物不在蛇身上
    for (let segment of snake) {
      if (segment.x === newFood.x && segment.y === newFood.y) {
        onSnake = true;
        break;
      }
    }
  } while (onSnake);
  
  food = newFood;
}

function checkCollision() {
  const head = snake[0];
  
  // 撞墙检测
  if (
    head.x < 0 ||
    head.x >= canvas.width / config.gridSize ||
    head.y < 0 ||
    head.y >= canvas.height / config.gridSize
  ) {
    gameOver();
    return;
  }
  
  // 撞自己检测
  for (let i = 1; i < snake.length; i++) {
    if (head.x === snake[i].x && head.y === snake[i].y) {
      gameOver();
      return;
    }
  }
}

function gameOver() {
  clearInterval(gameInterval);
  isGameOver = true;
  isPaused = true;
  
  // 更新最高分
  if (score > highScore) {
    highScore = score;
    localStorage.setItem('snakeHighScore', highScore);
    highScoreElement.textContent = highScore;
  }
  
  startBtn.textContent = '重新开始';
  
  // 显示游戏结束文字
  ctx.fillStyle = 'rgba(0, 0, 0, 0.7)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  ctx.fillStyle = '#fff';
  ctx.font = 'bold 24px Arial';
  ctx.textAlign = 'center';
  ctx.fillText('游戏结束!', canvas.width / 2, canvas.height / 2 - 20);
  ctx.font = '18px Arial';
  ctx.fillText(`得分: ${score}`, canvas.width / 2, canvas.height / 2 + 10);
}

// ==================== 渲染 ====================
function draw() {
  // 清空画布
  ctx.fillStyle = '#111';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  // 绘制蛇
  snake.forEach((segment, index) => {
    if (index === 0) {
      // 蛇头 - 亮绿色
      ctx.fillStyle = '#4CAF50';
    } else if (index === snake.length - 1) {
      // 蛇尾 - 暗绿色
      ctx.fillStyle = '#2E7D32';
    } else {
      // 蛇身 - 中等绿色
      ctx.fillStyle = '#66BB6A';
    }
    
    ctx.fillRect(
      segment.x * config.gridSize + 1,
      segment.y * config.gridSize + 1,
      config.gridSize - 2,
      config.gridSize - 2
    );
  });
  
  // 绘制食物
  ctx.fillStyle = '#FF5252';
  ctx.beginPath();
  const centerX = food.x * config.gridSize + config.gridSize / 2;
  const centerY = food.y * config.gridSize + config.gridSize / 2;
  ctx.arc(centerX, centerY, config.gridSize / 2 - 2, 0, Math.PI * 2);
  ctx.fill();
}

// ==================== 工具函数 ====================
function handleKeyPress(e) {
  if (isPaused && !isGameOver) return;
  
  switch(e.key) {
    case 'ArrowUp':
    case 'w':
    case 'W':
      if (dy !== 1) { dx = 0; dy = -1; }
      break;
    case 'ArrowDown':
    case 's':
    case 'S':
      if (dy !== -1) { dx = 0; dy = 1; }
      break;
    case 'ArrowLeft':
    case 'a':
    case 'A':
      if (dx !== 1) { dx = -1; dy = 0; }
      break;
    case 'ArrowRight':
    case 'd':
    case 'D':
      if (dx !== -1) { dx = 1; dy = 0; }
      break;
  }
}

function updateScore() {
  scoreElement.textContent = score;
  lengthElement.textContent = snake.length;
}

function getCurrentSpeed() {
  // 每吃5个食物加速一次
  const speedReduction = Math.floor(foodEaten / 5) * config.speedIncrease;
  return Math.max(config.initialSpeed - speedReduction, 50); // 最快50ms
}

// ==================== 启动游戏 ====================
if (document.readyState === 'loading') {
  document.addEventListener('DOMContentLoaded', init);
} else {
  init();
}
</script>

---
