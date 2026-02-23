---
layout: home
title: 素以为绚兮，绘事后素
body_class: home
---

---
<figure style="text-align: center; margin: 20px 0;">
    <img src="/assets/img/lantingxu.jpg" alt="兰亭集序" style="max-width: 100%; height: auto; border-radius: 2px;">
    <figcaption style="
        font-family: 'KaiTi', 'STKaiti', '楷体', serif; 
        font-size: 0.85rem; 
        color: #555; 
        margin-top: 8px;
    ">
        《兰亭序》卷 [东晋] 王羲之书（传[唐] 褚遂良摹本）
    </figcaption>
</figure>

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
- [日记](./diary)

---

<br>

### 花粉游弋（平面布朗运动）

<div style="text-align: center; margin: 20px 0;">
    <button id="bm-generate-btn" style="
        padding: 8px 16px;
        background-color: #333333;
        color: #ffffff;
        border: 1px solid #000000;
        border-radius: 2px;
        cursor: pointer;
        font-family: inherit;
        font-size: 0.9rem;
        transition: all 0.3s ease;
    ">
        游弋
    </button>
</div>

<div style="display: flex; justify-content: center; position: relative;">
    <canvas id="bm-canvas" width="640" height="360" style="
        border: 1px solid #cccccc;
        background-color: #ffffff;
        max-width: 100%;
        box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    "></canvas>
</div>
<p style="text-align: center; color: #888888; font-size: 0.8rem; margin-top: 5px; font-family: monospace;">
    游弋时间: <span id="bm-progress">0.0</span>s / 10.0s
</p>

<script>
(function() {
    const canvas = document.getElementById('bm-canvas');
    if (!canvas) return; // 防止未加载时报错
    
    const ctx = canvas.getContext('2d');
    const btn = document.getElementById('bm-generate-btn');
    const progressText = document.getElementById('bm-progress');

    // === 配置参数 ===
    const TOTAL_STEPS = 6000;    // 总步数
    const DURATION = 10000;      // 动画时长：10000毫秒
    const STEP_SIZE = 3;         // 步长

    // 状态变量
    let animationId = null;
    let currentX, currentY;
    let startTime = 0;

    // 1. 初始化背景（绘制浅灰色网格）
    function initCanvas() {
        const w = canvas.width;
        const h = canvas.height;
        
        // 清除并填充白色背景
        ctx.fillStyle = '#ffffff';
        ctx.fillRect(0, 0, w, h);
        
        // 绘制网格
        ctx.lineWidth = 1;
        ctx.strokeStyle = '#f2f2f2'; // 极浅的灰色网格
        ctx.beginPath();
        // 竖线
        for(let i=0; i<=w; i+=40) { 
            ctx.moveTo(i, 0); 
            ctx.lineTo(i, h); 
        }
        // 横线
        for(let i=0; i<=h; i+=40) { 
            ctx.moveTo(0, i); 
            ctx.lineTo(w, i); 
        }
        ctx.stroke();
    }

    // 2. 动画核心逻辑
    function animate(currentTime) {
        if (!startTime) startTime = currentTime;
        const elapsed = currentTime - startTime;
        
        // 计算进度 (0.0 到 1.0)
        let progress = Math.min(elapsed / DURATION, 1.0); 
        
        // 更新时间显示 (保留1位小数)
        if(progressText) {
            progressText.innerText = (elapsed / 1000).toFixed(1);
        }

        // 当前应该画到的步数
        const targetSteps = Math.floor(progress * TOTAL_STEPS);
        
        // 设置路径样式：深灰色，强调素雅
        ctx.lineWidth = 1.2;
        ctx.strokeStyle = '#222222'; // 深灰色路径，接近黑
        ctx.beginPath();
        ctx.moveTo(currentX, currentY);

        // 补齐自上一帧以来的步数
        // 这里的逻辑稍微调整：我们记录上一次画到的 stepsDrawn
        // 但为了简单，我们每帧都接续上一次的坐标画
        
        // 每一帧画一定数量的步子来追赶进度
        // 为了保持连贯性，这里使用一个临时循环
        let stepsToDrawNow = targetSteps - stepsDrawn;
        
        for (let i = 0; i < stepsToDrawNow; i++) {
            const dx = (Math.random() - 0.5) * STEP_SIZE * 2;
            const dy = (Math.random() - 0.5) * STEP_SIZE * 2;
            
            currentX += dx;
            currentY += dy;
            
            ctx.lineTo(currentX, currentY);
        }
        ctx.stroke();
        
        // 更新全局计数器
        stepsDrawn = targetSteps;

        // 检查是否结束
        if (progress < 1.0) {
            animationId = requestAnimationFrame(animate);
        } else {
            // 结束时画纯黑点
            ctx.beginPath();
            ctx.arc(currentX, currentY, 3, 0, 2 * Math.PI);
            ctx.fillStyle = '#000000'; // 纯黑终点
            ctx.fill();
            if(progressText) progressText.innerText = "10.0";
            btn.disabled = false;
            btn.style.opacity = '1';
            btn.innerText = "游弋";
        }
    }

    // 全局变量用于记录已绘制步数
    let stepsDrawn = 0;

    function startAnimation() {
        if (animationId) cancelAnimationFrame(animationId);
        
        initCanvas();
        
        // 重置状态
        currentX = canvas.width / 2;
        currentY = canvas.height / 2;
        stepsDrawn = 0;
        startTime = 0; // 重置开始时间，在第一帧时赋值
        
        // 按钮交互反馈
        btn.disabled = true;
        btn.style.opacity = '0.7';
        btn.innerText = "游弋";

        animationId = requestAnimationFrame(animate);
    }

    // 初始化
    initCanvas();

    // 绑定事件
    if(btn) {
        btn.onclick = startAnimation;
        // 鼠标悬停变黑
        btn.onmouseover = function() { if(!this.disabled) this.style.backgroundColor = '#000000'; };
        btn.onmouseout = function() { if(!this.disabled) this.style.backgroundColor = '#333333'; };
    }
})();
</script>
