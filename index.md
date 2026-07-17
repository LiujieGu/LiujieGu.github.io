---
layout: default
---

# Welcome

Hi, I'm **Gu Liujie**. This is my personal space on the web.

## Explore

- 📋 **[About](/about)** — who I am, my background and how to reach me
- 📝 **[Blog](/blog)** — thoughts on quant research, computer vision, and more
- ✨ **[Something Interesting](/something-interesting)** — random stuff I find fun

Use the menu above to navigate. Thanks for stopping by!

<p id="dedicate" style="position:fixed;left:14px;bottom:12px;margin:0;color:#8b949e;font-size:0.9rem;cursor:pointer;user-select:none;z-index:20;">Gu Liujie ♡</p>
<div id="dedicate-msg" style="position:fixed;left:14px;bottom:38px;color:#f778ba;font-size:0.9rem;opacity:0;transition:opacity .4s;z-index:20;pointer-events:none;">Dedicated to Z.J. ♡</div>
<canvas id="hearts" style="position:fixed;inset:0;width:100%;height:100%;pointer-events:none;z-index:15;"></canvas>

<script>
(function () {
  const btn = document.getElementById('dedicate');
  const msg = document.getElementById('dedicate-msg');
  const cv = document.getElementById('hearts');
  const ctx = cv.getContext('2d');
  let W, H;
  const DPR = Math.min(window.devicePixelRatio || 1, 2);
  function size() {
    W = cv.width = Math.round(window.innerWidth * DPR);
    H = cv.height = Math.round(window.innerHeight * DPR);
  }
  size();
  window.addEventListener('resize', size);

  const hearts = [];
  function burst() {
    const rect = btn.getBoundingClientRect();
    const ox = (rect.left + rect.width / 2) * DPR;
    const oy = (rect.top) * DPR;
    for (let i = 0; i < 24; i++) {
      const a = Math.random() * Math.PI * 2;
      const sp = (1 + Math.random() * 3) * DPR;
      hearts.push({
        x: ox, y: oy,
        vx: Math.cos(a) * sp, vy: Math.sin(a) * sp - 2 * DPR,
        r: (4 + Math.random() * 5) * DPR,
        life: 1, rot: Math.random() * Math.PI
      });
    }
  }
  function heart(x, y, r, col) {
    ctx.save();
    ctx.translate(x, y);
    ctx.scale(r / 16, r / 16);
    ctx.beginPath();
    ctx.moveTo(0, 4);
    ctx.bezierCurveTo(-8, -4, -16, 4, 0, 14);
    ctx.bezierCurveTo(16, 4, 8, -4, 0, 4);
    ctx.fillStyle = col;
    ctx.fill();
    ctx.restore();
  }
  function loop() {
    ctx.clearRect(0, 0, W, H);
    for (let i = hearts.length - 1; i >= 0; i--) {
      const h = hearts[i];
      h.vy += 0.06 * DPR;
      h.x += h.vx; h.y += h.vy;
      h.life -= 0.015;
      if (h.life <= 0) { hearts.splice(i, 1); continue; }
      ctx.globalAlpha = Math.max(0, h.life);
      heart(h.x, h.y, h.r, '#f778ba');
    }
    ctx.globalAlpha = 1;
    requestAnimationFrame(loop);
  }
  loop();

  btn.addEventListener('click', function () {
    burst();
    msg.style.opacity = '1';
    clearTimeout(btn._t);
    btn._t = setTimeout(() => { msg.style.opacity = '0'; }, 3000);
  });
})();
</script>
