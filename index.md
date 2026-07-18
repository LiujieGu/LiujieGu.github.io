---
layout: default
---

<div class="hero">
  <img class="hero-avatar" src="/assets/profile.png" alt="Gu Liujie">
  <div class="hero-text">
    <h1>Gu Liujie</h1>
    <p class="hero-sub">Quantitative researcher · CV &amp; AI · building things for fun</p>
  </div>
</div>

## Explore

- 📋 **[About](/about/)** — who I am, my background and how to reach me
- 📝 **[Blog](/blog/)** — thoughts on quant research, computer vision, and more
- 🚀 **[Projects](/projects/)** — open-source projects I've built or contributed to
- ✨ **[Something Interesting](/something-interesting/)** — random stuff I find fun

Use the menu above to navigate. Thanks for stopping by!

<style>
  .hero { display: flex; align-items: center; gap: 1.6rem; margin: .5rem 0 2rem; }
  .hero-avatar {
    width: 116px; height: 116px; border-radius: 50%;
    object-fit: cover;
    padding: 4px;
    background: linear-gradient(135deg, #58a6ff, #d2a8ff, #f778ba);
    box-shadow: 0 6px 24px rgba(88,166,255,.25);
    transition: transform .25s ease, box-shadow .25s ease;
  }
  .hero-avatar:hover { transform: scale(1.04); box-shadow: 0 10px 32px rgba(215,168,255,.4); }
  .hero-text h1 { margin: 0 0 .3rem; font-size: 1.9rem; }
  .hero-sub { margin: 0; color: #8b949e; font-size: .98rem; }
  @media (max-width: 480px) {
    .hero { flex-direction: column; text-align: center; }
  }
</style>

<p id="dedicate" style="margin-top:3rem;color:#8b949e;font-size:0.9rem;opacity:0;transition:opacity .4s;user-select:none;">Dedicated to Z.J. ♡</p>
<canvas id="hearts" style="position:fixed;inset:0;width:100%;height:100%;pointer-events:none;z-index:15;"></canvas>

<script>
(function () {
  const title = document.querySelector('.site-title');
  const msg = document.getElementById('dedicate');
  const cv = document.getElementById('hearts');
  const ctx = cv.getContext('2d');
  const DPR = Math.min(window.devicePixelRatio || 1, 2);
  let W, H;
  function size() {
    W = cv.width = Math.round(window.innerWidth * DPR);
    H = cv.height = Math.round(window.innerHeight * DPR);
  }
  size();
  window.addEventListener('resize', size);

  const hearts = [];
  function burst(x, y) {
    for (let i = 0; i < 24; i++) {
      const a = Math.random() * Math.PI * 2;
      const sp = (1 + Math.random() * 3) * DPR;
      hearts.push({
        x: x, y: y,
        vx: Math.cos(a) * sp, vy: Math.sin(a) * sp - 2 * DPR,
        r: (4 + Math.random() * 5) * DPR, life: 1
      });
    }
  }
  function heart(x, y, r) {
    ctx.save();
    ctx.translate(x, y);
    ctx.scale(r / 16, r / 16);
    ctx.beginPath();
    ctx.moveTo(0, 4);
    ctx.bezierCurveTo(-8, -4, -16, 4, 0, 14);
    ctx.bezierCurveTo(16, 4, 8, -4, 0, 4);
    ctx.fillStyle = '#f778ba';
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
      heart(h.x, h.y, h.r);
    }
    ctx.globalAlpha = 1;
    requestAnimationFrame(loop);
  }
  loop();

  if (title) {
    title.style.cursor = 'pointer';
    title.addEventListener('click', function (e) {
      e.preventDefault();
      const rect = title.getBoundingClientRect();
      burst((rect.left + rect.width / 2) * DPR, rect.bottom * DPR);
      msg.style.opacity = '1';
      clearTimeout(title._t);
      title._t = setTimeout(function () { msg.style.opacity = '0'; }, 3000);
    });
  }
})();
</script>
