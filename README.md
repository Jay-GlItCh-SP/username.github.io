# username.github.io

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Play & Watch — Games and Movies (Legal)</title>
  <style>
    :root{
      --bg:#0f1724; --card:#0b1220; --muted:#94a3b8; --accent:#7c3aed;
      --glass: rgba(255,255,255,0.03);
    }
    *{box-sizing:border-box}
    body{
      margin:0;font-family:Inter,system-ui,-apple-system,Segoe UI,Roboto,"Helvetica Neue",Arial;
      background:linear-gradient(180deg,var(--bg),#071024);color:#e6eef8;
      -webkit-font-smoothing:antialiased; -moz-osx-font-smoothing:grayscale;
    }
    header{
      display:flex;align-items:center;justify-content:space-between;padding:18px 24px;
      border-bottom:1px solid rgba(255,255,255,0.03);backdrop-filter: blur(6px);
    }
    .brand{display:flex;gap:12px;align-items:center}
    .logo{width:44px;height:44px;border-radius:8px;background:linear-gradient(135deg,var(--accent),#4f46e5);display:flex;align-items:center;justify-content:center;font-weight:700}
    h1{font-size:18px;margin:0}
    .tag{color:var(--muted);font-size:13px}
    .search{max-width:540px;flex:1;margin:0 24px}
    input[type="search"]{
      width:100%;padding:10px 14px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);
      background:var(--glass);color:inherit;font-size:14px;
    }
    main{padding:18px 24px;display:grid;grid-template-columns: 1fr 340px;gap:18px}
    /* left column */
    .panel{background:linear-gradient(180deg, rgba(255,255,255,0.02), transparent);padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.03)}
    .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:12px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.01));padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.03);min-height:120px;display:flex;flex-direction:column;justify-content:space-between}
    .card h3{margin:0 0 6px 0;font-size:15px}
    .meta{color:var(--muted);font-size:13px}
    .actions{display:flex;gap:8px;flex-wrap:wrap}
    .btn{padding:8px 10px;border-radius:8px;border:none;background:rgba(255,255,255,0.03);color:inherit;cursor:pointer;font-size:13px}
    .btn.primary{background:linear-gradient(90deg,var(--accent),#4f46e5);box-shadow:0 6px 18px rgba(79,70,229,0.12)}
    .sidebar .panel{position:sticky;top:18px}
    .category-row{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:8px}
    .chip{background:rgba(255,255,255,0.02);padding:6px 10px;border-radius:999px;font-size:13px;border:1px solid rgba(255,255,255,0.02)}
    footer{padding:12px 24px;color:var(--muted);font-size:13px;text-align:center;border-top:1px solid rgba(255,255,255,0.03);margin-top:18px}
    /* modal */
    .modal-bg{position:fixed;inset:0;background:rgba(2,6,23,0.6);display:none;align-items:center;justify-content:center;padding:20px;z-index:40}
    .modal{width:min(1100px,98%);max-height:88vh;overflow:auto;background:#081428;border-radius:12px;padding:12px;border:1px solid rgba(255,255,255,0.04)}
    .modal .close{float:right;border:none;background:none;color:var(--muted);font-size:18px;cursor:pointer}
    .video-wrap iframe, .game-wrap iframe{width:100%;height:60vh;border:0;border-radius:8px}
    @media (max-width:980px){main{grid-template-columns:1fr;}.search{margin:0 12px}}
  </style>
</head>
<body>
  <header>
    <div class="brand">
      <div class="logo">PW</div>
      <div>
        <h1>Play & Watch</h1>
        <div class="tag">Curated, legal browser games & public videos — share with friends (but follow your school's rules!)</div>
      </div>
    </div>

    <div class="search">
      <input id="q" type="search" placeholder="Search games, movies, or shows (e.g., 'Geometry Dash')" />
    </div>

    <div style="display:flex;gap:8px">
      <button class="btn" onclick="location.reload()">Refresh</button>
      <button class="btn primary" onclick="openRequest()">Request Access / Suggest</button>
    </div>
  </header>

  <main>
    <section>
      <div class="panel">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
          <strong>Games</strong>
          <div class="meta">Click a tile to open in a new tab or embed if available</div>
        </div>

        <div class="category-row" id="game-cats">
          <div class="chip" data-cat="all">All</div>
          <div class="chip" data-cat="arcade">Arcade</div>
          <div class="chip" data-cat="racing">Racing</div>
          <div class="chip" data-cat="platformer">Platformer</div>
          <div class="chip" data-cat="puzzle">Puzzle</div>
        </div>

        <div class="grid" id="games">
          <!-- Cards inserted by JS -->
        </div>
      </div>

      <div class="panel" style="margin-top:12px">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
          <strong>Movies & Shows (Legal / Public)</strong>
          <div class="meta">YouTube embeds and public-domain films</div>
        </div>

        <div class="grid" id="movies">
          <!-- Movie cards -->
        </div>
      </div>
    </section>

    <aside class="sidebar">
      <div class="panel">
        <strong>Quick Links</strong>
        <div style="margin-top:8px" class="meta">
          • Newgrounds / Itch.io for indie embeds (when permitted)<br>
          • CrazyGames & Kongregate — many games allow embedding or direct link<br>
          • YouTube for legally-available episodes / creative commons uploads
        </div>
        <hr style="margin:12px 0;border-color:rgba(255,255,255,0.03)" />
        <div style="display:flex;flex-direction:column;gap:8px">
          <button class="btn" onclick="requestWhitelist()">How to request whitelist</button>
          <button class="btn" onclick="reportIssue()">Report broken link</button>
          <a class="btn" href="https://pages.github.com/" target="_blank">Host on GitHub Pages</a>
        </div>
      </div>
    </aside>
  </main>

  <footer>
    Built with ❤️ — play responsibly. I can't help you bypass monitoring systems. If you need access for educational reasons, ask an admin.
  </footer>

  <!-- Modal -->
  <div id="modalBg" class="modal-bg" role="dialog" aria-hidden="true">
    <div class="modal">
      <button class="close" onclick="closeModal()">✕</button>
      <div id="modalContent">
        <!-- content injected -->
      </div>
    </div>
  </div>

<script>
  // Data: feel free to expand. These are link-based; many game vendors disallow iframe embedding.
  const gamesData = [
    {id:'slope', title:'Slope', cat:'arcade', src:'https://slope-game.com/', desc:'Fast-paced rolling challenge.'},
    {id:'smashkarts', title:'Smash Karts', cat:'racing', src:'https://www.crazygames.com/game/smash-karts', desc:'Multiplayer kart mayhem.'},
    {id:'geometry', title:'Geometry Dash (Fan / Web versions)', cat:'platformer', src:'https://www.crazygames.com/game/geometry-dash', desc:'Rhythm-based platformer.'},
    {id:'2048', title:'2048', cat:'puzzle', src:'https://play2048.co/', desc:'Slide to combine numbers.'},
    {id:'retro-racer', title:'Retro Racing (example)', cat:'racing', src:'https://www.retrogames.cc/embed/xxx', desc:'Classic-style racer (embed may vary).'}
  ];

  const moviesData = [
    {id:'short-film', title:'Public Domain Film: Example', src:'https://www.youtube.com/embed/YE7VzlLtp-4', desc:'A public-domain short (placeholder)'},
    {id:'creative-commons', title:'Creative Commons Clip', src:'https://www.youtube.com/embed/aqz-KE-bpKQ', desc:'Sample CC-licensed documentary clip'}
  ];

  const gamesEl = document.getElementById('games');
  const moviesEl = document.getElementById('movies');
  const q = document.getElementById('q');

  function makeGameCard(g){
    const div = document.createElement('div'); div.className='card';
    const h = document.createElement('h3'); h.textContent = g.title;
    const m = document.createElement('div'); m.className='meta'; m.textContent = g.desc;
    const actions = document.createElement('div'); actions.className='actions';
    const openBtn = document.createElement('button'); openBtn.className='btn primary'; openBtn.textContent='Open';
    openBtn.onclick = ()=> window.open(g.src,'_blank');
    const embedBtn = document.createElement('button'); embedBtn.className='btn'; embedBtn.textContent='Embed (if allowed)';
    embedBtn.onclick = ()=> openEmbed(g);
    actions.appendChild(openBtn); actions.appendChild(embedBtn);
    div.appendChild(h); div.appendChild(m); div.appendChild(actions);
    return div;
  }

  function makeMovieCard(mv){
    const div = document.createElement('div'); div.className='card';
    const h = document.createElement('h3'); h.textContent = mv.title;
    const m = document.createElement('div'); m.className='meta'; m.textContent = mv.desc;
    const play = document.createElement('button'); play.className='btn primary'; play.textContent='Play';
    play.onclick = ()=> openEmbed(mv);
    div.appendChild(h); div.appendChild(m); div.appendChild(play);
    return div;
  }

  function render(){
    gamesEl.innerHTML=''; moviesEl.innerHTML='';
    for(const g of gamesData) gamesEl.appendChild(makeGameCard(g));
    for(const m of moviesData) moviesEl.appendChild(makeMovieCard(m));
  }

  function openEmbed(item){
    // Many sites prevent embedding. We try only for trusted sources (YouTube, known embed URLs).
    const modalBg = document.getElementById('modalBg');
    const content = document.getElementById('modalContent');
    let html = `<h2 style="margin-top:6px">${item.title}</h2><p class="meta">${item.desc}</p>`;
    if(item.src.includes('youtube.com') || item.src.includes('youtube-nocookie.com')){
      html += `<div class="video-wrap"><iframe src="${item.src}" allowfullscreen></iframe></div>`;
    } else if(item.src.startsWith('http')){
      html += `<div class="game-wrap"><iframe src="${item.src}" sandbox="allow-scripts allow-same-origin"></iframe></div>
               <p class="meta" style="margin-top:8px">If embedding fails, click "Open" to open the game in a new tab.</p>`;
    } else {
      html += `<p class="meta">Embed not available. <button class="btn primary" onclick="window.open('${item.src}','_blank')">Open</button></p>`;
    }
    content.innerHTML = html;
    modalBg.style.display='flex';
  }

  function closeModal(){ document.getElementById('modalBg').style.display='none'; }

  // Search
  q.addEventListener('input', ()=>{
    const term = q.value.trim().toLowerCase();
    document.querySelectorAll('#games .card').forEach(card=>{
      const txt = card.querySelector('h3').textContent.toLowerCase() + ' ' + card.querySelector('.meta').textContent.toLowerCase();
      card.style.display = (txt.includes(term) ? '' : 'none');
    });
    document.querySelectorAll('#movies .card').forEach(card=>{
      const txt = card.querySelector('h3').textContent.toLowerCase() + ' ' + card.querySelector('.meta').textContent.toLowerCase();
      card.style.display = (txt.includes(term) ? '' : 'none');
    });
  });

  // Category chips
  document.getElementById('game-cats').addEventListener('click', (e)=>{
    const chip = e.target.closest('.chip'); if(!chip) return;
    const cat = chip.dataset.cat;
    document.querySelectorAll('#games .card').forEach((card, i)=>{
      const item = gamesData[i]; // order corresponds
      card.style.display = (cat==='all' || item.cat===cat ? '' : 'none');
    });
  });

  // Buttons
  function openRequest(){
    const modalBg = document.getElementById('modalBg');
    const content = document.getElementById('modalContent');
    content.innerHTML = `<h2>Request Access / Suggest Content</h2>
      <p class="meta">If you need a specific game or show for educational reasons, ask your admin or teacher. Here's a template you can copy & paste:</p>
      <pre style="background:#07122a;padding:10px;border-radius:8px;color:#cfefff">
Hello [Admin/Teacher],

I'd like to request that the URL for [game or video name + link] be whitelisted for class use on [date(s)]. This is for [brief reason — e.g., "game-based learning activity in Computer Science"].

Thanks,
[Your Name]
      </pre>
      <p class="meta">Or send me the title and I can craft a one-line request for you.</p>`;
    modalBg.style.display='flex';
  }

  function requestWhitelist(){
    alert('Tip: Ask an admin politely. I can draft a request message for you — tell me the game and the purpose.');
  }

  function reportIssue(){ alert('Thanks — tell me the broken link and I will update the site.'); }

  // Initialize
  render();

  // Accessibility: close modal with ESC
  document.addEventListener('keydown', (e)=>{ if(e.key==='Escape') closeModal(); });

  // Note: this site intentionally does NOT include ways to bypass filters.
</script>
