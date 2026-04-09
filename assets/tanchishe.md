---
layout: default
title: 🐍 贪吃蛇游戏
---

<div style="max-width: 800px; margin: 0 auto;">

# 🐍 贪吃蛇游戏

用 <kbd>方向键</kbd> 或 <kbd>WASD</kbd> 控制蛇移动，吃到红色食物变长，碰到墙壁或自己身体游戏结束。

<div style="text-align: center; margin: 2rem 0;">
  <canvas id="gameCanvas" width="400" height="400" style="border: 2px solid #222; display: block; margin: 0 auto; background: #111;"></canvas>
</div>

<div style="display: flex; justify-content: center; gap: 2rem; margin: 1rem 0; flex-wrap: wrap;">
  <div style="text-align: center;">
    <div style="font-size: 0.9rem; color: #666; margin-bottom: 0.5rem;">分数</div>
    <div id="score" style="font-size: 2rem; font-weight: bold; color: #222;">0</div>
  </div>
  <div style="text-align: center;">
    <div style="font-size: 0.9rem; color: #666; margin-bottom: 0.5rem;">最高分</div>
    <div id="highScore" style="font-size: 2rem; font-weight: bold; color: #222;">0</div>
  </div>
  <div style="text-align: center;">
    <div style="font-size: 0.9rem; color: #666; margin-bottom: 0.5rem;">长度</div>
    <div id="length" style="font-size: 2rem; font-weight: bold; color: #222;">1</div>
  </div>
</div>

<div style="text-align: center; margin: 2rem 0;">
  <button id="startBtn" style="padding: 0.9rem 2.5rem; margin: 0 0.5rem; color: #222; border: 2px solid #222; border-radius: 6px; background: transparent; font-weight: 600; cursor: pointer; transition: all 0.3s;">开始游戏</button>
  <button id="pauseBtn" style="padding: 0.9rem 2.5rem; margin: 0 0.5rem; color: #222; border: 2px solid #222; border-radius: 6px; background: transparent; font-weight: 600; cursor: pointer; transition: all 0.3s;">暂停/继续</button>
  <button id="resetBtn" style="padding: 0.9rem 2.5rem; margin: 0 0.5rem; color: #222; border: 2px solid #222; border-radius: 6px; background: transparent; font-weight: 600; cursor: pointer; transition: all 0.3s;">重新开始</button>
</div>

<div style="margin: 2rem 0; padding: 1.5rem; background: #f9f9f9; border-radius: 8px; border-left: 4px solid #222;">
  <h3 style="margin-top: 0;">游戏说明</h3>
  <ul style="margin-bottom: 0;">
    <li>控制：<kbd>↑</kbd> <kbd>↓</kbd> <kbd>←</kbd> <kbd>→</kbd> 或 <kbd>W</kbd> <kbd>A</kbd> <kbd>S</kbd> <kbd>D</kbd></li>
    <li>每吃一个食物：+10 分，蛇长度 +1</li>
    <li>撞墙或撞到自己：游戏结束</li>
    <li>最高分会保存在浏览器中</li>
  </ul>
</div>

</div>

<script>
// 游戏配置
const config = {
  gridSize: 20,      // 网格大小
  initialSpeed: 150  // 初始速度（毫秒）
};

// 游戏状态
let canvas, ctx;
let snake = [];
let food = {};
let dx = 0, dy = 0;
let score = 0;
let highScore = localStorage.getItem('snakeHighScore') || 0;
let gameInterval;
let isPaused = true;
let isGameOver = true;

// 初始化
function init() {
  canvas = document.getElementById('gameCanvas');
  ctx = canvas.getContext('2d');
  
  document.getElementById('highScore').textContent = highScore;
  
  resetGame();
  draw();
  
  // 事件监听
  document.addEventListener('keydown', handleKeyPress);
  document.getElementById('startBtn').addEventListener('click', startGame);
  document.getElementById('pauseBtn').addEventListener('click', togglePause);
  document.getElementById('resetBtn').addEventListener('click', resetGame);
  
  // 按钮悬停效果
  document.querySelectorAll('button').forEach(btn => {
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

// 重置游戏
function resetGame() {
  clearInterval(gameInterval);
  isPaused = true;
  isGameOver = true;
  
  // 初始化蛇
  snake = [
    {x: 10, y: 10}
  ];
  
  // 初始化食物
  generateFood();
  
  // 重置方向和分数
  dx = 0;
  dy = 0;
  score = 0;
  
  // 更新显示
  updateScore();
  draw();
  
  document.getElementById('startBtn').textContent = '开始游戏';
}

// 开始游戏
function startGame() {
  if (isGameOver) {
    resetGame();
    isGameOver = false;
  }
  isPaused = false;
  gameInterval = setInterval(gameLoop, config.initialSpeed);
  document.getElementById('startBtn').textContent = '游戏中...';
}

// 暂停/继续
function togglePause() {
  if (isGameOver) return;
  
  isPaused = !isPaused;
  if (isPaused) {
    clearInterval(gameInterval);
  } else {
    gameInterval = setInterval(gameLoop, config.initialSpeed);
  }
}

// 游戏主循环
function gameLoop() {
  moveSnake();
  checkCollision();
  draw();
}

// 移动蛇
function moveSnake() {
  if (dx === 0 && dy === 0) return;
  
  const head = {x: snake[0].x + dx, y: snake[0].y + dy};
  snake.unshift(head);
  
  // 检查是否吃到食物
  if (head.x === food.x && head.y === food.y) {
    score += 10;
    generateFood();
    updateScore();
  } else {
    snake.pop();
  }
}

// 生成食物
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

// 检查碰撞
function checkCollision() {
  const head = snake[0];
  
  // 撞墙
  if (
    head.x < 0 || 
    head.x >= canvas.width / config.gridSize ||
    head.y < 0 || 
    head.y >= canvas.height / config.gridSize
  ) {
    gameOver();
    return;
  }
  
  // 撞自己
  for (let i = 1; i < snake.length; i++) {
    if (head.x === snake[i].x && head.y === snake[i].y) {
      gameOver();
      return;
    }
  }
}

// 游戏结束
function gameOver() {
  clearInterval(gameInterval);
  isGameOver = true;
  isPaused = true;
  
  if (score > highScore) {
    highScore = score;
    localStorage.setItem('snakeHighScore', highScore);
    document.getElementById('highScore').textContent = highScore;
  }
  
  document.getElementById('startBtn').textContent = '重新开始';
  
  // 显示游戏结束文字
  ctx.fillStyle = 'rgba(0, 0, 0, 0.7)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  ctx.fillStyle = '#fff';
  ctx.font = '24px Arial';
  ctx.textAlign = 'center';
  ctx.fillText('游戏结束!', canvas.width / 2, canvas.height / 2 - 20);
  ctx.font = '16px Arial';
  ctx.fillText(`得分: ${score}`, canvas.width / 2, canvas.height / 2 + 10);
}

// 绘制游戏
function draw() {
  // 清空画布
  ctx.fillStyle = '#111';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  // 绘制蛇
  snake.forEach((segment, index) => {
    ctx.fillStyle = index === 0 ? '#4CAF50' : '#8BC34A'; // 头绿色，身体浅绿
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
  
  // 绘制网格（可选，调试用）
  if (false) { // 设置为 true 显示网格
    ctx.strokeStyle = '#222';
    ctx.lineWidth = 0.5;
    for (let x = 0; x <= canvas.width; x += config.gridSize) {
      ctx.beginPath();
      ctx.moveTo(x, 0);
      ctx.lineTo(x, canvas.height);
      ctx.stroke();
    }
    for (let y = 0; y <= canvas.height; y += config.gridSize) {
      ctx.beginPath();
      ctx.moveTo(0, y);
      ctx.lineTo(canvas.width, y);
      ctx.stroke();
    }
  }
}

// 按键处理
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

// 更新分数显示
function updateScore() {
  document.getElementById('score').textContent = score;
  document.getElementById('length').textContent = snake.length;
}

// 页面加载完成后初始化游戏
if (document.readyState === 'loading') {
  document.addEventListener('DOMContentLoaded', init);
} else {
  init();
}
</script>

<style>
  kbd {
    background: #f1f1f1;
    border: 1px solid #ccc;
    border-radius: 3px;
    padding: 2px 6px;
    font-family: monospace;
    font-size: 0.9em;
    box-shadow: 0 1px 0 rgba(0,0,0,0.2);
  }
  
  @media (max-width: 768px) {
    #gameCanvas {
      width: 95vw;
      height: 95vw;
      max-width: 400px;
      max-height: 400px;
    }
  }
</style>
