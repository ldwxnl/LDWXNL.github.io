---
layout: default
title: 首页
---
<!-- 1. 顶部 Header 区域：使用 Flexbox 居中，添加渐变背景 -->
<div style="background: linear-gradient(135deg, #2c3e50 0%, #3498db 100%); padding: 4rem 2rem; border-radius: 0 0 20px 20px; color: white; text-align: center; box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
  <!-- 头像：现在它会乖乖待在标题旁边了 -->
  <img src="/assets/images/avatar.jpg"
       alt="我的头像"
       style="width: 100px; height: 100px; border-radius: 50%; object-fit: cover; border: 4px solid white; box-shadow: 0 4px 10px rgba(0,0,0,0.2); margin-bottom: 1rem; display: inline-block; vertical-align: middle;">
  
  <div style="display: inline-block; vertical-align: middle; margin-left: 1rem; text-align: left;">
    <h1 style="margin: 0; font-size: 2.5rem; font-weight: 600;">首页</h1>
    <p style="margin: 0.5rem 0 0; font-size: 1.2rem; opacity: 0.9;">我的个人网站和博客
  </div>
</div>

<!-- 2. 主体内容区域：限制最大宽度，居中显示 -->
<div style="max-width: 900px; margin: 2rem auto; padding: 0 1.5rem;">

  <!-- 关于我卡片 -->
  <div style="background: #ffffff; padding: 2.5rem; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); margin-bottom: 2rem;">
    <h2 style="color: #333; border-bottom: 2px solid #4caf50; padding-bottom: 0.5rem; margin-top: 0;">关于我</h2>
    <p style="line-height: 1.8; color: #555; font-size: 1.1rem;">
      你好！我是 LDWXNL，热爱技术、分享与交流。这个网站是我记录学习、项目和生活的空间。你问我是谁，别问，问就是hrsi
    
    <div style="margin-top: 1.5rem; padding-top: 1rem; border-top: 1px solid #eee; font-size: 0.95rem; color: #777;">
      <span style="margin-right: 1rem;">📧 联系我: to@hrn.cc.cd</span>
      <span>🔗 <a href="https://github.com/ldwxnl" style="color: #0366d6; text-decoration: none;">GitHub</a></span>
      
      <!-- 探索更多按钮组 -->
      <div style="text-align: center; margin-top: 2rem;">
        <h4 style="color: #666; margin-bottom: 1.5rem;">🎯 探索更多</h4>
        <a href="/posts" style="display: inline-block; padding: 0.8rem 2rem; margin: 0 0.5rem; color: #4caf50; border: 2px solid #4caf50; border-radius: 8px; text-decoration: none; font-weight: bold; transition: all 0.3s;">
          📖 查看我的博客
        </a>
        <a href="/games" style="display: inline-block; padding: 0.8rem 2rem; margin: 0 0.5rem; color: #4caf50; border: 2px solid #4caf50; border-radius: 8px; text-decoration: none; font-weight: bold; transition: all 0.3s;">
          🎮 游戏中心
        </a>
      </div>
    </div>
  </div>

  <!-- 玩家留言板 -->
  <div style="background: #ffffff; padding: 2.5rem; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.05); margin-bottom: 2rem;">
    <h2 style="color: #333; text-align: center; margin-top: 0;">💬 玩家留言板</h2>
    <p style="color: #666; text-align: center; margin-bottom: 1.5rem;">
      欢迎大家在下方留言交流游戏心得、反馈问题或分享进服体验！
    
    <!-- Giscus 容器 -->
    <div class="giscus"></div>
  </div>

</div>

<!-- Giscus 脚本 (保持原样) -->
<script src="https://giscus.app/client.js"
        data-repo="LDWXNL/LDWXNL.github.io"
        data-repo-id="R_kgDOR96W3Q"
        data-category="Announcements"
        data-category-id="DIC_kwDOR96W3c4C8t89"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="top"
        data-theme="preferred_color_scheme"
        data-lang="zh-CN"
        crossorigin="anonymous"
        async>
</script>

<!-- 3. HRSI 聊天组件：优化悬浮样式 -->
<style>
  /* 全局样式微调 */
  body { background-color: #f4f7f6; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
  
  /* 聊天框样式优化 */
  #hrsi-box {
    position: fixed;
    bottom: 30px;
    right: 30px;
    width: 360px;
    height: 500px;
    background: #1e1e2e; /* 更酷的深色背景 */
    border-radius: 16px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.4);
    display: none;
    flex-direction: column;
    z-index: 9999;
    overflow: hidden;
    border: 1px solid #313244;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    transition: transform 0.3s ease;
  }
  
  #hrsi-box:hover {
    transform: translateY(-5px);
  }

  .hrsi-header {
    background: linear-gradient(90deg, #4caf50, #81c784);
    padding: 12px 16px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    font-weight: bold;
    font-size: 16px;
  }

  #hrsi-msgs {
    flex: 1;
    overflow-y: auto;
    padding: 16px;
    font-size: 14px;
    line-height: 1.6;
    background: #1e1e2e;
  }
  
  /* 自定义滚动条 */
  #hrsi-msgs::-webkit-scrollbar { width: 6px; }
  #hrsi-msgs::-webkit-scrollbar-thumb { background: #4caf50; border-radius: 3px; }

  .hrsi-input-area {
    display: flex;
    border-top: 1px solid #313244;
    padding: 12px;
    background: #181825;
  }

  #hrsi-input {
    flex: 1;
    padding: 10px 12px;
    border-radius: 20px;
    border: none;
    background: #313244;
    color: #cdd6f4;
    outline: none;
    font-size: 14px;
  }
  
  #hrsi-input::placeholder { color: #6c7086; }

  .send-btn {
    margin-left: 8px;
    padding: 10px 20px;
    background: #4caf50;
    border: none;
    border-radius: 20px;
    color: white;
    cursor: pointer;
    font-weight: bold;
    transition: background 0.2s;
  }
  
  .send-btn:hover { background: #66bb6a; }

  /* 消息气泡样式 */
  .msg-user { text-align: right; margin-bottom: 8px; }
  .msg-bot { text-align: left; margin-bottom: 8px; }
  
  .msg-user span {
    background: #4caf50;
    color: white;
    padding: 8px 12px;
    border-radius: 12px 12px 0 12px;
    display: inline-block;
    max-width: 80%;
    word-wrap: break-word;
  }
  
  .msg-bot span {
    background: #313244;
    color: #cdd6f4;
    padding: 8px 12px;
    border-radius: 12px 12px 12px 0;
    display: inline-block;
    max-width: 80%;
    word-wrap: break-word;
  }
</style>

<!-- HTML 结构保持不变，只是加了 class 方便 CSS 控制 -->
<button onclick="toggleHRSI()" style="position:fixed;bottom:30px;right:30px;background:#4caf50;color:#fff;border:none;border-radius:50%;width:56px;height:56px;font-size:24px;cursor:pointer;z-index:9998;box-shadow:0 4px 15px rgba(0,0,0,0.3);display:flex;align-items:center;justify-content:center;transition: transform 0.2s; hover:transform:scale(1.1);">
  💬
</button>

<div id="hrsi-box">
  <div class="hrsi-header">
    <span>🔥 HRSI AI 助手</span>
    <button onclick="toggleHRSI()" style="background:none;border:none;color:#fff;font-size:20px;cursor:pointer;padding:0;line-height:1;">✕</button>
  </div>
  <div id="hrsi-msgs"></div>
  <div class="hrsi-input-area">
    <input id="hrsi-input" placeholder="问 HRSI 点什么…" onkeypress="if(event.key==='Enter')sendHRSI()">
    <button class="send-btn" onclick="sendHRSI()">发送</button>
  </div>
</div>

<script>
function toggleHRSI() {
  const box = document.getElementById('hrsi-box')
  // 使用 flex 布局让内部元素垂直排列
  box.style.display = box.style.display === 'flex' ? 'none' : 'flex'
  box.style.flexDirection = 'column'
}

async function sendHRSI() {
  const input = document.getElementById('hrsi-input')
  const msg = input.value.trim()
  if (!msg) return
  
  const msgs = document.getElementById('hrsi-msgs')
  
  // 显示用户消息
  msgs.innerHTML += `<div class="msg-user"><span>${msg}</span></div>`
  input.value = ''
  
  try {
    const res = await fetch('https://hrsi-api.hrsi.cc.cd/api/generate', {
      method: 'POST',
      headers: {'Content-Type': 'application/json'},
      body: JSON.stringify({
        model: 'hrsi-model',
        prompt: `用户问："${msg}"\n\n用 HRSI 的身份（12岁技术建造者，中二自信，好燃 So Intense！）简短回答：`,
        stream: false
      })
    })
    const data = await res.json()
    
    // 显示机器人回复
    if(data.response) {
        msgs.innerHTML += `<div class="msg-bot"><span>${data.response.trim()}</span></div>`
    } else {
        msgs.innerHTML += `<div class="msg-bot"><span>哎呀，出错了：${data.error || '未知错误'}</span></div>`
    }
  } catch(e) {
    msgs.innerHTML += `<div class="msg-bot"><span>HRSI 挖矿去了，稍后再试！</span></div>`
  }
  
  msgs.scrollTop = msgs.scrollHeight // 自动滚动到底部
}
</script>
