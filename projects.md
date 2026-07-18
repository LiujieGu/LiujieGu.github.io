---
layout: page
title: Projects
permalink: /projects/
---

# Projects

A selection of open-source projects I've built or contributed to. Most live on [GitHub](https://github.com/LiujieGu).

<div class="project-list">

  <div class="project-card project-card--wide">
    <div class="proj-main">
      <h3><a href="https://github.com/LiujieGu/helix">helix</a></h3>
      <p class="proj-desc">A C++20 numerical optimization library: a sparse convex QP/LP solver built on OSQP, with workspace reuse, warm start, and portfolio examples (mean–variance QP, alpha max LP).</p>
      <p class="proj-meta"><span class="tag">C++20</span><span class="tag">Optimization</span><span class="tag">Quant</span></p>
    </div>
    <div class="proj-side">
      <div class="side-block">
        <span class="side-title">Features</span>
        <ul>
          <li>Convex QP &amp; LP (box / linear constraints)</li>
          <li>Simplex projection &amp; O(n) linear solve</li>
          <li>Workspace reuse &amp; warm start</li>
          <li>Structured status diagnostics</li>
        </ul>
      </div>
      <div class="side-block">
        <span class="side-title">Performance</span>
        <ul>
          <li>100 vars: 0.073 ms (warm)</li>
          <li>1k vars: 0.42 ms (warm)</li>
          <li>5k vars: 2.10 ms (warm)</li>
        </ul>
      </div>
      <div class="side-block">
        <span class="side-title">Status</span>
        <ul>
          <li>Alpha · OSQP backend</li>
          <li>Portfolio examples</li>
        </ul>
      </div>
    </div>
  </div>

  <div class="project-card project-card--wide">
    <div class="proj-main">
      <h3><a href="https://github.com/LiujieGu/databuffer">databuffer</a></h3>
      <p class="proj-desc">A small Python package for sharing factor data across processes via a POSIX shared-memory ring buffer, with optional file-backed <code>mmap</code> storage. One process writes cross-sectional snapshots with <code>BufferWriter</code>; others read the latest state, a recent window, or a timestamp range with <code>BufferReader</code>.</p>
      <p class="proj-meta"><span class="tag">Python</span><span class="tag">Shared Memory</span><span class="tag">Quant</span></p>
    </div>
    <div class="proj-side">
      <div class="side-block">
        <span class="side-title">Features</span>
        <ul>
          <li>POSIX shm ring buffer + optional mmap</li>
          <li>Read latest / window / timestamp range</li>
          <li>Version guard against torn reads</li>
          <li>Dynamic stock-map refresh (TTL)</li>
        </ul>
      </div>
      <div class="side-block">
        <span class="side-title">API</span>
        <ul>
          <li><code>BufferWriter.write_data()</code></li>
          <li><code>read_latest_data_as_dict()</code></li>
          <li><code>read_window_data(size)</code></li>
          <li><code>check_timestamp_continuity()</code></li>
        </ul>
      </div>
      <div class="side-block">
        <span class="side-title">Notes</span>
        <ul>
          <li>Single-writer, multi-reader</li>
          <li>float32 / float64 support</li>
          <li>loguru logging built-in</li>
        </ul>
      </div>
    </div>
  </div>

</div>

---

<p style="color:#8b949e;font-size:0.9rem;">
  Want to see everything? Visit my <a href="https://github.com/LiujieGu">GitHub profile</a>.
</p>

<style>
  .project-list { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 1.2rem; margin-top: 1.5rem; }
  .project-card { border: 1px solid #30363d; border-radius: 10px; padding: 1rem 1.2rem; background: #161b22; transition: border-color .2s, transform .2s; }
  .project-card:hover { border-color: #58a6ff; transform: translateY(-3px); }
  .project-card h3 { margin: 0 0 .4rem; font-size: 1.05rem; }
  .project-card h3 a { color: #58a6ff; text-decoration: none; }
  .proj-desc { margin: 0 0 .6rem; color: #c9d1d9; font-size: .92rem; line-height: 1.5; }
  .proj-meta { margin: 0; font-size: .8rem; color: #8b949e; }
  .tag { display: inline-block; background: #21262d; border: 1px solid #30363d; border-radius: 999px; padding: 1px 8px; margin-right: 4px; font-size: .75rem; color: #8b949e; }
  .project-card--wide { grid-column: 1 / -1; display: flex; gap: 1.5rem; flex-wrap: wrap; }
  .proj-main { flex: 1 1 300px; min-width: 260px; }
  .proj-side { flex: 1 1 300px; min-width: 240px; display: flex; flex-direction: column; gap: .8rem; border-left: 1px solid #30363d; padding-left: 1.2rem; }
  .side-block .side-title { display: block; font-size: .78rem; letter-spacing: .04em; text-transform: uppercase; color: #58a6ff; margin-bottom: .3rem; }
  .side-block ul { margin: 0; padding-left: 1.1rem; }
  .side-block li { font-size: .85rem; color: #c9d1d9; line-height: 1.6; }
  .project-card code {
    background: #0d1117;
    border: 1px solid #30363d;
    border-radius: 5px;
    padding: .08em .4em;
    color: #79c0ff;
    font-family: ui-monospace, SFMono-Regular, Menlo, monospace;
    font-size: .85em;
  }
  @media (max-width: 560px) {
    .proj-side { border-left: none; padding-left: 0; }
  }
</style>
