<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NEXUS INTELLIGENCE — Cellule de Renseignement</title>
<style>
/* ============================================================
   NEXUS INTELLIGENCE v4.0 — Cellule de Renseignement Premium
   ============================================================ */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');

:root {
  --bg-deep: #050508; --bg-primary: #07070e; --bg-secondary: #0b0b18; --bg-tertiary: #111122;
  --bg-card: rgba(16,16,34,0.75); --bg-card-hover: rgba(24,24,48,0.92); --bg-glass: rgba(255,255,255,0.03);
  --text-primary: #f0f0f5; --text-secondary: #9999bb; --text-muted: #555577;
  --accent: #00d4ff; --accent-dark: #00a8cc; --accent-glow: rgba(0,212,255,0.3);
  --green: #00ff88; --green-dim: rgba(0,255,136,0.12); --orange: #ff8800; --red: #ff2244; --purple: #7c3aed; --gold: #ffd700;
  --border: rgba(255,255,255,0.06); --border-light: rgba(255,255,255,0.1);
  --radius-sm: 8px; --radius-md: 14px; --radius-lg: 22px;
  --transition: 0.35s cubic-bezier(0.4,0,0.2,1); --transition-bounce: 0.5s cubic-bezier(0.34,1.56,0.64,1);
}

[data-theme="light"] {
  --bg-deep: #f0f0f5; --bg-primary: #fff; --bg-secondary: #f5f5fa; --bg-tertiary: #e8e8f0;
  --bg-card: rgba(255,255,255,0.85); --text-primary: #111; --text-secondary: #555; --text-muted: #888;
  --border: rgba(0,0,0,0.08); --border-light: rgba(0,0,0,0.12);
}

*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Inter','Segoe UI',system-ui,sans-serif;background:var(--bg-deep);color:var(--text-primary);min-height:100vh;overflow-x:hidden;-webkit-font-smoothing:antialiased}
::-webkit-scrollbar{width:4px}::-webkit-scrollbar-track{background:var(--bg-deep)}::-webkit-scrollbar-thumb{background:linear-gradient(180deg,var(--accent),var(--purple));border-radius:4px}

body::before{content:'';position:fixed;top:0;left:0;width:100%;height:100%;background:radial-gradient(ellipse at 15% 30%,rgba(124,58,237,0.05) 0%,transparent 55%),radial-gradient(ellipse at 85% 20%,rgba(0,212,255,0.04) 0%,transparent 50%);pointer-events:none;z-index:0}

.layout{display:grid;grid-template-columns:240px 1fr;min-height:100vh;position:relative;z-index:1}

.sidebar{background:linear-gradient(180deg,var(--bg-secondary),var(--bg-tertiary));border-right:1px solid var(--border);position:fixed;top:0;left:0;height:100vh;overflow:hidden;display:flex;flex-direction:column;transition:width var(--transition);width:240px;z-index:100}
.sidebar.collapsed{width:64px}.sidebar.collapsed:hover{width:240px}
.sidebar-inner{padding:20px 12px;display:flex;flex-direction:column;gap:1px;height:100%;overflow-y:auto;overflow-x:hidden}
.sidebar.collapsed .sidebar-inner{padding:20px 8px}

.logo-wrap{display:flex;align-items:center;gap:12px;padding:4px 10px;margin-bottom:22px;overflow:hidden;white-space:nowrap;min-height:40px}
.logo-icon-bg{flex-shrink:0;width:34px;height:34px;background:linear-gradient(135deg,var(--accent),var(--purple));border-radius:10px;display:flex;align-items:center;justify-content:center;font-size:18px;box-shadow:0 0 24px var(--accent-glow)}
.logo-text{font-size:16px;font-weight:800;letter-spacing:-0.5px}
.logo-text .accent{color:var(--accent)}.logo-text .dim{color:var(--text-muted)}

.nav-item{display:flex;align-items:center;gap:12px;padding:10px 14px;border-radius:var(--radius-md);cursor:pointer;font-size:12px;font-weight:500;color:var(--text-muted);transition:var(--transition);position:relative;overflow:hidden;white-space:nowrap;user-select:none}
.nav-item:hover{color:var(--text-primary);background:var(--bg-glass)}
.nav-item.active{color:var(--accent);background:linear-gradient(135deg,rgba(0,212,255,0.1),rgba(124,58,237,0.06));border:1px solid rgba(0,212,255,0.12)}
.nav-item.active .nav-slider{position:absolute;left:-14px;top:50%;transform:translateY(-50%);width:3px;height:20px;background:linear-gradient(180deg,var(--accent),var(--purple));border-radius:0 4px 4px 0;box-shadow:0 0 12px var(--accent-glow);animation:slideIn 0.4s ease}
@keyframes slideIn{from{height:0;opacity:0}to{height:20px;opacity:1}}
.nav-icon{font-size:15px;width:22px;text-align:center;flex-shrink:0}.nav-label{overflow:hidden;text-overflow:ellipsis}
.sidebar.collapsed .nav-label,.sidebar.collapsed .logo-text,.sidebar.collapsed .sidebar-footer-text{opacity:0;width:0}
.sidebar.collapsed .logo-wrap{justify-content:center;padding:4px 0}
.sidebar.collapsed .nav-item{justify-content:center;padding:10px 0}
.sidebar.collapsed .nav-item.active .nav-slider{left:-8px}
.sidebar.collapsed:hover .nav-label,.sidebar.collapsed:hover .logo-text,.sidebar.collapsed:hover .sidebar-footer-text{display:inline;opacity:1;width:auto}
.sidebar.collapsed:hover .nav-item{justify-content:flex-start;padding:10px 14px}
.sidebar.collapsed:hover .logo-wrap{justify-content:flex-start;padding:4px 10px}
.sidebar.collapsed:hover .nav-item.active .nav-slider{left:-14px}

.sidebar-toggle{position:absolute;top:20px;right:-14px;width:28px;height:28px;background:var(--bg-card);border:1px solid var(--border-light);border-radius:50%;display:flex;align-items:center;justify-content:center;cursor:pointer;font-size:12px;color:var(--text-muted);transition:var(--transition);z-index:10;backdrop-filter:blur(10px)}
.sidebar-toggle:hover{background:var(--accent);color:#000;transform:scale(1.1)}
.sidebar.collapsed .sidebar-toggle{transform:rotate(180deg)}

.sidebar-footer{margin-top:auto;padding:12px 14px 8px;border-top:1px solid var(--border);font-size:8px;color:var(--text-muted);text-align:center;overflow:hidden;white-space:nowrap}
.version-badge{display:inline-block;padding:2px 8px;border-radius:10px;background:var(--accent-glow);color:var(--accent);font-weight:700;font-size:7px;margin-bottom:4px}

.main{padding:20px 28px;position:relative;z-index:1;margin-left:240px;transition:margin var(--transition);min-height:100vh}
.sidebar.collapsed ~ .main{margin-left:64px}

.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:20px;gap:16px;flex-wrap:wrap}
.topbar-left{display:flex;align-items:center;gap:12px}
.topbar-left h1{font-size:20px;font-weight:800;background:linear-gradient(135deg,var(--text-primary) 30%,var(--accent) 100%);-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;letter-spacing:-0.5px}
.topbar-right{display:flex;align-items:center;gap:10px;flex-wrap:wrap}

.search-box{display:flex;align-items:center;background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius-lg);padding:7px 16px;gap:8px;transition:var(--transition);backdrop-filter:blur(16px);min-width:200px}
.search-box:focus-within{border-color:var(--accent);box-shadow:0 0 20px var(--accent-glow)}
.search-box input{background:none;border:none;color:var(--text-primary);font-size:12px;outline:none;width:100%;font-family:inherit}
.search-box input::placeholder{color:var(--text-muted)}

.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:10px;margin-bottom:16px}
.stat-card{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius-md);padding:14px;backdrop-filter:blur(16px);transition:var(--transition)}
.stat-card:hover{border-color:var(--border-light);transform:translateY(-2px)}
.stat-card .stat-value{font-size:22px;font-weight:800;letter-spacing:-0.5px}
.stat-card .stat-label{font-size:9px;color:var(--text-muted);margin-top:2px;font-weight:500;text-transform:uppercase;letter-spacing:0.5px}

.card{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius-md);padding:14px;backdrop-filter:blur(16px);transition:var(--transition)}
.card:hover{border-color:var(--border-light)}

.tabs{display:flex;gap:4px;margin-bottom:12px;flex-wrap:wrap}
.tabs button{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius-lg);padding:5px 14px;color:var(--text-muted);cursor:pointer;font-size:10px;font-weight:500;transition:var(--transition);font-family:inherit}
.tabs button:hover{color:var(--text-primary)}
.tabs button.active{background:linear-gradient(135deg,var(--accent),var(--accent-dark));color:#000;border-color:var(--accent);font-weight:700}

.btn{padding:7px 16px;border:none;border-radius:var(--radius-sm);cursor:pointer;font-size:11px;font-weight:600;transition:var(--transition);display:inline-flex;align-items:center;gap:6px;font-family:inherit;text-decoration:none}
.btn-primary{background:linear-gradient(135deg,var(--accent),#00a8cc);color:#000;box-shadow:0 3px 12px var(--accent-glow)}
.btn-primary:hover{transform:translateY(-1px);box-shadow:0 6px 20px var(--accent-glow)}
.btn-success{background:linear-gradient(135deg,var(--green),#00cc6a);color:#000}
.btn-danger{background:linear-gradient(135deg,var(--red),#cc0033);color:#fff}
.btn-warning{background:linear-gradient(135deg,var(--orange),#cc6600);color:#fff}
.btn-ghost{background:var(--bg-glass);color:var(--text-secondary);border:1px solid var(--border)}
.btn-ghost:hover{background:var(--bg-card-hover);color:var(--text-primary)}
.btn-sm{padding:4px 10px;font-size:9px}.btn-lg{padding:10px 20px;font-size:12px}.btn-block{width:100%;justify-content:center}

.input{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius-sm);padding:8px 12px;color:var(--text-primary);font-size:11px;width:100%;transition:var(--transition);font-family:inherit}
.input:focus{outline:none;border-color:var(--accent);box-shadow:0 0 16px var(--accent-glow)}
.textarea{background:var(--bg-card);border:1px solid var(--border);border-radius:var(--radius-sm);padding:8px 12px;color:var(--text-primary);font-size:11px;width:100%;resize:vertical;transition:var(--transition);font-family:inherit;min-height:60px}
.textarea:focus{outline:none;border-color:var(--accent)}
select.input{appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' fill='%238888aa'%3E%3Cpath d='M6 8L1 3h10z'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 12px center;padding-right:32px}
.input-group{margin-bottom:10px}.input-group label{display:block;font-size:10px;color:var(--text-secondary);margin-bottom:4px;font-weight:500}

.modal-overlay{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.7);backdrop-filter:blur(12px);z-index:1000;display:none;align-items:center;justify-content:center}
.modal-overlay.show{display:flex}
.modal{background:var(--bg-card);border:1px solid var(--border-light);border-radius:var(--radius-lg);padding:24px;max-width:560px;width:92%;max-height:85vh;overflow-y:auto;box-shadow:0 24px 80px rgba(0,0,0,0.6);animation:scaleIn 0.3s cubic-bezier(0.34,1.56,0.64,1);backdrop-filter:blur(24px)}
@keyframes scaleIn{from{opacity:0;transform:scale(0.88)}to{opacity:1;transform:scale(1)}}
.modal h3{font-size:16px;font-weight:700;margin-bottom:14px}

.toast{position:fixed;bottom:24px;right:24px;background:var(--bg-card);border:1px solid var(--border-light);color:var(--text-primary);padding:12px 18px;border-radius:var(--radius-md);font-size:11px;font-weight:500;z-index:2000;opacity:0;transform:translateY(16px) scale(0.95);transition:var(--transition-bounce);pointer-events:none;backdrop-filter:blur(24px);box-shadow:0 8px 32px rgba(0,0,0,0.4);display:flex;align-items:center;gap:8px}
.toast.show{opacity:1;transform:translateY(0) scale(1);pointer-events:auto}

.empty-state{text-align:center;padding:50px 20px;color:var(--text-muted)}
.empty-state .empty-icon{font-size:40px;margin-bottom:12px;opacity:0.4}
.empty-state .empty-title{font-size:14px;font-weight:700;color:var(--text-secondary);margin-bottom:4px}
.empty-state .empty-desc{font-size:11px}

.flex{display:flex;gap:8px;align-items:center}.flex-wrap{flex-wrap:wrap}.flex-col{flex-direction:column}
.gap-4{gap:4px}.mb-4{margin-bottom:4px}.mb-6{margin-bottom:6px}.mb-8{margin-bottom:8px}.mt-6{margin-top:6px}.mt-8{margin-top:8px}.text-center{text-align:center}.text-muted{color:var(--text-muted)}.font-sm{font-size:10px}.fw-700{font-weight:700}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:10px}.grid-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px}
.table{width:100%;border-collapse:collapse;font-size:10px}
.table th,.table td{padding:6px 8px;text-align:left;border-bottom:1px solid var(--border)}
.table th{color:var(--text-muted);font-weight:600;font-size:9px;text-transform:uppercase}
.source-item{display:flex;align-items:center;gap:8px;padding:6px 8px;border-radius:var(--radius-sm);font-size:10px;transition:var(--transition);justify-content:space-between}
.source-item:hover{background:var(--bg-glass)}

@media(max-width:768px){
  .layout{grid-template-columns:1fr}
  .sidebar{position:fixed;bottom:0;top:auto;height:auto;flex-direction:row;overflow-x:auto;border-top:1px solid var(--border);border-right:none;width:100%;backdrop-filter:blur(24px);background:rgba(10,10,15,0.94);z-index:100}
  .sidebar .sidebar-inner{flex-direction:row;padding:4px 6px;overflow-x:auto;gap:1px;width:100%;height:100%}
  .sidebar .logo-wrap,.sidebar .sidebar-footer,.sidebar .sidebar-toggle{display:none}
  .sidebar .nav-item{white-space:nowrap;flex-shrink:0;padding:6px 8px;font-size:10px;justify-content:center;min-width:44px}
  .sidebar .nav-item .nav-label{display:none}
  .sidebar .nav-item.active .nav-slider{display:none}
  .sidebar.collapsed{width:100%}.sidebar.collapsed:hover{width:100%}
  .main{padding:12px;padding-bottom:60px;margin-left:0}
  .sidebar.collapsed ~ .main{margin-left:0}
  .stats-grid,.grid-2,.grid-3{grid-template-columns:repeat(2,1fr)}
}
@media(max-width:480px){.stats-grid,.grid-2,.grid-3{grid-template-columns:1fr}}
</style>
</head>
<body>

<div class="layout">
  <nav class="sidebar" id="sidebar">
    <div class="sidebar-toggle" id="sidebarToggle">◀</div>
    <div class="sidebar-inner">
      <div class="logo-wrap"><div class="logo-icon-bg">⟡</div><span class="logo-text"><span class="accent">NEXUS</span><span class="dim">INTEL</span></span></div>
      <div class="nav-item active" data-page="dashboard"><span class="nav-slider"></span><span class="nav-icon">📊</span><span class="nav-label">Dashboard</span></div>
      <div class="nav-item" data-page="scan"><span class="nav-slider"></span><span class="nav-icon">📡</span><span class="nav-label">Scan RSS</span></div>
      <div class="nav-item" data-page="articles"><span class="nav-slider"></span><span class="nav-icon">📰</span><span class="nav-label">Articles</span></div>
      <div class="nav-item" data-page="synthese"><span class="nav-slider"></span><span class="nav-icon">📋</span><span class="nav-label">Synthèse</span></div>
      <div class="nav-item" data-page="sources"><span class="nav-slider"></span><span class="nav-icon">🌐</span><span class="nav-label">Sources</span></div>
      <div class="nav-item" data-page="config"><span class="nav-slider"></span><span class="nav-icon">⚙️</span><span class="nav-label">Config</span></div>
      <div class="nav-item" data-page="themes"><span class="nav-slider"></span><span class="nav-icon">🎨</span><span class="nav-label">Thèmes</span></div>
      <div class="sidebar-footer"><div class="version-badge">v4.0 CELLULE</div><div class="sidebar-footer-text">NEXUS RENSEIGNEMENT</div></div>
    </div>
  </nav>
  <main class="main" id="mainContent"></main>
</div>

<div class="modal-overlay" id="modalOverlay"><div class="modal" id="modalContent"></div></div>
<div class="toast" id="toast"><span id="toastIcon">⟡</span><span id="toastMsg">Message</span></div>

<script>
// ============================================================
// NEXUS INTELLIGENCE v4.0 — COMPLET & FONCTIONNEL
// ============================================================
const CONFIG = {
  scanInterval: 600000,
  maxArticles: 5000
}

const STATE = {
  articles: [],
  scanned: 0,
  lastScan: null,
  sources: [
    // NATIONAL = CÔTE D'IVOIRE UNIQUEMENT
    {name:"Abidjan.net",url:"https://news.abidjan.net/rss/",region:"national",cat:"general"},
    {name:"Fraternité Matin",url:"https://www.fratmat.info/actualite/rss.xml",region:"national",cat:"general"},
    {name:"Le Point Sur",url:"https://www.lepointsur.com/feed/",region:"national",cat:"general"},
    {name:"Soir Info",url:"https://www.soirinfo.com/feed/",region:"national",cat:"general"},
    {name:"7Info",url:"https://7info.ci/feed/",region:"national",cat:"general"},
    {name:"Linfodrome",url:"https://www.linfodrome.com/feed",region:"national",cat:"general"},
    {name:"Connection Ivoirienne",url:"https://www.connectionivoirienne.net/feed/",region:"national",cat:"general"},
    {name:"Pressecotedivoire",url:"https://www.pressecotedivoire.com/feed/",region:"national",cat:"general"},
    {name:"Koaci",url:"https://www.koaci.com/feed/",region:"national",cat:"general"},
    {name:"AllAfrica CI",url:"https://allafrica.com/tools/headlines/rss/cotedivoire/latest.xml",region:"national",cat:"general"},
    {name:"L'Intelligent d'Abidjan",url:"https://www.lintelligentdabidjan.com/feed/",region:"national",cat:"general"},
    {name:"L'Expression CI",url:"https://www.lexpressionci.com/feed/",region:"national",cat:"general"},
    {name:"Le Patriote",url:"https://www.lepatriote.net/feed/",region:"national",cat:"general"},
    {name:"Gouv CI",url:"https://www.gouv.ci/rss.xml",region:"national",cat:"gouv"},
    {name:"Portail CI",url:"https://www.portail-ci.com/feed/",region:"national",cat:"general"},
    {name:"Cote d'Ivoire Infos",url:"https://www.cotedivoireinfos.com/feed/",region:"national",cat:"general"},
    // CONTINENTAL = AFRIQUE
    {name:"Jeune Afrique",url:"https://www.jeuneafrique.com/feed/",region:"continental",cat:"economie"},
    {name:"RFI Afrique",url:"https://www.rfi.fr/fr/afrique/rss",region:"continental",cat:"general"},
    {name:"BBC Africa",url:"https://feeds.bbci.co.uk/news/world/africa/rss.xml",region:"continental",cat:"general"},
    {name:"Le Monde Afrique",url:"https://www.lemonde.fr/afrique/rss_full.xml",region:"continental",cat:"general"},
    {name:"Africa News",url:"https://www.africanews.com/feed/",region:"continental",cat:"general"},
    {name:"APA News",url:"https://www.apanews.net/feed/",region:"continental",cat:"general"},
    {name:"Africanews Sécurité",url:"https://www.africanews.com/feed/security/",region:"continental",cat:"securite"},
    {name:"WHO Africa",url:"https://www.afro.who.int/rss-feeds",region:"continental",cat:"sante"},
    {name:"Global Voices Africa",url:"https://globalvoices.org/region/africa/feed/",region:"continental",cat:"general"},
    {name:"Africa Intelligence",url:"https://www.africaintelligence.com/feeds/rss/politics",region:"continental",cat:"securite"},
    // INTERNATIONAL
    {name:"France24",url:"https://www.france24.com/fr/rss",region:"international",cat:"general"},
    {name:"The Guardian Africa",url:"https://www.theguardian.com/world/africa/rss",region:"international",cat:"general"},
    {name:"Reuters Africa",url:"https://www.reuters.com/places/africa/rss",region:"international",cat:"economie"},
    {name:"Al Jazeera",url:"https://www.aljazeera.com/xml/rss/all.xml",region:"international",cat:"general"},
    {name:"CNN Africa",url:"http://rss.cnn.com/rss/edition_africa.rss",region:"international",cat:"general"},
    {name:"Le Monde International",url:"https://www.lemonde.fr/international/rss_full.xml",region:"international",cat:"general"}
  ],
  keywords: {
    critique: ["alerte","attentat","cyberattaque","faille","0-day","vulnérabilité","crise","incident","attaque","danger","mort","guerre","conflit","émeute","coup d'état","urgence","exploit","massacre"],
    haute: ["piratage","intrusion","malware","ransomware","espionnage","fuite","sanction","menace","manifestation","grève","crash","accident","grave","violence"],
    moyenne: ["arnaque","phishing","ddos","darkweb","tribunal","enquête","fraude","escroquerie","corruption","détournement","procès"]
  },
  auth: {
    connected: false,
    user: null,
    users: [
      {id:1,login:"nexus",pass:"intel2025",nom:"Admin NEXUS",role:"Directeur"}
    ]
  },
  telegramConfig: {botToken:"",chatId:"",active:false,messages:[]},
  theme: "dark",
  accentColor: "#00d4ff",
  fontSize: "14px"
}

let currentPage = 'dashboard', searchQuery = '', sidebarCollapsed = false, scanning = false

// ===== FONCTIONS UTILITAIRES =====
function escHtml(s){if(typeof s!=='string')return'';return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;')}
function formatDate(d){if(!d)return'';try{return new Date(d).toLocaleDateString('fr-FR',{day:'numeric',month:'short',year:'numeric',hour:'2-digit',minute:'2-digit'})}catch(e){return d}}
function getDate24hAgo(){const d=new Date();d.setHours(d.getHours()-24);return d}
function getArticles24h(){return STATE.articles.filter(a=>new Date(a.date)>getDate24hAgo())}
function getAllSources(){return STATE.sources||[]}
function getRegionEmoji(r){return r==='national'?'🇨🇮':r==='continental'?'🌍':'🌐'}
function getRegionLabel(r){return r==='national'?'Côte d\'Ivoire':r==='continental'?'Afrique':'Monde'}

function showToast(msg,type){
  const t=document.getElementById('toast'),icon=document.getElementById('toastIcon'),txt=document.getElementById('toastMsg')
  const icons={success:'✅',error:'❌',info:'⟡',warning:'⚠️',scan:'📡'}
  icon.textContent=icons[type]||'⟡';txt.textContent=msg
  t.className='toast show';clearTimeout(t._timeout)
  t._timeout=setTimeout(()=>t.classList.remove('show'),3200)
}

function openModal(title,content){
  const overlay=document.getElementById('modalOverlay')
  document.getElementById('modalContent').innerHTML=`<div style="display:flex;justify-content:space-between;align-items:start;margin-bottom:14px"><h3>${title}</h3><button class="btn btn-ghost btn-sm" onclick="closeModal()" style="font-size:16px">✕</button></div>${content}`
  overlay.classList.add('show')
  overlay.onclick=function(e){if(e.target===this)closeModal()}
}

function closeModal(){document.getElementById('modalOverlay').classList.remove('show')}

function toggleSidebar(){
  sidebarCollapsed=!sidebarCollapsed
  document.getElementById('sidebar').classList.toggle('collapsed',sidebarCollapsed)
  localStorage.setItem('nexus-intel-sidebar',sidebarCollapsed?'collapsed':'')
}

function reRenderCurrent(){showPage(currentPage)}

// ===== AUTH =====
function checkAuth(){
  if(STATE.auth.connected) return true
  openModal('🔐 Connexion Admin',`
    <div class="input-group"><label>Identifiant</label><input class="input" id="authLogin" placeholder="login" value="nexus"></div>
    <div class="input-group"><label>Mot de passe</label><input class="input" id="authPass" type="password" placeholder="••••••" value="intel2025"></div>
    <button class="btn btn-primary btn-block mt-6" onclick="login()">🔐 Se connecter</button>
    <div style="font-size:9px;color:var(--text-muted);text-align:center;margin-top:8px">Identifiants: nexus / intel2025</div>
  `)
  return false
}

function login(){
  const l=document.getElementById('authLogin')?.value.trim()
  const p=document.getElementById('authPass')?.value.trim()
  const user=STATE.auth.users.find(u=>u.login===l&&u.pass===p)
  if(user){
    STATE.auth.connected=true
    STATE.auth.user=user
    saveState()
    closeModal()
    showToast(`✅ Bienvenue ${user.nom}`,'success')
    reRenderCurrent()
  } else {
    showToast('❌ Identifiants incorrects','error')
  }
}

function logout(){
  STATE.auth.connected=false
  STATE.auth.user=null
  saveState()
  showToast('🔌 Déconnecté','info')
  reRenderCurrent()
}

// ===== CLASSIFICATION =====
function classifyArticle(title,desc){
  const text=((title||'')+' '+(desc||'')).toLowerCase()
  const kw=STATE.keywords
  for(const k of kw.critique) if(text.includes(k)) return 'critique'
  for(const k of kw.haute) if(text.includes(k)) return 'haute'
  for(const k of kw.moyenne) if(text.includes(k)) return 'moyenne'
  return 'info'
}

// ===== NAVIGATION =====
function showPage(page){
  currentPage=page
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'))
  const el=document.querySelector(`.nav-item[data-page="${page}"]`)
  if(el) el.classList.add('active')

  switch(page){
    case'dashboard': renderDashboard(); break
    case'scan': renderScan(); break
    case'articles': renderArticles(); break
    case'synthese': renderSynthese(); break
    case'sources': renderSources(); break
    case'config': renderConfig(); break
    case'themes': renderThemes(); break
    default: renderDashboard()
  }
}

// ===== DASHBOARD =====
function renderDashboard(){
  if(!checkAuth()) return
  const app=document.getElementById('mainContent')
  const arts=STATE.articles
  const arts24h=getArticles24h()
  const crit=arts24h.filter(a=>a.level==='critique')
  const haut=arts24h.filter(a=>a.level==='haute')
  const nat=arts24h.filter(a=>a.region==='national').length
  const cont=arts24h.filter(a=>a.region==='continental').length
  const intl=arts24h.filter(a=>a.region==='international').length
  const lCrit=arts24h.filter(a=>a.level==='critique').length
  const lHaut=arts24h.filter(a=>a.level==='haute').length
  const lMoy=arts24h.filter(a=>a.level==='moyenne').length
  const lInfo=arts24h.filter(a=>a.level==='info').length

  app.innerHTML=`
    <div class="topbar">
      <div class="topbar-left"><h1>📊 Dashboard</h1><span class="font-sm text-muted">${escHtml(STATE.auth.user?.nom)}</span></div>
      <div class="topbar-right">
        <span style="font-size:9px;color:var(--text-muted)">👤 ${escHtml(STATE.auth.user?.nom)}</span>
        <button class="btn btn-ghost btn-sm" onclick="logout()">🔌 Déconnexion</button>
        <button class="btn btn-primary btn-sm" onclick="scanAllRSS()">📡 Scan</button>
      </div>
    </div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-value" style="color:var(--accent)">${arts.length}</div><div class="stat-label">Total Articles</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--green)">${arts24h.length}</div><div class="stat-label">24h</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--red)">${crit.length}</div><div class="stat-label">Critiques</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--orange)">${haut.length}</div><div class="stat-label">Hautes</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--gold)">${nat}</div><div class="stat-label">🇨🇮 National</div></div>
    </div>
    <div class="grid-2">
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:6px">📋 Brief 24h</h3>
        <div style="font-size:9px;line-height:1.7">
          <strong>${arts24h.length} articles</strong> · 🔴${lCrit} 🟠${lHaut} 🟡${lMoy} 🔵${lInfo}<br>
          🇨🇮 ${nat} CI · 🌍 ${cont} Afrique · 🌐 ${intl} Monde<br>
          Dernier scan: ${STATE.lastScan?formatDate(STATE.lastScan):'Jamais'}
        </div>
      </div>
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:6px">🌐 Sources</h3>
        <div style="font-size:9px;line-height:1.7">
          ${getAllSources().length} sources actives<br>
          <button class="btn btn-primary btn-sm mt-6" onclick="showPage('sources')">⚙️ Gérer les sources</button>
        </div>
      </div>
    </div>
    ${crit.length?`
    <div class="card mt-6" style="border-left:3px solid var(--red)">
      <h3 style="font-size:11px;color:var(--red);margin-bottom:6px">🚨 Alertes critiques (${crit.length})</h3>
      ${crit.slice(0,5).map(a=>`
        <div style="font-size:8px;padding:2px 0">${getRegionEmoji(a.region)} <strong>${escHtml(a.title)}</strong> — ${escHtml(a.source)}</div>
      `).join('')}
    </div>`:''}
  `
}

// ===== SCAN RSS =====
function renderScan(){
  const app=document.getElementById('mainContent')
  const src=getAllSources()
  const nat=src.filter(s=>s.region==='national').length
  const cont=src.filter(s=>s.region==='continental').length
  const intl=src.filter(s=>s.region==='international').length

  app.innerHTML=`
    <div class="topbar">
      <div class="topbar-left"><h1>📡 Scan RSS</h1><span class="font-sm text-muted">${src.length} sources · ${STATE.articles.length} articles</span></div>
      <div class="topbar-right">
        <button class="btn btn-primary btn-sm" onclick="scanAllRSS()">🔄 Lancer le scan</button>
      </div>
    </div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-value" style="color:var(--accent)">${src.length}</div><div class="stat-label">Sources</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--green)">${nat}</div><div class="stat-label">🇨🇮 CI</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--orange)">${cont}</div><div class="stat-label">🌍 Afrique</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--purple)">${intl}</div><div class="stat-label">🌐 Monde</div></div>
    </div>
    <button class="btn btn-primary btn-lg btn-block" onclick="scanAllRSS()">📡 LANCER LE SCAN (${src.length} sources)</button>
    <div id="scanLog" class="card mt-6" style="font-size:8px;line-height:1.8;max-height:300px;overflow-y:auto;font-family:monospace">
      <div style="color:var(--text-muted)">Prêt... Cliquez sur "Lancer le scan"</div>
    </div>
  `
}

async function scanAllRSS(){
  if(scanning) return showToast('Scan déjà en cours','warning')
  scanning=true
  const sources=getAllSources()
  const log=document.getElementById('scanLog')
  if(log) log.innerHTML='<div style="color:var(--accent)">📡 Scan en cours...</div>'
  let total=0

  for(const s of sources){
    try{
      const proxyUrl=`https://api.allorigins.win/raw?url=${encodeURIComponent(s.url)}`
      const resp=await fetch(proxyUrl,{signal:AbortSignal.timeout(12000)})
      if(!resp.ok) throw new Error(`HTTP ${resp.status}`)
      const text=await resp.text()
      const parser=new DOMParser()
      const xml=parser.parseFromString(text,'text/xml')
      const items=Array.from(xml.querySelectorAll('item')||[])
      let count=0

      for(const item of items.slice(0,20)){
        const title=item.querySelector('title')?.textContent?.trim()
        const desc=item.querySelector('description')?.textContent?.trim()
        const link=item.querySelector('link')?.textContent?.trim()
        const dateStr=item.querySelector('pubDate')?.textContent?.trim()
        if(!title) continue
        if(STATE.articles.find(a=>a.title===title&&a.source===s.name)) continue

        STATE.articles=[{
          id:Date.now().toString(36)+Math.random().toString(36).substr(2,4),
          title,desc:desc||'',link:link||'',source:s.name,
          region:s.region,cat:s.cat||'general',
          date:dateStr?new Date(dateStr).toISOString():new Date().toISOString(),
          level:classifyArticle(title,desc),read:false
        },...STATE.articles].slice(0,CONFIG.maxArticles)
        count++
      }
      if(count>0) total+=count
      if(log) log.innerHTML+=`<div style="color:var(--green)">✅ ${escHtml(s.name)} — ${count} nouveaux</div>`
    }catch(e){
      if(log) log.innerHTML+=`<div style="color:var(--red)">❌ ${escHtml(s.name)} — ${e.message}</div>`
    }
  }

  STATE.scanned=sources.length
  STATE.lastScan=new Date().toISOString()
  scanning=false
  saveState()
  if(log) log.innerHTML+=`<div style="color:var(--accent);font-weight:700;margin-top:4px;border-top:1px solid var(--border);padding-top:4px">✅ Scan terminé — ${total} nouveaux articles sur ${sources.length} sources</div>`
  showToast(`📡 Scan: ${total} nouveaux articles`,'scan')
}

// ===== ARTICLES =====
function renderArticles(){
  if(!checkAuth()) return
  const app=document.getElementById('mainContent')
  let arts=STATE.articles
  const filter=document.getElementById('artFilter')?.value||'all'
  if(filter==='unread') arts=arts.filter(a=>!a.read)
  else if(filter==='critique') arts=arts.filter(a=>a.level==='critique')

  app.innerHTML=`
    <div class="topbar">
      <div class="topbar-left"><h1>📰 Articles</h1><span class="font-sm text-muted">${arts.length} affichés / ${STATE.articles.length} total</span></div>
      <div class="topbar-right">
        <select class="input" id="artFilter" style="font-size:10px;max-width:130px" onchange="renderArticles()">
          <option value="all" ${filter==='all'?'selected':''}>📋 Tous</option>
          <option value="unread" ${filter==='unread'?'selected':''}>🆕 Non lus</option>
          <option value="critique" ${filter==='critique'?'selected':''}>🔴 Critiques</option>
        </select>
        <button class="btn btn-ghost btn-sm" onclick="STATE.articles.forEach(a=>a.read=true);saveState();renderArticles();showToast('✅ Tout marqué lu','success')">✅ Tout lu</button>
      </div>
    </div>
    <div style="display:flex;flex-direction:column;gap:4px">
      ${arts.length?arts.slice(0,200).map(a=>`
        <div class="card" style="padding:8px;cursor:pointer;${a.read?'opacity:.6':''}" onclick="openArticle('${a.id}')">
          <div style="display:flex;justify-content:space-between;align-items:start;gap:6px">
            <div style="flex:1;min-width:0">
              <div style="font-size:10px;font-weight:600">${getRegionEmoji(a.region)} ${escHtml(a.title)}</div>
              <div style="font-size:7px;color:var(--text-muted);margin-top:2px">${escHtml(a.source)} · ${formatDate(a.date)}</div>
            </div>
            <span style="background:${a.level==='critique'?'var(--red)':a.level==='haute'?'var(--orange)':a.level==='moyenne'?'#ffcc00':'var(--accent)'};color:${a.level==='moyenne'||a.level==='info'?'#000':'#fff'};padding:1px 6px;border-radius:3px;font-size:6px;font-weight:700;flex-shrink:0">${a.level}</span>
          </div>
        </div>`).join(''):`<div class="empty-state"><div class="empty-icon">📰</div><div class="empty-title">Aucun article</div><div class="empty-desc">Lancez un scan RSS pour obtenir des articles.</div></div>`}
    </div>`
}

function openArticle(id){
  const a=STATE.articles.find(x=>x.id===id)
  if(!a) return
  a.read=true
  saveState()
  renderArticles()

  openModal(`📰 Article`,`
    <div class="flex flex-wrap" style="font-size:8px;color:var(--text-muted);margin-bottom:6px;gap:4px">
      ${getRegionEmoji(a.region)} ${getRegionLabel(a.region)} · ${escHtml(a.source)} · ${formatDate(a.date)}
      <span style="background:${a.level==='critique'?'var(--red)':a.level==='haute'?'var(--orange)':a.level==='moyenne'?'#ffcc00':'var(--accent)'};color:#000;padding:1px 6px;border-radius:3px;font-size:6px;font-weight:700">${a.level}</span>
    </div>
    <h3 style="font-size:13px;margin-bottom:8px">${escHtml(a.title)}</h3>
    <div style="font-size:10px;line-height:1.6;color:var(--text-secondary)">${escHtml(a.desc||'Pas de description disponible.')}</div>
    ${a.link?`
    <hr style="border-color:var(--border);margin:12px 0">
    <a href="${a.link}" target="_blank" class="btn btn-primary btn-sm" style="text-decoration:none">🔗 Lire l'article original</a>`:''}
  `)
}

// ===== SYNTHÈSE 24h =====
function renderSynthese(){
  if(!checkAuth()) return
  const app=document.getElementById('mainContent')
  const a=getArticles24h()
  const crit=a.filter(x=>x.level==='critique')
  const haut=a.filter(x=>x.level==='haute')
  const nat=a.filter(x=>x.region==='national')
  const cont=a.filter(x=>x.region==='continental')
  const intl=a.filter(x=>x.region==='international')

  app.innerHTML=`
    <div class="topbar">
      <div class="topbar-left"><h1>📋 Synthèse 24h</h1><span class="font-sm text-muted">${new Date().toLocaleDateString('fr-FR',{weekday:'long',day:'numeric',month:'long',year:'numeric'})}</span></div>
    </div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-value" style="color:var(--accent)">${a.length}</div><div class="stat-label">Articles 24h</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--red)">${crit.length}</div><div class="stat-label">Critiques</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--orange)">${haut.length}</div><div class="stat-label">Hautes</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--green)">${nat.length}</div><div class="stat-label">🇨🇮 CI</div></div>
    </div>
    <div class="grid-3">
      <div class="card"><h3 style="font-size:10px;margin-bottom:4px;color:var(--green)">🇨🇮 Côte d'Ivoire (${nat.length})</h3>${nat.slice(0,8).map(x=>`<div style="font-size:7px;padding:1px 0;display:flex;gap:4px"><span style="background:${x.level==='critique'?'var(--red)':x.level==='haute'?'var(--orange)':x.level==='moyenne'?'#ffcc00':'var(--accent)'};color:#000;padding:0 4px;border-radius:2px;font-size:6px;font-weight:700">${x.level[0]}</span><span>${escHtml(x.title)}</span></div>`).join('')||'<span style="color:var(--text-muted);font-size:8px">Aucun</span>'}</div>
      <div class="card"><h3 style="font-size:10px;margin-bottom:4px;color:var(--orange)">🌍 Afrique (${cont.length})</h3>${cont.slice(0,8).map(x=>`<div style="font-size:7px;padding:1px 0;display:flex;gap:4px"><span style="background:${x.level==='critique'?'var(--red)':x.level==='haute'?'var(--orange)':x.level==='moyenne'?'#ffcc00':'var(--accent)'};color:#000;padding:0 4px;border-radius:2px;font-size:6px;font-weight:700">${x.level[0]}</span><span>${escHtml(x.title)}</span></div>`).join('')||'<span style="color:var(--text-muted);font-size:8px">Aucun</span>'}</div>
      <div class="card"><h3 style="font-size:10px;margin-bottom:4px;color:var(--purple)">🌐 Monde (${intl.length})</h3>${intl.slice(0,8).map(x=>`<div style="font-size:7px;padding:1px 0;display:flex;gap:4px"><span style="background:${x.level==='critique'?'var(--red)':x.level==='haute'?'var(--orange)':x.level==='moyenne'?'#ffcc00':'var(--accent)'};color:#000;padding:0 4px;border-radius:2px;font-size:6px;font-weight:700">${x.level[0]}</span><span>${escHtml(x.title)}</span></div>`).join('')||'<span style="color:var(--text-muted);font-size:8px">Aucun</span>'}</div>
    </div>
    ${crit.length?`
    <div class="card mt-6" style="border-left:3px solid var(--red)">
      <h3 style="font-size:10px;color:var(--red);margin-bottom:4px">🚨 ALERTES CRITIQUES (${crit.length})</h3>
      ${crit.map(x=>`<div style="font-size:8px;padding:2px 0">${getRegionEmoji(x.region)} <strong>${escHtml(x.title)}</strong> — ${escHtml(x.source)}</div>`).join('')}
    </div>`:''}
  `
}

// ===== SOURCES (MODIFIABLES) =====
function renderSources(){
  if(!checkAuth()) return
  const app=document.getElementById('mainContent')
  const src=getAllSources()
  const nat=src.filter(s=>s.region==='national')
  const cont=src.filter(s=>s.region==='continental')
  const intl=src.filter(s=>s.region==='international')

  app.innerHTML=`
    <div class="topbar">
      <div class="topbar-left"><h1>🌐 Gestion des sources</h1><span class="font-sm text-muted">${src.length} sources</span></div>
    </div>
    <div class="card mb-6">
      <h3 style="font-size:11px;margin-bottom:6px">➕ Ajouter une nouvelle source RSS</h3>
      <div class="flex flex-wrap" style="gap:4px">
        <input class="input" id="newSrcName" placeholder="Nom de la source" style="max-width:140px;font-size:10px">
        <input class="input" id="newSrcUrl" placeholder="URL du flux RSS" style="flex:1;font-size:10px">
        <select class="input" id="newSrcRegion" style="max-width:130px;font-size:10px">
          <option value="national">🇨🇮 Côte d'Ivoire</option>
          <option value="continental">🌍 Afrique</option>
          <option value="international">🌐 International</option>
        </select>
        <select class="input" id="newSrcCat" style="max-width:100px;font-size:10px">
          <option value="general">Général</option><option value="securite">Sécurité</option>
          <option value="economie">Économie</option><option value="gouv">Gouvernement</option><option value="sante">Santé</option>
        </select>
        <button class="btn btn-primary btn-sm" onclick="addSource()">➕ Ajouter</button>
      </div>
    </div>
    <div class="grid-3">
      <div class="card"><h3 style="font-size:10px;margin-bottom:4px">🇨🇮 Côte d'Ivoire (${nat.length})</h3>${nat.map((s,i)=>`<div class="source-item"><span style="flex:1;min-width:0"><strong>${escHtml(s.name)}</strong><br><span style="color:var(--text-muted);font-size:7px;word-break:break-all">${escHtml(s.url)}</span></span><div class="flex gap-4"><button class="btn btn-primary btn-sm" onclick="editSource('national',${i})">✏️</button><button class="btn btn-danger btn-sm" onclick="deleteSource(\\'${s.name}\\',\\'national\\')">✕</button></div></div>`).join('')||'<span style="color:var(--text-muted);font-size:9px">Aucune source</span>'}</div>
      <div class="card"><h3 style="font-size:10px;margin-bottom:4px">🌍 Afrique (${cont.length})</h3>${cont.map((s,i)=>`<div class="source-item"><span style="flex:1;min-width:0"><strong>${escHtml(s.name)}</strong><br><span style="color:var(--text-muted);font-size:7px;word-break:break-all">${escHtml(s.url)}</span></span><div class="flex gap-4"><button class="btn btn-primary btn-sm" onclick="editSource('continental',${i})">✏️</button><button class="btn btn-danger btn-sm" onclick="deleteSource(\\'${s.name}\\',\\'continental\\')">✕</button></div></div>`).join('')||'<span style="color:var(--text-muted);font-size:9px">Aucune source</span>'}</div>
      <div class="card"><h3 style="font-size:10px;margin-bottom:4px">🌐 International (${intl.length})</h3>${intl.map((s,i)=>`<div class="source-item"><span style="flex:1;min-width:0"><strong>${escHtml(s.name)}</strong><br><span style="color:var(--text-muted);font-size:7px;word-break:break-all">${escHtml(s.url)}</span></span><div class="flex gap-4"><button class="btn btn-primary btn-sm" onclick="editSource('international',${i})">✏️</button><button class="btn btn-danger btn-sm" onclick="deleteSource(\\'${s.name}\\',\\'international\\')">✕</button></div></div>`).join('')||'<span style="color:var(--text-muted);font-size:9px">Aucune source</span>'}</div>
    </div>`
}

function addSource(){
  const n=document.getElementById('newSrcName')?.value.trim()
  const u=document.getElementById('newSrcUrl')?.value.trim()
  const r=document.getElementById('newSrcRegion')?.value
  const c=document.getElementById('newSrcCat')?.value
  if(!n||!u) return showToast('❌ Nom et URL requis','error')
  if(!STATE.sources) STATE.sources=[]
  STATE.sources.push({name:n,url:u,region:r,cat:c})
  saveState()
  renderSources()
  showToast(`✅ Source "${n}" ajoutée`,'success')
}

function deleteSource(name,region){
  if(!confirm(`Supprimer "${name}" ?`)) return
  STATE.sources=STATE.sources.filter(s=>!(s.name===name&&s.region===region))
  saveState()
  renderSources()
  showToast('🗑️ Source supprimée','info')
}

function editSource(region,idx){
  const all=STATE.sources.filter(s=>s.region===region)
  const s=all[idx]
  if(!s) return

  const regionLabels={national:'🇨🇮 Côte d\'Ivoire',continental:'🌍 Afrique',international:'🌐 Monde'}
  const regionOptions=Object.entries(regionLabels).map(([val,label])=>
    `<option value="${val}" ${s.region===val?'selected':''}>${label}</option>`
  ).join('')

  const catOptions=['general','securite','economie','gouv','sante'].map(c=>
    `<option value="${c}" ${s.cat===c?'selected':''}>${c}</option>`
  ).join('')

  openModal(`✏️ Modifier : ${escHtml(s.name)}`,`
    <div class="input-group"><label>Nom</label><input class="input" id="esName" value="${escHtml(s.name)}"></div>
    <div class="input-group"><label>URL RSS</label><input class="input" id="esUrl" value="${escHtml(s.url)}"></div>
    <div class="flex">
      <div class="input-group" style="flex:1"><label>Région</label><select class="input" id="esRegion">${regionOptions}</select></div>
      <div class="input-group" style="flex:1"><label>Catégorie</label><select class="input" id="esCat">${catOptions}</select></div>
    </div>
    <button class="btn btn-primary btn-block mt-6" onclick="saveSourceEdit(\\'${region}\\',${idx})">💾 Sauvegarder</button>
  `)
}

function saveSourceEdit(region,idx){
  const all=STATE.sources.filter(s=>s.region===region)
  const s=all[idx]
  if(!s) return
  s.name=document.getElementById('esName')?.value||s.name
  s.url=document.getElementById('esUrl')?.value||s.url
  s.region=document.getElementById('esRegion')?.value||s.region
  s.cat=document.getElementById('esCat')?.value||s.cat
  saveState()
  closeModal()
  renderSources()
  showToast('✅ Source modifiée','success')
}

// ===== CONFIG (ADMIN + UTILISATEURS) =====
function renderConfig(){
  if(!checkAuth()) return
  const app=document.getElementById('mainContent')

  app.innerHTML=`
    <div class="topbar">
      <div class="topbar-left"><h1>⚙️ Configuration</h1><span class="font-sm text-muted">👤 ${escHtml(STATE.auth.user?.nom)}</span></div>
      <div class="topbar-right">
        <button class="btn btn-ghost btn-sm" onclick="logout()">🔌 Déconnexion</button>
      </div>
    </div>
    <div class="stats-grid">
      <div class="stat-card"><div class="stat-value" style="color:var(--accent)">${STATE.articles.length}</div><div class="stat-label">Articles</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--green)">${getAllSources().length}</div><div class="stat-label">Sources</div></div>
      <div class="stat-card"><div class="stat-value" style="color:var(--purple)">${STATE.auth.users.length}</div><div class="stat-label">Utilisateurs</div></div>
    </div>
    <div class="grid-2">
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:8px">👥 Gestion des utilisateurs</h3>
        <table class="table">
          <thead><tr><th>Login</th><th>Nom</th><th>Rôle</th><th>Actions</th></tr></thead>
          <tbody>${STATE.auth.users.map(u=>`
            <tr>
              <td>${escHtml(u.login)}</td>
              <td>${escHtml(u.nom)}</td>
              <td>${escHtml(u.role)}</td>
              <td>
                <button class="btn btn-primary btn-sm" onclick="editUser(${u.id})">✏️</button>
                <button class="btn btn-danger btn-sm" onclick="deleteUser(${u.id})">🗑️</button>
              </td>
            </tr>`).join('')}
          </tbody>
        </table>
        <button class="btn btn-primary btn-sm btn-block mt-6" onclick="addUser()">➕ Ajouter un utilisateur</button>
      </div>
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:8px">🔐 Administration</h3>
        <div class="input-group"><label>Login admin principal</label><input class="input" id="cfgLogin" value="${escHtml(STATE.auth.users[0]?.login||'nexus')}"></div>
        <div class="input-group"><label>Mot de passe</label><input class="input" id="cfgPass" value="${escHtml(STATE.auth.users[0]?.pass||'intel2025')}"></div>
        <button class="btn btn-primary btn-sm btn-block" onclick="saveAdmin()">💾 Sauvegarder</button>
        <hr style="border-color:var(--border);margin:12px 0">
        <div class="input-group"><label>Intervalle scan auto (ms)</label><input class="input" id="cfgInterval" value="${CONFIG.scanInterval}"></div>
        <div class="input-group"><label>Nombre max d'articles</label><input class="input" id="cfgMax" value="${CONFIG.maxArticles}"></div>
        <button class="btn btn-primary btn-sm btn-block mt-6" onclick="saveScanConfig()">💾 Config scan</button>
        <hr style="border-color:var(--border);margin:12px 0">
        <button class="btn btn-danger btn-sm btn-block" onclick="if(confirm('🗑️ Réinitialiser toutes les données ?')){localStorage.clear();location.reload()}">🗑️ Réinitialiser tout</button>
      </div>
    </div>
    <div class="grid-2 mt-6">
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:6px">🔴 Mots-clés critiques</h3>
        <textarea class="textarea" id="kwCritique" style="height:80px;font-size:9px">${STATE.keywords.critique.join('\n')}</textarea>
        <button class="btn btn-primary btn-sm btn-block mt-6" onclick="saveKW('critique')">💾 Sauvegarder</button>
      </div>
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:6px">🟠 Mots-clés hautes</h3>
        <textarea class="textarea" id="kwHaute" style="height:80px;font-size:9px">${STATE.keywords.haute.join('\n')}</textarea>
        <button class="btn btn-primary btn-sm btn-block mt-6" onclick="saveKW('haute')">💾 Sauvegarder</button>
      </div>
    </div>
    <div class="card mt-6">
      <h3 style="font-size:11px;margin-bottom:6px">🟡 Mots-clés moyennes</h3>
      <textarea class="textarea" id="kwMoyenne" style="height:80px;font-size:9px">${STATE.keywords.moyenne.join('\n')}</textarea>
      <button class="btn btn-primary btn-sm btn-block mt-6" onclick="saveKW('moyenne')">💾 Sauvegarder</button>
    </div>`
}

function saveScanConfig(){
  CONFIG.scanInterval=parseInt(document.getElementById('cfgInterval')?.value)||600000
  CONFIG.maxArticles=parseInt(document.getElementById('cfgMax')?.value)||5000
  saveState()
  showToast('✅ Configuration scan sauvegardée','success')
}

function saveKW(level){
  const el=document.getElementById('kw'+level.charAt(0).toUpperCase()+level.slice(1))
  if(el) STATE.keywords[level]=el.value.split('\n').map(s=>s.trim()).filter(Boolean)
  saveState()
  showToast(`✅ Mots-clés "${level}" sauvegardés`,'success')
}

function saveAdmin(){
  const l=document.getElementById('cfgLogin')?.value.trim()
  const p=document.getElementById('cfgPass')?.value.trim()
  if(l&&p){
    STATE.auth.users[0].login=l
    STATE.auth.users[0].pass=p
    saveState()
    showToast('✅ Admin mis à jour','success')
  } else {
    showToast('❌ Login et mot de passe requis','error')
  }
}

// ===== GESTION UTILISATEURS =====
function addUser(){
  openModal('➕ Ajouter un utilisateur',`
    <div class="input-group"><label>Login</label><input class="input" id="auLogin" placeholder="login"></div>
    <div class="input-group"><label>Mot de passe</label><input class="input" id="auPass" type="password" placeholder="••••••"></div>
    <div class="input-group"><label>Nom complet</label><input class="input" id="auNom" placeholder="Nom Prenom"></div>
    <div class="input-group"><label>Rôle</label><select class="input" id="auRole"><option value="Analyste">Analyste</option><option value="Directeur">Directeur</option><option value="Admin">Admin</option></select></div>
    <button class="btn btn-primary btn-block mt-6" onclick="submitAddUser()">✅ Ajouter</button>
  `)
}

function submitAddUser(){
  const l=document.getElementById('auLogin')?.value.trim()
  const p=document.getElementById('auPass')?.value.trim()
  const n=document.getElementById('auNom')?.value.trim()
  const r=document.getElementById('auRole')?.value
  if(!l||!p||!n) return showToast('❌ Tous les champs sont requis','error')
  if(STATE.auth.users.find(u=>u.login===l)) return showToast('❌ Ce login existe déjà','error')
  STATE.auth.users.push({id:STATE.auth.users.length+1,login:l,pass:p,nom:n,role:r})
  saveState()
  closeModal()
  renderConfig()
  showToast(`✅ Utilisateur "${n}" ajouté`,'success')
}

function editUser(id){
  const u=STATE.auth.users.find(x=>x.id===id)
  if(!u) return
  openModal(`✏️ Modifier : ${escHtml(u.nom)}`,`
    <div class="input-group"><label>Login</label><input class="input" id="euLogin" value="${escHtml(u.login)}"></div>
    <div class="input-group"><label>Mot de passe</label><input class="input" id="euPass" type="password" value="${escHtml(u.pass)}"></div>
    <div class="input-group"><label>Nom</label><input class="input" id="euNom" value="${escHtml(u.nom)}"></div>
    <div class="input-group"><label>Rôle</label><select class="input" id="euRole"><option value="Analyste" ${u.role==='Analyste'?'selected':''}>Analyste</option><option value="Directeur" ${u.role==='Directeur'?'selected':''}>Directeur</option><option value="Admin" ${u.role==='Admin'?'selected':''}>Admin</option></select></div>
    <button class="btn btn-primary btn-block mt-6" onclick="submitEditUser(${id})">💾 Sauvegarder</button>
  `)
}

function submitEditUser(id){
  const u=STATE.auth.users.find(x=>x.id===id)
  if(!u) return
  u.login=document.getElementById('euLogin')?.value||u.login
  u.pass=document.getElementById('euPass')?.value||u.pass
  u.nom=document.getElementById('euNom')?.value||u.nom
  u.role=document.getElementById('euRole')?.value||u.role
  saveState()
  closeModal()
  renderConfig()
  showToast('✅ Utilisateur modifié','success')
}

function deleteUser(id){
  if(STATE.auth.users.length<=1) return showToast('❌ Impossible de supprimer le dernier administrateur','error')
  if(!confirm('Supprimer cet utilisateur ?')) return
  STATE.auth.users=STATE.auth.users.filter(u=>u.id!==id)
  saveState()
  renderConfig()
  showToast('🗑️ Utilisateur supprimé','info')
}

// ===== THEMES =====
function renderThemes(){
  const app=document.getElementById('mainContent')
  app.innerHTML=`
    <div class="topbar"><div class="topbar-left"><h1>🎨 Thèmes & Apparence</h1></div></div>
    <div class="grid-2">
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:8px">🌙 Mode d'affichage</h3>
        <div class="flex" style="gap:10px">
          <button class="btn ${STATE.theme==='dark'?'btn-primary':'btn-ghost'} btn-sm" onclick="setTheme('dark')">🌙 Nuit</button>
          <button class="btn ${STATE.theme==='light'?'btn-primary':'btn-ghost'} btn-sm" onclick="setTheme('light')">☀️ Jour</button>
        </div>
      </div>
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:8px">🎨 Personnalisation</h3>
        <div class="input-group"><label>Couleur d'accent</label>
          <div class="flex" style="gap:6px">
            <button style="width:28px;height:28px;border-radius:50%;border:2px solid ${STATE.accentColor==='#00d4ff'?'var(--accent)':'transparent'};background:#00d4ff;cursor:pointer" onclick="setAccent('#00d4ff')" title="Cyan"></button>
            <button style="width:28px;height:28px;border-radius:50%;border:2px solid ${STATE.accentColor==='#ff6600'?'var(--accent)':'transparent'};background:#ff6600;cursor:pointer" onclick="setAccent('#ff6600')" title="Orange"></button>
            <button style="width:28px;height:28px;border-radius:50%;border:2px solid ${STATE.accentColor==='#7c3aed'?'var(--accent)':'transparent'};background:#7c3aed;cursor:pointer" onclick="setAccent('#7c3aed')" title="Violet"></button>
            <button style="width:28px;height:28px;border-radius:50%;border:2px solid ${STATE.accentColor==='#00ff88'?'var(--accent)':'transparent'};background:#00ff88;cursor:pointer" onclick="setAccent('#00ff88')" title="Vert"></button>
            <button style="width:28px;height:28px;border-radius:50%;border:2px solid ${STATE.accentColor==='#ff2244'?'var(--accent)':'transparent'};background:#ff2244;cursor:pointer" onclick="setAccent('#ff2244')" title="Rouge"></button>
          </div>
        </div>
        <div class="input-group"><label>Taille de police</label>
          <select class="input" style="font-size:10px" onchange="setFontSize(this.value)">
            <option value="12px" ${STATE.fontSize==='12px'?'selected':''}>Petite</option>
            <option value="14px" ${!STATE.fontSize||STATE.fontSize==='14px'?'selected':''}>Normale</option>
            <option value="16px" ${STATE.fontSize==='16px'?'selected':''}>Grande</option>
          </select>
        </div>
      </div>
    </div>
    <div class="card mt-6">
      <h3 style="font-size:11px;margin-bottom:6px">📊 Aperçu</h3>
      <div style="font-size:${STATE.fontSize||'14px'};color:var(--text-primary)">
        <div style="background:var(--bg-card);padding:10px;border-radius:8px;border:1px solid var(--border)">
          <p style="font-weight:600">Texte d'exemple</p>
          <p style="color:var(--text-secondary);font-size:0.9em">Ceci est un texte secondaire.</p>
          <span style="background:var(--accent);color:#000;padding:2px 8px;border-radius:4px;font-size:0.8em;font-weight:700">BADGE ACCENT</span>
        </div>
      </div>
    </div>`
}

function setTheme(t){
  STATE.theme=t
  document.documentElement.setAttribute('data-theme',t)
  saveState()
  renderThemes()
  showToast(`🎨 Mode ${t==='dark'?'Nuit':'Jour'} activé`,'success')
}

function setAccent(c){
  STATE.accentColor=c
  document.documentElement.style.setProperty('--accent',c)
  saveState()
  renderThemes()
  showToast('🎨 Couleur changée','success')
}

function setFontSize(s){
  STATE.fontSize=s
  saveState()
  renderThemes()
  showToast('🔤 Taille mise à jour','success')
}

// ===== STOCKAGE LOCAL =====
function saveState(){
  try{
    localStorage.setItem('nexus-intel-state',JSON.stringify(STATE))
    localStorage.setItem('nexus-intel-config',JSON.stringify(CONFIG))
  }catch(e){}
}

function loadState(){
  try{
    const s=localStorage.getItem('nexus-intel-state')
    if(s){const d=JSON.parse(s);Object.keys(d).forEach(k=>{STATE[k]=d[k]})}
    const c=localStorage.getItem('nexus-intel-config')
    if(c){const d=JSON.parse(c);Object.keys(d).forEach(k=>{if(k in CONFIG)CONFIG[k]=d[k]})}
  }catch(e){}
}

// ===== INITIALISATION =====
function init(){
  loadState()

  const saved=localStorage.getItem('nexus-intel-sidebar')
  if(saved==='collapsed'){sidebarCollapsed=true;document.getElementById('sidebar').classList.add('collapsed')}

  document.getElementById('sidebarToggle').addEventListener('click',toggleSidebar)

  document.querySelectorAll('.nav-item[data-page]').forEach(el=>{
    el.addEventListener('click',()=>showPage(el.dataset.page))
  })

  if(STATE.theme==='light') document.documentElement.setAttribute('data-theme','light')
  if(STATE.accentColor) document.documentElement.style.setProperty('--accent',STATE.accentColor)

  showPage('dashboard')

  if(!STATE.articles.length) setTimeout(scanAllRSS,3000)
  setInterval(saveState,30000)
  console.log('⟡ NEXUS INTELLIGENCE v4.0 chargée avec succès')
}

if(document.readyState==='loading') document.addEventListener('DOMContentLoaded',init)
else init()
</script>
</body>
</html>
