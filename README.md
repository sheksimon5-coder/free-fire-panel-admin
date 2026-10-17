<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Panel Bajar - Admin Panel</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f4f6f9; --card:#ffffff; --card2:#f8fafc; --border:#e2e8f0;
  --primary:#e11d48; --accent:#7c3aed; --text:#0f172a; --muted:#64748b;
  --green:#10b981; --amber:#f59e0b; --red:#ef4444; --bkash:#e2136e;
  --shadow-sm:0 1px 3px rgba(0,0,0,0.05),0 1px 2px rgba(0,0,0,0.03);
  --shadow-md:0 4px 6px -1px rgba(0,0,0,0.06),0 2px 4px -1px rgba(0,0,0,0.03);
}
body{font-family:-apple-system,'Segoe UI','Hind Siliguri',system-ui,sans-serif;background:var(--bg);color:var(--text);line-height:1.5;-webkit-font-smoothing:antialiased}
button{cursor:pointer;border:none;font-family:inherit;color:inherit;background:none}
input,select,textarea{background:#fff;border:1px solid var(--border);color:var(--text);border-radius:10px;padding:10px 13px;width:100%;font-family:inherit;font-size:14px;transition:.2s}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 3px rgba(225,29,72,.1)}
::-webkit-scrollbar{width:6px;height:6px}::-webkit-scrollbar-thumb{background:#cbd5e1;border-radius:3px}
header{position:sticky;top:0;z-index:40;background:rgba(255,255,255,.92);backdrop-filter:blur(16px);border-bottom:1px solid var(--border);box-shadow:0 1px 2px rgba(0,0,0,.02)}
.header-in{padding:0 16px;height:58px;display:flex;align-items:center;justify-content:space-between}
.logo{display:flex;align-items:center;gap:10px}
.logo-badge{width:34px;height:34px;border-radius:10px;background:linear-gradient(135deg,var(--primary),var(--accent));display:flex;align-items:center;justify-content:center;font-weight:900;color:#fff;font-size:15px;box-shadow:0 4px 10px rgba(225,29,72,.25)}
.logo-name{font-weight:800;font-size:15px;color:var(--text)}
.live-dot{display:inline-block;width:8px;height:8px;border-radius:50%;background:var(--green);margin-right:5px;animation:blink 1.5s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}
.btn-header{padding:7px 14px;border-radius:9px;font-size:12px;font-weight:700;background:var(--card2);border:1px solid var(--border);color:var(--text)}
.btn-header:hover{background:#eef2f7}
.layout{display:flex;min-height:calc(100vh - 58px)}
aside{width:250px;flex-shrink:0;background:#fff;border-right:1px solid var(--border);padding:14px;position:sticky;top:58px;height:calc(100vh - 58px);overflow-y:auto}
.side-btn{width:100%;text-align:left;padding:11px 13px;border-radius:10px;font-size:14px;display:flex;align-items:center;gap:9px;margin-bottom:3px;font-weight:600;transition:.2s;color:var(--text)}
.side-btn:hover{background:var(--bg)}
.side-btn.active{background:linear-gradient(135deg,var(--primary),#be123c);color:#fff;box-shadow:0 4px 12px rgba(225,29,72,.25)}
.side-divider{height:1px;background:var(--border);margin:10px 0}
.side-btn.danger{color:var(--red)}
.side-badge{margin-left:auto;background:var(--red);color:#fff;font-size:10px;font-weight:800;padding:1px 7px;border-radius:999px;min-width:18px;text-align:center}
.side-btn.active .side-badge{background:rgba(255,255,255,.35)}
main{flex:1;padding:18px;overflow-y:auto;max-width:900px}
.page-title{font-size:21px;font-weight:800;margin-bottom:18px;display:flex;justify-content:space-between;align-items:center;letter-spacing:-.3px;color:var(--text)}
.card{background:#fff;border:1px solid var(--border);border-radius:14px;box-shadow:var(--shadow-sm)}
.btn-primary{background:linear-gradient(135deg,var(--primary),#be123c);color:#fff;font-weight:700;transition:.2s;box-shadow:0 4px 12px rgba(225,29,72,.25)}
.btn-primary:hover{transform:translateY(-1px);box-shadow:0 6px 16px rgba(225,29,72,.35)}
.btn-sm{padding:7px 13px;border-radius:9px;font-size:13px;font-weight:700}
.btn-ghost{padding:7px 13px;border-radius:9px;font-size:13px;font-weight:700;background:var(--card2);border:1px solid var(--border);color:var(--text)}
.stat-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:13px;margin-bottom:18px}
.stat{padding:18px;position:relative;overflow:hidden}
.stat::before{content:'';position:absolute;top:0;left:0;width:4px;height:100%;background:var(--primary);opacity:.7}
.stat-icon{font-size:24px;margin-bottom:8px}
.stat-val{font-size:24px;font-weight:800;letter-spacing:-.5px}
.stat-label{font-size:10px;text-transform:uppercase;color:var(--muted);font-weight:700;letter-spacing:.5px;margin-top:3px}
@media(max-width:768px){
  aside{position:fixed;left:-270px;top:58px;z-index:50;transition:.3s;box-shadow:0 0 30px rgba(0,0,0,.1);height:calc(100vh - 58px)}
  aside.show{left:0}
  .overlay{display:none;position:fixed;inset:58px 0 0 0;background:rgba(15,23,42,.4);backdrop-filter:blur(2px);z-index:40}
  aside.show~.overlay{display:block}
}
.list-item{display:flex;align-items:flex-start;gap:12px;padding:14px;margin-bottom:10px;transition:.2s}
.list-item:hover{border-color:rgba(225,29,72,.3);box-shadow:var(--shadow-md)}
.list-icon{width:42px;height:42px;border-radius:11px;display:flex;align-items:center;justify-content:center;font-size:21px;background:var(--card2);flex-shrink:0;overflow:hidden}
.list-icon img{width:100%;height:100%;object-fit:cover}
.list-body{flex:1;min-width:0}
.list-title{font-weight:700;font-size:14px;color:var(--text)}
.list-sub{font-size:11px;color:var(--muted)}
.list-row{display:flex;gap:12px;flex-wrap:wrap;margin-top:3px;font-size:11px;color:var(--muted)}
.badge{font-size:10px;padding:3px 9px;border-radius:999px;font-weight:700}
.badge-green{background:rgba(16,185,129,.12);color:var(--green)}
.badge-amber{background:rgba(245,158,11,.12);color:var(--amber)}
.badge-red{background:rgba(239,68,68,.12);color:var(--red)}
.badge-pri{background:rgba(225,29,72,.12);color:var(--primary)}
.badge-muted{background:var(--card2);color:var(--muted)}
.btn-icon{width:34px;height:34px;border-radius:9px;display:flex;align-items:center;justify-content:center;font-size:13px;background:var(--card2);transition:.2s;border:1px solid var(--border)}
.btn-icon:hover{background:#eef2f7}
.btn-icon-danger{background:rgba(239,68,68,.08);color:var(--red);border-color:rgba(239,68,68,.2)}
.btn-icon-danger:hover{background:rgba(239,68,68,.15)}
.actions{display:flex;gap:5px;flex-shrink:0;flex-wrap:wrap}
.modal{position:fixed;inset:0;z-index:50;display:none;align-items:center;justify-content:center;background:rgba(15,23,42,.5);backdrop-filter:blur(6px);padding:16px}
.modal.show{display:flex;animation:fadeIn .2s}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.modal-card{background:#fff;border:1px solid var(--border);border-radius:16px;padding:20px;width:100%;max-width:560px;max-height:92vh;overflow-y:auto;box-shadow:0 20px 60px rgba(0,0,0,.25);animation:scaleIn .2s}
@keyframes scaleIn{from{transform:scale(.95);opacity:0}to{transform:scale(1);opacity:1}}
.modal-title{font-size:18px;font-weight:800;margin-bottom:16px;letter-spacing:-.3px;color:var(--text)}
.field{margin-bottom:13px}
.field label{font-size:12px;color:var(--muted);display:block;margin-bottom:5px;font-weight:600}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.grid-3{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
.btn-full{width:100%;padding:11px;border-radius:11px;font-weight:700;font-size:14px}
.switch{width:42px;height:23px;background:#cbd5e1;border-radius:12px;position:relative;cursor:pointer;transition:.2s;flex-shrink:0;border:none}
.switch.on{background:var(--primary)}
.switch::after{content:'';position:absolute;top:2px;left:2px;width:19px;height:19px;background:#fff;border-radius:50%;transition:.2s;box-shadow:0 2px 4px rgba(0,0,0,.2)}
.switch.on::after{transform:translateX(19px)}
.empty{text-align:center;padding:40px 20px;color:var(--muted)}
.toast{position:fixed;top:18px;left:50%;transform:translateX(-50%);background:var(--text);color:#fff;padding:13px 22px;border-radius:12px;z-index:100;animation:slideDown .3s;font-weight:600;font-size:13px;box-shadow:0 8px 24px rgba(0,0,0,.3)}
@keyframes slideDown{from{opacity:0;transform:translate(-50%,-20px)}to{opacity:1;transform:translate(-50%,0)}}
.section-card{padding:18px;margin-bottom:14px}
.section-title{font-size:14px;font-weight:800;margin-bottom:14px;display:flex;align-items:center;gap:8px;letter-spacing:-.2px;color:var(--text)}
.info-box{padding:12px 14px;border-radius:10px;font-size:12px;background:var(--card2);border:1px solid var(--border);line-height:1.6;color:var(--muted)}
.info-box code{color:var(--primary);font-family:monospace;background:rgba(225,29,72,.08);padding:1px 6px;border-radius:4px}
.hamburger{display:none;font-size:24px}
@media(max-width:768px){.hamburger{display:block}}
.fb-status{display:inline-flex;align-items:center;gap:6px;padding:3px 10px;border-radius:999px;font-size:11px;font-weight:700}
.fb-ok{background:rgba(16,185,129,.15);color:var(--green)}
.fb-no{background:rgba(245,158,11,.15);color:var(--amber)}
.order-code-box{margin-top:8px;font-family:monospace;font-size:13px;padding:10px 12px;border-radius:8px;display:inline-block;background:rgba(16,185,129,.08);color:var(--green);border:1px solid rgba(16,185,129,.25);word-break:break-all}
.plan-edit-row{display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:6px;margin-bottom:6px;align-items:end}
.plan-edit-row input{padding:8px 10px;font-size:12px}
.btn-add-plan{padding:8px 12px;border-radius:8px;font-size:12px;font-weight:700;background:var(--card2);color:var(--text);border:1px dashed var(--border);width:100%}
.btn-add-plan:hover{background:#eef2f7;border-color:var(--primary)}
.preview-img{width:100%;max-height:150px;object-fit:cover;border-radius:10px;margin-top:6px;border:1px solid var(--border)}

/* ====== AD MANAGER STYLES ====== */
.ad-item-row{display:flex;align-items:center;gap:10px;padding:10px;background:var(--card2);border:1px solid var(--border);border-radius:10px;margin-bottom:8px;transition:.2s}
.ad-item-row:hover{border-color:rgba(225,29,72,.3)}
.ad-thumb{width:64px;height:42px;object-fit:cover;border-radius:6px;border:1px solid var(--border);background:#fff;flex-shrink:0}
.ad-thumb-empty{width:64px;height:42px;border-radius:6px;border:1px dashed var(--border);display:flex;align-items:center;justify-content:center;color:var(--muted);font-size:11px;background:#fff;flex-shrink:0}
.ad-inputs{flex:1;display:flex;flex-direction:column;gap:4px;min-width:0}
.ad-inputs input{padding:6px 10px;font-size:11px;font-family:monospace}
.ad-order-btn{width:26px;height:26px;border-radius:6px;background:#fff;border:1px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:11px;color:var(--muted)}
.ad-order-btn:hover{background:var(--card);color:var(--primary);border-color:var(--primary)}
.ad-order-btn:disabled{opacity:.3;cursor:not-allowed}
.ad-preview-box{margin-top:14px;padding:10px;background:var(--card2);border:1px dashed var(--border);border-radius:10px;text-align:center}
.ad-preview-box .apb-label{font-size:11px;color:var(--muted);margin-bottom:8px;font-weight:600}
.ad-preview-slider{position:relative;aspect-ratio:16/7;border-radius:10px;overflow:hidden;background:#fff;border:1px solid var(--border);max-width:100%}
.ad-preview-slide{position:absolute;inset:0;opacity:0;transition:opacity .5s;display:flex;align-items:center;justify-content:center}
.ad-preview-slide.active{opacity:1}
.ad-preview-slide img{width:100%;height:100%;object-fit:cover;display:block}
.ad-preview-slide .apb-fallback{width:100%;height:100%;display:flex;align-items:center;justify-content:center;background:#f8fafc;font-size:36px;color:var(--muted)}
.ad-preview-dots{position:absolute;bottom:6px;left:50%;transform:translateX(-50%);display:flex;gap:4px;z-index:5}
.ad-preview-dot{width:6px;height:6px;border-radius:50%;background:rgba(255,255,255,.7);box-shadow:0 1px 2px rgba(0,0,0,.2)}
.ad-preview-dot.active{background:var(--primary);width:14px;border-radius:3px}
</style>
</head>
<body>
<header>
  <div class="header-in">
    <div class="logo">
      <button class="hamburger" onclick="document.getElementById('sidebar').classList.toggle('show')">☰</button>
      <div class="logo-badge">PB</div>
      <span class="logo-name">Admin Panel</span>
      <span style="font-size:11px;color:var(--green);font-weight:700;margin-left:4px"><span class="live-dot"></span>LIVE</span>
    </div>
    <div style="display:flex;gap:8px">
      <button class="btn-header" onclick="exportData()">📥 Backup</button>
    </div>
  </div>
</header>
<div class="layout">
<aside id="sidebar">
  <button class="side-btn active" data-tab="dashboard" onclick="setTab('dashboard')">📊 Dashboard</button>
  <button class="side-btn" data-tab="orders" onclick="setTab('orders')">🛒 Orders <span class="side-badge" id="pendingBadge" style="display:none">0</span></button>
  <button class="side-btn" data-tab="products" onclick="setTab('products')">📦 Products</button>
  <button class="side-btn" data-tab="users" onclick="setTab('users')">👥 Users</button>
  <div class="side-divider"></div>
  <button class="side-btn" data-tab="settings" onclick="setTab('settings')">⚙️ Settings</button>
  <button class="side-btn" data-tab="ads" onclick="setTab('ads')">🖼️ Ad Manager</button>
  <button class="side-btn" data-tab="integrations" onclick="setTab('integrations')">🔌 Integrations</button>
  <div class="side-divider"></div>
  <button class="side-btn danger" onclick="resetAll()">🗑️ সব রিসেট</button>
</aside>
<div class="overlay" onclick="document.getElementById('sidebar').classList.remove('show')"></div>
<main id="main"></main>
</div>
<div class="modal" id="modal" onclick="if(event.target===this)closeModal()"><div class="modal-card" id="modalContent"></div></div>

<script>
var FIREBASE_CONFIG={
  apiKey: "AIzaSyDt3gU-2iubzCZ94XFAGZswUnzxuDgUvFQ",
  authDomain: "free-fire-panel-611d6.firebaseapp.com",
  projectId: "free-fire-panel-611d6",
  storageBucket: "free-fire-panel-611d6.firebasestorage.app",
  messagingSenderId: "374641641780",
  appId: "1:374641641780:web:c87d374edf2371dae47d61",
  databaseURL:       ""
};
var TELEGRAM_CONFIG={ botToken: "8886507238:AAEW429taQKomorvb1mD2PhnZD3exlOPmyc", chatId: "7427334644" };
</script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
<script>
let fbApp=null,fbDb=null,fbAuth=null,fbConnected=false;
function initFirebase(){
  var c = (typeof FIREBASE_CONFIG!=='undefined') ? FIREBASE_CONFIG : {};
  if(!c.apiKey||!c.projectId||!c.appId){return false}
  try{
    if(typeof firebase==='undefined'){return false}
    const config={apiKey:c.apiKey,authDomain:c.authDomain||'',projectId:c.projectId,databaseURL:c.databaseURL||'',storageBucket:c.storageBucket||'',messagingSenderId:c.messagingSenderId||'',appId:c.appId};
    if(!firebase.apps.length){fbApp=firebase.initializeApp(config)}else{fbApp=firebase.app()}
    fbDb=firebase.firestore(); fbAuth=firebase.auth(); fbConnected=true; return true;
  }catch(e){return false}
}
function fbSync(collection,data){
  if(!fbConnected||!fbDb)return;
  try{fbDb.collection(collection).doc('main').set({data:JSON.stringify(data),updatedAt:new Date().toISOString()}).catch(()=>{})}catch(e){}
}
function fbLoad(collection,callback){
  if(!fbConnected||!fbDb){callback&&callback(null);return}
  try{fbDb.collection(collection).doc('main').get().then(doc=>{if(doc.exists){const data=JSON.parse(doc.data().data||'[]');callback&&callback(data)}else{callback&&callback(null)}}).catch(()=>{callback&&callback(null)})}catch(e){callback&&callback(null)}
}
function fbListen(collection,callback){
  if(!fbConnected||!fbDb)return;
  try{fbDb.collection(collection).doc('main').onSnapshot(doc=>{if(doc.exists){try{const data=JSON.parse(doc.data().data||'[]');callback&&callback(data)}catch(e){}}})}catch(e){}
}
</script>
<script>
let state={
  users:JSON.parse(localStorage.getItem('pb_users')||'[]'),
  products:JSON.parse(localStorage.getItem('pb_products')||'[]'),
  orders:JSON.parse(localStorage.getItem('pb_orders')||'[]'),
  settings:JSON.parse(localStorage.getItem('pb_settings')||JSON.stringify({
    site_name:'Panel Bajar',tagline:'Buy Premium Mods & Hacks',
    notification:'স্বাগতম Panel Bajar-এ!',notif_active:true,
    offer_text:'🔥 মEGA অফার! সব প্রোডাক্টে ৫০% ছাড় — সীমিত সময়ের জন্য! 🔥',offer_active:true,
    telegram:'https://t.me/panelbajar',youtube:'https://youtube.com/@panelbajar',
    bkash_number:'01XXXXXXXXX',help_url:'https://t.me/panelbajar',
    tg_bot_token:'',tg_chat_id:'',ads:[],ad_delay:3000,
    is_online:true,logo_url:'#',logo_image:'',
    online_start:'00:00',online_end:'23:59',whatsapp_number:'8801700000000'
  })),
  tab:'dashboard'
};
function save(){
  ['users','products','orders','settings'].forEach(k=>localStorage.setItem('pb_'+k,JSON.stringify(state[k])));
  fbSync('products',state.products);
  fbSync('orders',state.orders);
  fbSync('users',state.users);
  fbSync('settings',[state.settings]);
}
function uid(){return Date.now().toString(36)+Math.random().toString(36).slice(2,6)}
function $(id){return document.getElementById(id)}
function val(id){return $(id).value}
function toast(m){const t=document.createElement('div');t.className='toast';t.textContent=m;document.body.appendChild(t);setTimeout(()=>t.remove(),3000)}
function fmt(n){return '৳'+Number(n).toFixed(0)}
function tAgo(d){return new Date(d).toLocaleString('bn-BD')}
function sendTelegram(msg){
  const token=(TELEGRAM_CONFIG&&TELEGRAM_CONFIG.botToken)||state.settings.tg_bot_token||'';
  const chat=(TELEGRAM_CONFIG&&TELEGRAM_CONFIG.chatId)||state.settings.tg_chat_id||'';
  if(!token||!chat)return;
  try{fetch('https://api.telegram.org/bot'+token+'/sendMessage',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({chat_id:chat,text:msg,parse_mode:'HTML'})}).catch(()=>{})}catch(e){}
}
function setTab(t){state.tab=t;document.getElementById('sidebar').classList.remove('show');render()}
function openModal(html){$('modalContent').innerHTML=html;$('modal').classList.add('show')}
function closeModal(){$('modal').classList.remove('show')}
function updateBadge(){const po=state.orders.filter(o=>o.status==='PENDING').length;const b=$('pendingBadge');if(po>0){b.textContent=po;b.style.display='inline-block'}else b.style.display='none'}

function render(){
  document.querySelectorAll('.side-btn[data-tab]').forEach(b=>b.classList.toggle('active',b.dataset.tab===state.tab));
  updateBadge();
  const m=$('main');
  if(state.tab==='dashboard')m.innerHTML=adminDashboard();
  else if(state.tab==='products')m.innerHTML=adminProducts();
  else if(state.tab==='orders')m.innerHTML=adminOrders();
  else if(state.tab==='users')m.innerHTML=adminUsers();
  else if(state.tab==='settings')m.innerHTML=adminSettings();
  else if(state.tab==='ads')m.innerHTML=adminAds();
  else if(state.tab==='integrations')m.innerHTML=adminIntegrations();
  if(state.tab==='ads') startAdPreview();
}

function adminDashboard(){
  const revenue=state.orders.filter(o=>o.status==='COMPLETED').reduce((s,o)=>s+o.price,0);
  const pending=state.orders.filter(o=>o.status==='PENDING').length;
  const cards=[
    {l:'Total Users',v:state.users.length,c:'#3b82f6',i:'👥'},
    {l:'Total Products',v:state.products.length,c:'var(--green)',i:'📦'},
    {l:'Total Orders',v:state.orders.length,c:'var(--primary)',i:'🛒'},
    {l:'Revenue',v:fmt(revenue),c:'var(--green)',i:'💰'},
    {l:'Pending Orders',v:pending,c:'var(--amber)',i:'⏰'}
  ];
  return `<div class="page-title"><span>📊 Dashboard</span></div>
  <div class="stat-grid">${cards.map(c=>`<div class="card stat"><div class="stat-icon">${c.i}</div><div class="stat-val" style="color:${c.c}">${c.v}</div><div class="stat-label">${c.l}</div></div>`).join('')}</div>
  <div class="card" style="padding:16px">
    <div class="section-title">🛒 সাম্প্রতিক অর্ডার</div>
    ${state.orders.length===0?'<p style="font-size:12px;text-align:center;padding:16px;color:var(--muted)">কোনো অর্ডার নেই</p>':state.orders.slice(-10).reverse().map(o=>{
      const p=state.products.find(x=>x.id===o.productId);
      const u=state.users.find(x=>x.id===o.userId);
      return `<div style="display:flex;justify-content:space-between;font-size:12px;padding:7px 0;border-bottom:1px solid var(--border)">
        <div><div style="font-weight:600">${p?.name||'—'}</div><div class="list-sub">${u?.username||'—'} • Txn: ${o.txnId||'—'}</div></div>
        <div style="display:flex;flex-direction:column;align-items:flex-end;gap:3px">
          <div style="font-weight:700;color:var(--primary)">${fmt(o.price)}</div>
          <span class="badge ${o.status==='COMPLETED'?'badge-green':o.status==='PENDING'?'badge-amber':'badge-red'}">${o.status}</span>
        </div>
      </div>`}).join('')}
  </div>`;
}

function adminProducts(){
  return `<div class="page-title"><span>Products (${state.products.length})</span><button class="btn-primary btn-sm" onclick="productForm()">+ নতুন</button></div>
  ${state.products.length===0?'<div class="card empty">কোনো প্রোডাক্ট নেই</div>':state.products.map(p=>{
    const orders=state.orders.filter(o=>o.productId===p.id).length;
    return `<div class="card list-item">
      <div class="list-icon">${p.image?`<img src="${p.image}" onerror="this.style.display='none';this.parentElement.textContent='${p.icon||'🎮'}'">`:p.icon||'🎮'}</div>
      <div class="list-body">
        <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:center">
          <span class="list-title">${p.name}</span>
          <span class="badge ${p.category==='ROOT'?'badge-red':'badge-green'}">${p.category}</span>
          <span class="badge ${p.status==='ACTIVE'?'badge-green':'badge-muted'}">${p.status}</span>
          ${p.antiban?'<span class="badge badge-green">ANTI BAN</span>':''}
          ${p.maintenance?'<span class="badge badge-amber">MAINTENANCE</span>':''}
        </div>
        <div class="list-row">
          <span>অর্ডার: ${orders}</span>
          <span>Plans: ${p.plans?.length||0}</span>
          ${p.image?'<span style="color:var(--green)">📷 Image</span>':'<span style="color:var(--red)">No Image</span>'}
        </div>
      </div>
      <div class="actions">
        <button class="btn-icon" onclick="productForm('${p.id}')">✏️</button>
        <button class="btn-icon btn-icon-danger" onclick="delProduct('${p.id}')">🗑️</button>
      </div>
    </div>`}).join('')}`;
}

function productForm(id){
  const p=id?state.products.find(x=>x.id===id):null;
  const plans=p?.plans||[{dur:'1 Day',price:0,stock:99}];
  const plansHtml=plans.map((pl,i)=>`<div class="plan-edit-row">
    <div><label style="font-size:10px">Duration</label><input value="${pl.dur}" onchange="updatePlan(${i},'dur',this.value)" placeholder="1 Day" /></div>
    <div><label style="font-size:10px">Price (৳)</label><input type="number" value="${pl.price}" onchange="updatePlan(${i},'price',this.value)" /></div>
    <div><label style="font-size:10px">Stock</label><input type="number" value="${pl.stock}" onchange="updatePlan(${i},'stock',this.value)" /></div>
    <button class="btn-icon btn-icon-danger" onclick="removePlan(${i})">🗑️</button>
  </div>`).join('');
  openModal(`<div class="modal-title">${p?'প্রোডাক্ট এডিট':'নতুন প্রোডাক্ট'}</div>
  <div class="grid-2">
    <div class="field"><label>নাম</label><input id="f_name" value="${p?.name||''}" /></div>
    <div class="field"><label>আইকন (emoji)</label><input id="f_icon" value="${p?.icon||'🎮'}" /></div>
  </div>
  <div class="field"><label>📷 প্রোডাক্ট ছবির URL</label><input id="f_image" value="${p?.image||''}" placeholder="https://example.com/image.jpg" oninput="previewImage()" /><img id="imgPreview" class="preview-img" src="${p?.image||''}" style="${p?.image?'':'display:none'}" onerror="this.style.display='none'" /></div>
  <div class="field"><label>বর্ণনা</label><textarea id="f_desc" rows="2">${p?.description||''}</textarea></div>
  <div class="grid-3">
    <div class="field"><label>পুরোনো দাম</label><input id="f_old" type="number" value="${p?.oldPrice||''}" /></div>
    <div class="field"><label>ক্যাটেগরি</label><select id="f_cat">
      <option ${p?.category==='NON_ROOT'?'selected':''}>NON_ROOT</option>
      <option ${p?.category==='ROOT'?'selected':''}>ROOT</option>
      <option ${p?.category==='IPHONE'?'selected':''}>IPHONE</option>
      <option ${p?.category==='PC'?'selected':''}>PC</option>
    </select></div>
    <div class="field"><label>স্ট্যাটাস</label><select id="f_status">
      <option ${p?.status==='ACTIVE'?'selected':''}>ACTIVE</option>
      <option ${p?.status==='INACTIVE'?'selected':''}>INACTIVE</option>
    </select></div>
  </div>
  <div style="display:flex;gap:14px;margin-bottom:14px">
    <div style="display:flex;align-items:center;gap:8px"><div class="switch ${p?.antiban?'on':''}" id="f_antiban" onclick="this.classList.toggle('on')"></div><label style="font-size:12px;font-weight:600">100% ANTI BAN</label></div>
    <div style="display:flex;align-items:center;gap:8px"><div class="switch ${p?.maintenance?'on':''}" id="f_maint" onclick="this.classList.toggle('on')"></div><label style="font-size:12px;font-weight:600">MAINTENANCE</label></div>
  </div>
  <div class="section-card" style="background:var(--card2);padding:14px;margin-bottom:14px">
    <div class="section-title" style="margin-bottom:10px">📁 FILE & SETUP URLs</div>
    <div class="field"><label>📹 PANEL FULL DETAILS (Video URL)</label><input id="f_url_full" value="${p?.url_full_details||''}" placeholder="https://youtube.com/watch?v=..." style="font-family:monospace;font-size:11px" /></div>
    <div class="field"><label>🎬 PANEL SETUP VIDEO URL</label><input id="f_url_setup" value="${p?.url_setup_video||''}" placeholder="https://youtube.com/watch?v=..." style="font-family:monospace;font-size:11px" /></div>
    <div class="field"><label>⬇️ PANEL DOWNLOAD LINK</label><input id="f_url_download" value="${p?.url_download||''}" placeholder="https://mediafire.com/..." style="font-family:monospace;font-size:11px" /></div>
    <div class="field" style="margin-bottom:0"><label>📱 AIMKILL IPHONE SETUP VIDEO URL</label><input id="f_url_iphone" value="${p?.url_iphone_setup||''}" placeholder="https://youtube.com/watch?v=..." style="font-family:monospace;font-size:11px" /></div>
  </div>
  <div class="section-card" style="background:var(--card2);padding:14px;margin-bottom:14px">
    <div class="section-title" style="margin-bottom:10px">⏱️ Recharge Plans</div>
    <div id="planList">${plansHtml}</div>
    <button class="btn-add-plan" onclick="addPlan()">+ প্ল্যান যোগ করুন</button>
  </div>
  <button class="btn-primary btn-full" onclick="saveProduct('${id||''}')">সেভ করুন</button>`);
  window._editPlans=JSON.parse(JSON.stringify(plans));
}
function previewImage(){const url=val('f_image');const img=$('imgPreview');if(url){img.src=url;img.style.display='block'}else{img.style.display='none'}}
function addPlan(){window._editPlans.push({dur:'1 Day',price:0,stock:99});refreshPlanList()}
function removePlan(i){window._editPlans.splice(i,1);refreshPlanList()}
function updatePlan(i,k,v){if(window._editPlans[i])window._editPlans[i][k]=k==='dur'?v:Number(v)}
function refreshPlanList(){
  $('planList').innerHTML=window._editPlans.map((pl,i)=>`<div class="plan-edit-row">
    <div><label style="font-size:10px">Duration</label><input value="${pl.dur}" onchange="updatePlan(${i},'dur',this.value)" /></div>
    <div><label style="font-size:10px">Price</label><input type="number" value="${pl.price}" onchange="updatePlan(${i},'price',this.value)" /></div>
    <div><label style="font-size:10px">Stock</label><input type="number" value="${pl.stock}" onchange="updatePlan(${i},'stock',this.value)" /></div>
    <button class="btn-icon btn-icon-danger" onclick="removePlan(${i})">🗑️</button>
  </div>`).join('');
}
function saveProduct(id){
  const data={name:val('f_name'),icon:val('f_icon'),image:val('f_image'),description:val('f_desc'),oldPrice:val('f_old')?Number(val('f_old')):null,category:val('f_cat'),status:val('f_status'),antiban:$('f_antiban').classList.contains('on'),maintenance:$('f_maint').classList.contains('on'),url_full_details:val('f_url_full'),url_setup_video:val('f_url_setup'),url_download:val('f_url_download'),url_iphone_setup:val('f_url_iphone'),plans:window._editPlans||[]};
  if(!data.name){toast('নাম আবশ্যক');return}
  if(id)Object.assign(state.products.find(x=>x.id===id),data);
  else state.products.push({id:uid(),slug:data.name.toLowerCase().replace(/\s+/g,'-'),...data});
  save();closeModal();render();toast('সেভ হয়েছে');
}
function delProduct(id){if(!confirm('মুছে ফেলতে চান?'))return;state.products=state.products.filter(p=>p.id!==id);save();render();toast('মুছে ফেলা হয়েছে')}

function adminOrders(){
  return `<div class="page-title"><span>Orders (${state.orders.length})</span></div>
  ${state.orders.length===0?'<div class="card empty">কোনো অর্ডার নেই</div>':state.orders.slice().reverse().map(o=>{
    const p=state.products.find(x=>x.id===o.productId);
    const u=state.users.find(x=>x.id===o.userId);
    return `<div class="card list-item">
      <div class="list-icon">${p?.icon||'📦'}</div>
      <div class="list-body">
        <div style="display:flex;gap:8px;flex-wrap:wrap;align-items:center">
          <span class="list-title">${p?.name||'—'}</span>
          <span class="badge badge-pri">${fmt(o.price)}</span>
          ${o.planDur?`<span class="badge badge-muted">⏱ ${o.planDur}</span>`:''}
          ${o.qty>1?`<span class="badge badge-muted">${o.qty}x</span>`:''}
          <span class="badge ${o.status==='COMPLETED'?'badge-green':o.status==='PENDING'?'badge-amber':'badge-red'}">${o.status}</span>
        </div>
        <div class="list-sub" style="margin-top:5px">👤 ${u?.username||'—'} (${u?.email||''})<br>⏰ ${tAgo(o.createdAt)}<br>🧾 TxnID: ${o.txnId||'—'}</div>
        ${o.status==='COMPLETED'&&o.codeContent?`<div class="order-code-box">🎫 API Key: ${o.codeContent}</div>`:''}
        ${o.status==='PENDING'?`<div style="margin-top:8px;font-size:11px;color:var(--amber);font-weight:600">⏳ API Key দিয়ে অর্ডার একসেপ্ট করুন</div>`:''}
      </div>
      ${o.status==='PENDING'?`<div class="actions">
        <button class="btn-sm btn-primary" onclick="acceptOrder('${o.id}')">✓ একসেপ্ট</button>
        <button class="btn-sm" style="background:var(--red);color:#fff;border-radius:9px" onclick="cancelOrder('${o.id}')">✗</button>
      </div>`:''}
    </div>`}).join('')}`;
}
function acceptOrder(id){
  const o=state.orders.find(x=>x.id===id);if(!o)return;
  const p=state.products.find(x=>x.id===o.productId);
  const u=state.users.find(x=>x.id===o.userId);
  openModal(`<div class="modal-title">✅ অর্ডার একসেপ্ট — API Key দিন</div>
  <div style="background:var(--card2);padding:14px;border-radius:10px;margin-bottom:16px">
    <div style="font-size:13px;margin-bottom:4px"><strong>প্রোডাক্ট:</strong> ${p?.name||'—'}</div>
    ${o.planDur?`<div style="font-size:13px;margin-bottom:4px"><strong>প্ল্যান:</strong> ${o.planDur}</div>`:''}
    ${o.qty>1?`<div style="font-size:13px;margin-bottom:4px"><strong>পরিমাণ:</strong> ${o.qty}x</div>`:''}
    <div style="font-size:13px;margin-bottom:4px"><strong>ইউজার:</strong> ${u?.username||'—'}</div>
    <div style="font-size:13px;margin-bottom:4px"><strong>দাম:</strong> ${fmt(o.price)}</div>
    <div style="font-size:13px"><strong>TxnID:</strong> ${o.txnId||'—'}</div>
  </div>
  <div class="field"><label>🎫 API Key / কোড</label><textarea id="orderCode" rows="4" placeholder="এখানে API Key বা কোড লিখুন..." style="font-family:monospace"></textarea></div>
  <div style="display:flex;gap:8px">
    <button class="btn-sm" style="flex:1;background:var(--card2);border:1px solid var(--border)" onclick="closeModal()">বাতিল</button>
    <button class="btn-primary btn-sm" style="flex:1" onclick="confirmAccept('${id}')">✅ একসেপ্ট করুন</button>
  </div>`);
}
function confirmAccept(id){
  const o=state.orders.find(x=>x.id===id);if(!o)return;
  const code=$('orderCode').value.trim();
  if(!code){toast('API Key দিন');return}
  o.status='COMPLETED';o.codeContent=code;
  const u=state.users.find(x=>x.id===o.userId);
  if(u){u.totalOrders=(u.totalOrders||0)+1;u.totalSpent=(u.totalSpent||0)+o.price}
  save();closeModal();render();
  sendTelegram('✅ <b>অর্ডার একসেপ্ট!</b>\n\n👤 ইউজার: '+(u?.username||'—')+'\n📦 প্রোডাক্ট: '+(state.products.find(x=>x.id===o.productId)?.name||'—')+'\n🎫 API Key: <code>'+code+'</code>\n💰 দাম: '+fmt(o.price));
  toast('অর্ডার একসেপ্ট হয়েছে!');
}
function cancelOrder(id){const o=state.orders.find(x=>x.id===id);if(!o||o.status!=='PENDING')return;o.status='CANCELLED';save();render();toast('অর্ডার বাতিল')}

function adminUsers(){
  return `<div class="page-title"><span>Users (${state.users.length})</span></div>
  ${state.users.length===0?'<div class="card empty">কোনো ইউজার নেই</div>':state.users.map(u=>{
    const orders=state.orders.filter(o=>o.userId===u.id).length;
    return `<div class="card list-item">
      <div class="list-icon" style="border-radius:50%;background:${u.avatarColor};color:#fff;font-weight:800;font-size:13px">${u.username.slice(0,2).toUpperCase()}</div>
      <div class="list-body">
        <div style="display:flex;gap:8px;align-items:center"><span class="list-title">${u.username}</span>${u.role==='ADMIN'?'👑':''}${u.banned?'🚫':''}</div>
        <div class="list-sub" style="word-break:break-all">${u.email}</div>
        <div class="list-row"><span>অর্ডার: ${orders}</span><span>খরচ: ${fmt(u.totalSpent||0)}</span></div>
      </div>
      <div class="actions">
        <button class="btn-icon" onclick="userForm('${u.id}')">✏️</button>
        <button class="btn-icon btn-icon-danger" onclick="delUser('${u.id}')">🗑️</button>
      </div>
    </div>`}).join('')}`;
}
function userForm(id){
  const u=state.users.find(x=>x.id===id);
  openModal(`<div class="modal-title">ইউজার এডিট — ${u.username}</div>
  <div class="grid-2">
    <div class="field"><label>Total Spent</label><input id="u_spent" type="number" value="${u.totalSpent||0}" /></div>
    <div class="field"><label>Avatar Color</label><input id="u_color" value="${u.avatarColor}" /></div>
  </div>
  <div class="grid-2">
    <div class="field"><label>Role</label><select id="u_role">
      <option ${u.role==='USER'?'selected':''}>USER</option>
      <option ${u.role==='ADMIN'?'selected':''}>ADMIN</option>
    </select></div>
    <div class="field"><label>Password</label><input id="u_pass" value="${u.password}" /></div>
  </div>
  <div style="display:flex;justify-content:space-between;align-items:center;padding:13px;background:var(--card2);border-radius:11px;margin-bottom:14px">
    <div style="font-size:14px;font-weight:600">ব্যান করা</div>
    <div class="switch ${u.banned?'on':''}" id="u_ban" onclick="this.classList.toggle('on')"></div>
  </div>
  <button class="btn-primary btn-full" onclick="saveUser('${id}')">সেভ করুন</button>`);
}
function saveUser(id){
  const u=state.users.find(x=>x.id===id);
  u.totalSpent=Number(val('u_spent'));u.avatarColor=val('u_color');u.role=val('u_role');u.password=val('u_pass');u.banned=$('u_ban').classList.contains('on');
  save();closeModal();render();toast('সেভ হয়েছে');
}
function delUser(id){if(!confirm('মুছে ফেলতে চান?'))return;state.users=state.users.filter(u=>u.id!==id);save();render();toast('মুছে ফেলা হয়েছে')}

function adminSettings(){
  const s=state.settings;
  return `<div class="page-title"><span>⚙️ Settings</span></div>
  
  <div class="card section-card" style="border:1px solid var(--primary);background:rgba(225,29,72,.03)">
    <div class="section-title">⏰ অনলাইন / অফলাইন টাইমার</div>
    <div class="info-box" style="margin-bottom:14px">💡 নির্দিষ্ট সময়ে ওয়েবসাইট অনলাইন থাকবে, বাকি সময় অফলাইন। ২৪ ঘন্টা চালু রাখতে 00:00 থেকে 23:59 দিন।</div>
    <div class="grid-2">
      <div class="field"><label>শুরুর সময় (Start)</label><input id="s_online_start" type="time" value="${s.online_start||'00:00'}" /></div>
      <div class="field"><label>শেষের সময় (End)</label><input id="s_online_end" type="time" value="${s.online_end||'23:59'}" /></div>
    </div>
    <div style="display:flex;justify-content:space-between;align-items:center;padding:10px;background:var(--card2);border-radius:10px">
      <label style="font-size:13px;font-weight:700">Force Off (ম্যানুয়ালি বন্ধ)</label>
      <div style="display:flex;align-items:center;gap:8px">
        <span style="font-size:11px;color:var(--muted)">${s.is_online===false?'অফলাইন':'অনলাইন'}</span>
        <div class="switch ${s.is_online!==false?'on':''}" id="s_force_off" onclick="this.classList.toggle('on')"></div>
      </div>
    </div>
  </div>

  <div class="card section-card">
    <div class="section-title">🔗 লোগো সেটআপ</div>
    <div class="grid-2">
      <div class="field"><label>লোগো ছবির URL</label><input id="s_logo_image" value="${s.logo_image||''}" placeholder="https://example.com/logo.png" style="font-family:monospace;font-size:12px" oninput="previewLogo()" /></div>
      <div class="field"><label>লোগো ক্লিক লিংক</label><input id="s_logo_url" value="${s.logo_url||''}" placeholder="https://t.me/yourchannel" style="font-family:monospace;font-size:12px" /></div>
    </div>
    <img id="logoPreview" class="preview-img" src="${s.logo_image||''}" style="${s.logo_image?'':'display:none'}" onerror="this.style.display='none'" />
  </div>

  <div class="card section-card">
    <div class="section-title">💬 WhatsApp বাটন</div>
    <div class="field"><label>WhatsApp নাম্বার (দেশের কোড সহ)</label><input id="s_whatsapp" value="${s.whatsapp_number||''}" placeholder="8801700000000" style="font-family:monospace;font-size:15px;font-weight:700" /></div>
  </div>

  <div class="card section-card">
    <div class="section-title">🎁 Offer Bar</div>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
      <label style="font-size:13px;font-weight:600">অফার বার সক্রিয়</label>
      <div class="switch ${s.offer_active?'on':''}" id="s_offer" onclick="this.classList.toggle('on')"></div>
    </div>
    <div class="field"><label>অফার টেক্সট</label><textarea id="s_offer_txt" rows="2">${s.offer_text||''}</textarea></div>
  </div>

  <div class="card section-card">
    <div class="section-title">🌐 সাইট</div>
    <div class="field"><label>সাইটের নাম</label><input id="s_name" value="${s.site_name}" /></div>
    <div class="field"><label>ট্যাগলাইন</label><input id="s_tag" value="${s.tagline}" /></div>
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:14px">
      <label style="font-size:13px;font-weight:600">নোটিফিকেশন বার</label>
      <div class="switch ${s.notif_active?'on':''}" id="s_notif" onclick="this.classList.toggle('on')"></div>
    </div>
    <div class="field"><label>নোটিফিকেশন টেক্সট</label><textarea id="s_notif_txt" rows="2">${s.notification}</textarea></div>
  </div>

  <div class="card section-card">
    <div class="section-title">🔗 সোশ্যাল লিংক</div>
    <div class="field"><label>Telegram URL</label><input id="s_tg" value="${s.telegram}" style="font-family:monospace;font-size:12px" /></div>
    <div class="field"><label>YouTube URL</label><input id="s_yt" value="${s.youtube}" style="font-family:monospace;font-size:12px" /></div>
    <div class="field"><label>💬 Help Chat URL</label><input id="s_help" value="${s.help_url||''}" style="font-family:monospace;font-size:12px" /></div>
  </div>

  <div class="card section-card">
    <div class="section-title">📲 bKash</div>
    <div class="field" style="margin-bottom:0"><label>bKash Number</label><input id="s_bkash" value="${s.bkash_number||''}" placeholder="01XXXXXXXXX" style="font-family:monospace;font-size:15px;font-weight:700" /></div>
  </div>

  <button class="btn-primary btn-full" style="position:sticky;bottom:8px" onclick="saveSettings()">💾 সব সেভ করুন</button>`;
}
function previewLogo(){const url=val('s_logo_image');const img=$('logoPreview');if(url){img.src=url;img.style.display='block'}else{img.style.display='none'}}
function saveSettings(){
  state.settings=Object.assign({},state.settings,{
    site_name:val('s_name'),tagline:val('s_tag'),notification:val('s_notif_txt'),notif_active:$('s_notif').classList.contains('on'),
    offer_text:val('s_offer_txt'),offer_active:$('s_offer').classList.contains('on'),
    telegram:val('s_tg'),youtube:val('s_yt'),help_url:val('s_help'),bkash_number:val('s_bkash'),
    is_online:$('s_force_off').classList.contains('on'),
    logo_url:val('s_logo_url'),logo_image:val('s_logo_image'),
    online_start:val('s_online_start'),online_end:val('s_online_end'),
    whatsapp_number:val('s_whatsapp')
  });
  save();toast('সেটিংস সেভ হয়েছে');render();
}

// AD MANAGER
let adPreviewInterval=null;
function adminAds(){
  const s=state.settings;
  if(!Array.isArray(s.ads)) s.ads=[];
  return `<div class="page-title"><span>🖼️ Ad Manager (${s.ads.length})</span><button class="btn-primary btn-sm" onclick="addAd()">+ নতুন অ্যাড</button></div>
  
  <div class="card section-card">
    <div class="info-box" style="margin-bottom:14px">💡 এখানে ছবি URL দিলে ইউজার প্যানেলের উপরে সুন্দর fade+zoom স্লাইডার হিসেবে দেখাবে।<br>✅ ছবির সাইজ: <b>1200 × 525</b> (16:7) হলে সবচেয়ে ভালো।</div>
    
    <div id="adListContainer">
      ${s.ads.length===0?'<div style="text-align:center;padding:30px 12px;color:var(--muted);font-size:13px">এখনো কোনো অ্যাড নেই। উপরের "+ নতুন অ্যাড" বাটনে ক্লিক করুন।</div>':s.ads.map((ad,i)=>renderAdRow(ad,i,s.ads.length)).join('')}
    </div>

    <div class="field" style="margin-top:14px">
      <label>⏱️ অ্যাড চেঞ্জ হওয়ার সময় (মিলিসেকেন্ড)</label>
      <input id="s_ad_delay" type="number" value="${s.ad_delay||3000}" placeholder="3000" min="1500" step="500" />
      <div style="font-size:11px;color:var(--muted);margin-top:4px">💡 ৩০০০ = ৩ সেকেন্ড। সর্বনিম্ন ১৫০০।</div>
    </div>

    <div class="ad-preview-box">
      <div class="apb-label">🔍 Live Preview (User Panel-এ যেমন দেখাবে)</div>
      <div class="ad-preview-slider" id="adPreviewSlider"></div>
    </div>

    <button class="btn-primary btn-full" style="margin-top:14px" onclick="saveAds()">💾 অ্যাড সেটিংস সেভ করুন</button>
  </div>`;
}

function renderAdRow(ad,i,total){
  const hasUrl = ad.url && String(ad.url).trim()!=='';
  return `<div class="ad-item-row" data-idx="${i}">
    ${hasUrl?`<img class="ad-thumb" src="${ad.url}" onerror="this.style.display='none';this.nextElementSibling.style.display='flex'" /><div class="ad-thumb-empty" style="display:none">❌</div>`:`<div class="ad-thumb-empty">ছবি নেই</div>`}
    <div class="ad-inputs">
      <input type="text" value="${(ad.url||'').replace(/"/g,'&quot;')}" oninput="updateAdField(${i},'url',this.value)" placeholder="🖼️ Image URL (https://...)" />
      <input type="text" value="${(ad.link||'').replace(/"/g,'&quot;')}" oninput="updateAdField(${i},'link',this.value)" placeholder="🔗 Click Link (অপশনাল)" />
    </div>
    <div style="display:flex;flex-direction:column;gap:3px">
      <button class="ad-order-btn" onclick="moveAd(${i},-1)" ${i===0?'disabled':''} title="উপরে">▲</button>
      <button class="ad-order-btn" onclick="moveAd(${i},1)" ${i===total-1?'disabled':''} title="নিচে">▼</button>
    </div>
    <button class="btn-icon btn-icon-danger" onclick="removeAd(${i})" title="মুছুন">🗑️</button>
  </div>`;
}

function addAd(){
  if(!state.settings.ads) state.settings.ads=[];
  state.settings.ads.push({url:'',link:''});
  refreshAdList();
  startAdPreview();
  toast('নতুন অ্যাড যোগ হয়েছে — URL দিন');
}
function updateAdField(i,field,v){
  if(state.settings.ads[i]) state.settings.ads[i][field]=v;
}
function removeAd(i){
  if(!confirm('এই অ্যাডটি মুছে ফেলবেন?'))return;
  state.settings.ads.splice(i,1);
  refreshAdList();
  startAdPreview();
  toast('মুছে ফেলা হয়েছে');
}
function moveAd(i,dir){
  const ads=state.settings.ads;
  const ni=i+dir;
  if(ni<0||ni>=ads.length)return;
  [ads[i],ads[ni]]=[ads[ni],ads[i]];
  refreshAdList();
  startAdPreview();
}
function refreshAdList(){
  const s=state.settings;
  if(!Array.isArray(s.ads))s.ads=[];
  const c=$('adListContainer');
  if(!c)return;
  if(s.ads.length===0){
    c.innerHTML='<div style="text-align:center;padding:30px 12px;color:var(--muted);font-size:13px">এখনো কোনো অ্যাড নেই। উপরের "+ নতুন অ্যাড" বাটনে ক্লিক করুন।</div>';
    return;
  }
  c.innerHTML=s.ads.map((ad,i)=>renderAdRow(ad,i,s.ads.length)).join('');
}
function saveAds(){
  const delayEl=$('s_ad_delay');
  if(delayEl){
    const d=Number(delayEl.value)||3000;
    state.settings.ad_delay=Math.max(1500,d);
  }
  if(!Array.isArray(state.settings.ads)) state.settings.ads=[];
  // Remove empty ads
  const cleaned=state.settings.ads.filter(ad=>ad&&ad.url&&String(ad.url).trim()!=='');
  state.settings.ads=cleaned;
  save();
  toast('✅ অ্যাড সেটিংস সেভ হয়েছে!');
  refreshAdList();
  startAdPreview();
}

function startAdPreview(){
  if(adPreviewInterval){clearInterval(adPreviewInterval);adPreviewInterval=null}
  const slider=$('adPreviewSlider');
  if(!slider)return;
  const ads=(state.settings.ads||[]).filter(a=>a&&a.url&&String(a.url).trim()!=='');
  if(ads.length===0){
    slider.innerHTML='<div class="ad-preview-slide active"><div class="apb-fallback">🖼️ ছবি যোগ করুন</div></div>';
    return;
  }
  slider.innerHTML=ads.map((ad,i)=>`<div class="ad-preview-slide ${i===0?'active':''}"><img src="${(ad.url||'').replace(/"/g,'&quot;')}" onerror="this.parentElement.innerHTML='<div class=\\'apb-fallback\\'>❌ ভাঙা ছবি</div>'" /></div>`).join('')+
    `<div class="ad-preview-dots">${ads.map((_,i)=>`<div class="ad-preview-dot ${i===0?'active':''}"></div>`).join('')}</div>`;
  if(ads.length<=1)return;
  let idx=0;
  const delay=Math.max(1500,Number(state.settings.ad_delay)||3000);
  adPreviewInterval=setInterval(()=>{
    const slides=slider.querySelectorAll('.ad-preview-slide');
    const dots=slider.querySelectorAll('.ad-preview-dot');
    if(!slides.length)return;
    slides[idx].classList.remove('active');
    if(dots[idx])dots[idx].classList.remove('active');
    idx=(idx+1)%slides.length;
    slides[idx].classList.add('active');
    if(dots[idx])dots[idx].classList.add('active');
  },delay);
}

function adminIntegrations(){
  const tgOk=(TELEGRAM_CONFIG&&TELEGRAM_CONFIG.botToken&&TELEGRAM_CONFIG.chatId)||(state.settings.tg_bot_token&&state.settings.tg_chat_id);
  const fbOk=(FIREBASE_CONFIG&&FIREBASE_CONFIG.apiKey&&FIREBASE_CONFIG.projectId&&FIREBASE_CONFIG.appId);
  const fbStatus=fbConnected?'<span class="fb-status fb-ok">✓ কানেক্টেড</span>':fbOk?'<span class="fb-status fb-no">⚠ রিলোড করুন</span>':'<span class="fb-status fb-no">⚠ কনফিগার করুন</span>';
  return `<div class="page-title"><span>🔌 Integrations</span></div>
  <div class="info-box" style="margin-bottom:14px"><strong>📊 স্ট্যাটাস:</strong> Firebase: ${fbStatus} • Telegram: ${tgOk?'<span style="color:var(--green)">✓ সক্রিয়</span>':'<span style="color:var(--amber)">⚠ কনফিগার করুন</span>'}</div>
  
  <div class="card section-card">
    <div class="section-title">🤖 Telegram Bot ${tgOk?'<span class="fb-status fb-ok">✓ সক্রিয়</span>':'<span class="fb-status fb-no">⚠ কনফিগার করুন</span>'}</div>
    <div class="info-box" style="margin-bottom:14px">💡 <b>সেটআপ:</b><br>1. <code>@BotFather</code> → <code>/newbot</code><br>2. Bot Token কপি করুন<br>3. <code>@userinfobot</code> → আপনার Chat ID নিন</div>
    <div class="field"><label>Bot Token (ফলব্যাক)</label><input id="tg_token" value="${state.settings.tg_bot_token||''}" placeholder="123456789:ABC..." style="font-family:monospace;font-size:12px" /></div>
    <div class="field"><label>Chat ID (ফলব্যাক)</label><input id="tg_chat" value="${state.settings.tg_chat_id||''}" placeholder="123456789" style="font-family:monospace" /></div>
    <button class="btn-ghost btn-sm" style="margin-bottom:8px" onclick="testTelegram()">🧪 Test Notification</button>
  </div>
  
  <div class="card section-card">
    <div class="section-title">🔥 Firebase Configuration ${fbOk?'<span class="fb-status fb-ok">✓ কনফিগারড</span>':'<span class="fb-status fb-no">⚠ কনফিগার করুন</span>'}</div>
    <div class="info-box" style="margin-bottom:14px">💡 কোডের উপরে <code>FIREBASE_CONFIG</code> ভ্যারিয়েবলে আপনার আসল কনফিগ বসান।</div>
    <div class="info-box" style="margin-bottom:10px"><b>📋 আপনার Firebase:</b><br>
    <code style="display:block;margin-top:6px;font-size:10px;white-space:pre-line">Project: ${(FIREBASE_CONFIG&&FIREBASE_CONFIG.projectId)||'—'}\napiKey: ${((FIREBASE_CONFIG&&FIREBASE_CONFIG.apiKey)||'').substring(0,20)}...\nappId: ${((FIREBASE_CONFIG&&FIREBASE_CONFIG.appId)||'').substring(0,30)}...</code></div>
  </div>
  
  <button class="btn-primary btn-full" style="position:sticky;bottom:8px" onclick="saveIntegrations()">💾 Integrations সেভ</button>`;
}
function saveIntegrations(){
  state.settings=Object.assign({},state.settings,{tg_bot_token:val('tg_token'),tg_chat_id:val('tg_chat')});
  save();toast('সেভ হয়েছে');render();
}
function testTelegram(){
  const token=val('tg_token')||(TELEGRAM_CONFIG&&TELEGRAM_CONFIG.botToken)||'';
  const chat=val('tg_chat')||(TELEGRAM_CONFIG&&TELEGRAM_CONFIG.chatId)||'';
  if(!token||!chat){toast('Token ও Chat ID দিন');return}
  fetch('https://api.telegram.org/bot'+token+'/sendMessage',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({chat_id:chat,text:'✅ Test from Panel Bajar Admin!',parse_mode:'HTML'})})
    .then(r=>r.json()).then(d=>{if(d.ok)toast('✅ Test সফল! Telegram চেক করুন');else toast('❌ ব্যর্থ: '+(d.description||''))})
    .catch(()=>toast('❌ নেটওয়ার্ক সমস্যা'));
}

function exportData(){
  const data={users:state.users,products:state.products,orders:state.orders,settings:state.settings};
  const blob=new Blob([JSON.stringify(data,null,2)],{type:'application/json'});
  const a=document.createElement('a');a.href=URL.createObjectURL(blob);a.download='panel-bajar-backup.json';a.click();
  toast('ব্যাকআপ ডাউনলোড');
}
function resetAll(){if(!confirm('সব ডেটা মুছে ফেলবেন?'))return;localStorage.clear();location.reload()}

setInterval(function(){
  state.orders=JSON.parse(localStorage.getItem('pb_orders')||'[]');
  state.users=JSON.parse(localStorage.getItem('pb_users')||'[]');
  state.settings=JSON.parse(localStorage.getItem('pb_settings')||JSON.stringify(state.settings));
  updateBadge();
  if(['dashboard','orders'].includes(state.tab))render();
},2500);

function seed(){
  if(state.users.length>0||state.products.length>0)return;
  state.users.push({id:uid(),email:'admin@panelbajar.com',username:'admin',password:'admin123',role:'ADMIN',totalOrders:0,totalSpent:0,banned:false,avatarColor:'#7c3aed',createdAt:new Date().toISOString()});
  state.users.push({id:uid(),email:'saimon@example.com',username:'saimon',password:'user123',role:'USER',totalOrders:0,totalSpent:0,banned:false,avatarColor:'#ec4899',createdAt:new Date().toISOString()});
  const samples=[
    {name:'AIM HACK - ANDROID - IOS',icon:'🎯',category:'NON_ROOT',antiban:true,image:'',description:'100% Anti Ban • Auto Aim • Android & iOS',plans:[{dur:'1 Hour',price:15,stock:99},{dur:'12 Hours',price:120,stock:99},{dur:'1 Day',price:160,stock:99}]},
    {name:'BALA MODS - NON ROOT',icon:'🔥',category:'NON_ROOT',antiban:true,image:'',description:'Main ID Safe • Anti Ban • Non Root',plans:[{dur:'1 Day',price:25,stock:99},{dur:'7 Days',price:150,stock:99},{dur:'30 Days',price:500,stock:99}]},
    {name:'AIM HACK - ROOT',icon:'🎯',category:'ROOT',antiban:true,image:'',description:'Root Version • Premium Features',plans:[{dur:'1 Day',price:30,stock:99},{dur:'7 Days',price:180,stock:99}]},
    {name:'IPHONE MOD',icon:'📱',category:'IPHONE',antiban:true,image:'',description:'iOS Only • No Jailbreak',plans:[{dur:'1 Day',price:50,stock:99},{dur:'7 Days',price:300,stock:99}]},
    {name:'PC ESP HACK',icon:'💻',category:'PC',antiban:true,image:'',description:'PC Version • ESP • Aim • Wallhack',plans:[{dur:'1 Day',price:40,stock:99},{dur:'7 Days',price:250,stock:99}]}
  ];
  samples.forEach(s=>state.products.push({id:uid(),slug:s.name.toLowerCase().replace(/\s+/g,'-'),...s,status:'ACTIVE',url_full_details:'',url_setup_video:'',url_download:'',url_iphone_setup:''}));
  save();
}
seed();render();

setTimeout(function(){
  if(initFirebase()){
    fbListen('orders',function(data){if(data){state.orders=data;localStorage.setItem('pb_orders',JSON.stringify(data));updateBadge();if(['dashboard','orders'].includes(state.tab))render()}});
    fbListen('users',function(data){if(data){state.users=data;localStorage.setItem('pb_users',JSON.stringify(data));if(['dashboard','users'].includes(state.tab))render()}});
    fbListen('products',function(data){if(data){state.products=data;localStorage.setItem('pb_products',JSON.stringify(data));if(['dashboard','products'].includes(state.tab))render()}});
    fbListen('settings',function(data){if(data&&data[0]){state.settings=data[0];localStorage.setItem('pb_settings',JSON.stringify(data[0]));if(['dashboard','settings','ads'].includes(state.tab))render()}});
    fbLoad('orders',function(d){if(d){state.orders=d;localStorage.setItem('pb_orders',JSON.stringify(d));render()}});
    fbLoad('products',function(d){if(d){state.products=d;localStorage.setItem('pb_products',JSON.stringify(d));render()}});
    fbLoad('settings',function(d){if(d&&d[0]){state.settings=d[0];localStorage.setItem('pb_settings',JSON.stringify(d[0]));render()}});
  }
},1500);
</script>
</body>
</html>
