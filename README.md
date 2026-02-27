<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>House of Nitin — Creative Realm</title>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700;900&family=Cinzel:wght@400;600;700&family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&display=swap" rel="stylesheet"/>

  <style>
  /* ═══════════════════════════════════════════
     DESIGN TOKENS
  ═══════════════════════════════════════════ */
  :root {
    --black:      #04030a;
    --void:       #09071a;
    --iron:       #141220;
    --gold:       #c8a84b;
    --gold-lt:    #ecd98a;
    --gold-dim:   rgba(200,168,75,0.18);
    --ember:      #7a1408;
    --crimson:    #5c0f0f;
    --ash:        #8c8aa0;
    --parchment:  #e8e0cc;
    --white:      #f5f0e8;
    --border-gold: rgba(200,168,75,0.3);
    --border-iron: rgba(255,255,255,0.07);
  }

  /* ═══════════════════════════════════════════
     RESET & BASE
  ═══════════════════════════════════════════ */
  *, *::before, *::after { margin:0; padding:0; box-sizing:border-box; }
  html { scroll-behavior:smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'Cormorant Garamond', serif;
    overflow-x: hidden;
    cursor: none;
    min-height: 100vh;
  }

  /* ═══════════════════════════════════════════
     CURSOR
  ═══════════════════════════════════════════ */
  #cur-dot {
    position:fixed; width:8px; height:8px;
    background:var(--gold); border-radius:50%;
    pointer-events:none; z-index:99999;
    transform:translate(-50%,-50%);
    transition:width .15s, height .15s, background .2s;
    mix-blend-mode:screen;
  }
  #cur-ring {
    position:fixed; width:36px; height:36px;
    border:1px solid rgba(200,168,75,.45);
    border-radius:50%; pointer-events:none;
    z-index:99998; transform:translate(-50%,-50%);
    transition:all .18s ease-out;
  }
  body.hovering #cur-dot  { width:18px; height:18px; background:var(--gold-lt); }
  body.hovering #cur-ring { width:56px; height:56px; border-color:var(--gold); }

  /* ═══════════════════════════════════════════
     NOISE LAYER
  ═══════════════════════════════════════════ */
  .noise {
    position:fixed; inset:0; pointer-events:none; z-index:9990; opacity:.028;
    background-image:url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }

  /* ═══════════════════════════════════════════
     FIRE CANVAS
  ═══════════════════════════════════════════ */
  #fireCanvas {
    position:fixed; inset:0;
    pointer-events:none; z-index:1; opacity:.3;
  }

  /* ═══════════════════════════════════════════
     PAGE SYSTEM
  ═══════════════════════════════════════════ */
  .page { display:none; }
  .page.active {
    display:block;
    animation: pgIn .8s cubic-bezier(.16,1,.3,1) both;
  }
  @keyframes pgIn {
    from { opacity:0; transform:translateY(16px); }
    to   { opacity:1; transform:translateY(0); }
  }

  /* ═══════════════════════════════════════════
     ██████████ HOME PAGE ██████████
  ═══════════════════════════════════════════ */

  /* --- FULL-VIEWPORT CINEMATIC HERO --- */
  #home {
    position:relative;
    min-height: 100vh;
    display: grid;
    grid-template-rows: 1fr auto;
    overflow:hidden;
  }

  /* Dramatic diagonal split background */
  .home-bg {
    position:absolute; inset:0; z-index:0;
    background:
      /* left: deep cold void */
      linear-gradient(105deg,
        #04030a 0%,
        #09071a 38%,
        transparent 55%
      ),
      /* right: ember glow */
      linear-gradient(to left,
        rgba(90,10,5,.7) 0%,
        rgba(30,5,5,.4) 35%,
        transparent 55%
      ),
      var(--black);
  }

  /* Thin vertical gold accent line on the diagonal */
  .home-bg::after {
    content:'';
    position:absolute; top:0; bottom:0;
    left:52%; width:1px;
    background:linear-gradient(180deg,
      transparent 0%,
      var(--gold) 20%,
      var(--gold-lt) 50%,
      var(--gold) 80%,
      transparent 100%
    );
    opacity:.25;
    transform:skewX(-12deg) translateX(-50%);
  }

  /* Radial ember glow top-right */
  .home-bg::before {
    content:'';
    position:absolute;
    top:-20%; right:-10%;
    width:70vw; height:70vw;
    background:radial-gradient(circle, rgba(100,15,5,.35) 0%, transparent 65%);
    pointer-events:none;
  }

  /* === HERO CONTENT === */
  .hero-content {
    position:relative; z-index:5;
    display:grid;
    grid-template-columns: 1fr 1fr;
    min-height:100vh;
    align-items:center;
  }

  /* LEFT COLUMN — identity block */
  .hero-left {
    padding: 6rem 4rem 6rem 8%;
    display:flex; flex-direction:column;
    justify-content:center;
    gap:0;
  }

  .hl-eyebrow {
    font-family:'Cinzel', serif;
    font-size:.65rem;
    letter-spacing:7px;
    text-transform:uppercase;
    color:var(--gold);
    margin-bottom:2rem;
    display:flex; align-items:center; gap:1rem;
    opacity:0; animation:fadeUp .8s .3s forwards;
  }
  .hl-eyebrow::before {
    content:'';
    width:30px; height:1px;
    background:var(--gold); flex-shrink:0;
  }

  .hl-name {
    font-family:'Cinzel Decorative', cursive;
    font-weight:900;
    font-size:clamp(3.8rem, 6.5vw, 7.5rem);
    line-height:.88;
    color:var(--white);
    text-shadow:
      0 0 80px rgba(200,168,75,.15),
      0 4px 0 rgba(0,0,0,.6);
    margin-bottom:.5rem;
    opacity:0; animation:fadeUp 1s .5s forwards;
  }

  .hl-title {
    font-family:'Cormorant Garamond', serif;
    font-weight:300;
    font-size:clamp(1.1rem,2vw,1.7rem);
    font-style:italic;
    color:var(--gold);
    letter-spacing:3px;
    margin-bottom:3rem;
    opacity:0; animation:fadeUp .8s .7s forwards;
  }

  /* Animated gold ruler */
  .hl-ruler {
    width:0; height:1px;
    background:linear-gradient(90deg, var(--gold), transparent);
    margin-bottom:2.5rem;
    animation:growLine 1s 1s forwards;
  }
  @keyframes growLine { to { width:200px; } }

  .hl-desc {
    font-size:clamp(1rem,1.2vw,1.15rem);
    line-height:2;
    color:var(--ash);
    max-width:420px;
    margin-bottom:3rem;
    opacity:0; animation:fadeUp .8s .9s forwards;
  }
  .hl-desc strong { color:var(--parchment); font-weight:600; font-style:normal; }

  /* CTA BUTTON — medieval gate style */
  .gate-btn {
    display:inline-flex; align-items:center; gap:1rem;
    font-family:'Cinzel', serif;
    font-size:.75rem; letter-spacing:5px;
    text-transform:uppercase;
    color:var(--black);
    background:var(--gold);
    border:none; cursor:none;
    padding:1rem 2.8rem;
    position:relative; overflow:hidden;
    clip-path:polygon(12px 0%,100% 0%,calc(100% - 12px) 100%,0% 100%);
    transition:background .3s, box-shadow .3s;
    align-self:flex-start;
    opacity:0; animation:fadeUp .8s 1.1s forwards;
  }
  .gate-btn::after {
    content:'';
    position:absolute; inset:0;
    background:linear-gradient(90deg, transparent, rgba(255,255,255,.3), transparent);
    transform:translateX(-100%);
    transition:transform .55s;
  }
  .gate-btn:hover { background:var(--gold-lt); box-shadow:0 0 50px rgba(200,168,75,.45); }
  .gate-btn:hover::after { transform:translateX(100%); }
  .gate-btn-arrow {
    display:inline-block;
    transition:transform .3s;
  }
  .gate-btn:hover .gate-btn-arrow { transform:translateX(4px); }

  /* RIGHT COLUMN — sigil + stats */
  .hero-right {
    padding: 6rem 8% 6rem 2rem;
    display:flex; flex-direction:column;
    align-items:center; justify-content:center;
    gap:3rem;
    opacity:0; animation:fadeIn .9s 1.2s forwards;
  }

  /* BIG SIGIL */
  .big-sigil {
    position:relative;
    width:260px; height:260px;
    flex-shrink:0;
  }
  .big-sigil svg { width:100%; height:100%; }
  .sigil-ring-1 { animation:spin 28s linear infinite; transform-origin:center; }
  .sigil-ring-2 { animation:spin 18s linear infinite reverse; transform-origin:center; }

  @keyframes spin {
    from { transform:rotate(0deg); }
    to   { transform:rotate(360deg); }
  }

  /* Pulsing gold glow */
  .big-sigil::before {
    content:'';
    position:absolute; inset:0;
    background:radial-gradient(circle, rgba(200,168,75,.15) 0%, transparent 65%);
    animation:pulseGlow 3s ease-in-out infinite;
    border-radius:50%;
  }
  @keyframes pulseGlow {
    0%,100% { opacity:.6; transform:scale(1); }
    50%     { opacity:1; transform:scale(1.1); }
  }

  /* STATS STRIP */
  .stats-strip {
    display:flex; gap:2.5rem;
    padding:1.5rem 2rem;
    border:1px solid var(--border-gold);
    background:rgba(9,7,26,.7);
    backdrop-filter:blur(12px);
    position:relative;
  }
  .stats-strip::before, .stats-strip::after {
    content:''; position:absolute;
    width:16px; height:16px;
    border-color:var(--gold); border-style:solid;
  }
  .stats-strip::before { top:-1px; left:-1px; border-width:2px 0 0 2px; }
  .stats-strip::after  { bottom:-1px; right:-1px; border-width:0 2px 2px 0; }

  .stat { text-align:center; }
  .stat-num {
    font-family:'Cinzel Decorative', cursive;
    font-size:2rem; font-weight:700;
    color:var(--gold); display:block;
    line-height:1;
  }
  .stat-label {
    font-family:'Cinzel', serif;
    font-size:.55rem; letter-spacing:3px;
    text-transform:uppercase; color:var(--ash);
    margin-top:.4rem; display:block;
  }
  .stat-divider {
    width:1px; background:var(--border-iron);
    align-self:stretch;
  }

  /* House words */
  .house-words {
    font-family:'Cormorant Garamond', serif;
    font-style:italic;
    font-size:1rem;
    color:rgba(200,168,75,.6);
    letter-spacing:2px;
    text-align:center;
    position:relative;
    padding:0 2rem;
  }
  .house-words::before, .house-words::after {
    content:'❧';
    color:rgba(200,168,75,.4);
    margin:0 .8rem;
  }

  /* === ABOUT SCROLL SECTION === */
  .home-about {
    position:relative; z-index:5;
    padding:5rem 8% 8rem;
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:4rem;
    align-items:start;
    border-top:1px solid var(--border-iron);
    background:linear-gradient(180deg, transparent, rgba(9,7,26,.6));
  }

  .about-col-label {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:7px;
    text-transform:uppercase; color:var(--gold);
    margin-bottom:1.5rem;
    display:flex; align-items:center; gap:1rem;
  }
  .about-col-label::after {
    content:''; flex:1; height:1px;
    background:linear-gradient(90deg, var(--gold-dim), transparent);
  }

  .about-heading-big {
    font-family:'Cinzel Decorative', cursive;
    font-size:clamp(1.8rem,3vw,2.8rem);
    color:var(--white);
    line-height:1.1;
    margin-bottom:1.8rem;
    font-weight:700;
  }

  .about-body-text {
    font-size:1.15rem; line-height:2.05;
    color:var(--ash);
  }
  .about-body-text strong { color:var(--parchment); font-weight:600; }
  .about-body-text em     { color:rgba(200,168,75,.8); font-style:italic; }

  /* Skills rune list */
  .rune-list {
    list-style:none;
    display:flex; flex-direction:column; gap:1rem;
    margin-top:1rem;
  }
  .rune-list li {
    display:flex; align-items:center; gap:1rem;
    font-family:'Cinzel', serif;
    font-size:.75rem; letter-spacing:3px;
    text-transform:uppercase; color:var(--ash);
    padding:.9rem 1.2rem;
    border:1px solid var(--border-iron);
    background:rgba(255,255,255,.02);
    transition:border-color .3s, color .3s, background .3s;
    position:relative;
  }
  .rune-list li:hover {
    border-color:var(--border-gold);
    color:var(--gold);
    background:rgba(200,168,75,.04);
  }
  .rune-glyph {
    font-family:'Cinzel Decorative', cursive;
    font-size:1.1rem; color:var(--gold);
    width:24px; flex-shrink:0;
  }

  /* scroll reveal */
  .rev {
    opacity:0; transform:translateY(24px);
    transition:opacity .8s, transform .8s cubic-bezier(.16,1,.3,1);
  }
  .rev.in { opacity:1; transform:translateY(0); }

  /* ═══════════════════════════════════════════
     ██████████ GALLERY PAGE ██████████
  ═══════════════════════════════════════════ */
  #gallery {
    min-height:100vh;
    background:var(--void);
    position:relative;
  }

  /* Full-width cinematic header */
  .gal-hero {
    position:relative;
    overflow:hidden;
    background:linear-gradient(160deg, #0a0818 0%, #12080f 50%, #060310 100%);
    padding: 5rem 8% 4rem;
    border-bottom:1px solid var(--border-gold);
  }

  /* Decorative background text */
  .gal-hero-bg-text {
    position:absolute;
    top:50%; left:50%;
    transform:translate(-50%,-50%);
    font-family:'Cinzel Decorative', cursive;
    font-size:clamp(5rem,15vw,14rem);
    font-weight:900;
    color:rgba(200,168,75,.04);
    white-space:nowrap;
    pointer-events:none;
    letter-spacing:-.02em;
    user-select:none;
  }

  /* Ember line across top */
  .gal-hero::before {
    content:'';
    position:absolute; top:0; left:0; right:0; height:3px;
    background:linear-gradient(90deg, var(--ember), var(--gold), var(--gold-lt), var(--gold), var(--ember));
  }

  .gal-nav {
    display:flex; align-items:center;
    justify-content:space-between;
    margin-bottom:4rem;
    position:relative; z-index:2;
  }

  /* Back button — now styled as a heraldic shield badge */
  .shield-btn {
    font-family:'Cinzel', serif;
    font-size:.65rem; letter-spacing:4px;
    text-transform:uppercase; color:var(--ash);
    background:transparent;
    border:1px solid var(--border-iron);
    padding:.7rem 1.6rem; cursor:none;
    display:flex; align-items:center; gap:.8rem;
    transition:color .3s, border-color .3s, background .3s;
    clip-path:polygon(8px 0%,100% 0%,calc(100% - 8px) 100%,0% 100%);
  }
  .shield-btn:hover {
    color:var(--gold);
    border-color:var(--border-gold);
    background:rgba(200,168,75,.06);
  }

  .gal-header-center {
    text-align:center; position:relative; z-index:2;
  }
  .gal-header-eyebrow {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:7px;
    text-transform:uppercase; color:var(--gold);
    margin-bottom:.6rem;
  }
  .gal-header-title {
    font-family:'Cinzel Decorative', cursive;
    font-size:clamp(2rem,5vw,4.5rem);
    font-weight:700;
    color:var(--white);
    text-shadow:0 0 60px rgba(200,168,75,.15);
    line-height:1;
  }
  .gal-header-sub {
    font-family:'Cormorant Garamond', serif;
    font-style:italic; font-size:1.1rem;
    color:var(--ash); margin-top:.8rem;
    letter-spacing:1px;
  }

  /* Count badge */
  .gal-count {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:4px;
    text-transform:uppercase;
    color:var(--ash);
    display:flex; align-items:center; gap:.6rem;
  }
  .gal-count-num {
    font-family:'Cinzel Decorative', cursive;
    font-size:1.4rem; color:var(--gold); font-weight:700;
  }

  /* === FILTER TABS === */
  .filter-bar {
    position:relative; z-index:2;
    display:flex; gap:.6rem; justify-content:center;
    margin-top:3rem; flex-wrap:wrap;
  }
  .filter-tab {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:3px;
    text-transform:uppercase; color:var(--ash);
    background:transparent;
    border:1px solid var(--border-iron);
    padding:.55rem 1.4rem; cursor:none;
    transition:all .25s;
    clip-path:polygon(6px 0%,100% 0%,calc(100% - 6px) 100%,0% 100%);
  }
  .filter-tab:hover, .filter-tab.active {
    color:var(--gold); border-color:var(--border-gold);
    background:rgba(200,168,75,.08);
  }
  .filter-tab.active {
    background:var(--gold); color:var(--black);
    border-color:var(--gold);
  }

  /* === THE GRID === */
  .gal-body { padding:4rem 6% 8rem; }

  /* Horizontal scrolling featured strip */
  .featured-strip {
    margin-bottom:4rem;
  }
  .featured-label {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:6px;
    text-transform:uppercase; color:var(--gold);
    margin-bottom:1.2rem;
    display:flex; align-items:center; gap:1rem;
  }
  .featured-label::after {
    content:''; flex:1; height:1px;
    background:linear-gradient(90deg,var(--border-gold),transparent);
  }

  .scroll-row {
    display:flex; gap:1.2rem;
    overflow-x:auto; padding-bottom:1rem;
    scroll-snap-type:x mandatory;
    scrollbar-width:thin;
    scrollbar-color:var(--border-gold) transparent;
  }
  .scroll-row::-webkit-scrollbar { height:3px; }
  .scroll-row::-webkit-scrollbar-track { background:transparent; }
  .scroll-row::-webkit-scrollbar-thumb { background:var(--border-gold); border-radius:2px; }

  .scroll-card {
    flex-shrink:0; width:340px; height:200px;
    position:relative; overflow:hidden;
    scroll-snap-align:start;
    border:1px solid var(--border-iron);
    cursor:none;
    transition:border-color .4s, box-shadow .4s;
  }
  .scroll-card:hover {
    border-color:var(--border-gold);
    box-shadow:0 0 30px rgba(200,168,75,.15);
  }
  .scroll-card img {
    width:100%; height:100%; object-fit:cover;
    filter:saturate(.6) brightness(.85);
    transition:filter .5s, transform .6s cubic-bezier(.16,1,.3,1);
  }
  .scroll-card:hover img {
    filter:saturate(1) brightness(1);
    transform:scale(1.06);
  }
  .scroll-card-overlay {
    position:absolute; inset:0;
    background:linear-gradient(160deg, rgba(9,7,26,.3), transparent 50%, rgba(90,10,5,.4));
    opacity:0; transition:opacity .4s;
  }
  .scroll-card:hover .scroll-card-overlay { opacity:1; }

  /* === MAIN GRID === */
  .main-grid-label {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:6px;
    text-transform:uppercase; color:var(--ash);
    margin-bottom:1.5rem;
    display:flex; align-items:center; gap:1rem;
  }
  .main-grid-label::before, .main-grid-label::after {
    content:''; flex:1; height:1px;
    background:var(--border-iron);
  }

  .thumb-grid {
    display:grid;
    grid-template-columns:repeat(auto-fill, minmax(280px,1fr));
    gap:1.2rem;
  }

  .thumb-card {
    position:relative; overflow:hidden;
    aspect-ratio:16/9;
    border:1px solid var(--border-iron);
    cursor:none;
    transition:border-color .35s, transform .4s cubic-bezier(.16,1,.3,1), box-shadow .35s;
    background:var(--iron);
  }

  .thumb-card::before {
    content:'';
    position:absolute; inset:5px;
    border:1px solid rgba(200,168,75,.0);
    z-index:3; pointer-events:none;
    transition:border-color .35s;
  }

  .thumb-card:hover {
    border-color:var(--border-gold);
    transform:translateY(-4px);
    box-shadow:0 12px 40px rgba(0,0,0,.6), 0 0 20px rgba(200,168,75,.08);
  }
  .thumb-card:hover::before { border-color:rgba(200,168,75,.3); }

  .thumb-card img {
    width:100%; height:100%; object-fit:cover;
    filter:saturate(.65) contrast(1.05) brightness(.88);
    transition:filter .5s, transform .6s cubic-bezier(.16,1,.3,1);
    display:block;
  }
  .thumb-card:hover img {
    filter:saturate(1) contrast(1) brightness(1);
    transform:scale(1.05);
  }

  /* Overlay with card number + CTA */
  .thumb-overlay {
    position:absolute; inset:0; z-index:2;
    background:linear-gradient(to top, rgba(4,3,10,.88) 0%, transparent 50%);
    display:flex; flex-direction:column;
    justify-content:flex-end;
    padding:1rem 1.2rem;
    transform:translateY(8px);
    opacity:0;
    transition:opacity .35s, transform .35s cubic-bezier(.16,1,.3,1);
  }
  .thumb-card:hover .thumb-overlay { opacity:1; transform:translateY(0); }

  .thumb-num {
    font-family:'Cinzel Decorative', cursive;
    font-size:.65rem; color:var(--gold); letter-spacing:2px;
    margin-bottom:.2rem;
  }
  .thumb-cta {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:4px;
    text-transform:uppercase; color:var(--ash);
    display:flex; align-items:center; gap:.5rem;
  }
  .thumb-cta::after {
    content:'→'; transition:transform .3s;
  }
  .thumb-card:hover .thumb-cta::after { transform:translateX(4px); }

  /* Ember corner accent */
  .thumb-card::after {
    content:'';
    position:absolute; bottom:0; right:0;
    width:30px; height:30px;
    background:linear-gradient(135deg,transparent 50%,rgba(122,20,8,.5) 50%);
    z-index:3; opacity:0;
    transition:opacity .35s;
  }
  .thumb-card:hover::after { opacity:1; }

  /* ═══════════════════════════════════════════
     LIGHTBOX
  ═══════════════════════════════════════════ */
  #lightbox {
    position:fixed; inset:0;
    background:rgba(4,3,10,.97);
    z-index:9500;
    display:flex; flex-direction:column;
    align-items:center; justify-content:center;
    opacity:0; pointer-events:none;
    transition:opacity .4s;
    padding:2rem;
  }
  #lightbox.open { opacity:1; pointer-events:all; }

  .lb-inner {
    position:relative;
    max-width:90vw; max-height:85vh;
    border:1px solid var(--border-gold);
  }
  .lb-inner::before, .lb-inner::after {
    content:''; position:absolute;
    width:20px; height:20px;
    border-color:var(--gold-lt); border-style:solid;
    z-index:2;
  }
  .lb-inner::before { top:-1px; left:-1px; border-width:2px 0 0 2px; }
  .lb-inner::after  { bottom:-1px; right:-1px; border-width:0 2px 2px 0; }

  #lb-img {
    max-width:90vw; max-height:80vh;
    object-fit:contain; display:block;
  }

  .lb-bar {
    display:flex; align-items:center; justify-content:space-between;
    padding:.8rem 1.2rem;
    background:rgba(9,7,26,.95);
    border-top:1px solid var(--border-iron);
  }
  .lb-label {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:4px;
    text-transform:uppercase; color:var(--gold);
  }

  .lb-close {
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:3px;
    text-transform:uppercase; color:var(--ash);
    background:transparent; border:none; cursor:none;
    transition:color .3s;
  }
  .lb-close:hover { color:var(--white); }

  /* Prev/Next */
  .lb-prev, .lb-next {
    position:absolute; top:50%; transform:translateY(-50%);
    font-family:'Cinzel', serif;
    font-size:.65rem; letter-spacing:3px; text-transform:uppercase;
    color:var(--ash); background:rgba(4,3,10,.8);
    border:1px solid var(--border-iron);
    padding:.7rem 1.1rem; cursor:none;
    transition:color .3s, border-color .3s;
    z-index:3;
  }
  .lb-prev { left:-60px; }
  .lb-next { right:-60px; }
  .lb-prev:hover, .lb-next:hover { color:var(--gold); border-color:var(--border-gold); }

  /* ═══════════════════════════════════════════
     MUSIC BTN
  ═══════════════════════════════════════════ */
  #music-btn {
    position:fixed; bottom:2rem; right:2rem;
    font-family:'Cinzel', serif;
    font-size:.6rem; letter-spacing:3px; text-transform:uppercase;
    color:var(--gold); background:rgba(4,3,10,.92);
    border:1px solid var(--border-gold);
    padding:.7rem 1.4rem; cursor:none; z-index:9999;
    clip-path:polygon(6px 0%,100% 0%,calc(100% - 6px) 100%,0% 100%);
    transition:background .3s, color .3s;
    display:none;
  }
  #music-btn:hover { background:var(--gold); color:var(--black); }

  /* ═══════════════════════════════════════════
     KEYFRAMES
  ═══════════════════════════════════════════ */
  @keyframes fadeUp {
    from { opacity:0; transform:translateY(20px); }
    to   { opacity:1; transform:translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity:0; } to { opacity:1; }
  }

  /* ═══════════════════════════════════════════
     RESPONSIVE
  ═══════════════════════════════════════════ */
  @media(max-width:900px) {
    .hero-content { grid-template-columns:1fr; min-height:auto; }
    .hero-left { padding:6rem 6% 3rem; }
    .hero-right { padding:2rem 6% 5rem; }
    .home-about { grid-template-columns:1fr; padding:4rem 6% 6rem; }
    .gal-hero { padding:4rem 6% 3rem; }
    .gal-nav { flex-direction:column; gap:1.5rem; text-align:center; }
    .gal-body { padding:3rem 4% 6rem; }
    .lb-prev { left:-10px; }
    .lb-next { right:-10px; }
  }
  @media(max-width:600px) {
    .hl-name { font-size:3rem; }
    .stats-strip { gap:1.5rem; padding:1rem 1.2rem; }
    .big-sigil { width:180px; height:180px; }
    .thumb-grid { grid-template-columns:1fr 1fr; gap:.8rem; }
    .gal-count { display:none; }
  }
  </style>
</head>
<body>

  <!-- Cursor -->
  <div id="cur-dot"></div>
  <div id="cur-ring"></div>

  <!-- Noise -->
  <div class="noise"></div>

  <!-- Fire canvas -->
  <canvas id="fireCanvas"></canvas>

  <!-- Audio -->
  <audio id="got-audio" loop>
    <source src="music/got-theme.mp3" type="audio/mpeg">
  </audio>
  <button id="music-btn" onclick="toggleMusic()">♪ Silence</button>

  <!-- Lightbox -->
  <div id="lightbox" onclick="handleLbClick(event)">
    <div class="lb-inner">
      <button class="lb-prev" onclick="lbNav(-1); event.stopPropagation()">‹</button>
      <button class="lb-next" onclick="lbNav(1); event.stopPropagation()">›</button>
      <img id="lb-img" src="" alt=""/>
      <div class="lb-bar">
        <span class="lb-label" id="lb-label">Design</span>
        <button class="lb-close" onclick="closeLb()">✕ Close</button>
      </div>
    </div>
  </div>

  <!-- ══════════════════════════════════════════
       HOME PAGE
  ══════════════════════════════════════════ -->
  <main id="home" class="page active">

    <!-- BG -->
    <div class="home-bg"></div>

    <!-- HERO — two-column split -->
    <div class="hero-content">

      <!-- LEFT -->
      <div class="hero-left">
        <span class="hl-eyebrow">House of Nitin — Visual Realm</span>
        <h1 class="hl-name">Nitin</h1>
        <p class="hl-title">Thumbnail Designer &amp; Creator</p>
        <div class="hl-ruler"></div>
        <p class="hl-desc">
          Forging <strong>high-converting YouTube thumbnails</strong> in the fires of creativity.
          A song of design, strategy, and visual conquest — where every frame is a battle standard.
        </p>
        <button class="gate-btn" onclick="openGallery()">
          Enter the Armory <span class="gate-btn-arrow">→</span>
        </button>
      </div>

      <!-- RIGHT -->
      <div class="hero-right">

        <!-- Sigil -->
        <div class="big-sigil">
          <svg viewBox="0 0 200 200" fill="none" xmlns="http://www.w3.org/2000/svg">
            <!-- outer ring -->
            <circle cx="100" cy="100" r="95" stroke="rgba(200,168,75,.15)" stroke-width="1"/>
            <!-- rotating dashed ring 1 -->
            <g class="sigil-ring-1">
              <circle cx="100" cy="100" r="82" stroke="rgba(200,168,75,.2)" stroke-width="1" stroke-dasharray="6 5"/>
            </g>
            <!-- rotating ring 2 -->
            <g class="sigil-ring-2">
              <circle cx="100" cy="100" r="68" stroke="rgba(200,168,75,.12)" stroke-width="1" stroke-dasharray="2 8"/>
            </g>
            <!-- 8-point star -->
            <polygon points="100,8 105,92 192,100 105,108 100,192 95,108 8,100 95,92"
              fill="rgba(200,168,75,.12)" stroke="#c8a84b" stroke-width="1.2"/>
            <!-- inner star -->
            <polygon points="100,30 103,94 170,100 103,106 100,170 97,106 30,100 97,94"
              fill="rgba(200,168,75,.07)" stroke="rgba(200,168,75,.45)" stroke-width=".8"/>
            <!-- rune marks at cardinal points -->
            <rect x="96" y="5" width="8" height="3" fill="rgba(200,168,75,.5)" rx="1"/>
            <rect x="96" y="192" width="8" height="3" fill="rgba(200,168,75,.5)" rx="1"/>
            <rect x="5" y="98.5" width="3" height="8" fill="rgba(200,168,75,.5)" rx="1"/>
            <rect x="192" y="98.5" width="3" height="8" fill="rgba(200,168,75,.5)" rx="1"/>
            <!-- center gem -->
            <circle cx="100" cy="100" r="10" fill="none" stroke="rgba(200,168,75,.7)" stroke-width="1"/>
            <circle cx="100" cy="100" r="5" fill="#c8a84b"/>
            <circle cx="100" cy="100" r="2" fill="#04030a"/>
          </svg>
        </div>

        <!-- Stats -->
        <div class="stats-strip">
          <div class="stat">
            <span class="stat-num">24+</span>
            <span class="stat-label">Masterworks</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-num">CTR</span>
            <span class="stat-label">Optimised</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-num">∞</span>
            <span class="stat-label">Creativity</span>
          </div>
        </div>

        <p class="house-words">Fire &amp; Design — Conquer the Algorithm</p>
      </div>
    </div>

    <!-- ABOUT SECTION -->
    <section class="home-about">
      <div class="rev">
        <p class="about-col-label">The Grand Maester's Log</p>
        <h2 class="about-heading-big">Forged in<br/>Creative Fire</h2>
        <p class="about-body-text">
          Greetings, traveller. I am <strong>Nitin</strong> — a visual designer from the realms of tech and artistry. Like Valyrian steel, I forge YouTube thumbnails with precision, specialising in bold, aesthetic design that commands attention and <em>conquers the algorithm</em>.<br/><br/>
          Each thumbnail is a battle standard — crafted to boost your Click-Through Rate and make your channel reign supreme in its niche. When not locked in graphic design campaigns, I wander the ancient scrolls of web development.
        </p>
      </div>

      <div class="rev" style="transition-delay:.15s">
        <p class="about-col-label">Disciplines &amp; Craft</p>
        <ul class="rune-list">
          <li><span class="rune-glyph">✦</span>YouTube Thumbnail Design</li>
          <li><span class="rune-glyph">✦</span>CTR Optimisation Strategy</li>
          <li><span class="rune-glyph">✦</span>Visual Storytelling</li>
          <li><span class="rune-glyph">✦</span>Brand Identity &amp; Aesthetics</li>
          <li><span class="rune-glyph">✦</span>Web Development</li>
        </ul>
      </div>
    </section>

  </main>

  <!-- ══════════════════════════════════════════
       GALLERY PAGE
  ══════════════════════════════════════════ -->
  <main id="gallery" class="page">

    <!-- CINEMATIC HEADER -->
    <div class="gal-hero">
      <div class="gal-hero-bg-text">ARMORY</div>

      <nav class="gal-nav">
        <button class="shield-btn" onclick="openHome()">← Return to Keep</button>

        <div class="gal-header-center">
          <p class="gal-header-eyebrow">The Works of House Nitin</p>
          <h2 class="gal-header-title">The Armory</h2>
          <p class="gal-header-sub">Designs forged in the fires of creativity</p>
        </div>

        <div class="gal-count">
          <span class="gal-count-num">24</span>
          <span>Masterworks</span>
        </div>
      </nav>

      <!-- Filter Tabs -->
      <div class="filter-bar">
        <button class="filter-tab active" onclick="filterGallery('all',this)">All Works</button>
        <button class="filter-tab" onclick="filterGallery('png',this)">PNG Series</button>
        <button class="filter-tab" onclick="filterGallery('jpg',this)">JPG Series</button>
      </div>
    </div>

    <!-- GALLERY BODY -->
    <div class="gal-body">

      <!-- Featured horizontal scroll -->
      <div class="featured-strip">
        <p class="featured-label">Featured Pieces</p>
        <div class="scroll-row" id="featuredRow">
          <!-- injected by JS -->
        </div>
      </div>

      <!-- Main grid -->
      <p class="main-grid-label">All Masterworks</p>
      <div class="thumb-grid" id="thumbGrid">
        <!-- injected by JS -->
      </div>

    </div>
  </main>

  <!-- ══════════════════════════════════════════
       JAVASCRIPT
  ══════════════════════════════════════════ -->
  <script>
  /* ── CURSOR ── */
  const dot = document.getElementById('cur-dot');
  const ring = document.getElementById('cur-ring');
  document.addEventListener('mousemove', e => {
    dot.style.left = ring.style.left = e.clientX + 'px';
    dot.style.top  = ring.style.top  = e.clientY + 'px';
  });
  document.addEventListener('mouseover', e => {
    if (e.target.closest('button, a, .thumb-card, .scroll-card, .armory-item')) {
      document.body.classList.add('hovering');
    } else {
      document.body.classList.remove('hovering');
    }
  });

  /* ── FIRE CANVAS ── */
  (function(){
    const c = document.getElementById('fireCanvas');
    const ctx = c.getContext('2d');
    let W, H, pts = [];
    function resize(){ W = c.width = window.innerWidth; H = c.height = window.innerHeight; }
    resize(); window.addEventListener('resize', resize);
    class Pt {
      constructor(){ this.rst(); }
      rst(){
        this.x = Math.random()*W;
        this.y = H+8;
        this.vx = (Math.random()-.5)*.7;
        this.vy = -(Math.random()*1.6+.5);
        this.a = Math.random()*.35+.05;
        this.r = Math.random()*3+1;
        this.life = 0; this.max = Math.random()*160+80;
        const b=[255,200,160,120][0|Math.random()*4];
        this.col=`rgba(${b},${0|b*.38},8,`;
      }
      draw(){
        this.life++; this.x+=this.vx; this.y+=this.vy;
        this.vy-=.009; this.vx+=(Math.random()-.5)*.06;
        const t=this.life/this.max, a=this.a*(1-t*t);
        ctx.beginPath();
        ctx.arc(this.x,this.y,this.r*(1-t*.5),0,Math.PI*2);
        ctx.fillStyle=this.col+a+')'; ctx.fill();
        if(this.life>=this.max) this.rst();
      }
    }
    for(let i=0;i<55;i++){ const p=new Pt(); p.life=Math.random()*p.max; pts.push(p); }
    function loop(){ ctx.clearRect(0,0,W,H); pts.forEach(p=>p.draw()); requestAnimationFrame(loop); }
    loop();
  })();

  /* ── SCROLL REVEAL ── */
  const ro = new IntersectionObserver(es=>{
    es.forEach(e=>{ if(e.isIntersecting) e.target.classList.add('in'); });
  },{threshold:.12});
  document.querySelectorAll('.rev').forEach(el=>ro.observe(el));

  /* ── IMAGE DATA ── */
  const images = Array.from({length:24},(_,i)=>({
    src:`images/thumbnail${i+1}.${(i<6||i>=21)?'png':'jpg'}`,
    label:`Masterwork ${i+1}`,
    type:(i<6||i>=21)?'png':'jpg',
    featured: i < 6
  }));

  /* ── BUILD GALLERY ── */
  const featuredRow = document.getElementById('featuredRow');
  const thumbGrid   = document.getElementById('thumbGrid');

  images.forEach((img,i)=>{
    // Featured strip (first 6)
    if(img.featured){
      const sc = document.createElement('div');
      sc.className='scroll-card';
      sc.innerHTML=`
        <img src="${img.src}" alt="${img.label}" loading="lazy"
          onerror="this.closest('.scroll-card').style.display='none'"/>
        <div class="scroll-card-overlay"></div>`;
      sc.addEventListener('click',()=>openLb(i));
      featuredRow.appendChild(sc);
    }

    // Main grid
    const card = document.createElement('div');
    card.className='thumb-card';
    card.dataset.type=img.type;
    card.innerHTML=`
      <img src="${img.src}" alt="${img.label}" loading="lazy"
        onerror="this.closest('.thumb-card').style.display='none'"/>
      <div class="thumb-overlay">
        <span class="thumb-num">No. ${String(i+1).padStart(2,'0')}</span>
        <span class="thumb-cta">View Design</span>
      </div>`;
    card.addEventListener('click',()=>openLb(i));
    thumbGrid.appendChild(card);
  });

  /* ── FILTER ── */
  function filterGallery(type, btn){
    document.querySelectorAll('.filter-tab').forEach(t=>t.classList.remove('active'));
    btn.classList.add('active');
    document.querySelectorAll('.thumb-card').forEach(c=>{
      c.style.display = (type==='all'||c.dataset.type===type)?'':'none';
    });
  }

  /* ── LIGHTBOX ── */
  let lbIdx = 0;
  function openLb(idx){
    lbIdx = idx;
    document.getElementById('lb-img').src = images[idx].src;
    document.getElementById('lb-label').textContent = images[idx].label;
    document.getElementById('lightbox').classList.add('open');
  }
  function closeLb(){
    document.getElementById('lightbox').classList.remove('open');
  }
  function handleLbClick(e){
    if(e.target===document.getElementById('lightbox')) closeLb();
  }
  function lbNav(dir){
    lbIdx = (lbIdx + dir + images.length) % images.length;
    const img = document.getElementById('lb-img');
    img.style.opacity=0;
    setTimeout(()=>{
      img.src=images[lbIdx].src;
      document.getElementById('lb-label').textContent=images[lbIdx].label;
      img.style.opacity=1;
    },150);
    img.style.transition='opacity .15s';
  }
  document.addEventListener('keydown',e=>{
    if(e.key==='Escape') closeLb();
    if(e.key==='ArrowRight') lbNav(1);
    if(e.key==='ArrowLeft')  lbNav(-1);
  });

  /* ── PAGE NAV ── */
  function openGallery(){
    document.getElementById('home').classList.remove('active');
    document.getElementById('gallery').classList.add('active');
    window.scrollTo(0,0);
    document.getElementById('got-audio').play()
      .then(()=>{ document.getElementById('music-btn').style.display='block'; })
      .catch(()=>{});
  }
  function openHome(){
    document.getElementById('gallery').classList.remove('active');
    document.getElementById('home').classList.add('active');
    window.scrollTo(0,0);
  }

  /* ── MUSIC ── */
  let muted=false;
  document.getElementById('got-audio').volume=0.15;
  function toggleMusic(){
    const a=document.getElementById('got-audio');
    const b=document.getElementById('music-btn');
    muted=!muted; a.muted=muted;
    b.textContent=muted?'♪ Unmute':'♪ Silence';
  }
  </script>
</body>
</html>
