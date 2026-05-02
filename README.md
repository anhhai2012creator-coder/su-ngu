<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pokemon Odyssey Ultimate</title>
  <style>
    * { box-sizing: border-box; }
    :root{
      --bg1:#0f172a;
      --bg2:#1d4ed8;
      --glass:rgba(255,255,255,.12);
      --glass2:rgba(255,255,255,.18);
      --line:rgba(255,255,255,.16);
      --text:#eff6ff;
      --muted:#cbd5e1;
      --yellow:#facc15;
      --green:#4ade80;
      --red:#fb7185;
      --blue:#60a5fa;
      --purple:#a78bfa;
      --radius:24px;
      --shadow:0 18px 45px rgba(0,0,0,.25);
    }

    body{
      margin:0;
      font-family:system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;
      color:var(--text);
      min-height:100vh;
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.20), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(250,204,21,.18), transparent 18%),
        linear-gradient(135deg, var(--bg1), var(--bg2));
      transition:background .35s;
      overflow-x:hidden;
    }

    body.theme-forest{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.18), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(134,239,172,.20), transparent 18%),
        linear-gradient(135deg, #0b1320, #14532d 45%, #0f766e 100%);
    }
    body.theme-cave{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.14), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(148,163,184,.18), transparent 18%),
        linear-gradient(135deg, #0f172a, #1e293b 45%, #334155 100%);
    }
    body.theme-volcano{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.16), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(251,146,60,.22), transparent 18%),
        linear-gradient(135deg, #1f2937, #7f1d1d 45%, #ea580c 100%);
    }
    body.theme-ocean{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.16), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(125,211,252,.20), transparent 18%),
        linear-gradient(135deg, #082f49, #075985 45%, #2563eb 100%);
    }
    body.theme-sky{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.18), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(196,181,253,.25), transparent 18%),
        linear-gradient(135deg, #312e81, #2563eb 45%, #7c3aed 100%);
    }

    .app{
      max-width:1400px;
      margin:0 auto;
      padding:18px;
    }

    .topbar{
      display:flex;
      justify-content:space-between;
      gap:14px;
      flex-wrap:wrap;
      align-items:flex-start;
      margin-bottom:14px;
    }
    .brand h1{
      margin:0;
      font-size:clamp(28px, 4vw, 52px);
      line-height:1;
      letter-spacing:-1.5px;
    }
    .brand p{
      margin:8px 0 0;
      color:var(--muted);
      max-width:760px;
    }

    .stats{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      justify-content:flex-end;
    }
    .stat-pill{
      padding:10px 14px;
      border-radius:999px;
      background:rgba(0,0,0,.22);
      border:1px solid var(--line);
      backdrop-filter:blur(12px);
      font-weight:800;
      box-shadow:var(--shadow);
    }

    .tabs{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:14px;
    }
    .tab-btn{
      border:none;
      cursor:pointer;
      padding:12px 14px;
      border-radius:16px;
      background:rgba(255,255,255,.10);
      color:var(--text);
      font-weight:800;
      border:1px solid var(--line);
      backdrop-filter:blur(10px);
      transition:.18s;
    }
    .tab-btn.active,
    .tab-btn:hover{
      transform:translateY(-1px);
      background:rgba(255,255,255,.22);
    }

    .pane{
      display:none;
      grid-template-columns:1fr;
      gap:14px;
    }
    .pane.active{ display:grid; }

    .grid-2{ display:grid; grid-template-columns:1.08fr .92fr; gap:14px; }
    .grid-3{ display:grid; grid-template-columns:1fr 1fr 1fr; gap:14px; }

    .card{
      background:var(--glass);
      border:1px solid var(--line);
      border-radius:var(--radius);
      padding:16px;
      box-shadow:var(--shadow);
      backdrop-filter:blur(16px);
    }
    .card h2, .card h3{
      margin:0 0 12px;
    }
    .sub{
      color:var(--muted);
      font-size:14px;
    }

    .zone-strip{
      display:grid;
      grid-template-columns:repeat(5, 1fr);
      gap:10px;
      margin-top:10px;
    }
    .zone-card{
      background:rgba(0,0,0,.18);
      border:1px solid var(--line);
      border-radius:18px;
      padding:12px;
      cursor:pointer;
      transition:.16s;
    }
    .zone-card:hover,
    .zone-card.active{
      background:rgba(255,255,255,.22);
      transform:translateY(-1px);
    }
    .zone-card.locked{
      opacity:.45;
      cursor:not-allowed;
    }
    .zone-card b{ display:block; margin-bottom:4px; }

    .explore-actions{
      display:grid;
      grid-template-columns:repeat(5, 1fr);
      gap:10px;
    }
    .action-card{
      background:rgba(255,255,255,.10);
      border:1px solid var(--line);
      border-radius:18px;
      padding:14px;
      cursor:pointer;
      transition:.16s;
      min-height:125px;
    }
    .action-card:hover{
      transform:translateY(-2px);
      background:rgba(255,255,255,.20);
    }
    .action-card .icon{
      font-size:28px;
      margin-bottom:8px;
    }

    .big-btn, .small-btn{
      border:none;
      border-radius:16px;
      cursor:pointer;
      font-weight:800;
      transition:.15s;
      box-shadow:0 8px 18px rgba(0,0,0,.18);
    }
    .big-btn{
      padding:12px 16px;
      background:linear-gradient(135deg, #fde68a, #facc15);
      color:#111827;
    }
    .small-btn{
      padding:9px 12px;
      background:rgba(255,255,255,.92);
      color:#111827;
    }
    .big-btn:hover, .small-btn:hover{ transform:translateY(-1px); }
    .btn-green{ background:linear-gradient(135deg, #bbf7d0, #4ade80); color:#062a12; }
    .btn-red{ background:linear-gradient(135deg, #fecdd3, #fb7185); color:#3b0712; }
    .btn-blue{ background:linear-gradient(135deg, #dbeafe, #60a5fa); color:#0c2340; }
    .btn-purple{ background:linear-gradient(135deg, #ede9fe, #a78bfa); color:#241449; }

    .log{
      height:190px;
      overflow:auto;
      border-radius:18px;
      background:rgba(0,0,0,.22);
      border:1px solid var(--line);
      padding:12px;
      line-height:1.45;
      font-size:14px;
    }

    .battle-scene{
      position:relative;
      min-height:390px;
      border-radius:24px;
      overflow:hidden;
      border:1px solid var(--line);
      background:linear-gradient(180deg, rgba(255,255,255,.22), rgba(0,0,0,.12));
    }
    .battle-scene::before{
      content:"";
      position:absolute; inset:0;
      background:
        radial-gradient(circle at 75% 18%, rgba(255,255,255,.78) 0 7%, transparent 8%),
        linear-gradient(transparent 65%, rgba(0,0,0,.18) 66%);
      opacity:.7;
    }
    .battle-scene.forest{ background:linear-gradient(180deg, #7dd3fc, #34d399 58%, #14532d); }
    .battle-scene.cave{ background:linear-gradient(180deg, #64748b, #1f2937 60%, #0f172a); }
    .battle-scene.volcano{ background:linear-gradient(180deg, #fdba74, #b91c1c 58%, #111827); }
    .battle-scene.ocean{ background:linear-gradient(180deg, #bae6fd, #0ea5e9 58%, #082f49); }
    .battle-scene.sky{ background:linear-gradient(180deg, #ddd6fe, #60a5fa 60%, #312e81); }

    .arena-shadow{
      position:absolute;
      width:200px; height:56px;
      border-radius:50%;
      background:radial-gradient(ellipse, rgba(255,255,255,.35), rgba(0,0,0,.20));
      bottom:34px;
      filter:blur(1px);
    }
    .arena-shadow.left{ left:40px; }
    .arena-shadow.right{ right:40px; top:auto; bottom:104px; }

    .poke{
      position:absolute;
      width:180px;
      height:180px;
      object-fit:contain;
      z-index:3;
      filter:drop-shadow(0 18px 18px rgba(0,0,0,.35));
      transition:transform .26s, filter .26s;
    }
    .poke.player{ left:42px; bottom:48px; transform:scaleX(-1); }
    .poke.enemy{ right:42px; bottom:110px; }
    .poke.hit{ animation:hit .35s ease-in-out; }
    .poke.attack{ animation:attack .42s ease-in-out; }

    @keyframes hit{
      0%,100%{ filter:drop-shadow(0 18px 18px rgba(0,0,0,.35)); }
      50%{ filter:brightness(1.9) drop-shadow(0 0 18px #fff); transform:translateX(12px); }
    }
    @keyframes attack{
      0%,100%{}
      50%{ transform:translateX(34px) scale(1.08); }
    }

    .battle-hud{
      display:grid;
      grid-template-columns:1fr 1fr;
      gap:12px;
      margin-top:12px;
    }
    .hud-card{
      padding:12px;
      border-radius:18px;
      background:rgba(0,0,0,.18);
      border:1px solid var(--line);
    }
    .hud-head{
      display:flex;
      justify-content:space-between;
      gap:8px;
      font-weight:900;
    }
    .bar{
      height:12px;
      border-radius:999px;
      overflow:hidden;
      background:rgba(0,0,0,.30);
      margin-top:8px;
    }
    .bar span{
      display:block;
      height:100%;
      border-radius:999px;
      transition:width .3s;
    }
    .hp{ background:linear-gradient(90deg, #22c55e, #eab308, #ef4444); }
    .en{ background:linear-gradient(90deg, #38bdf8, #a78bfa); }

    .move-grid{
      display:grid;
      grid-template-columns:repeat(2, 1fr);
      gap:10px;
      margin-top:12px;
    }
    .move-btn{
      text-align:left;
      padding:12px;
      border:none;
      border-radius:18px;
      cursor:pointer;
      background:rgba(255,255,255,.92);
      color:#111827;
      box-shadow:0 8px 16px rgba(0,0,0,.12);
      transition:.15s;
    }
    .move-btn:hover{ transform:translateY(-1px); }
    .move-btn:disabled{ opacity:.45; cursor:not-allowed; }
    .move-btn small{
      display:block;
      margin-top:4px;
      color:#334155;
      font-weight:700;
    }

    .inline-actions{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-top:12px;
    }

    .team-grid, .dex-grid, .evo-grid, .shop-grid{
      display:grid;
      grid-template-columns:repeat(auto-fill, minmax(170px, 1fr));
      gap:10px;
    }
    .mini-mon{
      background:rgba(255,255,255,.12);
      border:1px solid var(--line);
      border-radius:18px;
      padding:10px;
      text-align:center;
      cursor:pointer;
      transition:.15s;
    }
    .mini-mon:hover, .mini-mon.active{
      transform:translateY(-1px);
      background:rgba(255,255,255,.24);
    }
    .mini-mon img{
      width:84px;
      height:84px;
      object-fit:contain;
      filter:drop-shadow(0 12px 12px rgba(0,0,0,.25));
    }

    .type-wrap{
      display:flex;
      flex-wrap:wrap;
      gap:4px;
      justify-content:center;
      margin-top:6px;
    }
    .type{
      font-size:11px;
      padding:4px 8px;
      border-radius:999px;
      background:rgba(0,0,0,.24);
      font-weight:800;
    }

    .search-row{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:12px;
    }
    input, select{
      padding:12px 14px;
      border-radius:14px;
      border:1px solid var(--line);
      background:rgba(255,255,255,.12);
      color:var(--text);
      outline:none;
      min-width:160px;
    }
    input::placeholder{ color:#e2e8f0; }

    .dex-list{
      display:grid;
      grid-template-columns:repeat(auto-fill, minmax(130px, 1fr));
      gap:10px;
      max-height:540px;
      overflow:auto;
      padding-right:4px;
    }
    .dex-item{
      background:rgba(255,255,255,.10);
      border:1px solid var(--line);
      border-radius:16px;
      padding:10px;
      text-align:center;
      cursor:pointer;
      transition:.15s;
    }
    .dex-item:hover{
      transform:translateY(-1px);
      background:rgba(255,255,255,.20);
    }
    .dex-item img{
      width:72px;
      height:72px;
      object-fit:contain;
    }

    .detail-grid{
      display:grid;
      grid-template-columns:repeat(2, 1fr);
      gap:10px;
    }
    .detail-box{
      background:rgba(0,0,0,.18);
      border:1px solid var(--line);
      border-radius:18px;
      padding:12px;
    }

    .badge-list{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
    }
    .badge{
      padding:10px 12px;
      border-radius:999px;
      background:rgba(255,255,255,.14);
      border:1px solid var(--line);
      font-weight:800;
    }

    .shop-item{
      background:rgba(255,255,255,.12);
      border:1px solid var(--line);
      border-radius:18px;
      padding:12px;
    }

    .toast{
      position:fixed;
      left:50%;
      bottom:18px;
      transform:translateX(-50%);
      padding:12px 16px;
      border-radius:999px;
      background:rgba(0,0,0,.76);
      border:1px solid var(--line);
      display:none;
      z-index:99;
      font-weight:800;
    }

    .fx-layer{
      position:absolute;
      inset:0;
      z-index:5;
      pointer-events:none;
      overflow:hidden;
    }
    .fx-shot{
      position:absolute;
      opacity:0;
      animation:fxfly .7s ease-out forwards;
    }
    .fx-ring{
      position:absolute;
      border-radius:50%;
      opacity:0;
      animation:fxring .65s ease-out forwards;
      border:6px solid white;
    }
    .fx-burst{
      position:absolute;
      border-radius:50%;
      opacity:0;
      animation:fxburst .7s ease-out forwards;
    }

    @keyframes fxfly{
      0%{ transform:translate(0,0) scale(.5); opacity:1; }
      100%{ transform:translate(var(--dx), var(--dy)) scale(1.3) rotate(360deg); opacity:0; }
    }
    @keyframes fxring{
      0%{ transform:scale(.2); opacity:0; }
      35%{ opacity:1; }
      100%{ transform:scale(1.7); opacity:0; }
    }
    @keyframes fxburst{
      0%{ transform:scale(.2); opacity:0; }
      45%{ opacity:1; }
      100%{ transform:scale(1.8); opacity:0; }
    }

    @media (max-width:1100px){
      .grid-2, .grid-3{ grid-template-columns:1fr; }
      .zone-strip{ grid-template-columns:repeat(2, 1fr); }
      .explore-actions{ grid-template-columns:repeat(2, 1fr); }
    }
    @media (max-width:720px){
      .move-grid, .battle-hud{ grid-template-columns:1fr; }
      .poke{ width:126px; height:126px; }
      .poke.player{ left:12px; }
      .poke.enemy{ right:12px; }
      .zone-strip, .explore-actions{ grid-template-columns:1fr; }
    }
  </style>
</head>
<body class="theme-forest">
  <div class="app">
    <div class="topbar">
      <div class="brand">
        <h1>Pokémon Odyssey Ultimate</h1>
        <p>Bản mở rộng lớn: nhiều tab riêng, Pokédex/Từ điển Pokémon, tiến hoá nhiều kiểu, khám phá đa dạng, thêm nhiều Pokémon, hiệu ứng chiêu thức đẹp và hành trình phong phú hơn.</p>
      </div>
      <div class="stats" id="topStats"></div>
    </div>

    <div class="tabs" id="tabs"></div>

    <section class="pane active" id="tab-explore"></section>
    <section class="pane" id="tab-battle"></section>
    <section class="pane" id="tab-team"></section>
    <section class="pane" id="tab-dex"></section>
    <section class="pane" id="tab-evolution"></section>
    <section class="pane" id="tab-journey"></section>
    <section class="pane" id="tab-shop"></section>
  </div>

  <div class="toast" id="toast"></div>

  <script>
    const API = "https://pokeapi.co/api/v2";
    const MAX_POKEMON = 251;

    const zones = [
      { id:0, name:"Verdant Forest", theme:"forest", min:1,   max:60,  unlock:0, desc:"Cỏ, bọ, chim, sinh vật rừng", badge:"Leaf Badge" },
      { id:1, name:"Crystal Cave",   theme:"cave",   min:41,  max:110, unlock:1, desc:"Đá, độc, chiến binh hang động", badge:"Stone Badge" },
      { id:2, name:"Blazing Volcano",theme:"volcano",min:56,  max:146, unlock:2, desc:"Lửa, đất, quái vật nóng chảy", badge:"Flame Badge" },
      { id:3, name:"Azure Coast",    theme:"ocean",  min:72,  max:186, unlock:3, desc:"Nước, băng, sinh vật đại dương", badge:"Wave Badge" },
      { id:4, name:"Sky Temple",     theme:"sky",    min:120, max:251, unlock:4, desc:"Tâm linh, rồng, hiếm và huyền thoại", badge:"Legend Badge" }
    ];

    const exploreModes = [
      { id:"wander", icon:"🌿", name:"Rảo quanh", desc:"Gặp Pokémon ngẫu nhiên, dễ nhặt item." },
      { id:"rare", icon:"✨", name:"Săn hiếm", desc:"Tăng cơ hội gặp Pokémon hiếm và mạnh." },
      { id:"water", icon:"🎣", name:"Tìm nguồn nước", desc:"Dễ gặp hệ Nước / Băng / Điện." },
      { id:"ruins", icon:"🏛️", name:"Khám phá phế tích", desc:"Có thể gặp hệ Tâm linh / Ma / Đá." },
      { id:"camp", icon:"⛺", name:"Dựng trại", desc:"Hồi đội, tăng tình bạn, nhận sự kiện nghỉ ngơi." }
    ];

    const itemCatalog = {
      pokeBall:      { name:"Poké Ball", price:80, emoji:"⚪", desc:"Bắt Pokémon thường." },
      greatBall:     { name:"Great Ball", price:180, emoji:"🔵", desc:"Tăng tỉ lệ bắt." },
      potion:        { name:"Potion", price:60, emoji:"🧪", desc:"+35 HP cho 1 Pokémon." },
      superPotion:   { name:"Super Potion", price:120, emoji:"💊", desc:"+70 HP cho 1 Pokémon." },
      rareCandy:     { name:"Rare Candy", price:250, emoji:"🍬", desc:"+1 cấp cho 1 Pokémon." },
      fireStone:     { name:"Fire Stone", price:400, emoji:"🔥", desc:"Tiến hoá bằng đá lửa." },
      waterStone:    { name:"Water Stone", price:400, emoji:"💧", desc:"Tiến hoá bằng đá nước." },
      thunderStone:  { name:"Thunder Stone", price:400, emoji:"⚡", desc:"Tiến hoá bằng đá điện." },
      leafStone:     { name:"Leaf Stone", price:400, emoji:"🍃", desc:"Tiến hoá bằng đá lá." },
      moonStone:     { name:"Moon Stone", price:420, emoji:"🌙", desc:"Tiến hoá bằng đá mặt trăng." },
      sunStone:      { name:"Sun Stone", price:420, emoji:"☀️", desc:"Tiến hoá bằng đá mặt trời." },
      linkCable:     { name:"Link Cable", price:360, emoji:"🔗", desc:"Mô phỏng trade evolution." },
      friendshipCharm:{ name:"Friendship Charm", price:300, emoji:"💖", desc:"+40 friendship cho 1 Pokémon." },
      evoShard:      { name:"Evolution Shard", price:500, emoji:"💠", desc:"Dùng cho vài tiến hoá đặc biệt." }
    };

    const typeMoves = {
      normal: [
        { name:"Quick Strike", power:18, cost:0, fx:"normal" },
        { name:"Double Hit", power:26, cost:10, fx:"normal" },
        { name:"Hyper Dash", power:42, cost:24, fx:"normal" },
        { name:"Omega Rush", power:62, cost:42, fx:"normal" }
      ],
      fire: [
        { name:"Ember Burst", power:20, cost:0, fx:"fire" },
        { name:"Flame Wheel", power:28, cost:10, fx:"fire" },
        { name:"Inferno Fang", power:46, cost:26, fx:"fire" },
        { name:"Solar Inferno", power:68, cost:48, fx:"fire" }
      ],
      water: [
        { name:"Bubble Jet", power:18, cost:0, fx:"water" },
        { name:"Aqua Slash", power:28, cost:10, fx:"water" },
        { name:"Tidal Crush", power:44, cost:24, fx:"water" },
        { name:"Ocean Cataclysm", power:66, cost:46, fx:"water" }
      ],
      grass: [
        { name:"Leaf Cutter", power:18, cost:0, fx:"grass" },
        { name:"Vine Lash", power:27, cost:10, fx:"grass" },
        { name:"Bloom Storm", power:44, cost:24, fx:"grass" },
        { name:"Emerald Tempest", power:65, cost:46, fx:"grass" }
      ],
      electric: [
        { name:"Spark Bolt", power:19, cost:0, fx:"electric" },
        { name:"Volt Dash", power:30, cost:12, fx:"electric" },
        { name:"Thunder Cage", power:48, cost:28, fx:"electric" },
        { name:"Heaven Thunder", power:72, cost:50, fx:"electric" }
      ],
      psychic: [
        { name:"Mind Tap", power:18, cost:0, fx:"psychic" },
        { name:"Psy Cut", power:28, cost:10, fx:"psychic" },
        { name:"Dream Nova", power:45, cost:25, fx:"psychic" },
        { name:"Astral Collapse", power:68, cost:48, fx:"psychic" }
      ],
      ice: [
        { name:"Frost Needle", power:18, cost:0, fx:"ice" },
        { name:"Ice Spear", power:28, cost:10, fx:"ice" },
        { name:"Snow Burst", power:45, cost:25, fx:"ice" },
        { name:"Absolute Zero", power:67, cost:48, fx:"ice" }
      ],
      rock: [
        { name:"Stone Toss", power:20, cost:0, fx:"rock" },
        { name:"Rock Break", power:28, cost:10, fx:"rock" },
        { name:"Meteor Crash", power:46, cost:26, fx:"rock" },
        { name:"Mountain Ruin", power:67, cost:48, fx:"rock" }
      ],
      ground: [
        { name:"Mud Jab", power:19, cost:0, fx:"ground" },
        { name:"Earth Kick", power:28, cost:10, fx:"ground" },
        { name:"Quake Roar", power:46, cost:26, fx:"ground" },
        { name:"Continental Rift", power:68, cost:48, fx:"ground" }
      ],
      ghost: [
        { name:"Spirit Touch", power:18, cost:0, fx:"ghost" },
        { name:"Night Swipe", power:29, cost:11, fx:"ghost" },
        { name:"Haunt Wave", power:46, cost:26, fx:"ghost" },
        { name:"Phantom Realm", power:67, cost:48, fx:"ghost" }
      ],
      dark: [
        { name:"Shadow Bite", power:20, cost:0, fx:"dark" },
        { name:"Night Claw", power:30, cost:12, fx:"dark" },
        { name:"Abyss Fang", power:47, cost:28, fx:"dark" },
        { name:"Eclipse Doom", power:70, cost:50, fx:"dark" }
      ],
      dragon: [
        { name:"Dragon Spark", power:22, cost:0, fx:"dragon" },
        { name:"Scale Break", power:32, cost:12, fx:"dragon" },
        { name:"Draco Rampage", power:50, cost:30, fx:"dragon" },
        { name:"Dragon Starfall", power:75, cost:52, fx:"dragon" }
      ],
      fighting: [
        { name:"Power Jab", power:20, cost:0, fx:"fighting" },
        { name:"Cross Punch", power:30, cost:12, fx:"fighting" },
        { name:"Aura Smash", power:48, cost:28, fx:"fighting" },
        { name:"Titan Breaker", power:70, cost:50, fx:"fighting" }
      ],
      poison: [
        { name:"Toxic Sting", power:18, cost:0, fx:"poison" },
        { name:"Venom Edge", power:28, cost:10, fx:"poison" },
        { name:"Sludge Wave", power:45, cost:24, fx:"poison" },
        { name:"Plague Bloom", power:67, cost:48, fx:"poison" }
      ],
      bug: [
        { name:"Bug Bite", power:18, cost:0, fx:"bug" },
        { name:"Wing Slice", power:27, cost:10, fx:"bug" },
        { name:"Swarm Burst", power:43, cost:24, fx:"bug" },
        { name:"Queen Swarm", power:64, cost:46, fx:"bug" }
      ],
      flying: [
        { name:"Gust Blade", power:18, cost:0, fx:"flying" },
        { name:"Sky Peck", power:28, cost:10, fx:"flying" },
        { name:"Storm Dive", power:45, cost:24, fx:"flying" },
        { name:"Hurricane Halo", power:66, cost:46, fx:"flying" }
      ],
      fairy: [
        { name:"Fairy Kiss", power:18, cost:0, fx:"fairy" },
        { name:"Moon Spark", power:28, cost:10, fx:"fairy" },
        { name:"Star Ribbon", power:45, cost:24, fx:"fairy" },
        { name:"Miracle Waltz", power:66, cost:46, fx:"fairy" }
      ],
      steel: [
        { name:"Iron Tap", power:19, cost:0, fx:"steel" },
        { name:"Metal Slash", power:29, cost:11, fx:"steel" },
        { name:"Chrome Cannon", power:47, cost:27, fx:"steel" },
        { name:"Titanium Storm", power:68, cost:48, fx:"steel" }
      ]
    };

    const tabs = [
      { id:"explore", text:"🌍 Khám phá" },
      { id:"battle", text:"⚔️ Chiến đấu" },
      { id:"team", text:"📦 Đội hình" },
      { id:"dex", text:"📘 Từ điển" },
      { id:"evolution", text:"🧬 Tiến hoá" },
      { id:"journey", text:"🏆 Hành trình" },
      { id:"shop", text:"🛒 Cửa hàng" }
    ];

    const actionPools = {
      water:[54,60,72,73,79,80,86,87,90,98,99,116,117,118,119,120,121,129,130,131,138,139,140,141,170,171,183,186,194,195,211,222,223,224,226,230],
      ruins:[63,64,65,92,93,94,95,96,97,102,103,104,105,122,124,144,150,200,201,202,203,205,208,213,228,229,235,237],
      rare:[25,26,59,65,68,94,130,131,143,149,150,151,154,157,160,181,196,197,212,214,230,243,244,245,248,249,250,251],
      volcanic:[37,38,58,59,77,78,126,136,155,156,157,218,219,228,229,240,244],
      cave:[41,42,74,75,76,95,104,105,109,110,111,112,169,185,198,200,207,208,213,214],
      forest:[10,11,12,13,14,15,16,17,18,19,20,21,22,43,44,45,46,47,48,49,69,70,71,83,84,85,114,123,127,151,152,153,154,163,164,165,166,167,168,177,178,187,188,189,190,191,192,193,204,205],
      sky:[16,17,18,21,22,41,42,84,85,144,145,146,163,164,177,178,187,188,189,198,225,226,227]
    };

    const state = {
      loading:true,
      currentTab:"explore",
      zone:0,
      coins:500,
      badges:0,
      zoneWins:[0,0,0,0,0],
      captureCount:0,
      battleBusy:false,
      cache:new Map(),
      speciesCache:new Map(),
      evoCache:new Map(),
      dexIndex:[],
      collection:[],
      activeIndex:0,
      enemy:null,
      seen:new Set(),
      logs:{
        explore:["Chào mừng đến với Pokémon Odyssey Ultimate!"],
        battle:["Hệ thống chiến đấu mới đã sẵn sàng."],
        journey:["Bắt đầu hành trình!"]
      },
      bag:{
        pokeBall:12,
        greatBall:4,
        potion:5,
        superPotion:2,
        rareCandy:2,
        fireStone:1,
        waterStone:1,
        thunderStone:1,
        leafStone:1,
        moonStone:1,
        sunStone:1,
        linkCable:1,
        friendshipCharm:2,
        evoShard:1
      }
    };

    const $ = id => document.getElementById(id);
    const cap = s => s ? s.charAt(0).toUpperCase() + s.slice(1).replace(/-/g, " ") : "";
    const rand = (a,b) => Math.floor(Math.random()*(b-a+1))+a;
    const pick = arr => arr[Math.floor(Math.random()*arr.length)];
    const clamp = (v,min,max) => Math.max(min, Math.min(max, v));

    function toast(msg){
      const t = $("toast");
      t.textContent = msg;
      t.style.display = "block";
      clearTimeout(t._timer);
      t._timer = setTimeout(()=>t.style.display="none", 1800);
    }

    function log(type, msg){
      state.logs[type].unshift("• " + msg);
      if(state.logs[type].length > 80) state.logs[type].length = 80;
      renderCurrentTab();
    }

    function bodyTheme(){
      document.body.className = "theme-" + zones[state.zone].theme;
    }

    async function fetchJSON(url){
      const r = await fetch(url);
      if(!r.ok) throw new Error("Fetch failed");
      return r.json();
    }

    async function getPokemonData(idOrName){
      const key = String(idOrName).toLowerCase();
      if(state.cache.has(key)) return state.cache.get(key);
      const data = await fetchJSON(`${API}/pokemon/${key}`);
      const base = {
        id:data.id,
        name:data.name,
        types:data.types.map(t=>t.type.name),
        abilities:data.abilities.map(a=>a.ability.name),
        stats:{
          hp:data.stats.find(s=>s.stat.name==="hp")?.base_stat || 45,
          attack:data.stats.find(s=>s.stat.name==="attack")?.base_stat || 49,
          defense:data.stats.find(s=>s.stat.name==="defense")?.base_stat || 49,
          speed:data.stats.find(s=>s.stat.name==="speed")?.base_stat || 45
        },
        height:data.height,
        weight:data.weight,
        sprite:data.sprites.other?.["official-artwork"]?.front_default || data.sprites.front_default,
        shiny:data.sprites.front_shiny,
        speciesUrl:data.species.url
      };
      state.cache.set(key, base);
      state.cache.set(String(base.id), base);
      return base;
    }

    async function getSpecies(idOrName){
      const key = String(idOrName).toLowerCase();
      if(state.speciesCache.has(key)) return state.speciesCache.get(key);
      const data = await fetchJSON(`${API}/pokemon-species/${key}`);
      const species = {
        id:data.id,
        name:data.name,
        color:data.color?.name || "-",
        habitat:data.habitat?.name || "unknown",
        shape:data.shape?.name || "unknown",
        evolvesFrom:data.evolves_from_species?.name || null,
        evolutionChainUrl:data.evolution_chain?.url,
        flavor:(data.flavor_text_entries.find(x=>x.language.name==="en")?.flavor_text || "No description.").replace(/\f|\n/g, " "),
        genus:data.genera.find(x=>x.language.name==="en")?.genus || "-",
        growthRate:data.growth_rate?.name || "-",
        captureRate:data.capture_rate || 0,
        isLegendary:data.is_legendary,
        isMythical:data.is_mythical
      };
      state.speciesCache.set(key, species);
      state.speciesCache.set(String(species.id), species);
      return species;
    }

    async function getDexIndex(){
      try{
        const data = await fetchJSON(`${API}/pokemon?limit=${MAX_POKEMON}`);
        state.dexIndex = data.results.map((x, i)=>({ id:i+1, name:x.name }));
      }catch(err){
        state.dexIndex = [
          {id:1,name:"bulbasaur"},{id:4,name:"charmander"},{id:7,name:"squirtle"},
          {id:25,name:"pikachu"},{id:39,name:"jigglypuff"},{id:52,name:"meowth"},
          {id:133,name:"eevee"},{id:150,name:"mewtwo"},{id:151,name:"mew"}
        ];
      }
    }

    function computeStats(base, level){
      const maxHp = Math.round(base.stats.hp + level * 5.2);
      const attack = Math.round(base.stats.attack + level * 2.2);
      const defense = Math.round(base.stats.defense + level * 1.8);
      const speed = Math.round(base.stats.speed + level * 1.5);
      return { maxHp, attack, defense, speed };
    }

    function chooseMoves(types, level){
      const t1 = types[0] || "normal";
      const t2 = types[1] || "normal";
      const pool = [
        ...(typeMoves[t1] || typeMoves.normal),
        ...(t2 !== t1 ? (typeMoves[t2] || typeMoves.normal) : []),
        ...typeMoves.normal
      ];

      const chosen = [];
      function addFrom(list, idx){
        if(list[idx] && !chosen.some(m=>m.name===list[idx].name)) chosen.push({...list[idx], type:list[idx].fx === "normal" ? "normal" : (list[idx].type || null)});
      }

      const t1Moves = typeMoves[t1] || typeMoves.normal;
      const t2Moves = typeMoves[t2] || typeMoves.normal;

      addFrom(t1Moves, 0);
      addFrom(t1Moves, level >= 12 ? 1 : 0);
      addFrom(t2Moves, level >= 15 ? 2 : 1);
      addFrom(t1Moves, level >= 20 ? 3 : 2);

      while(chosen.length < 4){
        const m = pick(pool);
        if(!chosen.some(x=>x.name===m.name)) chosen.push({...m});
      }

      return chosen.slice(0,4).map(m=>({
        ...m,
        type: inferTypeFromFx(m.fx)
      }));
    }

    function inferTypeFromFx(fx){
      const map = {
        fire:"fire", water:"water", grass:"grass", electric:"electric", psychic:"psychic",
        ice:"ice", rock:"rock", ground:"ground", ghost:"ghost", dark:"dark",
        dragon:"dragon", fighting:"fighting", poison:"poison", bug:"bug",
        flying:"flying", fairy:"fairy", steel:"steel", normal:"normal"
      };
      return map[fx] || "normal";
    }

    async function createOwnedPokemon(idOrName, level){
      const base = await getPokemonData(idOrName);
      const stats = computeStats(base, level);
      return {
        uid: Date.now() + Math.random(),
        id: base.id,
        name: base.name,
        sprite: base.sprite,
        shiny: base.shiny,
        types: base.types,
        abilities: base.abilities,
        level,
        exp:0,
        friendship:60,
        hp:stats.maxHp,
        maxHp:stats.maxHp,
        attack:stats.attack,
        defense:stats.defense,
        speed:stats.speed,
        energy:35,
        maxEnergy:100,
        moves:chooseMoves(base.types, level),
        status:null
      };
    }

    function updateOwnedFromBase(mon, base){
      const stats = computeStats(base, mon.level);
      const hpRate = mon.maxHp > 0 ? mon.hp / mon.maxHp : 1;
      mon.id = base.id;
      mon.name = base.name;
      mon.sprite = base.sprite;
      mon.shiny = base.shiny;
      mon.types = base.types;
      mon.abilities = base.abilities;
      mon.maxHp = stats.maxHp;
      mon.attack = stats.attack;
      mon.defense = stats.defense;
      mon.speed = stats.speed;
      mon.hp = Math.round(mon.maxHp * hpRate);
      mon.moves = chooseMoves(base.types, mon.level);
      mon.maxEnergy = Math.min(140, 100 + Math.floor(mon.level / 5) * 4);
      mon.energy = clamp(mon.energy + 20, 0, mon.maxEnergy);
    }

    function getActive(){
      return state.collection[state.activeIndex];
    }

    function allTypesHtml(types){
      return `<div class="type-wrap">${types.map(t=>`<span class="type">${cap(t)}</span>`).join("")}</div>`;
    }

    function renderTopStats(){
      $("topStats").innerHTML = `
        <div class="stat-pill">🏅 Huy hiệu: ${state.badges}/${zones.length}</div>
        <div class="stat-pill">🪙 Coins: ${state.coins}</div>
        <div class="stat-pill">🎯 Đã bắt: ${state.captureCount}</div>
        <div class="stat-pill">🎒 Poké Ball: ${state.bag.pokeBall}</div>
        <div class="stat-pill">🔵 Great Ball: ${state.bag.greatBall}</div>
        <div class="stat-pill">📍 Khu vực: ${zones[state.zone].name}</div>
      `;
    }

    function renderTabs(){
      $("tabs").innerHTML = tabs.map(tab=>`
        <button class="tab-btn ${state.currentTab===tab.id ? "active" : ""}" onclick="openTab('${tab.id}')">${tab.text}</button>
      `).join("");
    }

    function openTab(tab){
      state.currentTab = tab;
      document.querySelectorAll(".pane").forEach(p=>p.classList.remove("active"));
      $(`tab-${tab}`).classList.add("active");
      renderTabs();
      renderCurrentTab();
    }

    function renderCurrentTab(){
      renderTopStats();
      if(state.currentTab==="explore") renderExplore();
      if(state.currentTab==="battle") renderBattle();
      if(state.currentTab==="team") renderTeam();
      if(state.currentTab==="dex") renderDex();
      if(state.currentTab==="evolution") renderEvolution();
      if(state.currentTab==="journey") renderJourney();
      if(state.currentTab==="shop") renderShop();
    }

    function renderZoneStrip(){
      return `
        <div class="zone-strip">
          ${zones.map(z=>`
            <div class="zone-card ${state.zone===z.id ? "active":""} ${state.badges<z.unlock ? "locked":""}" onclick="selectZone(${z.id})">
              <b>${z.name}</b>
              <div class="sub">${z.desc}</div>
              <div class="sub">Mở khóa: ${z.unlock} huy hiệu</div>
            </div>
          `).join("")}
        </div>
      `;
    }

    function renderExplore(){
      const active = getActive();
      $("tab-explore").innerHTML = `
        <div class="card">
          <h2>🌍 Khám phá khu vực</h2>
          <div class="sub">Chọn kiểu khám phá để hành trình không còn 1 màu. Mỗi lựa chọn có sự kiện khác nhau: bắt Pokémon, gặp Pokémon hiếm, nhận vật phẩm, tăng tình bạn hoặc gặp trận chiến mạnh hơn.</div>
          ${renderZoneStrip()}
        </div>

        <div class="grid-2">
          <div class="card">
            <h3>✨ Chọn cách khám phá</h3>
            <div class="explore-actions">
              ${exploreModes.map(mode=>`
                <div class="action-card" onclick="explore('${mode.id}')">
                  <div class="icon">${mode.icon}</div>
                  <b>${mode.name}</b>
                  <div class="sub">${mode.desc}</div>
                </div>
              `).join("")}
            </div>
            <div class="inline-actions" style="margin-top:14px">
              <button class="big-btn btn-green" onclick="restAll()">⛺ Nghỉ toàn đội</button>
              <button class="big-btn btn-blue" onclick="trainAll()">💪 Luyện tập toàn đội</button>
              <button class="big-btn btn-purple" onclick="openTab('battle')">⚔️ Sang tab chiến đấu</button>
            </div>
          </div>

          <div class="card">
            <h3>🧭 Thông tin hành trình</h3>
            <div class="detail-grid">
              <div class="detail-box">
                <b>Pokémon đang dẫn đội</b>
                ${active ? `
                  <div style="display:flex; gap:12px; align-items:center; margin-top:10px">
                    <img src="${active.sprite}" alt="${active.name}" style="width:90px; height:90px; object-fit:contain">
                    <div>
                      <div><b>${cap(active.name)}</b> • Lv.${active.level}</div>
                      <div class="sub">HP ${active.hp}/${active.maxHp} • Energy ${active.energy}/${active.maxEnergy}</div>
                      ${allTypesHtml(active.types)}
                    </div>
                  </div>
                ` : `<div class="sub">Chưa có Pokémon.</div>`}
              </div>
              <div class="detail-box">
                <b>Khu vực hiện tại</b>
                <div style="margin-top:10px">${zones[state.zone].name}</div>
                <div class="sub">${zones[state.zone].desc}</div>
                <div class="sub" style="margin-top:6px">Thắng tại khu vực: ${state.zoneWins[state.zone]} trận</div>
                <div class="sub">Huy hiệu khu vực: ${zones[state.zone].badge}</div>
              </div>
            </div>
            <div style="margin-top:12px">
              <b>📝 Nhật ký khám phá</b>
              <div class="log">${state.logs.explore.map(x=>`<div>${x}</div>`).join("")}</div>
            </div>
          </div>
        </div>
      `;
    }

    function battleSceneHtml(){
      const player = getActive();
      const enemy = state.enemy;
      const zone = zones[state.zone];
      return `
        <div class="battle-scene ${zone.theme}" id="scene">
          <div class="fx-layer" id="fxLayer"></div>
          <div class="arena-shadow left"></div>
          <div class="arena-shadow right"></div>
          ${player ? `<img src="${player.sprite}" class="poke player" id="playerSprite" alt="${player.name}">` : ""}
          ${enemy ? `<img src="${enemy.sprite}" class="poke enemy" id="enemySprite" alt="${enemy.name}">` : ""}
        </div>
      `;
    }

    function renderBattle(){
      const player = getActive();
      const enemy = state.enemy;
      $("tab-battle").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>⚔️ Chiến đấu</h2>
            <div class="sub">Mỗi hệ có hiệu ứng kỹ năng khác nhau: lửa, nước, cỏ, điện, ma, rồng, thép, tiên...</div>
            ${battleSceneHtml()}

            ${player && enemy ? `
              <div class="battle-hud">
                <div class="hud-card">
                  <div class="hud-head"><span>${cap(player.name)}</span><span>Lv.${player.level}</span></div>
                  <div class="bar"><span class="hp" style="width:${player.hp/player.maxHp*100}%"></span></div>
                  <small>HP ${player.hp}/${player.maxHp}</small>
                  <div class="bar"><span class="en" style="width:${player.energy/player.maxEnergy*100}%"></span></div>
                  <small>Năng lượng ${player.energy}/${player.maxEnergy}</small>
                </div>
                <div class="hud-card">
                  <div class="hud-head"><span>Wild ${cap(enemy.name)}</span><span>Lv.${enemy.level}</span></div>
                  <div class="bar"><span class="hp" style="width:${enemy.hp/enemy.maxHp*100}%"></span></div>
                  <small>HP ${enemy.hp}/${enemy.maxHp}</small>
                  <div class="bar"><span class="en" style="width:${enemy.energy/enemy.maxEnergy*100}%"></span></div>
                  <small>Năng lượng ${enemy.energy}/${enemy.maxEnergy}</small>
                </div>
              </div>

              <div class="move-grid">
                ${player.moves.map((m, i)=>`
                  <button class="move-btn" onclick="useMove(${i})" ${state.battleBusy || player.energy < m.cost || player.hp<=0 ? "disabled":""}>
                    ${m.name}
                    <small>${cap(m.type)} • Power ${m.power} • Cost ${m.cost}</small>
                  </button>
                `).join("")}
              </div>

              <div class="inline-actions">
                <button class="big-btn btn-blue" onclick="chargeEnergy()" ${state.battleBusy ? "disabled":""}>⚡ Tích năng lượng</button>
                <button class="big-btn btn-green" onclick="throwBall('pokeBall')" ${state.battleBusy || state.bag.pokeBall<=0 ? "disabled":""}>⚪ Ném Poké Ball</button>
                <button class="big-btn btn-purple" onclick="throwBall('greatBall')" ${state.battleBusy || state.bag.greatBall<=0 ? "disabled":""}>🔵 Ném Great Ball</button>
                <button class="big-btn btn-red" onclick="explore('wander')">➡️ Gặp đối thủ khác</button>
              </div>
            ` : `
              <div class="inline-actions">
                <button class="big-btn" onclick="explore('wander')">🔎 Tìm đối thủ</button>
              </div>
            `}
          </div>

          <div class="card">
            <h3>📜 Nhật ký chiến đấu</h3>
            <div class="log">${state.logs.battle.map(x=>`<div>${x}</div>`).join("")}</div>
          </div>
        </div>
      `;
    }

    function renderTeam(){
      const active = getActive();
      $("tab-team").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>📦 Đội Pokémon</h2>
            <div class="sub">Mỗi Pokémon có level, friendship, năng lượng, kỹ năng riêng. Chọn 1 Pokémon để dẫn đội hoặc dùng item trực tiếp.</div>
            <div class="team-grid" style="margin-top:12px">
              ${state.collection.map((m, i)=>`
                <div class="mini-mon ${i===state.activeIndex ? "active":""}" onclick="setActive(${i})">
                  <img src="${m.sprite}" alt="${m.name}">
                  <b>${cap(m.name)}</b>
                  <div class="sub">Lv.${m.level} • HP ${m.hp}/${m.maxHp}</div>
                  <div class="sub">Friendship ${m.friendship} • Energy ${m.energy}/${m.maxEnergy}</div>
                  ${allTypesHtml(m.types)}
                </div>
              `).join("")}
            </div>
          </div>

          <div class="card">
            <h3>🎯 Pokémon đang chọn</h3>
            ${active ? `
              <div style="display:flex; gap:14px; align-items:center; flex-wrap:wrap">
                <img src="${active.sprite}" alt="${active.name}" style="width:120px; height:120px; object-fit:contain">
                <div>
                  <div style="font-size:22px; font-weight:900">${cap(active.name)}</div>
                  <div class="sub">${active.abilities.map(cap).join(", ")}</div>
                  <div class="sub">Lv.${active.level} • EXP ${active.exp}</div>
                  <div class="sub">HP ${active.hp}/${active.maxHp} • Energy ${active.energy}/${active.maxEnergy}</div>
                  <div class="sub">ATK ${active.attack} • DEF ${active.defense} • SPD ${active.speed}</div>
                  <div class="sub">Friendship ${active.friendship}</div>
                  ${allTypesHtml(active.types)}
                </div>
              </div>

              <div class="inline-actions">
                <button class="small-btn" onclick="useItemOnActive('potion')" ${state.bag.potion<=0 ? "disabled":""}>🧪 Potion (${state.bag.potion})</button>
                <button class="small-btn" onclick="useItemOnActive('superPotion')" ${state.bag.superPotion<=0 ? "disabled":""}>💊 Super Potion (${state.bag.superPotion})</button>
                <button class="small-btn" onclick="useItemOnActive('rareCandy')" ${state.bag.rareCandy<=0 ? "disabled":""}>🍬 Rare Candy (${state.bag.rareCandy})</button>
                <button class="small-btn" onclick="useItemOnActive('friendshipCharm')" ${state.bag.friendshipCharm<=0 ? "disabled":""}>💖 Friendship Charm (${state.bag.friendshipCharm})</button>
              </div>

              <div style="margin-top:12px">
                <b>🗡️ Bộ kỹ năng</b>
                <div class="team-grid" style="margin-top:10px">
                  ${active.moves.map(move=>`
                    <div class="detail-box">
                      <b>${move.name}</b>
                      <div class="sub">${cap(move.type)} • Power ${move.power} • Cost ${move.cost}</div>
                      <div class="sub">Hiệu ứng: ${cap(move.fx)}</div>
                    </div>
                  `).join("")}
                </div>
              </div>
            ` : `<div class="sub">Chưa có Pokémon.</div>`}
          </div>
        </div>
      `;
    }

    function renderDex(){
      const keyword = state.dexSearch || "";
      const filtered = state.dexIndex.filter(x => x.name.includes(keyword.toLowerCase())).slice(0, 251);

      $("tab-dex").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>📘 Từ điển Pokémon / Pokédex</h2>
            <div class="sub">Tìm kiếm Pokémon, xem mô tả, hệ, khả năng, sinh cảnh, màu sắc, tiến hoá.</div>
            <div class="search-row">
              <input id="dexSearchInput" value="${keyword}" placeholder="Tìm tên Pokémon..." oninput="dexSearch(this.value)">
              <button class="small-btn" onclick="loadDexDetail(${filtered[0]?.id || 1})">Mở Pokémon đầu tiên</button>
            </div>
            <div class="dex-list">
              ${filtered.map(mon=>`
                <div class="dex-item" onclick="loadDexDetail(${mon.id})">
                  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${mon.id}.png" alt="${mon.name}">
                  <b>#${mon.id}</b>
                  <div>${cap(mon.name)}</div>
                  <div class="sub">${state.seen.has(mon.id) ? "Đã gặp" : "Chưa gặp"}</div>
                </div>
              `).join("")}
            </div>
          </div>

          <div class="card" id="dexDetail">
            <h3>Chọn 1 Pokémon để xem chi tiết</h3>
            <div class="sub">Bạn có thể tra cứu như một từ điển Pokémon thực thụ.</div>
          </div>
        </div>
      `;
      if(state.dexSelected && !state.dexDetailLoading) fillDexDetail(state.dexSelected);
    }

    async function loadDexDetail(id){
      state.dexDetailLoading = true;
      state.dexSelected = id;
      renderDex();
      try{
        const base = await getPokemonData(id);
        const species = await getSpecies(id);
        const evo = await getEvolutionInfo(id);
        fillDexDetail({
          base,
          species,
          evo
        });
      }catch(err){
        $("dexDetail").innerHTML = `<h3>Lỗi tải dữ liệu Pokémon</h3><div class="sub">Không thể lấy thông tin từ API.</div>`;
      }
      state.dexDetailLoading = false;
    }

    function fillDexDetail(data){
      if(!data) return;
      const base = data.base || data.base?.base;
      const species = data.species || data.species?.species || {};
      const evo = data.evo || [];
      $("dexDetail").innerHTML = `
        <h3>📖 ${cap(base.name)} #${base.id}</h3>
        <div style="display:flex; gap:14px; align-items:center; flex-wrap:wrap">
          <img src="${base.sprite}" alt="${base.name}" style="width:150px; height:150px; object-fit:contain">
          <div>
            <div class="sub">${species.genus || "-"}</div>
            <div class="sub">${species.flavor || "-"}</div>
            ${allTypesHtml(base.types)}
          </div>
        </div>

        <div class="detail-grid" style="margin-top:12px">
          <div class="detail-box"><b>Khả năng</b><div class="sub">${base.abilities.map(cap).join(", ")}</div></div>
          <div class="detail-box"><b>Habitat</b><div class="sub">${cap(species.habitat || "unknown")}</div></div>
          <div class="detail-box"><b>Height / Weight</b><div class="sub">${base.height/10} m • ${base.weight/10} kg</div></div>
          <div class="detail-box"><b>Màu / Dáng</b><div class="sub">${cap(species.color || "-")} • ${cap(species.shape || "-")}</div></div>
          <div class="detail-box"><b>Tăng trưởng</b><div class="sub">${cap(species.growthRate || "-")}</div></div>
          <div class="detail-box"><b>Độ hiếm</b><div class="sub">${species.isLegendary ? "Legendary" : species.isMythical ? "Mythical" : "Normal"}</div></div>
        </div>

        <div style="margin-top:12px">
          <b>Stats gốc</b>
          <div class="detail-grid" style="margin-top:10px">
            <div class="detail-box">HP: ${base.stats.hp}</div>
            <div class="detail-box">Attack: ${base.stats.attack}</div>
            <div class="detail-box">Defense: ${base.stats.defense}</div>
            <div class="detail-box">Speed: ${base.stats.speed}</div>
          </div>
        </div>

        <div style="margin-top:12px">
          <b>Chuỗi tiến hoá</b>
          <div class="team-grid" style="margin-top:10px">
            ${evo.length ? evo.map(x=>`
              <div class="detail-box">
                <b>${cap(x.from)}</b> ➜ <b>${cap(x.to)}</b>
                <div class="sub">${x.requirement}</div>
              </div>
            `).join("") : `<div class="detail-box">Không có dữ liệu tiến hoá.</div>`}
          </div>
        </div>
      `;
    }

    async function renderEvolution(){
      $("tab-evolution").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>🧬 Phòng tiến hoá</h2>
            <div class="sub">Hỗ trợ nhiều kiểu tiến hoá: lên cấp, dùng đá tiến hoá, tình bạn, trade item, và vài dạng đặc biệt.</div>
            <div class="evo-grid" id="evoList">
              ${state.collection.map((m, i)=>`
                <div class="mini-mon" onclick="selectEvolutionMon(${i})">
                  <img src="${m.sprite}" alt="${m.name}">
                  <b>${cap(m.name)}</b>
                  <div class="sub">Lv.${m.level} • Friendship ${m.friendship}</div>
                  ${allTypesHtml(m.types)}
                </div>
              `).join("")}
            </div>
          </div>

          <div class="card" id="evoDetail">
            <h3>Chọn Pokémon để xem khả năng tiến hoá</h3>
          </div>
        </div>
      `;

      if(typeof state.evoSelected === "number"){
        await selectEvolutionMon(state.evoSelected);
      }
    }

    async function getEvolutionInfo(idOrName){
      const species = await getSpecies(idOrName);
      if(!species.evolutionChainUrl) return [];
      if(state.evoCache.has(species.evolutionChainUrl)) return state.evoCache.get(species.evolutionChainUrl);
      const data = await fetchJSON(species.evolutionChainUrl);

      const edges = [];
      function walk(node){
        if(!node) return;
        node.evolves_to.forEach(next=>{
          const d = next.evolution_details?.[0] || {};
          edges.push({
            from: node.species.name,
            to: next.species.name,
            requirement: formatEvolutionRequirement(d),
            detail: d
          });
          walk(next);
        });
      }
      walk(data.chain);
      state.evoCache.set(species.evolutionChainUrl, edges);
      return edges;
    }

    function formatEvolutionRequirement(d){
      if(!d || !Object.keys(d).length) return "Special evolution";
      if(d.trigger?.name === "level-up"){
        const parts = [];
        if(d.min_level) parts.push(`Lv ${d.min_level}+`);
        if(d.min_happiness) parts.push(`Friendship ${d.min_happiness}+`);
        if(d.time_of_day) parts.push(`Time: ${d.time_of_day}`);
        if(d.known_move_type) parts.push(`Biết move hệ ${d.known_move_type.name}`);
        if(d.held_item) parts.push(`Cần cầm ${cap(d.held_item.name)}`);
        return parts.length ? `Level-up: ${parts.join(" • ")}` : "Level-up";
      }
      if(d.trigger?.name === "use-item"){
        return `Use item: ${cap(d.item?.name || "special item")}`;
      }
      if(d.trigger?.name === "trade"){
        return `Trade evolution${d.held_item ? " + " + cap(d.held_item.name) : ""}`;
      }
      return cap(d.trigger?.name || "special");
    }

    async function selectEvolutionMon(index){
      state.evoSelected = index;
      const mon = state.collection[index];
      $("evoDetail").innerHTML = `<h3>Đang tải dữ liệu tiến hoá...</h3>`;
      try{
        const edges = await getEvolutionInfo(mon.id);
        const nextEdges = edges.filter(x=>x.from === mon.name);
        $("evoDetail").innerHTML = `
          <h3>${cap(mon.name)} • Lv.${mon.level}</h3>
          <div style="display:flex; gap:14px; align-items:center; flex-wrap:wrap">
            <img src="${mon.sprite}" style="width:120px; height:120px; object-fit:contain">
            <div>
              <div class="sub">Friendship ${mon.friendship}</div>
              <div class="sub">HP ${mon.hp}/${mon.maxHp}</div>
              ${allTypesHtml(mon.types)}
            </div>
          </div>

          <div style="margin-top:12px">
            <b>Các hướng tiến hoá hiện có</b>
            <div class="team-grid" style="margin-top:10px">
              ${nextEdges.length ? nextEdges.map((e, i)=>`
                <div class="detail-box">
                  <b>${cap(e.from)}</b> ➜ <b>${cap(e.to)}</b>
                  <div class="sub">${e.requirement}</div>
                  <button class="small-btn" style="margin-top:10px" onclick="evolveSelected(${index}, '${e.to}', ${i})">Tiến hoá</button>
                </div>
              `).join("") : `<div class="detail-box">Pokémon này hiện không có tiến hoá tiếp theo hoặc đã ở dạng cuối.</div>`}
            </div>
          </div>

          <div style="margin-top:12px">
            <b>Vật phẩm tiến hoá hiện có</b>
            <div class="sub" style="margin-top:6px">
              ${Object.keys(state.bag).filter(k=>["fireStone","waterStone","thunderStone","leafStone","moonStone","sunStone","linkCable","evoShard"].includes(k))
                .map(k=>`${itemCatalog[k].emoji} ${itemCatalog[k].name}: ${state.bag[k]}`).join(" • ")}
            </div>
          </div>
        `;
      }catch(err){
        $("evoDetail").innerHTML = `<h3>Lỗi tải tiến hoá</h3><div class="sub">Không lấy được evolution chain.</div>`;
      }
    }

    function canEvolve(mon, detail){
      if(!detail || !detail.trigger) return { ok: state.bag.evoShard > 0, consume:"evoShard", reason:"Cần Evolution Shard" };

      const trigger = detail.trigger.name;

      if(trigger === "level-up"){
        if(detail.min_level && mon.level < detail.min_level) return { ok:false, reason:`Cần Lv ${detail.min_level}` };
        if(detail.min_happiness && mon.friendship < detail.min_happiness) return { ok:false, reason:`Cần Friendship ${detail.min_happiness}` };
        return { ok:true, consume:null, reason:"Đủ điều kiện level-up" };
      }

      if(trigger === "use-item"){
        const itemKey = mapEvolutionItem(detail.item?.name);
        if(!itemKey) return { ok:false, reason:"Chưa hỗ trợ item này" };
        if(state.bag[itemKey] <= 0) return { ok:false, reason:`Thiếu ${itemCatalog[itemKey].name}` };
        return { ok:true, consume:itemKey, reason:`Dùng ${itemCatalog[itemKey].name}` };
      }

      if(trigger === "trade"){
        if(state.bag.linkCable <= 0) return { ok:false, reason:"Thiếu Link Cable" };
        return { ok:true, consume:"linkCable", reason:"Dùng Link Cable" };
      }

      if(state.bag.evoShard > 0) return { ok:true, consume:"evoShard", reason:"Dùng Evolution Shard" };
      return { ok:false, reason:"Thiếu Evolution Shard" };
    }

    function mapEvolutionItem(apiName){
      const map = {
        "fire-stone":"fireStone",
        "water-stone":"waterStone",
        "thunder-stone":"thunderStone",
        "leaf-stone":"leafStone",
        "moon-stone":"moonStone",
        "sun-stone":"sunStone"
      };
      return map[apiName] || null;
    }

    async function evolveSelected(index, targetName, edgeIndex){
      const mon = state.collection[index];
      const edges = await getEvolutionInfo(mon.id);
      const nextEdges = edges.filter(x=>x.from === mon.name);
      const edge = nextEdges[edgeIndex];
      if(!edge){
        toast("Không tìm thấy dữ liệu tiến hoá.");
        return;
      }
      const check = canEvolve(mon, edge.detail);
      if(!check.ok){
        toast(check.reason);
        return;
      }
      try{
        if(check.consume) state.bag[check.consume]--;
        const base = await getPokemonData(targetName);
        const oldName = mon.name;
        updateOwnedFromBase(mon, base);
        mon.friendship += 10;
        mon.hp = mon.maxHp;
        mon.energy = clamp(mon.energy + 30, 0, mon.maxEnergy);
        log("journey", `${cap(oldName)} đã tiến hoá thành ${cap(mon.name)}!`);
        log("explore", `${cap(oldName)} tiến hoá thành ${cap(mon.name)}.`);
        toast(`🎉 ${cap(oldName)} ➜ ${cap(mon.name)}`);
        renderCurrentTab();
      }catch(err){
        toast("Tiến hoá thất bại.");
      }
    }

    function renderJourney(){
      $("tab-journey").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>🏆 Hành trình & Huy hiệu</h2>
            <div class="sub">Mỗi khu vực sẽ có 1 huy hiệu. Thắng đủ trận trong khu vực sẽ nhận huy hiệu và mở khu mới.</div>
            ${renderZoneStrip()}

            <div style="margin-top:14px">
              <b>🎖️ Huy hiệu đã nhận</b>
              <div class="badge-list" style="margin-top:10px">
                ${zones.map((z, i)=>`
                  <div class="badge">${i < state.badges ? "✅" : "⬜"} ${z.badge}</div>
                `).join("")}
              </div>
            </div>

            <div style="margin-top:14px">
              <b>📈 Tiến độ khu vực</b>
              <div class="team-grid" style="margin-top:10px">
                ${zones.map((z, i)=>`
                  <div class="detail-box">
                    <b>${z.name}</b>
                    <div class="sub">Trận thắng: ${state.zoneWins[i]}</div>
                    <div class="sub">Mở khoá cần: ${z.unlock} huy hiệu</div>
                    <div class="sub">Phần thưởng: ${z.badge}</div>
                  </div>
                `).join("")}
              </div>
            </div>
          </div>

          <div class="card">
            <h3>📝 Nhật ký hành trình</h3>
            <div class="log">${state.logs.journey.map(x=>`<div>${x}</div>`).join("")}</div>
          </div>
        </div>
      `;
    }

    function renderShop(){
      $("tab-shop").innerHTML = `
        <div class="card">
          <h2>🛒 Cửa hàng</h2>
          <div class="sub">Mua bóng, bình hồi máu, kẹo tăng cấp và vật phẩm tiến hoá.</div>
          <div class="shop-grid" style="margin-top:12px">
            ${Object.entries(itemCatalog).map(([key, item])=>`
              <div class="shop-item">
                <div style="font-size:24px">${item.emoji}</div>
                <b>${item.name}</b>
                <div class="sub">${item.desc}</div>
                <div class="sub">Giá: ${item.price} coins</div>
                <div class="sub">Đang có: ${state.bag[key] || 0}</div>
                <button class="small-btn" style="margin-top:10px" onclick="buyItem('${key}')">Mua</button>
              </div>
            `).join("")}
          </div>
        </div>
      `;
    }

    function setActive(index){
      if(state.collection[index].hp <= 0){
        toast("Pokémon này đã kiệt sức, hãy hồi máu trước.");
        return;
      }
      state.activeIndex = index;
      log("explore", `${cap(state.collection[index].name)} được chọn làm Pokémon dẫn đội.`);
      renderCurrentTab();
    }

    function selectZone(id){
      if(state.badges < zones[id].unlock){
        toast("Chưa đủ huy hiệu để vào khu vực này.");
        return;
      }
      state.zone = id;
      bodyTheme();
      log("journey", `Đã chuyển đến ${zones[id].name}.`);
      renderCurrentTab();
    }

    function useItemOnActive(itemKey){
      const mon = getActive();
      if(!mon) return;
      if((state.bag[itemKey] || 0) <= 0){
        toast("Bạn không có item này.");
        return;
      }

      if(itemKey === "potion"){
        mon.hp = clamp(mon.hp + 35, 0, mon.maxHp);
      } else if(itemKey === "superPotion"){
        mon.hp = clamp(mon.hp + 70, 0, mon.maxHp);
      } else if(itemKey === "rareCandy"){
        mon.levelUpBonus = true;
        mon.exp += mon.level * 28;
        state.bag[itemKey]--;
        applyLevelUps(mon);
        log("journey", `${cap(mon.name)} dùng Rare Candy và lên cấp.`);
        renderCurrentTab();
        return;
      } else if(itemKey === "friendshipCharm"){
        mon.friendship = clamp(mon.friendship + 40, 0, 255);
      } else {
        toast("Item này dùng ở tab tiến hoá.");
        return;
      }

      state.bag[itemKey]--;
      toast(`Dùng ${itemCatalog[itemKey].name} cho ${cap(mon.name)}.`);
      renderCurrentTab();
    }

    function buyItem(itemKey){
      const item = itemCatalog[itemKey];
      if(state.coins < item.price){
        toast("Không đủ coins.");
        return;
      }
      state.coins -= item.price;
      state.bag[itemKey] = (state.bag[itemKey] || 0) + 1;
      toast(`Đã mua ${item.name}.`);
      renderCurrentTab();
    }

    function restAll(){
      state.collection.forEach(m=>{
        m.hp = m.maxHp;
        m.energy = Math.max(m.energy, 45);
        m.friendship = clamp(m.friendship + 4, 0, 255);
      });
      log("explore", "Toàn đội nghỉ ngơi: hồi HP, hồi năng lượng và tăng tình bạn.");
      renderCurrentTab();
    }

    function trainAll(){
      state.collection.forEach(m=>{
        m.exp += 10;
        m.energy = clamp(m.energy + 12, 0, m.maxEnergy);
      });
      state.coins = Math.max(0, state.coins - 20);
      state.collection.forEach(m=>applyLevelUps(m));
      log("journey", "Toàn đội luyện tập: tăng EXP, tăng năng lượng, tốn 20 coins.");
      renderCurrentTab();
    }

    async function explore(mode){
      if(mode === "camp"){
        restAll();
        if(Math.random() < 0.4){
          const reward = pick(["potion","pokeBall","friendshipCharm"]);
          state.bag[reward] = (state.bag[reward] || 0) + 1;
          log("explore", `Khi dựng trại, bạn tìm được ${itemCatalog[reward].name}.`);
        }
        openTab("explore");
        return;
      }

      const zone = zones[state.zone];
      const id = await pickEncounterId(mode, zone);
      try{
        const level = rand(5 + state.zone * 6, 10 + state.zone * 8);
        state.enemy = await createOwnedPokemon(id, level);
        state.enemy.friendship = 0;
        state.enemy.energy = rand(20, 55);
        state.seen.add(state.enemy.id);

        let eventText = `${cap(state.enemy.name)} xuất hiện!`;
        if(mode === "rare") eventText = `Bạn theo dấu hiếm và gặp ${cap(state.enemy.name)} cực kỳ mạnh!`;
        if(mode === "water") eventText = `Bên nguồn nước, ${cap(state.enemy.name)} xuất hiện!`;
        if(mode === "ruins") eventText = `Trong phế tích cổ, ${cap(state.enemy.name)} hiện ra!`;

        if(Math.random() < 0.22){
          const found = pick(["coins","item"]);
          if(found === "coins"){
            const extra = rand(25, 80);
            state.coins += extra;
            log("explore", `Bạn nhặt được ${extra} coins khi khám phá.`);
          }else{
            const reward = pick(["pokeBall","greatBall","potion","rareCandy"]);
            state.bag[reward] = (state.bag[reward] || 0) + 1;
            log("explore", `Bạn nhặt được ${itemCatalog[reward].name} trên đường.`);
          }
        }

        log("explore", eventText);
        log("battle", eventText);
        openTab("battle");
      }catch(err){
        toast("Không thể tạo encounter từ API.");
      }
    }

    async function pickEncounterId(mode, zone){
      let pool = [];
      for(let i=zone.min; i<=zone.max; i++) pool.push(i);

      if(mode === "rare"){
        pool = [...pool, ...actionPools.rare.filter(x=>x>=zone.min && x<=zone.max), ...actionPools.rare];
      }else if(mode === "water"){
        pool = [...pool, ...actionPools.water];
      }else if(mode === "ruins"){
        pool = [...pool, ...actionPools.ruins];
      }else if(zone.theme === "forest"){
        pool = [...pool, ...actionPools.forest];
      }else if(zone.theme === "cave"){
        pool = [...pool, ...actionPools.cave];
      }else if(zone.theme === "volcano"){
        pool = [...pool, ...actionPools.volcanic];
      }else if(zone.theme === "sky"){
        pool = [...pool, ...actionPools.sky];
      }

      pool = pool.filter(x=>x>=1 && x<=MAX_POKEMON);
      return pick(pool);
    }

    function damage(attacker, defender, move){
      const stab = attacker.types.includes(move.type) ? 1.18 : 1;
      const crit = Math.random() < 0.12 ? 1.65 : 1;
      const variance = Math.random() * 0.22 + 0.90;
      const raw = move.power + attacker.attack * 0.44 - defender.defense * 0.18;
      const dmg = Math.max(4, Math.round(raw * stab * crit * variance));
      defender.hp = Math.max(0, defender.hp - dmg);
      attacker.energy = clamp(attacker.energy + 10, 0, attacker.maxEnergy);
      return { dmg, crit: crit > 1 };
    }

    async function useMove(index){
      const player = getActive();
      const enemy = state.enemy;
      if(!player || !enemy || state.battleBusy) return;

      const move = player.moves[index];
      if(player.energy < move.cost){
        toast("Chưa đủ năng lượng.");
        return;
      }

      state.battleBusy = true;
      player.energy -= move.cost;
      renderBattle();

      animateMove(move, true);
      animateSprite("player", "attack");
      await wait(430);

      const result = damage(player, enemy, move);
      log("battle", `${cap(player.name)} dùng ${move.name}, gây ${result.dmg} sát thương${result.crit ? " chí mạng" : ""}!`);
      animateSprite("enemy", "hit");

      if(enemy.hp <= 0){
        await wait(340);
        await onWinBattle();
        state.battleBusy = false;
        renderCurrentTab();
        return;
      }

      await wait(460);
      await enemyTurn();
      state.battleBusy = false;
      renderCurrentTab();
    }

    async function enemyTurn(){
      const player = getActive();
      const enemy = state.enemy;
      if(!player || !enemy) return;

      const usable = enemy.moves.filter(m=>enemy.energy >= m.cost);
      if(!usable.length){
        enemy.energy = clamp(enemy.energy + 32, 0, enemy.maxEnergy);
        log("battle", `${cap(enemy.name)} tập trung để tích năng lượng.`);
        return;
      }

      const move = pick(usable);
      enemy.energy -= move.cost;
      renderBattle();

      animateMove(move, false);
      animateSprite("enemy", "attack");
      await wait(430);

      const result = damage(enemy, player, move);
      log("battle", `${cap(enemy.name)} dùng ${move.name}, gây ${result.dmg} sát thương${result.crit ? " chí mạng" : ""}!`);
      animateSprite("player", "hit");

      if(player.hp <= 0){
        player.hp = 0;
        log("battle", `${cap(player.name)} đã kiệt sức!`);
        const next = state.collection.findIndex(m=>m.hp > 0);
        if(next >= 0){
          state.activeIndex = next;
          log("battle", `${cap(state.collection[next].name)} được đổi vào sân.`);
        }else{
          log("journey", "Cả đội đã kiệt sức. Tự động nghỉ ngơi ở trại.");
          restAll();
          openTab("explore");
        }
      }
    }

    function chargeEnergy(){
      const player = getActive();
      if(!player || state.battleBusy) return;
      player.energy = clamp(player.energy + 34, 0, player.maxEnergy);
      log("battle", `${cap(player.name)} tích thêm 34 năng lượng.`);
      renderBattle();
      enemyTurn().then(renderCurrentTab);
    }

    async function throwBall(ballType){
      const enemy = state.enemy;
      const player = getActive();
      if(!enemy || !player || state.battleBusy) return;
      if((state.bag[ballType] || 0) <= 0){
        toast("Hết bóng rồi.");
        return;
      }
      state.bag[ballType]--;

      const hpFactor = 1 - enemy.hp / enemy.maxHp;
      const baseChance = ballType === "greatBall" ? 0.32 : 0.20;
      const chance = clamp(baseChance + hpFactor * 0.55 + state.badges * 0.03, 0.12, 0.92);

      if(Math.random() < chance){
        enemy.hp = Math.max(1, Math.round(enemy.maxHp * 0.65));
        enemy.energy = 35;
        enemy.friendship = 35;
        state.collection.push(enemy);
        state.captureCount++;
        state.coins += rand(30, 70);
        log("battle", `Bạn đã bắt được ${cap(enemy.name)}!`);
        log("journey", `Pokédex mở rộng: ${cap(enemy.name)} gia nhập đội.`);
        maybeAwardBadge();
        state.enemy = null;
        openTab("team");
      }else{
        log("battle", `${cap(enemy.name)} thoát khỏi bóng!`);
        await enemyTurn();
        renderCurrentTab();
      }
    }

    function applyLevelUps(mon){
      let leveled = false;
      while(mon.exp >= mon.level * 25){
        mon.exp -= mon.level * 25;
        mon.level++;
        mon.friendship = clamp(mon.friendship + 3, 0, 255);
        const baseStats = {
          hp: Math.round(mon.maxHp / (1 + (mon.level-1)*0.05)),
          attack:mon.attack,
          defense:mon.defense,
          speed:mon.speed
        };
        const baseLike = {
          id:mon.id,
          name:mon.name,
          sprite:mon.sprite,
          shiny:mon.shiny,
          types:mon.types,
          abilities:mon.abilities,
          stats:{
            hp: Math.max(35, baseStats.hp - mon.level),
            attack: Math.max(35, mon.attack - mon.level),
            defense: Math.max(35, mon.defense - mon.level),
            speed: Math.max(30, mon.speed - mon.level)
          }
        };
        const newStats = computeStats(baseLike, mon.level);
        mon.maxHp = newStats.maxHp;
        mon.attack = newStats.attack;
        mon.defense = newStats.defense;
        mon.speed = newStats.speed;
        mon.maxEnergy = Math.min(140, 100 + Math.floor(mon.level / 5) * 4);
        mon.hp = mon.maxHp;
        mon.energy = mon.maxEnergy;
        mon.moves = chooseMoves(mon.types, mon.level);
        leveled = true;
      }
      if(leveled){
        log("journey", `${cap(mon.name)} lên cấp ${mon.level}!`);
      }
    }

    async function onWinBattle(){
      const player = getActive();
      const enemy = state.enemy;
      if(!player || !enemy) return;

      const expGain = 20 + enemy.level * 4;
      const coinGain = rand(25, 80);
      player.exp += expGain;
      player.friendship = clamp(player.friendship + 5, 0, 255);
      state.coins += coinGain;
      if(Math.random() < 0.28) state.bag.pokeBall++;
      if(Math.random() < 0.12) state.bag.rareCandy++;

      log("battle", `${cap(enemy.name)} bị đánh bại!`);
      log("journey", `${cap(player.name)} nhận ${expGain} EXP và ${coinGain} coins.`);
      state.zoneWins[state.zone]++;

      applyLevelUps(player);
      maybeAwardBadge();

      state.enemy = null;
      toast("Chiến thắng!");
    }

    function maybeAwardBadge(){
      const needWins = 3 + state.zone * 2;
      if(state.badges === state.zone && state.zoneWins[state.zone] >= needWins){
        state.badges++;
        state.coins += 220 + state.zone * 80;
        state.bag.greatBall += 2;
        log("journey", `Bạn nhận được ${zones[state.zone].badge}! Mở khóa khu vực mới.`);
        toast(`🏅 Nhận ${zones[state.zone].badge}`);
      }
    }

    function animateSprite(which, cls){
      const id = which === "player" ? "playerSprite" : "enemySprite";
      const el = $(id);
      if(!el) return;
      el.classList.add(cls);
      setTimeout(()=>el.classList.remove(cls), 420);
    }

    function animateMove(move, fromPlayer){
      const layer = $("fxLayer");
      if(!layer) return;
      layer.innerHTML = "";

      const presets = {
        fire:{ count:8, color1:"#fff7ed", color2:"#fb923c", size:[16,34], shape:"circle" },
        water:{ count:9, color1:"#e0f2fe", color2:"#38bdf8", size:[12,28], shape:"drop" },
        grass:{ count:10, color1:"#dcfce7", color2:"#22c55e", size:[10,24], shape:"leaf" },
        electric:{ count:7, color1:"#fef9c3", color2:"#fde047", size:[18,34], shape:"bolt" },
        psychic:{ count:6, color1:"#f5d0fe", color2:"#c084fc", size:[22,38], shape:"ring" },
        ice:{ count:8, color1:"#ecfeff", color2:"#67e8f9", size:[14,28], shape:"star" },
        rock:{ count:8, color1:"#e7e5e4", color2:"#a8a29e", size:[12,28], shape:"rock" },
        ground:{ count:9, color1:"#fef3c7", color2:"#d97706", size:[12,30], shape:"dust" },
        ghost:{ count:7, color1:"#ddd6fe", color2:"#818cf8", size:[20,34], shape:"mist" },
        dark:{ count:7, color1:"#94a3b8", color2:"#111827", size:[20,36], shape:"shadow" },
        dragon:{ count:8, color1:"#dbeafe", color2:"#2563eb", size:[20,36], shape:"meteor" },
        fighting:{ count:7, color1:"#fee2e2", color2:"#ef4444", size:[18,34], shape:"shock" },
        poison:{ count:9, color1:"#f3e8ff", color2:"#a855f7", size:[14,28], shape:"bubble" },
        bug:{ count:10, color1:"#ecfccb", color2:"#84cc16", size:[12,26], shape:"leaf" },
        flying:{ count:9, color1:"#e0f2fe", color2:"#93c5fd", size:[12,28], shape:"feather" },
        fairy:{ count:10, color1:"#fce7f3", color2:"#f472b6", size:[12,26], shape:"sparkle" },
        steel:{ count:8, color1:"#f8fafc", color2:"#94a3b8", size:[12,28], shape:"metal" },
        normal:{ count:7, color1:"#f8fafc", color2:"#cbd5e1", size:[12,26], shape:"circle" }
      };

      const p = presets[move.fx] || presets.normal;
      const startX = fromPlayer ? 160 : window.innerWidth > 720 ? 680 : 240;
      const startY = fromPlayer ? 220 : 140;
      const dxBase = fromPlayer ? 360 : -360;
      const dyBase = fromPlayer ? -90 : 90;

      for(let i=0;i<p.count;i++){
        const shot = document.createElement("div");
        const size = rand(p.size[0], p.size[1]);
        const isRing = p.shape === "ring" || (Math.random() < 0.12 && ["psychic","fairy","ghost"].includes(move.fx));

        shot.className = isRing ? "fx-ring" : "fx-shot";
        if(!isRing){
          shot.style.width = size + "px";
          shot.style.height = size + "px";
          applyShapeStyle(shot, p, size);
        }else{
          shot.style.width = size + 30 + "px";
          shot.style.height = size + 30 + "px";
          shot.style.borderColor = p.color2;
        }

        const sx = startX + rand(-15, 20);
        const sy = startY + rand(-25, 30);
        shot.style.left = sx + "px";
        shot.style.top = sy + "px";
        shot.style.setProperty("--dx", (dxBase + rand(-40, 40)) + "px");
        shot.style.setProperty("--dy", (dyBase + rand(-80, 80)) + "px");
        shot.style.animationDelay = (i * 0.02) + "s";
        layer.appendChild(shot);
      }

      const burst = document.createElement("div");
      burst.className = "fx-burst";
      burst.style.width = "110px";
      burst.style.height = "110px";
      burst.style.left = fromPlayer ? "64%" : "18%";
      burst.style.top = fromPlayer ? "34%" : "54%";
      burst.style.background = `radial-gradient(circle, ${p.color1}, ${p.color2}, transparent 72%)`;
      layer.appendChild(burst);

      setTimeout(()=>layer.innerHTML = "", 820);
    }

    function applyShapeStyle(el, preset, size){
      const c1 = preset.color1;
      const c2 = preset.color2;
      if(["circle","bubble","shadow"].includes(preset.shape)){
        el.style.borderRadius = "50%";
        el.style.background = `radial-gradient(circle, ${c1}, ${c2})`;
      } else if(preset.shape === "drop"){
        el.style.borderRadius = "50% 50% 50% 0";
        el.style.transform = "rotate(45deg)";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
      } else if(preset.shape === "leaf" || preset.shape === "feather"){
        el.style.width = size + 8 + "px";
        el.style.height = Math.max(10, size - 4) + "px";
        el.style.borderRadius = "100% 0 100% 0";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
      } else if(preset.shape === "bolt"){
        el.style.width = size + 18 + "px";
        el.style.height = size + 18 + "px";
        el.style.clipPath = "polygon(40% 0, 72% 0, 56% 34%, 86% 34%, 30% 100%, 44% 52%, 18% 52%)";
        el.style.background = c2;
      } else if(preset.shape === "star" || preset.shape === "sparkle"){
        el.style.width = size + 14 + "px";
        el.style.height = size + 14 + "px";
        el.style.clipPath = "polygon(50% 0, 61% 37%, 100% 50%, 61% 63%, 50% 100%, 39% 63%, 0 50%, 39% 37%)";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
      } else if(["rock","dust","metal","meteor","shock"].includes(preset.shape)){
        el.style.borderRadius = "18%";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
        if(preset.shape === "meteor" || preset.shape === "shock"){
          el.style.boxShadow = `0 0 12px ${c2}`;
        }
      } else if(preset.shape === "mist"){
        el.style.borderRadius = "50%";
        el.style.background = `radial-gradient(circle, ${c2}, transparent 70%)`;
      } else {
        el.style.borderRadius = "50%";
        el.style.background = `radial-gradient(circle, ${c1}, ${c2})`;
      }
    }

    function dexSearch(value){
      state.dexSearch = value;
      renderDex();
    }

    function wait(ms){ return new Promise(r=>setTimeout(r, ms)); }

    async function initGame(){
      renderTabs();
      renderTopStats();
      bodyTheme();

      await getDexIndex();

      const starterIds = [1, 4, 7, 25, 133, 152];
      const levels = [6, 6, 6, 7, 6, 6];
      for(let i=0;i<starterIds.length;i++){
        const mon = await createOwnedPokemon(starterIds[i], levels[i]);
        state.collection.push(mon);
        state.seen.add(mon.id);
      }
      state.activeIndex = 0;

      log("journey", "Giáo sư trao cho bạn 6 Pokémon khởi đầu để hành trình thêm phong phú.");
      log("explore", "Bạn có thể khám phá theo nhiều cách khác nhau, không còn đơn điệu.");
      renderCurrentTab();
      await explore("wander");
    }

    initGame();

    window.openTab = openTab;
    window.selectZone = selectZone;
    window.explore = explore;
    window.setActive = setActive;
    window.useMove = useMove;
    window.chargeEnergy = chargeEnergy;
    window.throwBall = throwBall;
    window.restAll = restAll;
    window.trainAll = trainAll;
    window.useItemOnActive = useItemOnActive;
    window.buyItem = buyItem;
    window.dexSearch = dexSearch;
    window.loadDexDetail = loadDexDetail;
    window.selectEvolutionMon = selectEvolutionMon;
    window.evolveSelected = evolveSelected;
  </script>
</body>
</html>        radial-gradient(circle at 90% 0%, rgba(250,204,21,.18), transparent 18%),
        linear-gradient(135deg, var(--bg1), var(--bg2));
      transition:background .35s;
      overflow-x:hidden;
    }

    body.theme-forest{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.18), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(134,239,172,.20), transparent 18%),
        linear-gradient(135deg, #0b1320, #14532d 45%, #0f766e 100%);
    }
    body.theme-cave{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.14), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(148,163,184,.18), transparent 18%),
        linear-gradient(135deg, #0f172a, #1e293b 45%, #334155 100%);
    }
    body.theme-volcano{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.16), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(251,146,60,.22), transparent 18%),
        linear-gradient(135deg, #1f2937, #7f1d1d 45%, #ea580c 100%);
    }
    body.theme-ocean{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.16), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(125,211,252,.20), transparent 18%),
        linear-gradient(135deg, #082f49, #075985 45%, #2563eb 100%);
    }
    body.theme-sky{
      background:
        radial-gradient(circle at 10% 15%, rgba(255,255,255,.18), transparent 20%),
        radial-gradient(circle at 90% 0%, rgba(196,181,253,.25), transparent 18%),
        linear-gradient(135deg, #312e81, #2563eb 45%, #7c3aed 100%);
    }

    .app{
      max-width:1400px;
      margin:0 auto;
      padding:18px;
    }

    .topbar{
      display:flex;
      justify-content:space-between;
      gap:14px;
      flex-wrap:wrap;
      align-items:flex-start;
      margin-bottom:14px;
    }
    .brand h1{
      margin:0;
      font-size:clamp(28px, 4vw, 52px);
      line-height:1;
      letter-spacing:-1.5px;
    }
    .brand p{
      margin:8px 0 0;
      color:var(--muted);
      max-width:760px;
    }

    .stats{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      justify-content:flex-end;
    }
    .stat-pill{
      padding:10px 14px;
      border-radius:999px;
      background:rgba(0,0,0,.22);
      border:1px solid var(--line);
      backdrop-filter:blur(12px);
      font-weight:800;
      box-shadow:var(--shadow);
    }

    .tabs{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:14px;
    }
    .tab-btn{
      border:none;
      cursor:pointer;
      padding:12px 14px;
      border-radius:16px;
      background:rgba(255,255,255,.10);
      color:var(--text);
      font-weight:800;
      border:1px solid var(--line);
      backdrop-filter:blur(10px);
      transition:.18s;
    }
    .tab-btn.active,
    .tab-btn:hover{
      transform:translateY(-1px);
      background:rgba(255,255,255,.22);
    }

    .pane{
      display:none;
      grid-template-columns:1fr;
      gap:14px;
    }
    .pane.active{ display:grid; }

    .grid-2{ display:grid; grid-template-columns:1.08fr .92fr; gap:14px; }
    .grid-3{ display:grid; grid-template-columns:1fr 1fr 1fr; gap:14px; }

    .card{
      background:var(--glass);
      border:1px solid var(--line);
      border-radius:var(--radius);
      padding:16px;
      box-shadow:var(--shadow);
      backdrop-filter:blur(16px);
    }
    .card h2, .card h3{
      margin:0 0 12px;
    }
    .sub{
      color:var(--muted);
      font-size:14px;
    }

    .zone-strip{
      display:grid;
      grid-template-columns:repeat(5, 1fr);
      gap:10px;
      margin-top:10px;
    }
    .zone-card{
      background:rgba(0,0,0,.18);
      border:1px solid var(--line);
      border-radius:18px;
      padding:12px;
      cursor:pointer;
      transition:.16s;
    }
    .zone-card:hover,
    .zone-card.active{
      background:rgba(255,255,255,.22);
      transform:translateY(-1px);
    }
    .zone-card.locked{
      opacity:.45;
      cursor:not-allowed;
    }
    .zone-card b{ display:block; margin-bottom:4px; }

    .explore-actions{
      display:grid;
      grid-template-columns:repeat(5, 1fr);
      gap:10px;
    }
    .action-card{
      background:rgba(255,255,255,.10);
      border:1px solid var(--line);
      border-radius:18px;
      padding:14px;
      cursor:pointer;
      transition:.16s;
      min-height:125px;
    }
    .action-card:hover{
      transform:translateY(-2px);
      background:rgba(255,255,255,.20);
    }
    .action-card .icon{
      font-size:28px;
      margin-bottom:8px;
    }

    .big-btn, .small-btn{
      border:none;
      border-radius:16px;
      cursor:pointer;
      font-weight:800;
      transition:.15s;
      box-shadow:0 8px 18px rgba(0,0,0,.18);
    }
    .big-btn{
      padding:12px 16px;
      background:linear-gradient(135deg, #fde68a, #facc15);
      color:#111827;
    }
    .small-btn{
      padding:9px 12px;
      background:rgba(255,255,255,.92);
      color:#111827;
    }
    .big-btn:hover, .small-btn:hover{ transform:translateY(-1px); }
    .btn-green{ background:linear-gradient(135deg, #bbf7d0, #4ade80); color:#062a12; }
    .btn-red{ background:linear-gradient(135deg, #fecdd3, #fb7185); color:#3b0712; }
    .btn-blue{ background:linear-gradient(135deg, #dbeafe, #60a5fa); color:#0c2340; }
    .btn-purple{ background:linear-gradient(135deg, #ede9fe, #a78bfa); color:#241449; }

    .log{
      height:190px;
      overflow:auto;
      border-radius:18px;
      background:rgba(0,0,0,.22);
      border:1px solid var(--line);
      padding:12px;
      line-height:1.45;
      font-size:14px;
    }

    .battle-scene{
      position:relative;
      min-height:390px;
      border-radius:24px;
      overflow:hidden;
      border:1px solid var(--line);
      background:linear-gradient(180deg, rgba(255,255,255,.22), rgba(0,0,0,.12));
    }
    .battle-scene::before{
      content:"";
      position:absolute; inset:0;
      background:
        radial-gradient(circle at 75% 18%, rgba(255,255,255,.78) 0 7%, transparent 8%),
        linear-gradient(transparent 65%, rgba(0,0,0,.18) 66%);
      opacity:.7;
    }
    .battle-scene.forest{ background:linear-gradient(180deg, #7dd3fc, #34d399 58%, #14532d); }
    .battle-scene.cave{ background:linear-gradient(180deg, #64748b, #1f2937 60%, #0f172a); }
    .battle-scene.volcano{ background:linear-gradient(180deg, #fdba74, #b91c1c 58%, #111827); }
    .battle-scene.ocean{ background:linear-gradient(180deg, #bae6fd, #0ea5e9 58%, #082f49); }
    .battle-scene.sky{ background:linear-gradient(180deg, #ddd6fe, #60a5fa 60%, #312e81); }

    .arena-shadow{
      position:absolute;
      width:200px; height:56px;
      border-radius:50%;
      background:radial-gradient(ellipse, rgba(255,255,255,.35), rgba(0,0,0,.20));
      bottom:34px;
      filter:blur(1px);
    }
    .arena-shadow.left{ left:40px; }
    .arena-shadow.right{ right:40px; top:auto; bottom:104px; }

    .poke{
      position:absolute;
      width:180px;
      height:180px;
      object-fit:contain;
      z-index:3;
      filter:drop-shadow(0 18px 18px rgba(0,0,0,.35));
      transition:transform .26s, filter .26s;
    }
    .poke.player{ left:42px; bottom:48px; transform:scaleX(-1); }
    .poke.enemy{ right:42px; bottom:110px; }
    .poke.hit{ animation:hit .35s ease-in-out; }
    .poke.attack{ animation:attack .42s ease-in-out; }

    @keyframes hit{
      0%,100%{ filter:drop-shadow(0 18px 18px rgba(0,0,0,.35)); }
      50%{ filter:brightness(1.9) drop-shadow(0 0 18px #fff); transform:translateX(12px); }
    }
    @keyframes attack{
      0%,100%{}
      50%{ transform:translateX(34px) scale(1.08); }
    }

    .battle-hud{
      display:grid;
      grid-template-columns:1fr 1fr;
      gap:12px;
      margin-top:12px;
    }
    .hud-card{
      padding:12px;
      border-radius:18px;
      background:rgba(0,0,0,.18);
      border:1px solid var(--line);
    }
    .hud-head{
      display:flex;
      justify-content:space-between;
      gap:8px;
      font-weight:900;
    }
    .bar{
      height:12px;
      border-radius:999px;
      overflow:hidden;
      background:rgba(0,0,0,.30);
      margin-top:8px;
    }
    .bar span{
      display:block;
      height:100%;
      border-radius:999px;
      transition:width .3s;
    }
    .hp{ background:linear-gradient(90deg, #22c55e, #eab308, #ef4444); }
    .en{ background:linear-gradient(90deg, #38bdf8, #a78bfa); }

    .move-grid{
      display:grid;
      grid-template-columns:repeat(2, 1fr);
      gap:10px;
      margin-top:12px;
    }
    .move-btn{
      text-align:left;
      padding:12px;
      border:none;
      border-radius:18px;
      cursor:pointer;
      background:rgba(255,255,255,.92);
      color:#111827;
      box-shadow:0 8px 16px rgba(0,0,0,.12);
      transition:.15s;
    }
    .move-btn:hover{ transform:translateY(-1px); }
    .move-btn:disabled{ opacity:.45; cursor:not-allowed; }
    .move-btn small{
      display:block;
      margin-top:4px;
      color:#334155;
      font-weight:700;
    }

    .inline-actions{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-top:12px;
    }

    .team-grid, .dex-grid, .evo-grid, .shop-grid{
      display:grid;
      grid-template-columns:repeat(auto-fill, minmax(170px, 1fr));
      gap:10px;
    }
    .mini-mon{
      background:rgba(255,255,255,.12);
      border:1px solid var(--line);
      border-radius:18px;
      padding:10px;
      text-align:center;
      cursor:pointer;
      transition:.15s;
    }
    .mini-mon:hover, .mini-mon.active{
      transform:translateY(-1px);
      background:rgba(255,255,255,.24);
    }
    .mini-mon img{
      width:84px;
      height:84px;
      object-fit:contain;
      filter:drop-shadow(0 12px 12px rgba(0,0,0,.25));
    }

    .type-wrap{
      display:flex;
      flex-wrap:wrap;
      gap:4px;
      justify-content:center;
      margin-top:6px;
    }
    .type{
      font-size:11px;
      padding:4px 8px;
      border-radius:999px;
      background:rgba(0,0,0,.24);
      font-weight:800;
    }

    .search-row{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:12px;
    }
    input, select{
      padding:12px 14px;
      border-radius:14px;
      border:1px solid var(--line);
      background:rgba(255,255,255,.12);
      color:var(--text);
      outline:none;
      min-width:160px;
    }
    input::placeholder{ color:#e2e8f0; }

    .dex-list{
      display:grid;
      grid-template-columns:repeat(auto-fill, minmax(130px, 1fr));
      gap:10px;
      max-height:540px;
      overflow:auto;
      padding-right:4px;
    }
    .dex-item{
      background:rgba(255,255,255,.10);
      border:1px solid var(--line);
      border-radius:16px;
      padding:10px;
      text-align:center;
      cursor:pointer;
      transition:.15s;
    }
    .dex-item:hover{
      transform:translateY(-1px);
      background:rgba(255,255,255,.20);
    }
    .dex-item img{
      width:72px;
      height:72px;
      object-fit:contain;
    }

    .detail-grid{
      display:grid;
      grid-template-columns:repeat(2, 1fr);
      gap:10px;
    }
    .detail-box{
      background:rgba(0,0,0,.18);
      border:1px solid var(--line);
      border-radius:18px;
      padding:12px;
    }

    .badge-list{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
    }
    .badge{
      padding:10px 12px;
      border-radius:999px;
      background:rgba(255,255,255,.14);
      border:1px solid var(--line);
      font-weight:800;
    }

    .shop-item{
      background:rgba(255,255,255,.12);
      border:1px solid var(--line);
      border-radius:18px;
      padding:12px;
    }

    .toast{
      position:fixed;
      left:50%;
      bottom:18px;
      transform:translateX(-50%);
      padding:12px 16px;
      border-radius:999px;
      background:rgba(0,0,0,.76);
      border:1px solid var(--line);
      display:none;
      z-index:99;
      font-weight:800;
    }

    .fx-layer{
      position:absolute;
      inset:0;
      z-index:5;
      pointer-events:none;
      overflow:hidden;
    }
    .fx-shot{
      position:absolute;
      opacity:0;
      animation:fxfly .7s ease-out forwards;
    }
    .fx-ring{
      position:absolute;
      border-radius:50%;
      opacity:0;
      animation:fxring .65s ease-out forwards;
      border:6px solid white;
    }
    .fx-burst{
      position:absolute;
      border-radius:50%;
      opacity:0;
      animation:fxburst .7s ease-out forwards;
    }

    @keyframes fxfly{
      0%{ transform:translate(0,0) scale(.5); opacity:1; }
      100%{ transform:translate(var(--dx), var(--dy)) scale(1.3) rotate(360deg); opacity:0; }
    }
    @keyframes fxring{
      0%{ transform:scale(.2); opacity:0; }
      35%{ opacity:1; }
      100%{ transform:scale(1.7); opacity:0; }
    }
    @keyframes fxburst{
      0%{ transform:scale(.2); opacity:0; }
      45%{ opacity:1; }
      100%{ transform:scale(1.8); opacity:0; }
    }

    @media (max-width:1100px){
      .grid-2, .grid-3{ grid-template-columns:1fr; }
      .zone-strip{ grid-template-columns:repeat(2, 1fr); }
      .explore-actions{ grid-template-columns:repeat(2, 1fr); }
    }
    @media (max-width:720px){
      .move-grid, .battle-hud{ grid-template-columns:1fr; }
      .poke{ width:126px; height:126px; }
      .poke.player{ left:12px; }
      .poke.enemy{ right:12px; }
      .zone-strip, .explore-actions{ grid-template-columns:1fr; }
    }
  </style>
</head>
<body class="theme-forest">
  <div class="app">
    <div class="topbar">
      <div class="brand">
        <h1>Pokémon Odyssey Ultimate</h1>
        <p>Bản mở rộng lớn: nhiều tab riêng, Pokédex/Từ điển Pokémon, tiến hoá nhiều kiểu, khám phá đa dạng, thêm nhiều Pokémon, hiệu ứng chiêu thức đẹp và hành trình phong phú hơn.</p>
      </div>
      <div class="stats" id="topStats"></div>
    </div>

    <div class="tabs" id="tabs"></div>

    <section class="pane active" id="tab-explore"></section>
    <section class="pane" id="tab-battle"></section>
    <section class="pane" id="tab-team"></section>
    <section class="pane" id="tab-dex"></section>
    <section class="pane" id="tab-evolution"></section>
    <section class="pane" id="tab-journey"></section>
    <section class="pane" id="tab-shop"></section>
  </div>

  <div class="toast" id="toast"></div>

  <script>
    const API = "https://pokeapi.co/api/v2";
    const MAX_POKEMON = 251;

    const zones = [
      { id:0, name:"Verdant Forest", theme:"forest", min:1,   max:60,  unlock:0, desc:"Cỏ, bọ, chim, sinh vật rừng", badge:"Leaf Badge" },
      { id:1, name:"Crystal Cave",   theme:"cave",   min:41,  max:110, unlock:1, desc:"Đá, độc, chiến binh hang động", badge:"Stone Badge" },
      { id:2, name:"Blazing Volcano",theme:"volcano",min:56,  max:146, unlock:2, desc:"Lửa, đất, quái vật nóng chảy", badge:"Flame Badge" },
      { id:3, name:"Azure Coast",    theme:"ocean",  min:72,  max:186, unlock:3, desc:"Nước, băng, sinh vật đại dương", badge:"Wave Badge" },
      { id:4, name:"Sky Temple",     theme:"sky",    min:120, max:251, unlock:4, desc:"Tâm linh, rồng, hiếm và huyền thoại", badge:"Legend Badge" }
    ];

    const exploreModes = [
      { id:"wander", icon:"🌿", name:"Rảo quanh", desc:"Gặp Pokémon ngẫu nhiên, dễ nhặt item." },
      { id:"rare", icon:"✨", name:"Săn hiếm", desc:"Tăng cơ hội gặp Pokémon hiếm và mạnh." },
      { id:"water", icon:"🎣", name:"Tìm nguồn nước", desc:"Dễ gặp hệ Nước / Băng / Điện." },
      { id:"ruins", icon:"🏛️", name:"Khám phá phế tích", desc:"Có thể gặp hệ Tâm linh / Ma / Đá." },
      { id:"camp", icon:"⛺", name:"Dựng trại", desc:"Hồi đội, tăng tình bạn, nhận sự kiện nghỉ ngơi." }
    ];

    const itemCatalog = {
      pokeBall:      { name:"Poké Ball", price:80, emoji:"⚪", desc:"Bắt Pokémon thường." },
      greatBall:     { name:"Great Ball", price:180, emoji:"🔵", desc:"Tăng tỉ lệ bắt." },
      potion:        { name:"Potion", price:60, emoji:"🧪", desc:"+35 HP cho 1 Pokémon." },
      superPotion:   { name:"Super Potion", price:120, emoji:"💊", desc:"+70 HP cho 1 Pokémon." },
      rareCandy:     { name:"Rare Candy", price:250, emoji:"🍬", desc:"+1 cấp cho 1 Pokémon." },
      fireStone:     { name:"Fire Stone", price:400, emoji:"🔥", desc:"Tiến hoá bằng đá lửa." },
      waterStone:    { name:"Water Stone", price:400, emoji:"💧", desc:"Tiến hoá bằng đá nước." },
      thunderStone:  { name:"Thunder Stone", price:400, emoji:"⚡", desc:"Tiến hoá bằng đá điện." },
      leafStone:     { name:"Leaf Stone", price:400, emoji:"🍃", desc:"Tiến hoá bằng đá lá." },
      moonStone:     { name:"Moon Stone", price:420, emoji:"🌙", desc:"Tiến hoá bằng đá mặt trăng." },
      sunStone:      { name:"Sun Stone", price:420, emoji:"☀️", desc:"Tiến hoá bằng đá mặt trời." },
      linkCable:     { name:"Link Cable", price:360, emoji:"🔗", desc:"Mô phỏng trade evolution." },
      friendshipCharm:{ name:"Friendship Charm", price:300, emoji:"💖", desc:"+40 friendship cho 1 Pokémon." },
      evoShard:      { name:"Evolution Shard", price:500, emoji:"💠", desc:"Dùng cho vài tiến hoá đặc biệt." }
    };

    const typeMoves = {
      normal: [
        { name:"Quick Strike", power:18, cost:0, fx:"normal" },
        { name:"Double Hit", power:26, cost:10, fx:"normal" },
        { name:"Hyper Dash", power:42, cost:24, fx:"normal" },
        { name:"Omega Rush", power:62, cost:42, fx:"normal" }
      ],
      fire: [
        { name:"Ember Burst", power:20, cost:0, fx:"fire" },
        { name:"Flame Wheel", power:28, cost:10, fx:"fire" },
        { name:"Inferno Fang", power:46, cost:26, fx:"fire" },
        { name:"Solar Inferno", power:68, cost:48, fx:"fire" }
      ],
      water: [
        { name:"Bubble Jet", power:18, cost:0, fx:"water" },
        { name:"Aqua Slash", power:28, cost:10, fx:"water" },
        { name:"Tidal Crush", power:44, cost:24, fx:"water" },
        { name:"Ocean Cataclysm", power:66, cost:46, fx:"water" }
      ],
      grass: [
        { name:"Leaf Cutter", power:18, cost:0, fx:"grass" },
        { name:"Vine Lash", power:27, cost:10, fx:"grass" },
        { name:"Bloom Storm", power:44, cost:24, fx:"grass" },
        { name:"Emerald Tempest", power:65, cost:46, fx:"grass" }
      ],
      electric: [
        { name:"Spark Bolt", power:19, cost:0, fx:"electric" },
        { name:"Volt Dash", power:30, cost:12, fx:"electric" },
        { name:"Thunder Cage", power:48, cost:28, fx:"electric" },
        { name:"Heaven Thunder", power:72, cost:50, fx:"electric" }
      ],
      psychic: [
        { name:"Mind Tap", power:18, cost:0, fx:"psychic" },
        { name:"Psy Cut", power:28, cost:10, fx:"psychic" },
        { name:"Dream Nova", power:45, cost:25, fx:"psychic" },
        { name:"Astral Collapse", power:68, cost:48, fx:"psychic" }
      ],
      ice: [
        { name:"Frost Needle", power:18, cost:0, fx:"ice" },
        { name:"Ice Spear", power:28, cost:10, fx:"ice" },
        { name:"Snow Burst", power:45, cost:25, fx:"ice" },
        { name:"Absolute Zero", power:67, cost:48, fx:"ice" }
      ],
      rock: [
        { name:"Stone Toss", power:20, cost:0, fx:"rock" },
        { name:"Rock Break", power:28, cost:10, fx:"rock" },
        { name:"Meteor Crash", power:46, cost:26, fx:"rock" },
        { name:"Mountain Ruin", power:67, cost:48, fx:"rock" }
      ],
      ground: [
        { name:"Mud Jab", power:19, cost:0, fx:"ground" },
        { name:"Earth Kick", power:28, cost:10, fx:"ground" },
        { name:"Quake Roar", power:46, cost:26, fx:"ground" },
        { name:"Continental Rift", power:68, cost:48, fx:"ground" }
      ],
      ghost: [
        { name:"Spirit Touch", power:18, cost:0, fx:"ghost" },
        { name:"Night Swipe", power:29, cost:11, fx:"ghost" },
        { name:"Haunt Wave", power:46, cost:26, fx:"ghost" },
        { name:"Phantom Realm", power:67, cost:48, fx:"ghost" }
      ],
      dark: [
        { name:"Shadow Bite", power:20, cost:0, fx:"dark" },
        { name:"Night Claw", power:30, cost:12, fx:"dark" },
        { name:"Abyss Fang", power:47, cost:28, fx:"dark" },
        { name:"Eclipse Doom", power:70, cost:50, fx:"dark" }
      ],
      dragon: [
        { name:"Dragon Spark", power:22, cost:0, fx:"dragon" },
        { name:"Scale Break", power:32, cost:12, fx:"dragon" },
        { name:"Draco Rampage", power:50, cost:30, fx:"dragon" },
        { name:"Dragon Starfall", power:75, cost:52, fx:"dragon" }
      ],
      fighting: [
        { name:"Power Jab", power:20, cost:0, fx:"fighting" },
        { name:"Cross Punch", power:30, cost:12, fx:"fighting" },
        { name:"Aura Smash", power:48, cost:28, fx:"fighting" },
        { name:"Titan Breaker", power:70, cost:50, fx:"fighting" }
      ],
      poison: [
        { name:"Toxic Sting", power:18, cost:0, fx:"poison" },
        { name:"Venom Edge", power:28, cost:10, fx:"poison" },
        { name:"Sludge Wave", power:45, cost:24, fx:"poison" },
        { name:"Plague Bloom", power:67, cost:48, fx:"poison" }
      ],
      bug: [
        { name:"Bug Bite", power:18, cost:0, fx:"bug" },
        { name:"Wing Slice", power:27, cost:10, fx:"bug" },
        { name:"Swarm Burst", power:43, cost:24, fx:"bug" },
        { name:"Queen Swarm", power:64, cost:46, fx:"bug" }
      ],
      flying: [
        { name:"Gust Blade", power:18, cost:0, fx:"flying" },
        { name:"Sky Peck", power:28, cost:10, fx:"flying" },
        { name:"Storm Dive", power:45, cost:24, fx:"flying" },
        { name:"Hurricane Halo", power:66, cost:46, fx:"flying" }
      ],
      fairy: [
        { name:"Fairy Kiss", power:18, cost:0, fx:"fairy" },
        { name:"Moon Spark", power:28, cost:10, fx:"fairy" },
        { name:"Star Ribbon", power:45, cost:24, fx:"fairy" },
        { name:"Miracle Waltz", power:66, cost:46, fx:"fairy" }
      ],
      steel: [
        { name:"Iron Tap", power:19, cost:0, fx:"steel" },
        { name:"Metal Slash", power:29, cost:11, fx:"steel" },
        { name:"Chrome Cannon", power:47, cost:27, fx:"steel" },
        { name:"Titanium Storm", power:68, cost:48, fx:"steel" }
      ]
    };

    const tabs = [
      { id:"explore", text:"🌍 Khám phá" },
      { id:"battle", text:"⚔️ Chiến đấu" },
      { id:"team", text:"📦 Đội hình" },
      { id:"dex", text:"📘 Từ điển" },
      { id:"evolution", text:"🧬 Tiến hoá" },
      { id:"journey", text:"🏆 Hành trình" },
      { id:"shop", text:"🛒 Cửa hàng" }
    ];

    const actionPools = {
      water:[54,60,72,73,79,80,86,87,90,98,99,116,117,118,119,120,121,129,130,131,138,139,140,141,170,171,183,186,194,195,211,222,223,224,226,230],
      ruins:[63,64,65,92,93,94,95,96,97,102,103,104,105,122,124,144,150,200,201,202,203,205,208,213,228,229,235,237],
      rare:[25,26,59,65,68,94,130,131,143,149,150,151,154,157,160,181,196,197,212,214,230,243,244,245,248,249,250,251],
      volcanic:[37,38,58,59,77,78,126,136,155,156,157,218,219,228,229,240,244],
      cave:[41,42,74,75,76,95,104,105,109,110,111,112,169,185,198,200,207,208,213,214],
      forest:[10,11,12,13,14,15,16,17,18,19,20,21,22,43,44,45,46,47,48,49,69,70,71,83,84,85,114,123,127,151,152,153,154,163,164,165,166,167,168,177,178,187,188,189,190,191,192,193,204,205],
      sky:[16,17,18,21,22,41,42,84,85,144,145,146,163,164,177,178,187,188,189,198,225,226,227]
    };

    const state = {
      loading:true,
      currentTab:"explore",
      zone:0,
      coins:500,
      badges:0,
      zoneWins:[0,0,0,0,0],
      captureCount:0,
      battleBusy:false,
      cache:new Map(),
      speciesCache:new Map(),
      evoCache:new Map(),
      dexIndex:[],
      collection:[],
      activeIndex:0,
      enemy:null,
      seen:new Set(),
      logs:{
        explore:["Chào mừng đến với Pokémon Odyssey Ultimate!"],
        battle:["Hệ thống chiến đấu mới đã sẵn sàng."],
        journey:["Bắt đầu hành trình!"]
      },
      bag:{
        pokeBall:12,
        greatBall:4,
        potion:5,
        superPotion:2,
        rareCandy:2,
        fireStone:1,
        waterStone:1,
        thunderStone:1,
        leafStone:1,
        moonStone:1,
        sunStone:1,
        linkCable:1,
        friendshipCharm:2,
        evoShard:1
      }
    };

    const $ = id => document.getElementById(id);
    const cap = s => s ? s.charAt(0).toUpperCase() + s.slice(1).replace(/-/g, " ") : "";
    const rand = (a,b) => Math.floor(Math.random()*(b-a+1))+a;
    const pick = arr => arr[Math.floor(Math.random()*arr.length)];
    const clamp = (v,min,max) => Math.max(min, Math.min(max, v));

    function toast(msg){
      const t = $("toast");
      t.textContent = msg;
      t.style.display = "block";
      clearTimeout(t._timer);
      t._timer = setTimeout(()=>t.style.display="none", 1800);
    }

    function log(type, msg){
      state.logs[type].unshift("• " + msg);
      if(state.logs[type].length > 80) state.logs[type].length = 80;
      renderCurrentTab();
    }

    function bodyTheme(){
      document.body.className = "theme-" + zones[state.zone].theme;
    }

    async function fetchJSON(url){
      const r = await fetch(url);
      if(!r.ok) throw new Error("Fetch failed");
      return r.json();
    }

    async function getPokemonData(idOrName){
      const key = String(idOrName).toLowerCase();
      if(state.cache.has(key)) return state.cache.get(key);
      const data = await fetchJSON(`${API}/pokemon/${key}`);
      const base = {
        id:data.id,
        name:data.name,
        types:data.types.map(t=>t.type.name),
        abilities:data.abilities.map(a=>a.ability.name),
        stats:{
          hp:data.stats.find(s=>s.stat.name==="hp")?.base_stat || 45,
          attack:data.stats.find(s=>s.stat.name==="attack")?.base_stat || 49,
          defense:data.stats.find(s=>s.stat.name==="defense")?.base_stat || 49,
          speed:data.stats.find(s=>s.stat.name==="speed")?.base_stat || 45
        },
        height:data.height,
        weight:data.weight,
        sprite:data.sprites.other?.["official-artwork"]?.front_default || data.sprites.front_default,
        shiny:data.sprites.front_shiny,
        speciesUrl:data.species.url
      };
      state.cache.set(key, base);
      state.cache.set(String(base.id), base);
      return base;
    }

    async function getSpecies(idOrName){
      const key = String(idOrName).toLowerCase();
      if(state.speciesCache.has(key)) return state.speciesCache.get(key);
      const data = await fetchJSON(`${API}/pokemon-species/${key}`);
      const species = {
        id:data.id,
        name:data.name,
        color:data.color?.name || "-",
        habitat:data.habitat?.name || "unknown",
        shape:data.shape?.name || "unknown",
        evolvesFrom:data.evolves_from_species?.name || null,
        evolutionChainUrl:data.evolution_chain?.url,
        flavor:(data.flavor_text_entries.find(x=>x.language.name==="en")?.flavor_text || "No description.").replace(/\f|\n/g, " "),
        genus:data.genera.find(x=>x.language.name==="en")?.genus || "-",
        growthRate:data.growth_rate?.name || "-",
        captureRate:data.capture_rate || 0,
        isLegendary:data.is_legendary,
        isMythical:data.is_mythical
      };
      state.speciesCache.set(key, species);
      state.speciesCache.set(String(species.id), species);
      return species;
    }

    async function getDexIndex(){
      try{
        const data = await fetchJSON(`${API}/pokemon?limit=${MAX_POKEMON}`);
        state.dexIndex = data.results.map((x, i)=>({ id:i+1, name:x.name }));
      }catch(err){
        state.dexIndex = [
          {id:1,name:"bulbasaur"},{id:4,name:"charmander"},{id:7,name:"squirtle"},
          {id:25,name:"pikachu"},{id:39,name:"jigglypuff"},{id:52,name:"meowth"},
          {id:133,name:"eevee"},{id:150,name:"mewtwo"},{id:151,name:"mew"}
        ];
      }
    }

    function computeStats(base, level){
      const maxHp = Math.round(base.stats.hp + level * 5.2);
      const attack = Math.round(base.stats.attack + level * 2.2);
      const defense = Math.round(base.stats.defense + level * 1.8);
      const speed = Math.round(base.stats.speed + level * 1.5);
      return { maxHp, attack, defense, speed };
    }

    function chooseMoves(types, level){
      const t1 = types[0] || "normal";
      const t2 = types[1] || "normal";
      const pool = [
        ...(typeMoves[t1] || typeMoves.normal),
        ...(t2 !== t1 ? (typeMoves[t2] || typeMoves.normal) : []),
        ...typeMoves.normal
      ];

      const chosen = [];
      function addFrom(list, idx){
        if(list[idx] && !chosen.some(m=>m.name===list[idx].name)) chosen.push({...list[idx], type:list[idx].fx === "normal" ? "normal" : (list[idx].type || null)});
      }

      const t1Moves = typeMoves[t1] || typeMoves.normal;
      const t2Moves = typeMoves[t2] || typeMoves.normal;

      addFrom(t1Moves, 0);
      addFrom(t1Moves, level >= 12 ? 1 : 0);
      addFrom(t2Moves, level >= 15 ? 2 : 1);
      addFrom(t1Moves, level >= 20 ? 3 : 2);

      while(chosen.length < 4){
        const m = pick(pool);
        if(!chosen.some(x=>x.name===m.name)) chosen.push({...m});
      }

      return chosen.slice(0,4).map(m=>({
        ...m,
        type: inferTypeFromFx(m.fx)
      }));
    }

    function inferTypeFromFx(fx){
      const map = {
        fire:"fire", water:"water", grass:"grass", electric:"electric", psychic:"psychic",
        ice:"ice", rock:"rock", ground:"ground", ghost:"ghost", dark:"dark",
        dragon:"dragon", fighting:"fighting", poison:"poison", bug:"bug",
        flying:"flying", fairy:"fairy", steel:"steel", normal:"normal"
      };
      return map[fx] || "normal";
    }

    async function createOwnedPokemon(idOrName, level){
      const base = await getPokemonData(idOrName);
      const stats = computeStats(base, level);
      return {
        uid: Date.now() + Math.random(),
        id: base.id,
        name: base.name,
        sprite: base.sprite,
        shiny: base.shiny,
        types: base.types,
        abilities: base.abilities,
        level,
        exp:0,
        friendship:60,
        hp:stats.maxHp,
        maxHp:stats.maxHp,
        attack:stats.attack,
        defense:stats.defense,
        speed:stats.speed,
        energy:35,
        maxEnergy:100,
        moves:chooseMoves(base.types, level),
        status:null
      };
    }

    function updateOwnedFromBase(mon, base){
      const stats = computeStats(base, mon.level);
      const hpRate = mon.maxHp > 0 ? mon.hp / mon.maxHp : 1;
      mon.id = base.id;
      mon.name = base.name;
      mon.sprite = base.sprite;
      mon.shiny = base.shiny;
      mon.types = base.types;
      mon.abilities = base.abilities;
      mon.maxHp = stats.maxHp;
      mon.attack = stats.attack;
      mon.defense = stats.defense;
      mon.speed = stats.speed;
      mon.hp = Math.round(mon.maxHp * hpRate);
      mon.moves = chooseMoves(base.types, mon.level);
      mon.maxEnergy = Math.min(140, 100 + Math.floor(mon.level / 5) * 4);
      mon.energy = clamp(mon.energy + 20, 0, mon.maxEnergy);
    }

    function getActive(){
      return state.collection[state.activeIndex];
    }

    function allTypesHtml(types){
      return `<div class="type-wrap">${types.map(t=>`<span class="type">${cap(t)}</span>`).join("")}</div>`;
    }

    function renderTopStats(){
      $("topStats").innerHTML = `
        <div class="stat-pill">🏅 Huy hiệu: ${state.badges}/${zones.length}</div>
        <div class="stat-pill">🪙 Coins: ${state.coins}</div>
        <div class="stat-pill">🎯 Đã bắt: ${state.captureCount}</div>
        <div class="stat-pill">🎒 Poké Ball: ${state.bag.pokeBall}</div>
        <div class="stat-pill">🔵 Great Ball: ${state.bag.greatBall}</div>
        <div class="stat-pill">📍 Khu vực: ${zones[state.zone].name}</div>
      `;
    }

    function renderTabs(){
      $("tabs").innerHTML = tabs.map(tab=>`
        <button class="tab-btn ${state.currentTab===tab.id ? "active" : ""}" onclick="openTab('${tab.id}')">${tab.text}</button>
      `).join("");
    }

    function openTab(tab){
      state.currentTab = tab;
      document.querySelectorAll(".pane").forEach(p=>p.classList.remove("active"));
      $(`tab-${tab}`).classList.add("active");
      renderTabs();
      renderCurrentTab();
    }

    function renderCurrentTab(){
      renderTopStats();
      if(state.currentTab==="explore") renderExplore();
      if(state.currentTab==="battle") renderBattle();
      if(state.currentTab==="team") renderTeam();
      if(state.currentTab==="dex") renderDex();
      if(state.currentTab==="evolution") renderEvolution();
      if(state.currentTab==="journey") renderJourney();
      if(state.currentTab==="shop") renderShop();
    }

    function renderZoneStrip(){
      return `
        <div class="zone-strip">
          ${zones.map(z=>`
            <div class="zone-card ${state.zone===z.id ? "active":""} ${state.badges<z.unlock ? "locked":""}" onclick="selectZone(${z.id})">
              <b>${z.name}</b>
              <div class="sub">${z.desc}</div>
              <div class="sub">Mở khóa: ${z.unlock} huy hiệu</div>
            </div>
          `).join("")}
        </div>
      `;
    }

    function renderExplore(){
      const active = getActive();
      $("tab-explore").innerHTML = `
        <div class="card">
          <h2>🌍 Khám phá khu vực</h2>
          <div class="sub">Chọn kiểu khám phá để hành trình không còn 1 màu. Mỗi lựa chọn có sự kiện khác nhau: bắt Pokémon, gặp Pokémon hiếm, nhận vật phẩm, tăng tình bạn hoặc gặp trận chiến mạnh hơn.</div>
          ${renderZoneStrip()}
        </div>

        <div class="grid-2">
          <div class="card">
            <h3>✨ Chọn cách khám phá</h3>
            <div class="explore-actions">
              ${exploreModes.map(mode=>`
                <div class="action-card" onclick="explore('${mode.id}')">
                  <div class="icon">${mode.icon}</div>
                  <b>${mode.name}</b>
                  <div class="sub">${mode.desc}</div>
                </div>
              `).join("")}
            </div>
            <div class="inline-actions" style="margin-top:14px">
              <button class="big-btn btn-green" onclick="restAll()">⛺ Nghỉ toàn đội</button>
              <button class="big-btn btn-blue" onclick="trainAll()">💪 Luyện tập toàn đội</button>
              <button class="big-btn btn-purple" onclick="openTab('battle')">⚔️ Sang tab chiến đấu</button>
            </div>
          </div>

          <div class="card">
            <h3>🧭 Thông tin hành trình</h3>
            <div class="detail-grid">
              <div class="detail-box">
                <b>Pokémon đang dẫn đội</b>
                ${active ? `
                  <div style="display:flex; gap:12px; align-items:center; margin-top:10px">
                    <img src="${active.sprite}" alt="${active.name}" style="width:90px; height:90px; object-fit:contain">
                    <div>
                      <div><b>${cap(active.name)}</b> • Lv.${active.level}</div>
                      <div class="sub">HP ${active.hp}/${active.maxHp} • Energy ${active.energy}/${active.maxEnergy}</div>
                      ${allTypesHtml(active.types)}
                    </div>
                  </div>
                ` : `<div class="sub">Chưa có Pokémon.</div>`}
              </div>
              <div class="detail-box">
                <b>Khu vực hiện tại</b>
                <div style="margin-top:10px">${zones[state.zone].name}</div>
                <div class="sub">${zones[state.zone].desc}</div>
                <div class="sub" style="margin-top:6px">Thắng tại khu vực: ${state.zoneWins[state.zone]} trận</div>
                <div class="sub">Huy hiệu khu vực: ${zones[state.zone].badge}</div>
              </div>
            </div>
            <div style="margin-top:12px">
              <b>📝 Nhật ký khám phá</b>
              <div class="log">${state.logs.explore.map(x=>`<div>${x}</div>`).join("")}</div>
            </div>
          </div>
        </div>
      `;
    }

    function battleSceneHtml(){
      const player = getActive();
      const enemy = state.enemy;
      const zone = zones[state.zone];
      return `
        <div class="battle-scene ${zone.theme}" id="scene">
          <div class="fx-layer" id="fxLayer"></div>
          <div class="arena-shadow left"></div>
          <div class="arena-shadow right"></div>
          ${player ? `<img src="${player.sprite}" class="poke player" id="playerSprite" alt="${player.name}">` : ""}
          ${enemy ? `<img src="${enemy.sprite}" class="poke enemy" id="enemySprite" alt="${enemy.name}">` : ""}
        </div>
      `;
    }

    function renderBattle(){
      const player = getActive();
      const enemy = state.enemy;
      $("tab-battle").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>⚔️ Chiến đấu</h2>
            <div class="sub">Mỗi hệ có hiệu ứng kỹ năng khác nhau: lửa, nước, cỏ, điện, ma, rồng, thép, tiên...</div>
            ${battleSceneHtml()}

            ${player && enemy ? `
              <div class="battle-hud">
                <div class="hud-card">
                  <div class="hud-head"><span>${cap(player.name)}</span><span>Lv.${player.level}</span></div>
                  <div class="bar"><span class="hp" style="width:${player.hp/player.maxHp*100}%"></span></div>
                  <small>HP ${player.hp}/${player.maxHp}</small>
                  <div class="bar"><span class="en" style="width:${player.energy/player.maxEnergy*100}%"></span></div>
                  <small>Năng lượng ${player.energy}/${player.maxEnergy}</small>
                </div>
                <div class="hud-card">
                  <div class="hud-head"><span>Wild ${cap(enemy.name)}</span><span>Lv.${enemy.level}</span></div>
                  <div class="bar"><span class="hp" style="width:${enemy.hp/enemy.maxHp*100}%"></span></div>
                  <small>HP ${enemy.hp}/${enemy.maxHp}</small>
                  <div class="bar"><span class="en" style="width:${enemy.energy/enemy.maxEnergy*100}%"></span></div>
                  <small>Năng lượng ${enemy.energy}/${enemy.maxEnergy}</small>
                </div>
              </div>

              <div class="move-grid">
                ${player.moves.map((m, i)=>`
                  <button class="move-btn" onclick="useMove(${i})" ${state.battleBusy || player.energy < m.cost || player.hp<=0 ? "disabled":""}>
                    ${m.name}
                    <small>${cap(m.type)} • Power ${m.power} • Cost ${m.cost}</small>
                  </button>
                `).join("")}
              </div>

              <div class="inline-actions">
                <button class="big-btn btn-blue" onclick="chargeEnergy()" ${state.battleBusy ? "disabled":""}>⚡ Tích năng lượng</button>
                <button class="big-btn btn-green" onclick="throwBall('pokeBall')" ${state.battleBusy || state.bag.pokeBall<=0 ? "disabled":""}>⚪ Ném Poké Ball</button>
                <button class="big-btn btn-purple" onclick="throwBall('greatBall')" ${state.battleBusy || state.bag.greatBall<=0 ? "disabled":""}>🔵 Ném Great Ball</button>
                <button class="big-btn btn-red" onclick="explore('wander')">➡️ Gặp đối thủ khác</button>
              </div>
            ` : `
              <div class="inline-actions">
                <button class="big-btn" onclick="explore('wander')">🔎 Tìm đối thủ</button>
              </div>
            `}
          </div>

          <div class="card">
            <h3>📜 Nhật ký chiến đấu</h3>
            <div class="log">${state.logs.battle.map(x=>`<div>${x}</div>`).join("")}</div>
          </div>
        </div>
      `;
    }

    function renderTeam(){
      const active = getActive();
      $("tab-team").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>📦 Đội Pokémon</h2>
            <div class="sub">Mỗi Pokémon có level, friendship, năng lượng, kỹ năng riêng. Chọn 1 Pokémon để dẫn đội hoặc dùng item trực tiếp.</div>
            <div class="team-grid" style="margin-top:12px">
              ${state.collection.map((m, i)=>`
                <div class="mini-mon ${i===state.activeIndex ? "active":""}" onclick="setActive(${i})">
                  <img src="${m.sprite}" alt="${m.name}">
                  <b>${cap(m.name)}</b>
                  <div class="sub">Lv.${m.level} • HP ${m.hp}/${m.maxHp}</div>
                  <div class="sub">Friendship ${m.friendship} • Energy ${m.energy}/${m.maxEnergy}</div>
                  ${allTypesHtml(m.types)}
                </div>
              `).join("")}
            </div>
          </div>

          <div class="card">
            <h3>🎯 Pokémon đang chọn</h3>
            ${active ? `
              <div style="display:flex; gap:14px; align-items:center; flex-wrap:wrap">
                <img src="${active.sprite}" alt="${active.name}" style="width:120px; height:120px; object-fit:contain">
                <div>
                  <div style="font-size:22px; font-weight:900">${cap(active.name)}</div>
                  <div class="sub">${active.abilities.map(cap).join(", ")}</div>
                  <div class="sub">Lv.${active.level} • EXP ${active.exp}</div>
                  <div class="sub">HP ${active.hp}/${active.maxHp} • Energy ${active.energy}/${active.maxEnergy}</div>
                  <div class="sub">ATK ${active.attack} • DEF ${active.defense} • SPD ${active.speed}</div>
                  <div class="sub">Friendship ${active.friendship}</div>
                  ${allTypesHtml(active.types)}
                </div>
              </div>

              <div class="inline-actions">
                <button class="small-btn" onclick="useItemOnActive('potion')" ${state.bag.potion<=0 ? "disabled":""}>🧪 Potion (${state.bag.potion})</button>
                <button class="small-btn" onclick="useItemOnActive('superPotion')" ${state.bag.superPotion<=0 ? "disabled":""}>💊 Super Potion (${state.bag.superPotion})</button>
                <button class="small-btn" onclick="useItemOnActive('rareCandy')" ${state.bag.rareCandy<=0 ? "disabled":""}>🍬 Rare Candy (${state.bag.rareCandy})</button>
                <button class="small-btn" onclick="useItemOnActive('friendshipCharm')" ${state.bag.friendshipCharm<=0 ? "disabled":""}>💖 Friendship Charm (${state.bag.friendshipCharm})</button>
              </div>

              <div style="margin-top:12px">
                <b>🗡️ Bộ kỹ năng</b>
                <div class="team-grid" style="margin-top:10px">
                  ${active.moves.map(move=>`
                    <div class="detail-box">
                      <b>${move.name}</b>
                      <div class="sub">${cap(move.type)} • Power ${move.power} • Cost ${move.cost}</div>
                      <div class="sub">Hiệu ứng: ${cap(move.fx)}</div>
                    </div>
                  `).join("")}
                </div>
              </div>
            ` : `<div class="sub">Chưa có Pokémon.</div>`}
          </div>
        </div>
      `;
    }

    function renderDex(){
      const keyword = state.dexSearch || "";
      const filtered = state.dexIndex.filter(x => x.name.includes(keyword.toLowerCase())).slice(0, 251);

      $("tab-dex").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>📘 Từ điển Pokémon / Pokédex</h2>
            <div class="sub">Tìm kiếm Pokémon, xem mô tả, hệ, khả năng, sinh cảnh, màu sắc, tiến hoá.</div>
            <div class="search-row">
              <input id="dexSearchInput" value="${keyword}" placeholder="Tìm tên Pokémon..." oninput="dexSearch(this.value)">
              <button class="small-btn" onclick="loadDexDetail(${filtered[0]?.id || 1})">Mở Pokémon đầu tiên</button>
            </div>
            <div class="dex-list">
              ${filtered.map(mon=>`
                <div class="dex-item" onclick="loadDexDetail(${mon.id})">
                  <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${mon.id}.png" alt="${mon.name}">
                  <b>#${mon.id}</b>
                  <div>${cap(mon.name)}</div>
                  <div class="sub">${state.seen.has(mon.id) ? "Đã gặp" : "Chưa gặp"}</div>
                </div>
              `).join("")}
            </div>
          </div>

          <div class="card" id="dexDetail">
            <h3>Chọn 1 Pokémon để xem chi tiết</h3>
            <div class="sub">Bạn có thể tra cứu như một từ điển Pokémon thực thụ.</div>
          </div>
        </div>
      `;
      if(state.dexSelected && !state.dexDetailLoading) fillDexDetail(state.dexSelected);
    }

    async function loadDexDetail(id){
      state.dexDetailLoading = true;
      state.dexSelected = id;
      renderDex();
      try{
        const base = await getPokemonData(id);
        const species = await getSpecies(id);
        const evo = await getEvolutionInfo(id);
        fillDexDetail({
          base,
          species,
          evo
        });
      }catch(err){
        $("dexDetail").innerHTML = `<h3>Lỗi tải dữ liệu Pokémon</h3><div class="sub">Không thể lấy thông tin từ API.</div>`;
      }
      state.dexDetailLoading = false;
    }

    function fillDexDetail(data){
      if(!data) return;
      const base = data.base || data.base?.base;
      const species = data.species || data.species?.species || {};
      const evo = data.evo || [];
      $("dexDetail").innerHTML = `
        <h3>📖 ${cap(base.name)} #${base.id}</h3>
        <div style="display:flex; gap:14px; align-items:center; flex-wrap:wrap">
          <img src="${base.sprite}" alt="${base.name}" style="width:150px; height:150px; object-fit:contain">
          <div>
            <div class="sub">${species.genus || "-"}</div>
            <div class="sub">${species.flavor || "-"}</div>
            ${allTypesHtml(base.types)}
          </div>
        </div>

        <div class="detail-grid" style="margin-top:12px">
          <div class="detail-box"><b>Khả năng</b><div class="sub">${base.abilities.map(cap).join(", ")}</div></div>
          <div class="detail-box"><b>Habitat</b><div class="sub">${cap(species.habitat || "unknown")}</div></div>
          <div class="detail-box"><b>Height / Weight</b><div class="sub">${base.height/10} m • ${base.weight/10} kg</div></div>
          <div class="detail-box"><b>Màu / Dáng</b><div class="sub">${cap(species.color || "-")} • ${cap(species.shape || "-")}</div></div>
          <div class="detail-box"><b>Tăng trưởng</b><div class="sub">${cap(species.growthRate || "-")}</div></div>
          <div class="detail-box"><b>Độ hiếm</b><div class="sub">${species.isLegendary ? "Legendary" : species.isMythical ? "Mythical" : "Normal"}</div></div>
        </div>

        <div style="margin-top:12px">
          <b>Stats gốc</b>
          <div class="detail-grid" style="margin-top:10px">
            <div class="detail-box">HP: ${base.stats.hp}</div>
            <div class="detail-box">Attack: ${base.stats.attack}</div>
            <div class="detail-box">Defense: ${base.stats.defense}</div>
            <div class="detail-box">Speed: ${base.stats.speed}</div>
          </div>
        </div>

        <div style="margin-top:12px">
          <b>Chuỗi tiến hoá</b>
          <div class="team-grid" style="margin-top:10px">
            ${evo.length ? evo.map(x=>`
              <div class="detail-box">
                <b>${cap(x.from)}</b> ➜ <b>${cap(x.to)}</b>
                <div class="sub">${x.requirement}</div>
              </div>
            `).join("") : `<div class="detail-box">Không có dữ liệu tiến hoá.</div>`}
          </div>
        </div>
      `;
    }

    async function renderEvolution(){
      $("tab-evolution").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>🧬 Phòng tiến hoá</h2>
            <div class="sub">Hỗ trợ nhiều kiểu tiến hoá: lên cấp, dùng đá tiến hoá, tình bạn, trade item, và vài dạng đặc biệt.</div>
            <div class="evo-grid" id="evoList">
              ${state.collection.map((m, i)=>`
                <div class="mini-mon" onclick="selectEvolutionMon(${i})">
                  <img src="${m.sprite}" alt="${m.name}">
                  <b>${cap(m.name)}</b>
                  <div class="sub">Lv.${m.level} • Friendship ${m.friendship}</div>
                  ${allTypesHtml(m.types)}
                </div>
              `).join("")}
            </div>
          </div>

          <div class="card" id="evoDetail">
            <h3>Chọn Pokémon để xem khả năng tiến hoá</h3>
          </div>
        </div>
      `;

      if(typeof state.evoSelected === "number"){
        await selectEvolutionMon(state.evoSelected);
      }
    }

    async function getEvolutionInfo(idOrName){
      const species = await getSpecies(idOrName);
      if(!species.evolutionChainUrl) return [];
      if(state.evoCache.has(species.evolutionChainUrl)) return state.evoCache.get(species.evolutionChainUrl);
      const data = await fetchJSON(species.evolutionChainUrl);

      const edges = [];
      function walk(node){
        if(!node) return;
        node.evolves_to.forEach(next=>{
          const d = next.evolution_details?.[0] || {};
          edges.push({
            from: node.species.name,
            to: next.species.name,
            requirement: formatEvolutionRequirement(d),
            detail: d
          });
          walk(next);
        });
      }
      walk(data.chain);
      state.evoCache.set(species.evolutionChainUrl, edges);
      return edges;
    }

    function formatEvolutionRequirement(d){
      if(!d || !Object.keys(d).length) return "Special evolution";
      if(d.trigger?.name === "level-up"){
        const parts = [];
        if(d.min_level) parts.push(`Lv ${d.min_level}+`);
        if(d.min_happiness) parts.push(`Friendship ${d.min_happiness}+`);
        if(d.time_of_day) parts.push(`Time: ${d.time_of_day}`);
        if(d.known_move_type) parts.push(`Biết move hệ ${d.known_move_type.name}`);
        if(d.held_item) parts.push(`Cần cầm ${cap(d.held_item.name)}`);
        return parts.length ? `Level-up: ${parts.join(" • ")}` : "Level-up";
      }
      if(d.trigger?.name === "use-item"){
        return `Use item: ${cap(d.item?.name || "special item")}`;
      }
      if(d.trigger?.name === "trade"){
        return `Trade evolution${d.held_item ? " + " + cap(d.held_item.name) : ""}`;
      }
      return cap(d.trigger?.name || "special");
    }

    async function selectEvolutionMon(index){
      state.evoSelected = index;
      const mon = state.collection[index];
      $("evoDetail").innerHTML = `<h3>Đang tải dữ liệu tiến hoá...</h3>`;
      try{
        const edges = await getEvolutionInfo(mon.id);
        const nextEdges = edges.filter(x=>x.from === mon.name);
        $("evoDetail").innerHTML = `
          <h3>${cap(mon.name)} • Lv.${mon.level}</h3>
          <div style="display:flex; gap:14px; align-items:center; flex-wrap:wrap">
            <img src="${mon.sprite}" style="width:120px; height:120px; object-fit:contain">
            <div>
              <div class="sub">Friendship ${mon.friendship}</div>
              <div class="sub">HP ${mon.hp}/${mon.maxHp}</div>
              ${allTypesHtml(mon.types)}
            </div>
          </div>

          <div style="margin-top:12px">
            <b>Các hướng tiến hoá hiện có</b>
            <div class="team-grid" style="margin-top:10px">
              ${nextEdges.length ? nextEdges.map((e, i)=>`
                <div class="detail-box">
                  <b>${cap(e.from)}</b> ➜ <b>${cap(e.to)}</b>
                  <div class="sub">${e.requirement}</div>
                  <button class="small-btn" style="margin-top:10px" onclick="evolveSelected(${index}, '${e.to}', ${i})">Tiến hoá</button>
                </div>
              `).join("") : `<div class="detail-box">Pokémon này hiện không có tiến hoá tiếp theo hoặc đã ở dạng cuối.</div>`}
            </div>
          </div>

          <div style="margin-top:12px">
            <b>Vật phẩm tiến hoá hiện có</b>
            <div class="sub" style="margin-top:6px">
              ${Object.keys(state.bag).filter(k=>["fireStone","waterStone","thunderStone","leafStone","moonStone","sunStone","linkCable","evoShard"].includes(k))
                .map(k=>`${itemCatalog[k].emoji} ${itemCatalog[k].name}: ${state.bag[k]}`).join(" • ")}
            </div>
          </div>
        `;
      }catch(err){
        $("evoDetail").innerHTML = `<h3>Lỗi tải tiến hoá</h3><div class="sub">Không lấy được evolution chain.</div>`;
      }
    }

    function canEvolve(mon, detail){
      if(!detail || !detail.trigger) return { ok: state.bag.evoShard > 0, consume:"evoShard", reason:"Cần Evolution Shard" };

      const trigger = detail.trigger.name;

      if(trigger === "level-up"){
        if(detail.min_level && mon.level < detail.min_level) return { ok:false, reason:`Cần Lv ${detail.min_level}` };
        if(detail.min_happiness && mon.friendship < detail.min_happiness) return { ok:false, reason:`Cần Friendship ${detail.min_happiness}` };
        return { ok:true, consume:null, reason:"Đủ điều kiện level-up" };
      }

      if(trigger === "use-item"){
        const itemKey = mapEvolutionItem(detail.item?.name);
        if(!itemKey) return { ok:false, reason:"Chưa hỗ trợ item này" };
        if(state.bag[itemKey] <= 0) return { ok:false, reason:`Thiếu ${itemCatalog[itemKey].name}` };
        return { ok:true, consume:itemKey, reason:`Dùng ${itemCatalog[itemKey].name}` };
      }

      if(trigger === "trade"){
        if(state.bag.linkCable <= 0) return { ok:false, reason:"Thiếu Link Cable" };
        return { ok:true, consume:"linkCable", reason:"Dùng Link Cable" };
      }

      if(state.bag.evoShard > 0) return { ok:true, consume:"evoShard", reason:"Dùng Evolution Shard" };
      return { ok:false, reason:"Thiếu Evolution Shard" };
    }

    function mapEvolutionItem(apiName){
      const map = {
        "fire-stone":"fireStone",
        "water-stone":"waterStone",
        "thunder-stone":"thunderStone",
        "leaf-stone":"leafStone",
        "moon-stone":"moonStone",
        "sun-stone":"sunStone"
      };
      return map[apiName] || null;
    }

    async function evolveSelected(index, targetName, edgeIndex){
      const mon = state.collection[index];
      const edges = await getEvolutionInfo(mon.id);
      const nextEdges = edges.filter(x=>x.from === mon.name);
      const edge = nextEdges[edgeIndex];
      if(!edge){
        toast("Không tìm thấy dữ liệu tiến hoá.");
        return;
      }
      const check = canEvolve(mon, edge.detail);
      if(!check.ok){
        toast(check.reason);
        return;
      }
      try{
        if(check.consume) state.bag[check.consume]--;
        const base = await getPokemonData(targetName);
        const oldName = mon.name;
        updateOwnedFromBase(mon, base);
        mon.friendship += 10;
        mon.hp = mon.maxHp;
        mon.energy = clamp(mon.energy + 30, 0, mon.maxEnergy);
        log("journey", `${cap(oldName)} đã tiến hoá thành ${cap(mon.name)}!`);
        log("explore", `${cap(oldName)} tiến hoá thành ${cap(mon.name)}.`);
        toast(`🎉 ${cap(oldName)} ➜ ${cap(mon.name)}`);
        renderCurrentTab();
      }catch(err){
        toast("Tiến hoá thất bại.");
      }
    }

    function renderJourney(){
      $("tab-journey").innerHTML = `
        <div class="grid-2">
          <div class="card">
            <h2>🏆 Hành trình & Huy hiệu</h2>
            <div class="sub">Mỗi khu vực sẽ có 1 huy hiệu. Thắng đủ trận trong khu vực sẽ nhận huy hiệu và mở khu mới.</div>
            ${renderZoneStrip()}

            <div style="margin-top:14px">
              <b>🎖️ Huy hiệu đã nhận</b>
              <div class="badge-list" style="margin-top:10px">
                ${zones.map((z, i)=>`
                  <div class="badge">${i < state.badges ? "✅" : "⬜"} ${z.badge}</div>
                `).join("")}
              </div>
            </div>

            <div style="margin-top:14px">
              <b>📈 Tiến độ khu vực</b>
              <div class="team-grid" style="margin-top:10px">
                ${zones.map((z, i)=>`
                  <div class="detail-box">
                    <b>${z.name}</b>
                    <div class="sub">Trận thắng: ${state.zoneWins[i]}</div>
                    <div class="sub">Mở khoá cần: ${z.unlock} huy hiệu</div>
                    <div class="sub">Phần thưởng: ${z.badge}</div>
                  </div>
                `).join("")}
              </div>
            </div>
          </div>

          <div class="card">
            <h3>📝 Nhật ký hành trình</h3>
            <div class="log">${state.logs.journey.map(x=>`<div>${x}</div>`).join("")}</div>
          </div>
        </div>
      `;
    }

    function renderShop(){
      $("tab-shop").innerHTML = `
        <div class="card">
          <h2>🛒 Cửa hàng</h2>
          <div class="sub">Mua bóng, bình hồi máu, kẹo tăng cấp và vật phẩm tiến hoá.</div>
          <div class="shop-grid" style="margin-top:12px">
            ${Object.entries(itemCatalog).map(([key, item])=>`
              <div class="shop-item">
                <div style="font-size:24px">${item.emoji}</div>
                <b>${item.name}</b>
                <div class="sub">${item.desc}</div>
                <div class="sub">Giá: ${item.price} coins</div>
                <div class="sub">Đang có: ${state.bag[key] || 0}</div>
                <button class="small-btn" style="margin-top:10px" onclick="buyItem('${key}')">Mua</button>
              </div>
            `).join("")}
          </div>
        </div>
      `;
    }

    function setActive(index){
      if(state.collection[index].hp <= 0){
        toast("Pokémon này đã kiệt sức, hãy hồi máu trước.");
        return;
      }
      state.activeIndex = index;
      log("explore", `${cap(state.collection[index].name)} được chọn làm Pokémon dẫn đội.`);
      renderCurrentTab();
    }

    function selectZone(id){
      if(state.badges < zones[id].unlock){
        toast("Chưa đủ huy hiệu để vào khu vực này.");
        return;
      }
      state.zone = id;
      bodyTheme();
      log("journey", `Đã chuyển đến ${zones[id].name}.`);
      renderCurrentTab();
    }

    function useItemOnActive(itemKey){
      const mon = getActive();
      if(!mon) return;
      if((state.bag[itemKey] || 0) <= 0){
        toast("Bạn không có item này.");
        return;
      }

      if(itemKey === "potion"){
        mon.hp = clamp(mon.hp + 35, 0, mon.maxHp);
      } else if(itemKey === "superPotion"){
        mon.hp = clamp(mon.hp + 70, 0, mon.maxHp);
      } else if(itemKey === "rareCandy"){
        mon.levelUpBonus = true;
        mon.exp += mon.level * 28;
        state.bag[itemKey]--;
        applyLevelUps(mon);
        log("journey", `${cap(mon.name)} dùng Rare Candy và lên cấp.`);
        renderCurrentTab();
        return;
      } else if(itemKey === "friendshipCharm"){
        mon.friendship = clamp(mon.friendship + 40, 0, 255);
      } else {
        toast("Item này dùng ở tab tiến hoá.");
        return;
      }

      state.bag[itemKey]--;
      toast(`Dùng ${itemCatalog[itemKey].name} cho ${cap(mon.name)}.`);
      renderCurrentTab();
    }

    function buyItem(itemKey){
      const item = itemCatalog[itemKey];
      if(state.coins < item.price){
        toast("Không đủ coins.");
        return;
      }
      state.coins -= item.price;
      state.bag[itemKey] = (state.bag[itemKey] || 0) + 1;
      toast(`Đã mua ${item.name}.`);
      renderCurrentTab();
    }

    function restAll(){
      state.collection.forEach(m=>{
        m.hp = m.maxHp;
        m.energy = Math.max(m.energy, 45);
        m.friendship = clamp(m.friendship + 4, 0, 255);
      });
      log("explore", "Toàn đội nghỉ ngơi: hồi HP, hồi năng lượng và tăng tình bạn.");
      renderCurrentTab();
    }

    function trainAll(){
      state.collection.forEach(m=>{
        m.exp += 10;
        m.energy = clamp(m.energy + 12, 0, m.maxEnergy);
      });
      state.coins = Math.max(0, state.coins - 20);
      state.collection.forEach(m=>applyLevelUps(m));
      log("journey", "Toàn đội luyện tập: tăng EXP, tăng năng lượng, tốn 20 coins.");
      renderCurrentTab();
    }

    async function explore(mode){
      if(mode === "camp"){
        restAll();
        if(Math.random() < 0.4){
          const reward = pick(["potion","pokeBall","friendshipCharm"]);
          state.bag[reward] = (state.bag[reward] || 0) + 1;
          log("explore", `Khi dựng trại, bạn tìm được ${itemCatalog[reward].name}.`);
        }
        openTab("explore");
        return;
      }

      const zone = zones[state.zone];
      const id = await pickEncounterId(mode, zone);
      try{
        const level = rand(5 + state.zone * 6, 10 + state.zone * 8);
        state.enemy = await createOwnedPokemon(id, level);
        state.enemy.friendship = 0;
        state.enemy.energy = rand(20, 55);
        state.seen.add(state.enemy.id);

        let eventText = `${cap(state.enemy.name)} xuất hiện!`;
        if(mode === "rare") eventText = `Bạn theo dấu hiếm và gặp ${cap(state.enemy.name)} cực kỳ mạnh!`;
        if(mode === "water") eventText = `Bên nguồn nước, ${cap(state.enemy.name)} xuất hiện!`;
        if(mode === "ruins") eventText = `Trong phế tích cổ, ${cap(state.enemy.name)} hiện ra!`;

        if(Math.random() < 0.22){
          const found = pick(["coins","item"]);
          if(found === "coins"){
            const extra = rand(25, 80);
            state.coins += extra;
            log("explore", `Bạn nhặt được ${extra} coins khi khám phá.`);
          }else{
            const reward = pick(["pokeBall","greatBall","potion","rareCandy"]);
            state.bag[reward] = (state.bag[reward] || 0) + 1;
            log("explore", `Bạn nhặt được ${itemCatalog[reward].name} trên đường.`);
          }
        }

        log("explore", eventText);
        log("battle", eventText);
        openTab("battle");
      }catch(err){
        toast("Không thể tạo encounter từ API.");
      }
    }

    async function pickEncounterId(mode, zone){
      let pool = [];
      for(let i=zone.min; i<=zone.max; i++) pool.push(i);

      if(mode === "rare"){
        pool = [...pool, ...actionPools.rare.filter(x=>x>=zone.min && x<=zone.max), ...actionPools.rare];
      }else if(mode === "water"){
        pool = [...pool, ...actionPools.water];
      }else if(mode === "ruins"){
        pool = [...pool, ...actionPools.ruins];
      }else if(zone.theme === "forest"){
        pool = [...pool, ...actionPools.forest];
      }else if(zone.theme === "cave"){
        pool = [...pool, ...actionPools.cave];
      }else if(zone.theme === "volcano"){
        pool = [...pool, ...actionPools.volcanic];
      }else if(zone.theme === "sky"){
        pool = [...pool, ...actionPools.sky];
      }

      pool = pool.filter(x=>x>=1 && x<=MAX_POKEMON);
      return pick(pool);
    }

    function damage(attacker, defender, move){
      const stab = attacker.types.includes(move.type) ? 1.18 : 1;
      const crit = Math.random() < 0.12 ? 1.65 : 1;
      const variance = Math.random() * 0.22 + 0.90;
      const raw = move.power + attacker.attack * 0.44 - defender.defense * 0.18;
      const dmg = Math.max(4, Math.round(raw * stab * crit * variance));
      defender.hp = Math.max(0, defender.hp - dmg);
      attacker.energy = clamp(attacker.energy + 10, 0, attacker.maxEnergy);
      return { dmg, crit: crit > 1 };
    }

    async function useMove(index){
      const player = getActive();
      const enemy = state.enemy;
      if(!player || !enemy || state.battleBusy) return;

      const move = player.moves[index];
      if(player.energy < move.cost){
        toast("Chưa đủ năng lượng.");
        return;
      }

      state.battleBusy = true;
      player.energy -= move.cost;
      renderBattle();

      animateMove(move, true);
      animateSprite("player", "attack");
      await wait(430);

      const result = damage(player, enemy, move);
      log("battle", `${cap(player.name)} dùng ${move.name}, gây ${result.dmg} sát thương${result.crit ? " chí mạng" : ""}!`);
      animateSprite("enemy", "hit");

      if(enemy.hp <= 0){
        await wait(340);
        await onWinBattle();
        state.battleBusy = false;
        renderCurrentTab();
        return;
      }

      await wait(460);
      await enemyTurn();
      state.battleBusy = false;
      renderCurrentTab();
    }

    async function enemyTurn(){
      const player = getActive();
      const enemy = state.enemy;
      if(!player || !enemy) return;

      const usable = enemy.moves.filter(m=>enemy.energy >= m.cost);
      if(!usable.length){
        enemy.energy = clamp(enemy.energy + 32, 0, enemy.maxEnergy);
        log("battle", `${cap(enemy.name)} tập trung để tích năng lượng.`);
        return;
      }

      const move = pick(usable);
      enemy.energy -= move.cost;
      renderBattle();

      animateMove(move, false);
      animateSprite("enemy", "attack");
      await wait(430);

      const result = damage(enemy, player, move);
      log("battle", `${cap(enemy.name)} dùng ${move.name}, gây ${result.dmg} sát thương${result.crit ? " chí mạng" : ""}!`);
      animateSprite("player", "hit");

      if(player.hp <= 0){
        player.hp = 0;
        log("battle", `${cap(player.name)} đã kiệt sức!`);
        const next = state.collection.findIndex(m=>m.hp > 0);
        if(next >= 0){
          state.activeIndex = next;
          log("battle", `${cap(state.collection[next].name)} được đổi vào sân.`);
        }else{
          log("journey", "Cả đội đã kiệt sức. Tự động nghỉ ngơi ở trại.");
          restAll();
          openTab("explore");
        }
      }
    }

    function chargeEnergy(){
      const player = getActive();
      if(!player || state.battleBusy) return;
      player.energy = clamp(player.energy + 34, 0, player.maxEnergy);
      log("battle", `${cap(player.name)} tích thêm 34 năng lượng.`);
      renderBattle();
      enemyTurn().then(renderCurrentTab);
    }

    async function throwBall(ballType){
      const enemy = state.enemy;
      const player = getActive();
      if(!enemy || !player || state.battleBusy) return;
      if((state.bag[ballType] || 0) <= 0){
        toast("Hết bóng rồi.");
        return;
      }
      state.bag[ballType]--;

      const hpFactor = 1 - enemy.hp / enemy.maxHp;
      const baseChance = ballType === "greatBall" ? 0.32 : 0.20;
      const chance = clamp(baseChance + hpFactor * 0.55 + state.badges * 0.03, 0.12, 0.92);

      if(Math.random() < chance){
        enemy.hp = Math.max(1, Math.round(enemy.maxHp * 0.65));
        enemy.energy = 35;
        enemy.friendship = 35;
        state.collection.push(enemy);
        state.captureCount++;
        state.coins += rand(30, 70);
        log("battle", `Bạn đã bắt được ${cap(enemy.name)}!`);
        log("journey", `Pokédex mở rộng: ${cap(enemy.name)} gia nhập đội.`);
        maybeAwardBadge();
        state.enemy = null;
        openTab("team");
      }else{
        log("battle", `${cap(enemy.name)} thoát khỏi bóng!`);
        await enemyTurn();
        renderCurrentTab();
      }
    }

    function applyLevelUps(mon){
      let leveled = false;
      while(mon.exp >= mon.level * 25){
        mon.exp -= mon.level * 25;
        mon.level++;
        mon.friendship = clamp(mon.friendship + 3, 0, 255);
        const baseStats = {
          hp: Math.round(mon.maxHp / (1 + (mon.level-1)*0.05)),
          attack:mon.attack,
          defense:mon.defense,
          speed:mon.speed
        };
        const baseLike = {
          id:mon.id,
          name:mon.name,
          sprite:mon.sprite,
          shiny:mon.shiny,
          types:mon.types,
          abilities:mon.abilities,
          stats:{
            hp: Math.max(35, baseStats.hp - mon.level),
            attack: Math.max(35, mon.attack - mon.level),
            defense: Math.max(35, mon.defense - mon.level),
            speed: Math.max(30, mon.speed - mon.level)
          }
        };
        const newStats = computeStats(baseLike, mon.level);
        mon.maxHp = newStats.maxHp;
        mon.attack = newStats.attack;
        mon.defense = newStats.defense;
        mon.speed = newStats.speed;
        mon.maxEnergy = Math.min(140, 100 + Math.floor(mon.level / 5) * 4);
        mon.hp = mon.maxHp;
        mon.energy = mon.maxEnergy;
        mon.moves = chooseMoves(mon.types, mon.level);
        leveled = true;
      }
      if(leveled){
        log("journey", `${cap(mon.name)} lên cấp ${mon.level}!`);
      }
    }

    async function onWinBattle(){
      const player = getActive();
      const enemy = state.enemy;
      if(!player || !enemy) return;

      const expGain = 20 + enemy.level * 4;
      const coinGain = rand(25, 80);
      player.exp += expGain;
      player.friendship = clamp(player.friendship + 5, 0, 255);
      state.coins += coinGain;
      if(Math.random() < 0.28) state.bag.pokeBall++;
      if(Math.random() < 0.12) state.bag.rareCandy++;

      log("battle", `${cap(enemy.name)} bị đánh bại!`);
      log("journey", `${cap(player.name)} nhận ${expGain} EXP và ${coinGain} coins.`);
      state.zoneWins[state.zone]++;

      applyLevelUps(player);
      maybeAwardBadge();

      state.enemy = null;
      toast("Chiến thắng!");
    }

    function maybeAwardBadge(){
      const needWins = 3 + state.zone * 2;
      if(state.badges === state.zone && state.zoneWins[state.zone] >= needWins){
        state.badges++;
        state.coins += 220 + state.zone * 80;
        state.bag.greatBall += 2;
        log("journey", `Bạn nhận được ${zones[state.zone].badge}! Mở khóa khu vực mới.`);
        toast(`🏅 Nhận ${zones[state.zone].badge}`);
      }
    }

    function animateSprite(which, cls){
      const id = which === "player" ? "playerSprite" : "enemySprite";
      const el = $(id);
      if(!el) return;
      el.classList.add(cls);
      setTimeout(()=>el.classList.remove(cls), 420);
    }

    function animateMove(move, fromPlayer){
      const layer = $("fxLayer");
      if(!layer) return;
      layer.innerHTML = "";

      const presets = {
        fire:{ count:8, color1:"#fff7ed", color2:"#fb923c", size:[16,34], shape:"circle" },
        water:{ count:9, color1:"#e0f2fe", color2:"#38bdf8", size:[12,28], shape:"drop" },
        grass:{ count:10, color1:"#dcfce7", color2:"#22c55e", size:[10,24], shape:"leaf" },
        electric:{ count:7, color1:"#fef9c3", color2:"#fde047", size:[18,34], shape:"bolt" },
        psychic:{ count:6, color1:"#f5d0fe", color2:"#c084fc", size:[22,38], shape:"ring" },
        ice:{ count:8, color1:"#ecfeff", color2:"#67e8f9", size:[14,28], shape:"star" },
        rock:{ count:8, color1:"#e7e5e4", color2:"#a8a29e", size:[12,28], shape:"rock" },
        ground:{ count:9, color1:"#fef3c7", color2:"#d97706", size:[12,30], shape:"dust" },
        ghost:{ count:7, color1:"#ddd6fe", color2:"#818cf8", size:[20,34], shape:"mist" },
        dark:{ count:7, color1:"#94a3b8", color2:"#111827", size:[20,36], shape:"shadow" },
        dragon:{ count:8, color1:"#dbeafe", color2:"#2563eb", size:[20,36], shape:"meteor" },
        fighting:{ count:7, color1:"#fee2e2", color2:"#ef4444", size:[18,34], shape:"shock" },
        poison:{ count:9, color1:"#f3e8ff", color2:"#a855f7", size:[14,28], shape:"bubble" },
        bug:{ count:10, color1:"#ecfccb", color2:"#84cc16", size:[12,26], shape:"leaf" },
        flying:{ count:9, color1:"#e0f2fe", color2:"#93c5fd", size:[12,28], shape:"feather" },
        fairy:{ count:10, color1:"#fce7f3", color2:"#f472b6", size:[12,26], shape:"sparkle" },
        steel:{ count:8, color1:"#f8fafc", color2:"#94a3b8", size:[12,28], shape:"metal" },
        normal:{ count:7, color1:"#f8fafc", color2:"#cbd5e1", size:[12,26], shape:"circle" }
      };

      const p = presets[move.fx] || presets.normal;
      const startX = fromPlayer ? 160 : window.innerWidth > 720 ? 680 : 240;
      const startY = fromPlayer ? 220 : 140;
      const dxBase = fromPlayer ? 360 : -360;
      const dyBase = fromPlayer ? -90 : 90;

      for(let i=0;i<p.count;i++){
        const shot = document.createElement("div");
        const size = rand(p.size[0], p.size[1]);
        const isRing = p.shape === "ring" || (Math.random() < 0.12 && ["psychic","fairy","ghost"].includes(move.fx));

        shot.className = isRing ? "fx-ring" : "fx-shot";
        if(!isRing){
          shot.style.width = size + "px";
          shot.style.height = size + "px";
          applyShapeStyle(shot, p, size);
        }else{
          shot.style.width = size + 30 + "px";
          shot.style.height = size + 30 + "px";
          shot.style.borderColor = p.color2;
        }

        const sx = startX + rand(-15, 20);
        const sy = startY + rand(-25, 30);
        shot.style.left = sx + "px";
        shot.style.top = sy + "px";
        shot.style.setProperty("--dx", (dxBase + rand(-40, 40)) + "px");
        shot.style.setProperty("--dy", (dyBase + rand(-80, 80)) + "px");
        shot.style.animationDelay = (i * 0.02) + "s";
        layer.appendChild(shot);
      }

      const burst = document.createElement("div");
      burst.className = "fx-burst";
      burst.style.width = "110px";
      burst.style.height = "110px";
      burst.style.left = fromPlayer ? "64%" : "18%";
      burst.style.top = fromPlayer ? "34%" : "54%";
      burst.style.background = `radial-gradient(circle, ${p.color1}, ${p.color2}, transparent 72%)`;
      layer.appendChild(burst);

      setTimeout(()=>layer.innerHTML = "", 820);
    }

    function applyShapeStyle(el, preset, size){
      const c1 = preset.color1;
      const c2 = preset.color2;
      if(["circle","bubble","shadow"].includes(preset.shape)){
        el.style.borderRadius = "50%";
        el.style.background = `radial-gradient(circle, ${c1}, ${c2})`;
      } else if(preset.shape === "drop"){
        el.style.borderRadius = "50% 50% 50% 0";
        el.style.transform = "rotate(45deg)";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
      } else if(preset.shape === "leaf" || preset.shape === "feather"){
        el.style.width = size + 8 + "px";
        el.style.height = Math.max(10, size - 4) + "px";
        el.style.borderRadius = "100% 0 100% 0";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
      } else if(preset.shape === "bolt"){
        el.style.width = size + 18 + "px";
        el.style.height = size + 18 + "px";
        el.style.clipPath = "polygon(40% 0, 72% 0, 56% 34%, 86% 34%, 30% 100%, 44% 52%, 18% 52%)";
        el.style.background = c2;
      } else if(preset.shape === "star" || preset.shape === "sparkle"){
        el.style.width = size + 14 + "px";
        el.style.height = size + 14 + "px";
        el.style.clipPath = "polygon(50% 0, 61% 37%, 100% 50%, 61% 63%, 50% 100%, 39% 63%, 0 50%, 39% 37%)";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
      } else if(["rock","dust","metal","meteor","shock"].includes(preset.shape)){
        el.style.borderRadius = "18%";
        el.style.background = `linear-gradient(135deg, ${c1}, ${c2})`;
        if(preset.shape === "meteor" || preset.shape === "shock"){
          el.style.boxShadow = `0 0 12px ${c2}`;
        }
      } else if(preset.shape === "mist"){
        el.style.borderRadius = "50%";
        el.style.background = `radial-gradient(circle, ${c2}, transparent 70%)`;
      } else {
        el.style.borderRadius = "50%";
        el.style.background = `radial-gradient(circle, ${c1}, ${c2})`;
      }
    }

    function dexSearch(value){
      state.dexSearch = value;
      renderDex();
    }

    function wait(ms){ return new Promise(r=>setTimeout(r, ms)); }

    async function initGame(){
      renderTabs();
      renderTopStats();
      bodyTheme();

      await getDexIndex();

      const starterIds = [1, 4, 7, 25, 133, 152];
      const levels = [6, 6, 6, 7, 6, 6];
      for(let i=0;i<starterIds.length;i++){
        const mon = await createOwnedPokemon(starterIds[i], levels[i]);
        state.collection.push(mon);
        state.seen.add(mon.id);
      }
      state.activeIndex = 0;

      log("journey", "Giáo sư trao cho bạn 6 Pokémon khởi đầu để hành trình thêm phong phú.");
      log("explore", "Bạn có thể khám phá theo nhiều cách khác nhau, không còn đơn điệu.");
      renderCurrentTab();
      await explore("wander");
    }

    initGame();

    window.openTab = openTab;
    window.selectZone = selectZone;
    window.explore = explore;
    window.setActive = setActive;
    window.useMove = useMove;
    window.chargeEnergy = chargeEnergy;
    window.throwBall = throwBall;
    window.restAll = restAll;
    window.trainAll = trainAll;
    window.useItemOnActive = useItemOnActive;
    window.buyItem = buyItem;
    window.dexSearch = dexSearch;
    window.loadDexDetail = loadDexDetail;
    window.selectEvolutionMon = selectEvolutionMon;
    window.evolveSelected = evolveSelected;
  </script>
</body>
</html>const pool={water:[54,60,72,73,79,80,86,87,90,98,99,116,117,118,119,120,121,129,130,131,138,139,140,141,170,171,183,186,194,195,211,222,223,224,226,230],ruin:[63,64,65,92,93,94,95,96,97,102,103,104,105,122,124,144,150,200,201,202,203,205,208,213,228,229,235,237],rare:[25,26,59,65,68,94,130,131,143,149,150,151,154,157,160,181,196,197,212,214,230,243,244,245,248,249,250,251]};
const moveSets={normal:[['Quick Strike',18,0],['Hyper Rush',45,25],['Omega Dash',65,45]],fire:[['Ember Burst',20,0],['Flame Wheel',34,14],['Inferno Nova',70,50]],water:[['Bubble Jet',18,0],['Aqua Slash',34,14],['Ocean Crash',68,48]],grass:[['Leaf Cutter',18,0],['Vine Lash',32,12],['Emerald Storm',66,46]],electric:[['Spark Bolt',20,0],['Volt Dash',36,15],['Heaven Thunder',72,52]],psychic:[['Mind Tap',18,0],['Psy Cut',34,14],['Astral Collapse',68,48]],ice:[['Ice Shard',18,0],['Snow Burst',34,14],['Absolute Zero',68,50]],rock:[['Stone Toss',20,0],['Meteor Slam',38,16],['Mountain Ruin',70,50]],ground:[['Mud Shot',19,0],['Quake Roar',38,16],['Earth Rift',70,50]],ghost:[['Spirit Touch',19,0],['Haunt Wave',38,16],['Phantom Gate',70,50]],dark:[['Shadow Bite',20,0],['Night Claw',38,16],['Eclipse Doom',72,52]],dragon:[['Dragon Spark',24,0],['Scale Break',42,18],['Draco Meteor',78,58]],fighting:[['Power Jab',21,0],['Aura Smash',40,17],['Titan Breaker',72,52]],poison:[['Toxic Sting',18,0],['Venom Wave',36,15],['Plague Bloom',68,48]],bug:[['Bug Bite',18,0],['Swarm Dance',34,14],['Queen Swarm',66,46]],flying:[['Gust Blade',18,0],['Storm Dive',36,15],['Hurricane Halo',68,48]],fairy:[['Fairy Tap',18,0],['Moon Spark',36,15],['Miracle Waltz',68,48]],steel:[['Iron Tap',19,0],['Chrome Cannon',39,17],['Titanium Storm',70,50]]};
let S={tab:'explore',zone:0,badges:0,wins:[0,0,0,0,0],coins:600,caught:0,bag:{pokeBall:14,greatBall:5,potion:6,superPotion:2,rareCandy:2,fireStone:1,waterStone:1,thunderStone:1,leafStone:1,moonStone:1,sunStone:1,linkCable:1,friendshipCharm:2,evoShard:1},team:[],active:0,enemy:null,seen:new Set(),dex:[],cache:new Map(),species:new Map(),evoCache:new Map(),logs:{explore:['• Chào mừng đến bản cập nhật lớn có nhiều tab.'],battle:['• Hệ chiến đấu năng lượng đã sẵn sàng.'],journey:['• Hành trình mới bắt đầu.']},busy:false,search:'',dexDetail:null,evoSel:null};
const $=id=>document.getElementById(id),cap=s=>s?String(s).replaceAll('-',' ').split(' ').map(w=>w?w[0].toUpperCase()+w.slice(1):'').join(' '):'',rand=(a,b)=>Math.floor(Math.random()*(b-a+1))+a,pick=a=>a[Math.floor(Math.random()*a.length)],clamp=(v,a,b)=>Math.max(a,Math.min(b,v));
function toast(m){let t=$('toast');t.textContent=m;t.style.display='block';clearTimeout(t.tm);t.tm=setTimeout(()=>t.style.display='none',1700)}function log(k,m){S.logs[k].unshift('• '+m);S.logs[k]=S.logs[k].slice(0,80);render()}
const fallbackNames=['bulbasaur','charmander','squirtle','pikachu','jigglypuff','meowth','psyduck','growlithe','abra','machop','bellsprout','geodude','gastly','onix','krabby','cubone','staryu','magikarp','eevee','snorlax','dratini','chikorita','cyndaquil','totodile','mareep','marill','sudowoodo','espeon','umbreon','lugia','ho-oh','celebi'];
function fallbackPoke(id){id=Number(id)||1;let name=fallbackNames[(id-1)%fallbackNames.length]||('pokemon '+id),types=['normal'];if([4,5,6,58,59,155,156,157].includes(id))types=['fire'];else if([7,8,9,54,55,129,130,158,159,160].includes(id))types=['water'];else if([1,2,3,152,153,154].includes(id))types=['grass'];else if([25,26,179,180,181].includes(id))types=['electric'];else if([63,64,65,150,196].includes(id))types=['psychic'];else if([92,93,94,200].includes(id))types=['ghost'];else if([133,143].includes(id))types=['normal'];return{id,name,types,abilities:['offline-power'],stats:{hp:45+id%45,atk:45+id%55,def:40+id%50,spd:35+id%60},sprite:`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/${id}.png`}}
async function getJson(u){let r=await fetch(u);if(!r.ok)throw Error('net');return r.json()}
async function poke(id){let k=String(id).toLowerCase();if(S.cache.has(k))return S.cache.get(k);try{let p=await getJson(`${API}/pokemon/${k}`),o={id:p.id,name:p.name,types:p.types.map(x=>x.type.name),abilities:p.abilities.map(x=>x.ability.name),stats:{hp:p.stats[0].base_stat,atk:p.stats[1].base_stat,def:p.stats[2].base_stat,spd:p.stats[5].base_stat},sprite:(p.sprites.other&&p.sprites.other['official-artwork']&&p.sprites.other['official-artwork'].front_default)||p.sprites.front_default};S.cache.set(k,o);S.cache.set(String(o.id),o);return o}catch(err){let o=fallbackPoke(id);S.cache.set(k,o);S.cache.set(String(o.id),o);return o}}
async function species(id){let k=String(id).toLowerCase();if(S.species.has(k))return S.species.get(k);try{let p=await getJson(`${API}/pokemon-species/${k}`),fl=(p.flavor_text_entries.find(x=>x.language.name==='en')||{}).flavor_text||'Chưa có mô tả.';fl=fl.split(String.fromCharCode(10)).join(' ').split(String.fromCharCode(12)).join(' ');let o={id:p.id,name:p.name,chain:p.evolution_chain&&p.evolution_chain.url,from:p.evolves_from_species&&p.evolves_from_species.name,flavor:fl,genus:(p.genera.find(x=>x.language.name==='en')||{}).genus||'-',habitat:(p.habitat&&p.habitat.name)||'unknown',color:(p.color&&p.color.name)||'-',legend:p.is_legendary,myth:p.is_mythical,capture:p.capture_rate};S.species.set(k,o);S.species.set(String(o.id),o);return o}catch(err){let b=await poke(id);let o={id:b.id,name:b.name,chain:null,from:null,flavor:'Dữ liệu offline: Pokemon này được lưu trong bộ dữ liệu dự phòng để game vẫn chạy khi mạng bị chặn.',genus:'Offline Pokemon',habitat:'unknown',color:'unknown',legend:false,myth:false,capture:80};S.species.set(k,o);S.species.set(String(o.id),o);return o}}
function stats(b,l){return{maxHp:Math.round(b.stats.hp+l*5.2),atk:Math.round(b.stats.atk+l*2.1),def:Math.round(b.stats.def+l*1.7),spd:Math.round(b.stats.spd+l*1.5)}}function moves(types,l){let t=types[0]||'normal',t2=types[1]||'normal',a=[...(moveSets[t]||moveSets.normal),...(moveSets[t2]||[]),...moveSets.normal],out=[];while(out.length<4){let m=pick(a);if(!out.some(x=>x.name===m[0]))out.push({name:m[0],power:m[1],cost:m[2],type:moveSets[t]?.includes(m)?t:(moveSets[t2]?.includes(m)?t2:'normal')})}return out}
async function makeMon(id,l){let b=await poke(id),st=stats(b,l);return{uid:Date.now()+Math.random(),id:b.id,name:b.name,types:b.types,abilities:b.abilities,sprite:b.sprite,level:l,exp:0,friend:60,hp:st.maxHp,maxHp:st.maxHp,atk:st.atk,def:st.def,spd:st.spd,energy:35,maxEnergy:100,moves:moves(b.types,l)}}function active(){return S.team[S.active]}function typeHtml(t){return `<div class="types">${t.map(x=>`<span class="type">${cap(x)}</span>`).join('')}</div>`}
function renderBase(){document.body.className=zones[S.zone].c;$('stats').innerHTML=`<div class="pill">🏅 Huy hiệu ${S.badges}/5</div><div class="pill">🪙 Coins ${S.coins}</div><div class="pill">🎯 Đã bắt ${S.caught}</div><div class="pill">⚪ ${S.bag.pokeBall}</div><div class="pill">🔵 ${S.bag.greatBall}</div><div class="pill">📍 ${zones[S.zone].n}</div>`;$('tabs').innerHTML=tabs.map(t=>`<button class="tab ${S.tab===t[0]?'active':''}" onclick="openTab('${t[0]}')">${t[1]}</button>`).join('');document.querySelectorAll('.pane').forEach(p=>p.classList.remove('active'));$(S.tab).classList.add('active')}
function zonesHtml(){return `<div class="zonegrid">${zones.map((z,i)=>`<div class="zone ${S.zone===i?'active':''} ${S.badges<z.u?'lock':''}" onclick="selectZone(${i})"><b>${i+1}. ${z.n}</b><div class="sub">${z.d}</div><div class="sub">Cần ${z.u} huy hiệu • ${z.b}</div></div>`).join('')}</div>`}
function render(){renderBase();if(S.tab==='explore')renderExplore();if(S.tab==='battle')renderBattle();if(S.tab==='team')renderTeam();if(S.tab==='dex')renderDex();if(S.tab==='evo')renderEvo();if(S.tab==='journey')renderJourney();if(S.tab==='shop')renderShop()}function openTab(t){S.tab=t;render()}function selectZone(i){if(S.badges<zones[i].u)return toast('Chưa đủ huy hiệu!');S.zone=i;log('journey','Đã đến '+zones[i].n);render()}
function renderExplore(){let a=active();$('explore').innerHTML=`<div class="card"><h2>🌍 Khám phá đã làm lại</h2><div class="sub">Chọn kiểu khám phá khác nhau để gặp sự kiện, Pokemon và phần thưởng khác nhau.</div>${zonesHtml()}</div><div class="grid2" style="margin-top:14px"><div class="card"><h3>✨ Cách khám phá</h3><div class="exploregrid">${modes.map(m=>`<div class="explore" onclick="explore('${m[0]}')"><div class="ico">${m[1]}</div><b>${m[2]}</b><div class="sub">${m[3]}</div></div>`).join('')}</div><div class="actions"><button class="green" onclick="restAll()">⛺ Nghỉ toàn đội</button><button class="blue" onclick="trainAll()">💪 Luyện tập</button><button class="purple" onclick="openTab('battle')">⚔️ Sang chiến đấu</button></div></div><div class="card"><h3>🧭 Nhật ký</h3>${a?`<div class="box"><b>${cap(a.name)} đang dẫn đội</b><div style="display:flex;gap:12px;align-items:center;margin-top:8px"><img src="${a.sprite}" style="width:88px;height:88px;object-fit:contain"><div><div>Lv.${a.level} • HP ${a.hp}/${a.maxHp}</div><div class="sub">Energy ${a.energy}/${a.maxEnergy} • Friend ${a.friend}</div>${typeHtml(a.types)}</div></div></div>`:''}<div class="log" style="margin-top:10px">${S.logs.explore.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`}
function scene(){let a=active(),e=S.enemy,z=zones[S.zone];return `<div class="scene ${z.c}" id="scene"><div class="shadow l"></div><div class="shadow r"></div>${a?`<img id="pSprite" class="poke p" src="${a.sprite}">`:''}${e?`<img id="eSprite" class="poke e" src="${e.sprite}">`:''}</div>`}
function renderBattle(){let a=active(),e=S.enemy;$('battle').innerHTML=`<div class="grid2"><div class="card"><h2>⚔️ Chiến đấu năng lượng</h2><div class="sub">Mỗi chiêu tạo hiệu ứng theo hệ riêng: lửa, nước, cỏ, điện, ma, rồng, đá, băng...</div>${scene()}${a&&e?`<div class="hud"><div class="box"><b>${cap(a.name)} Lv.${a.level}</b><div class="bar"><span class="hp" style="width:${a.hp/a.maxHp*100}%"></span></div><small>HP ${a.hp}/${a.maxHp}</small><div class="bar"><span class="en" style="width:${a.energy/a.maxEnergy*100}%"></span></div><small>Energy ${a.energy}/${a.maxEnergy}</small></div><div class="box"><b>Wild ${cap(e.name)} Lv.${e.level}</b><div class="bar"><span class="hp" style="width:${e.hp/e.maxHp*100}%"></span></div><small>HP ${e.hp}/${e.maxHp}</small><div class="bar"><span class="en" style="width:${e.energy/e.maxEnergy*100}%"></span></div><small>Energy ${e.energy}/${e.maxEnergy}</small></div></div><div class="moves">${a.moves.map((m,i)=>`<button class="move" onclick="useMove(${i})" ${S.busy||a.energy<m.cost?'disabled':''}>${m.name}<small>${cap(m.type)} • Power ${m.power} • NL ${m.cost}</small></button>`).join('')}</div><div class="actions"><button class="blue" onclick="charge()">⚡ Tích năng lượng</button><button class="green" onclick="ball('pokeBall')">⚪ Poke Ball</button><button class="purple" onclick="ball('greatBall')">🔵 Great Ball</button><button class="red" onclick="explore('wander')">➡️ Đối thủ khác</button></div>`:`<div class="actions"><button onclick="explore('wander')">🔎 Tìm Pokemon hoang dã</button></div>`}</div><div class="card"><h3>📜 Battle Log</h3><div class="log">${S.logs.battle.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`}
function renderTeam(){let a=active();$('team').innerHTML=`<div class="grid2"><div class="card"><h2>📦 Đội hình</h2><div class="sub">Chọn Pokemon dẫn đội, dùng vật phẩm, xem chỉ số và bộ chiêu.</div><div class="teamgrid">${S.team.map((m,i)=>`<div class="mon ${i===S.active?'active':''}" onclick="setActive(${i})"><img src="${m.sprite}"><b>${cap(m.name)}</b><div class="sub">Lv.${m.level} • HP ${m.hp}/${m.maxHp}</div><div class="sub">Friend ${m.friend} • EN ${m.energy}</div>${typeHtml(m.types)}</div>`).join('')}</div></div><div class="card"><h3>🎯 Chi tiết</h3>${a?`<div style="display:flex;gap:12px;align-items:center;flex-wrap:wrap"><img src="${a.sprite}" style="width:130px;height:130px;object-fit:contain"><div><h2>${cap(a.name)}</h2><div class="sub">Ability: ${a.abilities.map(cap).join(', ')}</div><div>ATK ${a.atk} • DEF ${a.def} • SPD ${a.spd}</div><div>EXP ${a.exp} • Friendship ${a.friend}</div>${typeHtml(a.types)}</div></div><div class="actions"><button onclick="useItem('potion')">🧪 Potion (${S.bag.potion})</button><button onclick="useItem('superPotion')">💊 Super (${S.bag.superPotion})</button><button onclick="useItem('rareCandy')">🍬 Candy (${S.bag.rareCandy})</button><button onclick="useItem('friendshipCharm')">💖 Charm (${S.bag.friendshipCharm})</button></div><h3 style="margin-top:14px">Chiêu thức</h3><div class="teamgrid">${a.moves.map(m=>`<div class="box"><b>${m.name}</b><div class="sub">${cap(m.type)} • Power ${m.power} • NL ${m.cost}</div></div>`).join('')}</div>`:''}</div></div>`}
function renderDex(){let f=S.dex.filter(x=>x.name.includes(S.search.toLowerCase())).slice(0,251);$('dex').innerHTML=`<div class="grid2"><div class="card"><h2>📘 Từ điển Pokemon</h2><div class="search"><input placeholder="Tìm Pokemon..." value="${S.search}" oninput="S.search=this.value;renderDex()"><button onclick="loadDex(${f[0]?.id||1})">Mở Pokemon đầu</button></div><div class="dexlist">${f.map(x=>`<div class="dexitem" onclick="loadDex(${x.id})"><img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${x.id}.png"><b>#${x.id}</b><div>${cap(x.name)}</div><div class="sub">${S.seen.has(x.id)?'Đã gặp':'Chưa gặp'}</div></div>`).join('')}</div></div><div class="card" id="dexDetail">${S.dexDetail||'<h3>Chọn Pokemon để xem từ điển</h3><div class="sub">Có mô tả, hệ, chỉ số, habitat, độ hiếm và chuỗi tiến hoá.</div>'}</div></div>`}
async function loadDex(id){$('dexDetail').innerHTML='<h3>Đang tải...</h3>';let b=await poke(id),sp=await species(id),ev=await evoInfo(id);S.dexDetail=`<h2>📖 ${cap(b.name)} #${b.id}</h2><div style="display:flex;gap:14px;align-items:center;flex-wrap:wrap"><img src="${b.sprite}" style="width:155px;height:155px;object-fit:contain"><div><b>${sp.genus}</b><div class="sub">${sp.flavor}</div>${typeHtml(b.types)}</div></div><div class="grid2" style="margin-top:12px"><div class="box"><b>Stats</b><div>HP ${b.stats.hp} • ATK ${b.stats.atk} • DEF ${b.stats.def} • SPD ${b.stats.spd}</div></div><div class="box"><b>Sinh thái</b><div>${cap(sp.habitat)} • ${cap(sp.color)} • ${sp.legend?'Legendary':sp.myth?'Mythical':'Normal'}</div></div></div><h3 style="margin-top:12px">Chuỗi tiến hoá</h3><div class="teamgrid">${ev.length?ev.map(e=>`<div class="box"><b>${cap(e.from)} ➜ ${cap(e.to)}</b><div class="sub">${e.req}</div></div>`).join(''):'<div class="box">Không có tiến hoá.</div>'}</div>`;renderDex()}
async function evoInfo(id){let sp=await species(id);if(!sp.chain)return offlineEvo(id);if(S.evoCache.has(sp.chain))return S.evoCache.get(sp.chain);try{let d=await getJson(sp.chain),arr=[];function walk(n){n.evolves_to.forEach(to=>{let x=(to.evolution_details&&to.evolution_details[0])||{};arr.push({from:n.species.name,to:to.species.name,detail:x,req:req(x)});walk(to)})}walk(d.chain);S.evoCache.set(sp.chain,arr);return arr}catch(err){return offlineEvo(id)}}
function offlineEvo(id){const map={1:[['bulbasaur','ivysaur',16],['ivysaur','venusaur',32]],4:[['charmander','charmeleon',16],['charmeleon','charizard',36]],7:[['squirtle','wartortle',16],['wartortle','blastoise',36]],25:[['pikachu','raichu',20]],133:[['eevee','vaporeon',20],['eevee','jolteon',20],['eevee','flareon',20]],152:[['chikorita','bayleef',16],['bayleef','meganium',32]],155:[['cyndaquil','quilava',14],['quilava','typhlosion',36]],158:[['totodile','croconaw',18],['croconaw','feraligatr',30]]};let arr=[];Object.values(map).flat().forEach(x=>arr.push({from:x[0],to:x[1],detail:{trigger:{name:'level-up'},min_level:x[2]},req:'Level-up Lv '+x[2]}));return arr}function req(x){if(!x.trigger)return'Special';if(x.trigger.name==='level-up')return`Level-up ${x.min_level?'Lv '+x.min_level:''} ${x.min_happiness?'Friend '+x.min_happiness:''}`;if(x.trigger.name==='use-item')return`Dùng ${cap(x.item?.name||'item')}`;if(x.trigger.name==='trade')return'Trade hoặc Link Cable';return cap(x.trigger.name)}
function renderEvo(){let m=S.team[S.evoSel??S.active];$('evo').innerHTML=`<div class="grid2"><div class="card"><h2>🧬 Tiến hoá nhiều loại</h2><div class="sub">Hỗ trợ level-up, đá tiến hoá, friendship, trade/link cable và Evolution Shard.</div><div class="teamgrid">${S.team.map((x,i)=>`<div class="mon ${i===S.evoSel?'active':''}" onclick="selEvo(${i})"><img src="${x.sprite}"><b>${cap(x.name)}</b><div class="sub">Lv.${x.level} • Friend ${x.friend}</div>${typeHtml(x.types)}</div>`).join('')}</div></div><div class="card" id="evoDetail"><h3>Chọn Pokemon để xem tiến hoá</h3></div></div>`;if(m)selEvo(S.evoSel??S.active,false)}
async function selEvo(i,rer=true){S.evoSel=i;let m=S.team[i],ev=(await evoInfo(m.id)).filter(e=>e.from===m.name);let d=$('evoDetail');if(!d)return;d.innerHTML=`<h2>${cap(m.name)} Lv.${m.level}</h2><img src="${m.sprite}" style="width:130px;height:130px;object-fit:contain"><div class="sub">Friendship ${m.friend}</div>${typeHtml(m.types)}<h3 style="margin-top:12px">Có thể tiến hoá</h3><div class="teamgrid">${ev.length?ev.map((e,k)=>`<div class="box"><b>${cap(e.from)} ➜ ${cap(e.to)}</b><div class="sub">${e.req}</div><button onclick="evolve(${i},${k})">Tiến hoá</button></div>`).join(''):'<div class="box">Không còn dạng tiến hoá tiếp theo.</div>'}</div><h3 style="margin-top:12px">Vật phẩm</h3><div class="sub">🔥${S.bag.fireStone} 💧${S.bag.waterStone} ⚡${S.bag.thunderStone} 🍃${S.bag.leafStone} 🌙${S.bag.moonStone} ☀️${S.bag.sunStone} 🔗${S.bag.linkCable} 💠${S.bag.evoShard}</div>`;if(rer)renderBase()}
async function evolve(i,k){let m=S.team[i],ev=(await evoInfo(m.id)).filter(e=>e.from===m.name),e=ev[k];if(!e)return;let c=canEvo(m,e.detail);if(!c.ok)return toast(c.msg);if(c.item)S.bag[c.item]--;let old=m.name,b=await poke(e.to),st=stats(b,m.level);Object.assign(m,{id:b.id,name:b.name,types:b.types,abilities:b.abilities,sprite:b.sprite,maxHp:st.maxHp,atk:st.atk,def:st.def,spd:st.spd,hp:st.maxHp,energy:100,moves:moves(b.types,m.level),friend:m.friend+12});log('journey',`${cap(old)} tiến hoá thành ${cap(m.name)}!`);toast('Tiến hoá thành '+cap(m.name));render()}
function canEvo(m,d){if(!d?.trigger)return S.bag.evoShard>0?{ok:true,item:'evoShard'}:{ok:false,msg:'Cần Evolution Shard'};if(d.trigger.name==='level-up'){if(d.min_level&&m.level<d.min_level)return{ok:false,msg:'Cần Lv '+d.min_level};if(d.min_happiness&&m.friend<d.min_happiness)return{ok:false,msg:'Cần friendship '+d.min_happiness};return{ok:true}}if(d.trigger.name==='trade')return S.bag.linkCable>0?{ok:true,item:'linkCable'}:{ok:false,msg:'Cần Link Cable'};if(d.trigger.name==='use-item'){let map={'fire-stone':'fireStone','water-stone':'waterStone','thunder-stone':'thunderStone','leaf-stone':'leafStone','moon-stone':'moonStone','sun-stone':'sunStone'},it=map[d.item?.name];return it&&S.bag[it]>0?{ok:true,item:it}:{ok:false,msg:'Thiếu item tiến hoá'}}return S.bag.evoShard>0?{ok:true,item:'evoShard'}:{ok:false,msg:'Cần Evolution Shard'}}
function renderJourney(){$('journey').innerHTML=`<div class="grid2"><div class="card"><h2>🏆 Hành trình</h2>${zonesHtml()}<h3 style="margin-top:14px">Huy hiệu</h3><div class="teamgrid">${zones.map((z,i)=>`<div class="box"><b>${i<S.badges?'✅':'⬜'} ${z.b}</b><div class="sub">Thắng: ${S.wins[i]} • Cần: ${3+i*2}</div></div>`).join('')}</div></div><div class="card"><h3>Nhật ký hành trình</h3><div class="log">${S.logs.journey.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`}
function renderShop(){$('shop').innerHTML=`<div class="card"><h2>🛒 Cửa hàng</h2><div class="sub">Mua bóng, hồi máu, kẹo tăng cấp và vật phẩm tiến hoá.</div><div class="shopgrid" style="margin-top:12px">${Object.entries(bagItems).map(([k,v])=>`<div class="item"><div style="font-size:28px">${v[0]}</div><b>${v[1]}</b><div class="sub">${v[3]}</div><div>Giá: ${v[2]} coins</div><div>Đang có: ${S.bag[k]||0}</div><button style="margin-top:9px" onclick="buy('${k}')">Mua</button></div>`).join('')}</div></div>`}
async function explore(mode='wander'){if(mode==='camp'){restAll();let r=pick(['potion','pokeBall','friendshipCharm']);S.bag[r]++;log('explore','Dựng trại và nhặt được '+bagItems[r][1]);return}let z=zones[S.zone],ids=[];for(let i=z.min;i<=z.max;i++)ids.push(i);if(pool[mode])ids=[...ids,...pool[mode]];if(mode==='rare')ids=[...ids,...pool.rare,...pool.rare];ids=ids.filter(x=>x>=1&&x<=MAX);let id=pick(ids),lvl=rand(5+S.zone*6,11+S.zone*8);S.enemy=await makeMon(id,lvl);S.enemy.energy=rand(20,55);S.seen.add(S.enemy.id);if(Math.random()<.25){let r=pick(['coins','item']);if(r==='coins'){let c=rand(30,90);S.coins+=c;log('explore','Bạn nhặt được '+c+' coins.')}else{let it=pick(['pokeBall','greatBall','potion','rareCandy']);S.bag[it]++;log('explore','Bạn tìm thấy '+bagItems[it][1]+'.')}}log('explore',`Bạn gặp ${cap(S.enemy.name)} ở ${z.n}!`);log('battle',`Wild ${cap(S.enemy.name)} xuất hiện!`);S.tab='battle';render()}
function dmg(a,d,m){let crit=Math.random()<.12?1.65:1,stab=a.types.includes(m.type)?1.18:1,raw=m.power+a.atk*.44-d.def*.18,damage=Math.max(4,Math.round(raw*crit*stab*(.9+Math.random()*.22)));d.hp=Math.max(0,d.hp-damage);a.energy=clamp(a.energy+10,0,a.maxEnergy);return{damage,crit:crit>1}}
async function useMove(i){let a=active(),e=S.enemy,m=a.moves[i];if(S.busy||!e||a.energy<m.cost)return;S.busy=true;a.energy-=m.cost;renderBattle();fx(m.type,true);anim('pSprite','atk');await wait(480);let r=dmg(a,e,m);anim('eSprite','hit');log('battle',`${cap(a.name)} dùng ${m.name}, gây ${r.damage} sát thương${r.crit?' chí mạng':''}.`);if(e.hp<=0){win();S.busy=false;render();return}await wait(500);await enemyTurn();S.busy=false;render()}
async function enemyTurn(){let a=active(),e=S.enemy;if(!e)return;let ok=e.moves.filter(m=>e.energy>=m.cost);if(!ok.length){e.energy=clamp(e.energy+30,0,e.maxEnergy);log('battle',`${cap(e.name)} tích năng lượng.`);return}let m=pick(ok);e.energy-=m.cost;renderBattle();fx(m.type,false);await wait(430);let r=dmg(e,a,m);anim('pSprite','hit');log('battle',`${cap(e.name)} dùng ${m.name}, gây ${r.damage} sát thương.`);if(a.hp<=0){a.hp=0;let n=S.team.findIndex(x=>x.hp>0);if(n>=0){S.active=n;log('battle',`${cap(S.team[n].name)} vào sân.`)}else{restAll();log('journey','Cả đội kiệt sức, tự động nghỉ trại.')}}}
function charge(){let a=active();a.energy=clamp(a.energy+35,0,a.maxEnergy);log('battle',`${cap(a.name)} tích +35 năng lượng.`);enemyTurn().then(render)}async function ball(k){if(!S.enemy||S.bag[k]<=0)return toast('Không đủ bóng');S.bag[k]--;let e=S.enemy,ch=(k==='greatBall'?.32:.2)+(1-e.hp/e.maxHp)*.55+S.badges*.03;if(Math.random()<ch){e.hp=Math.max(1,Math.round(e.maxHp*.65));e.friend=35;S.team.push(e);S.caught++;S.coins+=rand(40,90);log('battle','Bắt được '+cap(e.name)+'!');log('journey',cap(e.name)+' gia nhập đội.');S.enemy=null;badge();S.tab='team';render()}else{log('battle',cap(e.name)+' thoát khỏi bóng!');await enemyTurn();render()}}
function win(){let a=active(),e=S.enemy,ex=20+e.level*4,c=rand(35,85);a.exp+=ex;a.friend=clamp(a.friend+5,0,255);S.coins+=c;S.wins[S.zone]++;log('battle',`${cap(e.name)} bị đánh bại! Nhận ${ex} EXP và ${c} coins.`);level(a);badge();S.enemy=null;toast('Chiến thắng!')}function level(m){while(m.exp>=m.level*25){m.exp-=m.level*25;m.level++;m.maxHp+=rand(8,14);m.atk+=rand(3,6);m.def+=rand(2,5);m.spd+=rand(2,5);m.hp=m.maxHp;m.maxEnergy=Math.min(150,m.maxEnergy+5);m.energy=m.maxEnergy;m.moves=moves(m.types,m.level);log('journey',cap(m.name)+' lên Lv.'+m.level+'!')}}function badge(){let need=3+S.zone*2;if(S.badges===S.zone&&S.wins[S.zone]>=need){S.badges++;S.coins+=250;S.bag.greatBall+=2;log('journey','Nhận '+zones[S.zone].b+' và mở khu vực mới!');toast('Nhận '+zones[S.zone].b)}}
function restAll(){S.team.forEach(m=>{m.hp=m.maxHp;m.energy=Math.max(m.energy,50);m.friend=clamp(m.friend+4,0,255)});log('explore','Toàn đội hồi HP, năng lượng và tăng tình bạn.');render()}function trainAll(){S.team.forEach(m=>{m.exp+=12;m.energy=clamp(m.energy+15,0,m.maxEnergy);level(m)});S.coins=Math.max(0,S.coins-20);log('journey','Toàn đội luyện tập, tốn 20 coins.');render()}function setActive(i){if(S.team[i].hp<=0)return toast('Pokemon này kiệt sức.');S.active=i;render()}function useItem(k){let m=active();if(S.bag[k]<=0)return toast('Không có item');if(k==='potion')m.hp=clamp(m.hp+35,0,m.maxHp);else if(k==='superPotion')m.hp=clamp(m.hp+75,0,m.maxHp);else if(k==='rareCandy'){m.exp+=m.level*30;level(m)}else if(k==='friendshipCharm')m.friend=clamp(m.friend+40,0,255);else return toast('Item này dùng ở tab Tiến hoá');S.bag[k]--;render()}function buy(k){let it=bagItems[k];if(S.coins<it[2])return toast('Không đủ coins');S.coins-=it[2];S.bag[k]=(S.bag[k]||0)+1;toast('Đã mua '+it[1]);renderShop();renderBase()}
function anim(id,c){let el=$(id);if(!el)return;el.classList.add(c);setTimeout(()=>el.classList.remove(c),430)}function fx(type,from){let sc=$('scene');if(!sc)return;let map={fire:['#fff7ed','#fb923c','circle'],water:['#e0f2fe','#38bdf8','drop'],grass:['#dcfce7','#22c55e','leaf'],electric:['#fef9c3','#fde047','bolt'],psychic:['#f5d0fe','#c084fc','ring'],ice:['#ecfeff','#67e8f9','star'],rock:['#e7e5e4','#a8a29e','rock'],ground:['#fef3c7','#d97706','rock'],ghost:['#ddd6fe','#818cf8','mist'],dark:['#94a3b8','#111827','mist'],dragon:['#dbeafe','#2563eb','star'],fighting:['#fee2e2','#ef4444','rock'],poison:['#f3e8ff','#a855f7','circle'],bug:['#ecfccb','#84cc16','leaf'],flying:['#e0f2fe','#93c5fd','drop'],fairy:['#fce7f3','#f472b6','star'],steel:['#f8fafc','#94a3b8','rock'],normal:['#fff','#cbd5e1','circle']},p=map[type]||map.normal;for(let i=0;i<10;i++){let e=document.createElement('div'),sz=rand(14,34);e.className='fx';e.style.width=sz+'px';e.style.height=sz+'px';e.style.left=(from?160:700)+rand(-20,20)+'px';e.style.top=(from?220:135)+rand(-30,30)+'px';e.style.setProperty('--dx',(from?rand(280,420):rand(-420,-280))+'px');e.style.setProperty('--dy',rand(-100,100)+'px');shape(e,p);sc.appendChild(e);setTimeout(()=>e.remove(),800)}let b=document.createElement('div');b.className='burst';b.style.left=from?'65%':'18%';b.style.top=from?'35%':'54%';b.style.width='110px';b.style.height='110px';b.style.background=`radial-gradient(circle,${p[0]},${p[1]},transparent 70%)`;sc.appendChild(b);setTimeout(()=>b.remove(),750)}function shape(e,p){e.style.background=`linear-gradient(135deg,${p[0]},${p[1]})`;if(p[2]==='bolt')e.style.clipPath='polygon(40% 0,72% 0,56% 34%,86% 34%,30% 100%,44% 52%,18% 52%)';else if(p[2]==='leaf')e.style.borderRadius='100% 0 100% 0';else if(p[2]==='drop')e.style.borderRadius='50% 50% 50% 0';else if(p[2]==='star')e.style.clipPath='polygon(50% 0,61% 37%,100% 50%,61% 63%,50% 100%,39% 63%,0 50%,39% 37%)';else e.style.borderRadius='50%'}function wait(ms){return new Promise(r=>setTimeout(r,ms))}
async function init(){S.dex=Array.from({length:MAX},(_,i)=>({id:i+1,name:fallbackNames[i%fallbackNames.length]||('pokemon '+(i+1))}));render();try{let d=await getJson(`${API}/pokemon?limit=${MAX}`);S.dex=d.results.map((x,i)=>({id:i+1,name:x.name}))}catch(err){log('explore','Không tải được PokéAPI, game chuyển sang dữ liệu offline dự phòng.')}for(let pair of [[1,6],[4,6],[7,6],[25,7],[133,6],[152,6]]){let m=await makeMon(pair[0],pair[1]);S.team.push(m);S.seen.add(m.id)}render();try{await explore('wander')}catch(err){log('explore','Đã sẵn sàng chơi ở chế độ offline. Hãy bấm một kiểu khám phá.')}}init();
window.openTab=openTab;window.selectZone=selectZone;window.explore=explore;window.restAll=restAll;window.trainAll=trainAll;window.useMove=useMove;window.charge=charge;window.ball=ball;window.setActive=setActive;window.useItem=useItem;window.buy=buy;window.loadDex=loadDex;window.selEvo=selEvo;window.evolve=evolve;window.S=S;
</script>
</body>
</html>
