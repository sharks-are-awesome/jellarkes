<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Jellarkes — Jellyfish! Sharks! And Whales!</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=Nunito:wght@400;600;700&display=swap');

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --sky: #87CEEB;
    --ocean-blue: #1565C0;
    --ocean-mid: #1976D2;
    --ocean-green: #00695C;
    --dark-blue: #0D1B3E;
    --turquoise: #00BCD4;
    --deep: #0A2342;
    --surface: #E0F7FA;
    --light-teal: #B2EBF2;
    --text-bright: #E0F7FA;
    --text-muted: #80DEEA;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Nunito', sans-serif;
    background: var(--deep);
    color: var(--text-bright);
    overflow-x: hidden;
  }

  /* ── PAGES ── */
  .page { display: none; min-height: 100vh; }
  .page.active { display: block; }

  /* ── UNDERWATER BANNER ── */
  .banner {
    position: relative;
    height: 320px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: linear-gradient(180deg,
      #87CEEB 0%,
      #29B6F6 18%,
      #1565C0 40%,
      #0D47A1 65%,
      #0A2342 100%
    );
  }

  /* Water surface shimmer */
  .banner::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 36px;
    background: repeating-linear-gradient(
      90deg,
      rgba(255,255,255,0.18) 0px,
      rgba(255,255,255,0.04) 30px,
      rgba(255,255,255,0.22) 60px,
      rgba(255,255,255,0.06) 90px
    );
    border-bottom: 2px solid rgba(255,255,255,0.25);
  }

  /* Light rays */
  .rays {
    position: absolute;
    inset: 0;
    overflow: hidden;
    pointer-events: none;
  }
  .ray {
    position: absolute;
    top: 0;
    width: 50px;
    height: 100%;
    background: linear-gradient(180deg, rgba(255,255,255,0.09) 0%, transparent 100%);
    transform-origin: top center;
  }

  .banner-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.6rem, 5vw, 2.8rem);
    font-weight: 900;
    color: #E0F7FA;
    text-shadow: 0 3px 16px rgba(0,0,0,0.55);
    text-align: center;
    letter-spacing: 1px;
    z-index: 2;
    line-height: 1.2;
    padding: 0 16px;
  }
  .banner-sub {
    font-family: 'Nunito', sans-serif;
    font-size: 1rem;
    color: #80DEEA;
    text-align: center;
    margin-top: 8px;
    letter-spacing: 8px;
    text-transform: uppercase;
    z-index: 2;
  }
  .banner-desc {
    font-size: 0.82rem;
    color: rgba(176,230,240,0.85);
    text-align: center;
    margin-top: 10px;
    max-width: 340px;
    line-height: 1.55;
    z-index: 2;
    padding: 0 16px;
  }

  /* Floating bubbles */
  .bubble {
    position: absolute;
    border-radius: 50%;
    border: 1.5px solid rgba(255,255,255,0.28);
    background: radial-gradient(circle at 35% 35%, rgba(255,255,255,0.18), transparent 70%);
    pointer-events: none;
  }

  /* ── HOME BODY ── */
  .home-body {
    background: linear-gradient(180deg, #0D47A1 0%, #01579B 30%, #00695C 70%, #004D40 100%);
    padding: 36px 16px 60px;
    min-height: calc(100vh - 280px);
    position: relative;
    overflow: hidden;
  }

  /* ── NAV BUTTONS ── */
  .nav-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 14px;
    max-width: 480px;
    margin: 0 auto 44px;
    position: relative;
    z-index: 2;
  }

  .nav-btn {
    background: rgba(0,188,212,0.12);
    border: 2px solid rgba(0,188,212,0.6);
    border-radius: 18px;
    color: #E0F7FA;
    font-family: 'Nunito', sans-serif;
    font-size: 1.05rem;
    font-weight: 700;
    letter-spacing: 2px;
    padding: 22px 10px;
    cursor: pointer;
    text-align: center;
    transition: background 0.2s, transform 0.12s, border-color 0.2s;
    text-transform: uppercase;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
  }
  .nav-btn .btn-icon { font-size: 2rem; }
  .nav-btn:hover {
    background: rgba(0,188,212,0.28);
    border-color: #00BCD4;
    transform: translateY(-2px);
  }
  .nav-btn:active { transform: scale(0.97); }

  /* ── DECORATIVE CREATURES ── */
  .creature-section {
    position: relative;
    z-index: 2;
  }
  .section-label {
    text-align: center;
    font-size: 0.7rem;
    letter-spacing: 4px;
    text-transform: uppercase;
    color: var(--text-muted);
    margin-bottom: 16px;
  }
  .creature-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    max-width: 560px;
    margin: 0 auto;
  }
  .creature-card {
    background: rgba(255,255,255,0.06);
    border: 1px solid rgba(0,188,212,0.22);
    border-radius: 14px;
    padding: 14px 4px;
    text-align: center;
    transition: background 0.2s;
  }
  .creature-card:hover { background: rgba(0,188,212,0.12); }
  .creature-card .icon { font-size: 2rem; display: block; margin-bottom: 5px; }
  .creature-card .name {
    font-size: 0.62rem;
    color: var(--text-muted);
    letter-spacing: 1px;
    text-transform: uppercase;
  }

  /* ── INNER PAGES ── */
  .inner-header {
    background: linear-gradient(180deg, #1565C0 0%, #0D47A1 100%);
    padding: 20px 20px 18px;
    display: flex;
    align-items: center;
    gap: 14px;
    border-bottom: 2px solid rgba(0,188,212,0.35);
    position: sticky;
    top: 0;
    z-index: 10;
  }
  .back-btn {
    background: rgba(0,188,212,0.15);
    border: 1.5px solid rgba(0,188,212,0.5);
    border-radius: 10px;
    color: #E0F7FA;
    padding: 8px 16px;
    cursor: pointer;
    font-size: 0.82rem;
    font-family: 'Nunito', sans-serif;
    font-weight: 700;
    letter-spacing: 1px;
    white-space: nowrap;
    transition: background 0.15s;
  }
  .back-btn:hover { background: rgba(0,188,212,0.3); }

  .inner-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2rem, 6vw, 3.2rem);
    font-weight: 900;
    color: #E0F7FA;
    letter-spacing: 4px;
    text-shadow: 0 2px 10px rgba(0,0,0,0.4);
  }

  /* ── HERO IMAGE PANEL ── */
  .hero-panel {
    background: linear-gradient(180deg, #0D47A1 0%, #0A2342 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 40px 20px;
    min-height: 260px;
    position: relative;
    overflow: hidden;
  }
  .hero-emoji {
    font-size: clamp(8rem, 22vw, 14rem);
    filter: drop-shadow(0 8px 30px rgba(0,188,212,0.35));
    z-index: 2;
    position: relative;
  }
  .hero-panel::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 50% 60%, rgba(0,188,212,0.12) 0%, transparent 70%);
  }

  /* ── FACTS ── */
  .facts-body {
    background: linear-gradient(180deg, #0A3060 0%, #0A2342 100%);
    padding: 32px 20px 60px;
  }
  .facts-heading {
    font-size: 0.72rem;
    letter-spacing: 5px;
    text-transform: uppercase;
    color: var(--turquoise);
    margin-bottom: 20px;
    border-bottom: 1px solid rgba(0,188,212,0.25);
    padding-bottom: 10px;
  }
  .fact-item {
    display: flex;
    gap: 14px;
    margin-bottom: 18px;
    background: rgba(255,255,255,0.04);
    border-left: 3px solid var(--turquoise);
    border-radius: 0 12px 12px 0;
    padding: 16px 18px;
  }
  .fact-num {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    color: var(--turquoise);
    min-width: 28px;
    line-height: 1;
  }
  .fact-text { flex: 1; }
  .fact-text strong {
    display: block;
    color: #80DEEA;
    font-size: 0.78rem;
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 5px;
  }
  .fact-text p {
    font-size: 0.92rem;
    line-height: 1.65;
    color: #CFE8F3;
  }

  /* ── MEMORY GAME ── */
  .game-body {
    background: linear-gradient(180deg, #004D40 0%, #0A2342 100%);
    padding: 28px 16px 60px;
    min-height: calc(100vh - 80px);
  }
  .game-status {
    display: flex;
    gap: 12px;
    justify-content: center;
    margin-bottom: 24px;
    flex-wrap: wrap;
  }
  .stat-box {
    background: rgba(0,188,212,0.12);
    border: 1px solid rgba(0,188,212,0.3);
    border-radius: 12px;
    padding: 10px 20px;
    text-align: center;
    min-width: 80px;
  }
  .stat-box .stat-val {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: #80DEEA;
    display: block;
  }
  .stat-box .stat-lbl {
    font-size: 0.65rem;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text-muted);
  }

  .memory-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    max-width: 480px;
    margin: 0 auto 28px;
  }

  .mem-card {
    aspect-ratio: 1;
    border-radius: 12px;
    cursor: pointer;
    position: relative;
    transform-style: preserve-3d;
    transition: transform 0.45s;
  }
  .mem-card.flipped { transform: rotateY(180deg); }
  .mem-card.matched { opacity: 0.55; cursor: default; }

  .mem-front, .mem-back {
    position: absolute;
    inset: 0;
    border-radius: 12px;
    backface-visibility: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.8rem;
  }
  .mem-front {
    background: linear-gradient(135deg, #1565C0, #00BCD4);
    border: 2px solid rgba(0,188,212,0.4);
    color: rgba(255,255,255,0.35);
    font-size: 1.4rem;
  }
  .mem-back {
    background: linear-gradient(135deg, #004D40, #006064);
    border: 2px solid rgba(0,188,212,0.5);
    transform: rotateY(180deg);
  }

  .restart-btn {
    display: block;
    margin: 0 auto;
    background: rgba(0,188,212,0.15);
    border: 2px solid rgba(0,188,212,0.5);
    border-radius: 14px;
    color: #E0F7FA;
    font-family: 'Nunito', sans-serif;
    font-size: 0.9rem;
    font-weight: 700;
    letter-spacing: 2px;
    padding: 14px 36px;
    cursor: pointer;
    text-transform: uppercase;
    transition: background 0.15s;
  }
  .restart-btn:hover { background: rgba(0,188,212,0.3); }

  .win-msg {
    text-align: center;
    padding: 20px;
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: #80DEEA;
    display: none;
  }
  .win-msg.visible { display: block; }
</style>
</head>
<body>

<!-- ════════════════════ HOME PAGE ════════════════════ -->
<div id="home" class="page active">

  <div class="banner">
    <div class="rays">
      <div class="ray" style="left:4%;transform:rotate(-10deg)"></div>
      <div class="ray" style="left:18%;transform:rotate(-4deg)"></div>
      <div class="ray" style="left:34%;transform:rotate(2deg)"></div>
      <div class="ray" style="left:50%;transform:rotate(-1deg)"></div>
      <div class="ray" style="left:66%;transform:rotate(5deg)"></div>
      <div class="ray" style="left:82%;transform:rotate(-6deg)"></div>
    </div>
    <div class="bubble" style="width:20px;height:20px;bottom:55px;left:12%"></div>
    <div class="bubble" style="width:11px;height:11px;bottom:95px;left:30%"></div>
    <div class="bubble" style="width:26px;height:26px;bottom:38px;right:18%"></div>
    <div class="bubble" style="width:8px;height:8px;bottom:115px;right:35%"></div>
    <div class="bubble" style="width:16px;height:16px;bottom:70px;left:58%"></div>
    <div class="bubble" style="width:13px;height:13px;bottom:42px;left:44%"></div>
    <div class="banner-title">Jellyfish! Sharks! And Whales!</div>
    <div class="banner-sub">Jellarkes</div>
    <div class="banner-desc">Your guide to the ocean's most amazing creatures — explore shark facts, jellyfish wonders, whale secrets, and test your memory!</div>
  </div>

  <div class="home-body">

    <div class="nav-grid">
      <button class="nav-btn" onclick="showPage('sharks')">
        <span class="btn-icon">🦈</span>SHARK
      </button>
      <button class="nav-btn" onclick="showPage('jellyfish')">
        <span class="btn-icon">🪼</span>Jellyfish
      </button>
      <button class="nav-btn" onclick="showPage('whales')">
        <span class="btn-icon">🐋</span>Whales
      </button>
      <button class="nav-btn" onclick="showPage('funfact')">
        <span class="btn-icon">🎮</span>Memory Game
      </button>
    </div>

    <div class="creature-section">
      <p class="section-label">Creatures of the Deep</p>
      <div class="creature-grid">
        <div class="creature-card"><span class="icon">🦈</span><span class="name">Shark</span></div>
        <div class="creature-card"><span class="icon">🪼</span><span class="name">Jellyfish</span></div>
        <div class="creature-card"><span class="icon">🐋</span><span class="name">Whale</span></div>
        <div class="creature-card"><span class="icon">🐡</span><span class="name">Pufferfish</span></div>
        <div class="creature-card"><span class="icon">🐙</span><span class="name">Octopus</span></div>
        <div class="creature-card"><span class="icon">🐠</span><span class="name">Clownfish</span></div>
        <div class="creature-card"><span class="icon">🦑</span><span class="name">Squid</span></div>
        <div class="creature-card"><span class="icon">🦭</span><span class="name">Seal</span></div>
        <div class="creature-card"><span class="icon">🐢</span><span class="name">Turtle</span></div>
        <div class="creature-card"><span class="icon">🦐</span><span class="name">Shrimp</span></div>
        <div class="creature-card"><span class="icon">🦀</span><span class="name">Crab</span></div>
        <div class="creature-card"><span class="icon">🐬</span><span class="name">Dolphin</span></div>
      </div>
    </div>

  </div>
</div>

<!-- ════════════════════ PAGE 1: SHARKS ════════════════════ -->
<div id="sharks" class="page">
  <div class="inner-header">
    <button class="back-btn" onclick="showPage('home')">← Back</button>
    <div class="inner-title">SHARKS</div>
  </div>
  <div class="hero-panel">
    <div class="bubble" style="width:14px;height:14px;top:30px;left:15%;opacity:0.5"></div>
    <div class="bubble" style="width:22px;height:22px;bottom:25px;right:12%;opacity:0.4"></div>
    <div class="bubble" style="width:9px;height:9px;top:60px;right:30%;opacity:0.5"></div>
    <span class="hero-emoji">🦈</span>
  </div>
  <div class="facts-body">
    <p class="facts-heading">Shark Facts</p>
    <div class="fact-item"><div class="fact-num">1</div><div class="fact-text"><strong>Ancient Predators</strong><p>Sharks have existed for over 450 million years — they predate the dinosaurs by more than 200 million years and survived five mass extinctions.</p></div></div>
    <div class="fact-item"><div class="fact-num">2</div><div class="fact-text"><strong>No Bones</strong><p>A shark's entire skeleton is made of cartilage, the same flexible material in your ears. This makes them lighter and more agile in water.</p></div></div>
    <div class="fact-item"><div class="fact-num">3</div><div class="fact-text"><strong>Endless Teeth</strong><p>Sharks can produce over 30,000 teeth in a lifetime. Rows of teeth grow constantly behind the front ones, replacing any that are lost within days.</p></div></div>
    <div class="fact-item"><div class="fact-num">4</div><div class="fact-text"><strong>Electric Sixth Sense</strong><p>Sharks detect the electrical fields of other animals using special organs called the Ampullae of Lorenzini — they can sense one billionth of a volt.</p></div></div>
    <div class="fact-item"><div class="fact-num">5</div><div class="fact-text"><strong>The Gentle Giant</strong><p>The whale shark is the world's largest fish at up to 12 metres long — yet it feeds entirely on tiny plankton by filter-feeding like a gentle vacuum.</p></div></div>
    <div class="fact-item"><div class="fact-num">6</div><div class="fact-text"><strong>Swimming Sleep</strong><p>Many sharks must keep swimming to breathe. Some rest parts of their brain while still moving — a kind of half-asleep, half-awake swimming state.</p></div></div>
    <div class="fact-item"><div class="fact-num">7</div><div class="fact-text"><strong>Skin Like Sandpaper</strong><p>Shark skin is covered in tiny tooth-like scales called dermal denticles, making it feel like sandpaper and reducing drag as they swim.</p></div></div>
  </div>
</div>

<!-- ════════════════════ PAGE 2: JELLYFISH ════════════════════ -->
<div id="jellyfish" class="page">
  <div class="inner-header">
    <button class="back-btn" onclick="showPage('home')">← Back</button>
    <div class="inner-title">JELLYFISH</div>
  </div>
  <div class="hero-panel">
    <div class="bubble" style="width:18px;height:18px;top:25px;left:20%;opacity:0.45"></div>
    <div class="bubble" style="width:10px;height:10px;bottom:40px;right:22%;opacity:0.4"></div>
    <span class="hero-emoji">🪼</span>
  </div>
  <div class="facts-body">
    <p class="facts-heading">Jellyfish Facts</p>
    <div class="fact-item"><div class="fact-num">1</div><div class="fact-text"><strong>No Brain, No Heart</strong><p>Jellyfish have no brain, no heart, no eyes, and no bones. Their bodies are 95% water, and they've managed perfectly well for 500 million years.</p></div></div>
    <div class="fact-item"><div class="fact-num">2</div><div class="fact-text"><strong>The Immortal Jellyfish</strong><p>Turritopsis dohrnii can revert back to its juvenile polyp form after reaching adulthood, restarting its life cycle — making it potentially immortal.</p></div></div>
    <div class="fact-item"><div class="fact-num">3</div><div class="fact-text"><strong>Deadly Sting</strong><p>The box jellyfish is one of the most venomous creatures on Earth. Its sting can stop a human heart within minutes of contact.</p></div></div>
    <div class="fact-item"><div class="fact-num">4</div><div class="fact-text"><strong>Natural Glow</strong><p>Many jellyfish are bioluminescent, producing blue-green light through chemical reactions in their bodies — creating living underwater lanterns.</p></div></div>
    <div class="fact-item"><div class="fact-num">5</div><div class="fact-text"><strong>A Smack of Jellyfish</strong><p>A group of jellyfish is called a "bloom" or a "smack." Some blooms contain millions of jellyfish and can stretch for many kilometres of ocean.</p></div></div>
    <div class="fact-item"><div class="fact-num">6</div><div class="fact-text"><strong>The Lion's Mane</strong><p>The lion's mane jellyfish is the largest species known. Its tentacles can stretch over 36 metres — longer than a blue whale — trailing behind it like ribbons.</p></div></div>
    <div class="fact-item"><div class="fact-num">7</div><div class="fact-text"><strong>No Gills Needed</strong><p>Jellyfish absorb oxygen directly through their thin, transparent skin from the surrounding seawater — no gills or lungs required.</p></div></div>
  </div>
</div>

<!-- ════════════════════ PAGE 3: WHALES ════════════════════ -->
<div id="whales" class="page">
  <div class="inner-header">
    <button class="back-btn" onclick="showPage('home')">← Back</button>
    <div class="inner-title">WHALES</div>
  </div>
  <div class="hero-panel">
    <div class="bubble" style="width:20px;height:20px;top:20px;left:10%;opacity:0.45"></div>
    <div class="bubble" style="width:12px;height:12px;bottom:35px;right:15%;opacity:0.4"></div>
    <div class="bubble" style="width:8px;height:8px;top:55px;right:25%;opacity:0.5"></div>
    <span class="hero-emoji">🐋</span>
  </div>
  <div class="facts-body">
    <p class="facts-heading">Whale Facts</p>
    <div class="fact-item"><div class="fact-num">1</div><div class="fact-text"><strong>Largest Animal Ever</strong><p>The blue whale is the largest animal ever known to exist on Earth, reaching 33 metres and weighing up to 200 tonnes — heavier than 30 elephants.</p></div></div>
    <div class="fact-item"><div class="fact-num">2</div><div class="fact-text"><strong>Whale Song</strong><p>Humpback whales sing elaborate songs lasting up to 20 hours. Scientists believe these songs travel across entire ocean basins at low frequencies.</p></div></div>
    <div class="fact-item"><div class="fact-num">3</div><div class="fact-text"><strong>Ancient Mariners</strong><p>Bowhead whales can live over 200 years. Scientists found one with a harpoon tip from the 1800s embedded in its blubber — it had survived the attack.</p></div></div>
    <div class="fact-item"><div class="fact-num">4</div><div class="fact-text"><strong>Deep Divers</strong><p>Sperm whales dive beyond 2,000 metres and hold their breath up to 90 minutes to hunt giant squid in total darkness on the ocean floor.</p></div></div>
    <div class="fact-item"><div class="fact-num">5</div><div class="fact-text"><strong>They Are Mammals</strong><p>Whales breathe air, give birth to live young, and nurse their calves on rich milk. They evolved from land-dwelling ancestors about 50 million years ago.</p></div></div>
    <div class="fact-item"><div class="fact-num">6</div><div class="fact-text"><strong>The Narwhal's Tusk</strong><p>The narwhal's spiral "horn" is actually a long tooth — a tusk that can reach 3 metres and contains up to 10 million nerve endings sensitive to pressure and temperature.</p></div></div>
    <div class="fact-item"><div class="fact-num">7</div><div class="fact-text"><strong>Carbon Heroes</strong><p>When whales die, they sink and carry tonnes of carbon to the seafloor. One whale can sequester as much carbon as 1,000 trees over its lifetime.</p></div></div>
  </div>
</div>

<!-- ════════════════════ PAGE 4: MEMORY GAME ════════════════════ -->
<div id="funfact" class="page">
  <div class="inner-header">
    <button class="back-btn" onclick="showPage('home')">← Back</button>
    <div class="inner-title" style="font-size:clamp(1.4rem,4vw,2.4rem)">Memory Game</div>
  </div>
  <div class="game-body">
    <div class="game-status">
      <div class="stat-box">
        <span class="stat-val" id="moves">0</span>
        <span class="stat-lbl">Moves</span>
      </div>
      <div class="stat-box">
        <span class="stat-val" id="pairs">0</span>
        <span class="stat-lbl">Pairs</span>
      </div>
      <div class="stat-box">
        <span class="stat-val" id="timer">0s</span>
        <span class="stat-lbl">Time</span>
      </div>
    </div>

    <div class="memory-grid" id="memGrid"></div>
    <div class="win-msg" id="winMsg">🎉 You matched them all!<br><span style="font-size:1rem;font-family:'Nunito',sans-serif;color:#B2EBF2;">Well done, ocean explorer!</span></div>
    <button class="restart-btn" onclick="initGame()">🔄 New Game</button>
  </div>
</div>

<script>
  /* ── PAGE NAV ── */
  function showPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    window.scrollTo(0, 0);
    if (id === 'funfact') initGame();
  }

  /* ── MEMORY GAME ── */
  const EMOJIS = ['🦈','🪼','🐋','🐡','🐙','🐠','🦑','🐬'];
  let flipped = [], matched = 0, moves = 0, locked = false;
  let timerInterval = null, seconds = 0, gameStarted = false;

  function shuffle(arr) {
    return [...arr].sort(() => Math.random() - 0.5);
  }

  function initGame() {
    clearInterval(timerInterval);
    seconds = 0; moves = 0; matched = 0; gameStarted = false; flipped = []; locked = false;
    document.getElementById('moves').textContent = 0;
    document.getElementById('pairs').textContent = 0;
    document.getElementById('timer').textContent = '0s';
    document.getElementById('winMsg').classList.remove('visible');

    const deck = shuffle([...EMOJIS, ...EMOJIS]);
    const grid = document.getElementById('memGrid');
    grid.innerHTML = '';

    deck.forEach((emoji, i) => {
      const card = document.createElement('div');
      card.className = 'mem-card';
      card.dataset.emoji = emoji;
      card.dataset.index = i;
      card.innerHTML = `
        <div class="mem-front">🌊</div>
        <div class="mem-back">${emoji}</div>
      `;
      card.addEventListener('click', () => flipCard(card));
      grid.appendChild(card);
    });
  }

  function startTimer() {
    timerInterval = setInterval(() => {
      seconds++;
      document.getElementById('timer').textContent = seconds + 's';
    }, 1000);
  }

  function flipCard(card) {
    if (locked || card.classList.contains('flipped') || card.classList.contains('matched')) return;
    if (!gameStarted) { gameStarted = true; startTimer(); }

    card.classList.add('flipped');
    flipped.push(card);

    if (flipped.length === 2) {
      locked = true;
      moves++;
      document.getElementById('moves').textContent = moves;
      checkMatch();
    }
  }

  function checkMatch() {
    const [a, b] = flipped;
    if (a.dataset.emoji === b.dataset.emoji) {
      a.classList.add('matched');
      b.classList.add('matched');
      matched++;
      document.getElementById('pairs').textContent = matched;
      flipped = [];
      locked = false;
      if (matched === EMOJIS.length) {
        clearInterval(timerInterval);
        setTimeout(() => document.getElementById('winMsg').classList.add('visible'), 400);
      }
    } else {
      setTimeout(() => {
        a.classList.remove('flipped');
        b.classList.remove('flipped');
        flipped = [];
        locked = false;
      }, 900);
    }
  }
</script>
</body>
</html>
