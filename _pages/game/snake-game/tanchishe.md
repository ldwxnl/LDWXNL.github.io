<!DOCTYPE html>
<html>
<head>
  <title>贪吃蛇测试</title>
  <style>
    body { margin: 0; padding: 20px; text-align: center; }
    canvas { border: 2px solid black; display: block; margin: 20px auto; }
    button { padding: 10px 20px; margin: 10px; font-size: 16px; }
  </style>
</head>
<body>
  <h1>贪吃蛇基础测试</h1>
  
  <canvas id="testCanvas" width="300" height="300"></canvas>
  
  <div>
    <button id="testBtn1">测试按钮1</button>
    <button id="testBtn2">测试按钮2</button>
  </div>
  
  <div id="output" style="margin-top: 20px; padding: 10px; background: #f0f0f0;"></div>

  <script>
    console.log("=== 测试开始 ===");
    
    // 获取元素
    const canvas = document.getElementById('testCanvas');
    const ctx = canvas.getContext('2d');
    const btn1 = document.getElementById('testBtn1');
    const btn2 = document.getElementById('testBtn2');
    const output = document.getElementById('output');
    
    console.log("找到的元素:", { canvas, btn1, btn2, output });
    
    // 检查元素是否存在
    if (!canvas) console.error("错误: 找不到Canvas");
    if (!btn1) console.error("错误: 找不到按钮1");
    if (!btn2) console.error("错误: 找不到按钮2");
    
    // 设置Canvas焦点
    canvas.setAttribute('tabindex', '0');
    canvas.focus();
    console.log("Canvas焦点状态:", document.activeElement === canvas);
    
    // 按钮1点击事件
    btn1.addEventListener('click', function(e) {
      console.log("✅ 按钮1被点击!", e);
      output.innerHTML += '<p>按钮1被点击 - ' + new Date().toLocaleTimeString() + '</p>';
      
      // 在Canvas上画一个矩形
      ctx.fillStyle = 'red';
      ctx.fillRect(50, 50, 100, 100);
    });
    
    // 按钮2点击事件
    btn2.addEventListener('click', function(e) {
      console.log("✅ 按钮2被点击!", e);
      output.innerHTML += '<p>按钮2被点击 - ' + new Date().toLocaleTimeString() + '</p>';
      
      // 清除Canvas
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    });
    
    // 键盘事件
    document.addEventListener('keydown', function(e) {
      console.log("⌨️ 键盘按下:", e.key, "code:", e.code);
      output.innerHTML += '<p>按键: ' + e.key + ' - ' + new Date().toLocaleTimeString() + '</p>';
      
      // 在Canvas上根据按键画图
      switch(e.key) {
        case 'ArrowUp':
          ctx.fillStyle = 'blue';
          ctx.fillRect(100, 50, 50, 50);
          break;
        case 'ArrowDown':
          ctx.fillStyle = 'green';
          ctx.fillRect(100, 200, 50, 50);
          break;
        case 'ArrowLeft':
          ctx.fillStyle = 'orange';
          ctx.fillRect(50, 125, 50, 50);
          break;
        case 'ArrowRight':
          ctx.fillStyle = 'purple';
          ctx.fillRect(200, 125, 50, 50);
          break;
      }
    });
    
    // Canvas点击事件
    canvas.addEventListener('click', function() {
      console.log("🎯 Canvas被点击");
      canvas.focus();
    });
    
    console.log("=== 测试设置完成 ===");
  </script>
</body>
</html>
