<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>True Nutra · CS Knowledge Base</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
/* ===== RESET & BASE ===== */
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth;font-size:14px}
body{font-family:'DM Sans',sans-serif;background:#f5f5f3;color:#1a1a1a;min-height:100vh;overflow-x:hidden}

/* ===== CSS VARIABLES ===== */
:root{
  --black:#0c0c0c;
  --dark:#1a1a1a;
  --mid:#444;
  --muted:#6b6b6b;
  --soft:#a0a0a0;
  --border:#e0e0dc;
  --bg:#f5f5f3;
  --white:#ffffff;
  --surface:#ffffff;
  --light:#eeeeeb;
}

/* ===== NAV BAR ===== */
.nav{
  position:fixed;top:0;left:0;right:0;z-index:200;
  background:rgba(12,12,12,0.97);
  backdrop-filter:blur(12px);
  border-bottom:1px solid rgba(255,255,255,0.07);
  display:flex;align-items:center;
  padding:0 32px;height:56px;
  gap:0;
}
.nav-logo{
  font-family:'DM Serif Display',serif;
  font-size:16px;color:#fff;
  text-decoration:none;
  margin-right:auto;
  letter-spacing:-.3px;
  display:flex;align-items:center;gap:8px;
}
.nav-logo span{font-size:10px;font-weight:600;letter-spacing:.1em;color:rgba(255,255,255,.4);text-transform:uppercase;border-left:1px solid rgba(255,255,255,.15);padding-left:10px;margin-left:2px}
.nav-links{display:flex;align-items:center;gap:2px}
.nav-link{
  font-size:12.5px;font-weight:500;color:rgba(255,255,255,.55);
  text-decoration:none;padding:6px 12px;border-radius:6px;
  transition:all .15s;letter-spacing:.01em;cursor:pointer;
  border:none;background:none;font-family:'DM Sans',sans-serif;
}
.nav-link:hover{color:#fff;background:rgba(255,255,255,.07)}
.nav-link.active{color:#fff;background:rgba(255,255,255,.1)}
.nav-search-btn{
  margin-left:12px;width:32px;height:32px;border-radius:6px;
  background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.1);
  display:flex;align-items:center;justify-content:center;
  cursor:pointer;color:rgba(255,255,255,.6);font-size:14px;
  transition:all .15s;
}
.nav-search-btn:hover{background:rgba(255,255,255,.14);color:#fff}

/* ===== PAGES ===== */
.page{display:none;padding-top:56px;min-height:100vh}
.page.active{display:block}

/* ===== HOME PAGE ===== */
.home-hero{
  min-height:calc(100vh - 56px);
  display:flex;flex-direction:column;
  align-items:center;justify-content:center;
  background:var(--black);
  position:relative;overflow:hidden;
  padding:40px 24px;
}
.home-hero::before{
  content:'';position:absolute;inset:0;
  background:radial-gradient(ellipse 80% 60% at 50% 40%,rgba(255,255,255,.03) 0%,transparent 70%);
  pointer-events:none;
}
.home-hero::after{
  content:'';position:absolute;inset:0;
  background:repeating-linear-gradient(
    0deg,rgba(255,255,255,.012) 0,rgba(255,255,255,.012) 1px,transparent 1px,transparent 48px
  ),repeating-linear-gradient(
    90deg,rgba(255,255,255,.012) 0,rgba(255,255,255,.012) 1px,transparent 1px,transparent 48px
  );
  pointer-events:none;
}
.home-tagline{
  font-size:11px;font-weight:600;letter-spacing:.14em;text-transform:uppercase;
  color:rgba(255,255,255,.35);margin-bottom:22px;position:relative;
}
.home-title{
  font-family:'DM Serif Display',serif;
  font-size:clamp(36px,5vw,56px);
  font-weight:400;color:#fff;
  text-align:center;
  line-height:1.12;letter-spacing:-.5px;
  margin-bottom:16px;position:relative;
}
.home-title em{font-style:italic;color:rgba(255,255,255,.55)}
.home-sub{
  font-size:15px;color:rgba(255,255,255,.4);
  text-align:center;margin-bottom:44px;
  line-height:1.6;max-width:440px;position:relative;
}

/* SEARCH BOX */
.home-search-wrap{width:100%;max-width:580px;position:relative;margin-bottom:64px;z-index:10}
.home-search{
  width:100%;padding:18px 24px 18px 56px;
  border:none;border-radius:4px;
  font-size:15px;font-family:'DM Sans',sans-serif;
  color:var(--dark);background:#fff;
  outline:none;
  box-shadow:0 2px 0 rgba(255,255,255,.2),0 20px 60px rgba(0,0,0,.5);
  transition:box-shadow .2s;
}
.home-search:focus{box-shadow:0 2px 0 rgba(255,255,255,.4),0 20px 60px rgba(0,0,0,.6)}
.home-search::placeholder{color:#b0b0b0}
.home-search-ico{position:absolute;left:20px;top:50%;transform:translateY(-50%);color:#b0b0b0;font-size:18px;pointer-events:none}
.search-results{
  display:none;position:absolute;top:calc(100% + 6px);left:0;right:0;
  background:#fff;border-radius:4px;
  box-shadow:0 24px 64px rgba(0,0,0,.3);
  z-index:100;max-height:380px;overflow-y:auto;
}
.search-results.show{display:block}
.sr-item{
  display:flex;align-items:flex-start;gap:12px;
  padding:13px 18px;border-bottom:1px solid #f0f0ee;
  cursor:pointer;transition:background .12s;
}
.sr-item:last-child{border-bottom:none}
.sr-item:hover{background:#f8f8f6}
.sr-type{
  font-size:9.5px;font-weight:700;padding:2px 6px;border-radius:3px;
  background:var(--black);color:#fff;white-space:nowrap;
  flex-shrink:0;margin-top:2px;letter-spacing:.05em;
}
.sr-type.faq-type{background:#444}
.sr-type.pend-type{background:#888}
.sr-label{font-size:13px;font-weight:500;color:var(--dark);line-height:1.4;margin-bottom:2px}
.sr-meta{font-size:11px;color:var(--muted)}
.sr-empty{padding:22px;text-align:center;font-size:13px;color:var(--soft)}

/* HOME ICON NAV */
.home-nav-grid{
  display:flex;gap:12px;flex-wrap:wrap;justify-content:center;
  position:relative;z-index:5;max-width:680px;
}
.hn-card{
  display:flex;flex-direction:column;align-items:center;gap:10px;
  padding:20px 18px;
  background:rgba(255,255,255,.05);
  border:1px solid rgba(255,255,255,.1);
  border-radius:4px;cursor:pointer;
  text-decoration:none;
  transition:all .18s;
  min-width:110px;flex:1;
}
.hn-card:hover{
  background:rgba(255,255,255,.1);
  border-color:rgba(255,255,255,.22);
  transform:translateY(-2px);
}
.hn-card:active{transform:translateY(0)}
.hn-emoji{font-size:28px;line-height:1}
.hn-label{font-size:11.5px;font-weight:600;color:rgba(255,255,255,.65);letter-spacing:.04em;text-align:center;white-space:nowrap}
.hn-count{font-size:10px;color:rgba(255,255,255,.3);margin-top:1px}

/* ===== INNER PAGE LAYOUT ===== */
.page-header{
  background:var(--black);
  padding:44px 0 48px;
  border-bottom:1px solid rgba(255,255,255,.06);
}
.page-header-inner{max-width:1100px;margin:0 auto;padding:0 32px}
.page-breadcrumb{
  font-size:11.5px;color:rgba(255,255,255,.35);
  margin-bottom:14px;display:flex;align-items:center;gap:6px;
}
.page-breadcrumb span{cursor:pointer;transition:color .12s}
.page-breadcrumb span:hover{color:rgba(255,255,255,.7)}
.page-breadcrumb .sep{color:rgba(255,255,255,.2)}
.page-h1{
  font-family:'DM Serif Display',serif;
  font-size:32px;font-weight:400;color:#fff;
  letter-spacing:-.4px;margin-bottom:8px;
}
.page-sub{font-size:14px;color:rgba(255,255,255,.4);line-height:1.5}

/* INNER BODY */
.page-body-wrap{max-width:1100px;margin:0 auto;padding:40px 32px 80px;display:grid;grid-template-columns:1fr 256px;gap:40px;align-items:start}
.page-body-wide{max-width:1100px;margin:0 auto;padding:40px 32px 80px}

/* SIDEBAR */
.inner-sidebar{position:sticky;top:72px}
.sb-widget{background:var(--surface);border:1px solid var(--border);border-radius:4px;margin-bottom:16px;overflow:hidden}
.sb-widget-head{padding:14px 18px;border-bottom:1px solid var(--border);font-size:12px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:.08em}
.sb-widget ul{list-style:none}
.sb-widget ul li{border-bottom:1px solid var(--border)}
.sb-widget ul li:last-child{border-bottom:none}
.sb-widget ul li a,.sb-widget ul li button{
  display:flex;align-items:center;justify-content:space-between;
  padding:11px 18px;font-size:13px;color:var(--dark);
  text-decoration:none;cursor:pointer;transition:all .13s;gap:8px;
  width:100%;text-align:left;border:none;background:none;font-family:'DM Sans',sans-serif;
}
.sb-widget ul li a:hover,.sb-widget ul li button:hover{background:var(--light);color:var(--black)}
.sb-badge{font-size:10px;font-weight:700;padding:1px 6px;border-radius:10px;background:var(--black);color:#fff;white-space:nowrap;flex-shrink:0}
.sb-badge.grey{background:var(--light);color:var(--muted)}
.sb-badge.danger{background:#1a1a1a;color:#fff}

.sb-support{background:var(--black);border-radius:4px;padding:20px;margin-bottom:16px}
.sb-support h3{font-family:'DM Serif Display',serif;font-size:16px;font-weight:400;color:#fff;margin-bottom:8px}
.sb-support p{font-size:12px;color:rgba(255,255,255,.5);line-height:1.65;margin-bottom:14px}
.sb-support a{display:inline-block;font-size:12px;font-weight:700;color:var(--black);background:#fff;padding:8px 16px;text-decoration:none;letter-spacing:.04em;border-radius:2px;transition:opacity .13s}
.sb-support a:hover{opacity:.85}

/* ===== CARDS ===== */
.card{background:var(--surface);border:1px solid var(--border);border-radius:4px;overflow:hidden;margin-bottom:20px}
.card-head{padding:18px 22px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:12px}
.card-ico{width:36px;height:36px;background:var(--black);border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.card-ico svg{width:17px;height:17px;stroke:#fff;fill:none;stroke-width:2;stroke-linecap:round;stroke-linejoin:round}
.card-title{font-family:'DM Serif Display',serif;font-size:17px;font-weight:400;color:var(--black)}
.card-count{margin-left:auto;font-size:11px;font-weight:600;padding:2px 9px;border-radius:10px;background:var(--light);color:var(--muted)}

/* ===== HELP TOPICS GRID ===== */
.topics-grid{display:grid;grid-template-columns:1fr 1fr;border-top:none}
.tc{
  display:flex;align-items:flex-start;gap:14px;
  padding:22px 20px;
  border-bottom:1px solid var(--border);border-right:1px solid var(--border);
  cursor:pointer;text-decoration:none;color:inherit;transition:background .13s;
}
.tc:nth-child(even){border-right:none}
.tc:nth-last-child(-n+2){border-bottom:none}
.tc:hover{background:var(--light)}
.tc-ico{width:44px;height:44px;background:var(--black);border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0;margin-top:1px}
.tc-ico svg{width:20px;height:20px;stroke:#fff;fill:none;stroke-width:1.9;stroke-linecap:round;stroke-linejoin:round}
.tc-name{font-size:14.5px;font-weight:600;color:var(--black);margin-bottom:5px}
.tc-desc{font-size:12.5px;color:var(--muted);line-height:1.55}
.tc-arrow{margin-left:auto;color:var(--soft);font-size:18px;align-self:center;flex-shrink:0}

/* ===== FAQ ===== */
.faq-item{border-bottom:1px solid var(--border)}
.faq-item:last-child{border-bottom:none}
.faq-q{display:flex;align-items:center;padding:16px 22px;cursor:pointer;gap:10px;user-select:none;transition:background .12s}
.faq-q:hover{background:var(--light)}
.fq-text{font-size:13.5px;font-weight:500;color:var(--dark);flex:1;line-height:1.4}
.fq-badge{font-size:9.5px;font-weight:700;padding:2px 7px;border-radius:9px;white-space:nowrap;flex-shrink:0;letter-spacing:.04em;border:1px solid var(--border);color:var(--mid)}
.fq-badge.ai{background:var(--black);color:#fff;border-color:var(--black)}
.fq-badge.prod{background:var(--mid);color:#fff;border-color:var(--mid)}
.fq-badge.ref{background:var(--light);color:var(--mid)}
.fq-badge.pol{background:var(--light);color:var(--mid)}
.fq-badge.leg{background:var(--light);color:var(--mid)}
.fq-badge.tech{background:var(--light);color:var(--mid)}
.fq-toggle{width:22px;height:22px;border:1.5px solid var(--border);border-radius:50%;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:15px;color:var(--muted);transition:all .2s;font-weight:300;line-height:1}
.faq-item.open .fq-toggle{background:var(--black);border-color:var(--black);color:#fff;transform:rotate(45deg)}
.faq-a{display:none;padding:2px 22px 20px;font-size:13px;color:var(--muted);line-height:1.78}
.faq-item.open .faq-a{display:block}
.faq-a ul{margin:10px 0 0 20px}
.faq-a ul li{margin-bottom:6px}
.faq-a strong{color:var(--dark)}
.kl{display:inline-flex;align-items:center;gap:4px;font-size:12px;color:var(--black);font-weight:600;text-decoration:none;border-bottom:1px solid var(--border);margin-top:10px;padding-bottom:1px}
.kl:hover{border-color:var(--black)}

/* ===== TICKETS ===== */
.tickets-controls{padding:14px 18px;border-bottom:1px solid var(--border);background:var(--light);display:flex;flex-direction:column;gap:10px}
.tab-row{display:flex;gap:6px;flex-wrap:wrap}
.cht{font-size:11.5px;padding:5px 12px;border-radius:20px;border:1.5px solid var(--border);background:#fff;color:var(--muted);cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:600;transition:all .13s}
.cht.on,.cht:hover{background:var(--black);color:#fff;border-color:var(--black)}
.ctb{font-size:11px;padding:4px 10px;border-radius:20px;border:1.5px solid var(--border);background:#fff;color:var(--muted);cursor:pointer;font-family:'DM Sans',sans-serif;font-weight:500;transition:all .13s}
.ctb.on,.ctb:hover{background:var(--dark);color:#fff;border-color:var(--dark)}
.t-row{display:flex;align-items:flex-start;gap:12px;padding:13px 20px;border-bottom:1px solid var(--border)}
.t-row:last-child{border-bottom:none}
.t-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;margin-top:6px}
.t-dot.open{background:var(--black)}
.t-dot.prog{background:var(--border);border:1.5px solid var(--soft)}
.t-info{flex:1;min-width:0}
.t-titlerow{display:flex;align-items:center;gap:7px;margin-bottom:2px;flex-wrap:wrap}
.t-title{font-size:13px;font-weight:500;color:var(--dark);line-height:1.4}
.t-src{font-size:9px;font-weight:700;padding:1px 5px;border:1px solid var(--border);color:var(--soft);letter-spacing:.05em;border-radius:3px;white-space:nowrap}
.t-by{font-size:11px;color:var(--muted)}
.tklink{font-size:11.5px;color:var(--black);text-decoration:none;font-weight:600;white-space:nowrap;align-self:center;flex-shrink:0;border-bottom:1px solid var(--border);padding-bottom:1px}
.tklink:hover{border-color:var(--black)}
.no-res{padding:30px;text-align:center;font-size:13px;color:var(--soft)}

/* ===== PENDING ===== */
.p-item{display:flex;gap:14px;padding:18px 20px;border-bottom:1px solid var(--border);align-items:flex-start}
.p-item:last-child{border-bottom:none}
.p-num{font-family:'DM Serif Display',serif;font-size:26px;color:var(--light);flex-shrink:0;line-height:1;width:32px;text-align:right;padding-top:2px}
.p-body{flex:1}
.p-title{font-size:13.5px;font-weight:500;color:var(--dark);margin-bottom:4px;line-height:1.4}
.p-meta{font-size:11.5px;color:var(--muted);margin-bottom:5px}
.p-open{display:inline-block;font-size:9.5px;font-weight:700;padding:1px 6px;background:var(--black);color:#fff;border-radius:3px;margin-right:6px;letter-spacing:.05em}
.pkl{font-size:11.5px;color:var(--black);text-decoration:none;border-bottom:1px solid var(--border);font-weight:600;padding-bottom:1px}
.pkl:hover{border-color:var(--black)}

/* ===== ESCALATION PAGE ===== */
.esc-grid{display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:20px}
.esc-person{background:var(--surface);border:1px solid var(--border);border-radius:4px;padding:20px;display:flex;gap:14px;align-items:flex-start}
.esc-avatar{width:44px;height:44px;border-radius:50%;background:var(--black);display:flex;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:#fff;flex-shrink:0}
.esc-avatar.grey{background:var(--mid)}
.esc-name{font-size:14px;font-weight:600;color:var(--black);margin-bottom:4px}
.esc-role{font-size:12px;color:var(--muted);line-height:1.5;margin-bottom:10px}
.esc-tags{display:flex;gap:5px;flex-wrap:wrap}
.esc-tag{font-size:11px;padding:2px 8px;border-radius:3px;background:var(--light);color:var(--mid);font-weight:500}
.rules-card{background:var(--surface);border:1px solid var(--border);border-radius:4px;overflow:hidden;margin-bottom:20px}
.rules-card-head{padding:16px 22px;border-bottom:1px solid var(--border);font-size:13px;font-weight:700;color:var(--black);text-transform:uppercase;letter-spacing:.07em}
.rule-row{display:flex;align-items:flex-start;gap:12px;padding:14px 22px;border-bottom:1px solid var(--border)}
.rule-row:last-child{border-bottom:none}
.rule-icon{font-size:18px;flex-shrink:0;width:26px;text-align:center}
.rule-body{}
.rule-label{font-size:13px;font-weight:600;color:var(--black);margin-bottom:3px}
.rule-text{font-size:12.5px;color:var(--muted);line-height:1.55}

/* STATS ROW */
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:16px;margin-bottom:28px}
.stat-card{background:var(--surface);border:1px solid var(--border);border-radius:4px;padding:20px 22px}
.stat-num{font-family:'DM Serif Display',serif;font-size:36px;font-weight:400;color:var(--black);line-height:1;margin-bottom:6px}
.stat-label{font-size:12px;color:var(--muted);font-weight:500}
.stat-sub{font-size:11px;color:var(--soft);margin-top:3px}

/* FOOTER */
.site-footer{background:var(--black);padding:32px;text-align:center}
.site-footer p{font-size:11.5px;color:rgba(255,255,255,.25);letter-spacing:.05em}
.site-footer p + p{margin-top:6px}

/* UTIL */
.divider{height:1px;background:var(--border);margin:28px 0}
.section-label{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.1em;color:var(--muted);margin-bottom:16px}

/* ANIMATIONS */
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.page.active .home-title{animation:fadeUp .5s ease both}
.page.active .home-sub{animation:fadeUp .5s .08s ease both}
.page.active .home-search-wrap{animation:fadeUp .5s .15s ease both}
.page.active .home-nav-grid{animation:fadeUp .5s .22s ease both}
.hn-card:nth-child(1){animation-delay:.05s}.hn-card:nth-child(2){animation-delay:.1s}.hn-card:nth-child(3){animation-delay:.15s}.hn-card:nth-child(4){animation-delay:.2s}.hn-card:nth-child(5){animation-delay:.25s}
</style>
</head>
<body>

<!-- ===== NAV ===== -->
<nav class="nav">
  <a class="nav-logo" href="#" onclick="goPage('home')">
    True Nutra <span>CS Knowledge Base</span>
  </a>
  <div class="nav-links">
    <button class="nav-link" onclick="goPage('topics')">Help Topics</button>
    <button class="nav-link" onclick="goPage('faq')">Common Questions</button>
    <button class="nav-link" onclick="goPage('tickets')">All Tickets</button>
    <button class="nav-link" onclick="goPage('pending')">Pending</button>
    <button class="nav-link" onclick="goPage('escalation')">Escalation</button>
  </div>
  <div class="nav-search-btn" onclick="focusSearch()" title="Search">🔍</div>
</nav>

<!-- ============================== -->
<!-- PAGE: HOME                     -->
<!-- ============================== -->
<div class="page active" id="page-home">
  <div class="home-hero">
    <div class="home-tagline">True Nutra · Customer Support</div>
    <h1 class="home-title">How can we <em>help?</em></h1>
    <p class="home-sub">Search tickets, browse help topics, or jump straight to what you need.</p>

    <!-- SEARCH -->
    <div class="home-search-wrap">
      <span class="home-search-ico">🔍</span>
      <input class="home-search" id="home-search" type="text" placeholder="Search tickets, questions, topics…"
        autocomplete="off" oninput="doSearch(this.value)" onfocus="doSearch(this.value)" onblur="setTimeout(closeSearch,180)"/>
      <div class="search-results" id="search-results"></div>
    </div>

    <!-- ICON NAV -->
    <div class="home-nav-grid">
      <div class="hn-card" onclick="goPage('topics')">
        <span class="hn-emoji">📋</span>
        <span class="hn-label">Help Topics</span>
        <span class="hn-count">6 categories</span>
      </div>
      <div class="hn-card" onclick="goPage('faq')">
        <span class="hn-emoji">❓</span>
        <span class="hn-label">Common Questions</span>
        <span class="hn-count">10 articles</span>
      </div>
      <div class="hn-card" onclick="goPage('tickets')">
        <span class="hn-emoji">🎫</span>
        <span class="hn-label">All Tickets</span>
        <span class="hn-count" id="home-ticket-count">56 tickets</span>
      </div>
      <div class="hn-card" onclick="goPage('pending')">
        <span class="hn-emoji">⚠️</span>
        <span class="hn-label">Pending Concerns</span>
        <span class="hn-count" id="home-pend-count">17 open</span>
      </div>
      <div class="hn-card" onclick="goPage('escalation')">
        <span class="hn-emoji">📞</span>
        <span class="hn-label">Escalation Guide</span>
        <span class="hn-count">7 contacts</span>
      </div>
    </div>
  </div>
</div>

<!-- ============================== -->
<!-- PAGE: HELP TOPICS              -->
<!-- ============================== -->
<div class="page" id="page-topics">
  <div class="page-header">
    <div class="page-header-inner">
      <div class="page-breadcrumb">
        <span onclick="goPage('home')">Home</span>
        <span class="sep">/</span>
        <span>Help Topics</span>
      </div>
      <h1 class="page-h1">Help Topics</h1>
      <p class="page-sub">Browse by category to find procedures, guidelines, and sample tickets.</p>
    </div>
  </div>
  <div class="page-body-wrap">
    <div class="main-col">

      <!-- OVERVIEW STATS -->
      <div class="stats-row">
        <div class="stat-card"><div class="stat-num" id="st-total">0</div><div class="stat-label">Total Tickets</div><div class="stat-sub">Across all 3 channels</div></div>
        <div class="stat-card"><div class="stat-num" id="st-open">0</div><div class="stat-label">Open</div><div class="stat-sub">Needs action</div></div>
        <div class="stat-card"><div class="stat-num" id="st-ai">0</div><div class="stat-label">AI Issues</div><div class="stat-sub">Ashley / Iris errors</div></div>
        <div class="stat-card"><div class="stat-num" id="st-ref">0</div><div class="stat-label">Refund Requests</div><div class="stat-sub">External refunds</div></div>
      </div>

      <!-- TOPIC CARDS -->
      <div class="card">
        <div class="card-head">
          <div class="card-ico"><svg viewBox="0 0 24 24"><path d="M4 6h16M4 12h16M4 18h10"/></svg></div>
          <span class="card-title">All Categories</span>
        </div>
        <div class="topics-grid">
          <div class="tc" onclick="goTickets('all','ref')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><path d="M12 2v20M2 12h20"/><path d="M17 7l-5-5-5 5M7 17l5 5 5-5"/></svg></div>
            <div><div class="tc-name">Refunds &amp; Payments</div><div class="tc-desc">External refunds via PayPal, Venmo, wire &amp; check. Approvals and Go Green guidelines.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('ai','ai')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="3"/><circle cx="8.5" cy="9.5" r="1.5" fill="#fff" stroke="none"/><circle cx="15.5" cy="9.5" r="1.5" fill="#fff" stroke="none"/><path d="M9 15s1 1.5 3 1.5 3-1.5 3-1.5"/></svg></div>
            <div><div class="tc-name">Ashley / Iris AI Issues</div><div class="tc-desc">Wrong refunds, bad product info, over-cancellations, and unnecessary escalations from AI agents.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('all','prod')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><path d="M20.84 4.61a5.5 5.5 0 00-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 00-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 000-7.78z"/></svg></div>
            <div><div class="tc-name">Product Quality &amp; Labels</div><div class="tc-desc">Wrong labels (Toplux), adverse reactions, format discrepancies, and ingredient questions.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('all','leg')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg></div>
            <div><div class="tc-name">Legal &amp; Compliance</div><div class="tc-desc">Trademark disputes, copycat websites, BBB complaints, and unauthorized domain concerns.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('all','acc')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><path d="M20 21v-2a4 4 0 00-4-4H8a4 4 0 00-4 4v2"/><circle cx="12" cy="7" r="4"/></svg></div>
            <div><div class="tc-name">Account &amp; Charge Lookup</div><div class="tc-desc">Missing accounts, duplicate charges, payment method mismatches, Shopify discrepancies.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('all','tech')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.07 4.93a10 10 0 010 14.14M4.93 4.93a10 10 0 000 14.14"/></svg></div>
            <div><div class="tc-name">Technical &amp; System Issues</div><div class="tc-desc">Shopify bugs, PayPal blocks, checkout errors, workflow outages, and Kustomer widget fixes.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('all','ship')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><path d="M1 3h15v13H1zM16 8h4l3 3v5h-7V8z"/><circle cx="5.5" cy="18.5" r="2.5"/><circle cx="18.5" cy="18.5" r="2.5"/></svg></div>
            <div><div class="tc-name">Shipping &amp; Fulfillment</div><div class="tc-desc">Wrong items, missing packages, customs failures, duplicate shipments.</div></div>
            <span class="tc-arrow">›</span>
          </div>
          <div class="tc" onclick="goTickets('all','q')">
            <div class="tc-ico"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M9.09 9a3 3 0 015.83 1c0 2-3 3-3 3M12 17h.01"/></svg></div>
            <div><div class="tc-name">Policy &amp; Q&amp;A</div><div class="tc-desc">Agent questions on procedures, product info, and how to handle edge cases.</div></div>
            <span class="tc-arrow">›</span>
          </div>
        </div>
      </div>

    </div>
    <aside class="inner-sidebar">
      <div class="sb-widget">
        <div class="sb-widget-head">Quick Jump</div>
        <ul>
          <li><a href="#" onclick="goPage('faq');return false;">Common Questions</a></li>
          <li><a href="#" onclick="goPage('tickets');return false;">All Tickets</a></li>
          <li><a href="#" onclick="goPage('pending');return false;">Pending Concerns <span class="sb-badge danger" id="sb2-pend">0</span></a></li>
          <li><a href="#" onclick="goPage('escalation');return false;">Escalation Guide</a></li>
        </ul>
      </div>
      <div class="sb-support">
        <h3>Open Kustomer</h3>
        <p>View full customer details and ticket history directly in Kustomer.</p>
        <a href="https://raicom.kustomerapp.com" target="_blank">Open Kustomer →</a>
      </div>
    </aside>
  </div>
</div>

<!-- ============================== -->
<!-- PAGE: FAQ                      -->
<!-- ============================== -->
<div class="page" id="page-faq">
  <div class="page-header">
    <div class="page-header-inner">
      <div class="page-breadcrumb"><span onclick="goPage('home')">Home</span><span class="sep">/</span><span>Common Questions</span></div>
      <h1 class="page-h1">Most Common Questions</h1>
      <p class="page-sub">Step-by-step answers to the issues raised most frequently across all channels.</p>
    </div>
  </div>
  <div class="page-body-wrap">
    <div class="main-col">
      <div class="card" id="faq-card">
        <div class="card-head">
          <div class="card-ico"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M9.09 9a3 3 0 015.83 1c0 2-3 3-3 3M12 17h.01"/></svg></div>
          <span class="card-title">Frequently Asked Questions</span>
          <span class="card-count">10 articles</span>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">How do I process an external refund (PayPal, Venmo, wire, check)?</span><span class="fq-badge ref">Refund</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">All external refunds require approval from <strong>Marge Laureola</strong> before processing.<ul>
            <li>PayPal: collect customer's PayPal email address</li>
            <li>Venmo: collect their @handle username</li>
            <li>Wire transfer: bank name, account number, account type (checking/savings)</li>
            <li>International wire: also collect SWIFT code and country</li>
            <li>Check: full legal name and mailing address</li>
            <li>Go Green = exactly <strong>50% refund</strong> — never process full refund unless customer explicitly declines</li>
            <li>Always verify the refund was actually completed — Ashley may confirm without acting</li>
            <li>Never refund Mystery Gift or the original order unless specifically requested</li>
          </ul></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">What do I do when a customer reports an adverse reaction to a product?</span><span class="fq-badge prod">Product</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Adverse reactions are high priority — do <strong>NOT</strong> offer retention.<ul>
            <li>Collect: symptoms, when they started, product name, dosage taken</li>
            <li>Physician or medical professional involved → flag <strong>urgent</strong>, escalate to Ryan Bailis immediately</li>
            <li>Cancel the subscription AND cancel/refund the order</li>
            <li>Order unfulfilled → cancel it. Order delivered → process full refund</li>
            <li>Do not commit to a cause without investigation. Log for QA and product review</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/69056d7f9f455e31225f7e1a/event/692e3c5f504706cf82ccb9e3" target="_blank">→ Sample ticket: Liquid NAD+ adverse reaction</a></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">What is the correct retention offer when a customer wants to cancel?</span><span class="fq-badge pol">Policy</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Standard retention options — offer both, let the customer choose:<ul>
            <li><strong>Option 1:</strong> Pause subscription for up to 6 months (based on their preference)</li>
            <li><strong>Option 2:</strong> 20% lifetime discount applied to their subscription</li>
            <li><strong>Never offer:</strong> 35% discount — Ashley has offered this incorrectly in the past</li>
            <li>For adverse reactions: skip retention entirely — cancel and refund immediately</li>
          </ul></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">Ashley cancelled the wrong thing — order instead of subscription. What now?</span><span class="fq-badge ai">AI Issue</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">This is a known Ashley error. Steps to fix:<ul>
            <li>Check if the cancellation can be reversed in Shopify / Fulfil</li>
            <li>If already fulfilled, process a replacement if the customer still wants the product</li>
            <li>Report in <strong>#cs-ai-issue-reporting</strong> and tag <strong>Enrico Dela Rosa</strong></li>
            <li>Always verify Ashley's actions before closing any ticket</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/69f803e9b32644c3cac74599/event/69f80b889ce2db1544b0c617" target="_blank">→ Sample ticket</a></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">A customer account cannot be found or a charge is not showing in the system.</span><span class="fq-badge pol">Account</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Account lookup steps — work through these in order:<ul>
            <li>Filter by last 4 digits of card + billing address in Kustomer</li>
            <li>Cross-check in CheckoutChamp (CC) if Kustomer returns nothing</li>
            <li>If still not found: ask the customer for their transaction ID or a bank statement screenshot</li>
            <li>Refund went to a different card → escalate to Ryan (possible unauthorized payment method change)</li>
            <li>Always confirm which email the subscription is under before taking any action</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/6941aa80a6e21e876d049e3d/event/696698397bc563015cddb6ea" target="_blank">→ Sample ticket: refund to wrong card</a></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">What are Ashley's known product information errors?</span><span class="fq-badge ai">AI Issue</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Always correct the customer for these known Ashley errors and report each one:<ul>
            <li>7-in-1 Blood Sugar Complex: Ashley says NOT liquid — <strong>it IS liquid</strong></li>
            <li>5-in-1 Vitamin B Complex: Ashley offers capsules — <strong>capsules do not exist</strong></li>
            <li>Vitamin D3+K2: Ashley says bottles — <strong>it comes in pouches/packs</strong></li>
            <li>Turmeric Curcumin 95: Ashley says 90 capsules — <strong>only 30 capsules per bottle</strong></li>
            <li>Vitamin D3+K2: Ashley offers "Black" &amp; "GLP" versions — <strong>only 1 version exists</strong></li>
            <li>Subscription pause: Ashley says 3-month max — <strong>actual limit is 6 months</strong></li>
            <li>Magnesium Complex 15 servings: correct because it is taken twice daily (30 capsules total)</li>
          </ul>
          Report all to <strong>#cs-ai-issue-reporting</strong> and tag Enrico Dela Rosa.</div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">A customer received the wrong item or a product with the wrong label (e.g. Toplux).</span><span class="fq-badge prod">Product</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Wrong item / label steps:<ul>
            <li>Request a photo from the customer immediately</li>
            <li>Check order in Kustomer and Fulfil for what was actually shipped</li>
            <li>"Toplux" label on True Nutra products → escalate to Ryan (known ongoing issue)</li>
            <li>For wrong item: process replacement for the correct item <strong>only</strong></li>
            <li><strong>Never use the "Resend" button</strong> — it sends the full order. Escalate to CS for partial replacements</li>
            <li>Discontinued TN011 (Beef Organ) &amp; TN013 (Hair Loss) → replace with Magnesium Complex + Vitamin B Complex</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/69d2aa2203068dc74e8e2c42/event/69f92a1d9ce2db154432e234" target="_blank">→ Sample ticket: wrong Turmeric label</a></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">We received a legal letter, BBB inquiry, or trademark complaint. What is the process?</span><span class="fq-badge leg">Legal</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">For any legal communication:<ul>
            <li><strong>Never respond directly</strong> to any legal letter — escalate to Ryan Bailis immediately</li>
            <li>BBB inquiries: assign to Angel for response drafting</li>
            <li>Trademark concerns (TRUE NUTRITION vs TRUE NUTRA): requires legal counsel — make no commitments</li>
            <li>Copycat sites (trytruenutrawellness.com, truenutra.co.za): report to Ryan and Mo immediately</li>
            <li>Do not close the ticket until the legal team confirms resolution</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/69ef7e07da0cf3efc3ca9d4a/event/69ef7e079ce2db1544912285" target="_blank">→ Sample ticket: trademark letter</a></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">A customer wants to reach Coach Tom — what contact options are available?</span><span class="fq-badge pol">Policy</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Coach Tom contact options:<ul>
            <li>Default: SMS / WhatsApp via the number on file</li>
            <li>International customers (Portugal, Germany, etc.): SMS not available — <strong>email is the alternative</strong></li>
            <li>Customer requests Coach Tom by name → assign ticket to Enrico Dela Rosa</li>
            <li>Do NOT share personal contact number directly in a Kustomer message</li>
            <li>Telegram group management → escalate to Ryan, not a standard CS action</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/69f0cb2e7199a1462207b8f2/event/69f0ecf876fd76d2d815daa4" target="_blank">→ Sample ticket: international Coach Tom request</a></div>
        </div>
        <div class="faq-item">
          <div class="faq-q" onclick="toggleFaq(this)"><span class="fq-text">The Go Green 50% refund is not processing correctly in Fulfil — what do I do?</span><span class="fq-badge tech">Tech</span><span class="fq-toggle">+</span></div>
          <div class="faq-a">Known Go Green / Fulfil issue:<ul>
            <li>Ashley may escalate because Fulfil does not show a "Plant a Tree" option — this is a known UI gap</li>
            <li>The 50% refund can still be processed — "Plant a Tree" is handled separately</li>
            <li>If Ashley escalates unnecessarily, check Fulfil manually — process if the refund went through</li>
            <li>Always verify the total order amount before processing to ensure exactly 50%</li>
          </ul>
          <a class="kl" href="https://raicom.kustomerapp.com/app/customers/69bcb33b92f99b66cea78092/event/69cde6d360b5fbedeb9aaa6f" target="_blank">→ Sample ticket</a></div>
        </div>
      </div>
    </div>
    <aside class="inner-sidebar">
      <div class="sb-widget">
        <div class="sb-widget-head">Articles</div>
        <ul>
          <li><button onclick="openFaq(0)">External refund process</button></li>
          <li><button onclick="openFaq(1)">Adverse product reactions</button></li>
          <li><button onclick="openFaq(2)">Subscription retention options</button></li>
          <li><button onclick="openFaq(3)">Ashley cancelled wrong item</button></li>
          <li><button onclick="openFaq(4)">Account &amp; charge lookup</button></li>
          <li><button onclick="openFaq(5)">Ashley product info errors</button></li>
          <li><button onclick="openFaq(6)">Wrong item / wrong label</button></li>
          <li><button onclick="openFaq(7)">Legal letter process</button></li>
          <li><button onclick="openFaq(8)">Coach Tom contact options</button></li>
          <li><button onclick="openFaq(9)">Go Green 50% refund issue</button></li>
        </ul>
      </div>
      <div class="sb-support">
        <h3>Need more help?</h3>
        <p>Can't find your answer? Escalate directly to the right person.</p>
        <a href="#" onclick="goPage('escalation');return false;">Escalation Guide →</a>
      </div>
    </aside>
  </div>
</div>

<!-- ============================== -->
<!-- PAGE: ALL TICKETS              -->
<!-- ============================== -->
<div class="page" id="page-tickets">
  <div class="page-header">
    <div class="page-header-inner">
      <div class="page-breadcrumb"><span onclick="goPage('home')">Home</span><span class="sep">/</span><span>All Tickets</span></div>
      <h1 class="page-h1">All Escalated Tickets</h1>
      <p class="page-sub">Every ticket raised across #cs-escalated-concerns, #cs-question-hub, and #cs-ai-issue-reporting.</p>
    </div>
  </div>
  <div class="page-body-wrap">
    <div class="main-col">
      <div class="card">
        <div class="card-head">
          <div class="card-ico"><svg viewBox="0 0 24 24"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 7V5a2 2 0 00-2-2h-4a2 2 0 00-2 2v2"/></svg></div>
          <span class="card-title">Ticket List</span>
          <span class="card-count" id="ticket-count-label">0 shown</span>
        </div>
        <div class="tickets-controls">
          <div class="tab-row">
            <button class="cht on" onclick="setChF('all',this)">All Channels</button>
            <button class="cht" onclick="setChF('esc',this)">#Escalated-Concerns</button>
            <button class="cht" onclick="setChF('hub',this)">#Question-Hub</button>
            <button class="cht" onclick="setChF('ai',this)">#AI-Issue-Reporting</button>
          </div>
          <div class="tab-row">
            <button class="ctb on" onclick="setCatF('all',this)">All</button>
            <button class="ctb" onclick="setCatF('ref',this)">Refund</button>
            <button class="ctb" onclick="setCatF('ai',this)">AI Issue</button>
            <button class="ctb" onclick="setCatF('prod',this)">Product</button>
            <button class="ctb" onclick="setCatF('leg',this)">Legal</button>
            <button class="ctb" onclick="setCatF('acc',this)">Account</button>
            <button class="ctb" onclick="setCatF('tech',this)">Technical</button>
            <button class="ctb" onclick="setCatF('ship',this)">Shipping</button>
            <button class="ctb" onclick="setCatF('q',this)">Policy/Q&amp;A</button>
          </div>
        </div>
        <div id="ticket-list"></div>
      </div>
    </div>
    <aside class="inner-sidebar">
      <div class="sb-widget">
        <div class="sb-widget-head">By Category</div>
        <ul>
          <li><button onclick="quickCat('all')">All Tickets <span class="sb-badge grey" id="sbcn-all">0</span></button></li>
          <li><button onclick="quickCat('ref')">Refunds <span class="sb-badge grey" id="sbcn-ref">0</span></button></li>
          <li><button onclick="quickCat('ai')">AI Issues <span class="sb-badge grey" id="sbcn-ai">0</span></button></li>
          <li><button onclick="quickCat('prod')">Product <span class="sb-badge grey" id="sbcn-prod">0</span></button></li>
          <li><button onclick="quickCat('leg')">Legal <span class="sb-badge grey" id="sbcn-leg">0</span></button></li>
          <li><button onclick="quickCat('acc')">Account <span class="sb-badge grey" id="sbcn-acc">0</span></button></li>
          <li><button onclick="quickCat('tech')">Technical <span class="sb-badge grey" id="sbcn-tech">0</span></button></li>
          <li><button onclick="quickCat('ship')">Shipping <span class="sb-badge grey" id="sbcn-ship">0</span></button></li>
          <li><button onclick="quickCat('q')">Policy/Q&A <span class="sb-badge grey" id="sbcn-q">0</span></button></li>
        </ul>
      </div>
      <div class="sb-widget">
        <div class="sb-widget-head">By Channel</div>
        <ul>
          <li><button onclick="setChF('esc',null)">#cs-escalated-concerns <span class="sb-badge grey" id="sbch-esc">0</span></button></li>
          <li><button onclick="setChF('hub',null)">#cs-question-hub <span class="sb-badge grey" id="sbch-hub">0</span></button></li>
          <li><button onclick="setChF('ai',null)">#cs-ai-issue-reporting <span class="sb-badge grey" id="sbch-ai">0</span></button></li>
        </ul>
      </div>
    </aside>
  </div>
</div>

<!-- ============================== -->
<!-- PAGE: PENDING                  -->
<!-- ============================== -->
<div class="page" id="page-pending">
  <div class="page-header">
    <div class="page-header-inner">
      <div class="page-breadcrumb"><span onclick="goPage('home')">Home</span><span class="sep">/</span><span>Pending Concerns</span></div>
      <h1 class="page-h1">Pending Concerns</h1>
      <p class="page-sub">Open escalations that still need resolution — who raised it and who must act.</p>
    </div>
  </div>
  <div class="page-body-wrap">
    <div class="main-col">
      <div class="card">
        <div class="card-head">
          <div class="card-ico"><svg viewBox="0 0 24 24"><path d="M10.29 3.86L1.82 18a2 2 0 001.71 3h16.94a2 2 0 001.71-3L13.71 3.86a2 2 0 00-3.42 0z"/><line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/></svg></div>
          <span class="card-title">Open Items</span>
          <span class="card-count" id="pend-label">0 open</span>
        </div>
        <div id="pending-list"></div>
      </div>
    </div>
    <aside class="inner-sidebar">
      <div class="sb-widget">
        <div class="sb-widget-head">Needs Action From</div>
        <ul>
          <li><button onclick="filterPend('Ryan Bailis')">Ryan Bailis <span class="sb-badge grey" id="pf-ryan">0</span></button></li>
          <li><button onclick="filterPend('Enrico Dela Rosa')">Enrico Dela Rosa <span class="sb-badge grey" id="pf-enrico">0</span></button></li>
          <li><button onclick="filterPend('all')">Show All <span class="sb-badge grey" id="pf-all">0</span></button></li>
        </ul>
      </div>
      <div class="sb-support">
        <h3>Escalate Now</h3>
        <p>Open the ticket directly in Kustomer and assign it to the right person.</p>
        <a href="https://raicom.kustomerapp.com" target="_blank">Open Kustomer →</a>
      </div>
    </aside>
  </div>
</div>

<!-- ============================== -->
<!-- PAGE: ESCALATION               -->
<!-- ============================== -->
<div class="page" id="page-escalation">
  <div class="page-header">
    <div class="page-header-inner">
      <div class="page-breadcrumb"><span onclick="goPage('home')">Home</span><span class="sep">/</span><span>Escalation Guide</span></div>
      <h1 class="page-h1">Escalation Guide</h1>
      <p class="page-sub">Who to contact for each type of issue, and the quick rules every agent needs to know.</p>
    </div>
  </div>
  <div class="page-body-wide">

    <div class="section-label">Team Contacts</div>
    <div class="esc-grid">
      <div class="esc-person"><div class="esc-avatar">ML</div><div><div class="esc-name">Marge Laureola</div><div class="esc-role">All external refunds require her approval before processing — PayPal, Venmo, wire, check.</div><div class="esc-tags"><span class="esc-tag">External Refunds</span><span class="esc-tag">Approvals</span></div></div></div>
      <div class="esc-person"><div class="esc-avatar">RB</div><div><div class="esc-name">Ryan Bailis</div><div class="esc-role">Product issues, legal matters, trademark concerns, complex account disputes, and manager escalations.</div><div class="esc-tags"><span class="esc-tag">Legal</span><span class="esc-tag">Product</span><span class="esc-tag">Account</span><span class="esc-tag">Manager</span></div></div></div>
      <div class="esc-person"><div class="esc-avatar">ED</div><div><div class="esc-name">Enrico Dela Rosa</div><div class="esc-role">All Ashley / Iris AI errors, behavior reports, and Coach Tom ticket assignments.</div><div class="esc-tags"><span class="esc-tag">AI Issues</span><span class="esc-tag">Coach Tom</span></div></div></div>
      <div class="esc-person"><div class="esc-avatar grey">JE</div><div><div class="esc-name">Jessie</div><div class="esc-role">Product quality information, ingredient reports, lab results, and product improvement feedback.</div><div class="esc-tags"><span class="esc-tag">Product Quality</span><span class="esc-tag">Lab Reports</span></div></div></div>
      <div class="esc-person"><div class="esc-avatar grey">MO</div><div><div class="esc-name">Mo Domah</div><div class="esc-role">Advertisement verification, copycat site reports, unauthorized brand use, and marketing questions.</div><div class="esc-tags"><span class="esc-tag">Ads</span><span class="esc-tag">Copycat Sites</span></div></div></div>
      <div class="esc-person"><div class="esc-avatar grey">SB</div><div><div class="esc-name">Sean Bailis</div><div class="esc-role">Kustomer widget bugs, incorrect order total displays, and technical system fixes.</div><div class="esc-tags"><span class="esc-tag">Kustomer Widget</span><span class="esc-tag">Tech Fixes</span></div></div></div>
      <div class="esc-person"><div class="esc-avatar grey">AN</div><div><div class="esc-name">Angel Madera</div><div class="esc-role">BBB inquiry responses, refund verifications, and proof of refund documentation requests.</div><div class="esc-tags"><span class="esc-tag">BBB</span><span class="esc-tag">Refund Verification</span></div></div></div>
    </div>

    <div class="divider"></div>
    <div class="section-label" style="margin-bottom:16px">Quick Rules Every Agent Must Know</div>
    <div class="rules-card">
      <div class="rules-card-head">Policy Quick Reference</div>
      <div class="rule-row"><div class="rule-icon">🔁</div><div class="rule-body"><div class="rule-label">Go Green Refund</div><div class="rule-text">Always exactly 50% of the order total. Customer keeps the product and a tree is planted in their name. Never process a full refund if customer agreed to Go Green.</div></div></div>
      <div class="rule-row"><div class="rule-icon">⏸</div><div class="rule-body"><div class="rule-label">Subscription Pause Limit</div><div class="rule-text">Up to 6 months maximum — not 3 months. Ashley has incorrectly told customers the limit is 3 months. Always correct this.</div></div></div>
      <div class="rule-row"><div class="rule-icon">💸</div><div class="rule-body"><div class="rule-label">Retention Discount Maximum</div><div class="rule-text">20% lifetime discount is the maximum. Ashley has offered 35% — this is incorrect. Never exceed 20%.</div></div></div>
      <div class="rule-row"><div class="rule-icon">🚨</div><div class="rule-body"><div class="rule-label">Adverse Reactions</div><div class="rule-text">Cancel subscription AND cancel/refund the order. Do not offer retention options. If a physician is involved, escalate to Ryan immediately as urgent.</div></div></div>
      <div class="rule-row"><div class="rule-icon">📦</div><div class="rule-body"><div class="rule-label">Partial Replacements</div><div class="rule-text">Never use the "Resend" button — it sends the full order. Escalate to CS to manually process only the missing or incorrect item.</div></div></div>
      <div class="rule-row"><div class="rule-icon">⚖️</div><div class="rule-body"><div class="rule-label">Legal Letters &amp; BBB</div><div class="rule-text">Never respond directly to any legal letter or BBB inquiry. Escalate to Ryan Bailis immediately. Do not make any commitments or statements.</div></div></div>
      <div class="rule-row"><div class="rule-icon">🤖</div><div class="rule-body"><div class="rule-label">Reporting AI Errors</div><div class="rule-text">All Ashley and Iris errors must be reported to #cs-ai-issue-reporting and tagged to Enrico Dela Rosa with a link to the sample ticket.</div></div></div>
      <div class="rule-row"><div class="rule-icon">🌱</div><div class="rule-body"><div class="rule-label">Discontinued Products</div><div class="rule-text">TN011 (Beef Organ Complex) and TN013 (Hair Loss Complex) are discontinued. Replace with 8-in-1 Magnesium Complex + 5-in-1 Vitamin B Complex.</div></div></div>
      <div class="rule-row"><div class="rule-icon">📞</div><div class="rule-body"><div class="rule-label">Callback Policy</div><div class="rule-text">We do NOT offer callbacks. Ashley has incorrectly promised callbacks to customers — always correct this and inform the customer of our available contact methods.</div></div></div>
      <div class="rule-row"><div class="rule-icon">🛡️</div><div class="rule-body"><div class="rule-label">Suspicious Emails</div><div class="rule-text">Always check the sender's email domain. Legitimate Shopify emails come from @shopify.com only — never from Gmail or other domains.</div></div></div>
    </div>
  </div>
</div>

<!-- FOOTER -->
<footer class="site-footer" id="site-footer" style="display:none">
  <p>True Nutra CS Knowledge Base</p>
  <p>#cs-escalated-concerns &nbsp;·&nbsp; #cs-question-hub &nbsp;·&nbsp; #cs-ai-issue-reporting</p>
</footer>

<!-- ===== DATA & LOGIC ===== -->
<script>
const TICKETS=[
  {ch:'esc',cat:'other',date:'May 11 2026',title:'Trustpilot message — needs Ryan review',by:'Shai',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/6a01f51e9554b9ff5cabf76e/event/6a01f51e0407ca63b87eb90f'},
  {ch:'esc',cat:'prod',date:'May 6 2026',title:'Wrong label on Turmeric — possible customs concern',by:'Zwingli Diamond',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69d2aa2203068dc74e8e2c42/event/69f92a1d9ce2db154432e234'},
  {ch:'esc',cat:'ref',date:'May 5 2026',title:'External wire transfer — Vera Young $33.95',by:'Shai',to:'Marge Laureola',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69a7ca14a6cc733d9a54a746/event/69e42a509ce2db1544f04d3b'},
  {ch:'esc',cat:'acc',date:'May 5 2026',title:'Customer account cannot be located',by:'Shai',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69f801947e2fb04b33652bfc/event/69f87fec9ce2db1544bd79ba'},
  {ch:'esc',cat:'leg',date:'Apr 28 2026',title:'Trademark legal letter — TRUE NUTRITION vs TRUE NUTRA',by:'Ann',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69ef7e07da0cf3efc3ca9d4a/event/69ef7e079ce2db1544912285'},
  {ch:'esc',cat:'ref',date:'Apr 25 2026',title:'Venmo refund — Patricia Wasdyke $36.86',by:'Julio Romero Jr',to:'Marge Laureola',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/6982757119efd3a25b16ba00/event/69ebd90d9ce2db1544a6fd92'},
  {ch:'esc',cat:'ref',date:'Apr 13 2026',title:'PayPal refund error — Mor Haham $179.70',by:'Patriz Brigoli',to:'Marge Laureola',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/676681dc0f9917c61c80ce2f/event/69dbeb289ce2db1544185031'},
  {ch:'esc',cat:'other',date:'Mar 31 2026',title:'Customer demanding manager phone call',by:'Shai',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69a3d478ad628e5a6943dbae/event/69c74a3ded618d6ceba467c5'},
  {ch:'esc',cat:'acc',date:'Jan 14 2026',title:'Refund issued to wrong card — 0524 vs 3844',by:'Zwingli Diamond',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/6941aa80a6e21e876d049e3d/event/696698397bc563015cddb6ea'},
  {ch:'esc',cat:'ship',date:'Jan 10 2026',title:'Fulfillment error — 3 packages sent, 1 expected (TN83308023)',by:'Zwingli Diamond',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/6952fdb4708e31b2098a2981/event/69613f0b7bc563015c219d72'},
  {ch:'esc',cat:'leg',date:'Jan 8 2026',title:'BBB email received — assigned to Angel',by:'Beth Pareja',to:'Angel',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/695e96a12ac354c9469a1dc9/event/695e96a27bc563015c2d3b11'},
  {ch:'esc',cat:'prod',date:'Dec 2 2025',title:'Adverse reaction to Liquid NAD+ — physician involved (URGENT)',by:'Dianne',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69056d7f9f455e31225f7e1a/event/692e3c5f504706cf82ccb9e3'},
  {ch:'esc',cat:'prod',date:'Jan 23 2026',title:'Wrong brand label — Magnesium Complex shows Toplux',by:'Dianne',to:'Ryan Bailis',status:'prog',link:'https://truenutrashop.com/products/fb-en-us-mc001'},
  {ch:'hub',cat:'q',date:'May 13 2026',title:'Invoice for tax purposes — AI-generated, needs Ryan approval',by:'Julio Romero Jr',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/693e0e88b38971b944c1634f/event/6a03abc30407ca63b855debe'},
  {ch:'hub',cat:'q',date:'May 12 2026',title:'Customer requesting CEO full name and phone number',by:'Leizel Cabilan',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69b5555f3f2ebd99d359d49c/event/6a0212230407ca63b89574b9'},
  {ch:'hub',cat:'prod',date:'May 1 2026',title:'5-in-1 Vitamin B Complex — detailed concentration request',by:'Beth Pareja',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/697d0902e9e8c188b33e59a1/event/69ebe1559ce2db1544ac62a6'},
  {ch:'hub',cat:'q',date:'Apr 29 2026',title:'Coach Tom — international customer cannot use SMS (Portugal)',by:'Julio Romero Jr',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69f0cb2e7199a1462207b8f2/event/69f0ecf876fd76d2d815daa4'},
  {ch:'hub',cat:'prod',date:'Apr 24 2026',title:'6-in-1 Lymphatic Complex — customer reports feeling sick',by:'Julio Romero Jr',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c6070d1a18ce85916a75ff/event/69eaec7e9ce2db15444e956d'},
  {ch:'hub',cat:'leg',date:'Apr 17 2026',title:'truenutra.co.za — unauthorized South Africa website',by:'Dianne',to:'Ryan Bailis',status:'prog',link:''},
  {ch:'hub',cat:'prod',date:'Apr 16 2026',title:'Vitamin D3+K2 — heart palpitations reported by customer',by:'Julio Romero Jr',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69d5335c785237ea137abad3/event/69d9aabc60b5fbedeb503f97'},
  {ch:'hub',cat:'tech',date:'Apr 12 2026',title:'Health & Wellness Guide — "No subscription found" error',by:'Patriz Brigoli',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69b6ad5cdb3121467dc50c35/event/69d6ca5b60b5fbedeb360b27'},
  {ch:'hub',cat:'prod',date:'Mar 31 2026',title:'Vitamin B Complex — dosage conflict (1.5ml vs 2 drops)',by:'Patriz Brigoli',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69a8aa12c823f38107dff4f5/event/69caca0e60b5fbedeb31b078'},
  {ch:'hub',cat:'leg',date:'Mar 30 2026',title:'Ad uses "Kate" — customer believes it is Jen Hatmaker',by:'Patriz Brigoli',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69c9c67c31ccfb400b8eea39/event/69c9c67c60b5fbedebd743b9'},
  {ch:'hub',cat:'tech',date:'Mar 29 2026',title:'Vitamin D3+K2 website missing Subscribe & Save option',by:'Patriz Brigoli',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c86525b852554acbbeb56c/event/69c86525ed618d6cebfe2d92'},
  {ch:'hub',cat:'ref',date:'Mar 26 2026',title:'Customer accidentally returned refund to company account',by:'Leizel Cabilan',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/694dad7901604bbe0bc24390/event/699781a4195316a4c738a116'},
  {ch:'hub',cat:'ship',date:'Mar 22 2026',title:'Order returned to sender — customs failure: replace or refund?',by:'Patriz Brigoli',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/68860ea481180a1c411715c7/event/69bb4f99ed618d6cebdbf281'},
  {ch:'hub',cat:'tech',date:'Feb 21 2026',title:'Free shipping charged anyway — checkout bug (2nd occurrence)',by:'Zwingli Diamond',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/6999a5a4735c9bc53f04a4a1/event/6999a5e4195316a4c7d9df12'},
  {ch:'hub',cat:'tech',date:'Feb 17 2026',title:'Shopify partial refund blocked — PayPal open case error',by:'Julio Romero Jr',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/68fe9d05bfa61d7f5ad4c7ed/event/698f76c6b60a4d240dd9ffee'},
  {ch:'hub',cat:'leg',date:'Feb 17 2026',title:'trunutra.com owner receiving 10-20 misdirected emails/day',by:'Leizel Cabilan',to:'Ryan Bailis',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69934554ebdc54d77dcfb4ca/event/69934554195316a4c7c308d0'},
  {ch:'hub',cat:'leg',date:'Dec 4 2025',title:'Copycat website — trytruenutrawellness.com using our branding',by:'Zwingli Diamond',to:'Ryan Bailis',status:'open',link:''},
  {ch:'hub',cat:'prod',date:'Dec 2 2025',title:'7-in-1 Blood Sugar Complex — tingling and GI discomfort reported',by:'Dianne',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/68ee3e89d6315167464b3234/event/68fe0b664f78542693a87cee'},
  {ch:'hub',cat:'prod',date:'Nov 11 2025',title:'Magnesium Complex — 15 servings vs 30 capsules confusion',by:'Julio Romero Jr',to:'Ryan Bailis',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/68f198f63deac3617f7b71ec/event/69125bb9893085344a83c272'},
  {ch:'ai',cat:'ai',date:'May 13 2026',title:'Ashley shows "Active" on cancelled subscriptions — UI bug',by:'Martin Bombon',to:'Enrico Dela Rosa',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69dd88b81302bfbdad84e638/event/6a0270410407ca63b8db1106'},
  {ch:'ai',cat:'ai',date:'May 12 2026',title:'~90 stuck tickets in inbox — Ashley not snoozed after reply',by:'Ann',to:'Enrico Dela Rosa',status:'open',link:''},
  {ch:'ai',cat:'ai',date:'May 12 2026',title:'Year-old tickets reopening — 2nd occurrence',by:'Shai',to:'Enrico Dela Rosa',status:'open',link:'https://raicom.kustomerapp.com/app/customers/67be0cd932572c9ab7ed944c/event/6814d5e8fa9aa75ca441bce4'},
  {ch:'ai',cat:'ai',date:'May 4 2026',title:'Ashley cancelled order AND subscription — only sub was requested',by:'Patriz Brigoli',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69f803e9b32644c3cac74599/event/69f80b889ce2db1544b0c617'},
  {ch:'ai',cat:'ai',date:'May 2 2026',title:'Ashley kept messaging after customer said no help needed',by:'Ann',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69ad734a09f4dce7aab0f1ff/event/69f5db089ce2db15440a0ba1'},
  {ch:'ai',cat:'ai',date:'Apr 30 2026',title:'Ashley refunded $59.95 instead of $47.95 for 2 items',by:'Leizel Cabilan',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69f0dab340715e6f00883e90/event/69f0e04b9ce2db15443f84ad'},
  {ch:'ai',cat:'ai',date:'Apr 25 2026',title:'Ashley telling customers all orders ship from US warehouse',by:'Dianne',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c71aec68691d2cfb9f2f7f/event/69eb033c9ce2db15445112db'},
  {ch:'ai',cat:'ai',date:'Apr 22 2026',title:'Feedback SMS triggered while order still in transit',by:'Zwingli Diamond',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c54fccef60c98125c5fe6b/event/69e8dcf09ce2db15446666a7'},
  {ch:'ai',cat:'ai',date:'Apr 14 2026',title:'Ashley offered 35% lifetime discount — policy max is 20%',by:'Beth Pareja',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/6988daf7764e0ea83809049b/event/69dd71fd9ce2db154499f096'},
  {ch:'ai',cat:'ai',date:'Apr 10 2026',title:'Ashley communicated wrong refund amount — said $88, actual $37.95',by:'Zwingli Diamond',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69b453b1398da534209a085b/event/69d7d60d60b5fbedeb89cdf2'},
  {ch:'ai',cat:'ai',date:'Apr 7 2026',title:'Ashley said Vitamin D3+K2 comes in bottles — it is pouches',by:'Dianne',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c679d4be02070923dc4b35/event/69d256e960b5fbedeb95f026'},
  {ch:'ai',cat:'ai',date:'Apr 5 2026',title:'Ashley processed full refund — customer only agreed to 50% Go Green',by:'Patriz Brigoli',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c84761eb6be4023a945bcd/event/69d11eea60b5fbedeb544578'},
  {ch:'ai',cat:'ai',date:'Apr 3 2026',title:'Iris asking for customer info already sent by system',by:'Leizel Cabilan',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69227f2930b8f77195b4a9a2/event/69cde21460b5fbedeb99ffda'},
  {ch:'ai',cat:'ai',date:'Apr 1 2026',title:'Ashley offered capsule version of Vitamin B Complex — does not exist',by:'Zwingli Diamond',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69324a6246b53ae56ddf0475/event/69cbdde260b5fbedeb95b2ab'},
  {ch:'ai',cat:'ai',date:'Mar 30 2026',title:'Ashley introduced herself as "Amy" to customer',by:'Angel Madera',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69a3526bb9bef8357fa6b0e9/event/69c85adaed618d6cebfa4aad'},
  {ch:'ai',cat:'ai',date:'Mar 25 2026',title:'Ashley outbound message missing the promised tracking link',by:'Zwingli Diamond',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69c01e13b53e29e1db4b0339/event/69c2d858ed618d6cebe6d22c'},
  {ch:'ai',cat:'ai',date:'Mar 11 2026',title:'Ashley only updated address for 1 of 3 orders',by:'Shai',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69add851ba2c631f746b3ff8/event/69addb4eed618d6cebfe3fbc'},
  {ch:'ai',cat:'ai',date:'Mar 9 2026',title:'Ashley tagging True Nutra tickets as Jewel — wrong brand',by:'Martin Bombon',to:'Enrico Dela Rosa',status:'open',link:'https://raicom.kustomerapp.com/app/customers/69587cf9b2f9fc2b58de7b13/event/69acc033ed618d6cebba53b9'},
  {ch:'ai',cat:'ai',date:'Mar 7 2026',title:'Ashley offered non-existent Vitamin D3+K2 label versions',by:'Julio Romero Jr',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/69ab07e1e8f4d66e3e64848d/event/69ab187ced618d6ceb151c44'},
  {ch:'ai',cat:'ai',date:'Mar 4 2026',title:'Ashley created 2 replacement orders for same missing delivery',by:'Patriz Brigoli',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/694b263b55473a90c2aaef80/event/696bdd687bc563015ca1f204'},
  {ch:'ai',cat:'ai',date:'Feb 28 2026',title:'Ashley repeatedly requested photos already provided by customer',by:'Dianne',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/6999a103e573ebfeb08ddba3/event/69a24b44438b7d35bd08e595'},
  {ch:'ai',cat:'ai',date:'Feb 10 2026',title:'Ashley said pause limit is 3 months — actually 6 months',by:'Julio Romero Jr',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/6956ab9bbaf81928ca00065e/event/6989f10bb60a4d240dd8c1be'},
  {ch:'ai',cat:'ai',date:'Feb 8 2026',title:'Ashley paused subscription when customer requested cancellation',by:'Ann',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/68cae46f1b34001b79797865/event/698797d3b60a4d240d2f7cd2'},
  {ch:'ai',cat:'ai',date:'Jan 29 2026',title:'Ashley said Blood Sugar Complex should not be liquid — incorrect',by:'Shai',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/68d443c52c5b624251d7675a/event/697a9022587f05dc1abf7b76'},
  {ch:'ai',cat:'ai',date:'Jan 26 2026',title:'Ashley said Turmeric Curcumin 95 has 90 capsules — actually 30',by:'Ann',to:'Enrico Dela Rosa',status:'prog',link:'https://raicom.kustomerapp.com/app/customers/692d97cb02a14a9476349406/event/6976b568587f05dc1a74a4c1'},
];

const PENDING=[
  {title:'Invoice for tax purposes — needs Ryan approval before sending',by:'Julio Romero Jr',to:'Ryan Bailis',dt:'May 13 2026',link:'https://raicom.kustomerapp.com/app/customers/693e0e88b38971b944c1634f/event/6a03abc30407ca63b855debe'},
  {title:'Ashley UI bug — shows "Active" on cancelled subscriptions (3+ tickets)',by:'Martin Bombon',to:'Enrico Dela Rosa',dt:'May 13 2026',link:'https://raicom.kustomerapp.com/app/customers/69dd88b81302bfbdad84e638/event/6a0270410407ca63b8db1106'},
  {title:'~90 stuck tickets in inbox — Ashley not snoozed after reply',by:'Ann',to:'Enrico Dela Rosa',dt:'May 12 2026',link:''},
  {title:'CEO contact info request — how to respond to customer?',by:'Leizel Cabilan',to:'Ryan Bailis',dt:'May 12 2026',link:'https://raicom.kustomerapp.com/app/customers/69b5555f3f2ebd99d359d49c/event/6a0212230407ca63b89574b9'},
  {title:'Trustpilot message — Ryan to assess and decide on response',by:'Shai',to:'Ryan Bailis',dt:'May 11 2026',link:'https://raicom.kustomerapp.com/app/customers/6a01f51e9554b9ff5cabf76e/event/6a01f51e0407ca63b87eb90f'},
  {title:'Wrong Turmeric label — possible customs issue, investigation needed',by:'Zwingli Diamond',to:'Ryan Bailis',dt:'May 6 2026',link:'https://raicom.kustomerapp.com/app/customers/69d2aa2203068dc74e8e2c42/event/69f92a1d9ce2db154432e234'},
  {title:'Customer account not found in any system — supervisor access needed',by:'Shai',to:'Ryan Bailis',dt:'May 5 2026',link:'https://raicom.kustomerapp.com/app/customers/69f801947e2fb04b33652bfc/event/69f87fec9ce2db1544bd79ba'},
  {title:'5-in-1 Vitamin B Complex — detailed concentrations needed from Jessie',by:'Beth Pareja',to:'Ryan Bailis / Jessie',dt:'May 1 2026',link:'https://raicom.kustomerapp.com/app/customers/697d0902e9e8c188b33e59a1/event/69ebe1559ce2db1544ac62a6'},
  {title:'Vitamin B Complex dosage conflict — 1.5ml label vs 2 drops on Instagram',by:'Patriz Brigoli',to:'Ryan Bailis',dt:'Mar 31 2026',link:'https://raicom.kustomerapp.com/app/customers/69a8aa12c823f38107dff4f5/event/69caca0e60b5fbedeb31b078'},
  {title:'"Jen Hatmaker" ad complaint — possible unauthorized photo use',by:'Patriz Brigoli',to:'Ryan Bailis',dt:'Mar 30 2026',link:'https://raicom.kustomerapp.com/app/customers/69c9c67c31ccfb400b8eea39/event/69c9c67c60b5fbedebd743b9'},
  {title:'Refund issued to wrong card — card 0524 vs customer card 3844',by:'Zwingli Diamond',to:'Ryan Bailis',dt:'Jan 14 2026',link:'https://raicom.kustomerapp.com/app/customers/6941aa80a6e21e876d049e3d/event/696698397bc563015cddb6ea'},
  {title:'Adverse reaction to Liquid NAD+ — physician involved (URGENT)',by:'Dianne',to:'Ryan Bailis',dt:'Dec 2 2025',link:'https://raicom.kustomerapp.com/app/customers/69056d7f9f455e31225f7e1a/event/692e3c5f504706cf82ccb9e3'},
  {title:'Copycat website — trytruenutrawellness.com using our brand',by:'Zwingli Diamond',to:'Ryan Bailis / Mo',dt:'Dec 4 2025',link:''},
  {title:'trunutra.com owner receiving 10-20 misdirected customer emails/day',by:'Leizel Cabilan',to:'Ryan Bailis',dt:'Feb 17 2026',link:'https://raicom.kustomerapp.com/app/customers/69934554ebdc54d77dcfb4ca/event/69934554195316a4c7c308d0'},
  {title:'Health & Wellness Guide — "No subscription found" error for users',by:'Patriz Brigoli',to:'Ryan Bailis',dt:'Apr 12 2026',link:'https://raicom.kustomerapp.com/app/customers/69b6ad5cdb3121467dc50c35/event/69d6ca5b60b5fbedeb360b27'},
  {title:'Ashley tagging True Nutra tickets as Jewel — recurring brand error',by:'Martin Bombon',to:'Enrico Dela Rosa',dt:'Mar 9 2026',link:'https://raicom.kustomerapp.com/app/customers/69587cf9b2f9fc2b58de7b13/event/69acc033ed618d6cebba53b9'},
  {title:'Company registration number request — are we allowed to share this?',by:'Patriz Brigoli',to:'Ryan Bailis',dt:'Feb 16 2026',link:'https://raicom.kustomerapp.com/app/customers/69591cbb31a2ce797053d668/event/697d0fcad403e9f00b4a1490'},
];

const CHLABELS={esc:'#escalated',hub:'#question-hub',ai:'#ai-issues'};
const cats=['ref','ai','prod','leg','acc','tech','ship','q','other'];
let curCh='all',curCat='all',curPend='all';
let currentPage='home';

// ---- INIT COUNTS ----
function initCounts(){
  document.getElementById('home-ticket-count').textContent=TICKETS.length+' tickets';
  document.getElementById('home-pend-count').textContent=PENDING.length+' open';
  document.getElementById('st-total').textContent=TICKETS.length;
  document.getElementById('st-open').textContent=TICKETS.filter(t=>t.status==='open').length;
  document.getElementById('st-ai').textContent=TICKETS.filter(t=>t.cat==='ai').length;
  document.getElementById('st-ref').textContent=TICKETS.filter(t=>t.cat==='ref').length;
  document.getElementById('sb2-pend').textContent=PENDING.length;
  document.getElementById('pend-label').textContent=PENDING.length+' open';
  document.getElementById('pf-all').textContent=PENDING.length;
  document.getElementById('pf-ryan').textContent=PENDING.filter(p=>p.to.includes('Ryan')).length;
  document.getElementById('pf-enrico').textContent=PENDING.filter(p=>p.to.includes('Enrico')).length;
  cats.forEach(c=>{
    ['sbcn-','cn-'].forEach(pfx=>{const el=document.getElementById(pfx+c);if(el)el.textContent=TICKETS.filter(t=>t.cat===c).length;});
  });
  document.getElementById('sbch-esc').textContent=TICKETS.filter(t=>t.ch==='esc').length;
  document.getElementById('sbch-hub').textContent=TICKETS.filter(t=>t.ch==='hub').length;
  document.getElementById('sbch-ai').textContent=TICKETS.filter(t=>t.ch==='ai').length;
}

// ---- PAGE ROUTING ----
function goPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  document.querySelectorAll('.nav-link').forEach(l=>l.classList.remove('active'));
  const nm={topics:0,faq:1,tickets:2,pending:3,escalation:4};
  const navLinks=document.querySelectorAll('.nav-link');
  if(nm[id]!==undefined) navLinks[nm[id]].classList.add('active');
  document.getElementById('site-footer').style.display=id==='home'?'none':'block';
  window.scrollTo(0,0);
  currentPage=id;
}

// ---- TICKET RENDER ----
function renderTickets(){
  let list=TICKETS;
  if(curCh!=='all') list=list.filter(t=>t.ch===curCh);
  if(curCat!=='all') list=list.filter(t=>t.cat===curCat);
  const lbl=document.getElementById('ticket-count-label');
  if(lbl) lbl.textContent=list.length+' shown';
  const el=document.getElementById('ticket-list');
  if(!el) return;
  if(!list.length){el.innerHTML='<div class="no-res">No tickets match your filters.</div>';return;}
  el.innerHTML=list.map(t=>`
    <div class="t-row">
      <div class="t-dot ${t.status}"></div>
      <div class="t-info">
        <div class="t-titlerow">
          <span class="t-title">${t.title}</span>
          <span class="t-src">${CHLABELS[t.ch]}</span>
        </div>
        <div class="t-by">${t.date} &nbsp;·&nbsp; <strong>${t.by}</strong> → ${t.to}</div>
      </div>
      ${t.link?`<a class="tklink" href="${t.link}" target="_blank">Open in Kustomer</a>`:''}
    </div>`).join('');
}

// ---- PENDING RENDER ----
function renderPending(filterTo){
  let list=PENDING;
  if(filterTo&&filterTo!=='all') list=list.filter(p=>p.to.includes(filterTo));
  const el=document.getElementById('pending-list');
  if(!el) return;
  el.innerHTML=list.map((p,i)=>`
    <div class="p-item">
      <div class="p-num">${String(i+1).padStart(2,'0')}</div>
      <div class="p-body">
        <div class="p-title"><span class="p-open">OPEN</span>${p.title}</div>
        <div class="p-meta">${p.dt} &nbsp;·&nbsp; Raised by <strong>${p.by}</strong> &nbsp;·&nbsp; Needs: <strong>${p.to}</strong></div>
        ${p.link?`<a class="pkl" href="${p.link}" target="_blank">Open in Kustomer →</a>`:''}
      </div>
    </div>`).join('');
}

// ---- FILTER HELPERS ----
function setChF(ch,btn){
  curCh=ch;
  if(btn){document.querySelectorAll('.cht').forEach(b=>b.classList.remove('on'));btn.classList.add('on');}
  else{const m={all:0,esc:1,hub:2,ai:3};document.querySelectorAll('.cht').forEach((b,i)=>b.classList.toggle('on',i===m[ch]));}
  renderTickets();
}
function setCatF(cat,btn){
  curCat=cat;
  if(btn){document.querySelectorAll('.ctb').forEach(b=>b.classList.remove('on'));btn.classList.add('on');}
  renderTickets();
}
function quickCat(cat){
  curCat=cat;
  const m={all:0,ref:1,ai:2,prod:3,leg:4,acc:5,tech:6,ship:7,q:8};
  document.querySelectorAll('.ctb').forEach((b,i)=>b.classList.toggle('on',i===m[cat]));
  renderTickets();
}
function goTickets(ch,cat){
  curCh=ch; curCat=cat;
  goPage('tickets');
  setTimeout(()=>{
    const m={all:0,esc:1,hub:2,ai:3};
    const cm={all:0,ref:1,ai:2,prod:3,leg:4,acc:5,tech:6,ship:7,q:8};
    document.querySelectorAll('.cht').forEach((b,i)=>b.classList.toggle('on',i===m[ch]));
    document.querySelectorAll('.ctb').forEach((b,i)=>b.classList.toggle('on',i===(cm[cat]!==undefined?cm[cat]:0)));
    renderTickets();
  },50);
}
function filterPend(who){
  curPend=who;
  renderPending(who==='all'?null:who);
}

// ---- FAQ ----
function toggleFaq(qEl){
  const item=qEl.closest('.faq-item');
  const wasOpen=item.classList.contains('open');
  document.querySelectorAll('.faq-item.open').forEach(i=>i.classList.remove('open'));
  if(!wasOpen) item.classList.add('open');
}
function openFaq(idx){
  goPage('faq');
  setTimeout(()=>{
    const items=document.querySelectorAll('.faq-item');
    if(items[idx]){
      document.querySelectorAll('.faq-item.open').forEach(i=>i.classList.remove('open'));
      items[idx].classList.add('open');
      setTimeout(()=>items[idx].scrollIntoView({behavior:'smooth',block:'center'}),100);
    }
  },80);
}

// ---- SEARCH ----
const SEARCH_INDEX=[
  ...TICKETS.map(t=>({type:'ticket',label:t.title,meta:t.date+' · '+t.by,ch:CHLABELS[t.ch],link:t.link,ch_raw:t.ch,cat:t.cat})),
  {type:'faq',label:'How to process an external refund (PayPal, Venmo, wire, check)',meta:'Common question · Refund',idx:0},
  {type:'faq',label:'Handling adverse product reactions',meta:'Common question · Product',idx:1},
  {type:'faq',label:'Correct subscription retention — pause up to 6 months or 20% discount',meta:'Common question · Policy',idx:2},
  {type:'faq',label:'Ashley cancelled wrong thing — order instead of subscription',meta:'Common question · AI Issue',idx:3},
  {type:'faq',label:'Account and charge lookup steps in Kustomer and CheckoutChamp',meta:'Common question · Account',idx:4},
  {type:'faq',label:'Known Ashley product information errors',meta:'Common question · AI Issue',idx:5},
  {type:'faq',label:'Customer received wrong item or wrong label (Toplux)',meta:'Common question · Product',idx:6},
  {type:'faq',label:'Legal letter BBB inquiry trademark complaint process',meta:'Common question · Legal',idx:7},
  {type:'faq',label:'Coach Tom contact options international customers',meta:'Common question · Policy',idx:8},
  {type:'faq',label:'Go Green 50% refund not processing correctly in Fulfil',meta:'Common question · Technical',idx:9},
  ...PENDING.map(p=>({type:'pending',label:p.title,meta:'Pending · '+p.to,link:p.link})),
];

function doSearch(v){
  const drop=document.getElementById('search-results');
  if(!v||v.length<2){drop.innerHTML='';drop.classList.remove('show');return;}
  const q=v.toLowerCase();
  const results=SEARCH_INDEX.filter(r=>r.label.toLowerCase().includes(q)||(r.meta&&r.meta.toLowerCase().includes(q))).slice(0,9);
  if(!results.length){drop.innerHTML='<div class="sr-empty">No results found for "'+v+'"</div>';drop.classList.add('show');return;}
  drop.innerHTML=results.map(r=>{
    const typeLabel=r.type==='ticket'?r.ch:r.type==='faq'?'FAQ':'PENDING';
    const typeClass=r.type==='faq'?'faq-type':r.type==='pending'?'pend-type':'';
    let action='';
    if(r.type==='ticket'&&r.link) action=`onclick="window.open('${r.link}','_blank')"`;
    else if(r.type==='ticket') action=`onclick="goPage('tickets')"`;
    else if(r.type==='faq') action=`onclick="openFaq(${r.idx})"`;
    else if(r.type==='pending'&&r.link) action=`onclick="window.open('${r.link}','_blank')"`;
    else action=`onclick="goPage('pending')"`;
    return`<div class="sr-item" ${action}>
      <span class="sr-type ${typeClass}">${typeLabel}</span>
      <div><div class="sr-label">${r.label}</div><div class="sr-meta">${r.meta||''}</div></div>
    </div>`;
  }).join('');
  drop.classList.add('show');
}
function closeSearch(){const d=document.getElementById('search-results');if(d)d.classList.remove('show')}
function focusSearch(){goPage('home');setTimeout(()=>document.getElementById('home-search').focus(),120)}

// ---- INIT ----
initCounts();
renderTickets();
renderPending();
</script>
</body>
</html>
