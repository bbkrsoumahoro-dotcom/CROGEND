<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NEXUS INTELLIGENCE — Scan & Synthèse</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{--bg:#0a0a0f;--card:#12121a;--card2:#1a1a28;--text:#e0e0e0;--text2:#888;--accent:#00d4ff;--border:#2a2a3a;--green:#00ff88;--orange:#ff8800;--red:#ff2244}
body{font-family:'Segoe UI',system-ui,sans-serif;background:var(--bg);color:var(--text);min-height:100vh}
.layout{display:grid;grid-template-columns:220px 1fr;min-height:100vh}
.sidebar{background:var(--card);border-right:1px solid var(--border);padding:16px;position:sticky;top:0;height:100vh;overflow-y:auto}
.logo{font-size:16px;font-weight:800;color:var(--accent);margin-bottom:20px;letter-spacing:-.5px}
.logo span{color:var(--text)}
.nav-item{display:flex;align-items:center;gap:8px;padding:8px 12px;border-radius:8px;cursor:pointer;font-size:12px;color:var(--text2);transition:.2s;margin-bottom:2px}
.nav-item:hover,.nav-item.active{background:var(--card2);color:var(--accent)}
.main{padding:20px}
.header{display:flex;justify-content:space-between;align-items:center;margin-bottom:20px}
.header h1{font-size:18px;font-weight:700}
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:8px;margin-bottom:16px}
.stat-card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:12px}
.stat-card .val{font-size:22px;font-weight:700}
.stat-card .lbl{font-size:9px;color:var(--text2);margin-top:2px}
.grid-3{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:8px}
.card{background:var(--card);border:1px solid var(--border);border-radius:10px;padding:12px;transition:.2s}
.card:hover{border-color:var(--accent)}
.badge{display:inline-block;padding:2px 6px;border-radius:4px;font-size:7px;font-weight:600}
.badge-critique{background:var(--red);color:#fff}
.badge-haute{background:var(--orange);color:#fff}
.badge-moyenne{background:#ffcc00;color:#000}
.badge-info{background:var(--accent);color:#000}
.badge-24h{background:var(--green);color:#000}
.btn{padding:6px 12px;border:none;border-radius:6px;cursor:pointer;font-size:10px;font-weight:600;transition:.2s}
.btn-primary{background:var(--accent);color:#000}
.btn-primary:hover{filter:brightness(1.2)}
.btn-danger{background:var(--red);color:#fff}
.btn-sm{padding:3px 8px;font-size:9px}
.scanner-bar{display:flex;gap:4px;margin-bottom:8px;flex-wrap:wrap}
.scanner-bar input,.scanner-bar select{background:var(--card2);border:1px solid var(--border);border-radius:6px;padding:6px 10px;color:var(--text);font-size:9px;flex:1;min-width:80px}
.mb-6{margin-bottom:6px}
.text-center{text-align:center}
#briefContent{font-size:9px;line-height:1.6}
#briefContent strong{color:var(--accent)}
.filter-tabs{display:flex;gap:4px;margin-bottom:8px;flex-wrap:wrap}
.filter-tabs button{background:var(--card2);border:1px solid var(--border);border-radius:6px;padding:4px 10px;color:var(--text2);cursor:pointer;font-size:9px}
.filter-tabs button.active{background:var(--accent);color:#000;border-color:var(--accent);font-weight:600}
.modal-overlay{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.7);z-index:1000;display:none;align-items:center;justify-content:center}
.modal-overlay.show{display:flex}
.modal{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:20px;max-width:600px;width:90%;max-height:80vh;overflow-y:auto}
.toast{position:fixed;bottom:20px;right:20px;background:var(--accent);color:#000;padding:8px 16px;border-radius:8px;font-size:10px;font-weight:600;z-index:2000;opacity:0;transform:translateY(20px);transition:.3s;pointer-events:none}
.toast.show{opacity:1;transform:translateY(0)}
@media(max-width:768px){.layout{grid-template-columns:1fr}.sidebar{position:fixed;bottom:0;height:auto;z-index:100;display:flex;overflow-x:auto;padding:8px;gap:4px;border-right:none;border-top:1px solid var(--border)}.sidebar .logo,.sidebar .nav-item span{display:none}.main{padding:12px;padding-bottom:60px}.stats-grid{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>

<div class="layout">
  <nav class="sidebar" id="sidebar">
    <div class="logo">⟡ NEXUS<span>INTEL</span></div>
    <div class="nav-item active" onclick="showPage('dashboard')">📊 <span>Dashboard</span></div>
    <div class="nav-item" onclick="showPage('scan')">📡 <span>Scan RSS</span></div>
    <div class="nav-item" onclick="showPage('articles')">📰 <span>Articles</span></div>
    <div class="nav-item" onclick="showPage('synthese')">📋 <span>Synthèse 24h</span></div>
    <div class="nav-item" onclick="showPage('sources')">🌐 <span>Sources</span></div>
    <div class="nav-item" onclick="showPage('config')">⚙️ <span>Configuration</span></div>
  </nav>

  <main class="main" id="mainContent">
    <!-- Le contenu est injecté ici par JS -->
  </main>
</div>

<div class="modal-overlay" id="modalOverlay" onclick="if(event.target===this)closeModal()">
  <div class="modal" id="modalContent"></div>
</div>

<div class="toast" id="toast"></div>

<script>
// ===================== CONFIG =====================
const CONFIG = {
  scanInterval: 600000,
  maxArticles: 1000,
  sources: [
    {name:"Abidjan.net",url:"https://news.abidjan.net/rss/",region:"national"},
    {name:"Fraternité Matin",url:"https://www.fratmat.info/actualite/rss.xml",region:"national"},
    {name:"L'Intelligent d'Abidjan",url:"https://www.lintelligentdabidjan.com/feed/",region:"national"},
    {name:"Le Point Sur",url:"https://www.lepointsur.com/feed/",region:"national"},
    {name:"Soir Info",url:"https://www.soirinfo.com/feed/",region:"national"},
    {name:"Gouv CI",url:"https://www.gouv.ci/rss.xml",region:"national"},
    {name:"Portail CI",url:"https://www.portail-ci.com/feed/",region:"national"},
    {name:"Jeune Afrique CI",url:"https://www.jeuneafrique.com/fil-rss/cote-divoire/",region:"national"},
    {name:"RFI Côte d'Ivoire",url:"https://www.rfi.fr/fr/cote-divoire/rss",region:"national"},
    {name:"BBC Africa CI",url:"https://feeds.bbci.co.uk/news/world/africa/rss.xml",region:"national"},
    {name:"L'Expression CI",url:"https://www.lexpressionci.com/feed/",region:"national"},
    {name:"Le Patriote",url:"https://www.lepatriote.net/feed/",region:"national"},
    {name:"Africa News",url:"https://www.africanews.com/feed/",region:"continental"},
    {name:"Le Monde Afrique",url:"https://www.lemonde.fr/afrique/rss_full.xml",region:"continental"},
    {name:"France24",url:"https://www.france24.com/fr/rss",region:"international"},
    {name:"The Guardian Africa",url:"https://www.theguardian.com/world/africa/rss",region:"international"},
  ],
  keywords: {
    critique: ["alerte","attentat","cyberattaque","faille","exploit","0-day","vulnérabilité","crise","incident","urgence","attaque","danger"],
    haute: ["piratage","intrusion","malware","ransomware","espionnage","fuite","sanction","menace","grave"],
    moyenne: ["arnaque","phishing","ddos","darkweb","tribunal","enquête","procès","fraude","escroquerie"]
  }
}

const STATE = {
  articles: [],
  scanned: 0,
  lastScan: null,
  customSources: [],
  customKeywords: {critique:[],haute:[],moyenne:[]}
}

// ===================== UTILITAIRES =====================
function escHtml(s){if(!s)return '';return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;')}
function formatDate(d){if(!d)return '';try{return new Date(d).toLocaleDateString('fr-FR',{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'})}catch(e){return d}}
function getDate24hAgo(){const d=new Date();d.setHours(d.getHours()-24);return d}
function getArticles24h(){return STATE.articles.filter(a=>new Date(a.date)>getDate24hAgo())}

function classifyArticle(title, desc) {
  const text = (title + ' ' + (desc||'')).toLowerCase()
  const kw = {...CONFIG.keywords}
  STATE.customKeywords.critique.forEach(k=>{if(!kw.critique.includes(k))kw.critique.push(k)})
  STATE.customKeywords.haute.forEach(k=>{if(!kw.haute.includes(k))kw.haute.push(k)})
  STATE.customKeywords.moyenne.forEach(k=>{if(!kw.moyenne.includes(k))kw.moyenne.push(k)})
  for(const k of kw.critique) if(text.includes(k)) return 'critique'
  for(const k of kw.haute) if(text.includes(k)) return 'haute'
  for(const k of kw.moyenne) if(text.includes(k)) return 'moyenne'
  return 'info'
}

function getRegionBadge(region){
  if(region==='national') return '🇨🇮'
  if(region==='continental') return '🌍'
  return '🌐'
}

function showToast(msg){
  const t=document.getElementById('toast');t.textContent=msg;t.classList.add('show')
  setTimeout(()=>t.classList.remove('show'),3000)
}

function openModal(title,content){
  document.getElementById('modalContent').innerHTML=`<h3 style="margin-bottom:12px;font-size:14px">${title}</h3>${content}<button class="btn btn-primary" onclick="closeModal()" style="margin-top:12px">Fermer</button>`
  document.getElementById('modalOverlay').classList.add('show')
}

function closeModal(){document.getElementById('modalOverlay').classList.remove('show')}

// ===================== PAGES =====================
function showPage(page){
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'))
  document.querySelector(`.nav-item[onclick*="'${page}'"]`)?.classList.add('active')
  if(page==='dashboard') renderDashboard()
  else if(page==='scan') renderScan()
  else if(page==='articles') renderArticles()
  else if(page==='synthese') renderSynthese()
  else if(page==='sources') renderSources()
  else if(page==='config') renderConfig()
}

// ----- DASHBOARD -----
function renderDashboard(){
  const app=document.getElementById('mainContent')
  const arts=STATE.articles
  const arts24h=getArticles24h()
  const critique=arts.filter(a=>a.level==='critique')
  const critique24h=arts24h.filter(a=>a.level==='critique')
  const haute24h=arts24h.filter(a=>a.level==='haute')
  const bySrc={}
  arts24h.forEach(a=>{bySrc[a.source]=bySrc[a.source]||{count:0,critique:0};bySrc[a.source].count++;if(a.level==='critique')bySrc[a.source].critique++})
  const topSrc=Object.entries(bySrc).sort((a,b)=>b[1].count-a[1].count).slice(0,5)
  const byReg={national:arts24h.filter(a=>a.region==='national').length,continental:arts24h.filter(a=>a.region==='continental').length,international:arts24h.filter(a=>a.region==='international').length}

  app.innerHTML=`
    <div class="header"><h1>📊 Dashboard Intelligence</h1><span style="font-size:9px;color:var(--text2)">Dernier scan: ${STATE.lastScan?formatDate(STATE.lastScan):'Jamais'} · ${STATE.scanned} flux</span></div>
    <div class="stats-grid">
      <div class="stat-card"><div class="val" style="color:var(--accent)">${arts.length}</div><div class="lbl">Total articles</div></div>
      <div class="stat-card"><div class="val" style="color:var(--green)">${arts24h.length}</div><div class="lbl">Dernières 24h</div></div>
      <div class="stat-card"><div class="val" style="color:var(--red)">${critique24h.length}</div><div class="lbl">Alertes critiques ⚠️</div></div>
      <div class="stat-card"><div class="val" style="color:var(--orange)">${haute24h.length}</div><div class="lbl">Alertes hautes</div></div>
    </div>

    <div style="display:grid;grid-template-columns:1fr 1fr;gap:12px;margin-bottom:12px">
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:6px">🇨🇮 Activité par région (24h)</h3>
        <div style="display:flex;gap:8px;font-size:9px">
          <span>🇨🇮 National: <strong style="color:var(--accent)">${byReg.national}</strong></span>
          <span>🌍 Continental: <strong style="color:var(--green)">${byReg.continental}</strong></span>
          <span>🌐 International: <strong style="color:var(--orange)">${byReg.international}</strong></span>
        </div>
      </div>
      <div class="card">
        <h3 style="font-size:11px;margin-bottom:6px">📡 Top sources actives</h3>
        <div style="font-size:8px">
          ${topSrc.length?topSrc.map(([s,v])=>`<div style="display:flex;justify-content:space-between;padding:1px 0"><span>${escHtml(s)}</span><span>${v.count} arts${v.critique?` <span style="color:var(--red)">⚠️${v.critique}</span>`:''}</span></div>`).join(''):'<span style="color:var(--text2)">Aucune donnée</span>'}
        </div>
      </div>
    </div>

    <div class="card">
      <h3 style="font-size:11px;margin-bottom:6px">📋 Brief 24h — ${new Date().toLocaleDateString('fr-FR')}</h3>
      <div id="briefContent" style="font-size:9px;line-height:1.6">
        ${generateBrief()}
      </div>
    </div>

    ${critique24h.length?`
      <div class="card" style="margin-top:8px;border-color:var(--red)">
        <h3 style="font-size:11px;margin-bottom:6px;color:var(--red)">🚨 Alertes critiques (${critique24h.length})</h3>
        ${critique24h.slice(0,10).map(a=>`
          <div style="display:flex;justify-content:space-between;padding:3px 0;border-bottom:1px solid var(--border);font-size:8px">
            <span>${getRegionBadge(a.region)} <strong>${escHtml(a.title)}</strong></span>
            <span style="color:var(--text2)">${escHtml(a.source)} · ${formatDate(a.date)}</span>
          </div>
        `).join('')}
      </div>
    `:''}

    <div style="margin-top:8px">
      <button class="btn btn-primary" onclick="scanAllRSS()">📡 Scanner maintenant</button>
      <button class="btn btn-primary" style="margin-left:4px" onclick="exportBriefPDF()">📥 Exporter brief PDF</button>
    </div>
  `
}

function generateBrief(){
  const arts24h=getArticles24h()
  if(!arts24h.length) return '<span style="color:var(--text2)">Aucun article dans les 24h. Lancez un scan.</span>'

  const bySrc={};arts24h.forEach(a=>{bySrc[a.source]=bySrc[a.source]||[];bySrc[a.source].push(a)})
  const levels={critique:arts24h.filter(a=>a.level==='critique').length,haute:arts24h.filter(a=>a.level==='haute').length,moyenne:arts24h.filter(a=>a.level==='moyenne').length,info:arts24h.filter(a=>a.level==='info').length}
  const topCritique=arts24h.filter(a=>a.level==='critique').slice(0,5)

  let html=`
    <strong>📊 Résumé:</strong> ${arts24h.length} articles scannés — 🔴${levels.critique} critique | 🟠${levels.haute} haute | 🟡${levels.moyenne} moyenne | 🔵${levels.info} info<br><br>
  `
  if(topCritique.length){
    html+=`<strong>🚨 Alertes majeures:</strong><br>`
    topCritique.forEach(a=>html+=`  • ${getRegionBadge(a.region)} <strong>${escHtml(a.title)}</strong> — ${escHtml(a.source)}<br>`)
    html+=`<br>`
  }

  html+=`<strong>📡 Activité par source:</strong><br>`
  Object.entries(bySrc).sort((a,b)=>b[1].length-a[1].length).forEach(([src,arts])=>{
    const c=arts.filter(a=>a.level==='critique').length
    html+=`  • ${escHtml(src)}: ${arts.length} articles${c?` <span style="color:var(--red)">⚠️${c} critique</span>`:''}<br>`
  })

  return html
}

// ----- SCAN RSS -----
async function renderScan(){
  const app=document.getElementById('mainContent')
  const sources=getAllSources()
  app.innerHTML=`
    <div class="header"><h1>📡 Scan RSS</h1><button class="btn btn-primary" onclick="scanAllRSS()">🔄 Scanner tout</button></div>
    <div class="stats-grid">
      <div class="stat-card"><div class="val" style="color:var(--accent)">${sources.length}</div><div class="lbl">Sources configurées</div></div>
      <div class="stat-card"><div class="val" style="color:var(--green)">${STATE.articles.length}</div><div class="lbl">Articles collectés</div></div>
      <div class="stat-card"><div class="val" style="color:var(--red)">${STATE.articles.filter(a=>a.level==='critique').length}</div><div class="lbl">Critiques</div></div>
    </div>
    <div id="scanLog" style="background:var(--card2);border-radius:8px;padding:10px;font-size:8px;font-family:monospace;max-height:400px;overflow-y:auto;border:1px solid var(--border)">
      <div style="color:var(--text2)">⏳ Prêt... Cliquez sur "Scanner tout"</div>
    </div>
  `
}

async function scanAllRSS(){
  const sources=getAllSources()
  const log=document.getElementById('scanLog')
  if(log) log.innerHTML='<div style="color:var(--accent)">📡 Scan en cours...</div>'

  let total=0
  for(const src of sources){
    try{
      const proxyUrl=`https://api.allorigins.win/raw?url=${encodeURIComponent(src.url)}`
      const resp=await fetch(proxyUrl,{signal:AbortSignal.timeout(15000)})
      if(!resp.ok)throw new Error('HTTP '+resp.status)
      const text=await resp.text()
      const parser=new DOMParser()
      const xml=parser.parseFromString(text,'text/xml')
      const items=Array.from(xml.querySelectorAll('item')||[])
      const newArts=[]
      for(const item of items.slice(0,30)){
        const title=item.querySelector('title')?.textContent?.trim()
        const desc=item.querySelector('description')?.textContent?.trim()
        const link=item.querySelector('link')?.textContent?.trim()
        const dateStr=item.querySelector('pubDate')?.textContent?.trim()
        if(!title)continue
        const existing=STATE.articles.find(a=>a.title===title&&a.source===src.name)
        if(existing)continue
        const art={id:Date.now().toString(36)+Math.random().toString(36).substr(2,4),title,desc:desc||'',link:link||'',source:src.name,region:src.region,date:dateStr?new Date(dateStr).toISOString():new Date().toISOString(),level:classifyArticle(title,desc),read:false,scannedAt:new Date().toISOString()}
        newArts.push(art)
      }
      if(newArts.length){
        STATE.articles=[...newArts,...STATE.articles].slice(0,CONFIG.maxArticles)
        total+=newArts.length
      }
      if(log) log.innerHTML+=`<div style="color:var(--green)">✅ ${escHtml(src.name)} — ${newArts.length} nouveaux</div>`
    }catch(e){
      if(log) log.innerHTML+=`<div style="color:var(--red)">❌ ${escHtml(src.name)} — ${e.message}</div>`
    }
  }

  STATE.scanned=sources.length
  STATE.lastScan=new Date().toISOString()
  saveState()
  if(log) log.innerHTML+=`<div style="color:var(--accent);font-weight:600;margin-top:4px">✅ Scan terminé — ${total} nouveaux articles</div>`
  showToast(`📡 Scan terminé: ${total} articles`)
}

function getAllSources(){
  return [...CONFIG.sources,...(STATE.customSources||[])]
}

// ----- ARTICLES -----
let articleFilter='all'
function renderArticles(){
  const app=document.getElementById('mainContent')
  let arts=STATE.articles
  if(articleFilter==='unread') arts=arts.filter(a=>!a.read)
  else if(articleFilter==='critique') arts=arts.filter(a=>a.level==='critique')
  else if(articleFilter==='saved') arts=arts.filter(a=>a.saved)

  app.innerHTML=`
    <div class="header"><h1>📰 Articles</h1><span style="font-size:9px;color:var(--text2)">${STATE.articles.length} total · ${STATE.articles.filter(a=>!a.read).length} non lus</span></div>
    <div class="filter-tabs">
      <button class="${articleFilter==='all'?'active':''}" onclick="setArticleFilter('all')">📋 Tous</button>
      <button class="${articleFilter==='unread'?'active':''}" onclick="setArticleFilter('unread')">🆕 Non lus</button>
      <button class="${articleFilter==='critique'?'active':''}" onclick="setArticleFilter('critique')">🔴 Critique</button>
      <button class="${articleFilter==='saved'?'active':''}" onclick="setArticleFilter('saved')">⭐ Sauvés</button>
      <button class="btn btn-sm btn-primary" onclick="markAllRead()">✅ Tout marquer lu</button>
    </div>
    <div style="display:flex;flex-direction:column;gap:4px">
      ${arts.length?arts.map(a=>`
        <div class="card" style="padding:8px;cursor:pointer;${a.read?'opacity:.6':''}" onclick="openArticle('${a.id}')">
          <div style="display:flex;justify-content:space-between;align-items:start">
            <div style="flex:1;min-width:0;font-size:10px;font-weight:600">${getRegionBadge(a.region)} ${escHtml(a.title)}</div>
            <div style="display:flex;gap:4px;flex-shrink:0">
              ${new Date(a.date)>getDate24hAgo()?'<span class="badge badge-24h">24h</span>':''}
              <span class="badge badge-${a.level}">${a.level}</span>
            </div>
          </div>
          <div style="font-size:7px;color:var(--text2);margin-top:2px">${escHtml(a.source)} · ${formatDate(a.date)}</div>
        </div>
      `).join(''):'<div style="text-align:center;color:var(--text2);padding:30px;font-size:10px">Aucun article</div>'}
    </div>
  `
}

function setArticleFilter(f){articleFilter=f;renderArticles()}

function openArticle(id){
  const a=STATE.articles.find(x=>x.id===id)
  if(!a)return
  a.read=true;saveState()
  openModal(`📰 ${escHtml(a.title)}`,`
    <div style="font-size:8px;color:var(--text2);margin-bottom:6px">
      ${getRegionBadge(a.region)} ${escHtml(a.source)} · ${formatDate(a.date)}
      <span class="badge badge-${a.level}" style="margin-left:4px">${a.level}</span>
      ${new Date(a.date)>getDate24hAgo()?'<span class="badge badge-24h" style="margin-left:4px">24h</span>':''}
    </div>
    <div style="font-size:9px;line-height:1.6;margin-bottom:8px">${escHtml(a.desc||'Pas de description')}</div>
    ${a.link?`<a href="${a.link}" target="_blank" class="btn btn-primary" style="display:inline-block;text-decoration:none">🔗 Lire l'original</a>`:''}
    <button class="btn ${a.saved?'btn-danger':'btn-primary'}" onclick="toggleSaveArticle('${a.id}')" style="margin-left:4px">${a.saved?'⭐ Retirer':'⭐ Sauvegarder'}</button>
  `)
}

function toggleSaveArticle(id){
  const a=STATE.articles.find(x=>x.id===id)
  if(!a)return
  a.saved=!a.saved;saveState()
  showToast(a.saved?'⭐ Article sauvegardé':'Article retiré')
  renderArticles()
}

function markAllRead(){
  STATE.articles.forEach(a=>a.read=true);saveState();renderArticles()
  showToast('✅ Tout marqué comme lu')
}

// ----- SYNTHESE -----
function renderSynthese(){
  const app=document.getElementById('mainContent')
  const arts24h=getArticles24h()
  const crit24h=arts24h.filter(a=>a.level==='critique')
  const haut24h=arts24h.filter(a=>a.level==='haute')

  const bySrc={}
  arts24h.forEach(a=>{bySrc[a.source]=bySrc[a.source]||[];bySrc[a.source].push(a)})
  const byRegion={national:[],continental:[],international:[]}
  arts24h.forEach(a=>{if(byRegion[a.region])byRegion[a.region].push(a)})

  app.innerHTML=`
    <div class="header"><h1>📋 Synthèse 24h</h1><span style="font-size:9px;color:var(--text2)">${new Date().toLocaleDateString('fr-FR','full')}</span></div>

    <div class="stats-grid">
      <div class="stat-card"><div class="val" style="color:var(--accent)">${arts24h.length}</div><div class="lbl">Articles 24h</div></div>
      <div class="stat-card"><div class="val" style="color:var(--red)">${crit24h.length}</div><div class="lbl">Critiques</div></div>
      <div class="stat-card"><div class="val" style="color:var(--orange)">${haut24h.length}</div><div class="lbl">Hautes</div></div>
      <div class="stat-card"><div class="val" style="color:var(--green)">${Object.keys(bySrc).length}</div><div class="lbl">Sources actives</div></div>
    </div>

    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:8px">
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:4px">🇨🇮 National (${byRegion.national.length})</h3>
        ${byRegion.national.slice(0,8).map(a=>`<div style="font-size:7px;padding:1px 0"><span class="badge badge-${a.level}" style="margin-right:2px">${a.level}</span> ${escHtml(a.title)}</div>`).join('')||'<span style="color:var(--text2);font-size:8px">Aucun</span>'}
      </div>
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:4px">🌍 Continental (${byRegion.continental.length})</h3>
        ${byRegion.continental.slice(0,8).map(a=>`<div style="font-size:7px;padding:1px 0"><span class="badge badge-${a.level}" style="margin-right:2px">${a.level}</span> ${escHtml(a.title)}</div>`).join('')||'<span style="color:var(--text2);font-size:8px">Aucun</span>'}
      </div>
    </div>

    ${crit24h.length?`
      <div class="card" style="border-color:var(--red);margin-bottom:8px">
        <h3 style="font-size:10px;color:var(--red);margin-bottom:4px">🚨 ALERTES CRITIQUES</h3>
        ${crit24h.map(a=>`<div style="font-size:8px;padding:2px 0;border-bottom:1px solid var(--border)">${getRegionBadge(a.region)} <strong>${escHtml(a.title)}</strong> — ${escHtml(a.source)} · ${formatDate(a.date)}</div>`).join('')}
      </div>
    `:''}

    <div class="card">
      <h3 style="font-size:10px;margin-bottom:4px">📡 Sources (${Object.keys(bySrc).length})</h3>
      ${Object.entries(bySrc).sort((a,b)=>b[1].length-a[1].length).map(([src,arts])=>`
        <div style="display:flex;justify-content:space-between;font-size:8px;padding:1px 0">
          <span>${escHtml(src)}</span>
          <span>${arts.length} arts (🔴${arts.filter(a=>a.level==='critique').length} 🟠${arts.filter(a=>a.level==='haute').length} 🟡${arts.filter(a=>a.level==='moyenne').length})</span>
        </div>
      `).join('')}
    </div>

    <button class="btn btn-primary" style="margin-top:8px" onclick="exportBriefPDF()">📥 Exporter brief PDF</button>
  `
}

function exportBriefPDF(){
  const arts24h=getArticles24h()
  const lines=[]
  lines.push('═══════════════════════════════════════')
  lines.push('  NEXUS INTELLIGENCE — BRIEF 24H')
  lines.push(`  ${new Date().toLocaleDateString('fr-FR','full')}`)
  lines.push(`  ${arts24h.length} articles · ${STATE.scanned} sources scannées`)
  lines.push('═══════════════════════════════════════')
  lines.push('')
  if(arts24h.length){
    const crit=arts24h.filter(a=>a.level==='critique')
    if(crit.length){
      lines.push('🚨 ALERTES CRITIQUES:')
      crit.forEach(a=>lines.push(`  • [${a.source}] ${a.title} (${formatDate(a.date)})`))
      lines.push('')
    }
    const bySrc={};arts24h.forEach(a=>{bySrc[a.source]=bySrc[a.source]||[];bySrc[a.source].push(a)})
    lines.push('📡 ACTIVITÉ PAR SOURCE:')
    Object.entries(bySrc).sort((a,b)=>b[1].length-a[1].length).forEach(([src,arts])=>{
      const c=arts.filter(a=>a.level==='critique').length
      lines.push(`  • ${src}: ${arts.length} articles${c?` (${c} critiques)`:''}`)
    })
    lines.push('')
    lines.push('📋 DERNIERS ARTICLES:')
    arts24h.slice(0,20).forEach(a=>lines.push(`  [${a.level.toUpperCase()}] ${a.title} — ${a.source}`))
  } else {
    lines.push('Aucun article dans les dernières 24h.')
  }
  lines.push('')
  lines.push('═══════════════════════════════════════')
  lines.push('  Généré par NEXUS INTELLIGENCE v1.0')
  lines.push('═══════════════════════════════════════')

  const blob=new Blob([lines.join('\n')],{type:'text/plain;charset=utf-8'})
  const a=document.createElement('a')
  a.href=URL.createObjectURL(blob);a.download=`NEXUS_BRIEF_${new Date().toISOString().slice(0,10)}.txt`;a.click()
  showToast('📥 Brief exporté')
}

// ----- SOURCES -----
function renderSources(){
  const app=document.getElementById('mainContent')
  const sources=getAllSources()
  const national=sources.filter(s=>s.region==='national')
  const continental=sources.filter(s=>s.region==='continental')
  const international=sources.filter(s=>s.region==='international')

  app.innerHTML=`
    <div class="header"><h1>🌐 Sources RSS</h1></div>
    <div class="scanner-bar">
      <input id="newSrcName" placeholder="Nom source" style="max-width:120px">
      <input id="newSrcUrl" placeholder="URL RSS" style="flex:1">
      <select id="newSrcRegion" style="background:var(--card2);color:var(--text);border:1px solid var(--border);border-radius:6px;padding:6px;font-size:9px">
        <option value="national">🇨🇮 National</option>
        <option value="continental">🌍 Continental</option>
        <option value="international">🌐 International</option>
      </select>
      <button class="btn btn-primary" onclick="addCustomSource()">➕ Ajouter</button>
    </div>
    <div style="margin-top:8px">
      <h3 style="font-size:11px;margin-bottom:4px">🇨🇮 Nationales (${national.length})</h3>
      ${national.map(s=>sourceCard(s)).join('')}
      <h3 style="font-size:11px;margin:8px 0 4px">🌍 Continentales (${continental.length})</h3>
      ${continental.map(s=>sourceCard(s)).join('')}
      <h3 style="font-size:11px;margin:8px 0 4px">🌐 Internationales (${international.length})</h3>
      ${international.map(s=>sourceCard(s)).join('')}
    </div>
  `
}

function sourceCard(s){
  return `<div style="display:flex;justify-content:space-between;padding:3px 6px;background:var(--card2);border-radius:4px;font-size:8px;margin-bottom:2px">
    <span>${getRegionBadge(s.region)} ${escHtml(s.name)}</span>
    <span style="color:var(--text2);font-size:7px">${s.url.substring(0,40)}...</span>
  </div>`
}

function addCustomSource(){
  const n=document.getElementById('newSrcName')?.value.trim()
  const u=document.getElementById('newSrcUrl')?.value.trim()
  if(!n||!u)return showToast('❌ Nom et URL requis')
  STATE.customSources=STATE.customSources||[]
  STATE.customSources.push({name:n,url:u,region:document.getElementById('newSrcRegion').value})
  saveState();renderSources()
  showToast('✅ Source ajoutée')
}

// ----- CONFIG -----
function renderConfig(){
  const app=document.getElementById('mainContent')
  app.innerHTML=`
    <div class="header"><h1>⚙️ Configuration</h1></div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:6px">Général</h3>
        <label style="font-size:8px;color:var(--text2)">Intervalle scan (ms)</label>
        <input id="cfgInterval" value="${CONFIG.scanInterval}" style="width:100%;background:var(--card2);border:1px solid var(--border);border-radius:4px;padding:4px 6px;color:var(--text);font-size:9px;margin-bottom:4px">
        <label style="font-size:8px;color:var(--text2)">Max articles</label>
        <input id="cfgMax" value="${CONFIG.maxArticles}" style="width:100%;background:var(--card2);border:1px solid var(--border);border-radius:4px;padding:4px 6px;color:var(--text);font-size:9px;margin-bottom:6px">
        <button class="btn btn-primary btn-sm" onclick="saveConfig()">💾 Sauvegarder</button>
      </div>
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:6px">🔴 Mots-clés critiques</h3>
        <textarea id="kwCrit" style="width:100%;height:60px;background:var(--card2);border:1px solid var(--border);border-radius:4px;padding:4px;color:var(--text);font-size:8px;margin-bottom:4px">${CONFIG.keywords.critique.join('\n')}</textarea>
        <button class="btn btn-sm btn-primary" onclick="saveKW('critique')">💾</button>
      </div>
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:6px">🟠 Mots-clés hautes</h3>
        <textarea id="kwHaute" style="width:100%;height:60px;background:var(--card2);border:1px solid var(--border);border-radius:4px;padding:4px;color:var(--text);font-size:8px;margin-bottom:4px">${CONFIG.keywords.haute.join('\n')}</textarea>
        <button class="btn btn-sm btn-primary" onclick="saveKW('haute')">💾</button>
      </div>
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:6px">🟡 Mots-clés moyennes</h3>
        <textarea id="kwMoy" style="width:100%;height:60px;background:var(--card2);border:1px solid var(--border);border-radius:4px;padding:4px;color:var(--text);font-size:8px;margin-bottom:4px">${CONFIG.keywords.moyenne.join('\n')}</textarea>
        <button class="btn btn-sm btn-primary" onclick="saveKW('moyenne')">💾</button>
      </div>
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:6px">Données</h3>
        <button class="btn btn-sm btn-primary" onclick="exportFullData()" style="width:100%;margin-bottom:4px">📤 Exporter tout</button>
        <button class="btn btn-sm btn-primary" onclick="document.getElementById('importFile').click()" style="width:100%;margin-bottom:4px">📥 Importer</button>
        <input type="file" id="importFile" style="display:none" onchange="importData(event)" accept=".json">
        <button class="btn btn-sm btn-danger" onclick="clearAll()" style="width:100%">🗑️ Tout effacer</button>
      </div>
      <div class="card">
        <h3 style="font-size:10px;margin-bottom:6px">Statistiques</h3>
        <p style="font-size:8px;color:var(--text2)">Articles: ${STATE.articles.length}</p>
        <p style="font-size:8px;color:var(--text2)">Sources: ${getAllSources().length}</p>
        <p style="font-size:8px;color:var(--text2)">Dernier scan: ${STATE.lastScan?formatDate(STATE.lastScan):'Jamais'}</p>
      </div>
    </div>
  `
}

function saveConfig(){
  CONFIG.scanInterval=parseInt(document.getElementById('cfgInterval').value)||600000
  CONFIG.maxArticles=parseInt(document.getElementById('cfgMax').value)||1000
  saveState();showToast('✅ Configuration sauvegardée')
}

function saveKW(level){
  const el=document.getElementById('kw'+level.charAt(0).toUpperCase()+level.slice(1))
  if(el)CONFIG.keywords[level]=el.value.split('\n').map(s=>s.trim()).filter(Boolean)
  saveState();showToast('✅ Mots-clés sauvegardés')
}

function exportFullData(){
  const data={state:STATE,config:CONFIG,date:new Date().toISOString()}
  const blob=new Blob([JSON.stringify(data,null,2)],{type:'application/json'})
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download=`NEXUS_INTEL_export_${new Date().toISOString().slice(0,10)}.json`;a.click()
  showToast('✅ Exporté')
}

function importData(event){
  const file=event.target.files[0];if(!file)return
  const reader=new FileReader()
  reader.onload=function(e){
    try{
      const d=JSON.parse(e.target.result)
      if(d.state){Object.keys(d.state).forEach(k=>{STATE[k]=d.state[k]})}
      if(d.config){Object.keys(d.config).forEach(k=>{if(k in CONFIG)CONFIG[k]=d.config[k]})}
      saveState();showToast('✅ Importé')
    }catch(err){showToast('❌ Erreur: '+err.message)}
  };reader.readAsText(file)
  event.target.value=''
}

function clearAll(){
  if(!confirm('🗑️ Tout effacer ?'))return
  STATE.articles=[];STATE.scanned=0;STATE.lastScan=null
  saveState();showPage('dashboard')
  showToast('🗑️ Tout effacé')
}

// ===================== STOCKAGE LOCAL =====================
function saveState(){
  try{
    localStorage.setItem('nexus-intel',JSON.stringify(STATE))
    localStorage.setItem('nexus-intel-config',JSON.stringify(CONFIG))
  }catch(e){console.warn('Save error:',e)}
}

function loadState(){
  try{
    const s=localStorage.getItem('nexus-intel')
    if(s){const d=JSON.parse(s);Object.keys(d).forEach(k=>{STATE[k]=d[k]})}
    const c=localStorage.getItem('nexus-intel-config')
    if(c){const d=JSON.parse(c);Object.keys(d).forEach(k=>{if(k in CONFIG)CONFIG[k]=d[k]})}
  }catch(e){console.warn('Load error:',e)}
}

// ===================== AUTO SCAN =====================
let scanTimer=null
function startAutoScan(){
  if(scanTimer)clearInterval(scanTimer)
  scanTimer=setInterval(scanAllRSS,CONFIG.scanInterval||600000)
}

// ===================== INIT =====================
loadState()
startAutoScan()
showPage('dashboard')
setInterval(saveState,30000)

// Lancer un premier scan si aucun article
if(!STATE.articles.length)setTimeout(scanAllRSS,3000)

console.log('⟡ NEXUS INTELLIGENCE v1.0 — Scan & Synthèse')
</script>
</body>
</html>
