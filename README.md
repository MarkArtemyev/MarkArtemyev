<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover" />
<meta name="theme-color" content="#0c0015" />
<title>NEON // CYBER Showcase</title>
<style>
  /* -------------------- CSS RESET (короткий) -------------------- */
  *,*::before,*::after{box-sizing:border-box}
  html,body{height:100%}
  body{margin:0;background:#03010a;color:#e9e9ff;font-family:Inter,Segoe UI,Roboto,Helvetica,Arial,sans-serif;overflow-x:hidden}
  img,svg,canvas{max-width:100%;display:block}
  a{color:inherit;text-decoration:none}
  :root{
    --bg: #070312;
    --fg: #e5e9ff;
    --muted:#8f99ff;
    --neon1:#00e6ff;
    --neon2:#7a00ff;
    --neon3:#ff00e6;
    --neon4:#00ffa3;
    --glass: rgba(255,255,255,0.04);
    --border: rgba(255,255,255,0.10);
    --scanline: rgba(255,255,255,0.03);
    --glow: drop-shadow(0 0 10px rgba(0,230,255,.75)) drop-shadow(0 0 30px rgba(122,0,255,.35));
  }
  /* Alt theme (toggle) */
  body.theme-alt{
    --bg:#010610;
    --fg:#dff6ff;
    --muted:#89f0ff;
    --neon1:#ffea00;
    --neon2:#ff006c;
    --neon3:#00ffd5;
    --neon4:#7c4dff;
  }

  /* -------------------- GLOBAL BACKGROUNDS -------------------- */
  .backdrop {
    position:fixed; inset:0; z-index:-3;
    background:
      radial-gradient(1200px 600px at 20% 10%, rgba(122,0,255,.25), transparent 60%),
      radial-gradient(900px 500px at 80% 20%, rgba(0,230,255,.25), transparent 60%),
      radial-gradient(600px 800px at 50% 100%, rgba(255,0,180,.20), transparent 60%),
      linear-gradient(180deg, #04000a, var(--bg) 35%, #02000a);
    filter: saturate(110%) contrast(105%);
  }
  .scanlines::before{
    content:""; position:fixed; inset:0; z-index:-1;
    background: repeating-linear-gradient(
      to bottom, rgba(255,255,255,.03), rgba(255,255,255,.03) 1px,
      transparent 2px, transparent 3px
    );
    mix-blend-mode:soft-light; pointer-events:none; opacity:.35;
  }
  .noise::after{
    content:""; position:fixed; inset:0; z-index:-2; pointer-events:none; opacity:.07;
    background-image:url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="140" height="140" viewBox="0 0 140 140"><filter id="n"><feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2" stitchTiles="stitch"/></filter><rect width="100%" height="100%" filter="url(%23n)"/></svg>');
    background-size:240px 240px; mix-blend-mode:overlay;
  }

  /* -------------------- HEADER / GLITCH TITLE -------------------- */
  header{
    position:relative; padding:8rem 1rem 3rem; text-align:center;
  }
  .title-wrap{position:relative; display:inline-block}
  .title{
    font-size: clamp(2.6rem, 6vw, 6.2rem);
    letter-spacing:.06em; font-weight:900; line-height:1; margin:0;
    background:conic-gradient(from 180deg, var(--neon1), var(--neon2), var(--neon3), var(--neon4), var(--neon1));
    -webkit-background-clip:text; background-clip:text; color:transparent;
    filter: var(--glow);
  }
  .title-glitch{
    position:absolute; inset:0; color:transparent; pointer-events:none;
    -webkit-text-stroke:2px rgba(255,255,255,.1);
    mix-blend-mode:screen;
  }
  .title-glitch::before, .title-glitch::after{
    content:attr(data-text); position:absolute; inset:0;
  }
  .title-glitch::before{
    transform: translate(2px,-1px);
    -webkit-text-stroke: 3px var(--neon2);
    filter: drop-shadow(0 0 10px var(--neon2));
    animation: glitchX 3s infinite linear alternate-reverse;
  }
  .title-glitch::after{
    transform: translate(-2px,1px);
    -webkit-text-stroke: 3px var(--neon1);
    filter: drop-shadow(0 0 10px var(--neon1));
    mix-blend-mode:screen;
    animation: glitchY 2.2s infinite linear alternate-reverse;
  }
  @keyframes glitchX{
    0%{clip-path: inset(0 0 85% 0)}
    20%{clip-path: inset(0 0 70% 0)}
    40%{clip-path: inset(5% 0 40% 0)}
    60%{clip-path: inset(25% 0 15% 0)}
    80%{clip-path: inset(35% 0 0 0)}
    100%{clip-path: inset(0 0 85% 0)}
  }
  @keyframes glitchY{
    0%{clip-path: inset(85% 0 0 0)}
    25%{clip-path: inset(60% 0 10% 0)}
    50%{clip-path: inset(30% 0 30% 0)}
    75%{clip-path: inset(10% 0 60% 0)}
    100%{clip-path: inset(85% 0 0 0)}
  }

  .subtitle{
    margin:.75rem auto 0; color:var(--muted);
    font-weight:600; letter-spacing:.14em; text-transform:uppercase;
    text-shadow:0 0 18px rgba(127,0,255,.45), 0 0 30px rgba(0,230,255,.25);
  }

  /* -------------------- MATRIX RAIN CANVAS -------------------- */
  #matrix {
    position:fixed; inset:0; z-index:-1; opacity:.22; pointer-events:none;
    filter: blur(.2px) brightness(1.15);
  }

  /* -------------------- GRID / CARD WALL -------------------- */
  .grid{
    width:min(1200px, 93vw); margin:2.5rem auto 4rem;
    display:grid; grid-template-columns:repeat(12,1fr); gap:16px;
  }
  .card{
    grid-column: span 4;
    background: linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.02));
    border:1px solid var(--border);
    border-radius:18px;
    padding:22px;
    position:relative; overflow:hidden;
    transition: transform .2s ease, box-shadow .2s ease, border-color .2s ease;
    backdrop-filter: blur(6px) saturate(130%);
    box-shadow: inset 0 0 0 1px rgba(255,255,255,.02), 0 10px 30px rgba(0,0,0,.35);
  }
  .card::before{
    content:""; position:absolute; inset:-1px;
    background: conic-gradient(from 180deg, transparent 10%, rgba(0,230,255,.28), transparent 30%, rgba(122,0,255,.28), transparent 60%, rgba(255,0,230,.28), transparent 90%);
    filter: blur(18px); opacity:.5; z-index:-1;
  }
  .card:hover{ transform: translateY(-4px); border-color:rgba(255,255,255,.22) }
  .card h3{
    margin:0 0 6px; font-size:1.05rem; letter-spacing:.06em; color:var(--fg);
  }
  .chip-row{
    display:flex; flex-wrap:wrap; gap:10px; margin-top:10px;
  }
  .chip{
    --c: var(--neon1);
    padding:10px 12px; border-radius:999px; font-weight:700; font-size:.9rem; letter-spacing:.06em;
    background: radial-gradient(120% 180% at 30% 20%, rgba(255,255,255,.10), transparent 60%),
                linear-gradient(90deg, rgba(0,0,0,.1), rgba(0,0,0,.0));
    border:1px solid rgba(255,255,255,.18);
    color:var(--fg);
    box-shadow: 0 0 0 1px rgba(255,255,255,.05), 0 0 22px rgba(0, 230, 255, .15);
    position:relative; overflow:hidden;
  }
  .chip::after{
    content:""; position:absolute; inset:0; pointer-events:none;
    background: radial-gradient(120px 40px at -10% -10%, rgba(255,255,255,.45), transparent 50%),
                radial-gradient(200px 80px at 120% 120%, rgba(0,255,200,.15), transparent 40%);
    mix-blend-mode: screen;
  }

  /* -------------------- MARQUEE (infinite) -------------------- */
  .marquee{
    margin:2.5rem 0 1rem; border-block:1px solid rgba(255,255,255,.08);
    background: linear-gradient(90deg, rgba(255,255,255,.04), rgba(255,255,255,.02));
    overflow:hidden; position:relative;
  }
  .marquee .track{
    display:flex; gap:36px; padding:14px 0; width:max-content;
    animation: scrollX 26s linear infinite;
    filter: drop-shadow(0 0 8px rgba(0,230,255,.5));
  }
  @keyframes scrollX{from{transform:translateX(0)}to{transform:translateX(-50%)}}
  .tag{
    padding:8px 14px; border-radius:999px; font-weight:800; letter-spacing:.14em; text-transform:uppercase;
    border:1px solid rgba(255,255,255,.16);
    background:linear-gradient(180deg, rgba(255,255,255,.08), rgba(255,255,255,.02));
    color:var(--fg);
  }

  /* -------------------- GLASS NEON PANEL -------------------- */
  .panel {
    width:min(1100px, 92vw); margin:2rem auto 4rem; position:relative;
    background: linear-gradient(180deg, rgba(255,255,255,.05), rgba(255,255,255,.015));
    border:1px solid var(--border); border-radius:20px; padding:26px;
    backdrop-filter: blur(8px) saturate(140%);
    box-shadow: 0 10px 36px rgba(0,0,0,.36);
  }
  .panel .hdr{
    display:flex; align-items:center; gap:12px; margin-bottom:6px;
    font-weight:800; letter-spacing:.12em; text-transform:uppercase; color:var(--muted);
  }
  .panel .grid-logos{
    display:grid; grid-template-columns:repeat(6,minmax(120px,1fr)); gap:16px; margin-top:16px;
  }
  .logo{
    aspect-ratio: 16/9; border:1px solid rgba(255,255,255,.15); border-radius:14px;
    display:grid; place-items:center; position:relative; overflow:hidden;
    background: radial-gradient(90% 90% at 50% 0%, rgba(255,255,255,.07), rgba(255,255,255,.02));
    transition:transform .2s ease, border-color .2s ease;
  }
  .logo:hover{ transform: translateY(-2px); border-color:rgba(255,255,255,.3) }
  .logo span{
    font-weight:900; letter-spacing:.08em; font-size:1rem; color:#fff;
    text-shadow: 0 0 10px var(--neon1), 0 0 22px var(--neon2);
  }

  /* -------------------- TOOLS HUD -------------------- */
  .hud{
    position:fixed; right:16px; bottom:16px; display:flex; gap:8px; z-index:40;
  }
  .hud button{
    appearance:none; border:none; cursor:pointer;
    padding:10px 12px; border-radius:12px; font-weight:800; letter-spacing:.08em;
    color:#0a0015; background:linear-gradient(180deg, var(--neon1), var(--neon2));
    box-shadow: 0 10px 24px rgba(0,0,0,.4), 0 0 24px rgba(0,230,255,.45);
  }

  /* -------------------- FOOTER -------------------- */
  footer{
    text-align:center; padding:3rem 1rem 6rem; color:var(--muted);
  }

  /* -------------------- RESPONSIVE -------------------- */
  @media (max-width: 980px){
    .card{ grid-column: span 6; }
    .panel .grid-logos{ grid-template-columns:repeat(3,minmax(120px,1fr)); }
  }
  @media (max-width: 640px){
    .card{ grid-column: span 12; }
    .title{ font-size: clamp(2.2rem, 10vw, 4rem); }
    .panel .grid-logos{ grid-template-columns:repeat(2,minmax(120px,1fr)); }
  }
</style>
</head>
<body class="scanlines noise">
<canvas id="matrix"></canvas>
<div class="backdrop"></div>

<header>
  <div class="title-wrap">
    <h1 class="title">NEON // CYBER</h1>
    <div class="title-glitch" data-text="NEON // CYBER" aria-hidden="true"></div>
  </div>
  <div class="subtitle">VISUALS • MOTION • ZERO BIO</div>
</header>

<!-- marquee -->
<section class="marquee" aria-hidden="true">
  <div class="track">
    <span class="tag">neon</span>
    <span class="tag">glitch</span>
    <span class="tag">scanlines</span>
    <span class="tag">matrix</span>
    <span class="tag">cyber</span>
    <span class="tag">hologram</span>
    <span class="tag">crt</span>
    <span class="tag">laser</span>

    <span class="tag">neon</span>
    <span class="tag">glitch</span>
    <span class="tag">scanlines</span>
    <span class="tag">matrix</span>
    <span class="tag">cyber</span>
    <span class="tag">hologram</span>
    <span class="tag">crt</span>
    <span class="tag">laser</span>
  </div>
</section>

<!-- Cards grid (pure visuals) -->
<section class="grid" aria-label="visual-wall">
  <article class="card">
    <h3>HOLOGRAPHIC PANEL</h3>
    <div class="chip-row">
      <div class="chip" style="--c:var(--neon1)">NEON</div>
      <div class="chip" style="--c:var(--neon2)">GLOW</div>
      <div class="chip" style="--c:var(--neon3)">GLITCH</div>
      <div class="chip" style="--c:var(--neon4)">CRT</div>
    </div>
  </article>

  <article class="card">
    <h3>VAPOR GRID</h3>
    <div class="chip-row">
      <div class="chip">WIREFRAME</div>
      <div class="chip">DEPTH</div>
      <div class="chip">PARALLAX</div>
      <div class="chip">SHADOW</div>
    </div>
  </article>

  <article class="card">
    <h3>LASER BLOOM</h3>
    <div class="chip-row">
      <div class="chip">BEAM</div>
      <div class="chip">BLOOM</div>
      <div class="chip">FLARE</div>
      <div class="chip">NOISE</div>
    </div>
  </article>

  <article class="card">
    <h3>HOLO CHIPSET</h3>
    <div class="chip-row">
      <div class="chip">ION</div>
      <div class="chip">CORE</div>
      <div class="chip">NOVA</div>
      <div class="chip">FLUX</div>
    </div>
  </article>

  <article class="card">
    <h3>XR TUNNEL</h3>
    <div class="chip-row">
      <div class="chip">WARP</div>
      <div class="chip">TUNNEL</div>
      <div class="chip">DEPTH</div>
      <div class="chip">ECHO</div>
    </div>
  </article>

  <article class="card">
    <h3>ION FOAM</h3>
    <div class="chip-row">
      <div class="chip">BOKEH</div>
      <div class="chip">ION</div>
      <div class="chip">FOAM</div>
      <div class="chip">GAS</div>
    </div>
  </article>
</section>

<!-- STACK ONLY (единственный смысловой блок) -->
<section class="panel" id="stack">
  <div class="hdr">STACK • ONLY</div>
  <div class="grid-logos">
    <div class="logo"><span>Go</span></div>
    <div class="logo"><span>PHP&nbsp;8</span></div>
    <div class="logo"><span>TS</span></div>
    <div class="logo"><span>React</span></div>
    <div class="logo"><span>Node</span></div>
    <div class="logo"><span>Postgres</span></div>

    <div class="logo"><span>MySQL</span></div>
    <div class="logo"><span>Redis</span></div>
    <div class="logo"><span>Docker</span></div>
    <div class="logo"><span>K8s</span></div>
    <div class="logo"><span>NGINX</span></div>
    <div class="logo"><span>GitHub&nbsp;Actions</span></div>
  </div>
</section>

<footer>
  <div>CYBER SURFACE — visuals first • no bio</div>
</footer>

<!-- HUD buttons -->
<div class="hud">
  <button id="themeBtn" title="Switch Neon Theme [T]">THEME</button>
  <button id="pulseBtn" title="Pulse Boost [P]">PULSE</button>
  <button id="scanBtn" title="Toggle Scanlines [S]">SCAN</button>
</div>

<script>
/* ========================= MATRIX RAIN ========================= */
(function matrixRain(){
  const c = document.getElementById('matrix');
  const x = c.getContext('2d');
  let W, H, cols, drops, rafId;
  const glyphs = 'アカサタナハマヤラワ0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ$#';

  const resize = () => {
    const dpr = Math.min(window.devicePixelRatio || 1, 2);
    W = c.width  = Math.floor(innerWidth  * dpr);
    H = c.height = Math.floor(innerHeight * dpr);
    c.style.width  = innerWidth + 'px';
    c.style.height = innerHeight + 'px';
    const fontSize = Math.max(14 * dpr, 12);
    x.font = fontSize + 'px monospace';
    cols = Math.floor(W / (fontSize * 0.65));
    drops = Array(cols).fill(0).map(()=>Math.random()*H/2);
  };

  const draw = () => {
    x.fillStyle = 'rgba(3,1,12,0.18)';
    x.fillRect(0,0,W,H);
    for(let i=0;i<cols;i++){
      const txt = glyphs[Math.floor(Math.random()*glyphs.length)];
      const hue = (i/cols*360)|0;
      x.fillStyle = `hsl(${hue}, 100%, 65%)`;
      const fs = parseInt(x.font,10) || 16;
      const y = drops[i]*fs;
      x.fillText(txt, i*fs*0.65, y);
      if(y > H && Math.random() > 0.975) drops[i]=0;
      drops[i]++;
    }
    rafId = requestAnimationFrame(draw);
  };

  addEventListener('resize', ()=>{ cancelAnimationFrame(rafId); resize(); draw(); }, {passive:true});
  resize(); draw();
})();

/* ========================= THEME / EFFECTS ========================= */
const $ = (sel)=>document.querySelector(sel);
const themeBtn = $('#themeBtn');
const pulseBtn = $('#pulseBtn');
const scanBtn  = $('#scanBtn');

themeBtn.addEventListener('click', toggleTheme);
pulseBtn.addEventListener('click', pulseBoost);
scanBtn .addEventListener('click', toggleScan);

document.addEventListener('keydown', (e)=>{
  if(e.key.toLowerCase()==='t') toggleTheme();
  if(e.key.toLowerCase()==='p') pulseBoost();
  if(e.key.toLowerCase()==='s') toggleScan();
});

function toggleTheme(){
  document.body.classList.toggle('theme-alt');
  // tiny flash
  flashBorder();
}

function toggleScan(){
  document.body.classList.toggle('scanlines');
}

function pulseBoost(){
  // pulse neon on major elements
  const els = document.querySelectorAll('.title,.card,.panel,.logo,.chip,.tag');
  els.forEach(el=>{
    el.animate([
      { filter:'brightness(1) saturate(1)' },
      { filter:'brightness(1.75) saturate(1.4)' },
      { filter:'brightness(1) saturate(1)' }
    ],{duration:700, easing:'ease-in-out'});
  });
  // ripple from HUD
  ripple(document.body, {x: innerWidth-80, y: innerHeight-80});
}

/* ========================= SMALL UTILS ========================= */
function flashBorder(){
  const root = document.documentElement;
  const el = document.createElement('div');
  el.style.position='fixed';
  el.style.inset='0';
  el.style.pointerEvents='none';
  el.style.border='4px solid rgba(0,255,255,.8)';
  el.style.boxShadow='inset 0 0 60px rgba(122,0,255,.35), 0 0 80px rgba(0,255,255,.3)';
  el.style.mixBlendMode='screen';
  el.style.borderRadius='8px';
  el.style.opacity='0';
  el.style.transition='opacity .14s ease';
  document.body.appendChild(el);
  requestAnimationFrame(()=>{ el.style.opacity='1'; });
  setTimeout(()=>{ el.style.opacity='0'; setTimeout(()=>el.remove(),180); }, 120);
}

function ripple(container, pos){
  const r = document.createElement('span');
  r.style.position='fixed';
  r.style.left=(pos.x||innerWidth/2)+'px';
  r.style.top=(pos.y||innerHeight/2)+'px';
  r.style.width=r.style.height='4px';
  r.style.transform='translate(-50%,-50%)';
  r.style.border='2px solid rgba(0,255,255,.9)';
  r.style.borderRadius='999px';
  r.style.boxShadow='0 0 30px rgba(0,255,255,.6), 0 0 60px rgba(122,0,255,.4)';
  r.style.pointerEvents='none';
  r.style.zIndex='50';
  document.body.appendChild(r);
  r.animate([
    {opacity:1, transform:'translate(-50%,-50%) scale(1)'},
    {opacity:0, transform:'translate(-50%,-50%) scale(60)'}
  ],{duration:850, easing:'cubic-bezier(.2,.6,.2,1)'})
  .addEventListener('finish', ()=>r.remove());
}

/* ========================= 3D Tilt on hover (logos) ========================= */
const cards = document.querySelectorAll('.logo,.card');
cards.forEach(el=>{
  let rx=0, ry=0, t;
  const lim = 10;
  function onMove(e){
    const r = el.getBoundingClientRect();
    const px = (e.clientX - r.left) / r.width;
    const py = (e.clientY - r.top)  / r.height;
    ry = (px-.5)*lim;
    rx = -(py-.5)*lim;
    el.style.transform = `rotateX(${rx}deg) rotateY(${ry}deg) translateY(-2px)`;
  }
  function onLeave(){
    el.style.transform = 'rotateX(0) rotateY(0)';
  }
  el.addEventListener('mousemove', onMove);
  el.addEventListener('mouseleave', onLeave);
});

/* ========================= Subtle Parallax on scroll ========================= */
const backdrop = document.querySelector('.backdrop');
let lastY = 0;
addEventListener('scroll',()=>{
  const y = scrollY;
  const d = (y - lastY) * 0.04;
  lastY = y;
  backdrop.style.transform = `translate3d(0,${-y*0.05}px,0) scale(1.02)`;
},{passive:true});
</script>
</body>
</html>
