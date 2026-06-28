---
layout: default
title: 🐍 贪吃蛇游戏
permalink: game/tanchishe
---

<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
    <title>🐍 贪吃蛇 - 单机/AI/联机</title>
    <style>
        *{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;-webkit-user-select:none;user-select:none}
        html,body{width:100%;min-height:100vh;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#1a1a1a;color:#e0e0e0;overflow-x:hidden}
        .app{max-width:800px;margin:0 auto;padding:1rem;min-height:100vh;display:flex;flex-direction:column}
        .header{text-align:center;padding:0.8rem 0;margin-bottom:0.8rem}
        .title{font-size:1.8rem;color:#4CAF50;margin-bottom:0.3rem}
        .sub{color:#aaa;font-size:0.9rem}
        .main{display:flex;flex-direction:column;gap:1rem;flex:1}
        
        /* 模式选择 */
        .mode-bar{display:flex;gap:0.5rem;background:#2a2a2a;border-radius:10px;padding:0.5rem}
        .mode-btn{flex:1;padding:0.6rem;background:#333;border:2px solid transparent;border-radius:6px;color:#fff;font-weight:600;cursor:pointer;text-align:center;transition:all 0.2s}
        .mode-btn.active{border-color:#4CAF50;background:rgba(76,175,80,0.15)}
        .mode-btn:hover{background:#3a3a3a}
        
        /* 画布 */
        .canvas-wrap{position:relative;width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;overflow:hidden;box-shadow:0 8px 30px rgba(0,0,0,0.4);touch-action:none;margin:0 auto}
        #canvas{width:100%;height:100%;display:block;background:#111}
        .overlay{position:absolute;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.88);display:flex;flex-direction:column;justify-content:center;align-items:center;z-index:10}
        .otitle{font-size:1.6rem;color:#4CAF50;margin-bottom:0.8rem;text-align:center}
        .otext{font-size:1rem;color:#ccc;margin-bottom:1.2rem;text-align:center;line-height:1.5}
        .btn{padding:0.7rem 1.3rem;border:none;border-radius:8px;font-size:0.95rem;font-weight:600;cursor:pointer;transition:all 0.2s}
        .btn-green{background:linear-gradient(135deg,#4CAF50,#2E7D32);color:white}
        .btn-green:hover{transform:translateY(-2px);box-shadow:0 4px 12px rgba(76,175,80,0.3)}
        .btn-gray{background:#333;color:#fff;border:1px solid #444}
        .btn-gray:hover{background:#3a3a3a;border-color:#4CAF50}
        
        /* 分数 */
        .score-row{display:flex;justify-content:center;gap:1rem;background:#2a2a2a;border-radius:10px;padding:0.8rem 1.5rem;flex-wrap:wrap}
        .score-item{text-align:center;min-width:70px}
        .score-label{color:#aaa;font-size:0.75rem;margin-bottom:0.2rem}
        .score-val{color:#fff;font-size:1.5rem;font-weight:bold}
        
        /* 控制按钮 */
        .ctrl-row{display:flex;gap:0.5rem;justify-content:center;flex-wrap:wrap}
        
        /* 统计 */
        .stats{display:grid;grid-template-columns:repeat(3,1fr);gap:0.8rem;background:#2a2a2a;border-radius:10px;padding:0.8rem}
        .stat{text-align:center}
        .stat-l{color:#aaa;font-size:0.75rem;margin-bottom:0.2rem}
        .stat-v{color:#fff;font-size:1.1rem;font-weight:bold}
        
        /* 设置面板 */
        .settings{background:#2a2a2a;border-radius:10px;padding:1rem}
        .settings h3{color:#4CAF50;font-size:1rem;margin-bottom:0.8rem;border-left:3px solid #4CAF50;padding-left:0.6rem}
        .setting-row{display:flex;align-items:center;gap:0.5rem;margin-bottom:0.5rem;flex-wrap:wrap}
        .setting-row label{font-size:0.85rem;color:#ccc;min-width:80px}
        .setting-row input[type="range"]{flex:1;min-width:100px}
        .setting-row input[type="text"],.setting-row select{flex:1;padding:0.4rem 0.6rem;background:#333;border:1px solid #444;border-radius:4px;color:#fff;font-size:0.85rem;outline:none;min-width:80px}
        .setting-row input:focus{border-color:#4CAF50}
        .setting-row span{color:#4CAF50;font-weight:bold;min-width:30px}
        
        /* 颜色选择 */
        .color-grid{display:grid;grid-template-columns:repeat(6,1fr);gap:0.4rem;margin-bottom:0.5rem}
        .color-btn{width:100%;aspect-ratio:1;border-radius:6px;border:2px solid transparent;cursor:pointer;transition:all 0.2s}
        .color-btn.active{border-color:#fff;transform:scale(1.1)}
        
        /* 联机区域 */
        .online-area{display:none;margin-top:0.5rem}
        .online-area .input-row{display:flex;gap:0.5rem;margin-bottom:0.5rem;flex-wrap:wrap}
        .online-area .input-row input{flex:1;padding:0.5rem 0.8rem;background:#333;border:1px solid #444;border-radius:6px;color:#fff;font-size:0.85rem;outline:none;min-width:100px}
        .online-area .input-row input:focus{border-color:#4CAF50}
        .online-area .input-row button{padding:0.5rem 1rem;background:#4CAF50;border:none;border-radius:6px;color:#fff;font-weight:600;cursor:pointer}
        .status-bar{display:flex;justify-content:space-between;padding:0.4rem 0.6rem;background:#222;border-radius:4px;font-size:0.8rem;margin-bottom:0.5rem}
        .status-on{color:#4CAF50}
        .status-off{color:#f44336}
        
        /* 玩家列表 */
        .player-list{margin-top:0.3rem}
        .player-item{display:flex;align-items:center;gap:0.4rem;padding:0.3rem 0.5rem;background:#222;border-radius:4px;margin-bottom:0.2rem;font-size:0.8rem}
        .player-dot{width:10px;height:10px;border-radius:50%}
        .player-name{flex:1}
        .player-sc{color:#4CAF50;font-weight:bold}
        
        /* 手机控制 */
        .mobile-ctrl{display:none;margin-top:0.5rem}
        .dpad{display:grid;grid-template-areas:". up ." "left . right" ". down .";gap:10px;justify-content:center;margin:0 auto}
        .dpad-btn{width:56px;height:56px;border:none;border-radius:50%;background:#333;color:#fff;font-size:22px;cursor:pointer;touch-action:manipulation;display:flex;align-items:center;justify-content:center;box-shadow:0 3px 6px rgba(0,0,0,0.3)}
        .dpad-btn:active{background:#4CAF50;transform:scale(0.93)}
        .dpad-btn.u{grid-area:up}.dpad-btn.d{grid-area:down}.dpad-btn.l{grid-area:left}.dpad-btn.r{grid-area:right}
        
        .help{background:#2a2a2a;border-radius:10px;padding:0.8rem;font-size:0.85rem;line-height:1.5}
        
        @media(max-width:640px){
            .app{padding:0.5rem}
            .title{font-size:1.4rem}
            .canvas-wrap{max-width:95vw}
            .score-val{font-size:1.2rem}
            .mobile-ctrl{display:block}
            .color-grid{grid-template-columns:repeat(4,1fr)}
        }
    </style>
</head>
<body>
<div class="app">
    <header class="header">
        <h1 class="title">🐍 贪吃蛇</h1>
        <p class="sub">单机 · AI对战 · 联机</p>
    </header>
    
    <main class="main">
        <!-- 模式选择 -->
        <div class="mode-bar">
            <button class="mode-btn active" data-mode="single">🎮 单人</button>
            <button class="mode-btn" data-mode="ai">🤖 AI对战</button>
            <button class="mode-btn" data-mode="online">🌐 联机</button>
        </div>
        
        <!-- 画布 -->
        <div class="canvas-wrap">
            <canvas id="canvas"></canvas>
            <div id="overlay" class="overlay">
                <h2 id="otitle" class="otitle">🐍 贪吃蛇</h2>
                <p id="otext" class="otext">选择模式开始游戏</p>
                <button id="startBtn" class="btn btn-green">开始游戏</button>
            </div>
        </div>
        
        <!-- 分数 -->
        <div class="score-row">
            <div class="score-item"><div class="score-label">分数</div><div id="myScore" class="score-val">0</div></div>
            <div class="score-item"><div class="score-label">长度</div><div id="myLen" class="score-val">1</div></div>
            <div class="score-item"><div class="score-label">最高分</div><div id="hiScore" class="score-val">0</div></div>
        </div>
        
        <!-- 控制 -->
        <div class="ctrl-row">
            <button id="pauseBtn" class="btn btn-gray">暂停</button>
            <button id="restartBtn" class="btn btn-gray">重开</button>
        </div>
        
        <!-- 统计 -->
        <div class="stats">
            <div class="stat"><div class="stat-l">时间</div><div id="gameTime" class="stat-v">00:00</div></div>
            <div class="stat"><div class="stat-l">食物</div><div id="foodCnt" class="stat-v">0</div></div>
            <div class="stat"><div class="stat-l">存活</div><div id="aliveCnt" class="stat-v">0</div></div>
        </div>
        
        <!-- 设置 -->
        <div class="settings">
            <h3>⚙ 设置</h3>
            
            <!-- 单人/AI设置 -->
            <div id="singleSettings">
                <div class="setting-row">
                    <label>AI数量</label>
                    <input type="range" id="aiCount" min="0" max="5" value="0">
                    <span id="aiCountVal">0</span>
                </div>
                <div class="setting-row">
                    <label>AI难度</label>
                    <select id="aiDiff">
                        <option value="0">简单</option>
                        <option value="1" selected>中等</option>
                        <option value="2">困难</option>
                        <option value="3">地狱</option>
                    </select>
                </div>
                <div class="setting-row">
                    <label>速度</label>
                    <input type="range" id="speed" min="1" max="5" value="3">
                    <span id="speedVal">普通</span>
                </div>
            </div>
            
            <!-- 联机设置 -->
            <div id="onlineSettings" style="display:none">
                <div class="online-area" style="display:block">
                    <div class="input-row">
                        <input type="text" id="serverAddr" placeholder="服务器地址" value="localhost:8080">
                        <input type="text" id="playerName" placeholder="你的名字" maxlength="10" value="玩家">
                        <button onclick="connect()">连接</button>
                    </div>
                    <div class="status-bar">
                        <span id="connStatus" class="status-off">● 未连接</span>
                        <span id="playerCount">在线: 0</span>
                    </div>
                    <div class="player-list" id="playerList"></div>
                </div>
            </div>
            
            <h3 style="margin-top:0.8rem">🎨 皮肤</h3>
            <div class="color-grid" id="colorGrid">
                <div class="color-btn active" style="background:#4CAF50" data-color="#4CAF50"></div>
                <div class="color-btn" style="background:#2196F3" data-color="#2196F3"></div>
                <div class="color-btn" style="background:#FF5722" data-color="#FF5722"></div>
                <div class="color-btn" style="background:#9C27B0" data-color="#9C27B0"></div>
                <div class="color-btn" style="background:#FFEB3B" data-color="#FFEB3B"></div>
                <div class="color-btn" style="background:#00BCD4" data-color="#00BCD4"></div>
                <div class="color-btn" style="background:#E91E63" data-color="#E91E63"></div>
                <div class="color-btn" style="background:#795548" data-color="#795548"></div>
                <div class="color-btn" style="background:#607D8B" data-color="#607D8B"></div>
                <div class="color-btn" style="background:#CDDC39" data-color="#CDDC39"></div>
                <div class="color-btn" style="background:#FF9800" data-color="#FF9800"></div>
                <div class="color-btn" style="background:#03A9F4" data-color="#03A9F4"></div>
            </div>
            <div class="setting-row">
                <label>自定义</label>
                <input type="color" id="customColor" value="#4CAF50">
                <input type="text" id="customHex" value="#4CAF50" style="max-width:80px">
                <button class="btn btn-green" onclick="applyColor()" style="padding:0.4rem 0.8rem;font-size:0.8rem">应用</button>
            </div>
        </div>
        
        <!-- 手机控制 -->
        <div class="mobile-ctrl">
            <div class="dpad">
                <button class="dpad-btn u">↑</button>
                <button class="dpad-btn d">↓</button>
                <button class="dpad-btn l">←</button>
                <button class="dpad-btn r">→</button>
            </div>
        </div>
        
        <div class="help">
            <p><strong>操作：</strong> 方向键/WASD移动 · 空格暂停</p>
            <p><strong>单人：</strong> 经典模式，吃食物长大</p>
            <p><strong>AI对战：</strong> 与AI蛇竞争，撞死AI得分</p>
            <p><strong>联机：</strong> 连接服务器与其他玩家对战</p>
        </div>
    </main>
</div>

<script>
// ==================== 配置 ====================
const CFG = {
    GRID: 20,
    SPEEDS: [250, 190, 145, 115, 90],
    SPEED_NAMES: ['极慢', '慢速', '普通', '快速', '极快'],
    FOOD_SCORE: 10,
    AI_KILL: 30,
    AI_COLORS: ['#9C27B0', '#2196F3', '#FF9800', '#E91E63', '#00BCD4']
};

// ==================== 状态 ====================
const S = {
    cv: null, cx: null,
    player: { snake: [], dir: {dx:0,dy:0}, score: 0, len: 1, color: '#4CAF50', name: '玩家', id: null },
    ai: [],
    others: {},
    food: {x:0,y:0},
    hiScore: parseInt(localStorage.getItem('snakeHi')) || 0,
    paused: true, over: true, mode: 'single',
    loop: null, startTime: 0, elapsed: 0, foodCnt: 0,
    sock: null, conn: false,
    tx: 0, ty: 0
};

// ==================== 初始化 ====================
function init() {
    S.cv = document.getElementById('canvas');
    S.cx = S.cv.getContext('2d');
    resize();
    document.getElementById('hiScore').textContent = S.hiScore;
    
    // 事件
    document.addEventListener('keydown', onKey);
    document.getElementById('startBtn').onclick = start;
    document.getElementById('pauseBtn').onclick = pause;
    document.getElementById('restartBtn').onclick = reset;
    
    // 模式切换
    document.querySelectorAll('.mode-btn').forEach(b => {
        b.onclick = function() {
            document.querySelectorAll('.mode-btn').forEach(x => x.classList.remove('active'));
            this.classList.add('active');
            S.mode = this.dataset.mode;
            document.getElementById('singleSettings').style.display = S.mode === 'online' ? 'none' : 'block';
            document.getElementById('onlineSettings').style.display = S.mode === 'online' ? 'block' : 'none';
            reset();
        };
    });
    
    // AI设置
    document.getElementById('aiCount').oninput = function() {
        document.getElementById('aiCountVal').textContent = this.value;
    };
    document.getElementById('speed').oninput = function() {
        document.getElementById('speedVal').textContent = CFG.SPEED_NAMES[this.value - 1];
    };
    
    // 颜色选择
    document.querySelectorAll('.color-btn').forEach(b => {
        b.onclick = function() {
            document.querySelectorAll('.color-btn').forEach(x => x.classList.remove('active'));
            this.classList.add('active');
            S.player.color = this.dataset.color;
            document.getElementById('customColor').value = S.player.color;
            document.getElementById('customHex').value = S.player.color;
            draw();
        };
    });
    
    // 自定义颜色
    document.getElementById('customColor').oninput = function() {
        document.getElementById('customHex').value = this.value;
    };
    document.getElementById('customHex').oninput = function() {
        if (/^#[0-9A-Fa-f]{6}$/.test(this.value)) {
            document.getElementById('customColor').value = this.value;
        }
    };
    
    // 虚拟方向键
    document.querySelectorAll('.dpad-btn').forEach(b => {
        b.addEventListener('touchstart', e => { e.preventDefault(); dir(b.textContent); });
        b.addEventListener('mousedown', () => dir(b.textContent));
    });
    
    // 触摸滑动
    S.cv.addEventListener('touchstart', e => {
        if (e.touches.length !== 1) return;
        S.tx = e.touches[0].clientX;
        S.ty = e.touches[0].clientY;
    }, {passive:true});
    S.cv.addEventListener('touchend', e => {
        if (!S.tx || S.paused) return;
        const dx = e.changedTouches[0].clientX - S.tx;
        const dy = e.changedTouches[0].clientY - S.ty;
        if (Math.abs(dx) < 15 && Math.abs(dy) < 15) return;
        if (Math.abs(dx) > Math.abs(dy)) dir(dx > 0 ? '→' : '←');
        else dir(dy > 0 ? '↓' : '↑');
        S.tx = 0;
    }, {passive:true});
    
    window.addEventListener('resize', () => { resize(); draw(); });
    
    reset();
    draw();
}

function resize() {
    const c = S.cv.parentElement;
    const s = Math.min(c.clientWidth, c.clientHeight);
    S.cv.width = s;
    S.cv.height = s;
}

// ==================== 方向 ====================
function dir(d) {
    if (S.paused && !S.over) return;
    const dd = S.player.dir;
    switch(d) {
        case '↑': case 'ArrowUp': if (dd.dy !== 1) S.player.dir = {dx:0,dy:-1}; break;
        case '↓': case 'ArrowDown': if (dd.dy !== -1) S.player.dir = {dx:0,dy:1}; break;
        case '←': case 'ArrowLeft': if (dd.dx !== 1) S.player.dir = {dx:-1,dy:0}; break;
        case '→': case 'ArrowRight': if (dd.dx !== -1) S.player.dir = {dx:1,dy:0}; break;
    }
}

function onKey(e) {
    switch(e.key) {
        case 'ArrowUp': case 'w': case 'W': dir('↑'); break;
        case 'ArrowDown': case 's': case 'S': dir('↓'); break;
        case 'ArrowLeft': case 'a': case 'A': dir('←'); break;
        case 'ArrowRight': case 'd': case 'D': dir('→'); break;
        case ' ': e.preventDefault(); pause(); break;
    }
}

// ==================== 游戏控制 ====================
function start() {
    if (S.over) { reset(); S.over = false; }
    if (S.paused) {
        S.paused = false;
        S.startTime = Date.now() - S.elapsed;
        const speed = CFG.SPEEDS[parseInt(document.getElementById('speed').value) - 1];
        S.loop = setInterval(update, speed);
        document.getElementById('overlay').style.display = 'none';
        document.getElementById('startBtn').textContent = '游戏中...';
        
        // AI模式初始化AI
        if (S.mode === 'ai' || S.mode === 'single') {
            const cnt = parseInt(document.getElementById('aiCount').value);
            if (cnt > 0) initAI(cnt);
        }
        S.cv.focus();
    }
}

function pause() {
    if (S.over) return;
    S.paused = !S.paused;
    if (S.paused) {
        clearInterval(S.loop);
        showOverlay('暂停', '点击继续');
        document.getElementById('startBtn').textContent = '继续';
    } else {
        const speed = CFG.SPEEDS[parseInt(document.getElementById('speed').value) - 1];
        S.loop = setInterval(update, speed);
        document.getElementById('overlay').style.display = 'none';
        document.getElementById('startBtn').textContent = '游戏中...';
    }
}

function reset() {
    clearInterval(S.loop);
    S.paused = true;
    S.over = true;
    S.ai = [];
    S.others = {};
    
    const sz = Math.floor(S.cv.width / CFG.GRID);
    const cx = Math.floor(sz / 2);
    S.player.snake = [{x:cx, y:cx}];
    S.player.dir = {dx:0, dy:0};
    S.player.score = 0;
    S.player.len = 1;
    S.foodCnt = 0;
    S.elapsed = 0;
    
    genFood();
    upDisplay();
    draw();
    
    showOverlay('🐍 贪吃蛇', S.mode === 'ai' ? 'AI对战模式' : S.mode === 'online' ? '联机模式' : '单人模式');
    document.getElementById('startBtn').textContent = '开始游戏';
    document.getElementById('gameTime').textContent = '00:00';
    upStats();
}

// ==================== AI系统 ====================
function initAI(cnt) {
    S.ai = [];
    const sz = Math.floor(S.cv.width / CFG.GRID);
    for (let i = 0; i < cnt; i++) {
        let x, y;
        do {
            x = Math.floor(Math.random() * (sz - 4)) + 2;
            y = Math.floor(Math.random() * (sz - 4)) + 2;
        } while (occ(x, y));
        
        S.ai.push({
            snake: [{x, y}],
            dir: {dx: 1, dy: 0},
            color: CFG.AI_COLORS[i % CFG.AI_COLORS.length],
            lastMove: Date.now(),
            delay: [400, 230, 150, 90][parseInt(document.getElementById('aiDiff').value)]
        });
    }
    upStats();
}

function occ(x, y) {
    for (const s of S.player.snake) if (s.x === x && s.y === y) return true;
    for (const a of S.ai) for (const s of a.snake) if (s.x === x && s.y === y) return true;
    return false;
}

function updateAI() {
    const now = Date.now();
    for (let i = S.ai.length - 1; i >= 0; i--) {
        const a = S.ai[i];
        if (now - a.lastMove < a.delay) continue;
        
        // AI决策
        const head = a.snake[0];
        const dirs = [{dx:1,dy:0},{dx:-1,dy:0},{dx:0,dy:1},{dx:0,dy:-1}];
        const valid = dirs.filter(d => !(d.dx === -a.dir.dx && d.dy === -a.dir.dy));
        
        // 根据难度决策
        let chosen;
        const diff = parseInt(document.getElementById('aiDiff').value);
        if (diff >= 3) { // 地狱
            chosen = bestDir(head, valid, S.food);
        } else if (diff >= 2) { // 困难
            chosen = Math.random() < 0.4 ? bestDir(head, valid, S.food) : valid[Math.floor(Math.random() * valid.length)];
        } else if (diff >= 1) { // 中等
            chosen = Math.random() < 0.2 ? bestDir(head, valid, S.food) : valid[Math.floor(Math.random() * valid.length)];
        } else { // 简单
            chosen = valid[Math.floor(Math.random() * valid.length)];
        }
        
        if (chosen) a.dir = chosen;
        
        // 移动
        const nh = {x: head.x + a.dir.dx, y: head.y + a.dir.dy};
        a.snake.unshift(nh);
        
        if (nh.x === S.food.x && nh.y === S.food.y) {
            genFood();
        } else {
            a.snake.pop();
        }
        
        // 碰撞检测
        if (checkAICollision(a)) {
            S.player.score += CFG.AI_KILL;
            S.ai.splice(i, 1);
            upStats();
        }
        
        a.lastMove = now;
    }
}

function bestDir(from, dirs, target) {
    let best = null, bestScore = -Infinity;
    for (const d of dirs) {
        const nx = from.x + d.dx, ny = from.y + d.dy;
        const sc = -(Math.abs(target.x - nx) + Math.abs(target.y - ny));
        if (sc > bestScore) { bestScore = sc; best = d; }
    }
    return best;
}

function checkAICollision(a) {
    const h = a.snake[0];
    const sz = Math.floor(S.cv.width / CFG.GRID);
    if (h.x < 0 || h.x >= sz || h.y < 0 || h.y >= sz) return true;
    for (let i = 1; i < a.snake.length; i++) if (h.x === a.snake[i].x && h.y === a.snake[i].y) return true;
    for (const s of S.player.snake) if (h.x === s.x && h.y === s.y) return true;
    for (const o of S.ai) if (o !== a) for (const s of o.snake) if (h.x === s.x && h.y === s.y) return true;
    return false;
}

// ==================== 游戏逻辑 ====================
function update() {
    if (S.paused || S.over) return;
    
    S.elapsed = Date.now() - S.startTime;
    document.getElementById('gameTime').textContent = fmt(S.elapsed);
    
    // 移动玩家
    const h = {
        x: S.player.snake[0].x + S.player.dir.dx,
        y: S.player.snake[0].y + S.player.dir.dy
    };
    S.player.snake.unshift(h);
    
    if (h.x === S.food.x && h.y === S.food.y) {
        S.player.score += CFG.FOOD_SCORE;
        S.player.len = S.player.snake.length;
        S.foodCnt++;
        genFood();
    } else {
        S.player.snake.pop();
    }
    
    // 更新AI
    if (S.mode === 'ai' || (S.mode === 'single' && S.ai.length > 0)) {
        updateAI();
    }
    
    // 碰撞检测
    if (checkColl()) { over(); return; }
    
    upDisplay();
    upStats();
    draw();
}

function genFood() {
    const sz = Math.floor(S.cv.width / CFG.GRID);
    let f;
    do {
        f = {x: Math.floor(Math.random() * sz), y: Math.floor(Math.random() * sz)};
    } while (occ(f.x, f.y));
    S.food = f;
}

function checkColl() {
    const h = S.player.snake[0];
    const sz = Math.floor(S.cv.width / CFG.GRID);
    if (h.x < 0 || h.x >= sz || h.y < 0 || h.y >= sz) return true;
    for (let i = 1; i < S.player.snake.length; i++) if (h.x === S.player.snake[i].x && h.y === S.player.snake[i].y) return true;
    for (const a of S.ai) for (const s of a.snake) if (h.x === s.x && h.y === s.y) return true;
    for (const id in S.others) for (const s of S.others[id].snake) if (h.x === s.x && h.y === s.y) return true;
    return false;
}

function over() {
    clearInterval(S.loop);
    S.over = true;
    S.paused = true;
    if (S.player.score > S.hiScore) {
        S.hiScore = S.player.score;
        localStorage.setItem('snakeHi', S.hiScore);
        document.getElementById('hiScore').textContent = S.hiScore;
    }
    showOverlay('游戏结束', `得分: ${S.player.score}<br>长度: ${S.player.len}`);
    document.getElementById('startBtn').textContent = '重新开始';
    
    // 通知联机服务器
    if (S.sock && S.sock.readyState === WebSocket.OPEN) {
        S.sock.send(JSON.stringify({type:'dead', score:S.player.score}));
    }
}

// ==================== 渲染 ====================
function draw() {
    const ctx = S.cx, cv = S.cv, cell = CFG.GRID;
    ctx.fillStyle = '#111';
    ctx.fillRect(0, 0, cv.width, cv.height);
    
    // 网格
    ctx.strokeStyle = '#1a1a1a';
    ctx.lineWidth = 0.5;
    for (let x = 0; x < cv.width; x += cell) { ctx.beginPath(); ctx.moveTo(x,0); ctx.lineTo(x,cv.height); ctx.stroke(); }
    for (let y = 0; y < cv.height; y += cell) { ctx.beginPath(); ctx.moveTo(0,y); ctx.lineTo(cv.width,y); ctx.stroke(); }
    
    // 食物
    ctx.fillStyle = '#FF5252';
    ctx.shadowColor = '#FF525280';
    ctx.shadowBlur = 8;
    ctx.beginPath();
    ctx.arc(S.food.x*cell+cell/2, S.food.y*cell+cell/2, cell/2-2, 0, Math.PI*2);
    ctx.fill();
    ctx.shadowBlur = 0;
    
    // AI蛇
    for (const a of S.ai) drawSnake(a.snake, a.color, false);
    
    // 其他玩家
    for (const id in S.others) drawSnake(S.others[id].snake, S.others[id].color || '#666', false);
    
    // 自己
    drawSnake(S.player.snake, S.player.color, true);
}

function drawSnake(snake, color, me) {
    const ctx = S.cx, cell = CFG.GRID;
    snake.forEach((seg, i) => {
        if (i === 0) {
            ctx.fillStyle = me ? color : '#FFF';
            ctx.fillRect(seg.x*cell+1, seg.y*cell+1, cell-2, cell-2);
            ctx.fillStyle = me ? '#FFF' : color;
            ctx.fillRect(seg.x*cell+4, seg.y*cell+4, cell-8, cell-8);
        } else {
            ctx.fillStyle = color;
            ctx.fillRect(seg.x*cell+1, seg.y*cell+1, cell-2, cell-2);
        }
    });
}

// ==================== UI ====================
function upDisplay() {
    document.getElementById('myScore').textContent = S.player.score;
    document.getElementById('myLen').textContent = S.player.len;
    document.getElementById('foodCnt').textContent = S.foodCnt;
}

function upStats() {
    const alive = S.ai.length + (S.over ? 0 : 1) + Object.keys(S.others).length;
    document.getElementById('aliveCnt').textContent = alive;
}

function showOverlay(title, text) {
    document.getElementById('otitle').innerHTML = title;
    document.getElementById('otext').innerHTML = text;
    document.getElementById('overlay').style.display = 'flex';
}

function fmt(ms) {
    const s = Math.floor(ms / 1000);
    return `${String(Math.floor(s/60)).padStart(2,'0')}:${String(s%60).padStart(2,'0')}`;
}

function applyColor() {
    const hex = document.getElementById('customHex').value;
    if (/^#[0-9A-Fa-f]{6}$/.test(hex)) {
        S.player.color = hex;
        document.querySelectorAll('.color-btn').forEach(c => c.classList.remove('active'));
        draw();
    }
}

// ==================== 联机 ====================
function connect() {
    const addr = document.getElementById('serverAddr').value || 'localhost:8080';
    const name = document.getElementById('playerName').value || '玩家';
    S.player.name = name;
    
    if (S.sock) S.sock.close();
    
    try {
        S.sock = new WebSocket('ws://' + addr);
        S.sock.onopen = () => {
            S.conn = true;
            document.getElementById('connStatus').className = 'status-on';
            document.getElementById('connStatus').textContent = '● 已连接';
            S.sock.send(JSON.stringify({type:'join', name:S.player.name, color:S.player.color}));
        };
        S.sock.onmessage = e => {
            const m = JSON.parse(e.data);
            switch(m.type) {
                case 'init':
                    S.player.id = m.id;
                    if (m.players) m.players.forEach(p => {
                        if (p.id !== S.player.id) S.others[p.id] = {snake:p.snake, score:p.score, color:p.color, name:p.name};
                    });
                    if (m.food) S.food = m.food;
                    upPlayerList();
                    upStats();
                    draw();
                    break;
                case 'player_join':
                    S.others[m.id] = {snake:m.snake, score:m.score, color:m.color, name:m.name};
                    upPlayerList();
                    upStats();
                    break;
                case 'player_leave':
                    delete S.others[m.id];
                    upPlayerList();
                    upStats();
                    break;
                case 'food_update':
                    if (m.food) S.food = m.food;
                    break;
                case 'game_over':
                    delete S.others[m.id];
                    upPlayerList();
                    upStats();
                    break;
            }
        };
        S.sock.onclose = () => {
            S.conn = false;
            document.getElementById('connStatus').className = 'status-off';
            document.getElementById('connStatus').textContent = '● 已断开';
        };
        S.sock.onerror = () => {
            document.getElementById('connStatus').className = 'status-off';
            document.getElementById('connStatus').textContent = '● 连接失败';
        };
    } catch(e) {
        alert('连接失败: ' + e.message);
    }
}

function upPlayerList() {
    const el = document.getElementById('playerList');
    let html = `<div class="player-item"><div class="player-dot" style="background:${S.player.color}"></div><span class="player-name">${S.player.name} (我)</span><span class="player-sc">${S.player.score}</span></div>`;
    for (const id in S.others) {
        const p = S.others[id];
        html += `<div class="player-item"><div class="player-dot" style="background:${p.color||'#666'}"></div><span class="player-name">${p.name||id}</span><span class="player-sc">${p.score||0}</span></div>`;
    }
    el.innerHTML = html;
    document.getElementById('playerCount').textContent = '在线: ' + (Object.keys(S.others).length + 1);
}

// ==================== 启动 ====================
document.addEventListener('DOMContentLoaded', () => setTimeout(init, 100));
</script>
</body>
</html>
