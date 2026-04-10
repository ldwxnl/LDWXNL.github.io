---
layout: default
title: 🎮 游戏中心
---

<!-- 视口控制：防止缩放，启用触摸 -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
  /* 基础重置 */
  * {
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
  }
  
  html, body {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    overflow: hidden; /* ✅ 完全禁止滚动 */
    background: #fafafa;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  }
  
  /* 游戏容器 */
  .game-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 1rem;
    height: 100vh; /* ✅ 占据全屏高度 */
    display: flex;
    flex-direction: column;
  }
  
  /* 标题区域 */
  .header {
    text-align: center;
    margin-bottom: 1rem;
    flex-shrink: 0;
  }
  
  h1 {
    color: #222;
    margin: 0.5rem 0;
    font-size: 1.8rem;
  }
  
  .subtitle {
    color: #666;
    margin: 0.5rem 0 1rem;
    font-size: 1rem;
  }
  
  /* 游戏画布 - 响应式核心 */
  .canvas-wrapper {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0.5rem 0;
    min-height: 0; /* ✅ 防止溢出 */
  }
  
  #gameCanvas {
    border: 3px solid #222;
    background: #111;
    border-radius: 8px;
    touch-action: none; /* ✅ 禁用所有浏览器触摸操作 */
    
    /* ✅ 核心：动态尺寸计算 */
    width: 85vmin;  /* 视口较小尺寸的85% */
    height: 85vmin; /* 保持正方形 */
    max-width: 400px;
    max-height: 400px;
  }
  
  /* 分数面板 */
  .stats {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    margin: 1rem 0;
    flex-wrap: wrap;
    flex-shrink: 0;
  }
  
  .stat {
    text-align: center;
    min-width: 100px;
  }
  
  .stat-label {
    color: #666;
    font-size: 0.85rem;
    margin-bottom: 0.3rem;
  }
  
  .stat-value {
    color: #222;
    font-size: 2rem;
    font-weight: bold;
  }
  
  /* 控制按钮 */
  .controls {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin: 1rem 0;
    flex-wrap: wrap;
    flex-shrink: 0;
  }
  
  .btn {
    padding: 0.8rem 1.8rem;
    border: 2px solid #222;
    border-radius: 6px;
    background: transparent;
    color: #222;
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.2s;
    touch-action: manipulation; /* ✅ 优化触摸响应 */
  }
  
  .btn:hover, .btn:active {
    background: #222;
    color: white;
  }
  
  /* 操作说明 */
  .instructions {
    background: #f5f5f5;
    border-radius: 8px;
    padding: 1.2rem;
    margin-top: 1rem;
    border-left: 4px solid #222;
    flex-shrink: 0;
  }
  
  .instructions h3 {
    margin-top: 0;
    color: #333;
  }
  
  .instructions ul {
    margin: 0.5rem 0;
    padding-left: 1.2rem;
  }
  
  .instructions li {
    margin: 0.3rem 0;
    line-height: 1.4;
  }
  
  kbd {
    background: #eee;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 0.2rem 0.5rem;
    font-family: monospace;
    font-size: 0.9em;
  }
  
  /* 手机特定优化 */
  .mobile-hint {
    text-align: center;
    color: #888;
    font-size: 0.9rem;
    margin: 0.5rem 0;
    display: none;
  }
  
  /* 媒体查询 */
  @media (max-width: 768px) {
    .game-container {
      padding: 0.8rem;
    }
    
    h1 {
      font-size: 1.6rem;
    }
    
    .subtitle {
      font-size: 0.9rem;
    }
    
    #gameCanvas {
      width: 90vmin;  /* ✅ 手机上调大一点 */
      height: 90vmin;
    }
    
    .stats {
      gap: 1rem;
    }
    
    .stat {
      min-width: 80px;
    }
    
    .stat-value {
      font-size: 1.8rem;
    }
    
    .controls {
      gap: 0.8rem;
    }
    
    .btn {
      padding: 0.7rem 1.5rem;
      font-size: 0.95rem;
    }
    
    .mobile-hint {
      display: block;
    }
  }
  
  @media (max-width: 480px) {
    #gameCanvas {
      width: 92vmin;
      height: 92vmin;
    }
    
    .controls {
      flex-direction: column;
      align-items: center;
    }
    
    .btn {
      width: 90%;
      max-width: 280px;
    }
  }
</style>

<div class="game-container">
  <!-- 标题 -->
  <div class="header">
    <h1>🐍 贪吃蛇游戏</h1>
    <p class="subtitle">滑动屏幕或使用键盘控制，吃到食物变长</p>
  </div>
  
  <!-- 游戏画布 -->
  <div class="canvas-wrapper">
    <canvas id="gameCanvas"></canvas>
  </div>
  
  <p class="mobile-hint">📱 在画布上滑动控制方向</p>
  
  <!-- 分数显示 -->
  <div class="stats">
    <div class="stat">
      <div class="stat-label">分数</div>
      <div id="score" class="stat-value">0</div>
    </div>
    <div class="stat">
      <div class="stat-label">最高分</div>
      <div id="highScore" class="stat-value">0</div>
    </div>
    <div class="stat">
      <div class="stat-label">长度</div>
      <div id="length" class="stat-value">1</div>
    </div>
  </div>
  
  <!-- 控制按钮 -->
  <div class="controls">
    <button id="startBtn" class="btn">开始游戏</button>
    <button id="pauseBtn" class="btn">暂停/继续</button>
    <button id="resetBtn" class="btn">重新开始</button>
  </div>
  
  <!-- 操作说明 -->
  <div class="instructions">
    <h3>游戏说明</h3>
    <ul>
      <li><strong>控制方式</strong>：
        <ul>
          <li>电脑：<kbd>方向键</kbd> 或 <kbd>WASD</kbd></li>
          <li>手机：<strong>在画布上滑动</strong>（上下左右）</li>
        </ul>
      </li>
      <li><strong>游戏规则</strong>：
        <ul>
          <li>每吃一个食物：<strong>+10 分</strong>，蛇长度 <strong>+1</strong></li>
          <li>撞墙或撞到自己：<strong>游戏结束</strong></li>
          <li>最高分自动保存</li>
        </ul>
      </li>
    </ul>
  </div>
</div>

<script>
// ==================== 游戏配置 ====================
const CONFIG = {
  GRID_SIZE: 20,
  INITIAL_SPEED: 150,
  FOOD_SCORE: 10,
  MIN_SWIPE_DISTANCE: 15  // ✅ 降低滑动阈值
};

// ==================== 游戏状态 ====================
let canvas, ctx;
let snake = [];
let food = { x: 0, y: 0 };
let dx = 0, dy = 0;
let score = 0;
let highScore = localStorage.getItem('snakeHighScore') || 0;
let gameLoopId = null;
let isPaused = true;
let isGameOver = true;
let touchStartX = 0, touchStartY = 0;

// ==================== DOM 元素 ====================
const scoreEl = document.getElementById('score');
const highScoreEl = document.getElementById('highScore');
const lengthEl = document.getElementById('length');
const startBtn = document.getElementById('startBtn');
const pauseBtn = document.getElementById('pauseBtn');
const resetBtn = document.getElementById('resetBtn');

// ==================== 初始化 ====================
function init() {
  canvas = document.getElementById('gameCanvas');
  ctx = canvas.getContext('2d');
  
  // 设置画布尺寸（基于CSS计算后的实际尺寸）
  const size = Math.min(canvas.offsetWidth, canvas.offsetHeight);
  canvas.width = size;
  canvas.height = size;
  
  // 显示最高分
  highScoreEl.textContent = highScore;
  
  // 初始化游戏
  resetGame();
  draw();
  
  // 事件监听
  document.addEventListener('keydown', handleKeyDown);
  startBtn.addEventListener('click', startGame);
  pauseBtn.addEventListener('click', togglePause);
  resetBtn.addEventListener('click', resetGame);
  
  // 触摸控制
  initTouchControls();
  
  // 防止上下文菜单
  canvas.addEventListener('contextmenu', (e) => e.preventDefault());
}

// ==================== 触摸控制 ====================
function initTouchControls() {
  // 触摸开始
  canvas.addEventListener('touchstart', (e) => {
    if (e.touches.length !== 1) return;
    
    const touch = e.touches[0];
    touchStartX = touch.clientX;
    touchStartY = touch.clientY;
    
    // ✅ 完全阻止所有默认行为
    e.preventDefault();
    e.stopPropagation();
    
    return false;
  }, { passive: false });
  
  // 触摸移动
  canvas.addEventListener('touchmove', (e) => {
    e.preventDefault();
    e.stopPropagation();
  }, { passive: false });
  
  // 触摸结束
  canvas.addEventListener('touchend', (e) => {
    if (!touchStartX || isPaused || isGameOver) return;
    
    if (e.changedTouches.length !== 1) return;
    const touch = e.changedTouches[0];
    
    const deltaX = touch.clientX - touchStartX;
    const deltaY = touch.clientY - touchStartY;
    
    // ✅ 更灵敏的阈值
    if (Math.abs(deltaX) < CONFIG.MIN_SWIPE_DISTANCE && 
        Math.abs(deltaY) < CONFIG.MIN_SWIPE_DISTANCE) {
      touchStartX = 0;
      return;
    }
    
    // 判断方向
    if (Math.abs(deltaX) > Math.abs(deltaY)) {
      // 横向
      if (deltaX > 0 && dx !== -1) { dx = 1; dy = 0; }    // 右
      else if (deltaX < 0 && dx !== 1) { dx = -1; dy = 0; } // 左
    } else {
      // 纵向
      if (deltaY > 0 && dy !== -1) { dx = 0; dy = 1; }    // 下
      else if (deltaY < 0 && dy !== 1) { dx = 0; dy = -1; } // 上
    }
    
    touchStartX = 0;
    e.preventDefault();
    e.stopPropagation();
    
    return false;
  }, { passive: false });
}

// ==================== 游戏控制 ====================
function startGame() {
  if (isGameOver) {
    resetGame();
    isGameOver = false;
  }
  
  if (isPaused) {
    isPaused = false;
    gameLoopId = setInterval(gameLoop, CONFIG.INITIAL_SPEED);
    startBtn.textContent = '游戏中...';
  }
}

function togglePause() {
  if (isGameOver) return;
  
  isPaused = !isPaused;
  if (isPaused) {
    clearInterval(gameLoopId);
    startBtn.textContent = '继续游戏';
  } else {
    gameLoopId = setInterval(gameLoop, CONFIG.INITIAL_SPEED);
    startBtn.textContent = '游戏中...';
  }
}

function resetGame() {
  clearInterval(gameLoopId);
  isPaused = true;
  isGameOver = true;
  
  // 重置蛇
  const center = Math.floor(canvas.width / CONFIG.GRID_SIZE / 2);
  snake = [{ x: center, y: center }];
  
  // 生成食物
  generateFood();
  
  // 重置状态
  dx = dy = 0;
  score = 0;
  
  // 更新显示
  updateUI();
  draw();
  
  startBtn.textContent = '开始游戏';
}

// ==================== 游戏逻辑 ====================
function gameLoop() {
  if (dx === 0 && dy === 0) return;
  
  // 移动蛇
  const head = { x: snake[0].x + dx, y: snake[0].y + dy };
  snake.unshift(head);
  
  // 检查是否吃到食物
  if (head.x === food.x && head.y === food.y) {
    score += CONFIG.FOOD_SCORE;
    generateFood();
  } else {
    snake.pop();
  }
  
  // 检查碰撞
  if (checkCollision(head)) {
    gameOver();
    return;
  }
  
  // 更新显示
  updateUI();
  draw();
}

function generateFood() {
  const gridCount = canvas.width / CONFIG.GRID_SIZE;
  let newFood;
  let onSnake;
  
  do {
    onSnake = false;
    newFood = {
      x: Math.floor(Math.random() * gridCount),
      y: Math.floor(Math.random() * gridCount)
    };
    
    for (const segment of snake) {
      if (segment.x === newFood.x && segment.y === newFood.y) {
        onSnake = true;
        break;
      }
    }
  } while (onSnake);
  
  food = newFood;
}

function checkCollision(head) {
  const gridCount = canvas.width / CONFIG.GRID_SIZE;
  
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

function gameOver() {
  clearInterval(gameLoopId);
  isGameOver = true;
  isPaused = true;
  
  // 更新最高分
  if (score > highScore) {
    highScore = score;
    localStorage.setItem('snakeHighScore', highScore);
    highScoreEl.textContent = highScore;
  }
  
  startBtn.textContent = '重新开始';
  
  // 显示游戏结束
  ctx.fillStyle = 'rgba(0, 0, 0, 0.7)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  ctx.fillStyle = '#fff';
  ctx.font = 'bold 24px Arial';
  ctx.textAlign = 'center';
  ctx.fillText('游戏结束!', canvas.width / 2, canvas.height / 2 - 20);
  ctx.font = '16px Arial';
  ctx.fillText(`得分: ${score}`, canvas.width / 2, canvas.height / 2 + 10);
}

// ==================== 渲染 ====================
function draw() {
  // 清空画布
  ctx.fillStyle = '#111';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  const cellSize = CONFIG.GRID_SIZE;
  
  // 绘制蛇
  snake.forEach((segment, index) => {
    if (index === 0) {
      ctx.fillStyle = '#4CAF50'; // 蛇头
    } else {
      ctx.fillStyle = '#8BC34A'; // 蛇身
    }
    
    ctx.fillRect(
      segment.x * cellSize + 1,
      segment.y * cellSize + 1,
      cellSize - 2,
      cellSize - 2
    );
  });
  
  // 绘制食物
  ctx.fillStyle = '#FF5252';
  ctx.beginPath();
  const centerX = food.x * cellSize + cellSize / 2;
  const centerY = food.y * cellSize + cellSize / 2;
  ctx.arc(centerX, centerY, cellSize / 2 - 2, 0, Math.PI * 2);
  ctx.fill();
}

// ==================== 工具函数 ====================
function handleKeyDown(e) {
  if (isPaused && !isGameOver) return;
  
  switch(e.key) {
    case 'ArrowUp': case 'w': case 'W':
      if (dy !== 1) { dx = 0; dy = -1; } break;
    case 'ArrowDown': case 's': case 'S':
      if (dy !== -1) { dx = 0; dy = 1; } break;
    case 'ArrowLeft': case 'a': case 'A':
      if (dx !== 1) { dx = -1; dy = 0; } break;
