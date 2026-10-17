<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<meta name="theme-color" content="#7c3aed" />
<title>Panel Bajar - Admin Panel</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
img,svg,video,canvas{max-width:100%;height:auto;display:block}
:root{
  --bg:#0a0f1c; --bg2:#111827; --card:#1a2332; --card2:#243044;
  --border:#2d3a4f; --border-light:#3d4a63;
  --primary:#7c3aed; --primary-light:#a78bfa; --primary-dark:#5b21b6;
  --accent:#e11d48; --accent-dark:#be123c;
  --text:#f1f5f9; --muted:#94a3b8; --muted2:#64748b;
  --green:#10b981; --amber:#f59e0b; --red:#ef4444; --blue:#3b82f6; --cyan:#06b6d4;
  --shadow-sm:0 1px 3px rgba(0,0,0,0.3);
  --shadow-md:0 4px 6px -1px rgba(0,0,0,0.3);
  --shadow-lg:0 10px 15px -3px rgba(0,0,0,0.5);
  --shadow-glow:0 0 24px rgba(124,58,237,0.35);
}
html{width:100%;max-width:100vw;overflow-x:hidden}
body{font-family:-apple-system,'Segoe UI','Hind Siliguri',system-ui,sans-serif;background:var(--bg);color:var(--text);min-height:100vh;line-height:1.5;-webkit-font-smoothing:antialiased;overflow-x:hidden}
a{color:inherit;text-decoration:none}
button{cursor:pointer;border:none;font-family:inherit;color:inherit;background:none}
input,select,textarea{background:var(--bg);border:1px solid var(--border);color:var(--text);border-radius:10px;padding:12px 14px;width:100%;font-family:inherit;font-size:14px;transition:.2s;max-width:100%}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 3px rgba(124,58,237,.2)}
textarea{resize:vertical;min-height:70px}
::-webkit-scrollbar{width:6px;height:6px}
::-webkit-scrollbar-track{background:var(--bg2)}
::-webkit-scrollbar-thumb{background:var(--border-light);border-radius:3px}

/* ====== LAYOUT ====== */
.app-layout{display:flex;min-height:100vh}
.sidebar{width:260px;min-width:260px;background:linear-gradient(180deg,var(--bg2),var(--bg));border-right:1px solid var(--border);display:flex;flex-direction:column;position:fixed;top:0;left:0;bottom:0;z-index:50;transition:transform .3s ease}
.sidebar-brand{padding:20px;display:flex;align-items:center;gap:12px;border-bottom:1px solid var(--border)}
.brand-logo{width:44px;height:44px;border-radius:12px;background:linear-gradient(135deg,var(--primary),var(--accent));display:flex;align-items:center;justify-content:center;font-weight:900;color:#fff;font-size:18px;box-shadow:var(--shadow-glow);flex-shrink:0;overflow:hidden}
.brand-logo img{width:100%;height:100%;object-fit:cover}
.brand-title{font-weight:800;font-size:16px;letter-spacing:-0.3px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.brand-sub{font-size:10px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;font-weight:600}
.sidebar-nav{flex:1;padding:16px 12px;overflow-y:auto;display:flex;flex-direction:column;gap:4px}
.nav-section-title{font-size:10px;color:var(--muted2);text-transform:uppercase;letter-spacing:1.2px;font-weight:700;padding:16px 12px 8px}
.sidebar-item{display:flex;align-items:center;gap:12px;padding:11px 14px;border-radius:10px;font-size:13px;font-weight:600;color:var(--muted);transition:all .2s;cursor:pointer;position:relative;overflow:hidden}
.sidebar-item:hover{background:var(--card2);color:var(--text)}
.sidebar-item.active{background:linear-gradient(135deg,rgba(124,58,237,.2),rgba(225,29,72,.15));color:var(--text);box-shadow:inset 0 0 0 1px rgba(124,58,237,.3)}
.sidebar-item.active::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:linear-gradient(180deg,var(--primary),var(--accent));border-radius:0 3px 3px 0}
.sidebar-item svg{width:18px;height:18px;flex-shrink:0}
.sidebar-item .badge-count{margin-left:auto;background:var(--accent);color:#fff;font-size:10px;font-weight:800;padding:2px 8px;border-radius:999px;min-width:20px;text-align:center}
.sidebar-foot{padding:12px;border-top:1px solid var(--border)}
.admin-profile{display:flex;align-items:center;gap:10px;padding:10px;border-radius:10px;background:var(--card);margin-bottom:8px}
.admin-avatar{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,var(--primary),var(--accent));display:flex;align-items:center;justify-content:center;font-weight:800;font-size:13px;color:#fff;flex-shrink:0}
.admin-name{font-size:13px;font-weight:700;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.admin-role{font-size:10px;color:var(--green);font-weight:700;text-transform:uppercase;letter-spacing:.5px}
.btn-logout{width:100%;padding:10px;border-radius:10px;font-size:13px;font-weight:700;background:rgba(239,68,68,.1);color:var(--red);border:1px solid rgba(239,68,68,.2);transition:.2s;display:flex;align-items:center;justify-content:center;gap:8px}
.btn-logout:hover{background:rgba(239,68,68,.2)}

/* ====== MAIN CONTENT ====== */
.main-content{flex:1;margin-left:260px;min-height:100vh;display:flex;flex-direction:column;min-width:0}
.topbar{height:64px;background:rgba(10,15,28,.85);backdrop-filter:blur(12px);border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;padding:0 24px;position:sticky;top:0;z-index:40;gap:12px}
.topbar-left{display:flex;align-items:center;gap:12px;min-width:0}
.menu-toggle{display:none;width:38px;height:38px;border-radius:10px;background:var(--card);border:1px solid var(--border);align-items:center;justify-content:center;flex-shrink:0}
.menu-toggle svg{width:20px;height:20px}
.page-heading h1{font-size:18px;font-weight:800;letter-spacing:-0.3px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.page-heading p{font-size:11px;color:var(--muted);font-weight:500}
.topbar-right{display:flex;align-items:center;gap:10px;flex-shrink:0}
.status-pill{display:flex;align-items:center;gap:6px;padding:6px 12px;border-radius:999px;font-size:11px;font-weight:700;border:1px solid transparent}
.status-pill.online{background:rgba(16,185,129,.1);color:var(--green);border-color:rgba(16,185,129,.25)}
.status-pill.offline{background:rgba(239,68,68,.1);color:var(--red);border-color:rgba(239,68,68,.25)}
.status-dot{width:7px;height:7px;border-radius:50%}
.status-pill.online .status-dot{background:var(--green);animation:blink 1.5s infinite}
.status-pill.offline .status-dot{background:var(--red)}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}
.icon-btn{width:38px;height:38px;border-radius:10px;background:var(--card);border:1px solid var(--border);display:flex;align-items:center;justify-content:center;transition:.2s}
.icon-btn:hover{background:var(--card2);border-color:var(--primary)}
.icon-btn svg{width:18px;height:18px;color:var(--muted)}
.content-area{flex:1;padding:24px;overflow-x:hidden}
.content-inner{max-width:1400px;margin:0 auto}

/* ====== CARDS ====== */
.card{background:var(--card);border:1px solid var(--border);border-radius:16px;box-shadow:var(--shadow-sm);overflow:hidden}
.card-pad{padding:20px}
.card-head{padding:18px 20px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;gap:12px;flex-wrap:wrap}
.card-head h3{font-size:15px;font-weight:800;display:flex;align-items:center;gap:8px}
.card-head p{font-size:12px;color:var(--muted);margin-top:2px}

/* ====== BUTTONS ====== */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:10px 18px;border-radius:10px;font-size:13px;font-weight:700;transition:all .2s;white-space:nowrap;border:1px solid transparent}
.btn:hover{transform:translateY(-1px)}
.btn svg{width:16px;height:16px}
.btn-primary{background:linear-gradient(135deg,var(--primary),var(--primary-dark));color:#fff;box-shadow:0 4px 12px rgba(124,58,237,.3)}
.btn-accent{background:linear-gradient(135deg,var(--accent),var(--accent-dark));color:#fff;box-shadow:0 4px 12px rgba(225,29,72,.3)}
.btn-green{background:linear-gradient(135deg,var(--green),#059669);color:#fff;box-shadow:0 4px 12px rgba(16,185,129,.3)}
.btn-amber{background:linear-gradient(135deg,var(--amber),#d97706);color:#fff;box-shadow:0 4px 12px rgba(245,158,11,.3)}
.btn-red{background:linear-gradient(135deg,var(--red),#dc2626);color:#fff;box-shadow:0 4px 12px rgba(239,68,68,.3)}
.btn-blue{background:linear-gradient(135deg,var(--blue),#1d4ed8);color:#fff;box-shadow:0 4px 12px rgba(59,130,246,.3)}
.btn-ghost{background:var(--card2);color:var(--text);border-color:var(--border)}
.btn-ghost:hover{background:var(--border)}
.btn-sm{padding:7px 12px;font-size:12px;border-radius:8px}
.btn-sm svg{width:14px;height:14px}
.btn-icon{width:34px;height:34px;padding:0;border-radius:8px}
.btn-icon svg{width:16px;height:16px}
.btn:disabled{opacity:.4;cursor:not-allowed;transform:none}

/* ====== STATS ====== */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:16px;margin-bottom:24px}
.stat-card{background:var(--card);border:1px solid var(--border);border-radius:16px;padding:20px;position:relative;overflow:hidden;transition:.3s;animation:statFadeUp .5s ease both}
.stat-card:hover{transform:translateY(-3px);box-shadow:var(--shadow-lg);border-color:var(--border-light)}
.stat-card::before{content:'';position:absolute;top:0;left:0;width:4px;height:100%;border-radius:0 4px 4px 0}
.stat-card.c-purple::before{background:linear-gradient(180deg,var(--primary),var(--primary-dark))}
.stat-card.c-green::before{background:linear-gradient(180deg,var(--green),#059669)}
.stat-card.c-amber::before{background:linear-gradient(180deg,var(--amber),#d97706)}
.stat-card.c-red::before{background:linear-gradient(180deg,var(--red),#dc2626)}
.stat-card.c-blue::before{background:linear-gradient(180deg,var(--blue),#1d4ed8)}
.stat-card.c-cyan::before{background:linear-gradient(180deg,var(--cyan),#0891b2)}
.stat-card .stat-icon{width:44px;height:44px;border-radius:12px;display:flex;align-items:center;justify-content:center;margin-bottom:14px;font-size:20px}
.stat-card.c-purple .stat-icon{background:rgba(124,58,237,.15);color:var(--primary-light)}
.stat-card.c-green .stat-icon{background:rgba(16,185,129,.15);color:var(--green)}
.stat-card.c-amber .stat-icon{background:rgba(245,158,11,.15);color:var(--amber)}
.stat-card.c-red .stat-icon{background:rgba(239,68,68,.15);color:var(--red)}
.stat-card.c-blue .stat-icon{background:rgba(59,130,246,.15);color:var(--blue)}
.stat-card.c-cyan .stat-icon{background:rgba(6,182,212,.15);color:var(--cyan)}
.stat-card .stat-label{font-size:11px;color:var(--muted);font-weight:700;text-transform:uppercase;letter-spacing:.8px}
.stat-card .stat-val{font-size:28px;font-weight:900;margin-top:4px;letter-spacing:-1px;line-height:1.1}
.stat-card .stat-sub{font-size:11px;color:var(--muted2);margin-top:6px;font-weight:500}
@keyframes statFadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}

/* ====== TABLES ====== */
.table-wrap{overflow-x:auto;border-radius:12px;border:1px solid var(--border)}
table{width:100%;border-collapse:collapse;font-size:13px}
thead{background:var(--bg2)}
th{text-align:left;padding:12px 16px;font-size:11px;font-weight:800;color:var(--muted);text-transform:uppercase;letter-spacing:.8px;border-bottom:1px solid var(--border);white-space:nowrap}
td{padding:14px 16px;border-bottom:1px solid rgba(45,58,79,.5);vertical-align:middle}
tbody tr{transition:.15s}
tbody tr:hover{background:rgba(45,58,79,.3)}
tbody tr:last-child td{border-bottom:none}
.td-title{font-weight:700;color:var(--text);font-size:13px}
.td-sub{font-size:11px;color:var(--muted);margin-top:2px;word-break:break-all}
.thumb{width:44px;height:44px;border-radius:10px;object-fit:cover;background:var(--bg2);display:flex;align-items:center;justify-content:center;font-size:20px;flex-shrink:0;overflow:hidden;border:1px solid var(--border)}
.thumb img{width:100%;height:100%;object-fit:cover}

/* ====== BADGES ====== */
.badge{display:inline-flex;align-items:center;gap:5px;padding:4px 10px;border-radius:999px;font-size:11px;font-weight:700;white-space:nowrap}
.badge-green{background:rgba(16,185,129,.15);color:var(--green)}
.badge-amber{background:rgba(245,158,11,.15);color:var(--amber)}
.badge-red{background:rgba(239,68,68,.15);color:var(--red)}
.badge-blue{background:rgba(59,130,246,.15);color:var(--blue)}
.badge-purple{background:rgba(124,58,237,.15);color:var(--primary-light)}
.badge-gray{background:rgba(100,116,139,.15);color:var(--muted)}

/* ====== FORMS ====== */
.form-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:16px}
.field{margin-bottom:16px}
.field label{display:block;font-size:12px;font-weight:700;color:var(--muted);margin-bottom:6px;text-transform:uppercase;letter-spacing:.5px}
.field label .req{color:var(--accent)}
.field .hint{font-size:11px;color:var(--muted2);margin-top:4px;font-weight:500}
.switch{position:relative;display:inline-flex;align-items:center;gap:10px;cursor:pointer;user-select:none}
.switch input{display:none}
.switch-track{width:44px;height:24px;border-radius:999px;background:var(--border-light);position:relative;transition:.25s;flex-shrink:0}
.switch-track::after{content:'';position:absolute;top:3px;left:3px;width:18px;height:18px;border-radius:50%;background:#fff;transition:.25s;box-shadow:0 1px 3px rgba(0,0,0,.3)}
.switch input:checked + .switch-track{background:var(--green)}
.switch input:checked + .switch-track::after{transform:translateX(20px)}
.switch-label{font-size:13px;font-weight:600}

/* ====== MODAL ====== */
.modal{position:fixed;inset:0;z-index:100;display:none;align-items:center;justify-content:center;background:rgba(0,0,0,.75);backdrop-filter:blur(6px);padding:16px}
.modal.show{display:flex;animation:fadeIn .2s}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
.modal-card{background:var(--card);border:1px solid var(--border);border-radius:20px;width:100%;max-width:600px;max-height:92vh;overflow-y:auto;box-shadow:0 25px 50px -12px rgba(0,0,0,.7);position:relative;animation:modalScale .25s cubic-bezier(.34,1.56,.64,1)}
@keyframes modalScale{from{transform:scale(.94);opacity:0}to{transform:scale(1);opacity:1}}
.modal-head{padding:20px 24px;border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;background:var(--card);z-index:2;border-radius:20px 20px 0 0}
.modal-head h2{font-size:17px;font-weight:800;letter-spacing:-0.3px}
.modal-close{width:32px;height:32px;border-radius:8px;background:var(--bg);display:flex;align-items:center;justify-content:center;color:var(--muted);transition:.2s}
.modal-close:hover{background:var(--red);color:#fff}
.modal-body{padding:24px}
.modal-foot{padding:16px 24px;border-top:1px solid var(--border);display:flex;justify-content:flex-end;gap:10px;flex-wrap:wrap;position:sticky;bottom:0;background:var(--card);border-radius:0 0 20px 20px}

/* ====== TOAST ====== */
.toast-wrap{position:fixed;top:20px;right:20px;z-index:200;display:flex;flex-direction:column;gap:10px;max-width:360px}
.toast{background:var(--card);border:1px solid var(--border);border-left:4px solid var(--primary);border-radius:10px;padding:14px 18px;box-shadow:var(--shadow-lg);animation:slideInRight .3s;display:flex;align-items:center;gap:12px;font-size:13px;font-weight:600}
.toast.success{border-left-color:var(--green)}
.toast.error{border-left-color:var(--red)}
.toast.warning{border-left-color:var(--amber)}
.toast .t-icon{font-size:18px;flex-shrink:0}
@keyframes slideInRight{from{opacity:0;transform:translateX(40px)}to{opacity:1;transform:translateX(0)}}

/* ====== IMAGE ANIMATIONS ====== */
.img-preview{width:100%;aspect-ratio:16/9;border-radius:12px;overflow:hidden;background:var(--bg2);border:1px dashed var(--border);display:flex;align-items:center;justify-content:center;margin-top:8px;position:relative}
.img-preview img{width:100%;height:100%;object-fit:cover;animation:imgZoom 6s ease-in-out infinite}
@keyframes imgZoom{0%,100%{transform:scale(1)}50%{transform:scale(1.08)}}
.img-preview .placeholder{color:var(--muted2);font-size:12px;text-align:center;padding:20px}
.ad-card{background:var(--bg2);border:1px solid var(--border);border-radius:12px;overflow:hidden;position:relative;transition:.25s}
.ad-card:hover{border-color:var(--primary);transform:translateY(-2px)}
.ad-card .ad-img{aspect-ratio:16/7;overflow:hidden;position:relative}
.ad-card .ad-img img{width:100%;height:100%;object-fit:cover;animation:imgZoom 8s ease-in-out infinite}
.ad-card .ad-body{padding:12px}
.ad-card .ad-url{font-size:11px;color:var(--muted);word-break:break-all;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;min-height:32px}
.ad-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:14px}

/* ====== EMPTY ====== */
.empty{text-align:center;padding:60px 20px;color:var(--muted)}
.empty-icon{font-size:56px;margin-bottom:16px;opacity:.5}
.empty h3{font-size:16px;font-weight:800;color:var(--text);margin-bottom:6px}
.empty p{font-size:13px;max-width:320px;margin:0 auto}

/* ====== PAGE ANIM ====== */
.page-enter{animation:pageEnter .35s ease both}
@keyframes pageEnter{from{opacity:0;transform:translateY(12px)}to{opacity:1;transform:translateY(0)}}

/* ====== PLAN EDITOR ====== */
.plan-row{display:grid;grid-template-columns:1.2fr 1fr 1fr auto;gap:8px;margin-bottom:8px;align-items:center}
.plan-row input{padding:8px 10px;font-size:12px}

/* ====== PRODUCT CARD ====== */
.product-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:16px}
.prod-card{background:var(--card);border:1px solid var(--border);border-radius:16px;overflow:hidden;transition:.3s}
.prod-card:hover{transform:translateY(-3px);box-shadow:var(--shadow-lg);border-color:rgba(124,58,237,.4)}
.prod-img{aspect-ratio:16/9;overflow:hidden;background:var(--bg2);position:relative}
.prod-img img{width:100%;height:100%;object-fit:cover;animation:imgZoom 8s ease-in-out infinite}
.prod-img .fallback{display:flex;align-items:center;justify-content:center;height:100%;font-size:56px}
.prod-img .badge{position:absolute;top:10px}
.prod-body{padding:16px}

/* ====== MOBILE ====== */
.sidebar-overlay{position:fixed;inset:0;background:rgba(0,0,0,.6);z-index:45;display:none;backdrop-filter:blur(4px)}
.sidebar-overlay.show{display:block}
@media(max-width:900px){
  .sidebar{transform:translateX(-100%)}
  .sidebar.open{transform:translateX(0)}
  .main-content{margin-left:0}
  .menu-toggle{display:flex}
  .content-area{padding:16px}
}
@media(max-width:600px){
  .topbar{padding:0 14px;height:58px}
  .page-heading h1{font-size:15px}
  .page-heading p{display:none}
  .content-area{padding:12px}
  .stats-grid{grid-template-columns:repeat(2,1fr);gap:10px}
  .stat-card{padding:14px}
  .stat-card .stat-val{font-size:22px}
  .stat-card .stat-icon{width:36px;height:36px;font-size:16px;margin-bottom:10px}
  .form-grid{grid-template-columns:1fr}
  .modal-card{max-width:100%;border-radius:16px}
  .modal-body{padding:18px}
  .toast-wrap{left:12px;right:12px;max-width:none}
  .plan-row{grid-template-columns:1fr 1fr 1fr auto}
}
@media(max-width:380px){
  .stats-grid{grid-template-columns:1fr}
  .plan-row{grid-template-columns:1fr 1fr auto}
  .plan-row input:nth-child(3){grid-column:span 2}
}
</style>
</head>
<body>

<div class="sidebar-overlay" id="sidebarOverlay" onclick="toggleSidebar()"></div>

<div class="app-layout">
  <!-- SIDEBAR -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-brand">
      <div class="brand-logo" id="brandLogo">PB</div>
      <div style="min-width:0">
        <div class="brand-title" id="brandTitle">Panel Bajar</div>
        <div class="brand-sub">Admin Panel</div>
      </div>
    </div>
    <nav class="sidebar-nav" id="sidebarNav">
      <div class="nav-section-title">Main</div>
      <div class="sidebar-item active" data-page="dashboard" onclick="navigate('dashboard')">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="9" rx="1"/><rect x="14" y="3" width="7" height="5" rx="1"/><rect x="14" y="12" width="7" height="9" rx="1"/><rect x="3" y="16" width="7" height="5" rx="1"/></svg>
        <span>Dashboard</span>
      </div>
      <div class="sidebar-item" data-page="orders" onclick="navigate('orders')">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M6 2l1 4h12l-2 8H8L6 2zM6 2H4M9 18a1 1 0 100 2 1 1 0 000-2zM17 18a1 1 0 100 2 1 1 0 000-2z"/></svg>
        <span>Orders</span>
        <span class="badge-count" id="pendingBadge">0</span>
      </div>
      <div class="nav-section-title">Catalog</div>
      <div class="sidebar-item" data-page="products" onclick="navigate('products')">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"/></svg>
        <span>Products</span>
      </div>
      <div class="sidebar-item" data-page="ads" onclick="navigate('ads')">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="3" y="5" width="18" height="14" rx="2"/><path d="M3 10h18"/></svg>
        <span>Ads Slider</span>
      </div>
      <div class="nav-section-title">Users</div>
      <div class="sidebar-item" data-page="users" onclick="navigate('users')">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="9" cy="8" r="4"/><path d="M2 21c0-4 3-7 7-7s7 3 7 7M17 4a4 4 0 010 8M22 21c0-3-2-5-4-6"/></svg>
        <span>Users</span>
      </div>
      <div class="nav-section-title">Settings</div>
      <div class="sidebar-item" data-page="settings" onclick="navigate('settings')">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 11-2.83 2.83l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 11-4 0v-.09a1.65 1.65 0 00-1-1.51 1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 11-2.83-2.83l.06-.06a1.65 1.65 0 00.33-1.82 1.65 1.65 0 00-1.51-1H3a2 2 0 110-4h.09a1.65 1.65 0 001.51-1 1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 112.83-2.83l.06.06a1.65 1.65 0 001.82.33H9a1.65 1.65 0 001-1.51V3a2 2 0 114 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 112.83 2.83l-.06.06a1.65 1.65 0 00-.33 1.82V9a1.65 1.65 0 001.51 1H21a2 2 0 110 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>
        <span>Site Settings</span>
      </div>
    </nav>
    <div class="sidebar-foot">
      <div class="admin-profile">
        <div class="admin-avatar">A</div>
        <div style="min-width:0;flex:1">
          <div class="admin-name" id="adminName">Admin</div>
          <div class="admin-role">● Administrator</div>
        </div>
      </div>
      <button class="btn-logout" onclick="logout()">
        <svg width="16" height="16" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4M16 17l5-5-5-5M21 12H9"/></svg>
        Logout
      </button>
    </div>
  </aside>

  <!-- MAIN -->
  <div class="main-content">
    <header class="topbar">
      <div class="topbar-left">
        <button class="menu-toggle" onclick="toggleSidebar()">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 6h18M3 12h18M3 18h18"/></svg>
        </button>
        <div class="page-heading">
          <h1 id="pageTitle">Dashboard</h1>
          <p id="pageSubtitle">Welcome back, Admin</p>
        </div>
      </div>
      <div class="topbar-right">
        <div class="status-pill online" id="storeStatus">
          <span class="status-dot"></span> online
        </div>
        <button class="icon-btn" onclick="navigate('settings')" title="Settings">
          <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 11-2.83 2.83l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 11-4 0v-.09a1.65 1.65 0 00-1-1.51 1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 11-2.83-2.83l.06-.06a1.65 1.65 0 00.33-1.82 1.65 1.65 0 00-1.51-1H3a2 2 0 110-4h.09a1.65 1.65 0 001.51-1 1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 112.83-2.83l.06.06a1.65 1.65 0 001.82.33H9a1.65 1.65 0 001-1.51V3a2 2 0 114 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 112.83 2.83l-.06.06a1.65 1.65 0 00-.33 1.82V9a1.65 1.65 0 001.51 1H21a2 2 0 110 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>
        </button>
      </div>
    </header>

    <main class="content-area">
      <div class="content-inner" id="contentArea"></div>
    </main>
  </div>
</div>

<div class="modal" id="modal" onclick="if(event.target===this)closeModal()">
  <div class="modal-card" id="modalContent"></div>
</div>
<div class="toast-wrap" id="toastWrap"></div>

<script>
var FIREBASE_CONFIG = {
  apiKey: "AIzaSyDt3gU-2iubzCZ94XFAGZswUnzxuDgUvFQ",
  authDomain: "free-fire-panel-611d6.firebaseapp.com",
  projectId: "free-fire-panel-611d6",
  storageBucket: "free-fire-panel-611d6.firebasestorage.app",
  messagingSenderId: "374641641780",
  appId: "1:374641641780:web:c87d374edf2371dae47d61",
  databaseURL: ""
};
</script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
<script>
/* ================= FIREBASE ================= */
let fbDb=null, fbConnected=false, syncStarted=false;
function initFirebase(){
  try{
    if(typeof firebase==='undefined' || fbConnected) return fbConnected;
    if(!firebase.apps.length){
      firebase.initializeApp({
        apiKey:FIREBASE_CONFIG.apiKey, authDomain:FIREBASE_CONFIG.authDomain,
        projectId:FIREBASE_CONFIG.projectId, storageBucket:FIREBASE_CONFIG.storageBucket,
        messagingSenderId:FIREBASE_CONFIG.messagingSenderId, appId:FIREBASE_CONFIG.appId
      });
    }
    fbDb=firebase.firestore(); fbConnected=true; return true;
  }catch(e){ console.warn(e); return false; }
}
function fbDoc(col){ return fbDb.collection(col).doc('main'); }
function fbSave(col, arr){
  if(!fbConnected) return Promise.resolve(false);
  try{
    return fbDoc(col).set({data:JSON.stringify(arr), updatedAt:new Date().toISOString()}).then(()=>true).catch(e=>{console.warn(e);return false;});
  }catch(e){ return Promise.resolve(false); }
}
function fbLoad(col, cb){
  if(!fbConnected){ cb && cb(null); return; }
  try{
    fbDoc(col).get().then(doc=>{
      if(doc.exists){ try{ cb && cb(JSON.parse(doc.data().data||'[]')); }catch(e){ cb && cb(null); } }
      else cb && cb(null);
    }).catch(()=>cb && cb(null));
  }catch(e){ cb && cb(null); }
}
function fbListen(col, cb){
  if(!fbConnected) return;
  try{
    fbDoc(col).onSnapshot(doc=>{
      if(doc.exists){ try{ cb && cb(JSON.parse(doc.data().data||'[]')); }catch(e){} }
    });
  }catch(e){}
}

/* ================= DEFAULT ================= */
const DEFAULT_SETTINGS = {
  site_name:'Panel Bajar', tagline:'Buy Premium Mods & Hacks',
  notification:'স্বাগতম Panel Bajar-এ!', notif_active:true,
  offer_text:'🔥 MEGA অফার! সব প্রোডাক্টে ৫০% ছাড়!', offer_active:true,
  telegram:'https://t.me/panelbajar', youtube:'https://youtube.com/@panelbajar',
  bkash_number:'01XXXXXXXXX', help_url:'https://t.me/panelbajar',
  ads:[], ad_delay:3000,
  is_online:true, logo_url:'#', logo_image:'',
  online_start:'00:00', online_end:'23:59', whatsapp_number:'8801700000000',
  welcome_active:false, welcome_image:'', welcome_text:'ভিডিওটি শুরু থেকে শেষ পর্যন্ত দেখুন, যাতে পেমেন্ট করতে বা প্যানেল কিনতে কোনো সমস্যা না হয়।', welcome_link:'',
  telegram_bot_token:'', telegram_chat_id:'' // নতুন যোগ করা হলো
};

let state = {
  admin: JSON.parse(localStorage.getItem('pb_admin')||'null'),
  users: JSON.parse(localStorage.getItem('pb_users')||'[]'),
  products: JSON.parse(localStorage.getItem('pb_products')||'[]'),
  orders: JSON.parse(localStorage.getItem('pb_orders')||'[]'),
  settings: {...DEFAULT_SETTINGS, ...JSON.parse(localStorage.getItem('pb_settings')||'{}')},
  page:'dashboard',
  orderFilter:'ALL',
  productFilter:'ALL',
  userFilter:'ALL'
};

const PAGES = {
  dashboard:{title:'Dashboard',subtitle:'Welcome back, Admin'},
  orders:{title:'Order Management',subtitle:'Manage all customer orders'},
  products:{title:'Products',subtitle:'Manage your product catalog'},
  ads:{title:'Ads Slider',subtitle:'Manage homepage ad banners'},
  users:{title:'Users',subtitle:'Manage registered users'},
  settings:{title:'Site Settings',subtitle:'Configure your store — syncs live to user panel'}
};

function saveLocal(){
  try{
    localStorage.setItem('pb_admin', JSON.stringify(state.admin));
    localStorage.setItem('pb_users', JSON.stringify(state.users));
    localStorage.setItem('pb_products', JSON.stringify(state.products));
    localStorage.setItem('pb_orders', JSON.stringify(state.orders));
    localStorage.setItem('pb_settings', JSON.stringify(state.settings));
  }catch(e){}
}
function uid(){ return Date.now().toString(36)+Math.random().toString(36).slice(2,7); }
function $(id){ return document.getElementById(id); }
function esc(s){ return String(s==null?'':s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c])); }
function fmt(n){ return '৳'+Number(n||0).toFixed(0); }
function dateStr(d){ try{ return new Date(d).toLocaleString('en-GB',{day:'2-digit',month:'short',year:'numeric',hour:'2-digit',minute:'2-digit'}); }catch(e){ return ''; } }

function toast(msg, type){
  const wrap=$('toastWrap');
  const icons={success:'✅',error:'❌',warning:'⚠️',info:'ℹ️'};
  const el=document.createElement('div');
  el.className='toast '+(type||'info');
  el.innerHTML='<span class="t-icon">'+(icons[type]||icons.info)+'</span><span>'+esc(msg)+'</span>';
  wrap.appendChild(el);
  setTimeout(()=>{ el.style.transition='opacity .3s,transform .3s'; el.style.opacity='0'; el.style.transform='translateX(40px)'; setTimeout(()=>el.remove(),300); }, 3000);
}

/* ================= AUTH ================= */
function tryLogin(email, password){
  const found = state.users.find(u=>u.email===email && u.password===password && u.role==='ADMIN');
  if(found){
    state.admin={id:found.id,email:found.email,username:found.username,role:'ADMIN'};
    localStorage.setItem('pb_admin',JSON.stringify(state.admin));
    return true;
  }
  if((state.users.length===0 || !state.users.find(u=>u.role==='ADMIN')) && email==='admin@panelbajar.com' && password==='admin123'){
    state.admin={id:'admin',email,username:'Admin',role:'ADMIN'};
    localStorage.setItem('pb_admin',JSON.stringify(state.admin));
    return true;
  }
  return false;
}
function doLogin(){
  const e=$('loginEmail').value.trim().toLowerCase();
  const p=$('loginPassword').value;
  if(!e||!p){ toast('Fill all fields','error'); return; }
  if(tryLogin(e,p)){ toast('Welcome back!','success'); setTimeout(()=>location.reload(), 400); }
  else toast('Invalid credentials','error');
}
function logout(){
  if(!confirm('Logout from admin panel?')) return;
  state.admin=null; localStorage.removeItem('pb_admin');
  location.reload();
}
function renderLogin(){
  document.body.innerHTML = `
  <div style="min-height:100vh;display:flex;align-items:center;justify-content:center;padding:20px;background:radial-gradient(circle at 30% 20%,#1a2332,#0a0f1c)">
    <div style="width:100%;max-width:400px">
      <div style="text-align:center;margin-bottom:28px">
        <div style="width:64px;height:64px;border-radius:18px;background:linear-gradient(135deg,#7c3aed,#e11d48);display:flex;align-items:center;justify-content:center;font-weight:900;color:#fff;font-size:26px;margin:0 auto 16px;box-shadow:0 0 24px rgba(124,58,237,0.5)">PB</div>
        <h1 style="font-size:24px;font-weight:900;letter-spacing:-0.5px;color:#f1f5f9">Panel Bajar</h1>
        <p style="font-size:13px;color:#94a3b8;margin-top:4px">Admin Panel Login</p>
      </div>
      <div style="background:#1a2332;border:1px solid #2d3a4f;border-radius:16px;padding:24px">
        <div style="margin-bottom:16px">
          <label style="display:block;font-size:12px;font-weight:700;color:#94a3b8;margin-bottom:6px;text-transform:uppercase">Email</label>
          <input id="loginEmail" type="email" placeholder="admin@panelbajar.com" style="background:#0a0f1c;border:1px solid #2d3a4f;color:#f1f5f9;border-radius:10px;padding:12px 14px;width:100%;font-size:14px">
        </div>
        <div style="margin-bottom:20px">
          <label style="display:block;font-size:12px;font-weight:700;color:#94a3b8;margin-bottom:6px;text-transform:uppercase">Password</label>
          <input id="loginPassword" type="password" placeholder="••••••••" onkeydown="if(event.key==='Enter')doLogin()" style="background:#0a0f1c;border:1px solid #2d3a4f;color:#f1f5f9;border-radius:10px;padding:12px 14px;width:100%;font-size:14px">
        </div>
        <button onclick="doLogin()" style="width:100%;padding:13px;border-radius:10px;background:linear-gradient(135deg,#7c3aed,#5b21b6);color:#fff;font-weight:700;font-size:14px;border:none;cursor:pointer;box-shadow:0 4px 12px rgba(124,58,237,.3)">Sign In →</button>
        <p style="text-align:center;font-size:11px;color:#64748b;margin-top:16px">Default: admin@panelbajar.com / admin123</p>
      </div>
    </div>
  </div>`;
}

/* ================= SIDEBAR ================= */
function toggleSidebar(){
  $('sidebar').classList.toggle('open');
  $('sidebarOverlay').classList.toggle('show');
}
function navigate(page){
  if(page===state.page) return;
  state.page=page;
  render();
  if(window.innerWidth<=900) toggleSidebar();
}

/* ================= RENDER ================= */
function render(){
  if(!state.admin){ renderLogin(); return; }
  
  document.querySelectorAll('.sidebar-item').forEach(el=>{
    el.classList.toggle('active', el.dataset.page===state.page);
  });
  const pg=PAGES[state.page]||PAGES.dashboard;
  $('pageTitle').textContent=pg.title;
  $('pageSubtitle').textContent=pg.subtitle;
  $('adminName').textContent=state.admin.username||'Admin';
  $('brandTitle').textContent=state.settings.site_name||'Panel Bajar';
  
  const logo=$('brandLogo');
  if(state.settings.logo_image && state.settings.logo_image.trim()){
    logo.innerHTML=`<img src="${esc(state.settings.logo_image)}" onerror="this.style.display='none';this.parentElement.textContent='PB'">`;
  } else logo.textContent='PB';
  
  const pending=state.orders.filter(o=>o.status==='PENDING').length;
  $('pendingBadge').textContent=pending;
  $('pendingBadge').style.display=pending>0?'inline-block':'none';
  
  const online=state.settings.is_online!==false;
  const sp=$('storeStatus');
  sp.className='status-pill '+(online?'online':'offline');
  sp.innerHTML='<span class="status-dot"></span> '+(online?'online':'offline');
  
  let html='';
  switch(state.page){
    case 'dashboard': html=renderDashboard(); break;
    case 'orders':    html=renderOrders();    break;
    case 'products':  html=renderProducts();  break;
    case 'ads':       html=renderAds();       break;
    case 'users':     html=renderUsers();     break;
    case 'settings':  html=renderSettings();  break;
    default:          html=renderDashboard();
  }
  $('contentArea').innerHTML=html;
  window.scrollTo(0,0);
}

/* ================= DASHBOARD ================= */
function renderDashboard(){
  const totalUsers=state.users.filter(u=>u.role!=='ADMIN').length;
  const totalOrders=state.orders.length;
  const pendingOrders=state.orders.filter(o=>o.status==='PENDING').length;
  const completedOrders=state.orders.filter(o=>o.status==='COMPLETED').length;
  const revenue=state.orders.filter(o=>o.status==='COMPLETED').reduce((s,o)=>s+(o.price||0),0);
  const recentOrders=state.orders.slice().reverse().slice(0,6);

  return `
  <div class="page-enter">
    <div class="stats-grid">
      <div class="stat-card c-purple">
        <div class="stat-icon"><svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"/></svg></div>
        <div class="stat-label">Products</div>
        <div class="stat-val">${state.products.length}</div>
        <div class="stat-sub">${state.products.filter(p=>p.status==='ACTIVE').length} active</div>
      </div>
      <div class="stat-card c-blue">
        <div class="stat-icon"><svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="9" cy="8" r="4"/><path d="M2 21c0-4 3-7 7-7s7 3 7 7"/></svg></div>
        <div class="stat-label">Users</div>
        <div class="stat-val">${totalUsers}</div>
        <div class="stat-sub">${state.users.filter(u=>u.banned).length} banned</div>
      </div>
      <div class="stat-card c-amber">
        <div class="stat-icon"><svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M6 2l1 4h12l-2 8H8L6 2zM6 2H4M9 18a1 1 0 100 2 1 1 0 000-2zM17 18a1 1 0 100 2 1 1 0 000-2z"/></svg></div>
        <div class="stat-label">Total Orders</div>
        <div class="stat-val">${totalOrders}</div>
        <div class="stat-sub">${pendingOrders} pending · ${completedOrders} done</div>
      </div>
      <div class="stat-card c-green">
        <div class="stat-icon"><svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M12 1v22M17 5H9.5a3.5 3.5 0 000 7h5a3.5 3.5 0 010 7H6"/></svg></div>
        <div class="stat-label">Revenue</div>
        <div class="stat-val">${fmt(revenue)}</div>
        <div class="stat-sub">Completed only</div>
      </div>
      <div class="stat-card c-red">
        <div class="stat-icon"><svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 8v4M12 16h.01"/></svg></div>
        <div class="stat-label">Pending</div>
        <div class="stat-val" style="color:var(--amber)">${pendingOrders}</div>
        <div class="stat-sub">Awaiting approval</div>
      </div>
      <div class="stat-card c-cyan">
        <div class="stat-icon"><svg width="22" height="22" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><rect x="2" y="5" width="20" height="14" rx="2"/><path d="M2 10h20"/></svg></div>
        <div class="stat-label">Ads</div>
        <div class="stat-val">${(state.settings.ads||[]).length}</div>
        <div class="stat-sub">Slider banners</div>
      </div>
    </div>

    <div style="display:grid;grid-template-columns:1fr;gap:20px">
      <div class="card">
        <div class="card-head">
          <div><h3>📋 Recent Orders</h3><p>Latest customer orders</p></div>
          <button class="btn btn-ghost btn-sm" onclick="navigate('orders')">View All →</button>
        </div>
        ${recentOrders.length===0?`<div class="empty"><div class="empty-icon">📭</div><h3>No orders yet</h3><p>Orders will appear here once customers start buying.</p></div>`:`
        <div style="overflow-x:auto">
          <table>
            <thead><tr><th>Product</th><th>User</th><th>Amount</th><th>Status</th><th>Date</th></tr></thead>
            <tbody>
              ${recentOrders.map(o=>{
                const p=state.products.find(x=>x.id===o.productId);
                const u=state.users.find(x=>x.id===o.userId);
                return `<tr>
                  <td><div style="display:flex;align-items:center;gap:10px"><div class="thumb">${p?.image?`<img src="${esc(p.image)}" onerror="this.style.display='none';this.parentElement.textContent='${esc(p.icon||'📦')}'">`:(p?.icon||'📦')}</div><div><div class="td-title">${esc(p?.name||'Deleted')}</div><div class="td-sub">${esc(o.planDur||'')}</div></div></div></td>
                  <td><div class="td-title">${esc(u?.username||'Unknown')}</div></td>
                  <td><div class="td-title" style="color:var(--green)">${fmt(o.price)}</div></td>
                  <td><span class="badge ${o.status==='COMPLETED'?'badge-green':o.status==='PENDING'?'badge-amber':'badge-red'}">${esc(o.status)}</span></td>
                  <td><div class="td-sub">${esc(dateStr(o.createdAt))}</div></td>
                </tr>`;
              }).join('')}
            </tbody>
          </table>
        </div>`}
      </div>

      <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px">
        <div class="card card-pad">
          <h3 style="font-size:14px;font-weight:800;margin-bottom:14px">⚡ Quick Actions</h3>
          <div style="display:flex;flex-direction:column;gap:10px">
            <button class="btn btn-primary" onclick="openProductModal()">+ Add New Product</button>
            <button class="btn btn-accent" onclick="openAdModal()">+ Add Ad Banner</button>
            <button class="btn btn-ghost" onclick="navigate('orders')">Review Pending Orders (${pendingOrders})</button>
            <button class="btn btn-ghost" onclick="navigate('settings')">Edit Site Settings</button>
          </div>
        </div>
        <div class="card card-pad">
          <h3 style="font-size:14px;font-weight:800;margin-bottom:14px">🛒 Store Status</h3>
          <div style="display:flex;flex-direction:column;gap:14px">
            <label class="switch">
              <input type="checkbox" ${state.settings.is_online!==false?'checked':''} onchange="toggleOnline(this.checked)">
              <span class="switch-track"></span>
              <span class="switch-label">Store is ${state.settings.is_online!==false?'Online':'Offline'}</span>
            </label>
            <div style="font-size:12px;color:var(--muted);line-height:1.6">
              When offline, Buy Now is blocked and users see a warning. Changes sync to user panel instantly.
            </div>
            <div style="padding-top:12px;border-top:1px solid var(--border);font-size:12px;color:var(--muted)">
              <strong style="color:var(--text)">bKash:</strong> ${esc(state.settings.bkash_number||'—')}<br>
              <strong style="color:var(--text)">WhatsApp:</strong> ${esc(state.settings.whatsapp_number||'—')}
            </div>
            <div style="padding-top:12px;border-top:1px solid var(--border);font-size:12px;color:var(--muted)">
              <strong style="color:var(--text)">Firebase:</strong> 
              <span class="badge ${fbConnected?'badge-green':'badge-red'}">${fbConnected?'✓ Connected':'✗ Offline'}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>`;
}

function toggleOnline(val){
  state.settings.is_online=val;
  saveLocal(); fbSave('settings',[state.settings]);
  toast(val?'Store is now ONLINE':'Store is now OFFLINE', val?'success':'warning');
  render();
}

/* ================= ORDERS ================= */
function renderOrders(){
  const filter=state.orderFilter||'ALL';
  let orders=state.orders.slice().reverse();
  if(filter!=='ALL') orders=orders.filter(o=>o.status===filter);
  
  const counts={
    ALL:state.orders.length,
    PENDING:state.orders.filter(o=>o.status==='PENDING').length,
    COMPLETED:state.orders.filter(o=>o.status==='COMPLETED').length,
    CANCELLED:state.orders.filter(o=>o.status==='CANCELLED').length
  };
  
  return `
  <div class="page-enter">
    <div style="display:flex;gap:8px;margin-bottom:18px;flex-wrap:wrap">
      ${['ALL','PENDING','COMPLETED','CANCELLED'].map(f=>`
        <button class="btn btn-sm ${filter===f?'btn-primary':'btn-ghost'}" onclick="state.orderFilter='${f}';render()">
          ${f} <span style="opacity:.7;margin-left:4px">(${counts[f]||0})</span>
        </button>`).join('')}
    </div>
    ${orders.length===0?`<div class="card"><div class="empty"><div class="empty-icon">📭</div><h3>No ${filter.toLowerCase()} orders</h3><p>Orders will appear here.</p></div></div>`:`
    <div class="card">
      <div style="overflow-x:auto;border-radius:16px">
        <table>
          <thead><tr><th>Order</th><th>User</th><th>Amount</th><th>Txn ID</th><th>Status</th><th>Date</th><th style="text-align:right">Actions</th></tr></thead>
          <tbody>
            ${orders.map(o=>{
              const p=state.products.find(x=>x.id===o.productId);
              const u=state.users.find(x=>x.id===o.userId);
              const statusBadge=o.status==='COMPLETED'?'badge-green':o.status==='PENDING'?'badge-amber':'badge-red';
              return `<tr>
                <td>
                  <div style="display:flex;align-items:center;gap:10px">
                    <div class="thumb">${p?.image?`<img src="${esc(p.image)}" onerror="this.style.display='none';this.parentElement.textContent='${esc(p.icon||'📦')}'">`:(p?.icon||'📦')}</div>
                    <div><div class="td-title">${esc(p?.name||'Deleted')}</div><div class="td-sub">${esc(o.planDur||'')}${o.qty>1?' × '+o.qty:''}</div></div>
                  </div>
                </td>
                <td><div class="td-title">${esc(u?.username||'Unknown')}</div><div class="td-sub">${esc(u?.email||'')}</div></td>
                <td><div class="td-title" style="color:var(--green)">${fmt(o.price)}</div></td>
                <td><div class="td-sub" style="font-family:monospace">${esc(o.txnId||'—')}</div></td>
                <td><span class="badge ${statusBadge}">${esc(o.status)}</span></td>
                <td><div class="td-sub">${esc(dateStr(o.createdAt))}</div></td>
                <td style="text-align:right">
                  <div style="display:flex;gap:6px;justify-content:flex-end">
                    ${o.status==='PENDING'?`<button class="btn btn-green btn-icon" title="Approve" onclick="openApproveModal('${o.id}')"><svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path d="M20 6L9 17l-5-5"/></svg></button>`:''}
                    ${o.status==='PENDING'?`<button class="btn btn-red btn-icon" title="Cancel" onclick="cancelOrder('${o.id}')"><svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24"><path d="M18 6L6 18M6 6l12 12"/></svg></button>`:''}
                    ${o.status==='COMPLETED'?`<button class="btn btn-blue btn-icon" title="View Key" onclick="viewOrderKey('${o.id}')"><svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/><circle cx="12" cy="12" r="3"/></svg></button>`:''}
                    <button class="btn btn-ghost btn-icon" title="Delete" onclick="deleteOrder('${o.id}')"><svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M3 6h18M8 6V4a2 2 0 012-2h4a2 2 0 012 2v2M19 6l-1 14a2 2 0 01-2 2H8a2 2 0 01-2-2L5 6"/></svg></button>
                  </div>
                </td>
              </tr>`;
            }).join('')}
          </tbody>
        </table>
      </div>
    </div>`}
  </div>`;
}

function openApproveModal(orderId){
  const o=state.orders.find(x=>x.id===orderId);
  if(!o) return;
  const p=state.products.find(x=>x.id===o.productId);
  openModal(`
    <div class="modal-head"><h2>✅ Approve Order</h2><button class="modal-close" onclick="closeModal()">✕</button></div>
    <div class="modal-body">
      <div style="background:var(--bg2);padding:14px;border-radius:12px;margin-bottom:18px;font-size:13px;line-height:1.7">
        <strong>${esc(p?.name||'Product')}</strong> · ${esc(o.planDur||'')}${o.qty>1?' × '+o.qty:''}<br>
        Amount: <strong style="color:var(--green)">${fmt(o.price)}</strong><br>
        Txn ID: <span style="font-family:monospace">${esc(o.txnId||'—')}</span>
      </div>
      <div class="field">
        <label>API Key / Code Content <span class="req">*</span></label>
        <textarea id="approveCode" placeholder="Enter the API key or code to deliver..."></textarea>
        <div class="hint">User sees this in "My Keys" tab after approval. Syncs instantly via Firebase.</div>
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
      <button class="btn btn-green" onclick="approveOrder('${orderId}')">✅ Approve & Deliver</button>
    </div>
  `);
}
function approveOrder(orderId){
  const code=$('approveCode').value.trim();
  if(!code){ toast('Enter the API key/code','error'); return; }
  const o=state.orders.find(x=>x.id===orderId);
  if(!o) return;
  o.status='COMPLETED';
  o.codeContent=code;
  o.completedAt=new Date().toISOString();
  const u=state.users.find(x=>x.id===o.userId);
  if(u){ u.totalOrders=(u.totalOrders||0)+1; u.totalSpent=(u.totalSpent||0)+(o.price||0); }
  saveLocal();
  fbSave('orders',state.orders);
  fbSave('users',state.users);
  closeModal();
  toast('Order approved & delivered!','success');
  render();
}
function cancelOrder(orderId){
  if(!confirm('Cancel this order?')) return;
  const o=state.orders.find(x=>x.id===orderId);
  if(!o) return;
  o.status='CANCELLED';
  saveLocal(); fbSave('orders',state.orders);
  toast('Order cancelled','warning');
  render();
}
function deleteOrder(orderId){
  if(!confirm('Permanently delete this order?')) return;
  state.orders=state.orders.filter(x=>x.id!==orderId);
  saveLocal(); fbSave('orders',state.orders);
  toast('Order deleted','error');
  render();
}
function viewOrderKey(orderId){
  const o=state.orders.find(x=>x.id===orderId);
  if(!o) return;
  openModal(`
    <div class="modal-head"><h2>🔑 Delivered Key</h2><button class="modal-close" onclick="closeModal()">✕</button></div>
    <div class="modal-body">
      <div style="background:var(--bg2);padding:16px;border-radius:12px;font-family:monospace;font-size:13px;word-break:break-all;border:1px solid var(--border)">
        ${esc(o.codeContent||'—')}
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeModal()">Close</button>
      <button class="btn btn-primary" onclick="copyText('${esc((o.codeContent||'').replace(/'/g,"\\'"))}')">📋 Copy</button>
    </div>
  `);
}

/* ================= PRODUCTS ================= */
function renderProducts(){
  const filter=state.productFilter||'ALL';
  let products=state.products.slice();
  if(filter!=='ALL') products=products.filter(p=>p.category===filter);
  
  return `
  <div class="page-enter">
    <div style="display:flex;gap:10px;margin-bottom:18px;flex-wrap:wrap;align-items:center;justify-content:space-between">
      <div style="display:flex;gap:6px;flex-wrap:wrap">
        ${['ALL','NON_ROOT','ROOT','IPHONE','PC'].map(f=>`
          <button class="btn btn-sm ${filter===f?'btn-primary':'btn-ghost'}" onclick="state.productFilter='${f}';render()">${f}</button>`).join('')}
      </div>
      <button class="btn btn-primary" onclick="openProductModal()">+ Add Product</button>
    </div>
    ${products.length===0?`<div class="card"><div class="empty"><div class="empty-icon">📦</div><h3>No products${filter!=='ALL'?' in '+filter:''}</h3><p>Click "Add Product" to create one.</p></div></div>`:`
    <div class="product-grid">
      ${products.map(p=>{
        const active=p.status==='ACTIVE';
        const plans=p.plans||[];
        const minPrice=plans.length?Math.min(...plans.map(x=>x.price)):0;
        return `<div class="prod-card">
          <div class="prod-img">
            ${p.image?`<img src="${esc(p.image)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div class=\\'fallback\\'>${esc(p.icon||'📦')}</div>'">`:`<div class="fallback">${esc(p.icon||'📦')}</div>`}
            <span class="badge ${active?'badge-green':'badge-gray'}" style="right:10px">${active?'Active':'Inactive'}</span>
            ${p.antiban?'<span class="badge badge-green" style="left:10px">Anti-Ban</span>':''}
          </div>
          <div class="prod-body">
            <div style="font-weight:800;font-size:14px;margin-bottom:4px">${esc(p.name)}</div>
            <div style="font-size:11px;color:var(--muted);margin-bottom:10px;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;min-height:32px">${esc(p.description||'')}</div>
            <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:12px">
              <div><span style="font-size:18px;font-weight:800;color:var(--primary-light)">${fmt(minPrice)}</span>${p.oldPrice?` <span style="font-size:11px;color:var(--muted);text-decoration:line-through">${fmt(p.oldPrice)}</span>`:''}</div>
              <span class="badge badge-purple">${esc(p.category||'—')}</span>
            </div>
            <div style="display:flex;gap:6px">
              <button class="btn btn-ghost btn-sm" style="flex:1" onclick="openProductModal('${p.id}')">Edit</button>
              <button class="btn ${active?'btn-amber':'btn-green'} btn-sm" style="flex:1" onclick="toggleProduct('${p.id}')">${active?'Hide':'Show'}</button>
              <button class="btn btn-red btn-icon btn-sm" onclick="deleteProduct('${p.id}')"><svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" style="width:14px;height:14px"><path d="M3 6h18M8 6V4a2 2 0 012-2h4a2 2 0 012 2v2"/></svg></button>
            </div>
          </div>
        </div>`;
      }).join('')}
    </div>`}
  </div>`;
}
function toggleProduct(pid){
  const p=state.products.find(x=>x.id===pid);
  if(!p) return;
  p.status=p.status==='ACTIVE'?'INACTIVE':'ACTIVE';
  saveLocal(); fbSave('products',state.products);
  toast(p.status==='ACTIVE'?'Product visible':'Product hidden','success');
  render();
}
function deleteProduct(pid){
  if(!confirm('Delete this product?')) return;
  state.products=state.products.filter(x=>x.id!==pid);
  saveLocal(); fbSave('products',state.products);
  toast('Product deleted','error');
  render();
}

let editingProductId=null;
function openProductModal(pid){
  editingProductId=pid||null;
  const p=pid?state.products.find(x=>x.id===pid):null;
  const plans=p?.plans?.length?p.plans:[{dur:'1 Day',price:0,stock:99}];
  openModal(`
    <div class="modal-head">
      <h2>${p?'✏️ Edit Product':'➕ Add Product'}</h2>
      <button class="modal-close" onclick="closeModal()">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-grid">
        <div class="field">
          <label>Product Name <span class="req">*</span></label>
          <input id="pmName" value="${esc(p?.name||'')}" placeholder="e.g. AIM HACK - ANDROID">
        </div>
        <div class="field">
          <label>Category <span class="req">*</span></label>
          <select id="pmCategory">
            ${['NON_ROOT','ROOT','IPHONE','PC'].map(c=>`<option value="${c}" ${p?.category===c?'selected':''}>${c}</option>`).join('')}
          </select>
        </div>
      </div>
      <div class="field">
        <label>Description</label>
        <input id="pmDesc" value="${esc(p?.description||'')}" placeholder="Short description shown on card">
      </div>
      <div class="form-grid">
        <div class="field">
          <label>Image URL</label>
          <input id="pmImage" value="${esc(p?.image||'')}" placeholder="https://... (empty for emoji)">
          <div class="img-preview" id="imgPreview">
            ${p?.image?`<img src="${esc(p.image)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div class=\\'placeholder\\'>Invalid image URL</div>'">`:`<div class="placeholder">🖼️ Image preview will appear here</div>`}
          </div>
        </div>
        <div class="field">
          <label>Emoji Icon (fallback)</label>
          <input id="pmIcon" value="${esc(p?.icon||'🎮')}" maxlength="4" style="font-size:20px;text-align:center" placeholder="🎮">
          <div style="margin-top:14px">
            <label>Old Price (sale badge)</label>
            <input id="pmOldPrice" type="number" value="${p?.oldPrice||''}" placeholder="0 = no sale">
          </div>
        </div>
      </div>
      <div style="display:flex;gap:20px;margin-bottom:16px;flex-wrap:wrap">
        <label class="switch"><input type="checkbox" id="pmAntiban" ${p?.antiban?'checked':''}><span class="switch-track"></span><span class="switch-label">Anti-Ban badge</span></label>
        <label class="switch"><input type="checkbox" id="pmMaintenance" ${p?.maintenance?'checked':''}><span class="switch-track"></span><span class="switch-label">Maintenance</span></label>
        <label class="switch"><input type="checkbox" id="pmActive" ${(!p||p.status==='ACTIVE')?'checked':''}><span class="switch-track"></span><span class="switch-label">Visible in store</span></label>
      </div>
      <div style="background:var(--bg2);border:1px solid var(--border);border-radius:12px;padding:16px;margin-bottom:16px">
        <div style="font-size:13px;font-weight:800;margin-bottom:12px">📦 Plans</div>
        <div id="plansList">
          ${plans.map((pl,i)=>renderPlanRow(pl,i)).join('')}
        </div>
        <button class="btn btn-ghost btn-sm" onclick="addPlanRow()" style="margin-top:10px">+ Add Plan</button>
      </div>
      <div style="border-top:1px solid var(--border);padding-top:16px">
        <div style="font-size:13px;font-weight:800;margin-bottom:12px">🔗 Setup / Download Links</div>
        <div class="form-grid">
          <div class="field"><label>Full Details Video</label><input id="pmUrlFull" value="${esc(p?.url_full_details||'')}" placeholder="https://youtube.com/..."></div>
          <div class="field"><label>Setup Video</label><input id="pmUrlSetup" value="${esc(p?.url_setup_video||'')}" placeholder="https://youtube.com/..."></div>
          <div class="field"><label>Download Link</label><input id="pmUrlDownload" value="${esc(p?.url_download||'')}" placeholder="https://..."></div>
          <div class="field"><label>iPhone Setup</label><input id="pmUrlIphone" value="${esc(p?.url_iphone_setup||'')}" placeholder="https://..."></div>
        </div>
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
      <button class="btn btn-primary" onclick="saveProduct()">💾 Save Product</button>
    </div>
  `);
  const imgInput=$('pmImage');
  if(imgInput) imgInput.addEventListener('input', function(){
    const v=this.value.trim();
    const prev=$('imgPreview');
    if(v) prev.innerHTML=`<img src="${esc(v)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div class=\\'placeholder\\'>Invalid image URL</div>'">`;
    else prev.innerHTML=`<div class="placeholder">🖼️ Image preview will appear here</div>`;
  });
}
function renderPlanRow(pl, idx){
  return `<div class="plan-row" data-idx="${idx}">
    <input placeholder="Duration" value="${esc(pl.dur||'')}" data-plan="dur">
    <input type="number" placeholder="Price" value="${pl.price||0}" data-plan="price">
    <input type="number" placeholder="Stock" value="${pl.stock||0}" data-plan="stock">
    <button class="btn btn-red btn-icon btn-sm" onclick="this.parentElement.remove()">✕</button>
  </div>`;
}
function addPlanRow(){
  const list=$('plansList');
  list.insertAdjacentHTML('beforeend', renderPlanRow({dur:'',price:0,stock:99}, list.children.length));
}
function collectPlans(){
  const rows=document.querySelectorAll('#plansList .plan-row');
  const plans=[];
  rows.forEach(r=>{
    const dur=r.querySelector('[data-plan="dur"]').value.trim();
    const price=Number(r.querySelector('[data-plan="price"]').value)||0;
    const stock=Number(r.querySelector('[data-plan="stock"]').value)||0;
    if(dur) plans.push({dur,price,stock});
  });
  return plans;
}
function saveProduct(){
  const name=$('pmName').value.trim();
  if(!name){ toast('Product name required','error'); return; }
  const plans=collectPlans();
  if(plans.length===0){ toast('Add at least one plan','error'); return; }
  
  const data={
    name,
    category:$('pmCategory').value,
    description:$('pmDesc').value.trim(),
    image:$('pmImage').value.trim(),
    icon:$('pmIcon').value.trim()||'🎮',
    oldPrice:Number($('pmOldPrice').value)||0,
    antiban:$('pmAntiban').checked,
    maintenance:$('pmMaintenance').checked,
    status:$('pmActive').checked?'ACTIVE':'INACTIVE',
    plans,
    url_full_details:$('pmUrlFull').value.trim(),
    url_setup_video:$('pmUrlSetup').value.trim(),
    url_download:$('pmUrlDownload').value.trim(),
    url_iphone_setup:$('pmUrlIphone').value.trim()
  };
  
  if(editingProductId){
    const p=state.products.find(x=>x.id===editingProductId);
    if(p) Object.assign(p,data);
    toast('Product updated','success');
  }else{
    state.products.push({id:uid(),createdAt:new Date().toISOString(),...data});
    toast('Product added','success');
  }
  saveLocal(); fbSave('products',state.products);
  closeModal(); render();
}

/* ================= ADS ================= */
function renderAds(){
  const ads=state.settings.ads||[];
  return `
  <div class="page-enter">
    <div style="display:flex;gap:10px;margin-bottom:18px;flex-wrap:wrap;align-items:center;justify-content:space-between">
      <div style="font-size:13px;color:var(--muted)">
        ${ads.length} banner${ads.length!==1?'s':''} · auto-slide every ${(state.settings.ad_delay||3000)/1000}s
      </div>
      <div style="display:flex;gap:8px">
        <button class="btn btn-ghost btn-sm" onclick="openAdDelayModal()">⚙️ Slide Delay</button>
        <button class="btn btn-primary" onclick="openAdModal()">+ Add Ad Banner</button>
      </div>
    </div>
    ${ads.length===0?`<div class="card"><div class="empty"><div class="empty-icon">🖼️</div><h3>No ad banners</h3><p>Add banners for animated slider on homepage.</p><button class="btn btn-primary" style="margin-top:16px" onclick="openAdModal()">+ Add Banner</button></div></div>`:`
    <div class="ad-grid">
      ${ads.map((ad,i)=>{
        const url=typeof ad==='string'?ad:(ad.url||'');
        const link=typeof ad==='object'?(ad.link||''):'';
        return `<div class="ad-card">
          <div class="ad-img">
            <img src="${esc(url)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div style=\\'display:flex;align-items:center;justify-content:center;height:100%;color:var(--muted2);font-size:12px\\'>Invalid image</div>'">
            <span class="badge badge-purple" style="position:absolute;top:8px;left:8px">#${i+1}</span>
          </div>
          <div class="ad-body">
            <div class="ad-url">${esc(url)}</div>
            ${link?`<div style="font-size:11px;color:var(--blue);margin-top:4px;word-break:break-all">🔗 ${esc(link)}</div>`:''}
            <div style="display:flex;gap:6px;margin-top:10px">
              <button class="btn btn-ghost btn-sm" style="flex:1" onclick="moveAd(${i},-1)" ${i===0?'disabled':''}>↑</button>
              <button class="btn btn-ghost btn-sm" style="flex:1" onclick="moveAd(${i},1)" ${i===ads.length-1?'disabled':''}>↓</button>
              <button class="btn btn-primary btn-sm" style="flex:1" onclick="openAdModal(${i})">Edit</button>
              <button class="btn btn-red btn-icon btn-sm" onclick="deleteAd(${i})">✕</button>
            </div>
          </div>
        </div>`;
      }).join('')}
    </div>`}
  </div>`;
}
function openAdModal(idx){
  const editing=idx!==undefined && idx!==null;
  const ads=state.settings.ads||[];
  const ad=editing?ads[idx]:null;
  const url=typeof ad==='string'?ad:(ad?.url||'');
  const link=typeof ad==='object'?(ad?.link||''):'';
  openModal(`
    <div class="modal-head"><h2>${editing?'✏️ Edit Banner':'🖼️ Add Banner'}</h2><button class="modal-close" onclick="closeModal()">✕</button></div>
    <div class="modal-body">
      <div class="field">
        <label>Image URL <span class="req">*</span></label>
        <input id="adUrl" value="${esc(url)}" placeholder="https://i.imgur.com/example.jpg">
        <div class="hint">Direct image URL. Recommended 1200×525px.</div>
        <div class="img-preview" id="adPreview">
          ${url?`<img src="${esc(url)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div class=\\'placeholder\\'>Invalid image URL</div>'">`:`<div class="placeholder">🖼️ Banner preview</div>`}
        </div>
      </div>
      <div class="field">
        <label>Click Link (optional)</label>
        <input id="adLink" value="${esc(link)}" placeholder="https://t.me/yourchannel">
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
      <button class="btn btn-primary" onclick="saveAd(${editing?idx:'null'})">💾 Save</button>
    </div>
  `);
  const inp=$('adUrl');
  if(inp) inp.addEventListener('input', function(){
    const v=this.value.trim();
    const prev=$('adPreview');
    if(v) prev.innerHTML=`<img src="${esc(v)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div class=\\'placeholder\\'>Invalid image URL</div>'">`;
    else prev.innerHTML=`<div class="placeholder">🖼️ Banner preview</div>`;
  });
}
function saveAd(idx){
  const url=$('adUrl').value.trim();
  const link=$('adLink').value.trim();
  if(!url){ toast('Image URL required','error'); return; }
  if(!Array.isArray(state.settings.ads)) state.settings.ads=[];
  const item={url,link};
  if(idx!==null && idx!==undefined){
    state.settings.ads[idx]=item;
    toast('Banner updated','success');
  }else{
    state.settings.ads.push(item);
    toast('Banner added','success');
  }
  saveLocal(); fbSave('settings',[state.settings]);
  closeModal(); render();
}
function deleteAd(idx){
  if(!confirm('Delete this banner?')) return;
  state.settings.ads.splice(idx,1);
  saveLocal(); fbSave('settings',[state.settings]);
  toast('Banner deleted','warning');
  render();
}
function moveAd(idx, dir){
  const ads=state.settings.ads;
  const ni=idx+dir;
  if(ni<0||ni>=ads.length) return;
  [ads[idx],ads[ni]]=[ads[ni],ads[idx]];
  saveLocal(); fbSave('settings',[state.settings]);
  render();
}
function openAdDelayModal(){
  const cur=(state.settings.ad_delay||3000)/1000;
  openModal(`
    <div class="modal-head"><h2>⚙️ Slider Timing</h2><button class="modal-close" onclick="closeModal()">✕</button></div>
    <div class="modal-body">
      <div class="field">
        <label>Auto-slide delay (seconds)</label>
        <input id="adDelay" type="number" min="1.5" step="0.5" value="${cur}">
        <div class="hint">How long each banner stays before sliding.</div>
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
      <button class="btn btn-primary" onclick="saveAdDelay()">💾 Save</button>
    </div>
  `);
}
function saveAdDelay(){
  const v=parseFloat($('adDelay').value);
  if(!v||v<1.5){ toast('Minimum 1.5s','error'); return; }
  state.settings.ad_delay=Math.round(v*1000);
  saveLocal(); fbSave('settings',[state.settings]);
  toast('Slider timing updated','success');
  closeModal(); render();
}

/* ================= USERS ================= */
function renderUsers(){
  const filter=state.userFilter||'ALL';
  let users=state.users.slice().reverse();
  if(filter==='ADMIN') users=users.filter(u=>u.role==='ADMIN');
  else if(filter==='USER') users=users.filter(u=>u.role!=='ADMIN');
  else if(filter==='BANNED') users=users.filter(u=>u.banned);
  
  return `
  <div class="page-enter">
    <div style="display:flex;gap:8px;margin-bottom:18px;flex-wrap:wrap">
      ${['ALL','USER','ADMIN','BANNED'].map(f=>`
        <button class="btn btn-sm ${filter===f?'btn-primary':'btn-ghost'}" onclick="state.userFilter='${f}';render()">${f}</button>`).join('')}
    </div>
    ${users.length===0?`<div class="card"><div class="empty"><div class="empty-icon">👥</div><h3>No users</h3></div></div>`:`
    <div class="card">
      <div style="overflow-x:auto;border-radius:16px">
        <table>
          <thead><tr><th>User</th><th>Role</th><th>Orders</th><th>Spent</th><th>Joined</th><th>Status</th><th style="text-align:right">Actions</th></tr></thead>
          <tbody>
            ${users.map(u=>`
              <tr>
                <td>
                  <div style="display:flex;align-items:center;gap:10px">
                    <div class="thumb" style="background:${esc(u.avatarColor||'#7c3aed')};color:#fff;font-weight:800;font-size:14px">${esc((u.username||'?').slice(0,2).toUpperCase())}</div>
                    <div><div class="td-title">${esc(u.username||'—')}</div><div class="td-sub">${esc(u.email||'')}</div></div>
                  </div>
                </td>
                <td><span class="badge ${u.role==='ADMIN'?'badge-purple':'badge-blue'}">${esc(u.role||'USER')}</span></td>
                <td><div class="td-title">${u.totalOrders||0}</div></td>
                <td><div class="td-title" style="color:var(--green)">${fmt(u.totalSpent||0)}</div></td>
                <td><div class="td-sub">${esc(dateStr(u.createdAt))}</div></td>
                <td><span class="badge ${u.banned?'badge-red':'badge-green'}">${u.banned?'Banned':'Active'}</span></td>
                <td style="text-align:right">
                  <div style="display:flex;gap:6px;justify-content:flex-end">
                    <button class="btn ${u.banned?'btn-green':'btn-amber'} btn-sm" onclick="toggleBan('${u.id}')">${u.banned?'Unban':'Ban'}</button>
                    <button class="btn btn-red btn-icon btn-sm" onclick="deleteUser('${u.id}')"><svg fill="none" stroke="currentColor" stroke-width="2.5" viewBox="0 0 24 24" style="width:14px;height:14px"><path d="M3 6h18M8 6V4a2 2 0 012-2h4a2 2 0 012 2v2"/></svg></button>
                  </div>
                </td>
              </tr>`).join('')}
          </tbody>
        </table>
      </div>
    </div>`}
  </div>`;
}
function toggleBan(uid){
  const u=state.users.find(x=>x.id===uid);
  if(!u) return;
  if(u.role==='ADMIN'){ toast('Cannot ban admin','error'); return; }
  u.banned=!u.banned;
  saveLocal(); fbSave('users',state.users);
  toast(u.banned?'User banned':'User unbanned', u.banned?'warning':'success');
  render();
}
function deleteUser(uid){
  if(!confirm('Delete user permanently?')) return;
  state.users=state.users.filter(x=>x.id!==uid);
  saveLocal(); fbSave('users',state.users);
  toast('User deleted','error');
  render();
}

/* ================= SETTINGS ================= */
function renderSettings(){
  const s=state.settings;
  return `
  <div class="page-enter" style="display:flex;flex-direction:column;gap:20px">
    <div class="card">
      <div class="card-head"><div><h3>🏪 Store Identity</h3><p>Branding and basic information</p></div></div>
      <div class="card-pad">
        <div class="form-grid">
          <div class="field"><label>Site Name</label><input id="setSiteName" value="${esc(s.site_name||'')}" placeholder="Panel Bajar"></div>
          <div class="field"><label>Tagline</label><input id="setTagline" value="${esc(s.tagline||'')}" placeholder="Buy Premium Mods & Hacks"></div>
        </div>
        <div class="form-grid">
          <div class="field">
            <label>Logo Image URL</label>
            <input id="setLogoImage" value="${esc(s.logo_image||'')}" placeholder="https://... (empty for PB text)">
            <div class="hint">Square image recommended.</div>
          </div>
          <div class="field">
            <label>Logo Click URL</label>
            <input id="setLogoUrl" value="${esc(s.logo_url||'#')}" placeholder="https://t.me/yourchannel">
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><div><h3>🤖 Telegram Bot Notification</h3><p>Get instant alerts when new orders arrive</p></div></div>
      <div class="card-pad">
        <div class="form-grid">
          <div class="field">
            <label>Bot Token</label>
            <input id="setTgToken" value="${esc(s.telegram_bot_token||'')}" placeholder="123456789:ABCdefGHIjklMNOpqrSTUvwxYZ">
            <div class="hint">Get it from @BotFather on Telegram.</div>
          </div>
          <div class="field">
            <label>Chat ID</label>
            <input id="setTgChat" value="${esc(s.telegram_chat_id||'')}" placeholder="-1001234567890 or 123456789">
            <div class="hint">Your Telegram user ID or group ID.</div>
          </div>
        </div>
        <button class="btn btn-blue" onclick="testTelegram()" style="margin-top:8px">🚀 Send Test Message</button>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><div><h3>🛑 Welcome Popup</h3><p>Show a popup message when users visit the site</p></div></div>
      <div class="card-pad">
        <label class="switch" style="margin-bottom:16px">
          <input type="checkbox" id="setWelcomeActive" ${s.welcome_active?'checked':''}>
          <span class="switch-track"></span><span class="switch-label">Show Welcome Popup</span>
        </label>
        <div class="form-grid">
          <div class="field">
            <label>Popup Image URL</label>
            <input id="setWelcomeImage" value="${esc(s.welcome_image||'')}" placeholder="https://... (Banner Image)">
            <div class="img-preview" id="welcomeImgPreview">
              ${s.welcome_image?`<img src="${esc(s.welcome_image)}" onerror="this.style.display='none';this.parentElement.innerHTML='<div class=\\'placeholder\\'>Invalid image URL</div>'">`:`<div class="placeholder">🖼️ Image preview</div>`}
            </div>
          </div>
          <div class="field">
            <label>Popup Text</label>
            <textarea id="setWelcomeText" style="height:110px">${esc(s.welcome_text||'ভিডিওটি শুরু থেকে শেষ পর্যন্ত দেখুন, যাতে পেমেন্ট করতে বা প্যানেল কিনতে কোনো সমস্যা না হয়।')}</textarea>
            <div style="margin-top:14px">
              <label>Video Link (Button)</label>
              <input id="setWelcomeLink" value="${esc(s.welcome_link||'')}" placeholder="https://youtube.com/...">
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><div><h3>📢 Notification & Offer Bar</h3><p>Scrolling messages on homepage</p></div></div>
      <div class="card-pad">
        <div class="field">
          <label>Notification Text</label>
          <textarea id="setNotif">${esc(s.notification||'')}</textarea>
          <label class="switch" style="margin-top:10px">
            <input type="checkbox" id="setNotifActive" ${s.notif_active?'checked':''}>
            <span class="switch-track"></span><span class="switch-label">Show notification</span>
          </label>
        </div>
        <div class="field" style="margin-top:20px;padding-top:20px;border-top:1px solid var(--border)">
          <label>Offer Bar Text</label>
          <textarea id="setOffer">${esc(s.offer_text||'')}</textarea>
          <label class="switch" style="margin-top:10px">
            <input type="checkbox" id="setOfferActive" ${s.offer_active?'checked':''}>
            <span class="switch-track"></span><span class="switch-label">Show offer bar</span>
          </label>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><div><h3>💳 Payment & Contact</h3><p>Payment method and social links</p></div></div>
      <div class="card-pad">
        <div class="form-grid">
          <div class="field"><label>bKash Number</label><input id="setBkash" value="${esc(s.bkash_number||'')}" placeholder="01XXXXXXXXX"></div>
          <div class="field"><label>WhatsApp Number</label><input id="setWhatsapp" value="${esc(s.whatsapp_number||'')}" placeholder="8801700000000"></div>
        </div>
        <div class="form-grid">
          <div class="field"><label>Telegram URL</label><input id="setTelegram" value="${esc(s.telegram||'')}" placeholder="https://t.me/..."></div>
          <div class="field"><label>YouTube URL</label><input id="setYoutube" value="${esc(s.youtube||'')}" placeholder="https://youtube.com/@..."></div>
        </div>
      </div>
    </div>

    <div class="card">
      <div class="card-head"><div><h3>🕐 Store Hours & Status</h3><p>Control when the store accepts orders</p></div></div>
      <div class="card-pad">
        <div style="display:flex;flex-direction:column;gap:16px">
          <label class="switch">
            <input type="checkbox" ${s.is_online!==false?'checked':''} onchange="saveInline('is_online',this.checked)">
            <span class="switch-track"></span>
            <span class="switch-label">Store is ${s.is_online!==false?'ONLINE':'OFFLINE'} (manual override)</span>
          </label>
          <div class="form-grid">
            <div class="field"><label>Auto-Online Start</label><input id="setOnlineStart" type="time" value="${esc(s.online_start||'00:00')}"></div>
            <div class="field"><label>Auto-Online End</label><input id="setOnlineEnd" type="time" value="${esc(s.online_end||'23:59')}"></div>
          </div>
          <div style="font-size:12px;color:var(--muted);background:var(--bg2);padding:12px;border-radius:8px;border:1px dashed var(--border)">
            💡 Manual override ON = online during time window. Override OFF = always offline.
          </div>
        </div>
      </div>
    </div>

    <div style="display:flex;justify-content:flex-end">
      <button class="btn btn-primary" style="padding:14px 32px" onclick="saveAllSettings()">
        <svg fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path d="M19 21H5a2 2 0 01-2-2V5a2 2 0 012-2h11l5 5v11a2 2 0 01-2 2z"/><path d="M17 21v-8H7v8M7 3v5h8"/></svg>
        💾 Save All Settings
      </button>
    </div>
  </div>`;
}
function saveInline(key, val){
  state.settings[key]=val;
  saveLocal(); fbSave('settings',[state.settings]);
  toast('Setting updated','success');
  render();
}
function saveAllSettings(){
  state.settings.site_name=$('setSiteName').value.trim()||'Panel Bajar';
  state.settings.tagline=$('setTagline').value.trim();
  state.settings.logo_image=$('setLogoImage').value.trim();
  state.settings.logo_url=$('setLogoUrl').value.trim()||'#';
  state.settings.telegram_bot_token=$('setTgToken').value.trim();
  state.settings.telegram_chat_id=$('setTgChat').value.trim();
  state.settings.notification=$('setNotif').value.trim();
  state.settings.notif_active=$('setNotifActive').checked;
  state.settings.offer_text=$('setOffer').value.trim();
  state.settings.offer_active=$('setOfferActive').checked;
  state.settings.bkash_number=$('setBkash').value.trim();
  state.settings.whatsapp_number=$('setWhatsapp').value.trim();
  state.settings.telegram=$('setTelegram').value.trim();
  state.settings.youtube=$('setYoutube').value.trim();
  state.settings.online_start=$('setOnlineStart').value;
  state.settings.online_end=$('setOnlineEnd').value;

  state.settings.welcome_active = $('setWelcomeActive').checked;
  state.settings.welcome_image = $('setWelcomeImage').value.trim();
  state.settings.welcome_text = $('setWelcomeText').value.trim();
  state.settings.welcome_link = $('setWelcomeLink').value.trim();

  saveLocal(); fbSave('settings',[state.settings]);
  toast('All settings saved & synced to user panel!','success');
  render();
}

/* ================= TELEGRAM TEST ================= */
function testTelegram(){
  const token = $('setTgToken').value.trim();
  const chatId = $('setTgChat').value.trim();
  if(!token || !chatId){ toast('Please enter both Bot Token and Chat ID', 'error'); return; }
  
  const msg = "✅ <b>Test Message from Panel Bajar</b>\n\nYour Telegram notification setup is working perfectly!";
  const url = `https://api.telegram.org/bot${token}/sendMessage`;
  
  fetch(url, {
    method:'POST',
    headers:{'Content-Type':'application/json'},
    body:JSON.stringify({chat_id:chatId, text:msg, parse_mode:'HTML'})
  }).then(r=>r.json()).then(d=>{
    if(d.ok) toast('Test message sent successfully! Check Telegram.', 'success');
    else toast('Error: ' + (d.description || 'Invalid Token/Chat ID'), 'error');
  }).catch(e=>toast('Network error. Please check your connection.', 'error'));
}


/* ================= MODAL & UTILS ================= */
function openModal(html){ $('modalContent').innerHTML=html; $('modal').classList.add('show'); }
function closeModal(){ $('modal').classList.remove('show'); }
function copyText(text){
  try{
    if(navigator.clipboard && navigator.clipboard.writeText){
      navigator.clipboard.writeText(text).then(()=>toast('Copied!','success')).catch(()=>fallbackCopy(text));
    }else fallbackCopy(text);
  }catch(e){ fallbackCopy(text); }
}
function fallbackCopy(text){
  const ta=document.createElement('textarea');
  ta.value=text; ta.style.position='fixed'; ta.style.opacity='0';
  document.body.appendChild(ta); ta.select();
  try{ document.execCommand('copy'); toast('Copied!','success'); }catch(e){ toast('Copy failed','error'); }
  document.body.removeChild(ta);
}

/* ================= SEED & BOOT ================= */
function seedLocal(){
  let changed=false;
  if(!state.users.find(u=>u.role==='ADMIN')){
    state.users.push({
      id:uid(),email:'admin@panelbajar.com',username:'Admin',password:'admin123',
      role:'ADMIN',totalOrders:0,totalSpent:0,banned:false,
      avatarColor:'#7c3aed',createdAt:new Date().toISOString()
    });
    changed=true;
  }
  if(!state.users.find(u=>u.email==='user@example.com')){
    state.users.push({
      id:uid(),email:'user@example.com',username:'Demo User',password:'user123',
      role:'USER',totalOrders:0,totalSpent:0,banned:false,
      avatarColor:'#ec4899',createdAt:new Date().toISOString()
    });
    changed=true;
  }
  if(state.products.length===0){
    const samples=[
      {name:'AIM HACK - ANDROID',icon:'🎯',category:'NON_ROOT',antiban:true,description:'100% Anti Ban • Auto Aim • Android & iOS',plans:[{dur:'1 Hour',price:15,stock:99},{dur:'12 Hours',price:120,stock:99},{dur:'1 Day',price:160,stock:99}]},
      {name:'BALA MODS - NON ROOT',icon:'🔥',category:'NON_ROOT',antiban:true,description:'Main ID Safe • Anti Ban • Aim • ESP',plans:[{dur:'1 Day',price:25,stock:99},{dur:'7 Days',price:150,stock:99},{dur:'30 Days',price:500,stock:99}]},
      {name:'AIM HACK - ROOT',icon:'🎯',category:'ROOT',antiban:true,description:'Root Version • Premium Features',plans:[{dur:'1 Day',price:30,stock:99},{dur:'7 Days',price:180,stock:99},{dur:'30 Days',price:600,stock:99}]},
      {name:'IPHONE MOD',icon:'📱',category:'IPHONE',antiban:true,description:'iOS Only • No Jailbreak',plans:[{dur:'1 Day',price:50,stock:99},{dur:'7 Days',price:300,stock:99},{dur:'30 Days',price:1000,stock:99}]},
      {name:'PC ESP HACK',icon:'💻',category:'PC',antiban:true,description:'PC Version • ESP • Aim',plans:[{dur:'1 Day',price:40,stock:99},{dur:'7 Days',price:250,stock:99},{dur:'30 Days',price:800,stock:99}]}
    ];
    samples.forEach(s=>state.products.push({id:uid(),status:'ACTIVE',image:'',oldPrice:0,maintenance:false,url_full_details:'',url_setup_video:'',url_download:'',url_iphone_setup:'',createdAt:new Date().toISOString(),...s}));
    changed=true;
  }
  if(changed) saveLocal();
}

function startFbSync(){
  if(syncStarted||!fbConnected) return;
  syncStarted=true;
  
  fbListen('products', d=>{
    if(d&&Array.isArray(d)&&d.length>0){ state.products=d; localStorage.setItem('pb_products',JSON.stringify(d)); if(state.page==='products'||state.page==='dashboard') render(); }
  });
  fbListen('orders', d=>{
    if(d&&Array.isArray(d)&&d.length>0){ state.orders=d; localStorage.setItem('pb_orders',JSON.stringify(d)); if(['orders','dashboard'].includes(state.page)) render(); }
  });
  fbListen('users', d=>{
    if(d&&Array.isArray(d)&&d.length>0){ state.users=d; localStorage.setItem('pb_users',JSON.stringify(d)); if(['users','dashboard'].includes(state.page)) render(); }
  });
  fbListen('settings', d=>{
    if(d&&Array.isArray(d)&&d.length>0&&d[0]){ state.settings={...DEFAULT_SETTINGS, ...d[0]}; localStorage.setItem('pb_settings',JSON.stringify(state.settings)); render(); }
  });
  
  fbLoad('products', d=>{ if(d&&d.length>0){ state.products=d; localStorage.setItem('pb_products',JSON.stringify(d)); if(state.page==='products'||state.page==='dashboard') render(); } else { fbSave('products',state.products); } });
  fbLoad('orders', d=>{ if(d&&d.length>0){ state.orders=d; localStorage.setItem('pb_orders',JSON.stringify(d)); if(['orders','dashboard'].includes(state.page)) render(); } else { fbSave('orders',state.orders); } });
  fbLoad('users', d=>{ if(d&&d.length>0){ state.users=d; localStorage.setItem('pb_users',JSON.stringify(d)); if(['users','dashboard'].includes(state.page)) render(); } else { fbSave('users',state.users); } });
  fbLoad('settings', d=>{ if(d&&d.length>0&&d[0]){ state.settings={...DEFAULT_SETTINGS, ...d[0]}; localStorage.setItem('pb_settings',JSON.stringify(state.settings)); render(); } else { fbSave('settings',[state.settings]); } });
}

document.addEventListener('DOMContentLoaded', function(){
  seedLocal();
  if(!state.admin){ renderLogin(); return; }
  render();
  if(initFirebase()) startFbSync();
});
</script>
</body>
</html>
