---
layout: home
title: 素以为绚兮
body_class: home
---

---
![兰亭集序](/assets/img/lantingxu.jpg)

---
<br>
我主要对

- 概率论和随机分析
- （泛函）分析和（偏微分）方程
- （微分和代数）几何

等方面感兴趣。


---
<br>

### 概览

- [笔记](./notes)
- [杂项](./others)

<br>
<hr>

### 随机游走 / 布朗运动演示

<div style="text-align: center; margin: 20px 0;">
    <button id="bm-generate-btn" style="
        padding: 8px 16px;
        background-color: #2c3e50;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-family: inherit;
        font-size: 0.9rem;
        transition: opacity 0.2s;
    ">
        生成路径 $W_t$
    </button>
</div>

<div style="display: flex; justify-content: center;">
    <canvas id="bm-canvas" width="640" height="360" style="
        border: 1px solid #e1e4e8;
        background-color: #fafafa;
        max-width: 100%;
        box-shadow: 0 2px 4px rgba(0,0,0,0.05);
    "></canvas>
</div>

<script>
(function() {
    const canvas = document.getElementById('bm-canvas');
    const ctx = canvas.getContext('2d');
    const btn = document.getElementById('bm-generate-btn');

    // 参数配置
    const STEPS = 2000;    // 步数
    const STEP_SIZE = 4;   // 步长尺度

    function drawBrownianPath() {
        const width = canvas.width;
        const height = canvas.height;
        
        // 清除画布
        ctx.clearRect(0, 0, width, height);
        
        // 绘制网格背景（可选，为了更有数学感）
        ctx.strokeStyle = '#f0f0f0';
        ctx.lineWidth = 1;
        ctx.beginPath();
        for(let i=0; i<width; i+=40) { ctx.moveTo(i,0); ctx.lineTo(i,height); }
        for(let i=0; i<height; i+=40) { ctx.moveTo(0,i); ctx.lineTo(width,i); }
        ctx.stroke();

        // 开始绘制路径
        ctx.beginPath();
        ctx.strokeStyle = '#0366d6'; // GitHub Blue
        ctx.lineWidth = 1.2;
        
        // 起点设为中心
        let x = width / 2;
        let y = height / 2;
        ctx.moveTo(x, y);

        // 模拟二维布朗运动 (Wiener Process近似)
        // 这里的增量服从均匀分布，根据中心极限定理，步数多了近似正态
        for (let i = 0; i < STEPS; i++) {
            // 简单的随机游走
            x += (Math.random() - 0.5) * STEP_SIZE * 2;
            y += (Math.random() - 0.5) * STEP_SIZE * 2;
            
            ctx.lineTo(x, y);
        }
        ctx.stroke();

        // 标记终点
        ctx.beginPath();
        ctx.arc(x, y, 3, 0, 2 * Math.PI);
        ctx.fillStyle = '#d73a49'; // Red
        ctx.fill();
    }

    // 绑定事件
    if(btn && canvas) {
        btn.addEventListener('click', drawBrownianPath);
        // 还有一种更加现代的写法：btn.onclick = drawBrownianPath;
        
        // 鼠标悬停效果
        btn.onmouseover = function() { this.style.opacity = 0.8; };
        btn.onmouseout = function() { this.style.opacity = 1; };
    }
})();
</script>
