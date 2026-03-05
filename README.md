<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Highrise Productions</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --navy-deep: #020b18;
    --navy-mid: #041426;
    --navy-light: #072040;
    --blue-glow: #0a4f8c;
    --blue-bright: #1475d4;
    --blue-electric: #2e9cff;
    --blue-sky: #7dc9ff;
    --accent-gold: #e8c460;
    --text-primary: #e8f4ff;
    --text-secondary: #8ab4d4;
    --text-muted: #4a7090;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background-color: var(--navy-deep);
    color: var(--text-primary);
    font-family: 'Outfit', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    position: fixed; width: 10px; height: 10px;
    background: var(--blue-electric); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, background 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    position: fixed; width: 36px; height: 36px;
    border: 1.5px solid var(--blue-electric);
    border-radius: 50%; pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: all 0.15s ease;
    opacity: 0.5;
  }

  /* NOISE OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 1; opacity: 0.5;
  }

  /* ANIMATED GRID BACKGROUND */
  .grid-bg {
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(20,117,212,0.07) 1px, transparent 1px),
      linear-gradient(90deg, rgba(20,117,212,0.07) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridDrift 20s linear infinite;
  }
  @keyframes gridDrift {
    0% { transform: translateY(0); }
    100% { transform: translateY(60px); }
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100; padding: 24px 60px;
    display: flex; justify-content: space-between; align-items: center;
    border-bottom: 1px solid rgba(46,156,255,0.1);
    backdrop-filter: blur(20px);
    background: rgba(2, 11, 24, 0.7);
  }
  .nav-logo {
    font-family: 'Bebas Neue', cursive;
    font-size: 1.5rem; letter-spacing: 0.15em;
    color: var(--text-primary);
  }
  .nav-logo span { color: var(--blue-electric); }
  .nav-links { display: flex; gap: 40px; }
  .nav-links a {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem; letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--text-secondary); text-decoration: none;
    position: relative; transition: color 0.3s;
  }
  .nav-links a::after {
    content: ''; position: absolute; left: 0; bottom: -4px;
    width: 0; height: 1px; background: var(--blue-electric);
    transition: width 0.3s;
  }
  .nav-links a:hover { color: var(--blue-electric); }
  .nav-links a:hover::after { width: 100%; }

  /* SECTIONS */
  section { position: relative; z-index: 2; }

  /* HERO */
  #hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    text-align: center; padding: 120px 40px 80px;
    overflow: hidden;
  }
  .hero-glow {
    position: absolute;
    width: 700px; height: 700px;
    background: radial-gradient(circle, rgba(20,117,212,0.18) 0%, transparent 70%);
    top: 50%; left: 50%; transform: translate(-50%, -50%);
    animation: pulseGlow 4s ease-in-out infinite;
    pointer-events: none;
  }
  @keyframes pulseGlow {
    0%, 100% { opacity: 0.7; transform: translate(-50%, -50%) scale(1); }
    50% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
  }
  .hero-eyebrow {
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem; letter-spacing: 0.3em;
    color: var(--blue-electric); text-transform: uppercase;
    margin-bottom: 28px; opacity: 0;
    animation: fadeUp 0.8s ease forwards 0.3s;
  }
  .hero-title {
    font-family: 'Bebas Neue', cursive;
    font-size: clamp(5rem, 14vw, 12rem);
    line-height: 0.9; letter-spacing: 0.02em;
    color: var(--text-primary);
    opacity: 0; animation: fadeUp 0.9s ease forwards 0.5s;
  }
  .hero-title .line-blue { color: var(--blue-electric); display: block; }
  .hero-subtitle {
    margin-top: 32px;
    font-size: 1.1rem; font-weight: 300;
    color: var(--text-secondary); letter-spacing: 0.06em;
    opacity: 0; animation: fadeUp 0.9s ease forwards 0.8s;
  }
  .hero-tagline {
    font-family: 'Space Mono', monospace;
    font-size: 0.8rem; letter-spacing: 0.25em;
    color: var(--accent-gold); text-transform: uppercase;
    margin-top: 16px;
    opacity: 0; animation: fadeUp 0.9s ease forwards 1s;
  }
  .hero-cta {
    margin-top: 52px; display: flex; gap: 20px; justify-content: center; flex-wrap: wrap;
    opacity: 0; animation: fadeUp 0.9s ease forwards 1.2s;
  }
  .btn-primary {
    padding: 14px 40px;
    background: var(--blue-bright);
    color: #fff; border: none;
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem; letter-spacing: 0.15em; text-transform: uppercase;
    text-decoration: none; cursor: none;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
    transition: background 0.3s, transform 0.2s, box-shadow 0.3s;
  }
  .btn-primary:hover {
    background: var(--blue-electric);
    box-shadow: 0 0 30px rgba(46,156,255,0.4);
    transform: translateY(-2px);
  }
  .btn-outline {
    padding: 14px 40px;
    background: transparent;
    color: var(--blue-sky); border: 1px solid var(--blue-glow);
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem; letter-spacing: 0.15em; text-transform: uppercase;
    text-decoration: none; cursor: none;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
    transition: border-color 0.3s, color 0.3s, box-shadow 0.3s;
  }
  .btn-outline:hover {
    border-color: var(--blue-electric);
    color: var(--blue-electric);
    box-shadow: 0 0 20px rgba(46,156,255,0.15);
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* SCROLLING MARQUEE */
  .marquee-wrap {
    border-top: 1px solid rgba(46,156,255,0.15);
    border-bottom: 1px solid rgba(46,156,255,0.15);
    background: rgba(4, 20, 38, 0.8);
    overflow: hidden; padding: 16px 0;
  }
  .marquee-track {
    display: flex; gap: 60px;
    width: max-content;
    animation: marquee 20s linear infinite;
  }
  .marquee-item {
    font-family: 'Bebas Neue', cursive;
    font-size: 1.4rem; letter-spacing: 0.2em;
    color: var(--text-muted); white-space: nowrap;
    display: flex; align-items: center; gap: 16px;
  }
  .marquee-item .dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--blue-electric); flex-shrink: 0;
  }
  @keyframes marquee {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }

  /* ABOUT */
  #about {
    padding: 120px 60px;
    max-width: 1200px; margin: 0 auto;
  }
  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem; letter-spacing: 0.35em;
    color: var(--blue-electric); text-transform: uppercase;
    margin-bottom: 20px; display: flex; align-items: center; gap: 14px;
  }
  .section-label::before {
    content: ''; width: 32px; height: 1px;
    background: var(--blue-electric);
  }
  .section-title {
    font-family: 'Bebas Neue', cursive;
    font-size: clamp(2.8rem, 6vw, 5rem);
    line-height: 1; letter-spacing: 0.03em;
    margin-bottom: 28px;
  }
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 80px; align-items: center; margin-top: 60px;
  }
  .about-text p {
    font-size: 1.05rem; font-weight: 300; line-height: 1.9;
    color: var(--text-secondary); margin-bottom: 20px;
  }
  .about-text p strong { color: var(--text-primary); font-weight: 500; }
  .status-badge {
    display: inline-flex; align-items: center; gap: 10px;
    padding: 8px 20px;
    border: 1px solid rgba(46,156,255,0.3);
    background: rgba(20,117,212,0.1);
    font-family: 'Space Mono', monospace; font-size: 0.72rem;
    letter-spacing: 0.12em; color: var(--blue-sky);
    margin-top: 10px;
  }
  .pulse-dot {
    width: 8px; height: 8px; border-radius: 50%;
    background: #4ade80;
    box-shadow: 0 0 0 0 rgba(74,222,128,0.4);
    animation: pulseDot 2s ease-in-out infinite;
  }
  @keyframes pulseDot {
    0%, 100% { box-shadow: 0 0 0 0 rgba(74,222,128,0.4); }
    50% { box-shadow: 0 0 0 6px rgba(74,222,128,0); }
  }
  .about-visual {
    position: relative; height: 360px;
  }
  .about-box {
    position: absolute; border: 1px solid rgba(46,156,255,0.2);
    background: rgba(4,20,38,0.7); backdrop-filter: blur(10px);
    padding: 28px;
  }
  .about-box-main {
    inset: 0;
    display: flex; flex-direction: column; justify-content: center;
    align-items: center; text-align: center;
  }
  .big-number {
    font-family: 'Bebas Neue', cursive;
    font-size: 6rem; color: var(--blue-glow);
    line-height: 1;
  }
  .big-number span { color: var(--blue-electric); }
  .big-label {
    font-size: 0.85rem; color: var(--text-secondary);
    letter-spacing: 0.1em; margin-top: 8px;
  }
  .corner-accent {
    position: absolute; width: 20px; height: 20px;
    border-color: var(--blue-electric); border-style: solid;
  }
  .ca-tl { top: -1px; left: -1px; border-width: 2px 0 0 2px; }
  .ca-tr { top: -1px; right: -1px; border-width: 2px 2px 0 0; }
  .ca-bl { bottom: -1px; left: -1px; border-width: 0 0 2px 2px; }
  .ca-br { bottom: -1px; right: -1px; border-width: 0 2px 2px 0; }

  /* TEAM */
  #team {
    padding: 100px 60px;
    background: rgba(4,20,38,0.5);
    border-top: 1px solid rgba(46,156,255,0.08);
    border-bottom: 1px solid rgba(46,156,255,0.08);
  }
  .team-inner { max-width: 1200px; margin: 0 auto; }
  .team-grid {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 2px; margin-top: 60px;
  }
  .team-card {
    background: rgba(7,32,64,0.6);
    border: 1px solid rgba(46,156,255,0.12);
    padding: 44px 36px;
    position: relative; overflow: hidden;
    transition: border-color 0.3s, transform 0.3s;
  }
  .team-card::before {
    content: ''; position: absolute;
    top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, transparent, var(--blue-electric), transparent);
    transform: translateX(-100%);
    transition: transform 0.5s;
  }
  .team-card:hover { border-color: rgba(46,156,255,0.4); transform: translateY(-4px); }
  .team-card:hover::before { transform: translateX(0); }
  .card-number {
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem; letter-spacing: 0.2em;
    color: var(--text-muted); margin-bottom: 28px;
  }
  .card-role {
    font-family: 'Bebas Neue', cursive;
    font-size: 1.8rem; letter-spacing: 0.06em;
    color: var(--text-primary); margin-bottom: 6px;
    line-height: 1;
  }
  .card-count {
    font-size: 0.78rem; color: var(--blue-electric);
    font-family: 'Space Mono', monospace;
    letter-spacing: 0.1em; margin-bottom: 32px;
  }
  .skill-list { list-style: none; }
  .skill-list li {
    padding: 9px 0;
    border-bottom: 1px solid rgba(46,156,255,0.08);
    font-size: 0.9rem; font-weight: 300;
    color: var(--text-secondary);
    display: flex; align-items: center; gap: 12px;
    transition: color 0.2s;
  }
  .skill-list li:last-child { border-bottom: none; }
  .skill-list li::before {
    content: ''; width: 4px; height: 4px; border-radius: 50%;
    background: var(--blue-bright); flex-shrink: 0;
  }
  .team-card:hover .skill-list li { color: var(--text-primary); }

  /* TECH STACK */
  #tech {
    padding: 100px 60px;
    max-width: 1200px; margin: 0 auto;
  }
  .tech-grid {
    display: grid; grid-template-columns: repeat(5, 1fr);
    gap: 16px; margin-top: 60px;
  }
  .tech-item {
    border: 1px solid rgba(46,156,255,0.15);
    background: rgba(7,32,64,0.4);
    padding: 32px 20px; text-align: center;
    position: relative; overflow: hidden;
    transition: border-color 0.3s, background 0.3s;
    cursor: none;
  }
  .tech-item::after {
    content: ''; position: absolute;
    inset: 0;
    background: radial-gradient(circle at center, rgba(46,156,255,0.08), transparent 70%);
    opacity: 0; transition: opacity 0.3s;
  }
  .tech-item:hover { border-color: rgba(46,156,255,0.5); background: rgba(20,75,140,0.2); }
  .tech-item:hover::after { opacity: 1; }
  .tech-icon { font-size: 2rem; margin-bottom: 12px; display: block; }
  .tech-name {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem; letter-spacing: 0.12em;
    color: var(--text-secondary); text-transform: uppercase;
  }
  .tech-category {
    font-size: 0.65rem; color: var(--text-muted);
    margin-top: 6px; letter-spacing: 0.05em;
  }

  /* PROJECT STRUCTURE */
  #structure {
    padding: 100px 60px;
    background: rgba(4,20,38,0.5);
    border-top: 1px solid rgba(46,156,255,0.08);
    border-bottom: 1px solid rgba(46,156,255,0.08);
  }
  .structure-inner { max-width: 1200px; margin: 0 auto; }
  .structure-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 60px; margin-top: 60px; }
  .file-tree {
    background: rgba(2,11,24,0.8);
    border: 1px solid rgba(46,156,255,0.15);
    padding: 36px; font-family: 'Space Mono', monospace;
    position: relative;
  }
  .file-tree-header {
    display: flex; align-items: center; gap: 8px;
    margin-bottom: 24px; padding-bottom: 16px;
    border-bottom: 1px solid rgba(46,156,255,0.1);
  }
  .dot-red { width: 10px; height: 10px; border-radius: 50%; background: #ff5f57; }
  .dot-yellow { width: 10px; height: 10px; border-radius: 50%; background: #febc2e; }
  .dot-green { width: 10px; height: 10px; border-radius: 50%; background: #28c840; }
  .file-line {
    font-size: 0.78rem; line-height: 2;
    color: var(--text-secondary);
  }
  .file-line.dir { color: var(--blue-sky); }
  .file-line.root { color: var(--accent-gold); }
  .file-line .indent { margin-left: 20px; }
  .file-line .indent2 { margin-left: 40px; }
  .structure-desc {
    display: flex; flex-direction: column; gap: 20px; justify-content: center;
  }
  .desc-item {
    padding: 20px 24px;
    border-left: 2px solid var(--blue-glow);
    background: rgba(7,32,64,0.3);
    transition: border-color 0.3s;
  }
  .desc-item:hover { border-color: var(--blue-electric); }
  .desc-item h4 {
    font-family: 'Space Mono', monospace;
    font-size: 0.8rem; letter-spacing: 0.1em;
    color: var(--blue-sky); margin-bottom: 6px;
  }
  .desc-item p {
    font-size: 0.88rem; color: var(--text-muted); font-weight: 300;
  }

  /* LICENSE */
  #license {
    padding: 80px 60px;
    max-width: 1200px; margin: 0 auto;
    text-align: center;
  }
  .license-box {
    display: inline-block;
    border: 1px solid rgba(46,156,255,0.2);
    background: rgba(7,32,64,0.3);
    padding: 40px 60px;
    position: relative;
  }
  .license-box .corner-accent { position: absolute; }
  .license-title {
    font-family: 'Bebas Neue', cursive;
    font-size: 3rem; letter-spacing: 0.1em;
    color: var(--text-primary); margin-bottom: 8px;
  }
  .license-sub {
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem; letter-spacing: 0.15em;
    color: var(--blue-electric);
  }

  /* FOOTER */
  footer {
    border-top: 1px solid rgba(46,156,255,0.12);
    padding: 48px 60px;
    display: flex; justify-content: space-between; align-items: center;
    position: relative; z-index: 2;
    background: rgba(2,11,24,0.8);
  }
  .footer-brand {
    font-family: 'Bebas Neue', cursive;
    font-size: 1.3rem; letter-spacing: 0.15em;
    color: var(--text-secondary);
  }
  .footer-brand span { color: var(--blue-electric); }
  .footer-tagline {
    font-family: 'Space Mono', monospace;
    font-size: 0.7rem; letter-spacing: 0.2em;
    color: var(--accent-gold); text-transform: uppercase;
    margin-top: 4px;
  }
  .footer-right {
    font-family: 'Space Mono', monospace;
    font-size: 0.65rem; letter-spacing: 0.1em;
    color: var(--text-muted); text-align: right;
  }

  /* FLOATING PARTICLES */
  .particles { position: fixed; inset: 0; z-index: 1; pointer-events: none; }
  .particle {
    position: absolute; border-radius: 50%;
    background: var(--blue-electric);
    animation: floatParticle linear infinite;
    opacity: 0;
  }
  @keyframes floatParticle {
    0% { opacity: 0; transform: translateY(100vh) scale(0); }
    10% { opacity: 0.6; }
    90% { opacity: 0.2; }
    100% { opacity: 0; transform: translateY(-20vh) scale(1.5); }
  }

  /* SCROLL ANIMATIONS */
  .reveal {
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }
  .reveal-delay-4 { transition-delay: 0.4s; }

  @media (max-width: 900px) {
    nav { padding: 20px 24px; }
    .nav-links { display: none; }
    #about, #tech, #structure { padding: 80px 24px; }
    #team, #license { padding: 80px 24px; }
    footer { padding: 36px 24px; flex-direction: column; gap: 20px; text-align: center; }
    .about-grid, .structure-grid { grid-template-columns: 1fr; gap: 40px; }
    .team-grid { grid-template-columns: 1fr; }
    .tech-grid { grid-template-columns: repeat(3, 1fr); }
    .about-visual { height: 260px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="grid-bg"></div>
<div class="particles" id="particles"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">Highrise<span>.</span></div>
  <div class="nav-links">
    <a href="#about">About</a>
    <a href="#team">Team</a>
    <a href="#tech">Stack</a>
    <a href="#structure">Structure</a>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-glow"></div>
  <div>
    <div class="hero-eyebrow">Est. Active Development &nbsp;·&nbsp; MIT License</div>
    <h1 class="hero-title">
      Highrise
      <span class="line-blue">Productions</span>
    </h1>
    <p class="hero-subtitle">Creative Multimedia · AI-Driven Development · Digital Innovation</p>
    <p class="hero-tagline">See Beyond the Ordinary</p>
    <div class="hero-cta">
      <a href="#team" class="btn-primary">Meet the Team</a>
      <a href="#tech" class="btn-outline">Our Stack</a>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track" id="marqueeTrack">
    <span class="marquee-item"><span class="dot"></span>Motion Graphics</span>
    <span class="marquee-item"><span class="dot"></span>AI Development</span>
    <span class="marquee-item"><span class="dot"></span>Adobe Creative Cloud</span>
    <span class="marquee-item"><span class="dot"></span>Machine Learning</span>
    <span class="marquee-item"><span class="dot"></span>Web Development</span>
    <span class="marquee-item"><span class="dot"></span>Automation</span>
    <span class="marquee-item"><span class="dot"></span>Visual Design</span>
    <span class="marquee-item"><span class="dot"></span>Digital Innovation</span>
    <span class="marquee-item"><span class="dot"></span>Motion Graphics</span>
    <span class="marquee-item"><span class="dot"></span>AI Development</span>
    <span class="marquee-item"><span class="dot"></span>Adobe Creative Cloud</span>
    <span class="marquee-item"><span class="dot"></span>Machine Learning</span>
    <span class="marquee-item"><span class="dot"></span>Web Development</span>
    <span class="marquee-item"><span class="dot"></span>Automation</span>
    <span class="marquee-item"><span class="dot"></span>Visual Design</span>
    <span class="marquee-item"><span class="dot"></span>Digital Innovation</span>
  </div>
</div>

<!-- ABOUT -->
<section id="about">
  <div class="section-label reveal">Overview</div>
  <h2 class="section-title reveal">Building at the<br><span style="color:var(--blue-electric)">Intersection</span></h2>
  <div class="about-grid">
    <div class="about-text reveal">
      <p>
        <strong>Highrise Productions</strong> is a creative-technical studio where
        artistic vision meets intelligent systems. We combine the expressive depth of
        multimedia production with the precision of AI-driven engineering.
      </p>
      <p>
        Our team unites a dedicated <strong>multimedia artist</strong> fluent in the full
        Adobe Creative Cloud suite with <strong>two AI developers</strong> building
        next-generation automation and web experiences.
      </p>
      <div class="status-badge">
        <span class="pulse-dot"></span>
        Active Development
      </div>
    </div>
    <div class="about-visual reveal">
      <div class="about-box about-box-main">
        <div class="corner-accent ca-tl"></div>
        <div class="corner-accent ca-tr"></div>
        <div class="corner-accent ca-bl"></div>
        <div class="corner-accent ca-br"></div>
        <div class="big-number">H<span>P</span></div>
        <div class="big-label">Highrise Productions</div>
      </div>
    </div>
  </div>
</section>

<!-- TEAM -->
<section id="team">
  <div class="team-inner">
    <div class="section-label reveal">People</div>
    <h2 class="section-title reveal">The <span style="color:var(--blue-electric)">Team</span></h2>
    <div class="team-grid">

      <div class="team-card reveal reveal-delay-1">
        <div class="card-number">// 01</div>
        <div class="card-role">Multimedia<br>Artist</div>
        <div class="card-count">×1 Member</div>
        <ul class="skill-list">
          <li>Adobe Photoshop</li>
          <li>Adobe Illustrator</li>
          <li>Adobe Premiere Pro</li>
          <li>Adobe After Effects</li>
          <li>Graphic Design</li>
          <li>Motion Graphics</li>
        </ul>
      </div>

      <div class="team-card reveal reveal-delay-2">
        <div class="card-number">// 02</div>
        <div class="card-role">AI<br>Developer</div>
        <div class="card-count">×2 Members</div>
        <ul class="skill-list">
          <li>Python</li>
          <li>JavaScript</li>
          <li>AI / Machine Learning</li>
          <li>Automation</li>
          <li>HTML & CSS</li>
          <li>Web Development</li>
        </ul>
      </div>

      <div class="team-card reveal reveal-delay-3" style="background: linear-gradient(135deg, rgba(20,75,140,0.25), rgba(7,32,64,0.6));">
        <div class="card-number">// ∞</div>
        <div class="card-role">Combined<br>Vision</div>
        <div class="card-count">3 Collaborators</div>
        <ul class="skill-list">
          <li>End-to-end Digital Products</li>
          <li>Creative × Technical Fusion</li>
          <li>AI-Powered Experiences</li>
          <li>Multimedia Storytelling</li>
          <li>Rapid Prototyping</li>
          <li>Innovation Pipeline</li>
        </ul>
      </div>

    </div>
  </div>
</section>

<!-- TECH STACK -->
<section id="tech">
  <div class="section-label reveal">Technologies</div>
  <h2 class="section-title reveal">Our <span style="color:var(--blue-electric)">Stack</span></h2>
  <div class="tech-grid">
    <div class="tech-item reveal reveal-delay-1">
      <span class="tech-icon">🐍</span>
      <div class="tech-name">Python</div>
      <div class="tech-category">Backend · AI</div>
    </div>
    <div class="tech-item reveal reveal-delay-2">
      <span class="tech-icon">⚡</span>
      <div class="tech-name">JavaScript</div>
      <div class="tech-category">Frontend · Logic</div>
    </div>
    <div class="tech-item reveal reveal-delay-3">
      <span class="tech-icon">🌐</span>
      <div class="tech-name">HTML / CSS</div>
      <div class="tech-category">Web · Layout</div>
    </div>
    <div class="tech-item reveal reveal-delay-4">
      <span class="tech-icon">🤖</span>
      <div class="tech-name">AI / ML</div>
      <div class="tech-category">Intelligence</div>
    </div>
    <div class="tech-item reveal reveal-delay-1">
      <span class="tech-icon">🎨</span>
      <div class="tech-name">Adobe CC</div>
      <div class="tech-category">Creative Suite</div>
    </div>
  </div>
</section>

<!-- PROJECT STRUCTURE -->
<section id="structure">
  <div class="structure-inner">
    <div class="section-label reveal">Architecture</div>
    <h2 class="section-title reveal">Project <span style="color:var(--blue-electric)">Structure</span></h2>
    <div class="structure-grid">
      <div class="file-tree reveal">
        <div class="file-tree-header">
          <span class="dot-red"></span>
          <span class="dot-yellow"></span>
          <span class="dot-green"></span>
        </div>
        <div class="file-line root">📁 project/</div>
        <div class="file-line indent">│</div>
        <div class="file-line indent dir">├── 📂 assets/</div>
        <div class="file-line indent2" style="color:var(--text-muted);">└── media, images, icons</div>
        <div class="file-line indent">│</div>
        <div class="file-line indent dir">├── 📂 src/</div>
        <div class="file-line indent2" style="color:var(--text-muted);">└── source code & scripts</div>
        <div class="file-line indent">│</div>
        <div class="file-line indent dir">├── 📂 docs/</div>
        <div class="file-line indent2" style="color:var(--text-muted);">└── documentation</div>
        <div class="file-line indent">│</div>
        <div class="file-line indent" style="color:var(--accent-gold);">└── 📄 README.md</div>
      </div>
      <div class="structure-desc reveal">
        <div class="desc-item">
          <h4>/ assets</h4>
          <p>All media, imagery, icons, and creative assets produced by the multimedia team.</p>
        </div>
        <div class="desc-item">
          <h4>/ src</h4>
          <p>Core source code including Python scripts, JS modules, AI models, and automation pipelines.</p>
        </div>
        <div class="desc-item">
          <h4>/ docs</h4>
          <p>Project documentation, technical specs, design references, and workflow guides.</p>
        </div>
        <div class="desc-item">
          <h4>README.md</h4>
          <p>Repository overview, setup instructions, and team information at a glance.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- LICENSE -->
<section id="license">
  <div class="reveal">
    <div class="section-label" style="justify-content:center;">Legal</div>
    <h2 class="section-title" style="text-align:center;">Open &amp; <span style="color:var(--blue-electric)">Free</span></h2>
    <div style="margin-top:40px;">
      <div class="license-box">
        <div class="corner-accent ca-tl"></div>
        <div class="corner-accent ca-tr"></div>
        <div class="corner-accent ca-bl"></div>
        <div class="corner-accent ca-br"></div>
        <div class="license-title">MIT License</div>
        <div class="license-sub">Open Source · Free to Use · Attribution Required</div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div>
    <div class="footer-brand">Highrise<span>.</span>Productions</div>
    <div class="footer-tagline">See Beyond the Ordinary</div>
  </div>
  <div class="footer-right">
    <div>© 2025 Highrise Productions</div>
    <div style="margin-top:4px;">MIT Licensed · Active Development</div>
  </div>
</footer>

<script>
  // CURSOR
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
  });
  function animateRing() {
    rx += (mx - rx) * 0.12; ry += (my - ry) *.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();
  document.querySelectorAll('a, button, .tech-item, .team-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(2)';
      ring.style.transform = 'translate(-50%,-50%) scale(1.5)';
      ring.style.opacity = '0.8';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(1)';
      ring.style.transform = 'translate(-50%,-50%) scale(1)';
      ring.style.opacity = '0.5';
    });
  });

  // PARTICLES
  const pContainer = document.getElementById('particles');
  for (let i = 0; i < 22; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    const size = Math.random() * 3 + 1;
    p.style.cssText = `
      width:${size}px; height:${size}px;
      left:${Math.random()*100}%;
      animation-duration:${Math.random()*20+15}s;
      animation-delay:${Math.random()*20}s;
      opacity:0;
    `;
    pContainer.appendChild(p);
  }

  // SCROLL REVEAL
  const reveals = document.querySelectorAll('.reveal');
  const obs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); }
    });
  }, { threshold: 0.1 });
  reveals.forEach(r => obs.observe(r));
</script>
</body>
</html>
