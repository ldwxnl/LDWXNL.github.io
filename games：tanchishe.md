---
layout: default
title: 🐍 贪吃蛇游戏
permalink: snake/
---

<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0,maximum-scale=5.0,user-scalable=yes">
<title>🐍 贪吃蛇</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;-webkit-user-select:none;user-select:none}
html,body{width:100%;min-height:100vh;font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:#1a1a1a;color:#e0e0e0;overflow-x:hidden}
.app{max-width:700px;margin:0 auto;padding:1rem;min-height:100vh;display:flex;flex-direction:column}
.header{text-align:center;padding:0.8rem 0}
.title{font-size:1.8rem;color:#4CAF50;margin-bottom:0.3rem}
.sub{color:#aaa;font-size:0.9rem}
.main{display:flex;flex-direction:column;gap:1rem;flex:1}
.mode-bar{display:flex;gap:0.5rem;background:#2a2a2a;border-radius:10px;padding:0.5rem}
.mode-btn{flex:1;padding:0.6rem;background:#333;border:2px solid transparent;border-radius:6px;color:#fff;font-weight:600;cursor:pointer;text-align:center;transition:all 0.2s}
.mode-btn.active{border-color:#4CAF50;background:rgba(76,175,80,0.15)}
.canvas-wrap{position:relative;width:100%;max-width:400px;aspect-ratio:1/1;border-radius:10px;overflow:hidden;box-shadow:0 8px 30px rgba(0,0,0,0.4);touch-action:none;margin:0 auto}
#c{width:100%;height:100%;display:block;background:#111}
.overlay{position:absolute;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.88);display:flex;flex-direction:column;justify-content:center;align-items:center;z-index:10;padding:1rem}
.ot{font-size:1.6rem;color:#4CAF50;margin-bottom:0.8rem;text-align:center}
.ox{font-size:1rem;color:#ccc;margin-bottom:1.2rem;text-align:center;line-height:1.5}
.btn{padding:0.7rem 1.3rem;border:none;border-radius:8px;font-size:0.95rem;font-weight:600;cursor:pointer;transition:all 0.2s}
.btn-g{background:linear-gradient(135deg,#4CAF50,#2E7D32);color:white}
.btn-g:hover{transform:translateY(-2px);box-shadow:0 4px 12px rgba(76,175,80,0.3)}
.btn-gr{background:#333;color:#fff;border:1px solid #444}
.btn-gr:hover{background:#3a3a3a;border-color:#4CAF50}
.sc{display:flex;justify-content:center;gap:1rem;background:#2a2a2a;border-radius:10px;padding:0.8rem 1.5rem;flex-wrap:wrap}
.sc-i{text-align:center;min-width:70px}
.sc-l{color:#aaa;font-size:0.75rem;margin-bottom:0.2rem}
.sc-v{color:#fff;font-size:1.5rem;font-weight:bold}
.cr{display:flex;gap:0.5rem;justify-content:center;flex-wrap:wrap}
.st{display:grid;grid-template-columns:repeat(3,1fr);gap:0.8rem;background:#2a2a2a;border-radius:10px;padding:0.8rem}
.st-i{text-align:center}
.st-l{color:#aaa;font-size:0.75rem;margin-bottom:0.2rem}
.st-v{color:#fff;font-size:1.1rem;font-weight:bold}
.stg{background:#2a2a2a;border-radius:10px;padding:1rem}
.stg h3{color:#4CAF50;font-size:1rem;margin-bottom:0.8rem;border-left:3px solid #4CAF50;padding-left:0.6rem}
.sr{display:flex;align-items:center;gap:0.5rem;margin-bottom:0.5rem;flex-wrap:wrap}
.sr label{font-size:0.85rem;color:#ccc;min-width:70px}
.sr input[type="range"]{flex:1;min-width:80px}
.sr select{flex:1;padding:0.4rem 0.6rem;background:#333;border:1px solid #444;border-radius:4px;color:#fff;font-size:0.85rem;outline:none}
.sr span{color:#4CAF50;font-weight:bold;min-width:30px}
.cg{display:grid;grid-template-columns:repeat(6,1fr);gap:0.4rem;margin-bottom:0.5rem}
.cb{width:100%;aspect-ratio:1;border-radius:6px;border:2px solid transparent;cursor:pointer;transition:all 0.2s}
.cb.active{border-color:#fff;transform:scale(1.1)}
.mc{display:none;margin-top:0.5rem}
.dp{display:grid;grid-template-areas:". u ." "l . r" ". d .";gap:10px;justify-content:center;margin:0 auto}
.db{width:56px;height:56px;border:none;border-radius:50%;background:#333;color:#fff;font-size:22px;cursor:pointer;touch-action:manipulation;display:flex;align-items:center;justify-content:center;box-shadow:0 3px 6px rgba(0,0,0,0.3)}
.db:active{background:#4CAF50;transform:scale(0.93)}
.db.u{grid-area:u}.db.d{grid-area:d}.db.l{grid-area:l}.db.r{grid-area:r}
.hp{background:#2a2a2a;border-radius:10px;padding:0.8rem;font-size:0.85rem;line-height:1.5}
@media(max-width:640px){
.app{padding:0.5rem}.title{font-size:1.4rem}.canvas-wrap{max-width:95vw}.sc-v{font-size:1.2rem}.mc{display:block}.cg{grid-template-columns:repeat(4,1fr)}
}
</style>
</head>
<body>
<div class="app">
<header class="header">
<h1 class="title">🐍 贪吃蛇</h1>
<p class="sub">单机 · AI</p>
</header>
<main class="main">
<div class="mode-bar">
<button class="mode-btn active" data-m="s">🎮 单人</button>
<button class="mode-btn" data-m="a">🤖 AI</button>
</div>
<div class="canvas-wrap">
<canvas id="c"></canvas>
<div id="ov" class="overlay">
<h2 id="ot" class="ot">🐍 贪吃蛇</h2>
<p id="ox" class="ox">选择模式开始</p>
<button id="sb" class="btn btn-g">开始</button>
</div>
</div>
<div class="sc">
<div class="sc-i"><div class="sc-l">分数</div><div id="ms" class="sc-v">0</div></div>
<div class="sc-i"><div class="sc-l">长度</div><div id="ml" class="sc-v">1</div></div>
<div class="sc-i"><div class="sc-l">最高</div><div id="hs" class="sc-v">0</div></div>
</div>
<div class="cr">
<button id="pb" class="btn btn-gr">暂停</button>
<button id="rb" class="btn btn-gr">重开</button>
</div>
<div class="st">
<div class="st-i"><div class="st-l">时间</div><div id="gt" class="st-v">00:00</div></div>
<div class="st-i"><div class="st-l">食物</div><div id="fc" class="st-v">0</div></div>
<div class="st-i"><div class="st-l">AI存活</div><div id="ac" class="st-v">0</div></div>
</div>
<div class="stg">
<h3>⚙ 设置</h3>
<div id="ss">
<div class="sr"><label>AI数量</label><input type="range" id="acnt" min="0" max="5" value="0"><span id="acv">0</span></div>
<div class="sr"><label>AI难度</label><select id="adf"><option value="0">简单</option><option value="1" selected>中等</option><option value="2">困难</option><option value="3">地狱</option></select></div>
<div class="sr"><label>速度</label><input type="range" id="spd" min="1" max="5" value="3"><span id="spv">普通</span></div>
</div>
<h3 style="margin-top:0.8rem">🎨 皮肤</h3>
<div class="cg" id="cg">
<div class="cb active" style="background:#4CAF50" data-c="#4CAF50"></div>
<div class="cb" style="background:#2196F3" data-c="#2196F3"></div>
<div class="cb" style="background:#FF5722" data-c="#FF5722"></div>
<div class="cb" style="background:#9C27B0" data-c="#9C27B0"></div>
<div class="cb" style="background:#FFEB3B" data-c="#FFEB3B"></div>
<div class="cb" style="background:#00BCD4" data-c="#00BCD4"></div>
<div class="cb" style="background:#E91E63" data-c="#E91E63"></div>
<div class="cb" style="background:#795548" data-c="#795548"></div>
<div class="cb" style="background:#607D8B" data-c="#607D8B"></div>
<div class="cb" style="background:#CDDC39" data-c="#CDDC39"></div>
<div class="cb" style="background:#FF9800" data-c="#FF9800"></div>
<div class="cb" style="background:#03A9F4" data-c="#03A9F4"></div>
</div>
<div class="sr"><label>自定义</label><input type="color" id="cc" value="#4CAF50"><input type="text" id="ch" value="#4CAF50" style="max-width:80px"><button class="btn btn-g" onclick="ac()" style="padding:0.4rem 0.8rem;font-size:0.8rem">应用</button></div>
</div>
<div class="mc">
<div class="dp">
<button class="db u">↑</button><button class="db d">↓</button><button class="db l">←</button><button class="db r">→</button>
</div>
</div>
<div class="hp">
<p><strong>操作：</strong> 方向键/WASD · 空格暂停</p>
<p><strong>单人：</strong> 经典模式，无AI</p>
<p><strong>AI：</strong> 与AI竞争，撞死AI得分，AI死后不复活</p>
</div>
</main>
</div>
<script>
const G=20,Ss=[250,190,145,115,90],Sn=['极慢','慢速','普通','快速','极快'],Fs=10,Ak=30,Ac=['#9C27B0','#2196F3','#FF9800','#E91E63','#00BCD4'];
const St={cv:null,cx:null,pl:{sk:[],dr:{dx:0,dy:0},sc:0,ln:1,co:'#4CAF50'},ai:[],fd:{x:0,y:0},hs:parseInt(localStorage.getItem('sh'))||0,pa:true,ov:true,mo:'s',lp:null,st:0,el:0,fc:0,tx:0,ty:0};
function it(){
St.cv=document.getElementById('c');St.cx=St.cv.getContext('2d');rs();
document.getElementById('hs').textContent=St.hs;
document.addEventListener('keydown',k);
document.getElementById('sb').onclick=st;document.getElementById('pb').onclick=pa;document.getElementById('rb').onclick=re;
document.querySelectorAll('.mode-btn').forEach(b=>{b.onclick=function(){document.querySelectorAll('.mode-btn').forEach(x=>x.classList.remove('active'));this.classList.add('active');St.mo=this.dataset.m;re()}});
document.getElementById('acnt').oninput=function(){document.getElementById('acv').textContent=this.value};
document.getElementById('spd').oninput=function(){document.getElementById('spv').textContent=Sn[this.value-1]};
document.querySelectorAll('.cb').forEach(b=>{b.onclick=function(){document.querySelectorAll('.cb').forEach(x=>x.classList.remove('active'));this.classList.add('active');St.pl.co=this.dataset.c;document.getElementById('cc').value=St.pl.co;document.getElementById('ch').value=St.pl.co;dw()}});
document.getElementById('cc').oninput=function(){document.getElementById('ch').value=this.value};
document.getElementById('ch').oninput=function(){if(/^#[0-9A-Fa-f]{6}$/.test(this.value))document.getElementById('cc').value=this.value};
document.querySelectorAll('.db').forEach(b=>{b.addEventListener('touchstart',e=>{e.preventDefault();di(b.textContent)});b.addEventListener('mousedown',()=>di(b.textContent))});
St.cv.addEventListener('touchstart',e=>{if(e.touches.length!==1)return;St.tx=e.touches[0].clientX;St.ty=e.touches[0].clientY},{passive:true});
St.cv.addEventListener('touchend',e=>{if(!St.tx||St.pa)return;const dx=e.changedTouches[0].clientX-St.tx,dy=e.changedTouches[0].clientY-St.ty;if(Math.abs(dx)<15&&Math.abs(dy)<15)return;if(Math.abs(dx)>Math.abs(dy))di(dx>0?'→':'←');else di(dy>0?'↓':'↑');St.tx=0},{passive:true});
window.addEventListener('resize',()=>{rs();dw()});
re();dw()
}
function rs(){const c=St.cv.parentElement,s=Math.min(c.clientWidth,c.clientHeight);St.cv.width=s;St.cv.height=s}
function di(d){if(St.pa&&!St.ov)return;const dd=St.pl.dr;switch(d){case'↑':case'ArrowUp':if(dd.dy!==1)St.pl.dr={dx:0,dy:-1};break;case'↓':case'ArrowDown':if(dd.dy!==-1)St.pl.dr={dx:0,dy:1};break;case'←':case'ArrowLeft':if(dd.dx!==1)St.pl.dr={dx:-1,dy:0};break;case'→':case'ArrowRight':if(dd.dx!==-1)St.pl.dr={dx:1,dy:0};break}}
function k(e){switch(e.key){case'ArrowUp':case'w':case'W':di('↑');break;case'ArrowDown':case's':case'S':di('↓');break;case'ArrowLeft':case'a':case'A':di('←');break;case'ArrowRight':case'd':case'D':di('→');break;case' ':e.preventDefault();pa();break}}
function st(){if(St.ov){re();St.ov=false}if(St.pa){St.pa=false;St.st=Date.now()-St.el;const sp=Ss[parseInt(document.getElementById('spd').value)-1];St.lp=setInterval(up,sp);document.getElementById('ov').style.display='none';document.getElementById('sb').textContent='游戏中...';if(St.mo==='a'){const cnt=parseInt(document.getElementById('acnt').value);if(cnt>0)ia(cnt)}St.cv.focus()}}
function pa(){if(St.ov)return;St.pa=!St.pa;if(St.pa){clearInterval(St.lp);so('暂停','点击继续');document.getElementById('sb').textContent='继续'}else{const sp=Ss[parseInt(document.getElementById('spd').value)-1];St.lp=setInterval(up,sp);document.getElementById('ov').style.display='none';document.getElementById('sb').textContent='游戏中...'}}
function re(){clearInterval(St.lp);St.pa=true;St.ov=true;St.ai=[];const sz=Math.floor(St.cv.width/G),cx=Math.floor(sz/2);St.pl.sk=[{x:cx,y:cx}];St.pl.dr={dx:0,dy:0};St.pl.sc=0;St.pl.ln=1;St.fc=0;St.el=0;gf();ud();dw();so('🐍 贪吃蛇',St.mo==='a'?'AI对战模式':'单人模式');document.getElementById('sb').textContent='开始';document.getElementById('gt').textContent='00:00';us()}
function ia(cnt){St.ai=[];const sz=Math.floor(St.cv.width/G);for(let i=0;i<cnt;i++){let x,y;do{x=Math.floor(Math.random()*(sz-4))+2;y=Math.floor(Math.random()*(sz-4))+2}while(oc(x,y));St.ai.push({sk:[{x,y}],dr:{dx:1,dy:0},co:Ac[i%Ac.length],lm:Date.now(),dl:[400,230,150,90][parseInt(document.getElementById('adf').value)]})}us()}
function oc(x,y){for(const s of St.pl.sk)if(s.x===x&&s.y===y)return true;for(const a of St.ai)for(const s of a.sk)if(s.x===x&&s.y===y)return true;return false}
function ua(){const n=Date.now();for(let i=St.ai.length-1;i>=0;i--){const a=St.ai[i];if(n-a.lm<a.dl)continue;const h=a.sk[0],ds=[{dx:1,dy:0},{dx:-1,dy:0},{dx:0,dy:1},{dx:0,dy:-1}],vl=ds.filter(d=>!(d.dx===-a.dr.dx&&d.dy===-a.dr.dy));let ch;const df=parseInt(document.getElementById('adf').value);if(df>=3)ch=bd(h,vl,St.fd);else if(df>=2)ch=Math.random()<0.4?bd(h,vl,St.fd):vl[Math.floor(Math.random()*vl.length)];else if(df>=1)ch=Math.random()<0.2?bd(h,vl,St.fd):vl[Math.floor(Math.random()*vl.length)];else ch=vl[Math.floor(Math.random()*vl.length)];if(ch)a.dr=ch;const nh={x:h.x+a.dr.dx,y:h.y+a.dr.dy};a.sk.unshift(nh);if(nh.x===St.fd.x&&nh.y===St.fd.y)gf();else a.sk.pop();if(ac2(a)){St.pl.sc+=Ak;St.ai.splice(i,1);us()}a.lm=n}}
function bd(fr,ds,tg){let be=null,bs=-Infinity;for(const d of ds){const nx=fr.x+d.dx,ny=fr.y+d.dy,sc=-(Math.abs(tg.x-nx)+Math.abs(tg.y-ny));if(sc>bs){bs=sc;be=d}}return be}
function ac2(a){const h=a.sk[0],sz=Math.floor(St.cv.width/G);if(h.x<0||h.x>=sz||h.y<0||h.y>=sz)return true;for(let i=1;i<a.sk.length;i++)if(h.x===a.sk[i].x&&h.y===a.sk[i].y)return true;for(const s of St.pl.sk)if(h.x===s.x&&h.y===s.y)return true;for(const o of St.ai)if(o!==a)for(const s of o.sk)if(h.x===s.x&&h.y===s.y)return true;return false}
function up(){if(St.pa||St.ov)return;St.el=Date.now()-St.st;document.getElementById('gt').textContent=fm(St.el);const h={x:St.pl.sk[0].x+St.pl.dr.dx,y:St.pl.sk[0].y+St.pl.dr.dy};St.pl.sk.unshift(h);if(h.x===St.fd.x&&h.y===St.fd.y){St.pl.sc+=Fs;St.pl.ln=St.pl.sk.length;St.fc++;gf()}else St.pl.sk.pop();if(St.mo==='a')ua();if(cc()){go();return}ud();us();dw()}
function gf(){const sz=Math.floor(St.cv.width/G);let f;do{f={x:Math.floor(Math.random()*sz),y:Math.floor(Math.random()*sz)}}while(oc(f.x,f.y));St.fd=f}
function cc(){const h=St.pl.sk[0],sz=Math.floor(St.cv.width/G);if(h.x<0||h.x>=sz||h.y<0||h.y>=sz)return true;for(let i=1;i<St.pl.sk.length;i++)if(h.x===St.pl.sk[i].x&&h.y===St.pl.sk[i].y)return true;for(const a of St.ai)for(const s of a.sk)if(h.x===s.x&&h.y===s.y)return true;return false}
function go(){clearInterval(St.lp);St.ov=true;St.pa=true;if(St.pl.sc>St.hs){St.hs=St.pl.sc;localStorage.setItem('sh',St.hs);document.getElementById('hs').textContent=St.hs}so('游戏结束','得分: '+St.pl.sc+'<br>长度: '+St.pl.ln);document.getElementById('sb').textContent='重新开始'}
function dw(){const ctx=St.cx,cv=St.cv,cl=G;ctx.fillStyle='#111';ctx.fillRect(0,0,cv.width,cv.height);ctx.strokeStyle='#1a1a1a';ctx.lineWidth=0.5;for(let x=0;x<cv.width;x+=cl){ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,cv.height);ctx.stroke()}for(let y=0;y<cv.height;y+=cl){ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(cv.width,y);ctx.stroke()}ctx.fillStyle='#FF5252';ctx.shadowColor='#FF525280';ctx.shadowBlur=8;ctx.beginPath();ctx.arc(St.fd.x*cl+cl/2,St.fd.y*cl+cl/2,cl/2-2,0,Math.PI*2);ctx.fill();ctx.shadowBlur=0;for(const a of St.ai)dwSn(a.sk,a.co,false);dwSn(St.pl.sk,St.pl.co,true)}
function dwSn(sk,co,me){const ctx=St.cx,cl=G;sk.forEach((sg,i)=>{if(i===0){ctx.fillStyle=me?co:'#FFF';ctx.fillRect(sg.x*cl+1,sg.y*cl+1,cl-2,cl-2);ctx.fillStyle=me?'#FFF':co;ctx.fillRect(sg.x*cl+4,sg.y*cl+4,cl-8,cl-8)}else{ctx.fillStyle=co;ctx.fillRect(sg.x*cl+1,sg.y*cl+1,cl-2,cl-2)}})}
function ud(){document.getElementById('ms').textContent=St.pl.sc;document.getElementById('ml').textContent=St.pl.ln;document.getElementById('fc').textContent=St.fc}
function us(){document.getElementById('ac').textContent=St.ai.length}
function so(t,x){document.getElementById('ot').innerHTML=t;document.getElementById('ox').innerHTML=x;document.getElementById('ov').style.display='flex'}
function fm(ms){const s=Math.floor(ms/1000);return String(Math.floor(s/60)).padStart(2,'0')+':'+String(s%60).padStart(2,'0')}
function ac(){const h=document.getElementById('ch').value;if(/^#[0-9A-Fa-f]{6}$/.test(h)){St.pl.co=h;document.querySelectorAll('.cb').forEach(c=>c.classList.remove('active'));dw()}}
document.addEventListener('DOMContentLoaded',()=>setTimeout(it,100));
</script>
</body>
</html>
