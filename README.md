<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>NEXUS DIAMOND — by SOUM — Veille Stratégique OSINT</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:'Segoe UI',system-ui,'Helvetica Neue',sans-serif;scroll-behavior:smooth}
:root{--bg:#060810;--surface:#0c0f1c;--card:#121828;--card2:#181f38;--text:#eef2fa;--text2:#8898c8;--accent:#00e5ff;--accent2:#ff6b35;--accent3:#00ff88;--accent4:#aa66ff;--gold:#ffd700;--diamond:#b8e2ff;--border:#1e2a4a;--shadow:0 8px 32px rgba(0,0,0,.6);--radius:16px;--nav-bg:#080b16;--red:#ff0030;--green:#00ff88;--orange:#ff6b00;--purple:#aa66ff;--pink:#ff44aa;--yellow:#ffcc00;--glow:0 0 20px rgba(0,229,255,.15);--gradient:linear-gradient(135deg,#00e5ff,#aa66ff,#ff44aa)}
body{background:var(--bg);color:var(--text);transition:.3s;min-height:100vh;background-image:radial-gradient(ellipse at 20% 50%,rgba(0,229,255,.03) 0%,transparent 50%),radial-gradient(ellipse at 80% 50%,rgba(170,102,255,.03) 0%,transparent 50%)}
.theme-dark{--bg:#060810;--surface:#0c0f1c;--card:#121828;--card2:#181f38;--text:#eef2fa;--text2:#8898c8;--border:#1e2a4a}
.theme-clair{--bg:#f0f2f8;--surface:#e4e7f0;--card:#ffffff;--card2:#f4f6fc;--text:#1a1d2e;--text2:#5a6a8a;--border:#d0d6e4}
.theme-noir{--bg:#000000;--surface:#0a0a0a;--card:#111111;--card2:#1a1a1a;--text:#ffffff;--text2:#888888;--border:#222222}
.theme-bleu{--bg:#0a1628;--surface:#0f1f3a;--card:#142850;--card2:#1a3366;--text:#e0eeff;--text2:#7a9ec8;--border:#1e4a7a}
.theme-vert{--bg:#0a1a0a;--surface:#0f2a0f;--card:#143a14;--card2:#1a4a1a;--text:#e0ffe0;--text2:#7ac87a;--border:#1e4a1e}
.theme-rouge{--bg:#1a0a0a;--surface:#2a0f0f;--card:#3a1414;--card2:#4a1a1a;--text:#ffe0e0;--text2:#c87a7a;--border:#4a1e1e}
.theme-violet{--bg:#100a1a;--surface:#1a0f2a;--card:#24143a;--card2:#2e1a4a;--text:#eee0ff;--text2:#9a7ac8;--border:#3a1e5a}
.theme-or{--bg:#1a180a;--surface:#2a2610;--card:#3a3416;--card2:#4a421c;--text:#fffae0;--text2:#c8b87a;--border:#5a4e1e}
.logo-icon{width:42px;height:42px;background:var(--gradient);border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:1.2rem;font-weight:900;color:#fff;box-shadow:0 0 25px rgba(0,229,255,.4);animation:logoPulse 3s ease-in-out infinite;position:relative}
.logo-icon:hover{transform:rotateY(180deg) scale(1.1)}
.logo-icon::before{content:'⟡';position:absolute;font-size:.8rem;top:-6px;right:-6px;color:var(--gold);text-shadow:0 0 10px rgba(255,215,0,.6);animation:sparkle 2s ease-in-out infinite}
@keyframes logoPulse{0%,100%{box-shadow:0 0 25px rgba(0,229,255,.4)}50%{box-shadow:0 0 45px rgba(0,229,255,.7)}}
@keyframes sparkle{0%,100%{opacity:1;transform:rotate(0deg) scale(1)}50%{opacity:.4;transform:rotate(180deg) scale(1.3)}}
.sidebar{position:fixed;top:0;left:0;bottom:0;width:52px;background:rgba(8,11,22,.98);border-right:1px solid var(--border);z-index:999;display:flex;flex-direction:column;align-items:center;padding:6px 0;overflow-y:auto;overflow-x:hidden;scrollbar-width:none;backdrop-filter:blur(10px);transition:width .2s ease}
.sidebar::-webkit-scrollbar{display:none}
.sidebar:hover{width:195px}
.sidebar .logo-mini{display:flex;align-items:center;gap:6px;padding:4px 8px;margin-bottom:4px;width:100%;justify-content:center;flex-shrink:0}
.sidebar .logo-mini .logo-icon{width:26px;height:26px;border-radius:7px;font-size:12px;box-shadow:0 0 12px rgba(0,229,255,.15)}
.sidebar .logo-mini .logo-text{font-size:12px;font-weight:800;background:var(--gradient);-webkit-background-clip:text;-webkit-text-fill-color:transparent;white-space:nowrap;display:none}
.sidebar:hover .logo-mini .logo-text{display:block}
.sidebar .nav-item{display:flex;align-items:center;gap:6px;padding:5px 8px;border-radius:5px;font-size:9px;font-weight:500;color:var(--text2);text-decoration:none;cursor:pointer;white-space:nowrap;width:100%;transition:all .1s;margin:1px 0}
.sidebar .nav-item:hover,.sidebar .nav-item.active{color:var(--accent);background:var(--card)}
.sidebar .nav-item .nav-icon{font-size:13px;width:22px;text-align:center;flex-shrink:0}
.sidebar .nav-item .nav-label{display:none;font-size:8px}
.sidebar:hover .nav-item .nav-label{display:inline}
.top-bar{position:fixed;top:0;left:52px;right:0;height:42px;background:rgba(8,11,22,.95);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 10px;z-index:900;backdrop-filter:blur(10px)}
.top-bar .page-title{font-size:13px;font-weight:700;color:var(--text)}
.top-bar .page-sub{font-size:8px;color:var(--text2);margin-left:6px}
.top-bar .top-actions{display:flex;align-items:center;gap:3px;margin-left:auto;flex-shrink:0}
.top-bar .top-actions button{width:24px;height:24px;border-radius:5px;border:1px solid var(--border);background:var(--card);color:var(--text2);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:10px}
.top-bar .top-actions button:hover{border-color:var(--accent);color:var(--accent)}
.top-bar .user-badge{display:flex;align-items:center;gap:2px;padding:2px 5px;border-radius:4px;background:var(--card);border:1px solid var(--border);font-size:8px;color:var(--accent);cursor:pointer}
.top-bar .user-badge .dot{width:4px;height:4px;border-radius:50%;background:var(--green)}
.content{max-width:1440px;margin:42px 12px 0 64px;padding:10px 12px;width:auto}
.page{display:none;animation:fadeIn .15s ease}.page.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(3px)}to{opacity:1;transform:translateY(0)}}
.grid{display:grid;gap:6px}
.grid-2{grid-template-columns:repeat(auto-fit,minmax(250px,1fr))}
.grid-3{grid-template-columns:repeat(auto-fit,minmax(220px,1fr))}
.grid-4{grid-template-columns:repeat(auto-fit,minmax(180px,1fr))}
.grid-5{grid-template-columns:repeat(auto-fit,minmax(140px,1fr))}
.card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);padding:10px;transition:all .15s;position:relative;overflow:hidden}
.card::before{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:var(--gradient);opacity:0;transition:.3s}
.card:hover{transform:translateY(-4px);box-shadow:0 12px 48px rgba(0,0,0,.6);border-color:var(--accent)}
.card:hover::before{opacity:1}
.card-header{display:flex;justify-content:space-between;align-items:center;margin-bottom:6px}
.card-header h3{font-size:11px;font-weight:600}
.btn{padding:4px 10px;border-radius:5px;border:none;font-size:9px;font-weight:600;cursor:pointer;display:inline-flex;align-items:center;gap:3px;text-decoration:none;font-family:inherit}
.btn-primary{background:var(--gradient);color:#fff}
.btn-outline{background:transparent;border:1px solid var(--border);color:var(--text2)}
.btn-outline:hover{border-color:var(--accent);color:var(--accent)}
.btn-danger{background:#ef4444;color:#fff}
.btn-sm{padding:3px 6px;font-size:8px}
.btn-lg{padding:8px 16px;font-size:12px}
.input,.textarea,.select{padding:5px 8px;border-radius:5px;border:1px solid var(--border);background:var(--surface);color:var(--text);font-size:10px;width:100%;outline:none;font-family:inherit}
.input:focus,.textarea:focus,.select:focus{border-color:var(--accent)}
.textarea{min-height:60px;resize:vertical}
.input-group{display:flex;gap:5px;margin-bottom:6px}
.input-group .input{flex:1}
.badge{display:inline-flex;padding:2px 9px;border-radius:12px;font-size:8px;font-weight:700;letter-spacing:.3px}
.badge.critique{background:var(--red);color:#fff;box-shadow:0 0 10px rgba(255,0,48,.3)}
.badge.haute{background:var(--orange);color:#fff;box-shadow:0 0 8px rgba(255,107,0,.2)}
.badge.moyenne{background:var(--yellow);color:#000}
.badge.info{background:var(--accent);color:#000}
.tabs{display:flex;gap:2px;margin-bottom:8px;overflow-x:auto;scrollbar-width:none;padding:2px 0}
.tabs::-webkit-scrollbar{display:none}
.tabs button{padding:4px 10px;border-radius:5px;border:none;background:transparent;color:var(--text2);font-size:9px;font-weight:500;cursor:pointer;white-space:nowrap;transition:all .15s}
.tabs button:hover{color:var(--text);background:var(--card)}
.tabs button.active{background:var(--card);color:var(--accent);border-bottom:2px solid var(--accent)}
.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(80px,1fr));gap:6px;margin-bottom:8px}
.stat-card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:8px 6px;text-align:center;transition:.2s}
.stat-card:hover{border-color:var(--accent);transform:translateY(-2px)}
.stat-card .num{font-size:1.1rem;font-weight:800;color:var(--accent);text-shadow:0 0 15px rgba(0,229,255,.2)}
.stat-card .label{font-size:7px;color:var(--text2);text-transform:uppercase;letter-spacing:.5px;font-weight:600}
.modal{display:none;position:fixed;top:0;left:0;right:0;bottom:0;background:rgba(0,0,0,.85);z-index:2000;align-items:center;justify-content:center;backdrop-filter:blur(8px)}
.modal.open{display:flex}
.modal-content{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:16px;max-width:600px;width:92%;max-height:80vh;overflow-y:auto;animation:slideUp .2s ease;position:relative}
@keyframes slideUp{from{transform:translateY(12px);opacity:0}to{transform:translateY(0);opacity:1}}
.modal-content h2{font-size:14px;margin-bottom:8px;background:var(--gradient);-webkit-background-clip:text;-webkit-text-fill-color:transparent;font-weight:800}
.modal-close{position:absolute;top:10px;right:10px;background:var(--card2);border:1px solid var(--border);color:var(--text2);width:26px;height:26px;border-radius:50%;cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:12px;transition:.2s}
.modal-close:hover{background:var(--red);color:#fff;border-color:var(--red)}
.alert-box{background:rgba(255,0,48,.08);border:1px solid var(--red);border-radius:8px;padding:6px 10px;margin-bottom:4px;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:4px;animation:slideAlert .3s}
@keyframes slideAlert{from{opacity:0;transform:translateX(-10px)}to{opacity:1;transform:translateX(0)}}
.alert-box .alert-text{color:var(--red);font-weight:600;font-size:10px}
.chatbot-btn{position:fixed;bottom:20px;right:20px;width:46px;height:46px;border-radius:50%;background:var(--gradient);color:#fff;border:none;font-size:1.2rem;cursor:pointer;box-shadow:0 4px 25px rgba(0,229,255,.4);z-index:999;transition:.3s;display:flex;align-items:center;justify-content:center}
.chatbot-btn:hover{transform:scale(1.1) rotate(10deg);box-shadow:0 6px 35px rgba(0,229,255,.6)}
.chatbot-panel{position:fixed;bottom:76px;right:20px;width:330px;max-height:450px;background:var(--card);border:1px solid var(--border);border-radius:var(--radius);box-shadow:0 20px 60px rgba(0,0,0,.7);display:none;flex-direction:column;z-index:998;overflow:hidden;backdrop-filter:blur(20px)}
.chatbot-panel.show{display:flex;animation:slideUp .3s}
.chatbot-header{background:var(--surface);padding:8px 12px;border-bottom:1px solid var(--border);display:flex;justify-content:space-between;align-items:center}
.chatbot-header span{font-weight:700;background:var(--gradient);-webkit-background-clip:text;-webkit-text-fill-color:transparent;font-size:11px}
.chatbot-header button{background:none;border:none;color:var(--text2);cursor:pointer;font-size:1rem;transition:.2s}
.chatbot-header button:hover{color:var(--accent);transform:rotate(90deg)}
.chatbot-msgs{flex:1;overflow-y:auto;padding:6px 10px;max-height:280px;font-size:11px}
.chatbot-msgs .msg{margin-bottom:4px;padding:5px 8px;border-radius:8px;max-width:92%;font-size:10px;line-height:1.4;animation:msgIn .2s}
@keyframes msgIn{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}
.chatbot-msgs .msg.user{margin-left:auto;background:var(--gradient);color:#fff}
.chatbot-msgs .msg.bot{background:var(--card2);color:var(--text);border:1px solid var(--border)}
.chatbot-input{display:flex;border-top:1px solid var(--border);padding:5px;gap:3px;background:var(--surface)}
.chatbot-input input{flex:1;background:var(--card);border:1px solid var(--border);padding:5px 8px;border-radius:6px;color:var(--text);font-size:10px;transition:.2s}
.chatbot-input input:focus{border-color:var(--accent);outline:none}
.chatbot-input button{background:var(--gradient);color:#fff;border:none;padding:5px 10px;border-radius:6px;cursor:pointer;font-weight:700;font-size:10px;transition:.2s}
.scanner-bar{display:flex;gap:4px;flex-wrap:wrap;align-items:center;margin-bottom:8px;padding:8px 10px;background:var(--card);border-radius:var(--radius);border:1px solid var(--border)}
.scanner-bar input,.scanner-bar select{flex:1;min-width:80px;background:var(--surface);border:1px solid var(--border);padding:5px 8px;border-radius:5px;color:var(--text);font-size:9px;transition:.2s}
.scanner-bar input:focus,.scanner-bar select:focus{border-color:var(--accent);outline:none}
.toast{position:fixed;bottom:80px;left:50%;transform:translateX(-50%);background:var(--card);border:1px solid var(--accent);color:var(--text);padding:8px 16px;border-radius:8px;font-size:10px;z-index:9999;box-shadow:0 10px 40px rgba(0,0,0,.5);animation:toastIn .3s;backdrop-filter:blur(10px)}
@keyframes toastIn{from{opacity:0;transform:translateX(-50%) translateY(20px)}to{opacity:1;transform:translateX(-50%) translateY(0)}}
.login-overlay{display:none}
.alert-marquee{background:linear-gradient(90deg,var(--red),#ff4488);color:#fff;padding:3px 8px;font-size:8px;font-weight:700;border-radius:4px;animation:pulseAlert 1s ease-in-out infinite;text-align:center;margin-bottom:6px}
@keyframes pulseAlert{0%,100%{opacity:1}50%{opacity:.7}}
.category-tag{display:inline-flex;padding:1px 6px;border-radius:3px;font-size:6px;font-weight:700;margin:1px}
.tag-politique{background:#3355aa;color:#fff}.tag-securite{background:#cc3300;color:#fff}.tag-defense{background:#555500;color:#fff}.tag-economie{background:#006633;color:#fff}.tag-cyber{background:#00aaff;color:#000}.tag-societe{background:#8800aa;color:#fff}.tag-diplomatie{background:#003366;color:#fff}.tag-sante{background:#00aa88;color:#fff}.tag-crise{background:#ff0033;color:#fff}.tag-influence{background:#ff8800;color:#fff}
@media(max-width:768px){
  .sidebar{width:42px}
  .sidebar:hover{width:170px}
  .top-bar{left:42px}
  .content{margin:42px 6px 0 48px;padding:6px}
  .grid{grid-template-columns:1fr}
  .stats{grid-template-columns:repeat(2,1fr)}
  .chatbot-panel{width:calc(100% - 12px);right:6px;bottom:70px}
}
</style>
</head>
<body>

<!-- SIDEBAR -->
<div class="sidebar">
  <div class="logo-mini">
    <div class="logo-icon">⬡</div>
    <div class="logo-text">NEXUS DIAMOND</div>
  </div>
  <a class="nav-item active" data-page="dashboard" onclick="showPage('dashboard')"><span class="nav-icon">📊</span><span class="nav-label">Dash</span></a>
  <a class="nav-item" data-page="flux" onclick="showPage('flux')"><span class="nav-icon">📡</span><span class="nav-label">Flux 24h</span></a>
  <a class="nav-item" data-page="alertes" onclick="showPage('alertes')"><span class="nav-icon">🚨</span><span class="nav-label">Alertes</span></a>
  <a class="nav-item" data-page="sources" onclick="showPage('sources')"><span class="nav-icon">📰</span><span class="nav-label">Sources</span></a>
  <a class="nav-item" data-page="influence" onclick="showPage('influence')"><span class="nav-icon">🎯</span><span class="nav-label">Influence</span></a>
  <a class="nav-item" data-page="personnalites" onclick="showPage('personnalites')"><span class="nav-icon">👤</span><span class="nav-label">Personnalités</span></a>
  <a class="nav-item" data-page="securite" onclick="showPage('securite')"><span class="nav-icon">🛡️</span><span class="nav-label">Sécurité</span></a>
  <a class="nav-item" data-page="economie" onclick="showPage('economie')"><span class="nav-icon">📈</span><span class="nav-label">Économie</span></a>
  <a class="nav-item" data-page="cyber" onclick="showPage('cyber')"><span class="nav-icon">💻</span><span class="nav-label">Cyber</span></a>
  <a class="nav-item" data-page="carte" onclick="showPage('carte')"><span class="nav-icon">🗺️</span><span class="nav-label">Carte</span></a>
  <a class="nav-item" data-page="recherche" onclick="showPage('recherche')"><span class="nav-icon">🔍</span><span class="nav-label">Recherche</span></a>
  <a class="nav-item" data-page="historique" onclick="showPage('historique')"><span class="nav-icon">📋</span><span class="nav-label">Historique</span></a>
  <a class="nav-item" data-page="admin" onclick="showPage('admin')"><span class="nav-icon">⚙️</span><span class="nav-label">Admin</span></a>
</div>

<div class="top-bar">
  <div class="page-title" id="pageTitle">📊 Dashboard</div>
  <div class="page-sub" id="pageSub">NEXUS DIAMOND — Veille Stratégique OSINT</div>
  <div class="top-actions">
    <button onclick="toggleThemeCycle()" title="Thème">🎨</button>
    <button onclick="scanAllSources()" title="Scanner">📡</button>
    <div class="user-badge"><span class="dot"></span><span>OSINT Pro</span></div>
  </div>
</div>

<div class="content">

<!-- DASHBOARD -->
<div class="page active" id="page-dashboard">
  <div style="display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:6px;margin-bottom:8px">
    <div><h2 style="font-size:16px">📊 Dashboard — Veille Stratégique</h2><p style="color:var(--text2);font-size:9px">Données des dernières 24h uniquement</p></div>
    <div style="display:flex;gap:4px;flex-wrap:wrap">
      <button class="btn btn-primary btn-sm" onclick="scanAllSources()">📡 Scanner tout</button>
      <button class="btn btn-outline btn-sm" onclick="generateRapport()">📋 Rapport 24h</button>
    </div>
  </div>
  <div id="alertesContainer" style="margin-bottom:6px"></div>
  <div class="stats" id="statsBar"></div>
  <div class="grid grid-3" style="margin-top:6px">
    <div class="card"><div class="card-header"><h3>🚨 Alertes critiques</h3><span class="badge critique" id="criticalBadge">0</span></div><div id="criticalAlertsList" style="max-height:200px;overflow-y:auto"></div></div>
    <div class="card"><div class="card-header"><h3>📡 Derniers flux</h3></div><div id="recentFlux" style="max-height:200px;overflow-y:auto"></div></div>
    <div class="card"><div class="card-header"><h3>📈 Rapport 24h</h3><button class="btn btn-sm btn-outline" onclick="generateRapport()">🔄</button></div><div id="dailyRapport" style="max-height:200px;overflow-y:auto"></div></div>
  </div>
</div>

<!-- FLUX 24H -->
<div class="page" id="page-flux">
  <h2 style="font-size:16px;margin-bottom:2px">📡 Flux en temps réel — 24h</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Toutes les sources classées par niveau de priorité</p>
  <div class="tabs" id="fluxTabs">
    <button class="active" data-level="all">🌐 Tous</button>
    <button data-level="100">🔴 Niv.100 Officiel</button>
    <button data-level="90">🟠 Niv.90 Média</button>
    <button data-level="80">🟡 Niv.80 Afrique</button>
    <button data-level="70">🔵 Niv.70 International</button>
    <button data-level="60">🟢 Niv.60 Réseaux</button>
  </div>
  <div class="scanner-bar">
    <input id="fluxSearch" placeholder="🔍 Filtrer par mot-clé, source, catégorie..." oninput="renderFlux()">
    <select id="fluxCategory" onchange="renderFlux()">
      <option value="all">📁 Toutes catégories</option>
      <option value="Politique">🏛️ Politique</option>
      <option value="Sécurité">🛡️ Sécurité</option>
      <option value="Défense">⚔️ Défense</option>
      <option value="Économie">📈 Économie</option>
      <option value="Cyber">💻 Cyber</option>
      <option value="Société">👥 Société</option>
      <option value="Diplomatie">🌍 Diplomatie</option>
      <option value="Santé">🏥 Santé</option>
      <option value="Crise">⚠️ Crise</option>
      <option value="Influence">📢 Influence</option>
    </select>
  </div>
  <div class="grid grid-2" id="fluxFeed"></div>
</div>

<!-- ALERTES -->
<div class="page" id="page-alertes">
  <h2 style="font-size:16px;margin-bottom:2px">🚨 Système d'alerte intelligent</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Alertes déclenchées uniquement après confirmation multi-sources</p>
  <div class="scanner-bar">
    <select id="alertLevelFilter" onchange="renderAlertes()" style="max-width:120px">
      <option value="all">Tous niveaux</option>
      <option value="critique">🔴 Critique</option>
      <option value="haute">🟠 Haute</option>
      <option value="moyenne">🟡 Moyenne</option>
    </select>
    <span style="font-size:8px;color:var(--text2)" id="alertCount"></span>
  </div>
  <div id="alertesList" style="display:flex;flex-direction:column;gap:4px"></div>
</div>

<!-- SOURCES -->
<div class="page" id="page-sources">
  <h2 style="font-size:16px;margin-bottom:2px">📰 Architecture des sources</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">200+ sources classées par niveau de priorité</p>
  <div class="tabs" id="sourcesTabs">
    <button class="active" data-src="100">🔴 Niv.100 Officiel CI</button>
    <button data-src="90">🟠 Niv.90 Médias CI</button>
    <button data-src="80">🟡 Niv.80 Afrique</button>
    <button data-src="70">🔵 Niv.70 International</button>
    <button data-src="think">🧠 Think Tanks</button>
    <button data-src="cyber">💻 Cybersécurité</button>
    <button data-src="eco">📈 Éco & Finance</button>
  </div>
  <div id="sourcesList" style="display:flex;flex-direction:column;gap:2px;margin-top:6px"></div>
</div>

<!-- INFLUENCE -->
<div class="page" id="page-influence">
  <h2 style="font-size:16px;margin-bottom:2px">🎯 Détection d'influence</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Comptes influents détectés automatiquement (audience > 20k)</p>
  <div class="scanner-bar">
    <input id="influenceSearch" placeholder="Rechercher..." oninput="renderInfluence()">
    <select id="influencePlatform" onchange="renderInfluence()">
      <option value="all">📱 Toutes plateformes</option>
      <option value="facebook">📘 Facebook</option>
      <option value="twitter">🐦 X/Twitter</option>
      <option value="instagram">📸 Instagram</option>
      <option value="tiktok">🎵 TikTok</option>
      <option value="telegram">✈️ Telegram</option>
      <option value="youtube">🎬 YouTube</option>
    </select>
  </div>
  <div class="grid grid-4" id="influenceGrid"></div>
</div>

<!-- PERSONNALITÉS -->
<div class="page" id="page-personnalites">
  <h2 style="font-size:16px;margin-bottom:2px">👤 Personnalités à suivre</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Surveillance automatique des décideurs et personnalités publiques</p>
  <div class="scanner-bar">
    <input id="persoSearch" placeholder="Rechercher..." oninput="renderPersonnalites()">
    <select id="persoCategory" onchange="renderPersonnalites()">
      <option value="all">Tous</option>
      <option value="Gouvernement">🏛️ Gouvernement</option>
      <option value="Institutions">⚖️ Institutions</option>
      <option value="Politique">🗳️ Politique</option>
      <option value="Sécurité">🛡️ Sécurité/Défense</option>
      <option value="Média">📺 Média</option>
      <option value="Société">👥 Société</option>
    </select>
  </div>
  <div class="grid grid-4" id="personnalitesGrid"></div>
</div>

<!-- SÉCURITÉ -->
<div class="page" id="page-securite">
  <h2 style="font-size:16px;margin-bottom:2px">🛡️ Zone Sécurité & Défense</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Surveillance Armée, Gendarmerie, Police, Terrorisme, Frontières, Sahel</p>
  <div id="securiteContent" style="display:flex;flex-direction:column;gap:4px"></div>
</div>

<!-- ÉCONOMIE -->
<div class="page" id="page-economie">
  <h2 style="font-size:16px;margin-bottom:2px">📈 Économie & Finance</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">BCEAO, BRVM, Banque Mondiale, FMI, Marchés</p>
  <div id="economieContent" style="display:flex;flex-direction:column;gap:4px"></div>
</div>

<!-- CYBER -->
<div class="page" id="page-cyber">
  <h2 style="font-size:16px;margin-bottom:2px">💻 Cybersécurité</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">ANSSI, CERT, Talos, CrowdStrike, Mandiant</p>
  <div id="cyberContent" style="display:flex;flex-direction:column;gap:4px"></div>
</div>

<!-- CARTE -->
<div class="page" id="page-carte">
  <h2 style="font-size:16px;margin-bottom:2px">🗺️ Carte des événements</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Événements localisés des dernières 24h</p>
  <div id="carteContent" style="min-height:300px;display:flex;align-items:center;justify-content:center;background:var(--card);border:1px solid var(--border);border-radius:var(--radius)">
    <div style="text-align:center;padding:20px">
      <div style="font-size:3rem;margin-bottom:8px">🗺️</div>
      <p style="font-size:9px;color:var(--text2)">Carte interactive — Les événements géolocalisés apparaîtront ici après scan.<br>Ils sont listés dans la section flux avec leurs coordonnées.</p>
    </div>
  </div>
</div>

<!-- RECHERCHE -->
<div class="page" id="page-recherche">
  <h2 style="font-size:16px;margin-bottom:2px">🔍 Moteur de recherche</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Recherche dans toutes les données des 24h</p>
  <div class="scanner-bar">
    <input id="searchGlobal" placeholder="Rechercher mots-clés, sources, catégories..." onkeydown="if(event.key==='Enter')doSearch()" style="flex:2">
    <select id="searchCategory" onchange="doSearch()" style="max-width:120px">
      <option value="all">Toutes</option>
      <option value="Politique">🏛️ Politique</option>
      <option value="Sécurité">🛡️ Sécurité</option>
      <option value="Défense">⚔️ Défense</option>
      <option value="Économie">📈 Économie</option>
      <option value="Cyber">💻 Cyber</option>
      <option value="Crise">⚠️ Crise</option>
    </select>
    <button class="btn btn-primary btn-sm" onclick="doSearch()">🔍</button>
  </div>
  <div id="searchResults"></div>
</div>

<!-- HISTORIQUE -->
<div class="page" id="page-historique">
  <h2 style="font-size:16px;margin-bottom:2px">📋 Historique des rapports</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Rapports générés automatiquement toutes les 24h</p>
  <button class="btn btn-outline btn-sm mb-6" onclick="generateRapport()">📋 Générer rapport maintenant</button>
  <div id="historiqueList"></div>
</div>

<!-- ADMIN -->
<div class="page" id="page-admin">
  <h2 style="font-size:16px;margin-bottom:2px">⚙️ Administration</h2>
  <p style="color:var(--text2);font-size:9px;margin-bottom:6px">Configuration et gestion</p>
  <div class="tabs" id="adminTabs">
    <button class="active" data-adm="config">⚙️ Config</button>
    <button data-adm="scan">📡 Scan</button>
    <button data-adm="motscles">🔑 Mots-clés</button>
    <button data-adm="themes">🎨 Thèmes</button>
    <button data-adm="export">📤 Export</button>
  </div>
  <div id="adminContent"></div>
</div>

</div>

<div class="modal" id="modal">
  <div class="modal-content">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <h2 id="modalTitle">Détails</h2>
    <div id="modalBody"></div>
  </div>
</div>

<button class="chatbot-btn" onclick="toggleChat()">⟡</button>
<div class="chatbot-panel" id="chatPanel">
  <div class="chatbot-header"><span>⟡ NEXUS IA — Veille</span><button onclick="toggleChat()">✕</button></div>
  <div class="chatbot-msgs" id="chatMsgsFloat">
    <div class="msg bot">⟡ Veille stratégique active. Commandes : alertes, rapport, scan, sources, crise</div>
  </div>
  <div class="chatbot-input">
    <input id="chatInputFloat" placeholder="Message..." onkeydown="if(event.key==='Enter')sendChatFloat()">
    <button onclick="sendChatFloat()">⟡</button>
  </div>
</div>

<script>
// ===================== STRUCTURE DE DONNÉES =====================
const NEXUS = {
  flux: [],         // Tous les articles/flux collectés (uniquement 24h)
  alertes: [],       // Alertes déclenchées
  rapports: [],      // Rapports générés
  influenceurs: [],  // Comptes influents détectés
  personnalites: [], // Personnalités suivies
  searchHistory: []  // Historique de recherche
}

// Mots-clés prioritaires pour le scoring
const KEYWORDS = {
  critique: ['attentat','attaque','cyberattaque','guerre','conflit','nucléaire','missile','bombe','terrorisme','massacre','génocide','crash','catastrophe','mort','décès','assassinat','crise','urgence','alerte','menace','invasion','frappe','insurrection','révolution','coup d\'état','pandémie','épidémie','tuerie','explosion','combat','offensive','blessé','victime','destruction','sanction','embargo','manifestation','grève','émeute','violence','tir','fusillade','prise d\'otage','enlèvement','kidnapping'],
  haute: ['cyberattaque','piratage','vulnérabilité','exploit','CVE','brèche','fuite','espionnage','désinformation','fraude','corruption','sanction','diplomatie','ONU','OTAN','dette','inflation','récession','pétrole','gouvernement','président','élection','vote','parlement','loi','décret','réforme','ministre','armée','police','gendarmerie','frontière','trafic','criminalité','justice','tribunal','accident','énergie'],
  moyenne: ['politique','élection','vote','parlement','gouvernement','président','réforme','loi','décret','nomination','discours','sommet','accord','développement','économie','finance','marché','entreprise','innovation','recherche','santé','éducation','culture','sport','environnement','climat']
}

const CATEGORIES = {
  'Politique': ['gouvernement','président','ministre','parlement','assemblée','sénat','élection','vote','parti','opposition','coalition','député','sénateur','loi','réforme','décret','constitution'],
  'Sécurité': ['armée','police','gendarmerie','sécurité','défense','militaire','frontière','terrorisme','attaque','violence','manifestation','émeute','criminalité','trafic','drogue','arme'],
  'Défense': ['défense','armée','militaire','général','colonel','bataillon','régiment','missile','drone','base','opération','patrouille','renseignement','espionnage'],
  'Économie': ['économie','finance','banque','marché','investissement','croissance','PIB','inflation','dette','budget','fiscal','commerce','export','import','BRVM','BCEAO','FMI','Banque Mondiale'],
  'Cyber': ['cyberattaque','piratage','virus','malware','ransomware','hack','vulnérabilité','CVE','sécurité informatique','ANSSI','CERT','donnée','fuite','brèche','SSI'],
  'Société': ['société','éducation','santé','culture','sport','religion','tradition','jeunesse','femme','droits','ONG','association','manifestation','grève'],
  'Diplomatie': ['diplomatie','ambassade','consulat','ONU','UA','CEDEAO','coopération','accord','traité','visite','sommet','relations internationales'],
  'Santé': ['santé','hôpital','médecin','vaccin','épidémie','pandémie','maladie','traitement','OMS','médicament','urgences'],
  'Crise': ['crise','urgence','catastrophe','attentat','attaque','guerre','conflit','tempête','inondation','séisme','incendie','accident','crash','naufrage'],
  'Influence': ['influence','propagande','désinformation','fake news','manipulation','réseaux sociaux','viral','tendance','hashtag','influenceur']
}

// ===================== SOURCES PAR NIVEAU =====================
const SOURCES = {
  niveau100: [
    {name:'Présidence CI',url:'https://www.presidence.ci/feed/',region:'CI',level:100},
    {name:'Gouvernement CI',url:'https://www.gouv.ci/flashs/rss',region:'CI',level:100},
    {name:'CICG',url:'https://cicg.gouv.ci/rss',region:'CI',level:100},
    {name:'Ministère Défense',url:'https://www.defense.gouv.ci/rss',region:'CI',level:100},
    {name:'Ministère Intérieur',url:'https://www.interieur.gouv.ci/rss',region:'CI',level:100},
    {name:'ANSSI CI',url:'https://anssi.gouv.ci/rss',region:'CI',level:100},
    {name:'CERT CI',url:'https://cert.gouv.ci/rss',region:'CI',level:100},
    {name:'Assemblée Nationale',url:'https://www.assemblee.ci/rss',region:'CI',level:100},
    {name:'CEI',url:'https://www.cei.ci/rss',region:'CI',level:100},
    {name:'BCEAO',url:'https://www.bceao.int/rss',region:'CI',level:100},
    {name:'BRVM',url:'https://www.brvm.org/rss',region:'CI',level:100},
    {name:'Port Abidjan',url:'https://www.paa-ci.org/rss',region:'CI',level:100},
    {name:'Port San Pedro',url:'https://www.pasp-ci.org/rss',region:'CI',level:100},
    {name:'Douanes CI',url:'https://www.douanes.ci/rss',region:'CI',level:100},
    {name:'Trésor Public',url:'https://www.tresor.gouv.ci/rss',region:'CI',level:100},
    {name:'INS CI',url:'https://www.ins.ci/rss',region:'CI',level:100},
    {name:'Protection Civile',url:'https://www.protectioncivile.ci/rss',region:'CI',level:100}
  ],
  niveau90: [
    {name:'AIP',url:'https://aip.ci/feed/',region:'CI',level:90},
    {name:'Abidjan.net',url:'https://www.abidjan.net/actus/rss.xml',region:'CI',level:90},
    {name:'Fraternité Matin',url:'https://www.fratmat.info/rss',region:'CI',level:90},
    {name:'RTI Info',url:'https://www.rti.ci/rss',region:'CI',level:90},
    {name:'NCI',url:'https://www.nci.ci/rss',region:'CI',level:90},
    {name:'7 Info',url:'https://7info.ci/rss',region:'CI',level:90},
    {name:'Soir Info',url:'https://www.soirinfo.com/rss',region:'CI',level:90},
    {name:'Koaci',url:'https://www.koaci.com/rss',region:'CI',level:90},
    {name:'Linfodrome',url:'https://www.linfodrome.com/24h?format=feed',region:'CI',level:90},
    {name:'Connection Ivoirienne',url:'https://www.connectionivoirienne.net/feed/',region:'CI',level:90},
    {name:'Alerte Info',url:'https://www.alerte-info.net/feed/',region:'CI',level:90},
    {name:'AbidjanTV',url:'https://www.abidjantv.net/feed/',region:'CI',level:90},
    {name:'Le Patriote',url:'https://www.lepatriote.net/feed/',region:'CI',level:90},
    {name:"L'Inter",url:'https://www.linter-ci.com/feed/',region:'CI',level:90},
    {name:'Notre Voie',url:'https://www.notrevoie.ci/feed/',region:'CI',level:90},
    {name:'Top News Africa',url:'https://topnewsafrica.net/feed/',region:'CI',level:90},
    {name:'Afrique Sur 7',url:'https://afriquesur7.ci/feed/',region:'CI',level:90},
    {name:'Life TV',url:'https://lifetv.ci/feed/',region:'CI',level:90},
    {name:"A+ Ivoire",url:'https://aplusivoire.com/feed/',region:'CI',level:90},
    {name:'Opera News CI',url:'https://www.operanews.com/ci/feed',region:'CI',level:90}
  ],
  niveau80: [
    {name:'Union Africaine',url:'https://au.int/rss',region:'Afrique',level:80},
    {name:'CEDEAO',url:'https://www.ecowas.int/rss',region:'Afrique',level:80},
    {name:'BAD',url:'https://www.afdb.org/rss',region:'Afrique',level:80},
    {name:'Jeune Afrique',url:'https://www.jeuneafrique.com/feed/',region:'Afrique',level:80},
    {name:'Africanews',url:'https://www.africanews.com/feed/',region:'Afrique',level:80},
    {name:'RFI Afrique',url:'https://www.rfi.fr/fr/afrique/rss',region:'Afrique',level:80},
    {name:'BBC Afrique',url:'https://www.bbc.com/afrique/rss.xml',region:'Afrique',level:80},
    {name:'VOA Afrique',url:'https://www.voaafrique.com/rss',region:'Afrique',level:80},
    {name:'APA News',url:'https://www.apanews.net/feed/',region:'Afrique',level:80},
    {name:'Financial Afrik',url:'https://www.financialafrik.com/feed/',region:'Afrique',level:80},
    {name:'Ecofin',url:'https://www.agenceecofin.com/rss',region:'Afrique',level:80},
    {name:'Africa Intelligence',url:'https://www.africaintelligence.com/rss',region:'Afrique',level:80},
    {name:'ISS Africa',url:'https://issafrica.org/rss',region:'Afrique',level:80},
    {name:'Africa Defense Forum',url:'https://adf-magazine.com/feed/',region:'Afrique',level:80},
    {name:'The Africa Report',url:'https://www.theafricareport.com/feed/',region:'Afrique',level:80},
    {name:'Le Monde Afrique',url:'https://www.lemonde.fr/afrique/rss_full.xml',region:'Afrique',level:80},
    {name:'France24 Afrique',url:'https://www.france24.com/fr/afrique/rss',region:'Afrique',level:80}
  ],
  niveau70: [
    {name:'Reuters',url:'https://www.reutersagency.com/feed/',region:'International',level:70},
    {name:'AFP',url:'https://www.afp.com/rss',region:'International',level:70},
    {name:'AP News',url:'https://apnews.com/apf-topnews.rss',region:'International',level:70},
    {name:'BBC News',url:'https://feeds.bbci.co.uk/news/rss.xml',region:'International',level:70},
    {name:'CNN World',url:'http://rss.cnn.com/rss/edition_world.rss',region:'International',level:70},
    {name:'Al Jazeera',url:'https://www.aljazeera.com/xml/rss/all.xml',region:'International',level:70},
    {name:'France 24',url:'https://www.france24.com/fr/rss',region:'International',level:70},
    {name:'The Guardian',url:'https://www.theguardian.com/world/rss',region:'International',level:70},
    {name:'Le Monde',url:'https://www.lemonde.fr/rss/une.xml',region:'International',level:70},
    {name:'NY Times',url:'https://rss.nytimes.com/services/xml/rss/nyt/World.xml',region:'International',level:70},
    {name:'Bloomberg',url:'https://www.bloomberg.com/feed/podcast/etf-report.xml',region:'International',level:70},
    {name:'Financial Times',url:'https://www.ft.com/rss/home/international',region:'International',level:70},
    {name:'DW',url:'https://rss.dw.com/rdf/rss-en-world',region:'International',level:70},
    {name:'Sky News',url:'https://feeds.skynews.com/feeds/rss/home.xml',region:'International',level:70},
    {name:'Euronews',url:'https://www.euronews.com/rss',region:'International',level:70},
    {name:'Washington Post',url:'https://feeds.washingtonpost.com/rss/world',region:'International',level:70}
  ],
  thinkTanks: [
    {name:'International Crisis Group',url:'https://www.crisisgroup.org/rss-0',region:'Think Tank',level:70},
    {name:'SIPRI',url:'https://www.sipri.org/rss',region:'Think Tank',level:70},
    {name:'ACLED',url:'https://www.acleddata.com/feed/',region:'Think Tank',level:70},
    {name:'Chatham House',url:'https://www.chathamhouse.org/rss',region:'Think Tank',level:70},
    {name:'Brookings',url:'https://www.brookings.edu/feed/',region:'Think Tank',level:70},
    {name:'Carnegie Endowment',url:'https://carnegieendowment.org/rss',region:'Think Tank',level:70},
    {name:'CSIS',url:'https://www.csis.org/rss',region:'Think Tank',level:70},
    {name:'RUSI',url:'https://rusi.org/rss',region:'Think Tank',level:70},
    {name:'Global Terrorism Index',url:'https://www.visionofhumanity.org/rss',region:'Think Tank',level:70},
    {name:'Small Arms Survey',url:'https://www.smallarmssurvey.org/rss',region:'Think Tank',level:70},
    {name:'ONU Info',url:'https://www.un.org/rss',region:'Think Tank',level:70},
    {name:'Interpol',url:'https://www.interpol.int/rss',region:'Think Tank',level:70},
    {name:'UNODC',url:'https://www.unodc.org/rss',region:'Think Tank',level:70},
    {name:'OMS',url:'https://www.who.int/rss',region:'Think Tank',level:70},
    {name:'Banque Mondiale',url:'https://www.worldbank.org/rss',region:'Think Tank',level:70},
    {name:'FMI',url:'https://www.imf.org/rss',region:'Think Tank',level:70},
    {name:'OCDE',url:'https://www.oecd.org/rss',region:'Think Tank',level:70}
  ],
  cyber: [
    {name:'ANSSI FR',url:'https://www.ssi.gouv.fr/rss',region:'Cyber',level:70},
    {name:'CERT-FR',url:'https://cert.ssi.gouv.fr/feed/',region:'Cyber',level:70},
    {name:'Cisco Talos',url:'https://blog.talosintelligence.com/feed/',region:'Cyber',level:70},
    {name:'Microsoft Security',url:'https://www.microsoft.com/security/blog/feed/',region:'Cyber',level:70},
    {name:'Google Threat Intel',url:'https://blog.google/threat-analysis/feed/',region:'Cyber',level:70},
    {name:'CrowdStrike',url:'https://www.crowdstrike.com/blog/feed/',region:'Cyber',level:70},
    {name:'Mandiant',url:'https://www.mandiant.com/resources/feed',region:'Cyber',level:70},
    {name:'Check Point',url:'https://blog.checkpoint.com/feed/',region:'Cyber',level:70},
    {name:'Kaspersky',url:'https://www.kaspersky.com/blog/feed/',region:'Cyber',level:70},
    {name:'Recorded Future',url:'https://www.recordedfuture.com/feed/',region:'Cyber',level:70},
    {name:'Unit 42',url:'https://unit42.paloaltonetworks.com/feed/',region:'Cyber',level:70}
  ],
  economie: [
    {name:'BCEAO Actus',url:'https://www.bceao.int/fr/actualites/rss',region:'Économie',level:70},
    {name:'BRVM Marchés',url:'https://www.brvm.org/fr/actualites/rss',region:'Économie',level:70},
    {name:'Bloomberg Markets',url:'https://www.bloomberg.com/markets/rss',region:'Économie',level:70},
    {name:'Financial Times Markets',url:'https://www.ft.com/markets/rss',region:'Économie',level:70},
    {name:'Trading Economics',url:'https://tradingeconomics.com/rss',region:'Économie',level:70},
    {name:'African Business',url:'https://africanbusinessmagazine.com/feed/',region:'Économie',level:70},
    {name:'Ecofin Pro',url:'https://www.agenceecofin.com/rss',region:'Économie',level:70},
    {name:'Financial Afrik Actu',url:'https://www.financialafrik.com/feed/',region:'Économie',level:70}
  ]
}

// ===================== INFLUENCEURS PRÉDÉFINIS =====================
const DEFAULT_INFLUENCEURS = [
  {name:'Presidence CI',plateforme:'twitter',followers:250000,type:'Institution',url:'https://twitter.com/PresidenceCI',niveau:100},
  {name:'Gouv CI Officiel',plateforme:'twitter',followers:180000,type:'Institution',url:'https://twitter.com/Gouvciofficiel',niveau:100},
  {name:'RTI Info',plateforme:'facebook',followers:890000,type:'Média',url:'https://facebook.com/RTICotedivoire',niveau:90},
  {name:'Abidjan.net',plateforme:'facebook',followers:650000,type:'Média',url:'https://facebook.com/abidjan.net',niveau:90},
  {name:'Fraternité Matin',plateforme:'facebook',followers:420000,type:'Média',url:'https://facebook.com/fratmat.info',niveau:90},
  {name:'7 Info CI',plateforme:'facebook',followers:380000,type:'Média',url:'https://facebook.com/7info.ci',niveau:90},
  {name:'Koaci',plateforme:'facebook',followers:310000,type:'Média',url:'https://facebook.com/koaci',niveau:90},
  {name:'Linfodrome',plateforme:'facebook',followers:290000,type:'Média',url:'https://facebook.com/linfodrome',niveau:90},
  {name:'NCI Officiel',plateforme:'facebook',followers:250000,type:'Média',url:'https://facebook.com/NCICotedivoire',niveau:90},
  {name:'Connection Ivoirienne',plateforme:'facebook',followers:180000,type:'Média',url:'https://facebook.com/connectionivoirienne',niveau:90},
  {name:'Alerte Info CI',plateforme:'facebook',followers:120000,type:'Média',url:'https://facebook.com/alerteinfo',niveau:90},
  {name:'Life TV CI',plateforme:'facebook',followers:95000,type:'Média',url:'https://facebook.com/lifetv.ci',niveau:90},
  {name:'A+ Ivoire',plateforme:'facebook',followers:78000,type:'Média',url:'https://facebook.com/aplusivoire',niveau:90},
  {name:'Abidjan Insta',plateforme:'instagram',followers:340000,type:'Influenceur',url:'https://instagram.com/abidjan_insta',niveau:60},
  {name:'CI Trends',plateforme:'instagram',followers:280000,type:'Influenceur',url:'https://instagram.com/citrends',niveau:60},
  {name:'Afrique Trends',plateforme:'tiktok',followers:560000,type:'Influenceur',url:'https://tiktok.com/@afrique_trends',niveau:60},
  {name:'CI Actu',plateforme:'tiktok',followers:420000,type:'Influenceur',url:'https://tiktok.com/@ci_actu',niveau:60},
  {name:'Infos CI',plateforme:'telegram',followers:125000,type:'Média',url:'https://t.me/infosci',niveau:60},
  {name:'Abidjan Actu',plateforme:'telegram',followers:83000,type:'Média',url:'https://t.me/abidjanactu',niveau:60},
  {name:'Burkina 24',plateforme:'telegram',followers:61000,type:'Média',url:'https://t.me/burkina24',niveau:60},
  {name:'Jeune Afrique',plateforme:'twitter',followers:1200000,type:'Média',url:'https://twitter.com/Jeune_Afrique',niveau:80},
  {name:'RFI Afrique',plateforme:'twitter',followers:980000,type:'Média',url:'https://twitter.com/rfiafrique',niveau:80},
  {name:'BBC Afrique',plateforme:'twitter',followers:750000,type:'Média',url:'https://twitter.com/bbcafrique',niveau:80},
  {name:'Al Jazeera',plateforme:'twitter',followers:2200000,type:'Média',url:'https://twitter.com/AJEnglish',niveau:70},
  {name:'France 24',plateforme:'twitter',followers:1800000,type:'Média',url:'https://twitter.com/France24',niveau:70},
  {name:'Le Monde',plateforme:'twitter',followers:1500000,type:'Média',url:'https://twitter.com/lemonde',niveau:70},
  {name:'NEXUS CI',plateforme:'telegram',followers:4500,type:'Communauté',url:'https://t.me/nexus_ci',niveau:60},
  {name:'YouTube Afrique Actu',plateforme:'youtube',followers:85000,type:'Média',url:'https://youtube.com/@afriqueactu',niveau:60}
]

// ===================== PERSONNALITÉS =====================
const DEFAULT_PERSONNALITES = [
  {nom:'Alassane Ouattara',fonction:'Président de la République',categorie:'Gouvernement',niveau:100,pays:'CI'},
  {nom:'Robert Beugré Mambé',fonction:'Premier Ministre',categorie:'Gouvernement',niveau:100,pays:'CI'},
  {nom:'Téné Birahima Ouattara',fonction:'Ministre de la Défense',categorie:'Sécurité',niveau:100,pays:'CI'},
  {nom:'Vagondo Diomandé',fonction:'Ministre de l\'Intérieur',categorie:'Sécurité',niveau:100,pays:'CI'},
  {nom:'Kassoum Kone',fonction:'Ministre de la Sécurité',categorie:'Sécurité',niveau:100,pays:'CI'},
  {nom:'Adama Coulibaly',fonction:'Ministre des Finances',categorie:'Gouvernement',niveau:100,pays:'CI'},
  {nom:'Kandia Camara',fonction:'Présidente du Sénat',categorie:'Institutions',niveau:100,pays:'CI'},
  {nom:'Adama Bictogo',fonction:'Président Assemblée Nationale',categorie:'Institutions',niveau:100,pays:'CI'},
  {nom:'Patrick Achi',fonction:'Ancien PM',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Pascal Affi N\'Guessan',fonction:'Président FPI',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Tiémoko Meyliet Koné',fonction:'Vice-Président',categorie:'Gouvernement',niveau:100,pays:'CI'},
  {nom:'Mamadou Touré',fonction:'Ministre Jeunesse',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Amadou Gon Coulibaly',fonction:'Ancien PM',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Hamed Bakayoko',fonction:'Ancien PM',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Guillaume Soro',fonction:'Ancien Président AN',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Laurent Gbagbo',fonction:'Ancien Président',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Charles Blé Goudé',fonction:'Ancien Ministre',categorie:'Politique',niveau:90,pays:'CI'},
  {nom:'Mamadou Koné',fonction:'Ministre de la Santé',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Amadou Koné',fonction:'Ministre Transports',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Nasseneba Touré',fonction:'Porte-parole Gouvernement',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Kobenan Kouassi Adjoumani',fonction:'Ministre Agriculture',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Souleymane Diarrassouba',fonction:'Ministre Commerce',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Moussa Dosso',fonction:'Ministre Budget',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Bruno Koné',fonction:'Ministre Communication',categorie:'Gouvernement',niveau:90,pays:'CI'},
  {nom:'Kidiéba Cissé',fonction:'Ministre Défense (ancien)',categorie:'Sécurité',niveau:90,pays:'CI'},
  {nom:'Général Lassina Doumbia',fonction:'CEMG',categorie:'Sécurité',niveau:100,pays:'CI'},
  {nom:'Général Youssouf Kouamé',fonction:'DG Police',categorie:'Sécurité',niveau:100,pays:'CI'},
  {nom:'Contrôleur Yao Kouakou',fonction:'Comdt Gendarmerie',categorie:'Sécurité',niveau:100,pays:'CI'},
  {nom:'Fidèle Sarassoro',fonction:'Secrétaire CNS',categorie:'Sécurité',niveau:100,pays:'CI'},
  {name:'CISCI Président',fonction:'Président CISCI',categorie:'Institutions',niveau:90,pays:'CI'}
]

// ===================== OUTILS =====================
function getAllSources() {
  const all = []
  Object.values(SOURCES).forEach(arr => arr.forEach(s => all.push(s)))
  return all
}

function escHtml(s){if(!s)return'';const d=document.createElement('div');d.textContent=s;return d.innerHTML}
function stripHtml(h){const d=document.createElement('div');d.innerHTML=h;return d.textContent||d.innerText||''}
function formatDate(dt){const d=new Date(dt);if(isNaN(d.getTime()))return dt;return d.toLocaleDateString('fr-FR',{day:'numeric',month:'short',year:'numeric',hour:'2-digit',minute:'2-digit'})}
function timeAgo(d){const diff=Date.now()-new Date(d).getTime();const m=Math.floor(diff/60000);if(m<60)return`${m}min`;const h=Math.floor(m/60);if(h<24)return`${h}h`;return`${Math.floor(h/24)}j`}

function openModal(title,body){document.getElementById('modalTitle').textContent=title;document.getElementById('modalBody').innerHTML=body;document.getElementById('modal').classList.add('open')}
function closeModal(){document.getElementById('modal').classList.remove('open')}
function showToast(msg){const e=document.querySelector('.toast');if(e)e.remove();const t=document.createElement('div');t.className='toast';t.textContent=msg;document.body.appendChild(t);setTimeout(()=>t.remove(),2500)}

// ===================== THÈMES =====================
const themeCycle=['dark','clair','noir','bleu','vert','rouge','violet','or']
let themeIdx=0
function applyTheme(n){document.body.className='theme-'+n;localStorage.setItem('nexus-theme',n)}
function toggleThemeCycle(){themeIdx=(themeIdx+1)%themeCycle.length;applyTheme(themeCycle[themeIdx])}

// ===================== CLASSIFICATION INTELLIGENTE =====================
function classifyItem(title, desc, sourceLevel, sourceRegion) {
  const txt = (title + ' ' + desc).toLowerCase()
  
  // Détection de catégorie
  let categorie = 'Général'
  for (const [cat, mots] of Object.entries(CATEGORIES)) {
    if (mots.some(m => txt.includes(m))) { categorie = cat; break }
  }

  // Niveau d'alerte basé sur mots-clés + source
  let level = 'info'
  let score = 0
  
  // Score selon la source
  const levelScores = {100:40,90:30,80:20,70:15,60:10}
  score += levelScores[sourceLevel] || 10

  // Mots-clés critiques
  for (const kw of KEYWORDS.critique) {
    if (txt.includes(kw)) { score += 50; level = 'critique'; break }
  }
  
  if (level === 'info') {
    for (const kw of KEYWORDS.haute) {
      if (txt.includes(kw)) { score += 30; level = 'haute'; break }
    }
  }
  
  if (level === 'info') {
    for (const kw of KEYWORDS.moyenne) {
      if (txt.includes(kw)) { score += 15; level = 'moyenne' }
    }
  }

  return { level, score, categorie }
}

// ===================== SCAN DES SOURCES =====================
let scanTimer = null

async function fetchRSS(url, timeout = 12000) {
  try {
    const r = await fetch(`https://api.allorigins.win/raw?url=${encodeURIComponent(url)}`, { signal: AbortSignal.timeout(timeout) })
    if (!r.ok) return []
    const txt = await r.text()
    const doc = new DOMParser().parseFromString(txt, 'text/xml')
    return Array.from(doc.querySelectorAll('item')).slice(0, 8).map(item => ({
      title: (item.querySelector('title')?.textContent || '').trim(),
      link: item.querySelector('link')?.textContent || '',
      description: (item.querySelector('description')?.textContent || '').replace(/<[^>]*>/g, '').trim(),
      pubDate: item.querySelector('pubDate')?.textContent || new Date().toISOString(),
      image: extractImage(item)
    }))
  } catch (e) { return [] }
}

function extractImage(item) {
  const m = item.querySelector('media\\:content, content')
  if (m) { const u = m.getAttribute('url'); if (u) return u }
  const e = item.querySelector('enclosure')
  if (e && e.getAttribute('type')?.startsWith('image/')) return e.getAttribute('url')
  const d = item.querySelector('description')?.textContent || ''
  const match = d.match(/src=["']([^"']+\.(jpg|jpeg|png|gif|webp))["']/i)
  return match ? match[1] : null
}

async function scanAllSources() {
  const btns = document.querySelectorAll('[onclick="scanAllSources()"]')
  btns.forEach(b => { b.textContent = '⏳ Scan...'; b.disabled = true })
  
  const sources = getAllSources()
  const results = await Promise.allSettled(sources.map(async src => {
    const items = await fetchRSS(src.url)
    return items.map(item => ({
      title: item.title,
      link: item.link,
      description: item.description,
      pubDate: item.pubDate,
      source: src.name,
      sourceLevel: src.level || 70,
      region: src.region || 'International',
      image: item.image || null,
      sourceType: src.level >= 100 ? 'Officiel' : src.level >= 90 ? 'Média' : src.level >= 80 ? 'Afrique' : src.level >= 70 ? 'International' : 'Réseaux'
    }))
  }))

  const now = Date.now()
  const dayAgo = now - 24 * 60 * 60 * 1000

  const newItems = results
    .filter(r => r.status === 'fulfilled')
    .flatMap(r => r.value)
    .filter(a => a.title && !NEXUS.flux.find(x => x.link === a.link))

  newItems.forEach(a => {
    const cls = classifyItem(a.title, a.description, a.sourceLevel, a.region)
    // Ne garder que les 24h
    const itemDate = new Date(a.pubDate).getTime()
    if (itemDate < dayAgo && newItems.indexOf(a) > -1) return
    
    NEXUS.flux.unshift({
      ...a,
      id: Date.now() + Math.random(),
      date: a.pubDate || new Date().toISOString(),
      level: cls.level,
      score: cls.score,
      categorie: cls.categorie,
      lu: false,
      sauvegarde: false,
      scannedAt: new Date().toISOString(),
      confirmed: false,
      confirmationCount: 0
    })
  })

  // Trier par date et score
  NEXUS.flux.sort((a, b) => {
    const scoreA = a.score || 0
    const scoreB = b.score || 0
    if (scoreA !== scoreB) return scoreB - scoreA
    return new Date(b.date) - new Date(a.date)
  })

  // Nettoyer pour ne garder que 24h
  NEXUS.flux = NEXUS.flux.filter(a => {
    const d = new Date(a.date).getTime()
    return (now - d) <= 24 * 60 * 60 * 1000
  })
  
  // Limiter à 500 max
  if (NEXUS.flux.length > 500) NEXUS.flux.length = 500

  // Détection multi-sources pour confirmation des alertes
  detectAlertesMultiSources()

  btns.forEach(b => { b.textContent = '📡 Scanner'; b.disabled = false })

  // Générer rapport et rafraîchir
  generateRapport()
  renderDash()
  renderFlux()
  renderAlertes()
  
  showToast(`✅ ${newItems.length} nouveaux flux détectés`)
}

// ===================== SYSTÈME D'ALERTE MULTI-SOURCES =====================
function detectAlertesMultiSources() {
  const now = Date.now()
  const dayAgo = now - 24 * 60 * 60 * 1000
  
  // Regrouper par similarité de contenu
  const alertesPotentielles = NEXUS.flux.filter(a => 
    (a.level === 'critique' || a.level === 'haute') && 
    new Date(a.date).getTime() > dayAgo
  )

  // Regrouper par mots-clés communs
  const groupes = {}
  alertesPotentielles.forEach(a => {
    const mots = (a.title + ' ' + a.description).toLowerCase().match(/\b\w{4,}\b/g) || []
    const key = mots.slice(0, 5).sort().join('_')
    if (!groupes[key]) groupes[key] = []
    groupes[key].push(a)
  })

  // Créer des alertes pour les groupes avec multiples sources
  Object.values(groupes).forEach(groupe => {
    if (groupe.length < 2) return // Pas de confirmation multi-source

    // Compter les sources uniques
    const sourcesUniques = [...new Set(groupe.map(a => a.source))]
    
    if (sourcesUniques.length >= 2 || groupe.some(a => a.sourceLevel >= 90)) {
      // Alerte confirmée !
      const meilleur = groupe.sort((a, b) => b.score - a.score)[0]
      
      if (!NEXUS.alertes.find(x => x.titre === meilleur.title)) {
        NEXUS.alertes.unshift({
          id: Date.now() + Math.random(),
          titre: meilleur.title,
          description: meilleur.description,
          niveau: meilleur.level,
          score: meilleur.score + (sourcesUniques.length * 10),
          sources: sourcesUniques,
          sourcesCount: sourcesUniques.length,
          categorie: meilleur.categorie,
          date: new Date().toISOString(),
          lien: meilleur.link,
          lue: false,
          confirmee: true
        })
        
        // Jouer une alerte sonore
        playAlert()
      }
    }
  })

  // Trier les alertes par score
  NEXUS.alertes.sort((a, b) => b.score - a.score || new Date(b.date) - new Date(a.date))
  
  // Limiter
  if (NEXUS.alertes.length > 100) NEXUS.alertes.length = 100
}

function playAlert() {
  try {
    const ctx = new(window.AudioContext || window.webkitAudioContext)()
    const osc = ctx.createOscillator()
    const gain = ctx.createGain()
    osc.connect(gain)
    gain.connect(ctx.destination)
    osc.frequency.value = 880
    osc.type = 'sine'
    gain.gain.setValueAtTime(0.3, ctx.currentTime)
    gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.5)
    osc.start(ctx.currentTime)
    osc.stop(ctx.currentTime + 0.5)
  } catch (e) {}
}

// ===================== GÉNÉRATION RAPPORT 24H =====================
function generateRapport() {
  const now = Date.now()
  const dayAgo = now - 24 * 60 * 60 * 1000
  const flux24h = NEXUS.flux.filter(a => new Date(a.date).getTime() > dayAgo)
  
  const total = flux24h.length
  const critiques = flux24h.filter(a => a.level === 'critique').length
  const hautes = flux24h.filter(a => a.level === 'haute').length
  const moyennes = flux24h.filter(a => a.level === 'moyenne').length
  
  // Stats par source
  const bySource = {}
  flux24h.forEach(a => {
    const s = a.source || 'Inconnu'
    if (!bySource[s]) bySource[s] = []
    bySource[s].push(a)
  })
  
  const sourcesActives = Object.keys(bySource).length
  const topSources = Object.entries(bySource).sort((a,b) => b[1].length - a[1].length).slice(0, 5)
  
  // Top catégories
  const byCat = {}
  flux24h.forEach(a => {
    const c = a.categorie || 'Général'
    if (!byCat[c]) byCat[c] = 0
    byCat[c]++
  })
  const topCats = Object.entries(byCat).sort((a,b) => b[1] - a[1]).slice(0, 5)

  // Mots-clés fréquents
  const words = flux24h.flatMap(a => 
    (a.title + ' ' + a.description).toLowerCase().match(/\b\w{4,}\b/g) || []
  )
  const wordFreq = {}
  words.forEach(w => { wordFreq[w] = (wordFreq[w] || 0) + 1 })
  const stopWords = ['pour','dans','avec','cette','depuis','entre','après','avant','être','faire','plus','moins','très','aussi','mais','ou','et','le','la','les','des','une','sur','que','pas','par','est','sont','aux','ces','ses','nos','vos','nous','vous','ils','elles','leur','lui','qui','quoi','dont','où']
  const topKeywords = Object.entries(wordFreq)
    .filter(([w]) => !stopWords.includes(w) && w.length > 3)
    .sort((a, b) => b[1] - a[1])
    .slice(0, 10)

  // Articles importants
  const importants = flux24h.filter(a => a.level === 'critique' || a.level === 'haute').slice(0, 8)

  // Créer le rapport
  const rapport = {
    id: Date.now(),
    date: new Date().toISOString(),
    total, critiques, hautes, moyennes,
    sourcesActives, topSources, topCats, topKeywords, importants
  }
  
  NEXUS.rapports = NEXUS.rapports || []
  NEXUS.rapports.unshift(rapport)
  if (NEXUS.rapports.length > 50) NEXUS.rapports.length = 50

  // Mettre à jour l'affichage
  updateStats()
  renderRapport()
  renderHistorique()
  
  return rapport
}

// ===================== RENDER DASHBOARD =====================
function renderDash() {
  updateStats()
  renderRapport()
  renderAlertesMarquantes()
}

function updateStats() {
  const now = Date.now()
  const dayAgo = now - 24 * 60 * 60 * 1000
  const flux24h = NEXUS.flux.filter(a => new Date(a.date).getTime() > dayAgo)
  
  const total = NEXUS.flux.length
  const nonLus = NEXUS.flux.filter(a => !a.lu).length
  const critiques = NEXUS.flux.filter(a => a.level === 'critique').length
  const hautes = NEXUS.flux.filter(a => a.level === 'haute').length
  const alertes = NEXUS.alertes.length
  const alertesNonLues = NEXUS.alertes.filter(a => !a.lue).length
  const flux24hCount = flux24h.length
  const sourcesActives = [...new Set(flux24h.map(a => a.source))].length

  const el = document.getElementById('statsBar')
  if (el) {
    el.innerHTML = `
      <div class="stat-card"><div class="num">${total}</div><div class="label">Total flux</div></div>
      <div class="stat-card"><div class="num" style="color:var(--accent)">${flux24hCount}</div><div class="label">24h</div></div>
      <div class="stat-card"><div class="num" style="color:var(--red)">${nonLus}</div><div class="label">Non lus</div></div>
      <div class="stat-card"><div class="num" style="color:var(--red)">${critiques}</div><div class="label">Critiques</div></div>
      <div class="stat-card"><div class="num" style="color:var(--orange)">${hautes}</div><div class="label">Hautes</div></div>
      <div class="stat-card"><div class="num" style="color:var(--yellow)">${alertes}</div><div class="label">Alertes</div></div>
      <div class="stat-card"><div class="num" style="color:var(--gold)">${alertesNonLues}</div><div class="label">Alertes non lues</div></div>
      <div class="stat-card"><div class="num">${sourcesActives}</div><div class="label">Sources actives</div></div>
    `
  }
  
  document.getElementById('criticalBadge').textContent = alertesNonLues
}

function renderAlertesMarquantes() {
  const critList = document.getElementById('criticalAlertsList')
  if (!critList) return
  
  const alertesNonLues = NEXUS.alertes.filter(a => !a.lue).slice(0, 8)
  
  critList.innerHTML = alertesNonLues.length
    ? alertesNonLues.map(a => `
        <div class="brief-item crit" style="cursor:pointer" onclick="openAlerte('${a.id}')">
          <div style="font-size:8px;font-weight:500">🚨 ${a.niveau === 'critique' ? '🔴' : '🟠'} ${a.titre?.substring(0, 50)}</div>
          <div class="brief-source">${a.sources?.join(', ') || 'Multi-sources'} · ${timeAgo(a.date)} · ${a.sourcesCount || 1} sources</div>
        </div>
      `).join('')
    : '<div style="font-size:8px;color:var(--text2);padding:4px;text-align:center">✅ Aucune alerte active</div>'
}

function renderRapport() {
  const el = document.getElementById('dailyRapport')
  if (!el) return
  
  const r = NEXUS.rapports?.[0]
  if (!r) {
    el.innerHTML = '<div style="font-size:8px;color:var(--text2);text-align:center;padding:8px">Lancez un scan pour générer le rapport 24h</div>'
    return
  }
  
  el.innerHTML = `
    <div class="brief-item" style="font-weight:600;margin-bottom:4px;background:var(--gradient);color:#fff;text-align:center;padding:4px 8px;border-radius:6px">
      📊 Rapport 24h — ${r.total} flux
    </div>
    <div style="display:flex;gap:4px;flex-wrap:wrap;margin-bottom:4px">
      <span style="font-size:7px;padding:2px 5px;background:rgba(255,0,48,.15);color:var(--red);border-radius:3px">${r.critiques} critiques</span>
      <span style="font-size:7px;padding:2px 5px;background:rgba(255,107,0,.15);color:var(--orange);border-radius:3px">${r.hautes} hautes</span>
      <span style="font-size:7px;padding:2px 5px;background:rgba(255,204,0,.15);color:var(--yellow);border-radius:3px">${r.moyennes} moyennes</span>
      <span style="font-size:7px;padding:2px 5px;background:rgba(0,229,255,.1);color:var(--accent);border-radius:3px">${r.sourcesActives} sources</span>
    </div>
    ${r.topCats?.length ? `
      <div style="font-size:7px;font-weight:600;color:var(--text2);margin-bottom:2px">📂 Catégories :</div>
      <div style="display:flex;flex-wrap:wrap;gap:2px;margin-bottom:4px">
        ${r.topCats.map(([c, n]) => `<span style="font-size:6px;background:var(--card2);padding:1px 4px;border-radius:3px;color:var(--text2)">${c} (${n})</span>`).join('')}
      </div>
    ` : ''}
    ${r.topKeywords?.length ? `
      <div style="font-size:7px;font-weight:600;color:var(--text2);margin-bottom:2px">🏷️ Tendances :</div>
      <div style="display:flex;flex-wrap:wrap;gap:2px">
        ${r.topKeywords.map(([w, c]) => `<span style="font-size:6px;background:var(--card2);padding:1px 4px;border-radius:3px;color:var(--text2)">${w} (${c})</span>`).join('')}
      </div>
    ` : ''}
    ${r.importants?.length ? `
      <div style="font-size:7px;font-weight:600;color:var(--red);margin-top:4px;margin-bottom:2px">⚠️ Importants :</div>
      ${r.importants.slice(0, 4).map(a => `
        <div class="brief-item ${a.level}" style="cursor:pointer;font-size:7px" onclick="openFluxItem('${a.id}')">
          <div>${a.level === 'critique' ? '🔴' : '🟠'} ${a.title?.substring(0, 45)}</div>
          <div class="brief-source">${a.source} · ${timeAgo(a.date)}</div>
        </div>
      `).join('')}
    ` : ''}
  `

  // Flux récents
  const recentEl = document.getElementById('recentFlux')
  if (recentEl) {
    const recent = NEXUS.flux.slice(0, 8)
    recentEl.innerHTML = recent.map(a => `
      <div style="display:flex;gap:3px;padding:2px 4px;border-bottom:1px solid var(--border);cursor:pointer;align-items:center" onclick="openFluxItem('${a.id}')">
        <span style="font-size:6px;flex-shrink:0">${a.level === 'critique' ? '🔴' : a.level === 'haute' ? '🟠' : a.level === 'moyenne' ? '🟡' : '🔵'}</span>
        <div style="flex:1;min-width:0">
          <div style="font-size:7px;font-weight:500;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${a.title?.substring(0, 55)}</div>
          <div style="font-size:6px;color:var(--text2)">${a.source} · ${timeAgo(a.date)}</div>
        </div>
      </div>
    `).join('')
    if (!recent.length) recentEl.innerHTML = '<div style="font-size:7px;color:var(--text2);padding:4px;text-align:center">Aucun flux récent</div>'
  }
}

// ===================== FLUX 24H =====================
function renderFlux() {
  const search = (document.getElementById('fluxSearch')?.value || '').toLowerCase()
  const levelFilter = document.querySelector('#fluxTabs .active')?.dataset.level || 'all'
  const catFilter = document.getElementById('fluxCategory')?.value || 'all'

  let items = [...NEXUS.flux]
  
  if (levelFilter !== 'all') {
    const lvl = parseInt(levelFilter)
    items = items.filter(a => a.sourceLevel === lvl)
  }
  if (catFilter !== 'all') items = items.filter(a => a.categorie === catFilter)
  if (search) items = items.filter(a => (a.title + ' ' + a.description + ' ' + a.source + ' ' + a.categorie).toLowerCase().includes(search))

  const el = document.getElementById('fluxFeed')
  if (!el) return

  if (!items.length) {
    el.innerHTML = `<div class="card" style="text-align:center;padding:20px;grid-column:1/-1"><p style="font-size:10px;color:var(--text2)">Aucun flux correspondant. Lancez un scan !</p></div>`
    return
  }

  el.innerHTML = items.map(a => {
    const badgeLevel = a.level === 'critique' ? 'badge critique' : a.level === 'haute' ? 'badge haute' : a.level === 'moyenne' ? 'badge moyenne' : 'badge info'
    const labelLevel = a.level === 'critique' ? '🔴 Critique' : a.level === 'haute' ? '🟠 Haute' : a.level === 'moyenne' ? '🟡 Moyenne' : '🔵 Info'
    const catTag = a.categorie ? `<span class="category-tag tag-${a.categorie.toLowerCase()}">${a.categorie}</span>` : ''
    const levelTag = a.sourceLevel ? `<span style="font-size:6px;background:var(--card2);padding:1px 4px;border-radius:2px;color:var(--text2)">Niv.${a.sourceLevel}</span>` : ''
    
    return `<div class="card" style="cursor:pointer;padding:8px" onclick="openFluxItem('${a.id}')">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;gap:4px">
        <div style="flex:1;min-width:0">
          <div style="font-size:9px;font-weight:600">${escHtml(a.title?.substring(0, 80))}</div>
          <div style="font-size:7px;color:var(--text2);margin-top:2px">${escHtml(a.description?.substring(0, 120))}</div>
          <div style="display:flex;gap:3px;margin-top:3px;flex-wrap:wrap;align-items:center">
            <span style="font-size:7px;color:var(--accent)">${a.source || 'Source inconnue'}</span>
            <span style="font-size:6px;color:var(--text2)">· ${timeAgo(a.date)}</span>
            ${levelTag}
            ${catTag}
          </div>
        </div>
        <div style="display:flex;flex-direction:column;gap:2px;align-items:flex-end">
          <span class="${badgeLevel}" style="font-size:6px;padding:1px 5px">${labelLevel}</span>
          <span style="font-size:7px;font-weight:700;color:var(--accent)">${a.score || 0}pts</span>
        </div>
      </div>
    </div>`
  }).join('')
}

function openFluxItem(id) {
  const a = NEXUS.flux.find(x => x.id == id)
  if (!a) return
  a.lu = true
  
  const catTag = a.categorie ? `<span class="category-tag tag-${a.categorie.toLowerCase()}">${a.categorie}</span>` : ''
  
  openModal(`📡 ${a.title?.substring(0, 60)}`, `
    <div style="display:flex;flex-direction:column;gap:6px">
      ${a.image ? `<img src="${a.image}" style="width:100%;max-height:200px;object-fit:cover;border-radius:8px" onerror="this.style.display='none'">` : ''}
      <div style="display:flex;gap:3px;flex-wrap:wrap;align-items:center">
        <span style="background:var(--card2);padding:2px 6px;border-radius:3px;font-size:7px">${a.region || 'International'}</span>
        <span style="background:var(--card2);padding:2px 6px;border-radius:3px;font-size:7px">${a.source || 'Inconnue'}</span>
        <span style="background:var(--card2);padding:2px 6px;border-radius:3px;font-size:7px">${formatDate(a.date)}</span>
        <span style="background:var(--card2);padding:2px 6px;border-radius:3px;font-size:7px">Niveau ${a.sourceLevel}</span>
        ${catTag}
      </div>
      <div style="display:flex;gap:3px;flex-wrap:wrap">
        <span class="badge ${a.level}" style="font-size:7px">${a.level?.toUpperCase()}</span>
        <span style="font-size:8px;font-weight:700;color:var(--accent)">Score: ${a.score || 0}</span>
      </div>
      <p style="font-size:9px;line-height:1.5">${escHtml(a.description)}</p>
      <div style="display:flex;gap:4px;margin-top:4px">
        <a href="${a.link}" target="_blank" class="btn btn-primary btn-sm">🔗 Lire l'original</a>
        <button class="btn btn-sm btn-outline" onclick="closeModal()">✅ Fermer</button>
      </div>
    </div>
  `)
  renderFlux()
  updateStats()
}

// ===================== ALERTES =====================
function renderAlertes() {
  const filter = document.getElementById('alertLevelFilter')?.value || 'all'
  let items = [...NEXUS.alertes]
  if (filter !== 'all') items = items.filter(a => a.niveau === filter)

  const el = document.getElementById('alertesList')
  const countEl = document.getElementById('alertCount')
  if (!el) return
  
  if (countEl) countEl.textContent = `${items.length} alertes`

  el.innerHTML = items.length ? items.map(a => `
    <div class="alert-box" style="cursor:pointer" onclick="openAlerte('${a.id}')">
      <div style="flex:1">
        <div class="alert-text" style="font-size:9px">${a.niveau === 'critique' ? '🔴' : '🟠'} ${a.titre?.substring(0, 60)}</div>
        <div style="font-size:7px;color:var(--text2);margin-top:2px">
          ${a.sources?.slice(0, 3).join(', ') || 'Multi-sources'} · ${a.sourcesCount || 1} sources · ${a.categorie || 'Général'} · ${timeAgo(a.date)}
        </div>
      </div>
      <div style="display:flex;align-items:center;gap:4px">
        <span style="font-size:8px;font-weight:700;color:var(--gold)">${a.score}pts</span>
        <span style="font-size:10px">${a.lue ? '✅' : '🆕'}</span>
      </div>
    </div>
  `).join('') : '<div style="text-align:center;padding:20px;color:var(--text2);font-size:9px">✅ Aucune alerte active</div>'
}

function openAlerte(id) {
  const a = NEXUS.alertes.find(x => x.id == id)
  if (!a) return
  a.lue = true

  openModal(`🚨 ${a.niveau === 'critique' ? '🔴 Critique' : '🟠 Haute'} : ${a.titre?.substring(0, 50)}`, `
    <div style="display:flex;flex-direction:column;gap:6px">
      <div style="display:flex;gap:3px;flex-wrap:wrap">
        <span style="background:${a.niveau === 'critique' ? 'rgba(255,0,48,.15)' : 'rgba(255,107,0,.15)'};color:${a.niveau === 'critique' ? 'var(--red)' : 'var(--orange)'};padding:2px 8px;border-radius:4px;font-size:8px;font-weight:700">${a.niveau?.toUpperCase()}</span>
        <span style="background:var(--card2);padding:2px 8px;border-radius:4px;font-size:8px">${a.categorie || 'Général'}</span>
        <span style="background:var(--card2);padding:2px 8px;border-radius:4px;font-size:8px">Score: ${a.score}</span>
      </div>
      <p style="font-size:9px;line-height:1.5">${escHtml(a.description)}</p>
      <div style="background:var(--card2);padding:6px 8px;border-radius:6px">
        <div style="font-size:8px;font-weight:600;color:var(--accent);margin-bottom:2px">📡 Sources de confirmation (${a.sourcesCount}) :</div>
        <div style="font-size:7px;color:var(--text2)">${a.sources?.join(', ') || 'Multiples sources'}</div>
      </div>
      <div style="font-size:7px;color:var(--text2)">🕐 ${formatDate(a.date)}</div>
      ${a.lien ? `<a href="${a.lien}" target="_blank" class="btn btn-primary btn-sm">🔗 Source originale</a>` : ''}
      <button class="btn btn-sm btn-outline" onclick="closeModal()">✅ Marquer comme lue</button>
    </div>
  `)
  renderAlertes()
  renderAlertesMarquantes()
  updateStats()
}

// ===================== SOURCES =====================
function renderSources() {
  const filter = document.querySelector('#sourcesTabs .active')?.dataset.src || '100'
  const el = document.getElementById('sourcesList')
  if (!el) return

  let sources = []
  if (filter === '100') sources = SOURCES.niveau100
  else if (filter === '90') sources = SOURCES.niveau90
  else if (filter === '80') sources = SOURCES.niveau80
  else if (filter === '70') sources = SOURCES.niveau70
  else if (filter === 'think') sources = SOURCES.thinkTanks
  else if (filter === 'cyber') sources = SOURCES.cyber
  else if (filter === 'eco') sources = SOURCES.economie

  const icons = {100:'🔴',90:'🟠',80:'🟡',70:'🔵'}
  
  el.innerHTML = sources.map(s => `
    <div style="display:flex;justify-content:space-between;align-items:center;padding:4px 8px;background:var(--card2);border-radius:4px;font-size:8px;margin-bottom:2px">
      <span>${icons[s.level] || '🌐'} <strong>${escHtml(s.name)}</strong></span>
      <span style="color:var(--text2);font-size:7px">${s.region || ''} · Niv.${s.level}</span>
      <a href="${s.url}" target="_blank" style="color:var(--accent);font-size:7px;text-decoration:none">🔗</a>
    </div>
  `).join('')
}

// ===================== INFLUENCE =====================
function renderInfluence() {
  const search = (document.getElementById('influenceSearch')?.value || '').toLowerCase()
  const platform = document.getElementById('influencePlatform')?.value || 'all'

  let items = [...(NEXUS.influenceurs?.length ? NEXUS.influenceurs : DEFAULT_INFLUENCEURS)]
  
  if (platform !== 'all') items = items.filter(i => i.plateforme === platform)
  if (search) items = items.filter(i => i.name.toLowerCase().includes(search))

  const icons = {twitter:'🐦',facebook:'📘',instagram:'📸',tiktok:'🎵',telegram:'✈️',youtube:'🎬'}
  const typeColors = {Institution:'var(--accent)',Média:'var(--orange)',Influenceur:'var(--pink)',Communauté:'var(--green)'}

  const el = document.getElementById('influenceGrid')
  if (!el) return

  el.innerHTML = items.map(i => `
    <a href="${i.url}" target="_blank" class="card" style="text-decoration:none;padding:8px">
      <div style="font-size:1.2rem;margin-bottom:2px">${icons[i.plateforme] || '🌐'}</div>
      <div style="font-size:8px;font-weight:600">${escHtml(i.name)}</div>
      <div style="font-size:6px;color:var(--text2)">${i.type || 'Influenceur'}</div>
      <div style="display:flex;justify-content:space-between;margin-top:2px">
        <span style="font-size:7px;color:${typeColors[i.type] || 'var(--text2)'}">👥 ${(i.followers/1000).toFixed(0)}k</span>
        <span style="font-size:6px;color:var(--accent)">Niv.${i.niveau || 60}</span>
      </div>
    </a>
  `).join('')
}

// ===================== PERSONNALITÉS =====================
function renderPersonnalites() {
  const search = (document.getElementById('persoSearch')?.value || '').toLowerCase()
  const cat = document.getElementById('persoCategory')?.value || 'all'

  let items = [...(NEXUS.personnalites?.length ? NEXUS.personnalites : DEFAULT_PERSONNALITES)]
  
  if (cat !== 'all') items = items.filter(p => p.categorie === cat)
  if (search) items = items.filter(p => p.nom.toLowerCase().includes(search) || (p.fonction || '').toLowerCase().includes(search))

  const catColors = {Gouvernement:'var(--accent)',Institutions:'var(--purple)',Politique:'var(--orange)',Sécurité:'var(--red)',Média:'var(--yellow)',Société:'var(--green)'}

  const el = document.getElementById('personnalitesGrid')
  if (!el) return

  el.innerHTML = items.map(p => `
    <div class="card" style="padding:8px;cursor:default">
      <div style="font-size:1rem;margin-bottom:2px">👤</div>
      <div style="font-size:8px;font-weight:600">${escHtml(p.nom || p.name || '')}</div>
      <div style="font-size:6px;color:var(--text2);margin-top:1px">${escHtml(p.fonction || p.role || '')}</div>
      <div style="display:flex;justify-content:space-between;margin-top:2px;align-items:center">
        <span style="font-size:6px;padding:1px 5px;border-radius:2px;background:${catColors[p.categorie] || 'var(--card2)'};color:#fff">${p.categorie || 'Général'}</span>
        <span style="font-size:6px;color:var(--accent)">Niv.${p.niveau || 70}</span>
      </div>
    </div>
  `).join('')
}

// ===================== SÉCURITÉ =====================
function renderSecurite() {
  const el = document.getElementById('securiteContent')
  if (!el) return
  
  const keywordsSecurite = ['attaque','terrorisme','armée','gendarmerie','police','défense','frontière','militaire','sécurité','crime','violence','manifestation','émeute','trafic','drogue','arme','blessé','victime','conflit','combat','offensive','patrouille','renseignement','espionnage','Sahel','Burkina','Mali','Niger','groupe armé']
  
  const items = NEXUS.flux.filter(a => {
    const txt = (a.title + ' ' + a.description).toLowerCase()
    return keywordsSecurite.some(k => txt.includes(k))
  }).slice(0, 20)
  
  el.innerHTML = items.length ? items.map(a => `
    <div class="brief-item ${a.level}" style="cursor:pointer" onclick="openFluxItem('${a.id}')">
      <div style="font-size:8px;font-weight:500">${a.level === 'critique' ? '🔴' : a.level === 'haute' ? '🟠' : '🟡'} ${a.title?.substring(0, 60)}</div>
      <div class="brief-source">${a.source} · ${timeAgo(a.date)} · ${a.categorie || 'Sécurité'}</div>
    </div>
  `).join('') : '<div style="text-align:center;padding:20px;color:var(--text2);font-size:9px">Aucune information Sécurité/Défense dans les 24h</div>'
}

// ===================== ÉCONOMIE =====================
function renderEconomie() {
  const el = document.getElementById('economieContent')
  if (!el) return
  
  const keywordsEco = ['économie','finance','banque','marché','investissement','croissance','PIB','inflation','dette','budget','fiscal','commerce','export','import','BRVM','BCEAO','FMI','Banque Mondiale','pétrole','énergie','entreprise','bourse','fonds','monnaie','taux','devise','or','café','cacao','agriculture']
  
  const items = NEXUS.flux.filter(a => {
    const txt = (a.title + ' ' + a.description).toLowerCase()
    return keywordsEco.some(k => txt.includes(k))
  }).slice(0, 20)
  
  el.innerHTML = items.length ? items.map(a => `
    <div class="brief-item ${a.level}" style="cursor:pointer" onclick="openFluxItem('${a.id}')">
      <div style="font-size:8px;font-weight:500">📈 ${a.title?.substring(0, 60)}</div>
      <div class="brief-source">${a.source} · ${timeAgo(a.date)} · ${a.categorie || 'Économie'}</div>
    </div>
  `).join('') : '<div style="text-align:center;padding:20px;color:var(--text2);font-size:9px">Aucune information économique dans les 24h</div>'
}

// ===================== CYBER =====================
function renderCyber() {
  const el = document.getElementById('cyberContent')
  if (!el) return
  
  const keywordsCyber = ['cyberattaque','piratage','virus','malware','ransomware','hack','vulnérabilité','CVE','sécurité informatique','ANSSI','CERT','donnée','fuite','brèche','SSI','cyber','informatique','hacker','phishing','rançon','cybercriminalité','cyberdéfense']
  
  const items = NEXUS.flux.filter(a => {
    const txt = (a.title + ' ' + a.description).toLowerCase()
    return keywordsCyber.some(k => txt.includes(k))
  }).slice(0, 20)
  
  el.innerHTML = items.length ? items.map(a => `
    <div class="brief-item ${a.level}" style="cursor:pointer" onclick="openFluxItem('${a.id}')">
      <div style="font-size:8px;font-weight:500">💻 ${a.title?.substring(0, 60)}</div>
      <div class="brief-source">${a.source} · ${timeAgo(a.date)} · ${a.categorie || 'Cyber'}</div>
    </div>
  `).join('') : '<div style="text-align:center;padding:20px;color:var(--text2);font-size:9px">Aucune information cyber dans les 24h</div>'
}

// ===================== RECHERCHE =====================
function doSearch() {
  const q = document.getElementById('searchGlobal')?.value.trim()
  const cat = document.getElementById('searchCategory')?.value || 'all'
  
  if (!q) {
    document.getElementById('searchResults').innerHTML = '<div style="text-align:center;color:var(--text2);font-size:9px;padding:20px">Entrez un mot-clé pour rechercher</div>'
    return
  }

  const qLower = q.toLowerCase()
  let results = NEXUS.flux.filter(a => {
    const txt = (a.title + ' ' + a.description + ' ' + a.source + ' ' + a.categorie).toLowerCase()
    return txt.includes(qLower) && (cat === 'all' || a.categorie === cat)
  })

  document.getElementById('searchResults').innerHTML = results.length ? `
    <div style="font-size:8px;color:var(--text2);margin-bottom:6px">${results.length} résultat(s) pour "${escHtml(q)}"</div>
    ${results.slice(0, 30).map(a => `
      <div class="brief-item ${a.level}" style="cursor:pointer" onclick="openFluxItem('${a.id}')">
        <div style="font-size:8px;font-weight:500">${a.level === 'critique' ? '🔴' : a.level === 'haute' ? '🟠' : '🟡'} ${a.title?.substring(0, 60)}</div>
        <div class="brief-source">${a.source} · ${timeAgo(a.date)} · Score: ${a.score || 0}</div>
      </div>
    `).join('')}
  ` : '<div style="text-align:center;padding:20px;color:var(--text2);font-size:9px">❌ Aucun résultat</div>'
}

// ===================== HISTORIQUE =====================
function renderHistorique() {
  const el = document.getElementById('historiqueList')
  if (!el) return
  
  const rapports = NEXUS.rapports || []
  el.innerHTML = rapports.length ? rapports.map((r, i) => `
    <div class="card" style="padding:8px;cursor:pointer" onclick="viewRapport(${i})">
      <div style="display:flex;justify-content:space-between;align-items:center">
        <div>
          <div style="font-size:9px;font-weight:600">📋 Rapport ${formatDate(r.date)}</div>
          <div style="font-size:7px;color:var(--text2)">${r.total} flux · ${r.critiques} critiques · ${r.hautes} hautes · ${r.sourcesActives} sources</div>
        </div>
        <span style="font-size:8px;color:var(--accent)">${timeAgo(r.date)}</span>
      </div>
    </div>
  `).join('') : '<div style="text-align:center;padding:20px;color:var(--text2);font-size:9px">Aucun rapport généré</div>'
}

function viewRapport(i) {
  const r = NEXUS.rapports?.[i]
  if (!r) return
  
  openModal(`📋 Rapport 24h — ${formatDate(r.date)}`, `
    <div style="display:flex;flex-direction:column;gap:6px">
      <div class="stats" style="grid-template-columns:repeat(3,1fr)">
        <div class="stat-card"><div class="num">${r.total}</div><div class="label">Flux</div></div>
        <div class="stat-card"><div class="num" style="color:var(--red)">${r.critiques}</div><div class="label">Critiques</div></div>
        <div class="stat-card"><div class="num" style="color:var(--orange)">${r.hautes}</div><div class="label">Hautes</div></div>
      </div>
      ${r.topSources?.length ? `
        <div style="font-size:8px;font-weight:600;color:var(--text2)">📡 Top sources :</div>
        <div style="display:flex;flex-direction:column;gap:2px">
          ${r.topSources.map(([s, c]) => `<div style="font-size:7px;background:var(--card2);padding:2px 6px;border-radius:3px">${s} (${c} articles)</div>`).join('')}
        </div>
      ` : ''}
      ${r.topCats?.length ? `
        <div style="font-size:8px;font-weight:600;color:var(--text2)">📂 Catégories :</div>
        <div style="display:flex;flex-wrap:wrap;gap:2px">
          ${r.topCats.map(([c, n]) => `<span style="font-size:7px;background:var(--card2);padding:2px 6px;border-radius:3px">${c}: ${n}</span>`).join('')}
        </div>
      ` : ''}
      ${r.topKeywords?.length ? `
        <div style="font-size:8px;font-weight:600;color:var(--text2)">🏷️ Tendances :</div>
        <div style="display:flex;flex-wrap:wrap;gap:2px">
          ${r.topKeywords.map(([w, c]) => `<span style="font-size:6px;background:var(--card2);padding:1px 5px;border-radius:3px;color:var(--text2)">${w} (${c})</span>`).join('')}
        </div>
      ` : ''}
    </div>
  `)
}

// ===================== ADMIN =====================
function renderAdmin() {
  const filter = document.querySelector('#adminTabs .active')?.dataset.adm || 'config'
  const el = document.getElementById('adminContent')
  if (!el) return

  if (filter === 'config') {
    el.innerHTML = `
      <div class="admin-grid">
        <div class="admin-card">
          <h3>⚙️ Configuration veille</h3>
          <label>Intervalle scan auto (ms)</label>
          <input id="admInterval" type="number" value="180000">
          <label>Max flux en mémoire</label>
          <input id="admMax" type="number" value="500">
          <button onclick="saveAdminConfig()">💾 Sauvegarder</button>
        </div>
        <div class="admin-card">
          <h3>📊 Statistiques</h3>
          <p style="font-size:8px;color:var(--text2)">Flux: ${NEXUS.flux.length}</p>
          <p style="font-size:8px;color:var(--text2)">Alertes: ${NEXUS.alertes.length}</p>
          <p style="font-size:8px;color:var(--text2)">Rapports: ${(NEXUS.rapports || []).length}</p>
          <p style="font-size:8px;color:var(--text2)">Sources configurées: ${getAllSources().length}</p>
          <p style="font-size:8px;color:var(--text2)">Influenceurs: ${(NEXUS.influenceurs || DEFAULT_INFLUENCEURS).length}</p>
          <p style="font-size:8px;color:var(--text2)">Personnalités: ${(NEXUS.personnalites || DEFAULT_PERSONNALITES).length}</p>
        </div>
        <div class="admin-card">
          <h3>💾 Données</h3>
          <button onclick="exportData()" style="width:100%;margin-bottom:4px">📤 Exporter JSON</button>
          <button onclick="document.getElementById('importFileInput').click()" style="width:100%">📥 Importer JSON</button>
          <input type="file" id="importFileInput" accept=".json" style="display:none" onchange="handleImport(event)">
          <button onclick="clearAllData()" class="danger" style="width:100%;margin-top:4px">🗑️ Tout effacer</button>
        </div>
      </div>
    `
  } else if (filter === 'scan') {
    el.innerHTML = `
      <div class="admin-grid">
        <div class="admin-card">
          <h3>📡 Contrôle du scan</h3>
          <button onclick="scanAllSources()" style="width:100%;margin-bottom:4px">🔄 Lancer le scan maintenant</button>
          <button onclick="startAutoScan()" style="width:100%;margin-bottom:4px">▶️ Activer scan auto</button>
          <button onclick="if(scanTimer){clearInterval(scanTimer);scanTimer=null;showToast('⏹️ Scan auto désactivé')}" style="width:100%">⏹️ Désactiver scan auto</button>
        </div>
        <div class="admin-card">
          <h3>📊 Dernier scan</h3>
          <div id="lastScanInfo" style="font-size:8px;color:var(--text2)">Aucun scan effectué</div>
        </div>
      </div>
    `
  } else if (filter === 'motscles') {
    el.innerHTML = `
      <div class="admin-grid">
        <div class="admin-card">
          <h3>🔴 Mots-clés critiques</h3>
          <textarea class="textarea" id="kwCrit" rows="4">${KEYWORDS.critique.join('\n')}</textarea>
          <button onclick="saveKeywords('critique')">💾</button>
        </div>
        <div class="admin-card">
          <h3>🟠 Mots-clés hautes</h3>
          <textarea class="textarea" id="kwHaut" rows="4">${KEYWORDS.haute.join('\n')}</textarea>
          <button onclick="saveKeywords('haute')">💾</button>
        </div>
        <div class="admin-card">
          <h3>🟡 Mots-clés moyennes</h3>
          <textarea class="textarea" id="kwMoy" rows="4">${KEYWORDS.moyenne.join('\n')}</textarea>
          <button onclick="saveKeywords('moyenne')">💾</button>
        </div>
      </div>
    `
  } else if (filter === 'themes') {
    const themes = {dark:'🌙 Sombre',clair:'☀️ Clair',noir:'⬛ Noir',bleu:'🔵 Bleu',vert:'🟢 Vert',rouge:'🔴 Rouge',violet:'🟣 Violet',or:'🟡 Or'}
    el.innerHTML = `
      <div class="admin-grid">
        ${Object.entries(themes).map(([k, v]) => `
          <div class="admin-card" style="cursor:pointer;text-align:center" onclick="applyTheme('${k}')">
            <div style="font-size:1.5rem;margin-bottom:4px">${v.split(' ')[0]}</div>
            <div style="font-size:9px;font-weight:600">${v}</div>
          </div>
        `).join('')}
      </div>
    `
  } else if (filter === 'export') {
    el.innerHTML = `
      <div class="admin-grid">
        <div class="admin-card">
          <h3>📤 Export</h3>
          <button onclick="exportData()" style="width:100%">📥 Télécharger JSON</button>
        </div>
        <div class="admin-card">
          <h3>📥 Import</h3>
          <button onclick="document.getElementById('importFileInput').click()" style="width:100%">📤 Choisir fichier</button>
        </div>
      </div>
    `
  }
}

function saveAdminConfig() {
  const interval = parseInt(document.getElementById('admInterval').value) || 180000
  showToast('✅ Configuration sauvegardée')
  if (scanTimer) { clearInterval(scanTimer); startAutoScan() }
}

function saveKeywords(level) {
  const el = document.getElementById('kw' + level.charAt(0).toUpperCase() + level.slice(1))
  if (el) KEYWORDS[level] = el.value.split('\n').map(s => s.trim()).filter(Boolean)
  showToast('✅ Mots-clés ' + level + ' sauvegardés')
}

function exportData() {
  const data = { nexus: NEXUS, keywords: KEYWORDS, date: new Date().toISOString() }
  const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' })
  const a = document.createElement('a')
  a.href = URL.createObjectURL(blob)
  a.download = 'NEXUS_OSINT_export_' + new Date().toISOString().slice(0, 10) + '.json'
  a.click()
  showToast('✅ Export téléchargé')
}

function handleImport(event) {
  const file = event.target.files[0]
  if (!file) return
  const reader = new FileReader()
  reader.onload = function(e) {
    try {
      const data = JSON.parse(e.target.result)
      if (data.nexus) {
        Object.keys(data.nexus).forEach(k => { if (k in NEXUS) NEXUS[k] = data.nexus[k] })
      }
      saveState()
      generateRapport()
      showToast('✅ Données importées')
    } catch (err) { showToast('❌ Erreur: ' + err.message) }
  }
  reader.readAsText(file)
  event.target.value = ''
}

function clearAllData() {
  if (!confirm('🗑️ Effacer toutes les données ?')) return
  Object.keys(NEXUS).forEach(k => { if (Array.isArray(NEXUS[k])) NEXUS[k] = [] })
  saveState()
  showToast('🗑️ Données effacées')
}

// ===================== CHATBOT =====================
function sendChatFloat() {
  const input = document.getElementById('chatInputFloat')
  const msg = input?.value.trim()
  if (!msg) return
  addChatMsgFloat(msg, 'user')
  input.value = ''
  setTimeout(() => {
    const response = chatbotResponse(msg)
    addChatMsgFloat(response, 'bot')
  }, 200)
}

function addChatMsgFloat(text, sender) {
  const el = document.getElementById('chatMsgsFloat')
  if (!el) return
  el.innerHTML += `<div class="msg ${sender}">${escHtml(text)}</div>`
  el.scrollTop = el.scrollHeight
}

function chatbotResponse(msg) {
  const m = msg.toLowerCase()
  
  // Stats
  if (m.includes('stats') || m.includes('statistique')) {
    const now = Date.now()
    const dayAgo = now - 24 * 60 * 60 * 1000
    const flux24h = NEXUS.flux.filter(a => new Date(a.date).getTime() > dayAgo)
    return `📊 **Stats**: ${NEXUS.flux.length} flux total, ${flux24h.length} dans les 24h, ${NEXUS.alertes.length} alertes dont ${NEXUS.alertes.filter(a => !a.lue).length} non lues`
  }
  
  // Alertes
  if (m.includes('alerte') || m.includes('critique') || m.includes('crise')) {
    const nonLues = NEXUS.alertes.filter(a => !a.lue).slice(0, 5)
    return nonLues.length 
      ? `🚨 ${nonLues.length} alerte(s) non lue(s) : ${nonLues.map(a => a.titre?.substring(0, 40)).join(' | ')}`
      : '✅ Aucune alerte non lue'
  }
  
  // Rapport
  if (m.includes('rapport') || m.includes('synthèse') || m.includes('résumé') || m.includes('brief')) {
    generateRapport()
    const r = NEXUS.rapports?.[0]
    return r ? `📋 Rapport 24h : ${r.total} flux, ${r.critiques} critiques, ${r.hautes} hautes, ${r.sourcesActives} sources actives. Consultez le Dashboard.` : 'Aucun rapport disponible. Lancez un scan.'
  }
  
  // Sources
  if (m.includes('source') || m.includes('niveau')) {
    return `📡 Sources configurées : ${SOURCES.niveau100.length} officielles CI, ${SOURCES.niveau90.length} médias CI, ${SOURCES.niveau80.length} africaines, ${SOURCES.niveau70.length} internationales, ${SOURCES.thinkTanks.length} think tanks, ${SOURCES.cyber.length} cyber. Total: ${getAllSources().length} sources`
  }
  
  // Scan
  if (m.includes('scan')) {
    scanAllSources()
    return '📡 Scan lancé...'
  }
  
  // Influence
  if (m.includes('influence') || m.includes('influenceur')) {
    const infl = NEXUS.influenceurs?.length ? NEXUS.influenceurs : DEFAULT_INFLUENCEURS
    return `🎯 ${infl.length} influenceurs détectés. Les plus suivis : ${infl.sort((a,b) => b.followers - a.followers).slice(0, 3).map(i => i.name + ' (' + (i.followers/1000).toFixed(0) + 'k)').join(', ')}`
  }
  
  // Thème
  if (m.includes('thème') || m.includes('theme')) {
    toggleThemeCycle()
    return '🎨 Thème changé'
  }
  
  // Aide
  if (m.includes('aide') || m.includes('command') || m.includes('help')) {
    return '⟡ **Commandes**: stats, alertes, rapport, sources, scan, influence, thème, crise, aide'
  }
  
  return `⟡ **NEXUS Veille** — Commande reçue. Tapez "aide" pour les commandes disponibles.`
}

function toggleChat() {
  document.getElementById('chatPanel')?.classList.toggle('show')
}

// ===================== PAGE NAVIGATION =====================
const PAGE_TITLES = {
  dashboard:'📊 Dashboard',flux:'📡 Flux 24h',alertes:'🚨 Alertes',sources:'📰 Sources',
  influence:'🎯 Influence',personnalites:'👤 Personnalités',securite:'🛡️ Sécurité',
  economie:'📈 Économie',cyber:'💻 Cyber',carte:'🗺️ Carte',recherche:'🔍 Recherche',
  historique:'📋 Historique',admin:'⚙️ Admin'
}
const PAGE_SUBS = {
  dashboard:'NEXUS DIAMOND — Veille Stratégique OSINT Intelligent',
  flux:'Toutes les sources classées par niveau de priorité — données 24h',
  alertes:'Alertes déclenchées uniquement après confirmation multi-sources',
  sources:'200+ sources classées par niveau de priorité',
  influence:'Comptes influents détectés automatiquement (audience > 20k)',
  personnalités:'Surveillance des décideurs et personnalités publiques',
  securite:'Armée, Gendarmerie, Police, Terrorisme, Frontières, Sahel',
  economie:'BCEAO, BRVM, Banque Mondiale, FMI, Marchés financiers',
  cyber:'ANSSI, CERT, Talos, CrowdStrike, Mandiant - Veille Cyber',
  carte:'Événements géolocalisés des dernières 24h',
  recherche:'Recherche dans toutes les données des 24h',
  historique:'Rapports générés automatiquement',
  admin:'Configuration et gestion'
}

function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'))
  const el = document.getElementById('page-' + id)
  if (el) el.classList.add('active')
  
  document.querySelectorAll('.sidebar .nav-item').forEach(a => a.classList.remove('active'))
  const nav = document.querySelector(`.sidebar .nav-item[data-page="${id}"]`)
  if (nav) nav.classList.add('active')
  
  const t = document.getElementById('pageTitle')
  if (t) t.textContent = PAGE_TITLES[id] || '📊 Dashboard'
  const s = document.getElementById('pageSub')
  if (s) s.textContent = PAGE_SUBS[id] || ''
  
  renderPage(id)
}

function renderPage(id) {
  const fns = {
    dashboard: renderDash, flux: renderFlux, alertes: renderAlertes,
    sources: renderSources, influence: renderInfluence, personnalites: renderPersonnalites,
    securite: renderSecurite, economie: renderEconomie, cyber: renderCyber,
    recherche: () => {}, historique: renderHistorique, admin: renderAdmin
  }
  if (fns[id]) fns[id]()
}

// ===================== SAUVEGARDE =====================
function saveState() {
  try {
    const toSave = {
      flux: NEXUS.flux.slice(0, 500),
      alertes: NEXUS.alertes.slice(0, 100),
      rapports: (NEXUS.rapports || []).slice(0, 50),
      influenceurs: NEXUS.influenceurs,
      personnalites: NEXUS.personnalites
    }
    localStorage.setItem('nexus-osint-data', JSON.stringify(toSave))
  } catch (e) { console.warn('Save error:', e) }
}

function loadState() {
  try {
    const saved = localStorage.getItem('nexus-osint-data')
    if (saved) {
      const data = JSON.parse(saved)
      Object.keys(data).forEach(k => { NEXUS[k] = data[k] || [] })
    }
    const theme = localStorage.getItem('nexus-theme')
    if (theme) applyTheme(theme)
  } catch (e) { console.warn('Load error:', e) }
}

// ===================== SCAN AUTO =====================
function startAutoScan() {
  if (scanTimer) clearInterval(scanTimer)
  scanTimer = setInterval(scanAllSources, 180000)
  showToast('▶️ Scan auto activé (toutes les 3 min)')
}

// ===================== INIT =====================
function initApp() {
  loadState()
  
  const arrays = ['flux', 'alertes', 'rapports', 'influenceurs', 'personnalites']
  arrays.forEach(k => { if (!NEXUS[k]) NEXUS[k] = [] })
  
  showPage('dashboard')
  
  setTimeout(scanAllSources, 1000)
  startAutoScan()
  setInterval(saveState, 60000)
  
  showToast('⟡ NEXUS DIAMOND — Veille Stratégique OSINT active')
}

// ===================== EVENT LISTENERS =====================
document.addEventListener('click', function(e) {
  // Flux tabs
  const fluxBtn = e.target.closest('#fluxTabs button')
  if (fluxBtn) {
    document.querySelectorAll('#fluxTabs button').forEach(b => b.classList.remove('active'))
    fluxBtn.classList.add('active')
    renderFlux()
  }
  
  // Sources tabs
  const srcBtn = e.target.closest('#sourcesTabs button')
  if (srcBtn) {
    document.querySelectorAll('#sourcesTabs button').forEach(b => b.classList.remove('active'))
    srcBtn.classList.add('active')
    renderSources()
  }
  
  // Admin tabs
  const adminBtn = e.target.closest('#adminTabs button')
  if (adminBtn) {
    document.querySelectorAll('#adminTabs button').forEach(b => b.classList.remove('active'))
    adminBtn.classList.add('active')
    renderAdmin()
  }
})

// Fermer modal en cliquant dehors
document.getElementById('modal')?.addEventListener('click', function(e) {
  if (e.target === this) closeModal()
})

// ===================== DÉMARRAGE =====================
document.addEventListener('DOMContentLoaded', initApp)

console.log('⟡ NEXUS DIAMOND — Veille Stratégique OSINT Intelligent v1.0')
console.log(`📡 ${getAllSources().length} sources configurées`)
console.log(`🎯 ${DEFAULT_INFLUENCEURS.length} influenceurs`)
console.log(`👤 ${DEFAULT_PERSONNALITES.length} personnalités`)
console.log('🔑 Mots-clés: ' + Object.values(KEYWORDS).flat().length + ' au total')
</script>
</body>
</html>
