<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smaran — Backend Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Bebas+Neue&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050A0E;
    --surface: #0C1318;
    --border: #1A2730;
    --accent: #00FFB2;
    --accent2: #FF6B35;
    --accent3: #7B61FF;
    --text: #E8F4F0;
    --muted: #4A6670;
    --glow: rgba(0, 255, 178, 0.15);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* Grid texture */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0, 255, 178, 0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0, 255, 178, 0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  /* Floating orbs */
  .orb {
    position: fixed;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
    animation: drift 20s ease-in-out infinite;
  }
  .orb-1 {
    width: 500px; height: 500px;
    background: rgba(0, 255, 178, 0.06);
    top: -100px; right: -100px;
    animation-delay: 0s;
  }
  .orb-2 {
    width: 400px; height: 400px;
    background: rgba(123, 97, 255, 0.07);
    bottom: 100px; left: -100px;
    animation-delay: -10s;
  }

  @keyframes drift {
    0%, 100% { transform: translate(0, 0); }
    33% { transform: translate(30px, -20px); }
    66% { transform: translate(-20px, 30px); }
  }

  /* Navigation */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 20px 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: rgba(5, 10, 14, 0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    font-family: 'Bebas Neue', cursive;
    font-size: 24px;
    letter-spacing: 3px;
    color: var(--accent);
    text-shadow: 0 0 20px var(--accent);
  }

  .nav-links {
    display: flex;
    gap: 32px;
    list-style: none;
  }

  .nav-links a {
    color: var(--muted);
    text-decoration: none;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  .nav-links a:hover { color: var(--accent); }

  .status-dot {
    display: flex;
    align-items: center;
    gap: 8px;
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--accent);
    letter-spacing: 1px;
  }

  .status-dot::before {
    content: '';
    width: 6px; height: 6px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse-dot 2s ease-in-out infinite;
    box-shadow: 0 0 8px var(--accent);
  }

  @keyframes pulse-dot {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.7); }
  }

  /* Main wrapper */
  main {
    position: relative;
    z-index: 1;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 40px;
  }

  /* Hero */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-top: 80px;
  }

  .hero-tag {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 4px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.2s;
  }

  .hero-name {
    font-family: 'Bebas Neue', cursive;
    font-size: clamp(80px, 14vw, 160px);
    line-height: 0.9;
    letter-spacing: 4px;
    color: var(--text);
    margin-bottom: 8px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.4s;
  }

  .hero-name span {
    color: var(--accent);
    text-shadow: 0 0 40px rgba(0, 255, 178, 0.4);
    display: inline-block;
    animation: glitch 8s infinite;
  }

  @keyframes glitch {
    0%, 92%, 100% { transform: translate(0); }
    93% { transform: translate(-2px, 1px); filter: hue-rotate(90deg); }
    94% { transform: translate(2px, -1px); }
    95% { transform: translate(0); }
    96% { transform: translate(-1px, 2px); filter: hue-rotate(-90deg); }
    97% { transform: translate(0); }
  }

  .hero-subtitle {
    font-family: 'Space Mono', monospace;
    font-size: 14px;
    color: var(--muted);
    letter-spacing: 2px;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.6s;
  }

  .hero-subtitle span {
    color: var(--accent2);
  }

  .hero-desc {
    font-size: 17px;
    color: var(--muted);
    max-width: 500px;
    line-height: 1.7;
    font-weight: 300;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.8s;
  }

  .hero-cta {
    display: flex;
    gap: 16px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 1s;
  }

  .btn {
    padding: 14px 32px;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    text-decoration: none;
    border: none;
    cursor: pointer;
    transition: all 0.2s;
    position: relative;
    overflow: hidden;
  }

  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    font-weight: 700;
  }

  .btn-primary:hover {
    background: transparent;
    color: var(--accent);
    box-shadow: inset 0 0 0 1px var(--accent), 0 0 20px var(--glow);
  }

  .btn-ghost {
    background: transparent;
    color: var(--muted);
    box-shadow: inset 0 0 0 1px var(--border);
  }

  .btn-ghost:hover {
    color: var(--text);
    box-shadow: inset 0 0 0 1px var(--muted);
  }

  /* Section styles */
  section {
    padding: 100px 0;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 60px;
  }

  .section-num {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 2px;
  }

  .section-title {
    font-family: 'Bebas Neue', cursive;
    font-size: 48px;
    letter-spacing: 3px;
    color: var(--text);
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* About grid */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
  }

  .about-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 32px;
    transition: border-color 0.2s, background 0.2s;
  }

  .about-card:hover {
    border-color: var(--accent);
    background: rgba(0, 255, 178, 0.03);
  }

  .about-card-icon {
    font-size: 28px;
    margin-bottom: 16px;
  }

  .about-card-title {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 3px;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .about-card-text {
    font-size: 15px;
    color: var(--muted);
    line-height: 1.6;
  }

  .about-card-text strong {
    color: var(--text);
  }

  /* Stack section */
  .stack-groups {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 2px;
  }

  .stack-group {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 28px 32px;
  }

  .stack-group-title {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 3px;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--border);
  }

  .stack-items {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .stack-tag {
    display: inline-block;
    padding: 6px 14px;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 1px;
    border: 1px solid var(--border);
    color: var(--muted);
    transition: all 0.2s;
    cursor: default;
  }

  .stack-tag:hover {
    border-color: var(--accent);
    color: var(--accent);
    background: var(--glow);
  }

  .stack-tag.highlight {
    border-color: rgba(0, 255, 178, 0.3);
    color: var(--accent);
    background: rgba(0, 255, 178, 0.05);
  }

  /* Projects */
  .projects-list {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 32px;
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 32px;
    transition: all 0.2s;
    text-decoration: none;
    color: inherit;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }

  .project-card::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: var(--accent);
    transform: scaleY(0);
    transition: transform 0.2s;
    transform-origin: bottom;
  }

  .project-card:hover {
    border-color: var(--accent);
    background: rgba(0, 255, 178, 0.03);
  }

  .project-card:hover::before {
    transform: scaleY(1);
  }

  .project-num {
    font-family: 'Bebas Neue', cursive;
    font-size: 40px;
    color: var(--border);
    width: 60px;
    line-height: 1;
  }

  .project-card:hover .project-num {
    color: rgba(0, 255, 178, 0.2);
  }

  .project-info {}

  .project-name {
    font-family: 'Bebas Neue', cursive;
    font-size: 28px;
    letter-spacing: 2px;
    color: var(--text);
    margin-bottom: 6px;
  }

  .project-desc {
    font-size: 14px;
    color: var(--muted);
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    margin-top: 10px;
  }

  .project-tag {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 1px;
    color: var(--accent);
    border: 1px solid rgba(0, 255, 178, 0.2);
    padding: 3px 8px;
    text-transform: uppercase;
  }

  .project-status {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 2px;
    text-align: right;
  }

  .status-live {
    color: var(--accent);
  }

  .status-soon {
    color: var(--accent2);
  }

  /* Stats bar */
  .stats-bar {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin: 60px 0;
  }

  .stat-item {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 32px;
    text-align: center;
  }

  .stat-num {
    font-family: 'Bebas Neue', cursive;
    font-size: 56px;
    color: var(--accent);
    text-shadow: 0 0 30px rgba(0, 255, 178, 0.3);
    line-height: 1;
    display: block;
  }

  .stat-label {
    font-family: 'Space Mono', monospace;
    font-size: 9px;
    letter-spacing: 3px;
    color: var(--muted);
    text-transform: uppercase;
    margin-top: 8px;
    display: block;
  }

  /* Quote */
  .quote-block {
    border-left: 3px solid var(--accent);
    padding: 32px 40px;
    background: var(--surface);
    margin: 60px 0;
    position: relative;
  }

  .quote-block::before {
    content: '"';
    font-family: 'Bebas Neue', cursive;
    font-size: 120px;
    color: rgba(0, 255, 178, 0.08);
    position: absolute;
    top: -20px;
    left: 20px;
    line-height: 1;
    pointer-events: none;
  }

  .quote-text {
    font-family: 'Bebas Neue', cursive;
    font-size: 32px;
    letter-spacing: 2px;
    color: var(--text);
    line-height: 1.2;
  }

  .quote-author {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--accent);
    letter-spacing: 3px;
    margin-top: 16px;
    text-transform: uppercase;
  }

  /* Footer */
  footer {
    border-top: 1px solid var(--border);
    padding: 60px 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .footer-logo {
    font-family: 'Bebas Neue', cursive;
    font-size: 20px;
    letter-spacing: 4px;
    color: var(--muted);
  }

  .footer-links {
    display: flex;
    gap: 24px;
    list-style: none;
  }

  .footer-links a {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    letter-spacing: 2px;
    color: var(--muted);
    text-decoration: none;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  .footer-links a:hover { color: var(--accent); }

  .footer-tagline {
    font-family: 'Space Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 2px;
  }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Scanline effect */
  .scanline {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0.15;
    animation: scan 8s linear infinite;
    pointer-events: none;
    z-index: 999;
  }

  @keyframes scan {
    0% { top: -2px; }
    100% { top: 100vh; }
  }

  /* Responsive */
  @media (max-width: 768px) {
    nav { padding: 16px 20px; }
    .nav-links { display: none; }
    main { padding: 0 20px; }
    .hero-name { font-size: clamp(60px, 18vw, 100px); }
    .about-grid { grid-template-columns: 1fr; }
    .stack-groups { grid-template-columns: 1fr; }
    .stats-bar { grid-template-columns: 1fr; }
    .project-card { grid-template-columns: 1fr; gap: 16px; }
    .project-num { display: none; }
    footer { flex-direction: column; gap: 24px; text-align: center; }
    .footer-links { flex-wrap: wrap; justify-content: center; }
  }
</style>
</head>
<body>

<div class="scanline"></div>
<div class="orb orb-1"></div>
<div class="orb orb-2"></div>

<!-- Nav -->
<nav>
  <div class="nav-logo">SMR</div>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#stack">Stack</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="status-dot">Available for collab</div>
</nav>

<main>

  <!-- Hero -->
  <section class="hero">
    <p class="hero-tag">// portfolio v1.0 — smaran9.dev</p>
    <h1 class="hero-name">SMA<span>RAN</span></h1>
    <p class="hero-subtitle">Backend Dev &nbsp;·&nbsp; <span>Data Science Explorer</span> &nbsp;·&nbsp; Future Engineer</p>
    <p class="hero-desc">Building robust systems from the ground up. Python-powered. Discipline-driven. Targeting GATE and a high-level tech career — one commit at a time.</p>
    <div class="hero-cta">
      <a href="#projects" class="btn btn-primary">View Projects</a>
      <a href="https://github.com/smaran9" class="btn btn-ghost">GitHub ↗</a>
    </div>
  </section>

  <!-- About -->
  <section id="about">
    <div class="section-header reveal">
      <span class="section-num">01</span>
      <h2 class="section-title">About</h2>
      <div class="section-line"></div>
    </div>
    <div class="about-grid reveal">
      <div class="about-card">
        <div class="about-card-icon">⚡</div>
        <div class="about-card-title">The Mission</div>
        <div class="about-card-text">Backend developer in progress, grinding toward <strong>GATE</strong> and a high-level tech career. Not waiting for motivation — running on <strong>discipline</strong>.</div>
      </div>
      <div class="about-card">
        <div class="about-card-icon">🤖</div>
        <div class="about-card-title">Current Build</div>
        <div class="about-card-text">Actively developing a <strong>Voice Assistant</strong> in Python. Exploring <strong>Data Science</strong> while building real, shipped projects.</div>
      </div>
      <div class="about-card">
        <div class="about-card-icon">🎯</div>
        <div class="about-card-title">Focus Areas</div>
        <div class="about-card-text">Backend architecture, <strong>system design</strong>, and Python data pipelines. Blending engineering rigor with data-driven thinking.</div>
      </div>
      <div class="about-card">
        <div class="about-card-icon">📊</div>
        <div class="about-card-title">The Mindset</div>
        <div class="about-card-text"><strong>No excuses. Only growth.</strong> Each day of consistency compounds. Systems built right, not fast.</div>
      </div>
    </div>
  </section>

  <!-- Stats -->
  <div class="stats-bar reveal">
    <div class="stat-item">
      <span class="stat-num">5+</span>
      <span class="stat-label">Languages</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">∞</span>
      <span class="stat-label">Daily Commits</span>
    </div>
    <div class="stat-item">
      <span class="stat-num">1</span>
      <span class="stat-label">Goal: GATE</span>
    </div>
  </div>

  <!-- Stack -->
  <section id="stack">
    <div class="section-header reveal">
      <span class="section-num">02</span>
      <h2 class="section-title">Tech Stack</h2>
      <div class="section-line"></div>
    </div>
    <div class="stack-groups reveal">
      <div class="stack-group">
        <div class="stack-group-title">// Languages</div>
        <div class="stack-items">
          <span class="stack-tag highlight">Python</span>
          <span class="stack-tag highlight">C++</span>
          <span class="stack-tag">C</span>
          <span class="stack-tag">JavaScript</span>
          <span class="stack-tag">TypeScript</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-title">// Backend</div>
        <div class="stack-items">
          <span class="stack-tag highlight">Flask</span>
          <span class="stack-tag highlight">MySQL</span>
          <span class="stack-tag">REST APIs</span>
          <span class="stack-tag">SQLite</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-title">// Frontend</div>
        <div class="stack-items">
          <span class="stack-tag">HTML5</span>
          <span class="stack-tag">CSS3</span>
        </div>
      </div>
      <div class="stack-group">
        <div class="stack-group-title">// Tools & Environment</div>
        <div class="stack-items">
          <span class="stack-tag highlight">Git</span>
          <span class="stack-tag highlight">GitHub</span>
          <span class="stack-tag">VS Code</span>
          <span class="stack-tag">Linux</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Projects -->
  <section id="projects">
    <div class="section-header reveal">
      <span class="section-num">03</span>
      <h2 class="section-title">Projects</h2>
      <div class="section-line"></div>
    </div>
    <div class="projects-list reveal">

      <div class="project-card">
        <div class="project-num">01</div>
        <div class="project-info">
          <div class="project-name">Voice Assistant</div>
          <div class="project-desc">Python-powered voice assistant with NLP, command parsing, and real-time speech recognition.</div>
          <div class="project-tags">
            <span class="project-tag">Python</span>
            <span class="project-tag">NLP</span>
            <span class="project-tag">Speech</span>
          </div>
        </div>
        <div class="project-status status-live">● In Progress</div>
      </div>

      <div class="project-card">
        <div class="project-num">02</div>
        <div class="project-info">
          <div class="project-name">Softline Infotech Website</div>
          <div class="project-desc">Full company website — designed and developed end-to-end. Production deployed.</div>
          <div class="project-tags">
            <span class="project-tag">HTML</span>
            <span class="project-tag">CSS</span>
            <span class="project-tag">Flask</span>
          </div>
        </div>
        <div class="project-status status-live">● Live</div>
      </div>

      <div class="project-card">
        <div class="project-num">03</div>
        <div class="project-info">
          <div class="project-name">Data Science Suite</div>
          <div class="project-desc">A growing collection of data science experiments — EDA, ML models, and visualization pipelines.</div>
          <div class="project-tags">
            <span class="project-tag">Python</span>
            <span class="project-tag">Pandas</span>
            <span class="project-tag">ML</span>
          </div>
        </div>
        <div class="project-status status-soon">◌ Coming Soon</div>
      </div>

    </div>
  </section>

  <!-- Quote -->
  <div class="quote-block reveal">
    <div class="quote-text">Discipline creates power.<br>Consistency creates results.</div>
    <div class="quote-author">— Smaran's operating system</div>
  </div>

  <!-- Contact -->
  <section id="contact">
    <div class="section-header reveal">
      <span class="section-num">04</span>
      <h2 class="section-title">Connect</h2>
      <div class="section-line"></div>
    </div>
    <div class="about-grid reveal">
      <div class="about-card">
        <div class="about-card-icon">📡</div>
        <div class="about-card-title">GitHub</div>
        <div class="about-card-text">All projects, commits, and code activity. Grinding daily. <br><br><a href="https://github.com/smaran9" style="color: var(--accent); font-family: 'Space Mono', monospace; font-size: 12px; text-decoration: none;">github.com/smaran9 ↗</a></div>
      </div>
      <div class="about-card">
        <div class="about-card-icon">🤝</div>
        <div class="about-card-title">Open To</div>
        <div class="about-card-text">Collaborations, open source, backend projects, and anyone who ships real work.</div>
      </div>
    </div>
  </section>

  <!-- Footer -->
  <footer>
    <div class="footer-logo">SMARAN</div>
    <ul class="footer-links">
      <li><a href="https://github.com/smaran9">GitHub</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#projects">Projects</a></li>
    </ul>
    <div class="footer-tagline">🔥 No excuses. Only growth.</div>
  </footer>

</main>

<script>
  // Reveal on scroll
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => observer.observe(el));

  // Counter animation for stats
  function animateCounter(el, target, suffix = '') {
    let count = 0;
    const step = target / 40;
    const interval = setInterval(() => {
      count += step;
      if (count >= target) {
        el.textContent = target + suffix;
        clearInterval(interval);
      } else {
        el.textContent = Math.floor(count) + suffix;
      }
    }, 30);
  }

  const statNums = document.querySelectorAll('.stat-num');
  const statObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const el = entry.target;
        const text = el.textContent;
        if (text === '5+') animateCounter(el, 5, '+');
        else if (text === '1') animateCounter(el, 1);
        statObserver.unobserve(el);
      }
    });
  }, { threshold: 0.5 });
  statNums.forEach(el => statObserver.observe(el));
</script>
</body>
</html>
