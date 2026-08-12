<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Suvani Waghmare — the enchanted garden</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,500;0,9..144,600;0,9..144,700;1,9..144,500&family=Manrope:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --void:#0a0714;
    --dusk:#150d24;
    --panel:#1d1330;
    --panel-2:#251a3d;
    --hair:#3a2b56;
    --lilac:#c9a3ff;
    --rose:#ff9dcb;
    --gold:#f0c96b;
    --mist:#f3ecff;
    --mist-dim:#a897c7;
    --font-display:'Fraunces', serif;
    --font-body:'Manrope', sans-serif;
    --font-mono:'JetBrains Mono', monospace;
    --radius:18px;
    --dur:.6s;
  }

  body.terminal{
    --void:#050806;
    --dusk:#0a120c;
    --panel:#0e1a10;
    --panel-2:#122015;
    --hair:#1f4a2c;
    --lilac:#7CFC9A;
    --rose:#7CFC9A;
    --gold:#ffcf7a;
    --mist:#d8ffe4;
    --mist-dim:#5f9a72;
  }

  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--void);
    color:var(--mist);
    font-family:var(--font-body);
    overflow-x:hidden;
    transition:background var(--dur) ease, color var(--dur) ease;
    position:relative;
  }
  body.terminal{font-family:var(--font-mono);}

  ::selection{background:var(--lilac); color:var(--void);}

  a{color:inherit; text-decoration:none;}

  /* ---------- Ambient background ---------- */
  #ambient{
    position:fixed; inset:0; z-index:0; pointer-events:none; overflow:hidden;
  }
  .firefly{
    position:absolute; width:4px; height:4px; border-radius:50%;
    background:var(--gold);
    box-shadow:0 0 8px 2px var(--gold);
    animation:drift linear infinite, glow 3s ease-in-out infinite;
    opacity:.7;
  }
  body.terminal .firefly{ box-shadow:0 0 6px 1px var(--gold); }
  @keyframes glow{ 0%,100%{opacity:.25;} 50%{opacity:.9;} }
  @keyframes drift{
    0%{ transform:translateY(0) translateX(0); }
    50%{ transform:translateY(-40px) translateX(20px); }
    100%{ transform:translateY(0) translateX(0); }
  }
  .butterfly{
    position:absolute; font-size:22px; opacity:.5; filter:saturate(1.1);
    animation:flutter 18s ease-in-out infinite;
  }
  body.terminal .butterfly{ opacity:0; }
  @keyframes flutter{
    0%{ transform:translate(0,0) rotate(0deg); }
    25%{ transform:translate(60px,-80px) rotate(10deg); }
    50%{ transform:translate(120px,10px) rotate(-8deg); }
    75%{ transform:translate(50px,90px) rotate(6deg); }
    100%{ transform:translate(0,0) rotate(0deg); }
  }
  .scanline{
    position:absolute; inset:0; opacity:0;
    background:repeating-linear-gradient(0deg, rgba(124,252,154,.05) 0px, rgba(124,252,154,.05) 1px, transparent 1px, transparent 3px);
    transition:opacity var(--dur) ease;
  }
  body.terminal .scanline{ opacity:1; }

  /* ---------- Layout helpers ---------- */
  .wrap{ max-width:1080px; margin:0 auto; padding:0 28px; position:relative; z-index:2;}
  section{ padding:120px 0; position:relative; }
  .eyebrow{
    font-family:var(--font-mono); font-size:12px; letter-spacing:.28em; text-transform:uppercase;
    color:var(--rose); margin-bottom:18px; display:flex; align-items:center; gap:10px;
  }
  .eyebrow::before{ content:''; width:26px; height:1px; background:var(--rose); display:inline-block;}
  h2.title{
    font-family:var(--font-display); font-weight:600; font-size:clamp(28px,4vw,44px);
    letter-spacing:-.01em; margin-bottom:20px; color:var(--mist);
  }
  body.terminal h2.title{ font-family:var(--font-mono); font-weight:700; }
  p.lede{ color:var(--mist-dim); font-size:17px; line-height:1.7; max-width:640px; }

  /* ---------- Nav ---------- */
  nav{
    position:fixed; top:0; left:0; right:0; z-index:50;
    backdrop-filter:blur(14px); background:rgba(10,7,20,.55);
    border-bottom:1px solid var(--hair);
    transition:background var(--dur) ease, border-color var(--dur) ease;
  }
  body.terminal nav{ background:rgba(5,8,6,.7); }
  .navbar{
    max-width:1080px; margin:0 auto; padding:16px 28px;
    display:flex; align-items:center; justify-content:space-between;
  }
  .brand{ font-family:var(--font-display); font-weight:700; font-size:19px; letter-spacing:.02em; }
  body.terminal .brand{ font-family:var(--font-mono); }
  .brand span{ color:var(--lilac); }
  .navlinks{ display:flex; gap:26px; font-size:13.5px; }
  .navlinks a{ color:var(--mist-dim); transition:color .25s ease; position:relative; }
  .navlinks a:hover{ color:var(--mist); }
  .mode-toggle{
    display:flex; align-items:center; gap:8px; font-size:12px; letter-spacing:.05em;
    background:var(--panel); border:1px solid var(--hair); padding:7px 14px; border-radius:999px;
    cursor:pointer; color:var(--mist); font-family:var(--font-mono); transition:all .3s ease;
  }
  .mode-toggle:hover{ border-color:var(--lilac); }
  @media (max-width:760px){ .navlinks{ display:none; } }

  /* ---------- Hero ---------- */
  #home{
    min-height:100vh; display:flex; flex-direction:column; align-items:center; justify-content:center;
    text-align:center; padding-top:100px;
  }
  .hero-kicker{
    font-family:var(--font-mono); font-size:13px; letter-spacing:.3em; text-transform:uppercase;
    color:var(--gold); margin-bottom:28px; opacity:.9;
  }
  h1.hero-title{
    font-family:var(--font-display); font-weight:600; font-size:clamp(46px,9vw,104px);
    line-height:.98; letter-spacing:-.02em; color:var(--mist);
    background:linear-gradient(180deg, var(--mist), var(--lilac) 140%);
    -webkit-background-clip:text; background-clip:text; -webkit-text-fill-color:transparent;
  }
  body.terminal h1.hero-title{ font-family:var(--font-mono); font-weight:700; background:none; -webkit-text-fill-color:var(--lilac); }
  .hero-sub{
    margin-top:26px; font-size:clamp(16px,2.2vw,21px); color:var(--mist-dim);
    font-family:var(--font-mono); min-height:32px;
  }
  .hero-sub .cursor{ display:inline-block; width:2px; background:var(--rose); margin-left:2px; animation:blink 1s steps(1) infinite; }
  @keyframes blink{ 50%{opacity:0;} }
  .hero-cta{ margin-top:44px; display:flex; gap:16px; flex-wrap:wrap; justify-content:center; }
  .btn{
    padding:13px 28px; border-radius:999px; font-size:14px; font-weight:700;
    font-family:var(--font-body); cursor:pointer; transition:transform .25s ease, box-shadow .25s ease;
    display:inline-flex; align-items:center; gap:8px; border:1px solid transparent;
  }
  body.terminal .btn{ font-family:var(--font-mono); border-radius:6px; }
  .btn-primary{ background:linear-gradient(135deg, var(--lilac), var(--rose)); color:var(--void); }
  body.terminal .btn-primary{ background:var(--lilac); color:#04120a; }
  .btn-ghost{ border-color:var(--hair); color:var(--mist); }
  .btn:hover{ transform:translateY(-2px); box-shadow:0 10px 30px -10px var(--lilac); }
  .scroll-hint{ margin-top:70px; font-size:22px; color:var(--mist-dim); animation:bob 2.4s ease-in-out infinite; }
  @keyframes bob{ 0%,100%{transform:translateY(0);} 50%{transform:translateY(8px);} }

  /* ---------- About / duality ---------- */
  .duality{ display:grid; grid-template-columns:1fr auto 1fr; gap:0; margin-top:56px; align-items:stretch; }
  .duality-col{ background:var(--panel); border:1px solid var(--hair); padding:36px 30px; }
  .duality-col:first-child{ border-radius:var(--radius) 0 0 var(--radius); }
  .duality-col:last-child{ border-radius:0 var(--radius) var(--radius) 0; }
  .duality-divider{ width:1px; background:linear-gradient(180deg, transparent, var(--hair) 20%, var(--hair) 80%, transparent); position:relative; }
  .duality-divider::after{
    content:'✦'; position:absolute; top:50%; left:50%; transform:translate(-50%,-50%);
    background:var(--void); padding:8px; color:var(--rose); font-size:14px;
  }
  .duality-col h3{ font-family:var(--font-display); font-size:22px; margin-bottom:14px; color:var(--lilac); }
  body.terminal .duality-col h3{ font-family:var(--font-mono); }
  .duality-col ul{ list-style:none; }
  .duality-col li{ color:var(--mist-dim); font-size:14.5px; padding:6px 0; display:flex; gap:10px; }
  .duality-col li::before{ content:'—'; color:var(--rose); }
  @media (max-width:700px){ .duality{ grid-template-columns:1fr; } .duality-divider{ display:none;} .duality-col{ border-radius:var(--radius) !important; margin-bottom:2px; } }

  .pull-quote{
    font-family:var(--font-display); font-style:italic; font-size:clamp(20px,2.6vw,28px);
    text-align:center; max-width:680px; margin:60px auto 0; color:var(--mist); line-height:1.5;
  }
  body.terminal .pull-quote{ font-family:var(--font-mono); font-style:normal; }
  .pull-quote span{ color:var(--gold); }

  /* ---------- Skills / vines ---------- */
  .skill-row{ margin-bottom:26px; }
  .skill-head{ display:flex; justify-content:space-between; font-size:14px; margin-bottom:8px; font-family:var(--font-mono); }
  .skill-head .label{ color:var(--mist); font-weight:600; }
  .skill-head .tag{ color:var(--mist-dim); }
  .track{ height:9px; border-radius:999px; background:var(--panel-2); border:1px solid var(--hair); overflow:hidden; }
  .fill{
    height:100%; width:0%; border-radius:999px;
    background:linear-gradient(90deg, var(--rose), var(--lilac));
    transition:width 1.4s cubic-bezier(.16,1,.3,1);
  }
  body.terminal .fill{ background:var(--lilac); }

  .icon-cluster{ display:flex; flex-wrap:wrap; gap:14px; margin-top:18px; }
  .icon-pill{
    background:var(--panel); border:1px solid var(--hair); border-radius:14px; padding:14px 18px;
    display:flex; align-items:center; gap:10px; font-size:13px; color:var(--mist-dim);
    transition:transform .25s ease, border-color .25s ease;
  }
  .icon-pill:hover{ transform:translateY(-3px); border-color:var(--lilac); color:var(--mist); }
  .icon-pill img{ height:20px; }

  .grid2{ display:grid; grid-template-columns:1fr 1fr; gap:60px; margin-top:20px;}
  @media (max-width:760px){ .grid2{ grid-template-columns:1fr; gap:40px;} }

  /* ---------- Projects ---------- */
  .card-grid{ display:grid; grid-template-columns:repeat(2,1fr); gap:20px; margin-top:40px; }
  @media (max-width:700px){ .card-grid{ grid-template-columns:1fr; } }
  .proj-card{
    background:var(--panel); border:1px solid var(--hair); border-radius:var(--radius); padding:30px;
    transition:transform .3s ease, border-color .3s ease, background .3s ease;
    position:relative; overflow:hidden;
  }
  .proj-card:hover{ transform:translateY(-6px); border-color:var(--lilac); }
  .proj-card .num{ font-family:var(--font-mono); font-size:12px; color:var(--gold); letter-spacing:.15em; }
  .proj-card h3{ font-family:var(--font-display); font-size:21px; margin:10px 0 10px; color:var(--mist); }
  body.terminal .proj-card h3{ font-family:var(--font-mono); }
  .proj-card p{ color:var(--mist-dim); font-size:14px; line-height:1.6; }

  /* ---------- Terminal card (Suvani.exe) ---------- */
  .term-card{
    background:#0c0716; border:1px solid var(--hair); border-radius:14px; overflow:hidden;
    font-family:var(--font-mono); max-width:640px; margin:44px auto 0;
    box-shadow:0 30px 60px -30px rgba(0,0,0,.6);
  }
  body.terminal .term-card{ background:#050a06; }
  .term-bar{ display:flex; gap:8px; padding:12px 16px; background:var(--panel-2); border-bottom:1px solid var(--hair); }
  .term-dot{ width:11px; height:11px; border-radius:50%; }
  .term-body{ padding:22px 24px; font-size:13.5px; line-height:1.9; color:var(--lilac); }
  .term-body .comment{ color:var(--mist-dim); }
  .term-body .key{ color:var(--rose); }
  .term-body .val{ color:var(--mist); }
  .barmini{ display:inline-block; width:140px; height:8px; background:var(--panel-2); border-radius:4px; overflow:hidden; vertical-align:middle; margin-left:8px;}
  .barmini i{ display:block; height:100%; background:linear-gradient(90deg,var(--rose),var(--lilac)); width:0%; transition:width 1.2s ease;}
  body.terminal .barmini i{ background:var(--lilac); }

  /* ---------- Writing ---------- */
  .writing-banner{
    background:linear-gradient(135deg, var(--panel), var(--panel-2));
    border:1px solid var(--hair); border-radius:24px; padding:60px 46px; text-align:center; margin-top:40px;
    position:relative;
  }
  .stat-big{ font-family:var(--font-display); font-size:clamp(48px,7vw,80px); color:var(--gold); line-height:1; }
  body.terminal .stat-big{ font-family:var(--font-mono); }
  .stat-cap{ font-size:13px; letter-spacing:.2em; text-transform:uppercase; color:var(--mist-dim); margin-top:10px; }
  .tag-row{ display:flex; gap:10px; flex-wrap:wrap; justify-content:center; margin-top:26px; }
  .tag{ border:1px solid var(--hair); padding:7px 16px; border-radius:999px; font-size:12.5px; color:var(--mist-dim); font-family:var(--font-mono); }

  /* ---------- Journey timeline ---------- */
  .timeline{ position:relative; margin-top:50px; padding-left:32px; }
  .timeline::before{ content:''; position:absolute; left:6px; top:6px; bottom:6px; width:2px; background:linear-gradient(180deg, var(--rose), var(--lilac)); }
  .tl-item{ position:relative; padding-bottom:38px; }
  .tl-item:last-child{ padding-bottom:0; }
  .tl-item::before{
    content:''; position:absolute; left:-32px; top:2px; width:14px; height:14px; border-radius:50%;
    background:var(--void); border:2px solid var(--lilac);
  }
  .tl-item.next::before{ background:var(--gold); border-color:var(--gold); }
  .tl-item .step{ font-family:var(--font-mono); font-size:11px; color:var(--rose); letter-spacing:.15em; }
  .tl-item h4{ font-family:var(--font-display); font-size:19px; margin:4px 0 4px; color:var(--mist); }
  body.terminal .tl-item h4{ font-family:var(--font-mono); }
  .tl-item p{ color:var(--mist-dim); font-size:14px; }

  /* ---------- Mission ---------- */
  .mission-grid{ display:grid; grid-template-columns:repeat(4,1fr); gap:14px; margin-top:36px; }
  @media (max-width:760px){ .mission-grid{ grid-template-columns:repeat(2,1fr); } }
  .mission-item{
    border:1px solid var(--hair); border-radius:14px; padding:22px 16px; text-align:center;
    background:var(--panel); font-size:13px; color:var(--mist-dim); cursor:default; transition:.25s ease;
  }
  .mission-item:hover{ border-color:var(--gold); color:var(--mist); transform:translateY(-3px); }
  .mission-item .em{ font-size:24px; display:block; margin-bottom:10px; }

  /* ---------- Stats / night sky ---------- */
  .stat-frame{ border:1px solid var(--hair); border-radius:18px; overflow:hidden; margin-top:26px; background:var(--panel); }
  .stat-frame img{ width:100%; display:block; }
  .stat-frame-row{ display:grid; grid-template-columns:1fr 1fr; gap:18px; margin-top:18px; }
  @media (max-width:700px){ .stat-frame-row{ grid-template-columns:1fr; } }

  /* ---------- Connect ---------- */
  .connect-grid{ display:grid; grid-template-columns:repeat(3,1fr); gap:14px; margin-top:40px; }
  @media (max-width:760px){ .connect-grid{ grid-template-columns:repeat(2,1fr); } }
  @media (max-width:480px){ .connect-grid{ grid-template-columns:1fr; } }
  .connect-link{
    border:1px solid var(--hair); border-radius:14px; padding:20px; background:var(--panel);
    display:flex; align-items:center; gap:12px; transition:.25s ease; font-size:14px; font-weight:600;
  }
  .connect-link:hover{ border-color:var(--lilac); transform:translateY(-3px); background:var(--panel-2); }
  .connect-link .dot{ width:8px; height:8px; border-radius:50%; background:var(--rose); flex-shrink:0; }

  footer{ text-align:center; padding:70px 0 40px; color:var(--mist-dim); font-family:var(--font-mono); font-size:13px; }
  footer .fline{ margin-bottom:10px; letter-spacing:.15em; color:var(--gold); }

  .reveal{ opacity:0; transform:translateY(28px); transition:opacity .8s ease, transform .8s ease; }
  .reveal.in{ opacity:1; transform:translateY(0); }

  @media (prefers-reduced-motion: reduce){
    *{ animation:none !important; transition:none !important; }
  }
</style>
</head>
<body>

<div id="ambient">
  <div class="scanline"></div>
</div>

<nav>
  <div class="navbar">
    <div class="brand">suvani<span>.</span>garden</div>
    <div class="navlinks">
      <a href="#about">about</a>
      <a href="#skills">skills</a>
      <a href="#projects">projects</a>
      <a href="#journey">journey</a>
      <a href="#writing">writing</a>
      <a href="#connect">connect</a>
    </div>
    <div class="mode-toggle" id="modeToggle">
      <span id="modeIcon">🦋</span>
      <span id="modeLabel">garden mode</span>
    </div>
  </div>
</nav>

<!-- HERO -->
<section id="home">
  <div class="wrap">
    <div class="hero-kicker">CSE student · builder · storyteller</div>
    <h1 class="hero-title">Suvani<br>Waghmare</h1>
    <div class="hero-sub"><span id="typedText"></span><span class="cursor">&nbsp;</span></div>
    <div class="hero-cta">
      <a class="btn btn-primary" href="#projects">see what I'm building</a>
      <a class="btn btn-ghost" href="#connect">say hello</a>
    </div>
    <div class="scroll-hint">↓</div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="wrap">
    <div class="eyebrow">about</div>
    <h2 class="title">Somewhere between a terminal<br>and a fairytale</h2>
    <p class="lede">I'm a CSE student who lives in two worlds at once — one where problems get solved with logic, and one where entire worlds get built out of a single sentence. Most days, I'm doing both before lunch.</p>

    <div class="duality reveal">
      <div class="duality-col">
        <h3>🐍 the coder</h3>
        <ul>
          <li>Learning Python, DSA & Java</li>
          <li>Exploring Data Science & Machine Learning</li>
          <li>Building small, practical web projects</li>
          <li>Believes a project doesn't have to be huge to be worth building</li>
        </ul>
      </div>
      <div class="duality-divider"></div>
      <div class="duality-col">
        <h3>🦋 the storyteller</h3>
        <ul>
          <li>Writes fiction, characters, and entire worlds</li>
          <li>Can turn one random idea into a full story</li>
          <li>Averages 20+ stories a month</li>
          <li>Has more late-night commits than she'd like to admit</li>
        </ul>
      </div>
    </div>

    <p class="pull-quote">"Code gives me <span>problems to solve.</span><br>Writing gives me <span>worlds to create.</span>"</p>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="wrap">
    <div class="eyebrow">skills</div>
    <h2 class="title">My tech universe</h2>
    <p class="lede">What's growing in the garden right now — tracked honestly, not inflated.</p>

    <div class="grid2">
      <div>
        <div class="skill-row" data-pct="72">
          <div class="skill-head"><span class="label">Python</span><span class="tag">learning</span></div>
          <div class="track"><div class="fill"></div></div>
        </div>
        <div class="skill-row" data-pct="60">
          <div class="skill-head"><span class="label">DSA</span><span class="tag">grinding</span></div>
          <div class="track"><div class="fill"></div></div>
        </div>
        <div class="skill-row" data-pct="42">
          <div class="skill-head"><span class="label">Machine Learning</span><span class="tag">exploring</span></div>
          <div class="track"><div class="fill"></div></div>
        </div>
        <div class="skill-row" data-pct="52">
          <div class="skill-head"><span class="label">Web Development</span><span class="tag">building</span></div>
          <div class="track"><div class="fill"></div></div>
        </div>
        <div class="skill-row" data-pct="92">
          <div class="skill-head"><span class="label">Writing</span><span class="tag">dangerous</span></div>
          <div class="track"><div class="fill"></div></div>
        </div>
      </div>
      <div>
        <h3 style="font-family:var(--font-display); font-size:18px; margin-bottom:14px; color:var(--mist);">languages &amp; tools</h3>
        <div class="icon-cluster">
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=python" alt="Python">Python</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=java" alt="Java">Java</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=c" alt="C">C</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=js" alt="JavaScript">JavaScript</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=html" alt="HTML">HTML</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=css" alt="CSS">CSS</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=git" alt="Git">Git</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=github" alt="GitHub">GitHub</div>
          <div class="icon-pill"><img src="https://skillicons.dev/icons?i=vscode" alt="VS Code">VS Code</div>
        </div>
        <h3 style="font-family:var(--font-display); font-size:18px; margin:26px 0 14px; color:var(--mist);">data &amp; ai</h3>
        <div class="icon-cluster">
          <div class="icon-pill">Pandas</div>
          <div class="icon-pill">NumPy</div>
          <div class="icon-pill">Scikit-learn</div>
          <div class="icon-pill">DBMS</div>
          <div class="icon-pill">OOP</div>
        </div>
      </div>
    </div>

    <div class="term-card reveal">
      <div class="term-bar">
        <div class="term-dot" style="background:#ff5f57;"></div>
        <div class="term-dot" style="background:#febc2e;"></div>
        <div class="term-dot" style="background:#28c840;"></div>
      </div>
      <div class="term-body">
        <div class="comment">// suvani.exe — status check</div>
        <div><span class="key">class</span>&nbsp; <span class="val">Data Scientist in Progress</span></div>
        <div><span class="key">second</span> <span class="val">Professional Storyteller</span></div>
        <div style="margin-top:10px;">python&nbsp;&nbsp;<span class="barmini" data-pct="72"><i></i></span></div>
        <div>dsa&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="barmini" data-pct="60"><i></i></span></div>
        <div>ml&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="barmini" data-pct="42"><i></i></span></div>
        <div>writing&nbsp;<span class="barmini" data-pct="92"><i></i></span></div>
        <div style="margin-top:10px;"><span class="key">status</span>&nbsp; <span class="val">online ☕</span></div>
        <div><span class="key">bug</span>&nbsp;&nbsp;&nbsp; <span class="comment">"it worked yesterday."</span></div>
      </div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="wrap">
    <div class="eyebrow">projects</div>
    <h2 class="title">Every project begins with a tiny question — <em style="font-style:italic; color:var(--lilac);">"what if I tried this?"</em></h2>
    <div class="card-grid">
      <div class="proj-card">
        <div class="num">01 · data science</div>
        <h3>🧪 Exploring datasets</h3>
        <p>Analysis, visualization, and small machine-learning experiments built while learning the fundamentals.</p>
      </div>
      <div class="proj-card">
        <div class="num">02 · coding</div>
        <h3>💻 Practical builds</h3>
        <p>Small experiments and practical projects, built one concept at a time as new tools get learned.</p>
      </div>
      <div class="proj-card">
        <div class="num">03 · dsa</div>
        <h3>🧩 Problem solving</h3>
        <p>Strengthening algorithmic thinking — one problem, one pattern, one "aha" at a time.</p>
      </div>
      <div class="proj-card">
        <div class="num">04 · creative</div>
        <h3>✍️ Worlds on paper</h3>
        <p>Writing, storytelling, and digital content — the other half of the garden, just as alive.</p>
      </div>
    </div>
  </div>
</section>

<!-- WRITING -->
<section id="writing">
  <div class="wrap">
    <div class="eyebrow">the writer's garden</div>
    <h2 class="title">Yes, I code. But I also write.</h2>
    <p class="lede">Outside the terminal, there's a whole other practice — characters, emotions, and worlds built from nothing but an idea.</p>
    <div class="writing-banner reveal">
      <div class="stat-big" id="storyCount">0</div>
      <div class="stat-cap">stories written in a month</div>
      <div class="tag-row">
        <div class="tag">fiction</div>
        <div class="tag">storytelling</div>
        <div class="tag">creative writing</div>
        <div class="tag">content writing</div>
      </div>
      <p style="margin-top:22px; color:var(--mist-dim); font-size:13px; font-family:var(--font-mono);">apparently my imagination doesn't believe in office hours 🦋</p>
    </div>
  </div>
</section>

<!-- JOURNEY -->
<section id="journey">
  <div class="wrap">
    <div class="eyebrow">journey</div>
    <h2 class="title">The path so far</h2>
    <div class="timeline">
      <div class="tl-item"><div class="step">STEP 01</div><h4>🌱 Started coding</h4><p>The first line, the first bug, the first "it works!"</p></div>
      <div class="tl-item"><div class="step">STEP 02</div><h4>💻 Started building</h4><p>Turning tutorials into actual, if small, projects.</p></div>
      <div class="tl-item"><div class="step">STEP 03</div><h4>🧩 Discovered DSA</h4><p>Where logic stopped being abstract and started being a skill.</p></div>
      <div class="tl-item"><div class="step">STEP 04</div><h4>📊 Fell into data</h4><p>Datasets, patterns, and the pull toward data science.</p></div>
      <div class="tl-item"><div class="step">STEP 05</div><h4>🤖 Explored ML</h4><p>Still early, still curious, still asking "how does this actually work?"</p></div>
      <div class="tl-item"><div class="step">STEP 06</div><h4>🚀 Built more</h4><p>More projects, more late nights, more commits.</p></div>
      <div class="tl-item"><div class="step">STEP 07</div><h4>🌙 Still learning</h4><p>Because the garden is never really finished.</p></div>
      <div class="tl-item next"><div class="step">NEXT</div><h4>Build something amazing</h4><p>The next chapter — still being written.</p></div>
    </div>
  </div>
</section>

<!-- MISSION -->
<section id="mission">
  <div class="wrap">
    <div class="eyebrow">2026 mission</div>
    <h2 class="title">One step at a time. One project at a time.</h2>
    <div class="mission-grid">
      <div class="mission-item"><span class="em">🐍</span>Master Python</div>
      <div class="mission-item"><span class="em">🧩</span>Level up DSA</div>
      <div class="mission-item"><span class="em">🤖</span>Learn ML</div>
      <div class="mission-item"><span class="em">🚀</span>Build projects</div>
      <div class="mission-item"><span class="em">🏆</span>Join hackathons</div>
      <div class="mission-item"><span class="em">💼</span>Find opportunities</div>
      <div class="mission-item"><span class="em">📚</span>Keep learning</div>
      <div class="mission-item"><span class="em">✍️</span>Keep writing</div>
    </div>
  </div>
</section>

<!-- STATS -->
<section id="stats">
  <div class="wrap">
    <div class="eyebrow">the night sky</div>
    <h2 class="title">Contribution garden</h2>
    <div class="stat-frame"><img src="https://github-readme-streak-stats.herokuapp.com?user=suvaniwaghmare085-droid&theme=tokyonight&hide_border=true&background=0D1117&ring=FF8FC7&fire=FF8FC7&currStreakLabel=E8C7FF" alt="streak stats" loading="lazy"></div>
    <div class="stat-frame-row">
      <div class="stat-frame"><img src="https://leetcard.jacoblin.cool/Suvani_12?theme=dark&font=Fira%20Code&ext=heatmap" alt="leetcode card" loading="lazy"></div>
      <div class="stat-frame"><img src="https://github-readme-stats.vercel.app/api/top-langs/?username=suvaniwaghmare085-droid&layout=donut&theme=tokyonight&hide_border=true&langs_count=8" alt="top languages" loading="lazy"></div>
    </div>
  </div>
</section>

<!-- CONNECT -->
<section id="connect">
  <div class="wrap">
    <div class="eyebrow">connect</div>
    <h2 class="title">If you're building something interesting, come say hello 🦋</h2>
    <p class="lede">Open to collaborations, project ideas, hackathons, opportunities, and learning together.</p>
    <div class="connect-grid">
      <a class="connect-link" href="https://www.linkedin.com/in/suvani-waghmare-4a0949379" target="_blank"><span class="dot"></span>LinkedIn</a>
      <a class="connect-link" href="https://leetcode.com/u/Suvani_12/" target="_blank"><span class="dot"></span>LeetCode</a>
      <a class="connect-link" href="https://www.hackerrank.com/profile/suvaniwaghmare01" target="_blank"><span class="dot"></span>HackerRank</a>
      <a class="connect-link" href="https://www.codechef.com/users/suvani_12" target="_blank"><span class="dot"></span>CodeChef</a>
      <a class="connect-link" href="https://www.geeksforgeeks.org/profile/suvani12" target="_blank"><span class="dot"></span>GeeksforGeeks</a>
      <a class="connect-link" href="https://medium.com/@suvaniwaghmare02" target="_blank"><span class="dot"></span>Medium</a>
      <a class="connect-link" href="https://hashnode.com/@suvani12" target="_blank"><span class="dot"></span>Hashnode</a>
      <a class="connect-link" href="https://www.hackerearth.com/suvaniwaghmare02" target="_blank"><span class="dot"></span>HackerEarth</a>
    </div>
  </div>
</section>

<footer>
  <div class="fline">🦋 ✦ 🌙 ✦ 🦋</div>
  <div>building quietly, dreaming loudly.</div>
  <div style="margin-top:6px; opacity:.6;">code · create · learn · repeat</div>
</footer>

<script>
  // ambient fireflies + butterflies
  const ambient = document.getElementById('ambient');
  for(let i=0;i<26;i++){
    const f = document.createElement('div');
    f.className='firefly';
    f.style.left = Math.random()*100+'vw';
    f.style.top = Math.random()*100+'vh';
    f.style.animationDuration = (6+Math.random()*8)+'s, '+(2+Math.random()*3)+'s';
    f.style.animationDelay = (Math.random()*5)+'s';
    ambient.appendChild(f);
  }
  const butterflies = ['🦋','🦋','🦋','🦋','🦋'];
  butterflies.forEach((b,i)=>{
    const el = document.createElement('div');
    el.className='butterfly';
    el.textContent=b;
    el.style.left = (10+i*20)+'vw';
    el.style.top = (10+Math.random()*70)+'vh';
    el.style.animationDuration = (14+Math.random()*10)+'s';
    el.style.animationDelay = (Math.random()*6)+'s';
    ambient.appendChild(el);
  });

  // typewriter
  const lines = [
    "Welcome to my little digital garden.",
    "I turn ideas into code.",
    "I turn characters into worlds.",
    "Learning Data Science, one problem at a time.",
    "Building quietly. Dreaming loudly."
  ];
  const typedEl = document.getElementById('typedText');
  let li=0, ci=0, deleting=false;
  function typeLoop(){
    const current = lines[li];
    if(!deleting){
      ci++;
      typedEl.textContent = current.slice(0,ci);
      if(ci===current.length){ deleting=true; setTimeout(typeLoop,1400); return; }
    } else {
      ci--;
      typedEl.textContent = current.slice(0,ci);
      if(ci===0){ deleting=false; li=(li+1)%lines.length; }
    }
    setTimeout(typeLoop, deleting?28:55);
  }
  typeLoop();

  // reveal on scroll
  const revealEls = document.querySelectorAll('.reveal');
  const io = new IntersectionObserver(entries=>{
    entries.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('in'); });
  },{threshold:.2});
  revealEls.forEach(el=>io.observe(el));

  // skill bars fill on view
  const skillRows = document.querySelectorAll('.skill-row');
  const barIo = new IntersectionObserver(entries=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        const pct = e.target.getAttribute('data-pct');
        e.target.querySelector('.fill').style.width = pct+'%';
        barIo.unobserve(e.target);
      }
    });
  },{threshold:.4});
  skillRows.forEach(el=>barIo.observe(el));

  const miniBars = document.querySelectorAll('.barmini');
  const miniIo = new IntersectionObserver(entries=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        e.target.querySelector('i').style.width = e.target.getAttribute('data-pct')+'%';
        miniIo.unobserve(e.target);
      }
    });
  },{threshold:.4});
  miniBars.forEach(el=>miniIo.observe(el));

  // story count-up
  const storyEl = document.getElementById('storyCount');
  let counted=false;
  const storyIo = new IntersectionObserver(entries=>{
    entries.forEach(e=>{
      if(e.isIntersecting && !counted){
        counted=true;
        let n=0;
        const target=22;
        const t=setInterval(()=>{
          n++; storyEl.textContent = n+'+';
          if(n>=target) clearInterval(t);
        },45);
      }
    });
  },{threshold:.5});
  storyIo.observe(storyEl);

  // mode toggle: garden <-> terminal
  const toggle = document.getElementById('modeToggle');
  const icon = document.getElementById('modeIcon');
  const label = document.getElementById('modeLabel');
  toggle.addEventListener('click', ()=>{
    const isTerminal = document.body.classList.toggle('terminal');
    icon.textContent = isTerminal ? '🌙' : '🦋';
    label.textContent = isTerminal ? 'terminal mode' : 'garden mode';
  });
</script>
</body>
</html>
