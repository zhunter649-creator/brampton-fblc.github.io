<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Brampton FBLC — We Don't Follow. We Lead.</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Cormorant+Garamond:ital,wght@0,300;0,600;0,700;1,300;1,600&family=Manrope:wght@200;300;400;500;700&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:auto;overflow-x:hidden}
:root{
  --black:#03040a;
  --deep:#070a12;
  --g1:#b8852a;
  --g2:#daa84a;
  --g3:#f0cc72;
  --g4:#fce99a;
  --cream:#f5efe0;
  --fog:rgba(245,239,224,.5);
  --fog2:rgba(245,239,224,.15);
  --bdr:rgba(184,133,42,.18);
}
body{background:var(--black);color:var(--cream);font-family:'Manrope',sans-serif;overflow-x:hidden;cursor:none}

/* ── LOADER ── */
#loader{
  position:fixed;inset:0;z-index:99999;background:var(--black);
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  transition:opacity .8s ease, visibility .8s ease;
}
#loader.gone{opacity:0;visibility:hidden}
.loader-logo{
  font-family:'Anton',sans-serif;font-size:clamp(60px,12vw,140px);
  letter-spacing:.12em;color:transparent;
  -webkit-text-stroke:1px rgba(184,133,42,.4);
  position:relative;overflow:hidden;
}
.loader-fill{
  position:absolute;inset:0;background:linear-gradient(90deg,var(--g1),var(--g3),var(--g1));
  background-size:200% 100%;
  -webkit-background-clip:text;background-clip:text;color:transparent;
  animation:shimmer 1.6s ease-in-out infinite;
  clip-path:inset(0 100% 0 0);
  transition:clip-path 1.2s cubic-bezier(.23,1,.32,1);
}
.loader-fill.loaded{clip-path:inset(0 0% 0 0)}
@keyframes shimmer{0%{background-position:200% 0}100%{background-position:-200% 0}}
.loader-bar{width:280px;height:1px;background:rgba(184,133,42,.15);margin-top:32px;overflow:hidden}
.loader-prog{height:100%;background:linear-gradient(90deg,var(--g1),var(--g3));transform-origin:left;transform:scaleX(0);transition:transform 1.2s cubic-bezier(.23,1,.32,1)}

/* ── CURSOR ── */
#cur-d,#cur-r{position:fixed;pointer-events:none;z-index:99990;border-radius:50%;transform:translate(-50%,-50%)}
#cur-d{width:6px;height:6px;background:var(--g3);mix-blend-mode:screen;transition:width .15s,height .15s}
#cur-r{
  width:30px;height:30px;border:1px solid rgba(184,133,42,.5);
  transition:width .3s cubic-bezier(.23,1,.32,1),height .3s,border-color .3s,background .3s,border-radius .3s;
}
body.ch #cur-d{width:10px;height:10px;background:var(--g4)}
body.ch #cur-r{width:50px;height:50px;border-color:var(--g2);background:rgba(184,133,42,.06)}
body.ck #cur-r{width:20px;height:20px;background:rgba(184,133,42,.25)}
body.txt #cur-r{width:3px;height:36px;border-radius:2px;border-color:var(--g2)}
.cspark{position:fixed;pointer-events:none;z-index:99989;border-radius:50%;transform:translate(-50%,-50%);animation:csp .8s ease forwards}
@keyframes csp{0%{opacity:.9;transform:translate(-50%,-50%) scale(1)}100%{opacity:0;transform:translate(calc(-50% + var(--dx)),calc(-50% + var(--dy))) scale(0)}}

/* ── PROGRESS ── */
#pb{position:fixed;top:0;left:0;height:2px;z-index:9999;background:linear-gradient(90deg,var(--g1),var(--g3),var(--g4));transform-origin:left;transform:scaleX(0);box-shadow:0 0 16px rgba(240,204,114,.6)}

/* ── CANVAS ── */
#c3{position:fixed;inset:0;z-index:1;pointer-events:none}

/* ── NAV ── */
nav{
  position:fixed;top:0;width:100%;z-index:8000;padding:24px 60px;
  display:flex;align-items:center;justify-content:space-between;
  transition:all .4s;
}
nav.sc{padding:14px 60px;background:rgba(3,4,10,.92);backdrop-filter:blur(24px);border-bottom:1px solid var(--bdr)}
.nl{font-family:'Anton',sans-serif;font-size:20px;letter-spacing:.14em;color:var(--cream);text-decoration:none}
.nl em{color:var(--g2);font-style:normal}
.nlinks{display:flex;gap:40px;list-style:none}
.nlinks a{font-family:'Manrope',sans-serif;font-size:11px;font-weight:400;letter-spacing:.14em;text-transform:uppercase;color:var(--fog);text-decoration:none;transition:color .2s;position:relative}
.nlinks a::after{content:'';position:absolute;bottom:-3px;left:0;width:0;height:1px;background:var(--g2);transition:width .3s}
.nlinks a:hover{color:var(--cream)}
.nlinks a:hover::after{width:100%}
.ncta{
  font-family:'Manrope',sans-serif;font-size:11px;font-weight:700;letter-spacing:.14em;text-transform:uppercase;
  padding:11px 28px;background:transparent;border:1px solid var(--g1);color:var(--g2);
  text-decoration:none;transition:all .25s;position:relative;overflow:hidden;
}
.ncta::before{content:'';position:absolute;inset:0;background:linear-gradient(90deg,var(--g1),var(--g2));transform:scaleX(0);transform-origin:left;transition:transform .3s cubic-bezier(.23,1,.32,1)}
.ncta span{position:relative;z-index:1}
.ncta:hover::before{transform:scaleX(1)}
.ncta:hover{color:var(--black);border-color:var(--g2)}

/* ── PAGE CONTENT ── */
.pg{position:relative;z-index:10}

/* ── HERO ── */
.hero{
  min-height:100vh;display:flex;flex-direction:column;justify-content:center;
  padding:0 60px;position:relative;overflow:hidden;
}
.hero-bg-text{
  position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);
  font-family:'Anton',sans-serif;font-size:clamp(120px,20vw,280px);
  letter-spacing:.06em;color:transparent;
  -webkit-text-stroke:1px rgba(184,133,42,.06);
  pointer-events:none;white-space:nowrap;user-select:none;z-index:0;
}
.hero-inner{position:relative;z-index:2;max-width:1400px;margin:0 auto;width:100%}
.hero-chip{
  display:inline-flex;align-items:center;gap:10px;
  background:rgba(184,133,42,.08);border:1px solid var(--bdr);
  padding:8px 18px;margin-bottom:36px;
  font-family:'Manrope',sans-serif;font-size:10px;font-weight:500;letter-spacing:.2em;text-transform:uppercase;color:var(--g2);
  opacity:0;animation:fu .8s .8s ease forwards;
}
.chip-dot{width:6px;height:6px;border-radius:50%;background:var(--g2);animation:pulse 2s infinite}
@keyframes pulse{0%,100%{opacity:1;box-shadow:0 0 0 0 rgba(218,168,74,.5)}50%{opacity:.7;box-shadow:0 0 0 6px rgba(218,168,74,0)}}
.hero h1{
  font-family:'Anton',sans-serif;
  font-size:clamp(64px,9.5vw,148px);
  line-height:.88;letter-spacing:.03em;
  color:var(--cream);position:relative;z-index:2;
}
.h1-line{display:block;overflow:hidden;padding-bottom:.06em}
.h1-line span{display:block;transform:translateY(110%);animation:slide-up .9s cubic-bezier(.16,1,.3,1) both}
.h1-line:nth-child(1) span{animation-delay:.9s}
.h1-line:nth-child(2) span{animation-delay:1.05s}
.h1-line:nth-child(3) span{animation-delay:1.2s}
@keyframes slide-up{to{transform:translateY(0)}}
.hero h1 .glow{
  color:var(--g2);position:relative;
  text-shadow:0 0 80px rgba(218,168,74,.35),0 0 160px rgba(218,168,74,.15);
}
.hero-sub{
  margin-top:36px;max-width:560px;
  font-family:'Cormorant Garamond',serif;font-size:20px;font-weight:300;font-style:italic;
  color:var(--fog);line-height:1.65;
  opacity:0;animation:fu .9s 1.5s ease forwards;
}
.hero-ctas{
  margin-top:52px;display:flex;gap:20px;flex-wrap:wrap;align-items:center;
  opacity:0;animation:fu .9s 1.7s ease forwards;
}
.btn-main{
  font-family:'Manrope',sans-serif;font-size:12px;font-weight:700;letter-spacing:.12em;text-transform:uppercase;
  padding:18px 48px;background:linear-gradient(135deg,var(--g1),var(--g2));color:var(--black);
  text-decoration:none;position:relative;overflow:hidden;
  transition:transform .25s,box-shadow .25s;
  clip-path:polygon(0 0,calc(100% - 12px) 0,100% 12px,100% 100%,12px 100%,0 calc(100% - 12px));
}
.btn-main::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,var(--g2),var(--g4));opacity:0;transition:opacity .3s}
.btn-main:hover::before{opacity:1}
.btn-main:hover{transform:translateY(-4px);box-shadow:0 20px 60px rgba(184,133,42,.45)}
.btn-main span{position:relative;z-index:1}
.btn-ghost{
  font-family:'Manrope',sans-serif;font-size:12px;font-weight:500;letter-spacing:.12em;text-transform:uppercase;
  padding:18px 40px;border:1px solid rgba(245,239,224,.2);color:var(--fog);
  text-decoration:none;transition:all .25s;
}
.btn-ghost:hover{border-color:var(--g2);color:var(--cream);transform:translateY(-4px)}
.hero-stats-row{
  margin-top:80px;display:flex;gap:0;
  opacity:0;animation:fu .9s 2s ease forwards;
}
.hstat{padding:28px 40px 28px 0;border-right:1px solid var(--bdr);margin-right:40px}
.hstat:last-child{border-right:none}
.hstat-n{font-family:'Anton',sans-serif;font-size:54px;letter-spacing:.02em;line-height:1;color:var(--g2)}
.hstat-l{font-family:'Manrope',sans-serif;font-size:10px;font-weight:400;letter-spacing:.14em;text-transform:uppercase;color:var(--fog);margin-top:6px}
.scroll-indicator{
  position:absolute;bottom:48px;left:60px;
  display:flex;align-items:center;gap:16px;
  font-family:'Manrope',sans-serif;font-size:10px;letter-spacing:.18em;text-transform:uppercase;color:var(--fog2);
  opacity:0;animation:fu .8s 2.4s ease forwards;
}
.si-line{width:48px;height:1px;background:linear-gradient(90deg,var(--g1),transparent);animation:pline 2.5s ease-in-out infinite}
@keyframes pline{0%,100%{transform:scaleX(.2);opacity:.4}50%{transform:scaleX(1);opacity:1}}

/* ── MARQUEE ── */
.mq{overflow:hidden;padding:24px 0;background:rgba(184,133,42,.03);border-top:1px solid var(--bdr);border-bottom:1px solid var(--bdr)}
.mqt{display:flex;width:max-content;animation:mq 30s linear infinite}
.mqt:hover{animation-play-state:paused}
.mqi{font-family:'Anton',sans-serif;font-size:14px;letter-spacing:.22em;color:rgba(245,239,224,.22);padding:0 48px;white-space:nowrap}
.mqi .dot{color:var(--g2);margin-left:48px}
@keyframes mq{to{transform:translateX(-50%)}}

/* ── SECTIONS ── */
section{padding:130px 60px;position:relative}
.stag{font-family:'Manrope',sans-serif;font-size:10px;font-weight:500;letter-spacing:.24em;text-transform:uppercase;color:var(--g2);margin-bottom:20px}
.stitle{font-family:'Anton',sans-serif;font-size:clamp(44px,5.5vw,80px);letter-spacing:.03em;line-height:.92;margin-bottom:26px}
.sbody{font-family:'Manrope',sans-serif;font-size:15px;font-weight:300;color:var(--fog);line-height:1.8;max-width:560px}

/* ── REVEAL ── */
.rv{opacity:0;transform:translateY(56px);transition:opacity .9s cubic-bezier(.23,1,.32,1),transform .9s cubic-bezier(.23,1,.32,1)}
.rv.fl{transform:translateX(-72px)}
.rv.fr{transform:translateX(72px)}
.rv.si{transform:scale(.82)}
.rv.rz{transform:perspective(800px) rotateX(28deg) translateY(24px);transform-origin:center top}
.rv.vis{opacity:1!important;transform:none!important}
.d1{transition-delay:.08s}.d2{transition-delay:.18s}.d3{transition-delay:.28s}
.d4{transition-delay:.38s}.d5{transition-delay:.48s}.d6{transition-delay:.58s}.d7{transition-delay:.68s}

/* ── ABOUT ── */
.about{background:var(--deep)}
.about-grid{max-width:1400px;margin:0 auto;display:grid;grid-template-columns:1fr 1fr;gap:120px;align-items:start}
.big-quote{
  font-family:'Cormorant Garamond',serif;font-size:clamp(26px,3vw,42px);font-weight:600;font-style:italic;
  line-height:1.25;color:var(--cream);margin-top:40px;
  padding:32px;border:1px solid var(--bdr);position:relative;
}
.big-quote::before{content:'\201C';font-size:120px;color:var(--g1);opacity:.2;position:absolute;top:-20px;left:16px;line-height:1;font-style:normal}
.big-quote em{color:var(--g2);font-style:italic}
.vals{margin-top:8px}
.v{padding:24px 0;border-bottom:1px solid var(--bdr);display:flex;gap:24px;align-items:flex-start;position:relative;transition:all .3s;overflow:hidden}
.v::after{content:'';position:absolute;left:0;top:0;bottom:0;width:0;background:linear-gradient(90deg,rgba(184,133,42,.06),transparent);transition:width .4s cubic-bezier(.23,1,.32,1)}
.v:hover::after{width:100%}
.v:hover{padding-left:8px}
.vn{font-family:'Anton',sans-serif;font-size:38px;letter-spacing:.04em;color:rgba(184,133,42,.2);flex-shrink:0;width:56px;line-height:1}
.vt h4{font-family:'Manrope',sans-serif;font-size:11px;font-weight:700;letter-spacing:.16em;text-transform:uppercase;color:var(--g2);margin-bottom:7px}
.vt p{font-family:'Manrope',sans-serif;font-size:13px;font-weight:300;color:var(--fog);line-height:1.7}

/* ── 3 ORGS SHOWCASE ── */
.orgs{background:var(--black)}
.orgs-inner{max-width:1400px;margin:0 auto}
.orgs-head{margin-bottom:80px}
.orgs-cards{display:grid;grid-template-columns:repeat(3,1fr);gap:0;border:1px solid var(--bdr)}
.oc{
  padding:56px 48px;position:relative;overflow:hidden;border-right:1px solid var(--bdr);
  transition:background .4s;
  background:var(--black);
}
.oc:last-child{border-right:none}
.oc-glow{position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,transparent,var(--g2),transparent);transform:scaleX(0);transform-origin:left;transition:transform .6s cubic-bezier(.23,1,.32,1)}
.oc:hover .oc-glow{transform:scaleX(1)}
.oc-shine{position:absolute;inset:0;background:radial-gradient(ellipse at 50% 0%,rgba(184,133,42,.07),transparent 60%);opacity:0;transition:opacity .4s}
.oc:hover .oc-shine{opacity:1}
.oc-num{font-family:'Anton',sans-serif;font-size:100px;letter-spacing:.02em;color:rgba(184,133,42,.06);line-height:1;position:absolute;top:16px;right:24px}
.oc-icon{font-size:36px;margin-bottom:28px;display:block;position:relative;z-index:1;transition:transform .3s}
.oc:hover .oc-icon{transform:scale(1.15) rotate(-5deg)}
.oc h3{font-family:'Anton',sans-serif;font-size:28px;letter-spacing:.05em;margin-bottom:16px;color:var(--cream);position:relative;z-index:1;line-height:1}
.oc p{font-family:'Manrope',sans-serif;font-size:13px;font-weight:300;color:var(--fog);line-height:1.8;position:relative;z-index:1}
.oc-tag{
  display:inline-block;margin-top:24px;font-family:'Manrope',sans-serif;font-size:10px;font-weight:600;
  letter-spacing:.16em;text-transform:uppercase;color:var(--g2);
  border-bottom:1px solid var(--g1);padding-bottom:2px;position:relative;z-index:1;
}

/* ── STATS BAND ── */
.sband{
  padding:0 60px;
  background:var(--deep);border-top:1px solid var(--bdr);border-bottom:1px solid var(--bdr);
  overflow:hidden;position:relative;
}
.sband::before{content:'';position:absolute;inset:0;background:radial-gradient(ellipse 60% 80% at 50% 50%,rgba(184,133,42,.04),transparent)}
.sband-inner{max-width:1400px;margin:0 auto;display:grid;grid-template-columns:repeat(4,1fr)}
.sbn{padding:60px 40px;text-align:center;border-right:1px solid var(--bdr);position:relative}
.sbn:last-child{border-right:none}
.sbn-n{font-family:'Anton',sans-serif;font-size:80px;letter-spacing:.02em;line-height:1;color:var(--g2)}
.sbn-l{font-family:'Manrope',sans-serif;font-size:10px;font-weight:400;letter-spacing:.16em;text-transform:uppercase;color:var(--fog);margin-top:10px}

/* ── COMPETITIONS ── */
.comp{background:var(--black)}
.comp-inner{max-width:1400px;margin:0 auto}
.comp-head{margin-bottom:64px}
.comp-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:0;border:1px solid var(--bdr)}
.cc{
  padding:40px 44px;display:flex;gap:28px;align-items:flex-start;
  border-right:1px solid var(--bdr);border-bottom:1px solid var(--bdr);
  position:relative;overflow:hidden;background:var(--black);
  transition:background .3s;
}
.cc:nth-child(2n){border-right:none}
.cc:nth-last-child(-n+2){border-bottom:none}
.cc::before{content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(184,133,42,.04),transparent 60%);opacity:0;transition:opacity .3s}
.cc:hover::before{opacity:1}
.cc:hover{background:rgba(184,133,42,.025)}
.cbadge{
  width:52px;height:52px;flex-shrink:0;border:1px solid var(--bdr);
  display:flex;align-items:center;justify-content:center;font-size:22px;
  transition:all .3s;position:relative;z-index:1;
}
.cc:hover .cbadge{border-color:var(--g2);transform:rotate(-8deg) scale(1.1)}
.cinfo{position:relative;z-index:1}
.cinfo h4{font-family:'Manrope',sans-serif;font-size:14px;font-weight:600;margin-bottom:7px;color:var(--cream);letter-spacing:.02em}
.cinfo p{font-family:'Manrope',sans-serif;font-size:13px;font-weight:300;color:var(--fog);line-height:1.7}

/* ── TIMELINE ── */
.tl-sec{background:var(--deep)}
.tl-inner{max-width:900px;margin:0 auto}
.tl-list{padding-left:44px;position:relative;margin-top:20px}
.tl-list::before{content:'';position:absolute;left:9px;top:8px;bottom:8px;width:1px;background:linear-gradient(to bottom,var(--g2),rgba(184,133,42,.04))}
.tli{position:relative;margin-bottom:60px}
.tlid{position:absolute;left:-40px;top:6px;width:18px;height:18px;background:var(--deep);border:1.5px solid var(--g1);border-radius:50%;transition:all .35s}
.tli:hover .tlid{transform:scale(1.5);box-shadow:0 0 20px rgba(218,168,74,.7);background:rgba(184,133,42,.18);border-color:var(--g3)}
.tly{font-family:'Anton',sans-serif;font-size:11px;letter-spacing:.22em;color:var(--g2);margin-bottom:8px}
.tltt{font-family:'Manrope',sans-serif;font-size:18px;font-weight:500;margin-bottom:9px;color:var(--cream)}
.tld{font-family:'Manrope',sans-serif;font-size:13px;font-weight:300;color:var(--fog);line-height:1.75}

/* ── JOIN ── */
.join{
  background:var(--black);padding:160px 60px;text-align:center;position:relative;overflow:hidden;
}
.join::before{
  content:'';position:absolute;inset:0;
  background:radial-gradient(ellipse 80% 70% at 50% 50%,rgba(184,133,42,.07),transparent 65%);
  animation:breathe 6s ease-in-out infinite;
}
@keyframes breathe{0%,100%{transform:scale(1)}50%{transform:scale(1.1)}}
.join-inner{max-width:800px;margin:0 auto;position:relative;z-index:2}
.jt{
  font-family:'Anton',sans-serif;font-size:clamp(56px,8vw,112px);
  letter-spacing:.04em;line-height:.88;margin-bottom:28px;
}
.jt em{color:var(--g2);font-style:normal;text-shadow:0 0 80px rgba(218,168,74,.4),0 0 160px rgba(218,168,74,.15)}
.jb{font-family:'Cormorant Garamond',serif;font-size:19px;font-style:italic;font-weight:300;color:var(--fog);line-height:1.75;margin-bottom:56px}
.jbtns{display:flex;gap:20px;justify-content:center;flex-wrap:wrap}

/* ── FOOTER ── */
footer{background:var(--deep);border-top:1px solid var(--bdr);padding:56px 60px;display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:32px}
.fb{font-family:'Anton',sans-serif;font-size:18px;letter-spacing:.14em;color:var(--cream)}
.fb em{color:var(--g2);font-style:normal}
.ftag{font-family:'Manrope',sans-serif;font-size:11px;font-weight:300;color:var(--fog);margin-top:5px;letter-spacing:.06em}
.flinks{display:flex;gap:32px;list-style:none;flex-wrap:wrap}
.flinks a{font-family:'Manrope',sans-serif;font-size:11px;font-weight:300;letter-spacing:.1em;text-transform:uppercase;color:var(--fog);text-decoration:none;transition:color .2s}
.flinks a:hover{color:var(--g2)}
.fcopy{width:100%;text-align:center;font-family:'Manrope',sans-serif;font-size:11px;font-weight:200;color:rgba(245,239,224,.18);letter-spacing:.08em;margin-top:8px}

.dv{height:1px;background:linear-gradient(90deg,transparent,var(--bdr),transparent)}
@keyframes fu{from{opacity:0;transform:translateY(32px)}to{opacity:1;transform:translateY(0)}}

@media(max-width:960px){
  body{cursor:auto}#cur-d,#cur-r{display:none}
  nav{padding:16px 24px}nav.sc{padding:12px 24px}
  .nlinks{display:none}
  .hero{padding:100px 24px 80px}
  section{padding:80px 24px}
  .about-grid{grid-template-columns:1fr;gap:60px}
  .orgs-cards{grid-template-columns:1fr}
  .oc{border-right:none;border-bottom:1px solid var(--bdr)}
  .sband-inner{grid-template-columns:1fr 1fr}
  .comp-grid{grid-template-columns:1fr}
  .cc{border-right:none!important}
  footer{padding:36px 24px;flex-direction:column;align-items:flex-start}
  .hero-stats-row{gap:0;flex-wrap:wrap}
  .hstat{padding:20px 24px 20px 0}
}
</style>
</head>
<body>

<!-- LOADER -->
<div id="loader">
  <div class="loader-logo">
    FBLC
    <div class="loader-fill" id="lf">FBLC</div>
  </div>
  <div class="loader-bar"><div class="loader-prog" id="lp"></div></div>
</div>

<div id="cur-d"></div>
<div id="cur-r"></div>
<div id="pb"></div>
<canvas id="c3"></canvas>

<nav id="nav">
  <a href="#" class="nl">BRAMPTON <em>FBLC</em></a>
  <ul class="nlinks">
    <li><a href="#about">About</a></li>
    <li><a href="#orgs">Programs</a></li>
    <li><a href="#compete">Compete</a></li>
    <li><a href="#story">Story</a></li>
    <li><a href="#join" class="ncta"><span>Join Now</span></a></li>
  </ul>
</nav>

<div class="pg">
<!-- HERO -->
<section class="hero">
  <div class="hero-bg-text">FBLC</div>
  <div class="hero-inner">
    <div class="hero-chip"><span class="chip-dot"></span>Brampton · FBL Canada · Est. 2024</div>
    <h1>
      <span class="h1-line"><span>WE DON'T</span></span>
      <span class="h1-line"><span class="glow">FOLLOW.</span></span>
      <span class="h1-line"><span>WE LEAD.</span></span>
    </h1>
    <p class="hero-sub">Brampton's only FBL Canada chapter with two subsidiaries — shaping the entrepreneurs, investors &amp; executives of tomorrow.</p>
    <div class="hero-ctas">
      <a href="https://form.jotform.com/252156876829270" target="_blank" class="btn-main"><span>Apply Now — 2025/26</span></a>
      <a href="#about" class="btn-ghost">Discover More ↓</a>
    </div>
    <div class="hero-stats-row">
      <div class="hstat"><div class="hstat-n" data-count="120" data-sfx="+">0</div><div class="hstat-l">Founder's Den Students</div></div>
      <div class="hstat"><div class="hstat-n" data-count="380" data-sfx="+">0</div><div class="hstat-l">Stock Competition</div></div>
      <div class="hstat"><div class="hstat-n" data-count="16" data-sfx="">0</div><div class="hstat-l">CNLC Events</div></div>
      <div class="hstat"><div class="hstat-n" data-count="3" data-sfx="">0</div><div class="hstat-l">Organizations</div></div>
    </div>
  </div>
  <div class="scroll-indicator"><div class="si-line"></div>Scroll to explore</div>
</section>

<!-- MARQUEE -->
<div class="mq">
  <div class="mqt">
    <span class="mqi">Business Leadership<span class="dot"> ✦</span></span>
    <span class="mqi">Financial Literacy<span class="dot"> ✦</span></span>
    <span class="mqi">Entrepreneurship<span class="dot"> ✦</span></span>
    <span class="mqi">CNLC Competitions<span class="dot"> ✦</span></span>
    <span class="mqi">Founder's Den 2026<span class="dot"> ✦</span></span>
    <span class="mqi">Stock Pitch Competition<span class="dot"> ✦</span></span>
    <span class="mqi">Target Alpha<span class="dot"> ✦</span></span>
    <span class="mqi">JEC Brampton<span class="dot"> ✦</span></span>
    <span class="mqi">FBL Canada<span class="dot"> ✦</span></span>
    <span class="mqi">Business Leadership<span class="dot"> ✦</span></span>
    <span class="mqi">Financial Literacy<span class="dot"> ✦</span></span>
    <span class="mqi">Entrepreneurship<span class="dot"> ✦</span></span>
    <span class="mqi">CNLC Competitions<span class="dot"> ✦</span></span>
    <span class="mqi">Founder's Den 2026<span class="dot"> ✦</span></span>
    <span class="mqi">Stock Pitch Competition<span class="dot"> ✦</span></span>
    <span class="mqi">Target Alpha<span class="dot"> ✦</span></span>
    <span class="mqi">JEC Brampton<span class="dot"> ✦</span></span>
    <span class="mqi">FBL Canada<span class="dot"> ✦</span></span>
  </div>
</div>

<!-- ABOUT -->
<section class="about" id="about">
  <div class="about-grid">
    <div>
      <p class="stag rv">Who We Are</p>
      <h2 class="stitle rv d1">Brampton's<br>Premier<br>Youth Club</h2>
      <blockquote class="big-quote rv d2">The only FBL Canada chapter with <em>two subsidiaries</em> — built for those who want more.</blockquote>
      <p class="sbody rv d3" style="margin-top:28px">We are Brampton FBLC, JEC &amp; TA — a community-based organization dedicated to producing real business leaders. Not students who read about business. Students who do it.</p>
    </div>
    <div class="vals">
      <div class="v rv fr d1"><div class="vn">01</div><div class="vt"><h4>Innovation</h4><p>Creativity isn't encouraged here — it's the entry price. We continuously push the boundaries of what a student organization can be.</p></div></div>
      <div class="v rv fr d2"><div class="vn">02</div><div class="vt"><h4>Integrity</h4><p>Honesty and transparency in everything we do — within the club and in the world. No shortcuts. No excuses.</p></div></div>
      <div class="v rv fr d3"><div class="vn">03</div><div class="vt"><h4>Collaboration</h4><p>Nobody wins alone. We build each other up, challenge each other forward, and celebrate together.</p></div></div>
      <div class="v rv fr d4"><div class="vn">04</div><div class="vt"><h4>Inclusivity</h4><p>Every background. Every skill level. If you want to grow — this is your place.</p></div></div>
    </div>
  </div>
</section>

<!-- STATS -->
<div class="sband">
  <div class="sband-inner">
    <div class="sbn rv si d1"><div class="sbn-n" data-count="120" data-sfx="+">0</div><div class="sbn-l">Founder's Den Attendees</div></div>
    <div class="sbn rv si d2"><div class="sbn-n" data-count="3" data-sfx="">0</div><div class="sbn-l">Organizations Under One Roof</div></div>
    <div class="sbn rv si d3"><div class="sbn-n" data-count="380" data-sfx="+">0</div><div class="sbn-l">Stock Competition Participants</div></div>
    <div class="sbn rv si d4"><div class="sbn-n" data-count="16" data-sfx="">0</div><div class="sbn-l">CNLC Competitive Events</div></div>
  </div>
</div>

<!-- ORGS -->
<section class="orgs" id="orgs">
  <div class="orgs-inner">
    <div class="orgs-head">
      <p class="stag rv">What We Offer</p>
      <h2 class="stitle rv d1">Three Organizations.<br>One Mission.</h2>
      <p class="sbody rv d2">The only FBL Canada chapter operating with two fully active subsidiaries. More opportunities. More impact. More you.</p>
    </div>
    <div class="orgs-cards">
      <div class="oc rv rz d1">
        <div class="oc-glow"></div><div class="oc-shine"></div>
        <div class="oc-num">01</div>
        <span class="oc-icon">📈</span>
        <h3>FBLC<br>Business<br>Leadership</h3>
        <p>Hands-on learning, leadership development, workshops, and community engagement. 16 competitive events at the Canadian National Leadership Conference (CNLC) annually.</p>
        <span class="oc-tag">Explore FBLC →</span>
      </div>
      <div class="oc rv rz d2">
        <div class="oc-glow"></div><div class="oc-shine"></div>
        <div class="oc-num">02</div>
        <span class="oc-icon">💡</span>
        <h3>JEC<br>Junior<br>Entrepreneurship</h3>
        <p>Build startup thinking. Sharpen your pitch. Develop frameworks that work in the real world. Home of Founder's Den — the event that drew 120+ students nationwide.</p>
        <span class="oc-tag">Explore JEC →</span>
      </div>
      <div class="oc rv rz d3">
        <div class="oc-glow"></div><div class="oc-shine"></div>
        <div class="oc-num">03</div>
        <span class="oc-icon">📊</span>
        <h3>Target Alpha<br>Financial<br>Education</h3>
        <p>Deep financial literacy — personal finance, the stock market, investing strategies. Powering Canada's largest high school Stock Pitch Competition with 380+ participants.</p>
        <span class="oc-tag">Explore TA →</span>
      </div>
    </div>
  </div>
</section>

<div class="dv"></div>

<!-- COMPETITIONS -->
<section class="comp" id="compete">
  <div class="comp-inner">
    <div class="comp-head">
      <p class="stag rv">Compete &amp; Excel</p>
      <h2 class="stitle rv d1">The Arena.<br>Are You Ready?</h2>
      <p class="sbody rv d2" style="margin-bottom:0">Competitions that build real skills, real confidence, and real résumés.</p>
    </div>
    <div class="comp-grid rv d3">
      <div class="cc"><div class="cbadge">🏆</div><div class="cinfo"><h4>Canadian National Leadership Conference</h4><p>FBL Canada's flagship annual event. 16 competitive events, national networking, and speakers who have actually built things. This is the big one.</p></div></div>
      <div class="cc"><div class="cbadge">🚀</div><div class="cinfo"><h4>Founder's Den</h4><p>120+ students. Real pitches. Real judges. Our signature co-hosted entrepreneurship event where the next generation of founders gets their first taste of the arena.</p></div></div>
      <div class="cc"><div class="cbadge">📉</div><div class="cinfo"><h4>Stock Pitch Competition (SPC)</h4><p>Canada's largest high school stock pitch competition. Research a company. Build the case. Defend it in front of financial professionals. 380+ participants last year.</p></div></div>
      <div class="cc"><div class="cbadge">💹</div><div class="cinfo"><h4>Stock Trading Competition (STC)</h4><p>A 3-month live trading simulation. Real market. Real decisions. Sponsor-led workshops to sharpen your edge throughout the competition.</p></div></div>
      <div class="cc"><div class="cbadge">📋</div><div class="cinfo"><h4>Financial Planners' Conference</h4><p>Teams of 1–4 tackle a real financial planning case study and present to industry professionals. Client work before you've graduated.</p></div></div>
      <div class="cc"><div class="cbadge">🎙️</div><div class="cinfo"><h4>The Leader's Voice Podcast</h4><p>Unfiltered conversations with entrepreneurs, executives, and thought leaders. Insight to Impact workshops. Knowledge that doesn't wait for a university lecture.</p></div></div>
    </div>
  </div>
</section>

<div class="dv"></div>

<!-- TIMELINE -->
<section class="tl-sec" id="story">
  <div class="tl-inner">
    <p class="stag rv">Our Story</p>
    <h2 class="stitle rv d1">Built From<br>Nothing.</h2>
    <p class="sbody rv d2">From a registration form to Brampton's most impactful youth organization — here's how.</p>
    <div class="tl-list">
      <div class="tli rv fl d1"><div class="tlid"></div><p class="tly">Chapter Founded</p><p class="tltt">Brampton FBLC officially registered</p><p class="tld">President Resakan and VP Piraneerth register Brampton FBLC as a chapter of FBL Canada. A blank canvas. An enormous vision.</p></div>
      <div class="tli rv fl d2"><div class="tlid"></div><p class="tly">The Trio Forms</p><p class="tltt">VP Hasham joins as co-founder</p><p class="tld">The original three founders are assembled. The leadership DNA that would shape everything is locked in.</p></div>
      <div class="tli rv fl d3"><div class="tlid"></div><p class="tly">Open Doors</p><p class="tltt">General member applications launch</p><p class="tld">The first recruitment drive opens. Students across Brampton begin joining something that didn't exist a year before.</p></div>
      <div class="tli rv fl d4"><div class="tlid"></div><p class="tly">Expansion</p><p class="tltt">TA &amp; JEC acquired — two subsidiaries, zero peers</p><p class="tld">VP Hasham acquires Target Alpha and JEC Brampton. Brampton FBLC becomes the only FBL Canada chapter in the country with two fully operating subsidiaries.</p></div>
      <div class="tli rv fl d5"><div class="tlid"></div><p class="tly">National Moment</p><p class="tltt">Founder's Den — 120+ students from across Canada</p><p class="tld">The co-hosted Founder's Den draws students nationwide. Brampton FBLC is no longer just a local club — it's a force in Canadian business education.</p></div>
    </div>
  </div>
</section>

<!-- JOIN -->
<section class="join" id="join">
  <div class="join-inner">
    <h2 class="jt rv"><em>YOUR</em><br>MOVE.</h2>
    <p class="jb rv d2">2025–2026 applications are open. Join Brampton's most ambitious student community — competitions, mentorship, workshops, and a network that will follow you for life.</p>
    <div class="jbtns rv d3">
      <a href="https://form.jotform.com/252156876829270" target="_blank" class="btn-main"><span>Apply as a Member</span></a>
      <a href="https://heyzine.com/flip-book/5819f86d41.html" target="_blank" class="btn-ghost">Read the Prospectus</a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div>
    <div class="fb">BRAMPTON <em>FBLC</em>, JEC &amp; TA</div>
    <div class="ftag">Empowering future business leaders, one step at a time.</div>
  </div>
  <ul class="flinks">
    <li><a href="https://www.bramptonfblc.ca" target="_blank">Website</a></li>
    <li><a href="https://linktr.ee/Brampton_FBLC_JEC_TA" target="_blank">Linktree</a></li>
    <li><a href="https://www.instagram.com/bramptonfblc/" target="_blank">Instagram</a></li>
    <li><a href="https://m.youtube.com/@bramptonfblc-jec-ta" target="_blank">YouTube</a></li>
    <li><a href="https://ca.linkedin.com/company/brampton-fblc-jec-ta" target="_blank">LinkedIn</a></li>
  </ul>
  <p class="fcopy">© 2025–2026 Brampton FBLC, JEC &amp; TA · A chapter of FBL Canada</p>
</footer>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
/* ═══════════════════════════════════════════
   LOADER
═══════════════════════════════════════════ */
window.addEventListener('load', () => {
  const lf = document.getElementById('lf');
  const lp = document.getElementById('lp');
  setTimeout(() => { lp.style.transform = 'scaleX(1)'; lf.classList.add('loaded'); }, 80);
  setTimeout(() => { document.getElementById('loader').classList.add('gone'); }, 1600);
});

/* ═══════════════════════════════════════════
   THREE.JS — FULL SCENE
═══════════════════════════════════════════ */
(function () {
  const canvas = document.getElementById('c3');
  const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  renderer.shadowMap.enabled = true;
  renderer.setClearColor(0x000000, 0);

  const scene = new THREE.Scene();
  const cam = new THREE.PerspectiveCamera(55, 1, 0.1, 500);
  cam.position.z = 7;

  function onResize() {
    renderer.setSize(window.innerWidth, window.innerHeight);
    cam.aspect = window.innerWidth / window.innerHeight;
    cam.updateProjectionMatrix();
  }
  onResize();
  window.addEventListener('resize', onResize, { passive: true });

  /* Lights */
  scene.add(new THREE.AmbientLight(0xffffff, 0.25));
  const p1 = new THREE.PointLight(0xdaa84a, 5, 30); p1.position.set(5, 4, 5);
  const p2 = new THREE.PointLight(0xb8852a, 2.5, 20); p2.position.set(-5, -3, 4);
  const p3 = new THREE.PointLight(0xfce99a, 1.5, 15); p3.position.set(0, 6, 2);
  const p4 = new THREE.PointLight(0x4466ff, 0.8, 25); p4.position.set(-6, 2, -3);
  scene.add(p1, p2, p3, p4);

  /* Gold material */
  const gMat = new THREE.MeshStandardMaterial({ color: 0xc9973a, metalness: 0.95, roughness: 0.1, emissive: 0x3a2200, emissiveIntensity: 0.3 });
  const gEdge = new THREE.MeshStandardMaterial({ color: 0xf0cc72, metalness: 1, roughness: 0.05, emissive: 0x4d3200, emissiveIntensity: 0.5, wireframe: true });
  const gGlass = new THREE.MeshStandardMaterial({ color: 0xe8c06a, metalness: 0.9, roughness: 0.0, emissive: 0x2a1800, emissiveIntensity: 0.2, transparent: true, opacity: 0.7 });

  /* ── MAIN LOGO GROUP ── */
  const LOGO = new THREE.Group();

  /* "F" letterform using merged boxes */
  function mkBox(w, h, d, x, y, z, mat) {
    const m = new THREE.Mesh(new THREE.BoxGeometry(w, h, d, 2, 2, 2), mat || gMat);
    m.position.set(x, y, z);
    m.castShadow = true;
    return m;
  }
  // vertical stroke
  LOGO.add(mkBox(0.45, 3.2, 0.45, -0.5, 0, 0));
  // top bar
  LOGO.add(mkBox(1.8, 0.45, 0.45, 0.4, 1.37, 0));
  // mid bar
  LOGO.add(mkBox(1.3, 0.4, 0.45, 0.15, 0.35, 0));

  /* Orbiting torus rings */
  const rings = [];
  [2.4, 3.0, 3.6].forEach((r, i) => {
    const geo = new THREE.TorusGeometry(r, 0.015 + i * 0.006, 6, 90);
    const mat = new THREE.MeshStandardMaterial({
      color: i === 1 ? 0xe8c06a : 0xc9973a, metalness: 1, roughness: 0.05,
      transparent: true, opacity: 0.5 - i * 0.1
    });
    const torus = new THREE.Mesh(geo, mat);
    torus.rotation.x = (i * 0.7) + 0.3;
    torus.rotation.y = i * 0.5;
    rings.push(torus);
    LOGO.add(torus);
  });

  /* Orbiting satellites */
  const sats = [];
  const satGeos = [
    new THREE.IcosahedronGeometry(0.26, 0),
    new THREE.OctahedronGeometry(0.22, 0),
    new THREE.TetrahedronGeometry(0.28, 0),
    new THREE.IcosahedronGeometry(0.18, 0),
    new THREE.OctahedronGeometry(0.16, 0),
  ];
  const satMats = [gMat, gEdge, gGlass, gMat, gEdge];
  satGeos.forEach((geo, i) => {
    const s = new THREE.Mesh(geo, satMats[i]);
    sats.push(s);
    LOGO.add(s);
  });

  /* Shockwave ring (expands on load) */
  const shockGeo = new THREE.TorusGeometry(0.1, 0.04, 6, 60);
  const shockMat = new THREE.MeshStandardMaterial({ color: 0xf0cc72, emissive: 0xf0cc72, emissiveIntensity: 2, transparent: true, opacity: 1 });
  const shock = new THREE.Mesh(shockGeo, shockMat);
  LOGO.add(shock);

  scene.add(LOGO);

  /* Background particle cloud */
  const N = 350;
  const ptPos = new Float32Array(N * 3);
  const ptSizes = new Float32Array(N);
  for (let i = 0; i < N; i++) {
    const r = 8 + Math.random() * 18;
    const theta = Math.random() * Math.PI * 2;
    const phi = Math.acos(2 * Math.random() - 1);
    ptPos[i*3]   = r * Math.sin(phi) * Math.cos(theta);
    ptPos[i*3+1] = r * Math.sin(phi) * Math.sin(theta);
    ptPos[i*3+2] = r * Math.cos(phi);
    ptSizes[i] = Math.random() * 0.06 + 0.02;
  }
  const ptGeo = new THREE.BufferGeometry();
  ptGeo.setAttribute('position', new THREE.BufferAttribute(ptPos, 3));
  ptGeo.setAttribute('size', new THREE.BufferAttribute(ptSizes, 1));
  const ptMat = new THREE.PointsMaterial({ color: 0xc9973a, size: 0.05, transparent: true, opacity: 0.6, sizeAttenuation: true });
  const pts = new THREE.Points(ptGeo, ptMat);
  scene.add(pts);

  /* Wireframe sphere (globe) */
  const globeGeo = new THREE.IcosahedronGeometry(5.5, 2);
  const globeMat = new THREE.MeshStandardMaterial({ color: 0xb8852a, metalness: 0.8, roughness: 0.2, wireframe: true, transparent: true, opacity: 0.06 });
  const globe = new THREE.Mesh(globeGeo, globeMat);
  scene.add(globe);

  /* Grid floor */
  const grid = new THREE.GridHelper(40, 40, 0xb8852a, 0x120c00);
  grid.position.y = -5.5;
  grid.material.opacity = 0.15;
  grid.material.transparent = true;
  scene.add(grid);

  /* Shockwave state */
  let shockR = 0.1, shockActive = true;
  setTimeout(() => { shockActive = false; }, 2200);

  /* Scroll + mouse */
  let scrollY = 0, targScrollY = 0, mouseX = 0, mouseY = 0, t = 0;
  window.addEventListener('scroll', () => { scrollY = window.scrollY; }, { passive: true });
  window.addEventListener('mousemove', e => {
    mouseX = (e.clientX / window.innerWidth  - 0.5) * 2;
    mouseY = (e.clientY / window.innerHeight - 0.5) * 2;
  });

  /* Sat orbit configs */
  const orbits = [
    { r: 2.0, speed: 1.0, phase: 0,   tilt: 0.4,  yr: 1.2, yr2: 0.8 },
    { r: 2.6, speed: 0.7, phase: 2.1, tilt: -0.6, yr: 0.7, yr2: 1.3 },
    { r: 1.6, speed: 1.4, phase: 4.2, tilt: 1.1,  yr: 1.5, yr2: 0.6 },
    { r: 3.0, speed: 0.5, phase: 1.0, tilt: -0.3, yr: 0.9, yr2: 1.1 },
    { r: 2.3, speed: 1.1, phase: 3.5, tilt: 0.8,  yr: 1.3, yr2: 0.7 },
  ];

  (function loop() {
    requestAnimationFrame(loop);
    t += 0.013;
    targScrollY += (scrollY - targScrollY) * 0.07;

    const vH = window.innerHeight;
    const docH = document.body.scrollHeight - vH;
    const spct = Math.min(targScrollY / (vH * 1.4), 1); // 0→1 over first 1.4 screens

    /* Shockwave expand */
    if (shockActive) {
      shockR = Math.min(shockR + 0.18, 5.5);
      shock.scale.setScalar(shockR / 0.1);
      shockMat.opacity = Math.max(0, 1 - shockR / 5.5);
    } else {
      shockMat.opacity = 0;
    }

    /* Logo: spin fast then disappear on scroll */
    LOGO.rotation.y = t * 0.55 + spct * Math.PI * 4;
    LOGO.rotation.x = Math.sin(t * 0.2) * 0.2 + mouseX * 0.06;
    LOGO.rotation.z = Math.cos(t * 0.15) * 0.08 + mouseY * 0.04;
    const logoScale = Math.max(0.001, 1 - spct * 1.1);
    LOGO.scale.setScalar(logoScale);
    LOGO.position.z  = -spct * 4;
    LOGO.position.y  =  spct * 2;
    gMat.opacity   = Math.max(0, 1 - spct * 1.5);
    gMat.transparent = true;
    gGlass.opacity = Math.max(0, 0.7 - spct * 1.2);
    gEdge.opacity  = Math.max(0, 1  - spct * 1.5);

    /* Satellite orbits */
    sats.forEach((s, i) => {
      const o = orbits[i];
      const angle = t * o.speed + o.phase;
      s.position.x = Math.cos(angle) * o.r;
      s.position.y = Math.sin(angle * 0.7) * o.r * Math.sin(o.tilt);
      s.position.z = Math.sin(angle) * o.r;
      s.rotation.x += 0.02 * o.yr;
      s.rotation.y += 0.015 * o.yr2;
    });

    /* Rings rotate */
    rings[0].rotation.z += 0.003;
    rings[1].rotation.y += 0.0025;
    rings[2].rotation.x += 0.002;

    /* Globe & particles drift */
    globe.rotation.y = t * 0.04;
    globe.rotation.x = t * 0.015;
    pts.rotation.y = t * 0.025;
    pts.rotation.x = t * 0.008;
    ptMat.opacity = 0.5 * (1 - spct * 0.5);

    /* Grid parallax */
    grid.position.z = -spct * 6;
    grid.material.opacity = 0.15 * (1 - spct * 0.6);

    /* Camera mouse follow */
    cam.position.x += (mouseX * 0.3 - cam.position.x) * 0.04;
    cam.position.y += (-mouseY * 0.22 - cam.position.y) * 0.04;
    cam.lookAt(0, 0, 0);

    /* Scrolled-in: subtle ambient scene rotation */
    if (spct >= 1) {
      scene.rotation.y = t * 0.004;
    }

    renderer.render(scene, cam);
  })();
})();

/* ═══════════════════════════════════════════
   CURSOR
═══════════════════════════════════════════ */
const cd = document.getElementById('cur-d');
const cr = document.getElementById('cur-r');
let cmx = -400, cmy = -400, crx = -400, cry = -400, cTick = 0;

document.addEventListener('mousemove', e => {
  cmx = e.clientX; cmy = e.clientY;
  cd.style.left = cmx + 'px'; cd.style.top = cmy + 'px';
  if (++cTick % 5 === 0) {
    const sp = document.createElement('div');
    sp.className = 'cspark';
    const dx = (Math.random() - 0.5) * 20;
    const dy = (Math.random() - 0.5) * 20;
    const sz = (Math.random() * 4 + 2) + 'px';
    sp.style.cssText = `left:${cmx}px;top:${cmy}px;width:${sz};height:${sz};background:rgba(218,168,74,${Math.random()*.5+.15});--dx:${dx}px;--dy:${dy}px`;
    document.body.appendChild(sp);
    setTimeout(() => sp.remove(), 800);
  }
});
(function rl() {
  crx += (cmx - crx) * 0.1;
  cry += (cmy - cry) * 0.1;
  cr.style.left = crx + 'px';
  cr.style.top  = cry + 'px';
  requestAnimationFrame(rl);
})();

document.querySelectorAll('a,button,.oc,.cc,.v,.tli,.btn-main,.btn-ghost').forEach(el => {
  el.addEventListener('mouseenter', () => document.body.classList.add('ch'));
  el.addEventListener('mouseleave', () => document.body.classList.remove('ch'));
});
document.querySelectorAll('p,.sbody,.tld,.cinfo p,.vt p').forEach(el => {
  el.addEventListener('mouseenter', () => document.body.classList.add('txt'));
  el.addEventListener('mouseleave', () => document.body.classList.remove('txt'));
});
document.addEventListener('mousedown', () => document.body.classList.add('ck'));
document.addEventListener('mouseup',   () => document.body.classList.remove('ck'));

/* ═══════════════════════════════════════════
   PROGRESS + NAV
═══════════════════════════════════════════ */
const pb = document.getElementById('pb');
window.addEventListener('scroll', () => {
  pb.style.transform = 'scaleX(' + Math.min(scrollY / (document.body.scrollHeight - innerHeight), 1) + ')';
  document.getElementById('nav').classList.toggle('sc', scrollY > 60);
}, { passive: true });

/* ═══════════════════════════════════════════
   SCROLL REVEAL
═══════════════════════════════════════════ */
const ro = new IntersectionObserver(es => {
  es.forEach(e => { if (e.isIntersecting) { e.target.classList.add('vis'); ro.unobserve(e.target); } });
}, { threshold: 0.08, rootMargin: '0px 0px -30px 0px' });
document.querySelectorAll('.rv').forEach(el => ro.observe(el));

/* ═══════════════════════════════════════════
   COUNTERS
═══════════════════════════════════════════ */
function animN(el) {
  const t = +el.dataset.count, sfx = el.dataset.sfx || '', dur = 1800, s = performance.now();
  (function f(n) {
    const p = Math.min((n - s) / dur, 1), e = 1 - Math.pow(1 - p, 3);
    el.textContent = Math.round(e * t) + (p >= 1 ? sfx : '');
    if (p < 1) requestAnimationFrame(f);
  })(s);
}
const co = new IntersectionObserver(es => {
  es.forEach(e => { if (e.isIntersecting) { animN(e.target); co.unobserve(e.target); } });
}, { threshold: 0.5 });
document.querySelectorAll('[data-count]').forEach(el => co.observe(el));

/* ═══════════════════════════════════════════
   MAGNETIC BUTTONS
═══════════════════════════════════════════ */
document.querySelectorAll('.btn-main,.btn-ghost,.ncta').forEach(btn => {
  btn.addEventListener('mousemove', e => {
    const r = btn.getBoundingClientRect();
    btn.style.transform = `translate(${(e.clientX-r.left-r.width/2)*.2}px,${(e.clientY-r.top-r.height/2)*.2-3}px)`;
  });
  btn.addEventListener('mouseleave', () => { btn.style.transform = ''; });
});

/* ═══════════════════════════════════════════
   PARALLAX HERO ON SCROLL
═══════════════════════════════════════════ */
const heroInner = document.querySelector('.hero-inner');
window.addEventListener('scroll', () => {
  if (scrollY < innerHeight && heroInner) {
    heroInner.style.transform = `translateY(${scrollY * 0.15}px)`;
    heroInner.style.opacity = Math.max(0, 1 - scrollY / (innerHeight * 0.7));
  }
}, { passive: true });
</script>
</body>
</html>
