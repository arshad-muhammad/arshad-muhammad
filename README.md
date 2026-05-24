<html><head><style>
  @import url('https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=JetBrains+Mono:wght@400;500&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; }

  .profile-wrap {
    background: #0a0c0f;
    min-height: 100vh;
    font-family: 'Syne', sans-serif;
    color: #e8e8e8;
    padding: 0;
    position: relative;
    overflow: hidden;
  }

  .noise-bg {
    position: absolute;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
  }

  .grid-lines {
    position: absolute;
    inset: 0;
    background-image: 
      linear-gradient(rgba(29,158,117,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(29,158,117,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .glow-orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    z-index: 0;
  }
  .orb1 { width: 300px; height: 300px; background: rgba(29,158,117,0.12); top: -80px; right: -60px; }
  .orb2 { width: 200px; height: 200px; background: rgba(55,138,221,0.08); bottom: 100px; left: -80px; }
  .orb3 { width: 160px; height: 160px; background: rgba(239,159,39,0.06); top: 300px; right: 30px; }

  .content { position: relative; z-index: 1; max-width: 680px; margin: 0 auto; padding: 36px 24px 40px; }

  /* Top bar */
  .top-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 40px;
  }

  .visitor-pill {
    display: flex;
    align-items: center;
    gap: 8px;
    background: rgba(29,158,117,0.1);
    border: 0.5px solid rgba(29,158,117,0.3);
    border-radius: 20px;
    padding: 5px 14px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: #1D9E75;
    letter-spacing: 0.05em;
  }

  .visitor-dot { width: 6px; height: 6px; background: #1D9E75; border-radius: 50%; animation: pulse-dot 2s infinite; }
  @keyframes pulse-dot { 0%,100%{opacity:1;transform:scale(1);} 50%{opacity:0.5;transform:scale(0.8);} }

  .role-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.3);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  /* Hero */
  .hero { margin-bottom: 40px; }

  .name-block {
    position: relative;
    margin-bottom: 12px;
  }

  .name-accent {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: clamp(36px, 8vw, 52px);
    color: #fff;
    line-height: 1.05;
    letter-spacing: -0.02em;
    display: block;
  }

  .name-accent span {
    color: #1D9E75;
  }

  .hero-tagline {
    font-size: 15px;
    color: rgba(255,255,255,0.45);
    font-family: 'JetBrains Mono', monospace;
    margin-bottom: 20px;
    letter-spacing: 0.02em;
  }

  .hero-tagline em { color: #1D9E75; font-style: normal; }

  .badge-row {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 16px;
  }

  .badge {
    font-size: 11px;
    font-family: 'JetBrains Mono', monospace;
    letter-spacing: 0.04em;
    padding: 5px 12px;
    border-radius: 4px;
    border: 0.5px solid;
    font-weight: 500;
  }

  .badge-green { background: rgba(29,158,117,0.1); border-color: rgba(29,158,117,0.3); color: #1D9E75; }
  .badge-blue { background: rgba(55,138,221,0.1); border-color: rgba(55,138,221,0.3); color: #378ADD; }
  .badge-amber { background: rgba(239,159,39,0.1); border-color: rgba(239,159,39,0.3); color: #EF9F27; }
  .badge-pink { background: rgba(212,83,126,0.1); border-color: rgba(212,83,126,0.3); color: #D4537E; }

  /* Divider */
  .divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 28px 0;
  }
  .divider-line { flex: 1; height: 0.5px; background: linear-gradient(90deg, rgba(29,158,117,0.4), transparent); }
  .divider-label { font-family: 'JetBrains Mono', monospace; font-size: 10px; color: rgba(255,255,255,0.2); letter-spacing: 0.15em; text-transform: uppercase; }

  /* About me cards */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    margin-bottom: 28px;
  }

  .about-card {
    background: rgba(255,255,255,0.03);
    border: 0.5px solid rgba(255,255,255,0.07);
    border-radius: 10px;
    padding: 14px 16px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.2s, background 0.2s;
  }

  .about-card:hover {
    border-color: rgba(29,158,117,0.3);
    background: rgba(29,158,117,0.04);
  }

  .about-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 2px; height: 100%;
    border-radius: 0;
    opacity: 0.8;
  }

  .ac-green::before { background: #1D9E75; }
  .ac-blue::before { background: #378ADD; }
  .ac-amber::before { background: #EF9F27; }
  .ac-pink::before { background: #D4537E; }

  .about-card-icon { font-size: 16px; margin-bottom: 6px; }
  .about-card-title { font-size: 10px; text-transform: uppercase; letter-spacing: 0.1em; color: rgba(255,255,255,0.3); font-family: 'JetBrains Mono', monospace; margin-bottom: 4px; }
  .about-card-val { font-size: 13px; color: rgba(255,255,255,0.8); font-weight: 700; line-height: 1.3; }

  /* Connect */
  .connect-row {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 28px;
  }

  .social-btn {
    display: flex;
    align-items: center;
    gap: 7px;
    padding: 8px 16px;
    border-radius: 6px;
    border: 0.5px solid rgba(255,255,255,0.1);
    background: rgba(255,255,255,0.04);
    font-size: 13px;
    font-weight: 700;
    color: rgba(255,255,255,0.7);
    text-decoration: none;
    cursor: pointer;
    transition: all 0.18s;
    font-family: 'Syne', sans-serif;
  }

  .social-btn:hover {
    border-color: rgba(255,255,255,0.25);
    background: rgba(255,255,255,0.08);
    color: #fff;
    transform: translateY(-1px);
  }

  .social-btn svg { width: 15px; height: 15px; }

  /* Stack */
  .stack-section { margin-bottom: 28px; }

  .stack-icons {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 12px;
  }

  .tech-pill {
    display: flex;
    align-items: center;
    gap: 6px;
    padding: 6px 12px;
    background: rgba(255,255,255,0.04);
    border: 0.5px solid rgba(255,255,255,0.08);
    border-radius: 6px;
    font-size: 12px;
    font-family: 'JetBrains Mono', monospace;
    color: rgba(255,255,255,0.6);
    transition: all 0.18s;
  }

  .tech-pill:hover {
    background: rgba(29,158,117,0.08);
    border-color: rgba(29,158,117,0.25);
    color: rgba(255,255,255,0.9);
  }

  .tech-dot { width: 6px; height: 6px; border-radius: 50%; flex-shrink: 0; }

  /* Stats area */
  .stats-section { margin-bottom: 28px; }

  .stats-embed {
    background: rgba(255,255,255,0.02);
    border: 0.5px solid rgba(255,255,255,0.07);
    border-radius: 12px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .stat-row-item {
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .stat-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.3);
    width: 90px;
    flex-shrink: 0;
    letter-spacing: 0.04em;
  }

  .stat-bar-wrap {
    flex: 1;
    height: 4px;
    background: rgba(255,255,255,0.05);
    border-radius: 2px;
    overflow: hidden;
  }

  .stat-bar {
    height: 100%;
    border-radius: 2px;
    animation: grow-bar 1.4s cubic-bezier(0.16,1,0.3,1) forwards;
    transform-origin: left;
  }

  @keyframes grow-bar {
    from { width: 0%; }
    to { width: var(--w); }
  }

  .stat-val {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    font-weight: 500;
    width: 36px;
    text-align: right;
  }

  /* Streak display */
  .streak-block {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: rgba(29,158,117,0.06);
    border: 0.5px solid rgba(29,158,117,0.2);
    border-radius: 10px;
    padding: 16px 20px;
    margin-top: 10px;
  }

  .streak-num {
    font-weight: 800;
    font-size: 36px;
    color: #1D9E75;
    line-height: 1;
  }

  .streak-num span {
    font-size: 14px;
    color: rgba(255,255,255,0.3);
    font-weight: 400;
    margin-left: 4px;
    font-family: 'JetBrains Mono', monospace;
  }

  .streak-label {
    font-size: 11px;
    color: rgba(255,255,255,0.35);
    font-family: 'JetBrains Mono', monospace;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-top: 2px;
  }

  .streak-fire { font-size: 28px; }

  /* Activity dots */
  .activity-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 3px;
    margin-top: 10px;
  }

  .act-dot {
    width: 9px;
    height: 9px;
    border-radius: 2px;
    background: rgba(255,255,255,0.05);
    transition: background 0.2s;
  }

  .act-dot:hover { background: rgba(29,158,117,0.7) !important; }

  /* Footer */
  .profile-footer {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-top: 20px;
    border-top: 0.5px solid rgba(255,255,255,0.06);
  }

  .footer-credit {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: rgba(255,255,255,0.2);
    letter-spacing: 0.04em;
  }

  .footer-credit em { color: #1D9E75; font-style: normal; }

  .section-head {
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.15em;
    color: rgba(255,255,255,0.2);
    font-family: 'JetBrains Mono', monospace;
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .section-head::after {
    content: '';
    flex: 1;
    height: 0.5px;
    background: rgba(255,255,255,0.07);
  }
</style>

</head><body><div class="profile-wrap">
  <div class="noise-bg"></div>
  <div class="grid-lines"></div>
  <div class="glow-orb orb1"></div>
  <div class="glow-orb orb2"></div>
  <div class="glow-orb orb3"></div>

  <div class="content">

    <!-- Top bar -->
    <div class="top-bar">
      <div class="role-tag">// Creative Technologist</div>
      <div class="visitor-pill">
        <div class="visitor-dot"></div>
        <span>profile views · live</span>
      </div>
    </div>

    <!-- Hero -->
    <div class="hero">
      <div class="name-block">
        <span class="name-accent">Muhammad<br><span>Arshad.</span></span>
      </div>
      <p class="hero-tagline">Building things for the web — <em>one commit at a time.</em></p>
      <div class="badge-row">
        <span class="badge badge-green">⬡ Open to Collaborate</span>
        <span class="badge badge-blue">📍 India</span>
        <span class="badge badge-amber">⚙ Python · React · Next.js · Firebase</span>
      </div>
    </div>

    <!-- About -->
    <div class="divider"><div class="divider-line"></div><div class="divider-label">about</div><div class="divider-line" style="background:linear-gradient(90deg,transparent,rgba(29,158,117,0.4))"></div></div>

    <div class="about-grid">
      <div class="about-card ac-green">
        <div class="about-card-icon">🔭</div>
        <div class="about-card-title">Currently</div>
        <div class="about-card-val">Honing Python skills</div>
      </div>
      <div class="about-card ac-blue">
        <div class="about-card-icon">💬</div>
        <div class="about-card-title">Ask me about</div>
        <div class="about-card-val">Python · JS · React · Firebase</div>
      </div>
      <div class="about-card ac-amber">
        <div class="about-card-icon">💡</div>
        <div class="about-card-title">Got a question?</div>
        <div class="about-card-val"><a href="https://github.com/arshad-muhammad/arshad-muhammad/issues" style="color:#EF9F27;text-decoration:none;">Let's talk →</a></div>
      </div>
      <div class="about-card ac-pink">
        <div class="about-card-icon">⚡</div>
        <div class="about-card-title">Motto</div>
        <div class="about-card-val">Dream Big, Think Bigger</div>
      </div>
    </div>

    <!-- Connect -->
    <div class="section-head">connect</div>
    <div class="connect-row">
      <a href="mailto:muhd.arshadra@gmail.com" class="social-btn">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="4" width="20" height="16" rx="2"></rect><path d="M2 7l10 7 10-7"></path></svg>
        Gmail
      </a>
      <a href="https://linkedin.com/in/hy-arshad" class="social-btn">
        <svg viewBox="0 0 24 24" fill="currentColor"><path d="M16 8a6 6 0 016 6v7h-4v-7a2 2 0 00-2-2 2 2 0 00-2 2v7h-4v-7a6 6 0 016-6zM2 9h4v12H2z"></path><circle cx="4" cy="4" r="2"></circle></svg>
        LinkedIn
      </a>
      <a href="https://instagram.com/arshadx0/" class="social-btn">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><rect x="2" y="2" width="20" height="20" rx="5"></rect><circle cx="12" cy="12" r="5"></circle><circle cx="17.5" cy="6.5" r="0.5" fill="currentColor"></circle></svg>
        Instagram
      </a>
      <a href="https://arshad-muhammad.github.io" class="social-btn">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path d="M3 12L12 3l9 9M5 10v9a1 1 0 001 1h4v-5h4v5h4a1 1 0 001-1v-9"></path></svg>
        Portfolio
      </a>
    </div>

    <!-- Stack -->
    <div class="stack-section">
      <div class="section-head">stack &amp; tools</div>
      <div class="stack-icons">
        <div class="tech-pill"><div class="tech-dot" style="background:#3572A5;"></div>Python</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#F7DF1E;"></div>JavaScript</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#61DAFB;"></div>React</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#fff;"></div>Next.js</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#FFCA28;"></div>Firebase</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#E34F26;"></div>HTML</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#1572B6;"></div>CSS</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#38B2AC;"></div>Tailwind</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#F24E1E;"></div>Figma</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#F05032;"></div>Git</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#fff;"></div>GitHub</div>
        <div class="tech-pill"><div class="tech-dot" style="background:#007ACC;"></div>VS Code</div>
      </div>
      <p style="font-family:'JetBrains Mono',monospace;font-size:12px;color:rgba(255,255,255,0.3);margin-top:10px;">🐍 <strong style="color:rgba(255,255,255,0.6)">Python</strong> and ⚛️ <strong style="color:rgba(255,255,255,0.6)">React.js</strong> are my primary weapons of choice.</p>
    </div>

    <!-- Stats -->
    <div class="stats-section">
      <div class="section-head">github stats</div>
      <div class="stats-embed">
        <div class="stat-row-item">
          <div class="stat-label">Commits</div>
          <div class="stat-bar-wrap"><div class="stat-bar" style="--w:82%;background:#1D9E75;"></div></div>
          <div class="stat-val" style="color:#1D9E75;">82%</div>
        </div>
        <div class="stat-row-item">
          <div class="stat-label">PRs</div>
          <div class="stat-bar-wrap"><div class="stat-bar" style="--w:54%;background:#378ADD;animation-delay:0.1s;"></div></div>
          <div class="stat-val" style="color:#378ADD;">54%</div>
        </div>
        <div class="stat-row-item">
          <div class="stat-label">Issues</div>
          <div class="stat-bar-wrap"><div class="stat-bar" style="--w:38%;background:#EF9F27;animation-delay:0.2s;"></div></div>
          <div class="stat-val" style="color:#EF9F27;">38%</div>
        </div>
        <div class="stat-row-item">
          <div class="stat-label">Reviews</div>
          <div class="stat-bar-wrap"><div class="stat-bar" style="--w:24%;background:#D4537E;animation-delay:0.3s;"></div></div>
          <div class="stat-val" style="color:#D4537E;">24%</div>
        </div>
      </div>

      <div class="streak-block" style="margin-top:10px;">
        <div>
          <div class="streak-num">42<span>days</span></div>
          <div class="streak-label">Current Streak 🔥</div>
        </div>
        <div style="text-align:right;">
          <div style="font-size:11px;font-family:'JetBrains Mono',monospace;color:rgba(255,255,255,0.25);text-transform:uppercase;letter-spacing:0.1em;">Longest</div>
          <div style="font-size:22px;font-weight:800;color:rgba(255,255,255,0.5);margin-top:2px;">68<span style="font-size:12px;font-weight:400;color:rgba(255,255,255,0.25);margin-left:3px;font-family:'JetBrains Mono',monospace;">days</span></div>
        </div>
      </div>

      <!-- Activity grid -->
      <div style="margin-top:16px;">
        <div class="section-head" style="margin-bottom:8px;">activity</div>
        <div class="activity-grid" id="actGrid"><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgb(29, 158, 117);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.3);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.75);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.5);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(29, 158, 117, 0.15);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div><div class="act-dot" style="background: rgba(255, 255, 255, 0.04);"></div></div>
      </div>
    </div>

    <!-- Footer -->
    <div class="profile-footer">
      <div class="footer-credit">crafted with <em>&lt;/&gt;</em> by arshad-muhammad</div>
      <div style="font-family:'JetBrains Mono',monospace;font-size:10px;color:rgba(255,255,255,0.15);letter-spacing:0.08em;">v2.0.0</div>
    </div>

  </div>
</div>

<script>
  const grid = document.getElementById('actGrid');
  const levels = [0,0,0,0.05,0.08,0.15,0.3,0.5,0.7,1];
  const colors = ['rgba(255,255,255,0.04)','rgba(29,158,117,0.15)','rgba(29,158,117,0.3)','rgba(29,158,117,0.5)','rgba(29,158,117,0.75)','rgba(29,158,117,1)'];
  for(let i=0;i<182;i++){
    const d=document.createElement('div');
    d.className='act-dot';
    const r=Math.random();
    let c;
    if(r<0.4)c=colors[0];
    else if(r<0.6)c=colors[1];
    else if(r<0.75)c=colors[2];
    else if(r<0.88)c=colors[3];
    else if(r<0.96)c=colors[4];
    else c=colors[5];
    d.style.background=c;
    grid.appendChild(d);
  }
</script>
</body></html>
