<!DOCTYPE html>
<html lang="en" data-mode="pm">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Parth Prakash Mall · PM × Engineer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Caveat:wght@400;600;700;800&family=Patrick+Hand&family=Kalam:wght@300;400;700&family=JetBrains+Mono:ital,wght@0,300;0,400;0,600;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}

/* ══════════════════════════════════════════
   PM  MODE  VARIABLES  (paper + doodle)
══════════════════════════════════════════ */
:root{
  --bg:#faf7f0;--surface:#f0e8d8;
  --card:rgba(255,253,245,0.92);
  --border:rgba(30,40,65,0.2);--border-h:rgba(30,40,65,0.5);
  --acc:#c0392b;--acc2:#e74c3c;
  --acc-dim:rgba(192,57,43,0.1);--acc-glow:rgba(192,57,43,0.22);
  --acc-rgb:192,57,43;
  --tx:#1e2841;--tx2:#7a6652;--tx3:#b8a898;
  --ff-d:'Caveat',cursive;
  --ff-b:'Patrick Hand',cursive;
  --ff-m:'Kalam',cursive;
  --ease:cubic-bezier(.4,0,.2,1);--ease-spring:cubic-bezier(.34,1.56,.64,1);
  --r:4px 8px 5px 6px / 6px 5px 8px 4px;
  --r-sm:3px 5px 4px 4px / 4px 4px 5px 3px;
}

/* ══════════════════════════════════════════
   SDE  MODE  VARIABLES  (terminal + code)
══════════════════════════════════════════ */
html[data-mode=sde]{
  --bg:#060810;--surface:#0d0e18;
  --card:rgba(0,232,122,0.03);
  --border:rgba(0,232,122,0.12);--border-h:rgba(0,232,122,0.3);
  --acc:#00e87a;--acc2:#00ff88;
  --acc-dim:rgba(0,232,122,0.08);--acc-glow:rgba(0,232,122,0.3);
  --acc-rgb:0,232,122;
  --tx:#cdd6f4;--tx2:#6c7086;--tx3:#313244;
  --ff-d:'JetBrains Mono',monospace;
  --ff-b:'JetBrains Mono',monospace;
  --ff-m:'JetBrains Mono',monospace;
  --r:4px;--r-sm:3px;
}

/* ══════════════════════════════════════════
   BODY & BACKGROUNDS
══════════════════════════════════════════ */
body{
  background:var(--bg);color:var(--tx);font-family:var(--ff-b);
  line-height:1.6;overflow-x:hidden;
  transition:background .6s,color .5s,font-family .55s;
}

/* PM: NOTEBOOK PAPER */
html[data-mode=pm] body{
  background-color:#faf7f0;
  background-image:
    linear-gradient(90deg,transparent 68px,rgba(210,70,70,.2) 68px,rgba(210,70,70,.2) 70px,transparent 70px),
    repeating-linear-gradient(transparent,transparent 27px,rgba(90,120,200,.11) 27px,rgba(90,120,200,.11) 28px);
}

/* PM: watercolor blobs */
html[data-mode=pm] .orb{filter:blur(80px);opacity:.08}
html[data-mode=pm] .orb1{background:radial-gradient(circle,#f6b93b,transparent 65%);top:0;left:-100px}
html[data-mode=pm] .orb2{background:radial-gradient(circle,#c0392b,transparent 65%);top:25%;right:-120px;opacity:.06}
html[data-mode=pm] .orb3{background:radial-gradient(circle,#2980b9,transparent 65%);bottom:100px;left:30%;opacity:.05}

/* SDE: DOT GRID */
html[data-mode=sde] body{
  background-color:#060810;
  background-image:radial-gradient(circle,rgba(0,232,122,.045) 1px,transparent 1px);
  background-size:28px 28px;
}

/* SDE: SCANLINES */
html[data-mode=sde] body::after{
  content:'';position:fixed;inset:0;z-index:2000;pointer-events:none;
  background:repeating-linear-gradient(0deg,rgba(0,0,0,.04) 0px,rgba(0,0,0,.04) 1px,transparent 1px,transparent 4px);
}

/* SDE: CRT flicker */
@keyframes flicker{0%,100%{opacity:1}96%{opacity:1}97%{opacity:.98}98%{opacity:1}}
html[data-mode=sde] main{animation:flicker 8s ease infinite}

::-webkit-scrollbar{width:3px}
::-webkit-scrollbar-track{background:var(--bg)}
::-webkit-scrollbar-thumb{background:var(--acc);border-radius:2px}
::selection{background:var(--acc-dim);color:var(--acc)}

/* ══════════════════════════════════════════
   ANIMATED BACKGROUND LAYERS
══════════════════════════════════════════ */
.bg-canvas{position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden}
.orb{position:absolute;border-radius:50%;animation:drift 22s ease-in-out infinite}
.orb1{width:600px;height:600px;top:-100px;left:-150px}
.orb2{width:500px;height:500px;top:30%;right:-200px;animation-duration:30s;animation-delay:-9s}
.orb3{width:400px;height:400px;bottom:-50px;left:40%;animation-duration:18s;animation-delay:-14s}
@keyframes drift{0%,100%{transform:translate(0,0)}30%{transform:translate(50px,-40px)}70%{transform:translate(-40px,55px)}}
html[data-mode=sde] .orb1{background:radial-gradient(circle,rgba(0,232,122,.12),transparent 65%);filter:blur(90px);opacity:.12}
html[data-mode=sde] .orb2{background:radial-gradient(circle,rgba(100,0,255,.08),transparent 65%);filter:blur(80px);opacity:.08}
html[data-mode=sde] .orb3{background:radial-gradient(circle,rgba(0,232,122,.07),transparent 65%);filter:blur(70px);opacity:.07}

/* Matrix rain canvas */
#matrix-canvas{position:fixed;inset:0;z-index:0;opacity:0;transition:opacity 1.2s ease;pointer-events:none}
html[data-mode=sde] #matrix-canvas{opacity:.18}

/* ══════════════════════════════════════════
   NAV
══════════════════════════════════════════ */
nav{
  position:fixed;top:0;left:0;right:0;z-index:200;
  display:flex;align-items:center;justify-content:space-between;
  padding:13px 52px;
  transition:all .5s;
}

/* PM NAV: notebook header */
html[data-mode=pm] nav{
  background:rgba(250,247,240,.92);
  backdrop-filter:blur(8px);
  border-bottom:2px solid rgba(30,40,65,.15);
  box-shadow:0 2px 0 rgba(30,40,65,.06),0 4px 0 rgba(30,40,65,.03);
}
html[data-mode=pm] nav::after{
  content:'';position:absolute;bottom:-5px;left:0;right:0;height:3px;
  border-bottom:1px solid rgba(30,40,65,.08);
}

/* SDE NAV: IDE titlebar */
html[data-mode=sde] nav{
  background:rgba(6,8,16,.9);
  backdrop-filter:blur(30px);
  border-bottom:1px solid rgba(0,232,122,.12);
}
html[data-mode=sde] nav::before{
  content:'● ● ●';position:absolute;left:20px;font-size:.55rem;
  color:rgba(0,232,122,.3);letter-spacing:4px;pointer-events:none;
}
html[data-mode=sde] nav::after{
  content:'';position:absolute;bottom:0;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,var(--acc),transparent);opacity:.25;
}

.nav-logo{font-family:var(--ff-d);font-weight:800;font-size:1.15rem;letter-spacing:-.01em;transition:all .5s;cursor:default}
.nav-logo span{color:var(--acc)}
html[data-mode=sde] .nav-logo::before{content:'> ';color:var(--acc);font-size:.9rem;opacity:.7}

.nav-links{display:flex;gap:30px;list-style:none}
.nav-links a{font-size:.82rem;color:var(--tx2);text-decoration:none;transition:color .25s;position:relative;padding-bottom:2px;font-family:var(--ff-b)}
.nav-links a::after{content:'';position:absolute;bottom:0;left:0;width:0;height:1.5px;background:var(--acc);transition:width .3s}
.nav-links a:hover{color:var(--tx)}.nav-links a:hover::after{width:100%}
html[data-mode=sde] .nav-links a::before{content:'./';color:var(--acc);opacity:.5;font-family:var(--ff-m);font-size:.75rem}
.nav-r{display:flex;align-items:center;gap:12px}

/* ══════════════════════════════════════════
   MODE SWITCHER
══════════════════════════════════════════ */
.ms{
  display:flex;align-items:center;gap:10px;
  border-radius:100px;padding:5px 11px 5px 14px;
  cursor:pointer;user-select:none;transition:all .35s;
  font-family:var(--ff-m);
}
html[data-mode=pm] .ms{
  background:rgba(255,252,245,.8);
  border:2px solid rgba(30,40,65,.22);
  box-shadow:2px 2px 0 rgba(30,40,65,.1);
}
html[data-mode=pm] .ms:hover{border-color:var(--acc);box-shadow:3px 3px 0 rgba(192,57,43,.2)}
html[data-mode=sde] .ms{
  background:rgba(0,232,122,.05);
  border:1px solid rgba(0,232,122,.25);
  box-shadow:0 0 16px rgba(0,232,122,.1);
}
html[data-mode=sde] .ms:hover{border-color:var(--acc);box-shadow:0 0 24px rgba(0,232,122,.2)}

.ms-lbl{font-size:.7rem;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--tx2);transition:color .3s}
.ms-lbl.on{color:var(--acc)}
.ms-track{width:42px;height:22px;background:var(--acc-dim);border-radius:100px;position:relative;border:1px solid rgba(var(--acc-rgb),.3);transition:all .5s}
.ms-thumb{
  width:16px;height:16px;background:var(--acc);border-radius:50%;
  position:absolute;top:2px;left:2px;
  transition:all .45s var(--ease-spring);
}
html[data-mode=pm] .ms-thumb{box-shadow:1px 1px 0 rgba(30,40,65,.3)}
html[data-mode=sde] .ms-thumb{box-shadow:0 0 12px var(--acc-glow)}
html[data-mode=sde] .ms-thumb{left:calc(100% - 18px)}

/* BUTTONS */
.btn-cta,.btn-primary,.btn-ghost{
  display:inline-flex;align-items:center;gap:7px;font-family:var(--ff-b);
  font-size:.88rem;text-decoration:none;cursor:pointer;border:none;
  transition:all .3s var(--ease);
}
html[data-mode=pm] .btn-cta,html[data-mode=pm] .btn-primary{
  padding:10px 22px;background:var(--acc);color:#fff;
  font-family:var(--ff-d);font-size:.95rem;font-weight:700;
  border:2px solid var(--tx);
  border-radius:2px 6px 4px 5px / 5px 3px 6px 4px;
  box-shadow:3px 3px 0 var(--tx);
}
html[data-mode=pm] .btn-cta:hover,html[data-mode=pm] .btn-primary:hover{transform:translate(-1px,-1px);box-shadow:4px 4px 0 var(--tx)}
html[data-mode=pm] .btn-ghost{
  padding:10px 22px;background:transparent;color:var(--tx);
  font-family:var(--ff-d);font-size:.95rem;
  border:2px dashed var(--border);
  border-radius:2px 6px 4px 5px / 5px 3px 6px 4px;
}
html[data-mode=pm] .btn-ghost:hover{border-color:var(--acc);color:var(--acc)}

html[data-mode=sde] .btn-cta,html[data-mode=sde] .btn-primary{
  padding:10px 22px;background:var(--acc);color:#000;font-weight:700;
  border-radius:4px;font-family:var(--ff-m);font-size:.82rem;letter-spacing:.02em;
}
html[data-mode=sde] .btn-cta::before{content:'$ ';opacity:.7}
html[data-mode=sde] .btn-cta:hover,html[data-mode=sde] .btn-primary:hover{transform:translateY(-2px);box-shadow:0 8px 28px var(--acc-glow)}
html[data-mode=sde] .btn-ghost{
  padding:10px 22px;background:transparent;color:var(--tx2);
  border:1px solid var(--border);border-radius:4px;font-family:var(--ff-m);font-size:.78rem;
}
html[data-mode=sde] .btn-ghost::before{content:'# ';color:var(--acc);opacity:.6}
html[data-mode=sde] .btn-ghost:hover{border-color:var(--acc);color:var(--acc);background:var(--acc-dim)}

/* FLASH */
#flash{position:fixed;inset:0;z-index:999;pointer-events:none;opacity:0}
#flash.go{animation:fl .6s var(--ease) forwards}
@keyframes fl{0%{opacity:0}15%{opacity:.14}100%{opacity:0}}

/* ══════════════════════════════════════════
   LAYOUT
══════════════════════════════════════════ */
main{position:relative;z-index:1;padding-top:72px}
section{padding:90px 52px;max-width:1320px;margin:0 auto}

/* PM: SECTION LABELS look like pen annotations */
html[data-mode=pm] .sec-label{
  font-family:var(--ff-d);font-size:.85rem;font-weight:700;color:var(--acc);
  margin-bottom:10px;letter-spacing:.02em;
  display:inline-flex;align-items:center;gap:8px;
}
html[data-mode=pm] .sec-label::before{content:'→';font-size:1rem;opacity:.7}

/* SDE: SECTION LABELS look like code comments */
html[data-mode=sde] .sec-label{
  font-family:var(--ff-m);font-size:.72rem;color:var(--tx2);
  margin-bottom:8px;letter-spacing:.05em;opacity:1;
  display:block;
}
html[data-mode=sde] .sec-label::before{content:'/* '}
html[data-mode=sde] .sec-label::after{content:' */'}

.sec-title{font-family:var(--ff-d);font-size:clamp(2rem,3vw,2.8rem);font-weight:800;letter-spacing:-.02em;margin-bottom:10px;transition:all .5s;line-height:1.1}

/* PM: SECTION TITLE with hand-drawn underline */
html[data-mode=pm] .sec-title{
  font-family:'Caveat',cursive;font-size:clamp(2.2rem,3vw,3rem);
  color:var(--tx);letter-spacing:.01em;
}
html[data-mode=pm] .sec-title::after{
  content:'';display:block;margin-top:6px;
  height:3px;width:70%;max-width:280px;
  background:var(--acc);
  border-radius:0 3px 1px 2px;
  transform:rotate(-.3deg);
  opacity:.7;
}

/* SDE: SECTION TITLE looks like function declaration */
html[data-mode=sde] .sec-title{
  font-family:var(--ff-m);font-size:clamp(1.4rem,2.2vw,1.9rem);
  color:var(--tx);
}
html[data-mode=sde] .sec-title::before{content:'function ';color:#7c3aed;font-size:.75em;opacity:.8}
html[data-mode=sde] .sec-title::after{content:'() {';color:var(--tx2);font-size:.75em;opacity:.7}

.sec-sub{font-size:.95rem;color:var(--tx2);max-width:500px;margin-bottom:52px;font-weight:300;line-height:1.75;font-family:var(--ff-b)}
html[data-mode=sde] .sec-sub{font-family:var(--ff-m);font-size:.8rem}
html[data-mode=sde] .sec-sub::before{content:'// ';opacity:.6}

/* VISIBILITY */
.pm-only{display:block}.sde-only{display:none}
html[data-mode=sde] .pm-only{display:none}
html[data-mode=sde] .sde-only{display:block}
.pm-flex{display:flex}.sde-flex{display:none}
html[data-mode=sde] .pm-flex{display:none}
html[data-mode=sde] .sde-flex{display:flex}

/* ══════════════════════════════════════════
   HERO
══════════════════════════════════════════ */
#hero{min-height:92vh;display:flex;flex-direction:column;justify-content:center;padding-top:120px;padding-bottom:60px}

.hero-badge{display:inline-flex;align-items:center;gap:10px;margin-bottom:28px;width:fit-content;font-family:var(--ff-m)}
html[data-mode=pm] .hero-badge{
  font-family:var(--ff-d);font-size:.9rem;color:var(--tx2);padding:5px 0;
  border-bottom:2px dashed rgba(30,40,65,.25);letter-spacing:.02em;
}
html[data-mode=sde] .hero-badge{
  font-size:.7rem;letter-spacing:.12em;text-transform:uppercase;color:var(--acc);
  padding:6px 14px;border:1px solid rgba(var(--acc-rgb),.25);
  background:rgba(var(--acc-rgb),.06);border-radius:4px;backdrop-filter:blur(8px);
}
.badge-dot{width:7px;height:7px;border-radius:50%;background:var(--acc);animation:pd 2.4s ease infinite}
html[data-mode=pm] .badge-dot{display:none}
@keyframes pd{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.35;transform:scale(.7)}}

/* PM HERO H1: giant handwriting */
html[data-mode=pm] .hero-h1{
  font-family:'Caveat',cursive;font-size:clamp(3rem,6.5vw,6.2rem);
  font-weight:800;line-height:1.02;letter-spacing:-.01em;
  color:var(--tx);margin-bottom:22px;max-width:880px;
}
/* SDE HERO H1: terminal prompt style */
html[data-mode=sde] .hero-h1{
  font-family:var(--ff-m);font-size:clamp(1.8rem,3.5vw,3.2rem);
  font-weight:400;line-height:1.4;color:var(--tx);margin-bottom:22px;max-width:900px;
}
.hero-h1 .dim{color:var(--tx2)}.hero-h1 .hi{color:var(--acc)}

/* PM: accent word gets a marker highlight */
html[data-mode=pm] .hero-h1 .hi{
  color:var(--acc);position:relative;display:inline-block;
  text-decoration:underline;text-decoration-color:rgba(192,57,43,.4);text-decoration-thickness:3px;text-underline-offset:4px;
}

.hero-sub{font-size:1.05rem;color:var(--tx2);max-width:510px;line-height:1.78;margin-bottom:46px;font-weight:300}
html[data-mode=pm] .hero-sub{font-family:'Patrick Hand',cursive;font-size:1.1rem;font-weight:400}
html[data-mode=sde] .hero-sub{font-family:var(--ff-m);font-size:.82rem}
html[data-mode=sde] .hero-sub::before{content:'// ';opacity:.5}

.hero-acts{display:flex;gap:14px;flex-wrap:wrap;margin-bottom:64px}

/* ── KPI CARDS ── */
.kpi-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;max-width:760px}

html[data-mode=pm] .kpi-card{
  background:rgba(255,252,244,.95);
  border:2px solid var(--tx);
  border-radius:var(--r);
  padding:20px 22px;position:relative;overflow:hidden;
  box-shadow:3px 3px 0 rgba(30,40,65,.12);
  transition:all .3s;
}
html[data-mode=pm] .kpi-card:nth-child(odd){transform:rotate(-.4deg)}
html[data-mode=pm] .kpi-card:nth-child(even){transform:rotate(.3deg)}
html[data-mode=pm] .kpi-card:hover{transform:rotate(0) translateY(-3px);box-shadow:5px 5px 0 rgba(192,57,43,.2)}
html[data-mode=pm] .kpi-card::after{content:'';position:absolute;bottom:0;left:0;right:0;height:3px;background:var(--acc);opacity:.6}

html[data-mode=sde] .kpi-card{
  background:rgba(0,232,122,.03);border:1px solid rgba(0,232,122,.15);
  border-radius:4px;padding:20px 22px;position:relative;
  transition:all .35s;
}
html[data-mode=sde] .kpi-card::before{content:'// metric';position:absolute;top:8px;right:10px;font-family:var(--ff-m);font-size:.58rem;color:var(--tx3);opacity:.7}
html[data-mode=sde] .kpi-card:hover{border-color:rgba(0,232,122,.35);box-shadow:0 0 24px rgba(0,232,122,.1)}

.kpi-val{font-family:var(--ff-d);font-size:2.2rem;font-weight:800;color:var(--acc);line-height:1;margin-bottom:6px;transition:font-family .5s}
html[data-mode=pm] .kpi-val{font-family:'Caveat',cursive;font-size:2.4rem}
html[data-mode=sde] .kpi-val{font-family:var(--ff-m);font-size:1.8rem;color:var(--acc)}
.kpi-lbl{font-size:.68rem;color:var(--tx2);text-transform:uppercase;letter-spacing:.08em;font-family:var(--ff-m)}
html[data-mode=pm] .kpi-lbl{font-family:'Patrick Hand',cursive;font-size:.78rem;text-transform:none;letter-spacing:0}

/* ── TERMINAL ── */
.terminal{
  background:rgba(6,8,16,.97);border:1px solid var(--border);border-radius:12px;overflow:hidden;
  max-width:700px;font-family:var(--ff-m);font-size:.82rem;line-height:1.78;
  box-shadow:0 24px 80px rgba(0,0,0,.5);
}
.t-head{display:flex;align-items:center;gap:7px;padding:12px 18px;background:rgba(255,255,255,.03);border-bottom:1px solid var(--border)}
.t-dot{width:10px;height:10px;border-radius:50%}
.t-r{background:#ff5f56}.t-y{background:#ffbd2e}.t-g{background:#27c93f}
.t-fn{margin-left:10px;font-size:.7rem;color:var(--tx2)}
.t-body{padding:22px 26px;min-height:220px}
.t-body pre{white-space:pre-wrap;word-break:break-word}
.t-k{color:#c792ea}.t-s{color:var(--acc)}.t-cl{color:#82aaff}.t-n{color:#f78c6c}.t-c{color:#3a3a5a}
.cur{display:inline-block;width:2px;height:1.05em;background:var(--acc);vertical-align:text-bottom;animation:bl 1s step-end infinite}
@keyframes bl{50%{opacity:0}}

/* ══════════════════════════════════════════
   GLASS CARD BASE
══════════════════════════════════════════ */
.glass-card{
  background:var(--card);border:1px solid var(--border);
  border-radius:var(--r);padding:28px;
  position:relative;
  overflow:hidden;            /* SDE needs this for the top-gradient line */
}

/* PM: paper card — overflow visible so irregular border-radius shows cleanly */
html[data-mode=pm] .glass-card{
  background:rgba(255,253,245,.92);
  border:2px solid rgba(30,40,65,.2);
  border-radius:var(--r);
  box-shadow:3px 3px 0 rgba(30,40,65,.1);
  overflow:visible;
}
html[data-mode=pm] .glass-card:hover{
  box-shadow:5px 5px 0 rgba(192,57,43,.15);
  border-color:var(--acc);
}

html[data-mode=sde] .glass-card{
  background:rgba(0,232,122,.025);border:1px solid rgba(0,232,122,.1);border-radius:4px;
}
html[data-mode=sde] .glass-card::before{
  content:'';position:absolute;top:0;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,rgba(0,232,122,.4),transparent);
}
html[data-mode=sde] .glass-card:hover{border-color:rgba(0,232,122,.25);box-shadow:0 0 30px rgba(0,232,122,.07)}

.gc-title{font-family:var(--ff-d);font-size:1rem;font-weight:700;margin-bottom:4px;transition:all .5s}
html[data-mode=pm] .gc-title{font-family:'Caveat',cursive;font-size:1.25rem}
html[data-mode=sde] .gc-title{font-family:var(--ff-m);font-size:.9rem;color:var(--acc)}
html[data-mode=sde] .gc-title::before{content:'> ';opacity:.6}
.gc-sub{font-size:.7rem;color:var(--tx2);margin-bottom:22px;font-family:var(--ff-m)}
html[data-mode=pm] .gc-sub{font-family:'Patrick Hand',cursive;font-size:.82rem}
html[data-mode=sde] .gc-sub::before{content:'// ';opacity:.5}

/* MATRIX widget */
.matrix{
  position:relative;width:100%;
  height:240px;               /* fixed height instead of aspect-ratio — prevents card height mismatch */
  border:1px solid var(--border);border-radius:var(--r-sm);
  background:var(--surface);overflow:hidden;
  flex-shrink:0;
}
html[data-mode=pm] .matrix{
  /* Handled inside #skills-inner .glass-card rule above */
}
.mx-h{position:absolute;height:1px;left:0;right:0;top:50%;background:var(--border)}
.mx-v{position:absolute;width:1px;top:0;bottom:0;left:50%;background:var(--border)}
.mx-q{position:absolute;font-size:.58rem;color:var(--tx3);padding:7px;text-transform:uppercase;letter-spacing:.07em}
html[data-mode=pm] .mx-q{font-family:'Patrick Hand',cursive;font-size:.68rem;color:var(--tx2)}
.mx-ax{position:absolute;font-size:.6rem;color:var(--tx3);text-transform:uppercase;letter-spacing:.1em}
html[data-mode=pm] .mx-ax{font-family:'Patrick Hand',cursive;font-size:.7rem}
.mx-ax-x{bottom:9px;left:0;right:0;text-align:center}
.mx-ax-y{left:5px;top:50%;transform:translateY(-50%) rotate(-90deg);white-space:nowrap}

.fdot{
  position:absolute;width:40px;height:40px;border-radius:50%;
  background:var(--acc-dim);border:1.5px solid rgba(var(--acc-rgb),.5);
  cursor:pointer;display:flex;align-items:center;justify-content:center;
  font-size:.52rem;color:var(--acc);text-align:center;line-height:1.25;
  transform:translate(-50%,-50%);transition:all .35s var(--ease-spring);
}
html[data-mode=pm] .fdot{font-family:'Kalam',cursive;font-size:.6rem}
.fdot:hover,.fdot.lit{transform:translate(-50%,-50%) scale(1.2);box-shadow:0 0 20px var(--acc-glow);border-color:var(--acc)}
html[data-mode=pm] .fdot.lit{background:var(--acc);color:#fff;font-weight:700}
html[data-mode=sde] .fdot.lit{background:var(--acc);color:#000;font-weight:700}

#mx-tip{margin-top:12px;min-height:44px;font-size:.76rem;color:var(--tx2);padding:11px 14px;background:var(--surface);border-radius:var(--r-sm);border:1px solid var(--border);display:none;animation:fadeIn .2s ease}
html[data-mode=pm] #mx-tip{font-family:'Patrick Hand',cursive;font-size:.85rem;background:rgba(255,252,244,.9);border:1.5px dashed var(--border)}
@keyframes fadeIn{from{opacity:0;transform:translateY(4px)}to{opacity:1;transform:none}}

/* TECH PILLS */
.tech-grid{display:flex;flex-wrap:wrap;gap:9px}
.tp{padding:8px 15px;background:var(--card);border:1px solid var(--border);border-radius:100px;font-family:var(--ff-m);font-size:.73rem;color:var(--tx2);cursor:pointer;transition:all .3s}
html[data-mode=pm] .tp{font-family:'Kalam',cursive;font-size:.82rem;border:2px solid rgba(30,40,65,.2);border-radius:var(--r-sm);background:rgba(255,252,244,.8);box-shadow:2px 2px 0 rgba(30,40,65,.08);border-radius:2px 5px 4px 3px/3px 4px 5px 2px}
html[data-mode=pm] .tp:hover{border-color:var(--acc);color:var(--acc);transform:rotate(-.5deg) translateY(-2px);box-shadow:3px 3px 0 rgba(192,57,43,.15)}
html[data-mode=sde] .tp{border-radius:3px;border:1px solid rgba(0,232,122,.12);font-size:.72rem}
html[data-mode=sde] .tp:hover,html[data-mode=sde] .tp.on{background:rgba(0,232,122,.08);border-color:rgba(0,232,122,.3);color:var(--acc);box-shadow:0 0 12px rgba(0,232,122,.1)}
html[data-mode=pm] .tp.on{background:rgba(192,57,43,.08);border-color:var(--acc);color:var(--acc)}
.tp .cnt{display:inline-block;margin-left:5px;background:var(--acc);color:#000;font-size:.57rem;width:15px;height:15px;border-radius:50%;text-align:center;line-height:15px;font-weight:700;vertical-align:middle}
html[data-mode=pm] .tp .cnt{color:#fff}
#tech-panel{margin-top:18px;padding:14px 16px;background:var(--surface);border-radius:var(--r-sm);border:1px solid var(--border);min-height:58px;font-size:.78rem;color:var(--tx2);font-family:var(--ff-m);line-height:1.68;display:none;animation:fadeIn .2s ease}
html[data-mode=pm] #tech-panel{font-family:'Patrick Hand',cursive;font-size:.88rem;border:1.5px dashed var(--border);background:rgba(255,252,244,.9);border-radius:var(--r-sm)}

/* TAGS */
.tag-row{display:flex;flex-wrap:wrap;gap:7px;margin-top:16px}
.tag{font-family:var(--ff-m);font-size:.63rem;padding:4px 10px;border-radius:5px;background:var(--surface);border:1px solid var(--border);color:var(--tx2)}
.tag-acc{background:var(--acc-dim);border-color:rgba(var(--acc-rgb),.3);color:var(--acc)}
html[data-mode=pm] .tag{font-family:'Kalam',cursive;font-size:.75rem;border:1.5px solid rgba(30,40,65,.2);background:rgba(255,252,244,.8);border-radius:2px 4px 3px 3px/3px 3px 4px 2px;box-shadow:1px 1px 0 rgba(30,40,65,.08)}
html[data-mode=pm] .tag-acc{background:rgba(192,57,43,.08);border-color:rgba(192,57,43,.35);color:var(--acc)}
html[data-mode=sde] .tag{border-radius:3px}

/* ── SKILLS INNER GRID ── */
#skills-inner{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:20px;
  align-items:start;
}
/* PM mode: single column = full-width cards (bigger breadth, less wrapping = smaller length) */
html[data-mode=pm] #skills-inner{
  grid-template-columns:1fr;
}
/* SDE mode: single column, sde card full width */
html[data-mode=sde] #skills-inner{
  grid-template-columns:1fr;
}
html[data-mode=sde] #skills-inner .sde-only{
  display:block;
  width:100%;
}
/* Glass cards inside skills as flex columns */
#skills-inner .glass-card{
  display:flex;
  flex-direction:column;
  overflow:visible;
}
/* PM matrix: reduce height since card is now full-width landscape */
html[data-mode=pm] .matrix{
  border:2px solid rgba(30,40,65,.18);
  border-radius:var(--r-sm);
  background:#faf5e8;
  height:180px; /* shorter — card is wide so content spreads horizontally */
}
/* ── BENTO GRID ── */
#projects .bento{
  display:grid;
  grid-template-columns:repeat(12,1fr);
  grid-auto-rows:minmax(190px,auto);
  gap:16px;
}
.s7{grid-column:span 7}.s5{grid-column:span 5}.s4{grid-column:span 4}
.s6{grid-column:span 6}.s3{grid-column:span 3}.s8{grid-column:span 8}
.s12{grid-column:span 12}.r2{grid-row:span 2}

/* KrishiRakshak featured card: left info + right tabs, side by side */
.kr-split{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:28px;
  align-items:start;
  margin-top:14px;
}
html[data-mode=pm] .kr-split{
  gap:32px;
  padding-top:14px;
  border-top:1.5px dashed rgba(30,40,65,.15);
}
html[data-mode=sde] .kr-split{
  gap:28px;
  padding-top:14px;
  border-top:1px solid rgba(0,232,122,.1);
}

/* ── BENTO CARD BASE ── */
.bc{
  background:var(--card);border:1px solid var(--border);border-radius:var(--r);
  padding:26px;position:relative;overflow:hidden;display:flex;flex-direction:column;
  transition:all .4s var(--ease);
}

/* PM CARDS: paper cutouts with ink borders */
html[data-mode=pm] .bc{
  background:rgba(255,253,245,.92);
  border:2px solid rgba(30,40,65,.22);
  border-radius:var(--r);
  box-shadow:3px 3px 0 rgba(30,40,65,.12),5px 5px 0 rgba(30,40,65,.05);
}
html[data-mode=pm] .bc:nth-child(3n+1){transform:rotate(-.35deg)}
html[data-mode=pm] .bc:nth-child(3n+2){transform:rotate(.3deg)}
html[data-mode=pm] .bc:nth-child(3n){transform:rotate(-.2deg)}
html[data-mode=pm] .bc:hover{
  transform:rotate(0) translateY(-5px) !important;
  box-shadow:5px 5px 0 rgba(192,57,43,.2),8px 8px 0 rgba(192,57,43,.08);
  border-color:var(--acc);
}
/* Paper corner fold effect */
html[data-mode=pm] .bc::after{
  content:'';position:absolute;bottom:0;right:0;
  width:18px;height:18px;
  background:linear-gradient(225deg,rgba(30,40,65,.08) 50%,transparent 50%);
  border-top:1px solid rgba(30,40,65,.15);border-left:1px solid rgba(30,40,65,.15);
}

/* SDE CARDS: code blocks */
html[data-mode=sde] .bc{
  background:rgba(0,232,122,.025);
  border:1px solid rgba(0,232,122,.1);
  border-radius:4px;
}
html[data-mode=sde] .bc::before{
  content:'';position:absolute;top:0;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,rgba(0,232,122,.35),transparent);
}
html[data-mode=sde] .bc:hover{
  border-color:rgba(0,232,122,.28);
  transform:translateY(-4px);
  box-shadow:0 16px 50px rgba(0,0,0,.35),0 0 0 1px rgba(0,232,122,.12);
}
html[data-mode=sde] .bc:hover::before{opacity:1}

/* CODE BLOCK HEADER in SDE mode */
html[data-mode=sde] .bc{
  padding-top: 38px; /* space for the file-path header bar */
}
html[data-mode=sde] .bc::after{
  content:attr(data-file);
  position:absolute;top:0;left:0;right:0;
  padding:7px 14px;
  font-family:var(--ff-m);font-size:.6rem;color:var(--tx2);
  background:rgba(0,0,0,.25);border-bottom:1px solid rgba(0,232,122,.1);
  display:block;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;
}
/* PM corner fold stays small and doesn't need padding compensation */
html[data-mode=pm] .bc{
  padding-top: 26px;
}

.bc-tag{display:inline-flex;align-items:center;gap:5px;font-family:var(--ff-m);font-size:.62rem;letter-spacing:.1em;text-transform:uppercase;color:var(--acc);margin-bottom:12px;opacity:.85}
.bc-tag::before{content:'';width:5px;height:5px;border-radius:50%;background:var(--acc)}
html[data-mode=pm] .bc-tag{font-family:'Patrick Hand',cursive;font-size:.75rem;text-transform:none;letter-spacing:0;opacity:1}
html[data-mode=pm] .bc-tag::before{border-radius:0;transform:rotate(45deg);width:6px;height:6px;background:none;border:2px solid var(--acc)}
html[data-mode=sde] .bc-tag::before{box-shadow:0 0 6px var(--acc)}

.bc-title{font-family:var(--ff-d);font-size:1.15rem;font-weight:700;margin-bottom:8px;line-height:1.3}
html[data-mode=pm] .bc-title{font-family:'Caveat',cursive;font-size:1.4rem;color:var(--tx)}
html[data-mode=sde] .bc-title{font-family:var(--ff-m);font-size:.95rem;color:var(--acc)}
/* NO ::before on bc-title — it shifts card heights */

.bc-desc{font-size:.8rem;color:var(--tx2);line-height:1.68;flex:1}
html[data-mode=pm] .bc-desc{font-family:'Patrick Hand',cursive;font-size:.9rem}
html[data-mode=sde] .bc-desc{font-family:var(--ff-m);font-size:.74rem}
/* NO ::before/::after on bc-desc — they change text wrapping and break card heights */

.badge-feat{
  position:absolute;top:16px;right:16px;
  font-family:var(--ff-m);font-size:.57rem;letter-spacing:.1em;text-transform:uppercase;
  color:#000;background:linear-gradient(135deg,var(--acc),var(--acc2));
  padding:3px 10px;border-radius:100px;font-weight:700;
}
html[data-mode=pm] .badge-feat{
  font-family:'Kalam',cursive;font-size:.68rem;
  background:var(--acc);border-radius:2px 6px 4px 5px/5px 3px 6px 3px;
  border:1.5px solid rgba(30,40,65,.2);color:#fff;
  box-shadow:2px 2px 0 rgba(30,40,65,.15);
}
html[data-mode=sde] .badge-feat{box-shadow:0 2px 12px var(--acc-glow)}

.metrics{display:flex;gap:8px;flex-wrap:wrap;margin-top:14px}
.met{font-family:var(--ff-m);font-size:.66rem;color:var(--acc);background:var(--acc-dim);padding:4px 10px;border-radius:6px;border:1px solid rgba(var(--acc-rgb),.2)}
html[data-mode=pm] .met{font-family:'Kalam',cursive;font-size:.78rem;border:1.5px solid rgba(192,57,43,.3);background:rgba(192,57,43,.07);border-radius:var(--r-sm);box-shadow:1px 1px 0 rgba(30,40,65,.1)}
html[data-mode=sde] .met{border-radius:3px}
html[data-mode=sde] .met::before{content:'+ ';opacity:.6}

/* ══════════════════════════════════════════
   TABS
══════════════════════════════════════════ */
.tabs{display:flex;gap:3px;background:rgba(255,255,255,.03);border:1px solid var(--border);border-radius:var(--r-sm);padding:4px;margin:18px 0 14px;position:relative}

/* PM TABS: paper folder tabs */
html[data-mode=pm] .tabs{
  background:transparent;border:none;padding:0;gap:6px;
  border-bottom:2px solid rgba(30,40,65,.2);
  border-radius:0;
}
html[data-mode=pm] .tb{
  border:2px solid rgba(30,40,65,.2);border-bottom:none;
  border-radius:4px 8px 0 0 / 5px 6px 0 0;
  background:rgba(250,247,240,.7);color:var(--tx2);
  font-family:'Kalam',cursive;font-size:.85rem;
  padding:7px 16px;flex:none;
  transition:all .25s;
  display:flex;align-items:center;gap:6px;
}
html[data-mode=pm] .tb:hover:not(.on){background:rgba(255,252,244,.9);border-color:rgba(30,40,65,.35)}
html[data-mode=pm] .tb.on{
  background:rgba(255,253,248,1);color:var(--acc);
  font-weight:700;border-color:var(--acc);
  box-shadow:none;
  margin-bottom:-2px;padding-bottom:9px;
}

/* SDE TABS: IDE file tabs */
html[data-mode=sde] .tabs{
  background:#0a0c16;border:none;
  border-bottom:1px solid rgba(0,232,122,.1);
  padding:0;gap:0;border-radius:4px 4px 0 0;
}
html[data-mode=sde] .tb{
  border-radius:0;border:none;
  border-right:1px solid rgba(0,232,122,.08);
  padding:8px 16px;color:var(--tx2);
  font-family:var(--ff-m);font-size:.66rem;
  flex:none;display:flex;align-items:center;gap:6px;
  transition:all .25s;
}
html[data-mode=sde] .tb:hover:not(.on){color:var(--tx);background:rgba(255,255,255,.03)}
html[data-mode=sde] .tb.on{
  background:rgba(0,232,122,.05);color:var(--acc);
  font-weight:600;border-bottom:2px solid var(--acc);
  box-shadow:none;
}
html[data-mode=sde] .tb .ti{font-size:.8rem}

.tc{display:none;animation:fadeIn .25s ease}.tc.on{display:block}
.td-txt{font-size:.77rem;color:var(--tx2);line-height:1.75}
html[data-mode=pm] .td-txt{font-family:'Patrick Hand',cursive;font-size:.88rem;color:var(--tx2)}
html[data-mode=sde] .td-txt{font-family:var(--ff-m);font-size:.73rem}
.td-txt strong{color:var(--acc);font-family:var(--ff-m);font-size:.63rem;text-transform:uppercase;letter-spacing:.1em;display:flex;align-items:center;gap:6px;margin-top:11px;margin-bottom:5px}
html[data-mode=pm] .td-txt strong{font-family:'Patrick Hand',cursive;font-size:.82rem;text-transform:none;letter-spacing:0;color:var(--tx);text-decoration:underline;text-decoration-color:rgba(192,57,43,.4);text-decoration-thickness:2px}
html[data-mode=pm] .td-txt strong::before{display:none}
html[data-mode=sde] .td-txt strong::before{content:'→';display:inline-block;opacity:.5}

.card-lnk{
  display:inline-flex;align-items:center;gap:6px;margin-top:14px;font-size:.73rem;
  font-family:var(--ff-m);color:var(--acc);text-decoration:none;
  padding:6px 14px;border-radius:var(--r-sm);border:1px solid rgba(var(--acc-rgb),.25);
  background:rgba(var(--acc-rgb),.06);transition:all .3s;width:fit-content;
}
html[data-mode=pm] .card-lnk{
  font-family:'Kalam',cursive;font-size:.82rem;
  border:1.5px solid rgba(192,57,43,.3);background:rgba(192,57,43,.05);
  border-radius:var(--r-sm);box-shadow:2px 2px 0 rgba(30,40,65,.08);
}
html[data-mode=pm] .card-lnk:hover{transform:translate(-1px,-1px);box-shadow:3px 3px 0 rgba(192,57,43,.2)}
html[data-mode=sde] .card-lnk:hover{background:rgba(0,232,122,.12);border-color:rgba(0,232,122,.4);transform:translateY(-1px)}
.card-lnk svg{width:12px;height:12px}

/* ══════════════════════════════════════════
   TIMELINE
══════════════════════════════════════════ */
#timeline .roadmap{display:grid;grid-template-columns:repeat(6,1fr);gap:14px;position:relative;margin-top:40px}
#timeline .roadmap::before{content:'';position:absolute;top:30px;left:3%;right:3%;height:1.5px;opacity:.25}
html[data-mode=pm] #timeline .roadmap::before{background:repeating-linear-gradient(90deg,rgba(30,40,65,.3) 0,rgba(30,40,65,.3) 6px,transparent 6px,transparent 12px)}
html[data-mode=sde] #timeline .roadmap::before{background:linear-gradient(90deg,var(--acc),transparent)}

.qc{background:var(--card);border:1px solid var(--border);border-radius:var(--r-sm);padding:18px 15px;cursor:pointer;transition:all .35s;position:relative}
html[data-mode=pm] .qc{background:rgba(255,253,245,.9);border:2px solid rgba(30,40,65,.18);border-radius:var(--r-sm);box-shadow:2px 2px 0 rgba(30,40,65,.08)}
html[data-mode=pm] .qc:nth-child(odd){transform:rotate(-.3deg)}
html[data-mode=pm] .qc:nth-child(even){transform:rotate(.25deg)}
html[data-mode=pm] .qc:hover,.html[data-mode=pm] .qc.on{transform:rotate(0) translateY(-3px);border-color:var(--acc);box-shadow:3px 3px 0 rgba(192,57,43,.2)}
html[data-mode=sde] .qc{background:rgba(0,232,122,.025);border:1px solid rgba(0,232,122,.1);border-radius:4px}
html[data-mode=sde] .qc:hover,html[data-mode=sde] .qc.on{border-color:rgba(0,232,122,.3);background:rgba(0,232,122,.05)}

.q-dot{width:9px;height:9px;border-radius:50%;background:var(--tx3);border:2px solid var(--tx3);margin-bottom:12px;transition:all .35s var(--ease-spring)}
html[data-mode=pm] .q-dot{border-radius:0;transform:rotate(45deg);width:8px;height:8px;background:rgba(30,40,65,.15);border-color:rgba(30,40,65,.3)}
.qc:hover .q-dot,.qc.on .q-dot{background:var(--acc);border-color:var(--acc)}
html[data-mode=pm] .qc:hover .q-dot,html[data-mode=pm] .qc.on .q-dot{transform:rotate(45deg) scale(1.3);background:var(--acc);border-color:var(--acc)}
html[data-mode=sde] .qc:hover .q-dot,html[data-mode=sde] .qc.on .q-dot{box-shadow:0 0 12px var(--acc-glow);border-radius:50%;transform:scale(1.2)}

.q-lbl{font-family:var(--ff-m);font-size:.62rem;color:var(--tx3);letter-spacing:.14em;text-transform:uppercase;margin-bottom:5px}
html[data-mode=pm] .q-lbl{font-family:'Patrick Hand',cursive;font-size:.72rem;letter-spacing:.02em;text-transform:none}
.q-title{font-family:var(--ff-d);font-size:.82rem;font-weight:700;margin-bottom:3px;transition:all .5s}
html[data-mode=pm] .q-title{font-family:'Caveat',cursive;font-size:1rem}
html[data-mode=sde] .q-title{font-family:var(--ff-m);font-size:.76rem;color:var(--acc)}
.q-sub{font-size:.7rem;color:var(--tx2);line-height:1.4}
html[data-mode=pm] .q-sub{font-family:'Patrick Hand',cursive;font-size:.8rem}

.tl-detail{display:none;margin-top:20px;background:var(--card);border:1px solid var(--acc);border-radius:var(--r);padding:32px;animation:sd .4s var(--ease) both;position:relative;overflow:hidden}
html[data-mode=pm] .tl-detail{background:rgba(255,253,245,.95);border:2px solid var(--acc);border-radius:var(--r);box-shadow:5px 5px 0 rgba(192,57,43,.15)}
html[data-mode=pm] .tl-detail::before{content:'';position:absolute;top:0;left:0;right:0;height:3px;background:repeating-linear-gradient(90deg,var(--acc) 0,var(--acc) 8px,transparent 8px,transparent 16px)}
html[data-mode=sde] .tl-detail{background:rgba(0,232,122,.04);border:1px solid rgba(0,232,122,.25)}
html[data-mode=sde] .tl-detail::before{content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(90deg,var(--acc),rgba(0,232,122,.2))}
.tl-detail.on{display:block}
@keyframes sd{from{opacity:0;transform:translateY(-10px)}to{opacity:1;transform:none}}

.td-hd{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:24px;flex-wrap:wrap;gap:12px}
.td-title{font-family:var(--ff-d);font-size:1.5rem;font-weight:800;transition:all .5s}
html[data-mode=pm] .td-title{font-family:'Caveat',cursive;font-size:2rem}
html[data-mode=sde] .td-title{font-family:var(--ff-m);font-size:1.1rem;color:var(--acc)}
.td-period{font-family:var(--ff-m);font-size:.7rem;color:var(--acc);background:var(--acc-dim);padding:5px 14px;border-radius:100px;border:1px solid rgba(var(--acc-rgb),.25)}
html[data-mode=pm] .td-period{font-family:'Kalam',cursive;font-size:.82rem;border-radius:var(--r-sm);border:1.5px solid rgba(192,57,43,.3);background:rgba(192,57,43,.07)}
html[data-mode=sde] .td-period{border-radius:3px}

.td-ach-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin-bottom:22px}
.td-ach{background:var(--surface);border-radius:var(--r-sm);padding:16px;border:1px solid var(--border);text-align:center}
html[data-mode=pm] .td-ach{background:rgba(255,253,245,.9);border:2px solid rgba(30,40,65,.18);border-radius:var(--r-sm);box-shadow:2px 2px 0 rgba(30,40,65,.1)}
html[data-mode=sde] .td-ach{background:rgba(0,232,122,.03);border:1px solid rgba(0,232,122,.1);border-radius:4px}
.td-ach-v{font-family:var(--ff-d);font-size:1.4rem;font-weight:800;color:var(--acc);transition:all .5s}
html[data-mode=pm] .td-ach-v{font-family:'Caveat',cursive;font-size:1.9rem}
html[data-mode=sde] .td-ach-v{font-family:var(--ff-m);font-size:1.2rem}
.td-ach-l{font-size:.66rem;color:var(--tx2);margin-top:4px;font-family:var(--ff-m);text-transform:uppercase;letter-spacing:.07em}
html[data-mode=pm] .td-ach-l{font-family:'Patrick Hand',cursive;font-size:.78rem;text-transform:none;letter-spacing:0}
.td-body-txt{font-size:.83rem;color:var(--tx2);line-height:1.82}
html[data-mode=pm] .td-body-txt{font-family:'Patrick Hand',cursive;font-size:.95rem;color:var(--tx2)}
html[data-mode=sde] .td-body-txt{font-family:var(--ff-m);font-size:.76rem}
html[data-mode=sde] .td-body-txt::before{content:'/* ';color:var(--tx3)}
html[data-mode=sde] .td-body-txt::after{content:' */';color:var(--tx3)}

/* ══════════════════════════════════════════
   CONTACT
══════════════════════════════════════════ */
#contact{border-top:1px solid var(--border);position:relative;overflow:hidden}
html[data-mode=pm] #contact{border-top:2px dashed rgba(30,40,65,.2)}
html[data-mode=sde] #contact::before{content:'';position:absolute;top:-50%;left:50%;transform:translateX(-50%);width:600px;height:600px;background:radial-gradient(circle,rgba(0,232,122,.06),transparent 65%);pointer-events:none}
.contact-inner{display:flex;flex-direction:column;align-items:center;text-align:center;gap:28px;position:relative}
.contact-h{font-family:var(--ff-d);font-size:clamp(2.2rem,4vw,3.8rem);font-weight:800;letter-spacing:-.02em;transition:all .5s;line-height:1.05}
html[data-mode=pm] .contact-h{font-family:'Caveat',cursive;font-size:clamp(2.8rem,5vw,4.5rem);letter-spacing:.01em}
html[data-mode=sde] .contact-h{font-family:var(--ff-m);font-size:clamp(1.5rem,2.5vw,2.5rem)}
html[data-mode=sde] .contact-h::before{content:'> echo "';color:var(--tx2);opacity:.6;font-size:.55em}
html[data-mode=sde] .contact-h::after{content:'"';color:var(--tx2);opacity:.6;font-size:.55em}
.contact-sub{font-size:.95rem;color:var(--tx2);max-width:440px;line-height:1.75}
html[data-mode=pm] .contact-sub{font-family:'Patrick Hand',cursive;font-size:1.05rem}
html[data-mode=sde] .contact-sub{font-family:var(--ff-m);font-size:.78rem}
.contact-links{display:flex;gap:12px;flex-wrap:wrap;justify-content:center}
.cl{font-family:var(--ff-m);font-size:.76rem;color:var(--tx2);text-decoration:none;padding:9px 18px;border:1px solid var(--border);border-radius:var(--r-sm);transition:all .3s;background:var(--card)}
html[data-mode=pm] .cl{font-family:'Kalam',cursive;font-size:.85rem;border:2px solid rgba(30,40,65,.2);border-radius:var(--r-sm);background:rgba(255,252,244,.8);box-shadow:2px 2px 0 rgba(30,40,65,.08)}
html[data-mode=pm] .cl:hover{border-color:var(--acc);color:var(--acc);transform:translate(-1px,-1px);box-shadow:3px 3px 0 rgba(192,57,43,.2)}
html[data-mode=sde] .cl:hover{border-color:rgba(0,232,122,.4);color:var(--acc);background:rgba(0,232,122,.06)}

footer{border-top:1px solid var(--border);padding:30px 52px;max-width:1320px;margin:0 auto;display:flex;justify-content:space-between;align-items:center}
html[data-mode=pm] footer{border-top:2px solid rgba(30,40,65,.15)}
.f-logo{font-family:var(--ff-d);font-weight:800;font-size:1rem;transition:all .5s}
html[data-mode=pm] .f-logo{font-family:'Caveat',cursive;font-size:1.3rem}
html[data-mode=sde] .f-logo{font-family:var(--ff-m);font-size:.88rem}
html[data-mode=sde] .f-logo::before{content:'$ ';color:var(--acc);opacity:.7}
.f-copy{font-family:var(--ff-m);font-size:.66rem;color:var(--tx3)}
html[data-mode=pm] .f-copy{font-family:'Patrick Hand',cursive;font-size:.78rem}
html[data-mode=sde] .f-copy::before{content:'// ';opacity:.5}

/* ══════════════════════════════════════════
   SCROLL REVEAL
══════════════════════════════════════════ */
.fr{opacity:0;transform:translateY(22px);transition:opacity .7s var(--ease),transform .7s var(--ease)}
.fr.vis{opacity:1;transform:none}
.fr:nth-child(1){transition-delay:.0s}.fr:nth-child(2){transition-delay:.07s}
.fr:nth-child(3){transition-delay:.14s}.fr:nth-child(4){transition-delay:.21s}
.fr:nth-child(5){transition-delay:.28s}.fr:nth-child(6){transition-delay:.35s}
.fr:nth-child(7){transition-delay:.42s}.fr:nth-child(8){transition-delay:.49s}

/* ── SMOOTH MODE TRANSITION OVERLAY ── */
#flash{
  position:fixed;inset:0;z-index:999;pointer-events:none;opacity:0;
  transition:none;
}
#flash.go-sde{background:#04040c;animation:fl-in .85s ease forwards}
#flash.go-pm {background:#faf7f0;animation:fl-in .85s ease forwards}
@keyframes fl-in{
  0%  {opacity:0}
  35% {opacity:.72}
  100%{opacity:0}
}

/* Global crossfade for ALL themed elements */
*{transition:
  background-color .55s ease,
  border-color .5s ease,
  color .45s ease,
  box-shadow .5s ease !important;
}
/* Override for things that must NOT transition (layout, position) */
.fr,.cur,.badge-dot,.orb,.ms-thumb{transition:none !important}
.ms-thumb{transition:left .45s cubic-bezier(.34,1.56,.64,1) !important}
.fr{transition:opacity .7s var(--ease),transform .7s var(--ease) !important}
.fr.vis{opacity:1;transform:none}

/* PM: DOODLE DECORATIONS */
.doodle-wrap{position:absolute;pointer-events:none;opacity:.35}
html[data-mode=sde] .doodle-wrap{display:none}

/* SDE: SKILLS section closing brace */
html[data-mode=sde] #skills::after{content:'}';display:block;font-family:var(--ff-m);font-size:1.5rem;color:var(--tx2);opacity:.4;margin-top:20px;padding-left:52px;max-width:1320px;margin:0 auto;padding:0 52px 20px}
html[data-mode=sde] #projects::after{content:'}';display:block;font-family:var(--ff-m);font-size:1.5rem;color:var(--tx2);opacity:.4;padding:0 52px 20px}

@media(max-width:1024px){section{padding:70px 28px}nav{padding:13px 24px}.nav-links{display:none}#skills .inner{grid-template-columns:1fr}#timeline .roadmap{grid-template-columns:repeat(3,1fr)}}
@media(max-width:768px){.kpi-grid{grid-template-columns:repeat(2,1fr)}#projects .bento{grid-template-columns:1fr 1fr}.s7,.s5,.s6,.s4,.s3,.s8{grid-column:span 2}.r2{grid-row:span 1}.td-ach-grid{grid-template-columns:1fr 1fr}footer{flex-direction:column;gap:14px;text-align:center}#timeline .roadmap{grid-template-columns:repeat(2,1fr)}}
@media(max-width:480px){#projects .bento{grid-template-columns:1fr}.s7,.s5,.s6,.s4,.s3,.s8{grid-column:span 1}.kpi-grid{grid-template-columns:repeat(2,1fr)}}
</style>
</head>
<body>

<!-- BACKGROUND LAYERS -->
<div class="bg-canvas" aria-hidden="true">
  <div class="orb orb1"></div>
  <div class="orb orb2"></div>
  <div class="orb orb3"></div>
</div>
<canvas id="matrix-canvas" aria-hidden="true"></canvas>

<!-- SVG DEFS for PM doodle filter -->
<svg style="display:none" aria-hidden="true">
  <defs>
    <filter id="rough-border" x="-2%" y="-2%" width="104%" height="104%">
      <feTurbulence type="fractalNoise" baseFrequency="0.04" numOctaves="4" seed="5" result="noise"/>
      <feDisplacementMap in="SourceGraphic" in2="noise" scale="1.8" xChannelSelector="R" yChannelSelector="G"/>
    </filter>
  </defs>
</svg>

<div id="flash"></div>

<!-- ═══ NAV ═══ -->
<nav>
  <div class="nav-logo display">Parth<span style="color:var(--acc)">.</span></div>
  <ul class="nav-links">
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#timeline">Journey</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-r">
    <button class="ms" id="modeBtn" aria-label="Toggle PM / SDE mode">
      <span class="ms-lbl on" id="lbl-pm">PM</span>
      <div class="ms-track"><div class="ms-thumb"></div></div>
      <span class="ms-lbl" id="lbl-sde">SDE</span>
    </button>
    <a href="mailto:parthprakashmall@gmail.com" class="btn-cta">Hire Me ↗</a>
  </div>
</nav>

<main>

<!-- ═══ HERO ═══ -->
<section id="hero">

  <!-- PM doodles in hero -->
  <div class="pm-only" style="position:relative">
    <!-- Decorative arrow doodle -->
    <svg class="doodle-wrap" style="top:60px;left:820px;width:80px;height:60px" viewBox="0 0 80 60">
      <path d="M5 30 Q30 10 55 28" stroke="#c0392b" stroke-width="2" fill="none" stroke-dasharray="4 3"/>
      <polygon points="55,22 62,30 52,34" fill="#c0392b" opacity=".6"/>
    </svg>
    <!-- Spiral doodle -->
    <svg class="doodle-wrap" style="top:180px;right:120px;width:50px;height:50px;opacity:.2" viewBox="0 0 50 50">
      <path d="M25 25 Q32 18 28 12 Q22 5 14 10 Q6 16 10 26 Q14 38 26 36 Q38 32 35 20 Q31 8 18 8" stroke="#1e2841" stroke-width="1.5" fill="none"/>
    </svg>
  </div>

  <div class="hero-badge fr">
    <span class="badge-dot"></span>
    <span id="badge-txt">Product Manager &amp; Engineer · IIT Kharagpur</span>
  </div>

  <!-- PM MODE -->
  <div class="pm-only">
    <h1 class="hero-h1 fr">
      Thinking like a PM.<br>
      <span class="dim">Building like an</span> <span class="hi">Engineer.</span>
    </h1>
    <p class="hero-sub fr">I design, ship, and measure digital products by bridging user empathy with technical execution — from wireframe to working code, GTM strategy to git commit.</p>
    <div class="hero-acts fr">
      <a href="#projects" class="btn-primary">View Projects ↓</a>
      <a href="https://linkedin.com/in/parth-prakash-mall" class="btn-ghost" target="_blank">LinkedIn ↗</a>
      <a href="https://github.com/PART-H-TRAP" class="btn-ghost" target="_blank">GitHub ↗</a>
    </div>
    <div class="kpi-grid fr" id="kpi-grid">
      <div class="kpi-card"><div class="kpi-val" data-target="40" data-sfx="%">0%</div><div class="kpi-lbl">Effort Reduced</div></div>
      <div class="kpi-card"><div class="kpi-val" data-target="20" data-sfx="%">0%</div><div class="kpi-lbl">Brand Awareness ↑</div></div>
      <div class="kpi-card"><div class="kpi-val" data-target="35" data-sfx="%">0%</div><div class="kpi-lbl">Delivery Time ↓</div></div>
      <div class="kpi-card"><div class="kpi-val" data-target="700" data-sfx="+">0+</div><div class="kpi-lbl">Users Engaged</div></div>
    </div>
  </div>

  <!-- SDE MODE -->
  <div class="sde-only">
    <h1 class="hero-h1 fr" style="font-size:clamp(1.4rem,3vw,2.6rem);font-family:'JetBrains Mono',monospace">
      <span style="color:var(--acc)">parth@iit-kgp</span><span style="color:var(--tx2)">:~$</span> cat profile.json<br>
      <span style="font-size:.7em;color:var(--tx2);display:block;margin-top:8px">
        { "name": "Parth Prakash Mall", "cgpa": 8.74,<br>
        &nbsp;&nbsp;"roles": ["PM", "SDE", "Founder"], "repos": 9 }
      </span>
    </h1>
    <div class="terminal fr" style="margin-bottom:36px">
      <div class="t-head">
        <div class="t-dot t-r"></div><div class="t-dot t-y"></div><div class="t-dot t-g"></div>
        <span class="t-fn">ProductManager.py — ~/parth-mall</span>
      </div>
      <div class="t-body"><pre id="term-code"></pre><span class="cur" id="term-cur"></span></div>
    </div>
    <div class="hero-acts fr">
      <a href="https://github.com/PART-H-TRAP" class="btn-primary" target="_blank">GitHub ↗</a>
      <a href="#projects" class="btn-ghost">View Projects ↓</a>
    </div>
  </div>

</section>

<!-- ═══ SKILLS ═══ -->
<section id="skills" class="fr">
  <div class="sec-label">02 — Core Skills</div>
  <h2 class="sec-title">The Engine Room</h2>
  <p class="sec-sub">Where product intuition meets engineering precision.</p>
  <div id="skills-inner">

    <div class="glass-card pm-only" style="justify-content:space-between">
      <div>
        <div class="gc-title">Feature Prioritization Matrix</div>
        <div class="gc-sub">Click any bubble to reveal the rationale</div>
        <div class="matrix">
          <div class="mx-h"></div><div class="mx-v"></div>
          <div class="mx-q" style="top:0;left:0">Low Impact</div>
          <div class="mx-q" style="top:0;right:0;text-align:right">High Impact</div>
          <div class="mx-q" style="bottom:14px;left:0">Low Effort</div>
          <div class="mx-q" style="bottom:14px;right:0;text-align:right">High Effort</div>
          <div class="mx-ax mx-ax-x">→ Impact</div>
          <div class="mx-ax mx-ax-y">Effort ↑</div>
          <div class="fdot lit" style="left:72%;top:60%" data-n="KrishiRakshak AI Bot" data-d="High impact for 140M+ smallholders, moderate effort. Core differentiator — priority #1.">AI Bot</div>
          <div class="fdot" style="left:80%;top:78%" data-n="WhatsApp Channel" data-d="Near-zero effort (API exists), massive reach. Ship in sprint 1 — quickest win.">WA</div>
          <div class="fdot" style="left:60%;top:38%" data-n="Carbon Credit Platform" data-d="Enormous TAM ($50B+) but complex regulatory. Phase 2 — validate AI bot first.">Carbon</div>
          <div class="fdot" style="left:38%;top:74%" data-n="Farmer Onboarding" data-d="Low effort, medium reach. Quick win — good UX unlocks downstream metrics.">Onboard</div>
          <div class="fdot" style="left:85%;top:46%" data-n="Insurance Aggregator" data-d="High impact per user. 6 services unified via MoSCoW + Impact-Effort analysis.">Ins.Agg</div>
          <div class="fdot" style="left:25%;top:68%" data-n="Admin Dashboard" data-d="Operational necessity, low user-facing impact. Buffer time — never a blocker.">Admin</div>
        </div>
        <div id="mx-tip"></div>
      </div>
      <div class="tag-row" style="margin-top:16px"><div class="tag">MoSCoW</div><div class="tag">RICE</div><div class="tag">OKRs</div><div class="tag">Impact-Effort</div><div class="tag">GTM Strategy</div><div class="tag">User Research</div></div>
    </div>

    <div class="glass-card pm-only" style="justify-content:space-between">
      <div>
        <div class="gc-title">PM Toolkit</div>
        <div class="gc-sub">Frameworks &amp; methodologies I ship with</div>
        <div class="tag-row" style="margin-top:0">
          <div class="tag tag-acc">Product Strategy</div><div class="tag tag-acc">Market Sizing</div>
          <div class="tag tag-acc">Competitor Analysis</div><div class="tag tag-acc">User Personas</div>
          <div class="tag tag-acc">Wireframing</div><div class="tag tag-acc">A/B Testing</div>
          <div class="tag">Corporate Comms</div><div class="tag">Stakeholder Mgmt</div>
          <div class="tag">Revenue Modeling</div><div class="tag">Cross-functional Leadership</div>
          <div class="tag">Sprint Planning</div><div class="tag">North Star Metrics</div>
          <div class="tag">Supply Chain Ops</div><div class="tag">Pricing Strategy</div>
        </div>
      </div>
      <div style="margin-top:20px;padding-top:16px;border-top:1px solid var(--border)">
        <div class="gc-title" style="font-size:.88rem;margin-bottom:10px">Academic Edge</div>
        <div class="tag-row" style="margin-top:0">
          <div class="tag">Entrepreneurship Essentials</div><div class="tag">International Business</div>
          <div class="tag">Probability &amp; Statistics</div><div class="tag">Programming &amp; DSA</div>
        </div>
      </div>
    </div>

    <div class="glass-card sde-only" style="grid-column:1/-1">
      <div class="gc-title">tech_stack.json</div>
      <div class="gc-sub">Hover a skill to see which projects used it</div>
      <div class="tech-grid" id="tech-grid">
        <div class="tp" data-skill="react">React <span class="cnt">2</span></div>
        <div class="tp" data-skill="django">Django</div>
        <div class="tp" data-skill="firebase">Firebase <span class="cnt">2</span></div>
        <div class="tp" data-skill="python">Python <span class="cnt">3</span></div>
        <div class="tp" data-skill="cpp">C++ <span class="cnt">1</span></div>
        <div class="tp" data-skill="c">C <span class="cnt">1</span></div>
        <div class="tp" data-skill="js">JavaScript <span class="cnt">2</span></div>
        <div class="tp" data-skill="auth">Auth APIs</div>
        <div class="tp" data-skill="whatsapp">WhatsApp API</div>
        <div class="tp" data-skill="jenkins">Jenkins / CI-CD</div>
        <div class="tp" data-skill="algorithms">Algorithms <span class="cnt">4</span></div>
        <div class="tp" data-skill="pygame">Pygame <span class="cnt">2</span></div>
        <div class="tp" data-skill="oop">OOP Design</div>
        <div class="tp" data-skill="cmake">CMake</div>
        <div class="tp" data-skill="vite">Vite</div>
      </div>
      <div id="tech-panel"></div>
    </div>
  </div>
</section>

<!-- ═══ PROJECTS ═══ -->
<section id="projects" class="fr">
  <div class="sec-label">03 — Work &amp; Projects</div>
  <h2 class="sec-title">The Product Catalog</h2>
  <p class="sec-sub">Every card ships with a PM Spec and a Tech breakdown. Toggle between them.</p>
  <div class="bento">

    <div class="bc s12 featured" data-file="// KrishiRakshak · co-founder · mar 2025">
      <div class="badge-feat">Co-Founder · Live</div>
      <div class="bc-tag">Startup · AgriTech · Mar 2025</div>
      <div class="bc-title">KrishiRakshak</div>
      <div class="kr-split">
        <!-- LEFT: description + metrics -->
        <div>
          <div class="bc-desc">AI-powered platform empowering Indian farmers with crop disease detection, natural remedy suggestions, and a path to carbon credit monetization — all through WhatsApp, where farmers already live.</div>
          <div class="metrics" style="margin-top:16px">
            <div class="met">35+ farmer interviews</div>
            <div class="met">2 products in roadmap</div>
            <div class="met">AI-first · WhatsApp-native</div>
          </div>
        </div>
        <!-- RIGHT: tabs + content -->
        <div>
          <div class="tabs">
            <button class="tb on" onclick="tab(this,'kr-s')"><span class="ti">📊</span> PM Spec</button>
            <button class="tb" onclick="tab(this,'kr-t')"><span class="ti">💻</span> Tech Stack</button>
          </div>
          <div class="tc on" id="kr-s"><div class="td-txt">
            <strong>User Persona</strong>Smallholder Indian farmers (2–5 acres), WhatsApp-native. Pain: crop disease = ₹500–₹1500 loss/season. No accessible agronomist.
            <strong>Problem Statement</strong>Indian farmers lose ~₹900B/yr to undetected crop disease. Carbon markets inaccessible. No unified, low-bandwidth solution existed.
            <strong>North Star Metric</strong>Farmers monetising ≥1 carbon credit within 6 months of activation.
            <strong>GTM Strategy</strong>FPO partnerships → 2-district pilot → state-wide via agri-NGO tie-ups. 35+ farmer interviews completed.
          </div></div>
          <div class="tc" id="kr-t"><div class="td-txt">
            <strong>Architecture</strong>WhatsApp Business API → Webhook → Python ML pipeline → Firebase Realtime DB → Response formatter.
            <strong>Key Challenges</strong>Low-bandwidth image transmission, multi-language NLP for regional dialects, offline-first data sync.
            <strong>Stack</strong>
            <div class="tag-row" style="margin-top:7px"><div class="tag">WhatsApp Business API</div><div class="tag">Python</div><div class="tag">Firebase</div><div class="tag">ML · Image Classification</div><div class="tag">Webhooks</div></div>
          </div></div>
        </div>
      </div>
    </div>

    <div class="bc s6" data-file="// pwc-prioritization-app · internship · may 2025">
      <div class="bc-tag">SDE Internship · PwC India · May–Jun 2025</div>
      <div class="bc-title">PwC Prioritization App</div>
      <div class="bc-desc">Web-based initiative prioritization platform automating T-Map diagram generation with dependency mapping and cost tables. Deployed internally at PwC Mumbai.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'pwc-s')"><span class="ti">📊</span> PM Spec</button>
        <button class="tb" onclick="tab(this,'pwc-t')"><span class="ti">💻</span> Tech Stack</button>
      </div>
      <div class="tc on" id="pwc-s"><div class="td-txt">
        <strong>Impact</strong>Reduced manual effort 70%, processing time 90%. Initiative dependency accuracy improved 40%.
        <strong>Key Win</strong>Decision-making velocity doubled. Eliminated 90% of spreadsheet-based manual work.
      </div></div>
      <div class="tc" id="pwc-t"><div class="td-txt">
        <strong>Stack</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">Django</div><div class="tag">React</div><div class="tag">Python</div><div class="tag">REST APIs</div><div class="tag">Jenkins CI/CD</div></div>
        <strong>Architecture</strong>React frontend → Django REST API → T-Map engine → PDF/Excel export pipeline.
      </div></div>
      <div class="metrics"><div class="met">70% effort ↓</div><div class="met">90% faster</div><div class="met">40% accuracy ↑</div></div>
    </div>

    <div class="bc s6" data-file="// ChatRoom.jsx · react + firebase · may 2025">
      <div class="bc-tag">Full-Stack · JavaScript · May–Jun 2025</div>
      <div class="bc-title">ChatRoom</div>
      <div class="bc-desc">Real-time chat app built with React + Vite + Firebase. Room management, admin moderation, image sharing, and persistent login — 500+ concurrent users across 25k+ chat records.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'cr-s')"><span class="ti">📊</span> PM Spec</button>
        <button class="tb" onclick="tab(this,'cr-t')"><span class="ti">💻</span> Tech Stack</button>
      </div>
      <div class="tc on" id="cr-s"><div class="td-txt">
        <strong>Scale</strong>5k profiles · 10k catalogs · 25k chat records in Firebase Realtime DB.
        <strong>Retention Win</strong>Admin moderation + persistent login → +20% retention. Unauthorized login reduced 95%.
      </div></div>
      <div class="tc" id="cr-t"><div class="td-txt">
        <strong>Stack · JS 67.7% · CSS 31.3%</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">React</div><div class="tag">Vite</div><div class="tag">Firebase Realtime DB</div><div class="tag">Auth APIs</div><div class="tag">JavaScript</div></div>
      </div></div>
      <div class="metrics"><div class="met">500+ concurrent</div><div class="met">95% auth ↑</div><div class="met">+20% retention</div></div>
      <a class="card-lnk" href="https://github.com/PART-H-TRAP/ChatRoom" target="_blank">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        PART-H-TRAP/ChatRoom
      </a>
    </div>

    <div class="bc s4" data-file="// insurance-aggregator · pm project · mar 2025">
      <div class="bc-tag">PM · GC Championship · Mar–Apr 2025</div>
      <div class="bc-title">Unified Insurance Platform</div>
      <div class="bc-desc">Redesigned India's fragmented digital insurance into a single AI-powered mobile aggregator. 12 user interviews, market sizing, 8 competitor analysis.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'gc-s')"><span class="ti">📊</span> PM Spec</button>
        <button class="tb" onclick="tab(this,'gc-t')"><span class="ti">🔍</span> Research</button>
      </div>
      <div class="tc on" id="gc-s"><div class="td-txt">
        <strong>Problem</strong>India's 6+ insurance verticals all require separate apps — fragmentation drives abandonment.
        <strong>Solution</strong>Unified aggregator with AI-recommendations, document locker, claim tracker — 11 features across 5 journey stages.
      </div></div>
      <div class="tc" id="gc-t"><div class="td-txt">
        <strong>Research</strong>12 structured user interviews + benchmarking 8 platforms (PolicyBazaar, Acko, IRDAI).
        <strong>Deliverables</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">Wireframes</div><div class="tag">User Personas</div><div class="tag">Market Sizing</div><div class="tag">Aggregator Model</div></div>
      </div></div>
      <div class="metrics" style="margin-top:auto"><div class="met">6 services unified</div><div class="met">11 features</div></div>
    </div>

    <div class="bc s4" data-file="// chess.py · python + pygame · dec 2023">
      <div class="bc-tag">Python · Pygame · Dec 2023–Jan 2024</div>
      <div class="bc-title">Chess Game</div>
      <div class="bc-desc">Full-featured 2-player chess engine. Castling, en passant, pawn promotion. Modular OOP with checkmate detection, keyboard shortcuts, and 4 board themes.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'ch-s')"><span class="ti">📊</span> Approach</button>
        <button class="tb" onclick="tab(this,'ch-t')"><span class="ti">💻</span> Code</button>
      </div>
      <div class="tc on" id="ch-s"><div class="td-txt">
        <strong>Design</strong>Modular OOP — each piece a class, each rule a method. Simplified maintenance 30%.
        <strong>Coverage</strong>100% standard rules across 50+ scenarios. 4 themes, keyboard shortcuts for 20% faster input.
      </div></div>
      <div class="tc" id="ch-t"><div class="td-txt">
        <strong>Stack · Python 100%</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">Python</div><div class="tag">Pygame</div><div class="tag">OOP</div><div class="tag">CI/CD Workflows</div></div>
        <strong>Files</strong><code style="font-size:.72rem;color:var(--acc);font-family:'JetBrains Mono',monospace">main.py · chess_pieces/</code>
      </div></div>
      <div class="metrics" style="margin-top:auto"><div class="met">100% rules</div><div class="met">50+ scenarios</div></div>
      <a class="card-lnk" href="https://github.com/PART-H-TRAP/CHESS" target="_blank">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        PART-H-TRAP/CHESS
      </a>
    </div>

    <div class="bc s4" data-file="// pathfinder.py · bfs/dfs/a* · may 2024">
      <div class="bc-tag">Python · Pygame · May–Jun 2024</div>
      <div class="bc-title">Pathfinding Visualizer</div>
      <div class="bc-desc">Real-time maze generation and pathfinding. BFS, DFS, Greedy, and A* with drag-and-drop obstacles and multi-stop routing — live graphical rendering of all 4 algorithms.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'pf-s')"><span class="ti">📊</span> Approach</button>
        <button class="tb" onclick="tab(this,'pf-t')"><span class="ti">💻</span> Code</button>
      </div>
      <div class="tc on" id="pf-s"><div class="td-txt">
        <strong>Algo Comparison</strong>BFS (shortest), DFS (fast, non-optimal), Greedy (heuristic), A* (optimal+efficient). Live side-by-side.
        <strong>UX</strong>Drag-and-drop + real-time visual progress improved algo understanding 30%.
      </div></div>
      <div class="tc" id="pf-t"><div class="td-txt">
        <strong>Stack · Python 100%</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">Python</div><div class="tag">Pygame</div><div class="tag">BFS</div><div class="tag">DFS</div><div class="tag">A*</div><div class="tag">Greedy</div></div>
        <strong>File</strong><code style="font-size:.72rem;color:var(--acc);font-family:'JetBrains Mono',monospace">pathfinder.py</code>
      </div></div>
      <div class="metrics" style="margin-top:auto"><div class="met">4 algorithms</div><div class="met">40% faster demos</div></div>
      <a class="card-lnk" href="https://github.com/PART-H-TRAP/pathfinder" target="_blank">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        PART-H-TRAP/pathfinder
      </a>
    </div>

    <div class="bc s6" data-file="// rubiksSolver_V1.c · heuristic bfs · nov 2024">
      <div class="bc-tag">C · Heuristic BFS · Nov 2024 — V1</div>
      <div class="bc-title">Rubik's Cube Solver V1</div>
      <div class="bc-desc">First iteration in pure C — under 800 lines. Heuristic BFS with open/close table. Full console display for all 6 faces. Solves any scramble in ~10s. The lean foundation that revealed what V2 needed.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'rv1-s')"><span class="ti">📊</span> Approach</button>
        <button class="tb" onclick="tab(this,'rv1-t')"><span class="ti">💻</span> Code</button>
      </div>
      <div class="tc on" id="rv1-s"><div class="td-txt">
        <strong>Algorithm</strong>Heuristic BFS with open table (queue) + close table. Evaluation function scores cube proximity to solved state; pruning discards low-promise branches.
        <strong>Commands</strong><code style="font-size:.7rem;color:var(--acc);font-family:'JetBrains Mono',monospace">rand N · input · solve · init · help · exit</code>
        <strong>V1 → V2 Gap</strong>~10s solve time exposed the need for Korf's IDA* + pattern databases.
      </div></div>
      <div class="tc" id="rv1-t"><div class="td-txt">
        <strong>Stack · C 100% · LGPL-3.0</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">C</div><div class="tag">Heuristic BFS</div><div class="tag">2D Array Model</div><div class="tag">Console UI</div><div class="tag">&lt;800 lines</div></div>
        <strong>Files</strong><code style="font-size:.7rem;color:var(--acc);font-family:'JetBrains Mono',monospace">cube.c · cube.exe · readme.txt</code>
      </div></div>
      <div class="metrics"><div class="met">~10s solve</div><div class="met">&lt;800 lines</div></div>
      <a class="card-lnk" href="https://github.com/PART-H-TRAP/rubiksSolver_V1" target="_blank">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        PART-H-TRAP/rubiksSolver_V1
      </a>
    </div>

    <div class="bc s6" data-file="// rubiksSolver_V2.cpp · korf's IDA* · dec 2024">
      <div class="bc-tag">C++ · Korf's IDA* · Nov–Dec 2024 — V2</div>
      <div class="bc-title">Rubik's Cube Solver V2</div>
      <div class="bc-desc">Production-grade upgrade. Korf's IDA* with precomputed pattern databases solves any scramble in under 4 seconds. 50% memory reduction via nibble arrays. Modular 3-directory architecture with CMake.</div>
      <div class="tabs">
        <button class="tb on" onclick="tab(this,'rv2-s')"><span class="ti">📊</span> Approach</button>
        <button class="tb" onclick="tab(this,'rv2-t')"><span class="ti">💻</span> Code</button>
      </div>
      <div class="tc on" id="rv2-s"><div class="td-txt">
        <strong>Algorithm</strong>Korf's IDA* — iterative deepening A* with admissible heuristic from precomputed corner+edge pattern databases. Optimal solutions guaranteed.
        <strong>V1 → V2</strong>10s → &lt;4s · 50% memory via nibble arrays · modular codebase · CMake build.
      </div></div>
      <div class="tc" id="rv2-t"><div class="td-txt">
        <strong>Stack · C++ 98.8% · CMake 1.2%</strong>
        <div class="tag-row" style="margin-top:7px"><div class="tag">C++</div><div class="tag">Korf's IDA*</div><div class="tag">Pattern Databases</div><div class="tag">Nibble Arrays</div><div class="tag">CMake</div></div>
        <strong>Structure</strong><code style="font-size:.7rem;color:var(--acc);font-family:'JetBrains Mono',monospace">Model/ · PatternDatabases/ · Solver/ · main.cpp</code>
      </div></div>
      <div class="metrics"><div class="met">&lt;4 sec solve</div><div class="met">50% memory ↓</div><div class="met">30% speed ↑</div></div>
      <a class="card-lnk" href="https://github.com/PART-H-TRAP/rubiksSolver_V2" target="_blank">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 00-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0020 4.77 5.07 5.07 0 0019.91 1S18.73.65 16 2.48a13.38 13.38 0 00-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 005 4.77a5.44 5.44 0 00-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 009 18.13V22"/></svg>
        PART-H-TRAP/rubiksSolver_V2
      </a>
    </div>

  </div>
</section>

<!-- ═══ TIMELINE ═══ -->
<section id="timeline" class="fr">
  <div class="sec-label">04 — Journey</div>
  <h2 class="sec-title">Product Roadmap: My Career</h2>
  <p class="sec-sub">Click any quarter to expand shipped work and impact metrics.</p>
  <div class="roadmap" id="roadmap">
    <div class="qc" data-q="q2-24"><div class="q-dot"></div><div class="q-lbl">Q2–Q3 2024</div><div class="q-title">Dual PM Internships</div><div class="q-sub">Crazy Snacks · Trumio.ai</div></div>
    <div class="qc" data-q="q4-24"><div class="q-dot"></div><div class="q-lbl">Q4 2024</div><div class="q-title">Algorithms Dive</div><div class="q-sub">Rubik's Solver · Chess</div></div>
    <div class="qc" data-q="q1-25"><div class="q-dot"></div><div class="q-lbl">Q1 2025</div><div class="q-title">PM + Startup</div><div class="q-sub">GC Tech · KrishiRakshak</div></div>
    <div class="qc" data-q="q2-25"><div class="q-dot"></div><div class="q-lbl">Q2–Q3 2025</div><div class="q-title">Industry Internships</div><div class="q-sub">PwC India · Stone World</div></div>
    <div class="qc" data-q="now"><div class="q-dot"></div><div class="q-lbl">2026 — Now</div><div class="q-title">Building in Public</div><div class="q-sub">KrishiRakshak · CGPA 8.74</div></div>
    <div class="qc" style="border-style:dashed;opacity:.65" data-q="next"><div class="q-dot"></div><div class="q-lbl">Next Chapter</div><div class="q-title">Open to Roles</div><div class="q-sub">PM · SDE · Hybrid</div></div>
  </div>
  <div class="tl-detail" id="tl-detail">
    <div class="td-hd"><div class="td-title" id="td-title">—</div><div class="td-period" id="td-period">—</div></div>
    <div class="td-ach-grid" id="td-achs"></div>
    <p class="td-body-txt" id="td-body"></p>
  </div>
</section>

<!-- ═══ CONTACT ═══ -->
<section id="contact" class="fr">
  <div class="contact-inner">
    <div class="sec-label" style="margin-bottom:0">05 — Contact</div>
    <h2 class="contact-h">Let's build something<br><span style="color:var(--acc)">worth shipping.</span></h2>
    <p class="contact-sub">Open to PM, SDE, and hybrid roles where thinking like a product manager and building like an engineer creates maximum leverage.</p>
    <a href="mailto:parthprakashmall@gmail.com" class="btn-primary" style="padding:16px 36px;font-size:1rem">Say Hello ↗</a>
    <div class="contact-links">
      <a href="https://linkedin.com/in/parth-prakash-mall" class="cl" target="_blank">LinkedIn ↗</a>
      <a href="https://github.com/PART-H-TRAP" class="cl" target="_blank">GitHub ↗</a>
      <a href="tel:+918306582027" class="cl">+91 83065 82027</a>
      <a href="mailto:parthprakashmall@gmail.com" class="cl">Email</a>
    </div>
    <div style="font-family:var(--ff-m);font-size:.68rem;color:var(--tx3)">IIT Kharagpur · Dual Degree · Metallurgical &amp; Materials Engineering · 2022–2027</div>
  </div>
</section>
</main>

<footer>
  <div class="f-logo">Parth Prakash Mall<span style="color:var(--acc)">.</span></div>
  <div class="f-copy">© 2026 · PM thinking × SDE hands</div>
</footer>

<script>
/* ─── TIMELINE DATA ─── */
const tlData={
  'q2-24':{title:'Dual PM Internships',period:'Jun–Aug 2024',
    achs:[{v:'+12%',l:'Revenue · Crazy Snacks'},{v:'35%',l:'Delivery Time Cut'},{v:'700+',l:'Students Engaged · Trumio'}],
    body:'At Crazy Snacks Limited, reverse-engineered two competitors\' pricing models and reduced farm-to-factory delivery time by 35% through logistics optimization. Implemented 3 quality benchmarks. At Trumio.ai, mapped 20+ IIT KGP societies, drove 700+ student engagement, led 4 client projects worth ₹4L, and formulated GTM plans with 2 institutional tie-ups.'},
  'q4-24':{title:'Algorithms & Game Dev',period:'Nov 2024 – Jan 2025',
    achs:[{v:'<4s',l:'Rubik\'s V2 Solve'},{v:'50%',l:'Memory Optimized'},{v:'100%',l:'Chess Rules Coverage'}],
    body:'Built Rubik\'s Cube Solver V1 in C (heuristic BFS, ~10s) then redesigned as V2 in C++ with Korf\'s IDA* and pattern databases — solving any configuration in under 4 seconds with 50% memory reduction via nibble arrays. Concurrently built a full Python Chess engine with 100% standard rules, 50+ scenarios, checkmate detection, and 4 board themes.'},
  'q1-25':{title:'PM Championship + KrishiRakshak',period:'Jan–Apr 2025',
    achs:[{v:'11',l:'Features Designed'},{v:'35+',l:'Farmers Interviewed'},{v:'6',l:'Insurance Services Unified'}],
    body:'Won IIT KGP General Championship Technology track by redesigning India\'s digital insurance UX — 12 user interviews, MoSCoW + Impact-Effort analysis, 11 features across 5 journey stages. Simultaneously co-founded KrishiRakshak, interviewed 35+ farmers, and built the initial WhatsApp AI chatbot prototype for crop disease detection.'},
  'q2-25':{title:'Industry: PwC + Stone World',period:'May–Jul 2025',
    achs:[{v:'90%',l:'Processing Time Cut'},{v:'6.5%',l:'Revenue Up (Stone World)'},{v:'30%',l:'Waste Reduced'}],
    body:'At PwC India, engineered a Django + React prioritization app reducing manual effort by 70% and processing time by 90%. At Stone World Limited, developed 3 new products from industrial byproducts, co-led cross-functional teams achieving 20% brand awareness growth, and implemented 5 cost-cutting measures.'},
  'now':{title:'Building in Public · IIT KGP',period:'2026 – Present',
    achs:[{v:'8.74',l:'CGPA (Dual Degree)'},{v:'2027',l:'Graduation Year'},{v:'∞',l:'Problems to Solve'}],
    body:'Actively developing KrishiRakshak — formulating GTM strategy for carbon credit platform, iterating on WhatsApp AI chatbot, expanding farmer validation. Continuing dual degree in Metallurgical & Materials Engineering at IIT Kharagpur. Open to PM, SDE, and hybrid roles.'},
  'next':{title:'Open to Opportunities',period:'2026 Onwards',
    achs:[{v:'PM',l:'Product Management'},{v:'SDE',l:'Engineering'},{v:'Both',l:'Hybrid / Founding'}],
    body:'Looking for roles where thinking like a PM and building like an engineer creates maximum leverage. Passionate about early-stage startups, impact-driven tech, agritech, and products that solve real human problems at scale.'}
};

const techData={
  react:{p:['ChatRoom','PwC Prioritization App'],d:'React state management for ChatRoom\'s real-time room UI and PwC\'s T-Map dashboard. Built with component-first architecture.'},
  django:{p:['PwC App'],d:'Backend REST API, data processing pipeline, T-Map generation engine for the PwC consulting tool.'},
  firebase:{p:['ChatRoom','KrishiRakshak'],d:'Realtime DB powers ChatRoom (25k chats, 5k profiles) and KrishiRakshak\'s prototype farmer backend.'},
  python:{p:['Pathfinding Visualizer','Chess Game','KrishiRakshak ML'],d:'Core language for algorithm work (BFS, A*, DFS), Pygame game builds, and ML pipeline for crop disease detection.'},
  cpp:{p:["Rubik's Cube V2"],d:"Korf's IDA* in C++. Nibble array optimization → 50% memory reduction, <4s solve time."},
  c:{p:["Rubik's Cube V1"],d:"Pure C heuristic BFS solver in <800 lines. Console-based. Foundation for V2 redesign."},
  js:{p:['ChatRoom','PwC App'],d:'React + Vanilla JS for frontend logic, real-time event handling, and UI state management.'},
  auth:{p:['ChatRoom'],d:'Token-based session management. Reduced unauthorized login by 95%, persistent sessions.'},
  whatsapp:{p:['KrishiRakshak'],d:'WhatsApp Business API — primary distribution channel meeting farmers where they already are.'},
  jenkins:{p:['PwC Internship'],d:'CI/CD pipeline for automated deployment and test runs of the PwC platform.'},
  algorithms:{p:["Rubik's V1","Rubik's V2","Pathfinding","Chess"],d:'BFS, DFS, Heuristic BFS, IDDFS, Korf\'s IDA*, A*, Greedy — implemented across 4 projects.'},
  pygame:{p:['Chess Game','Pathfinding Visualizer'],d:'Python Pygame for real-time graphical UIs — drag-and-drop pathfinder and full chess engine.'},
  oop:{p:['All Major Projects'],d:'Object-oriented architecture as backbone of every project.'},
  cmake:{p:["Rubik's V2"],d:'CMake build system for cross-platform C++ compilation of the IDA* solver.'},
  vite:{p:['ChatRoom'],d:'Vite bundler for fast HMR dev server and optimized production builds in ChatRoom.'}
};

const termLines=[
  '<span class="t-c"># Parth Prakash Mall · IIT Kharagpur · 2022–2027</span>',
  '',
  '<span class="t-k">class</span> <span class="t-cl">ProductManager</span>:',
  '    <span class="t-k">def</span> <span class="t-cl">__init__</span>(self):',
  '        self.name     = <span class="t-s">"Parth Prakash Mall"</span>',
  '        self.cgpa     = <span class="t-n">8.74</span>',
  '        self.skills   = [<span class="t-s">"PM"</span>, <span class="t-s">"SDE"</span>, <span class="t-s">"Founder"</span>]',
  '        self.repos    = <span class="t-n">9</span>  <span class="t-c"># github.com/PART-H-TRAP</span>',
  '',
  '    <span class="t-k">def</span> <span class="t-cl">ship</span>(self, idea):',
  '        spec = self.think_like_pm(idea)   <span class="t-c"># user empathy first</span>',
  '        code = self.build_like_sde(spec)  <span class="t-c"># technical execution</span>',
  '        <span class="t-k">return</span> code.deploy()              <span class="t-c"># 🚀</span>',
];

/* ─── MATRIX RAIN ─── */
let matrixRain=null;
function initMatrix(){
  const canvas=document.getElementById('matrix-canvas');
  const ctx=canvas.getContext('2d');
  function resize(){canvas.width=window.innerWidth;canvas.height=window.innerHeight}
  resize();window.addEventListener('resize',resize);
  const chars='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789@#$%^&*<>{}[]|;:,./?⊕∑∫∂';
  const fs=13;let cols=Math.floor(canvas.width/fs);let drops=new Array(cols).fill(1);
  let interval=null;
  return {
    start(){
      if(interval)return;
      drops=new Array(Math.floor(canvas.width/fs)).fill(1);
      interval=setInterval(()=>{
        ctx.fillStyle='rgba(6,8,16,.06)';ctx.fillRect(0,0,canvas.width,canvas.height);
        for(let i=0;i<drops.length;i++){
          const ch=chars[Math.floor(Math.random()*chars.length)];
          const x=i*fs,y=drops[i]*fs;
          const isHead=Math.random()>.88;
          const isBright=Math.random()>.7;
          if(isHead){
            ctx.fillStyle='rgba(220,255,235,1)';  /* bright white-green lead char */
          } else if(isBright){
            ctx.fillStyle='rgba(0,232,122,.95)';  /* vivid green */
          } else {
            ctx.fillStyle='rgba(0,200,100,.55)';  /* dimmer trail */
          }
          ctx.font=`${fs}px 'JetBrains Mono',monospace`;
          ctx.fillText(ch,x,y);
          if(y>canvas.height&&Math.random()>.975)drops[i]=0;
          drops[i]++;
        }
      },55);
    },
    stop(){clearInterval(interval);interval=null;ctx.clearRect(0,0,canvas.width,canvas.height)}
  };
}

/* ─── MODE SWITCHER ─── */
const html=document.documentElement;
let mode='pm',termDone=false;
matrixRain=initMatrix();

document.getElementById('modeBtn').addEventListener('click',()=>{
  mode=mode==='pm'?'sde':'pm';

  /* Step 1: flash overlay fades in, covering the switch */
  const fl=document.getElementById('flash');
  fl.className='';void fl.offsetWidth;
  fl.classList.add(mode==='sde'?'go-sde':'go-pm');

  /* Step 2: apply new mode at peak opacity (~300ms in) */
  setTimeout(()=>{
    html.setAttribute('data-mode',mode);
    const pm=document.getElementById('lbl-pm'),sde=document.getElementById('lbl-sde');
    if(mode==='sde'){
      pm.classList.remove('on');sde.classList.add('on');
      document.getElementById('badge-txt').textContent='Full-Stack Engineer · IIT Kharagpur · CGPA 8.74';
      matrixRain.start();
      if(!termDone){termDone=true;setTimeout(typeTerminal,500)}
    } else {
      sde.classList.remove('on');pm.classList.add('on');
      document.getElementById('badge-txt').textContent='Product Manager & Engineer · IIT Kharagpur';
      matrixRain.stop();
      setTimeout(animateKPIs,550);
    }
  },280);
});

/* ─── KPI COUNTERS ─── */
function animateKPIs(){
  document.querySelectorAll('.kpi-val[data-target]').forEach(el=>{
    const tgt=+el.dataset.target,sfx=el.dataset.sfx||'';
    let cur=0;const dur=1400,step=tgt/(dur/16);
    el.textContent='0'+sfx;
    const t=setInterval(()=>{cur=Math.min(cur+step,tgt);el.textContent=Math.round(cur)+sfx;if(cur>=tgt)clearInterval(t)},16);
  });
}

/* ─── TERMINAL TYPING ─── */
function typeTerminal(){
  const el=document.getElementById('term-code');
  let li=0,ci=0,lines=[];
  function tick(){
    if(li>=termLines.length)return;
    const line=termLines[li];
    if(ci===0)lines.push('');
    const rem=line.slice(ci);
    if(rem.startsWith('<span')){const end=line.indexOf('</span>',ci)+7;lines[li]=line.slice(0,end);ci=end;}
    else if(ci<line.length){lines[li]=line.slice(0,ci+1);ci++;}
    else{li++;ci=0;el.innerHTML=lines.join('\n');setTimeout(tick,55);return;}
    el.innerHTML=lines.join('\n');setTimeout(tick,ci%4===0?20:11);
  }
  setTimeout(tick,250);
}

/* ─── MATRIX WIDGET ─── */
document.querySelectorAll('.fdot').forEach(d=>{
  d.addEventListener('click',()=>{
    document.querySelectorAll('.fdot').forEach(x=>x.classList.remove('lit'));
    d.classList.add('lit');
    const tip=document.getElementById('mx-tip');
    tip.style.display='block';
    tip.innerHTML=`<span style="color:var(--acc);display:block;margin-bottom:5px;font-weight:700">${d.dataset.n}</span>${d.dataset.d}`;
  });
});

/* ─── TECH PILLS ─── */
document.querySelectorAll('.tp').forEach(p=>{
  p.addEventListener('mouseenter',()=>{
    const k=p.dataset.skill,info=techData[k];
    document.querySelectorAll('.tp').forEach(x=>x.classList.remove('on'));
    p.classList.add('on');
    const panel=document.getElementById('tech-panel');
    if(info){panel.style.display='block';panel.innerHTML=`<span style="color:var(--acc);display:block;margin-bottom:7px;font-weight:600">Used in: ${info.p.join(' · ')}</span>${info.d}`;}
  });
});

/* ─── CARD TABS ─── */
function tab(btn,id){
  const card=btn.closest('.bc,.glass-card');
  card.querySelectorAll('.tb').forEach(b=>b.classList.remove('on'));
  card.querySelectorAll('.tc').forEach(c=>c.classList.remove('on'));
  btn.classList.add('on');
  document.getElementById(id).classList.add('on');
}

/* ─── TIMELINE ─── */
document.querySelectorAll('.qc').forEach(c=>{
  c.addEventListener('click',()=>{
    const q=c.dataset.q,d=tlData[q];if(!d)return;
    const wasOn=c.classList.contains('on');
    document.querySelectorAll('.qc').forEach(x=>x.classList.remove('on'));
    const det=document.getElementById('tl-detail');
    if(wasOn){det.classList.remove('on');return;}
    c.classList.add('on');
    document.getElementById('td-title').textContent=d.title;
    document.getElementById('td-period').textContent=d.period;
    document.getElementById('td-achs').innerHTML=d.achs.map(a=>`<div class="td-ach"><div class="td-ach-v">${a.v}</div><div class="td-ach-l">${a.l}</div></div>`).join('');
    document.getElementById('td-body').textContent=d.body;
    det.classList.add('on');
    setTimeout(()=>det.scrollIntoView({behavior:'smooth',block:'nearest'}),90);
  });
});

/* ─── SCROLL REVEAL ─── */
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){e.target.classList.add('vis');if(e.target.id==='kpi-grid')animateKPIs();}
  });
},{threshold:.1});
document.querySelectorAll('.fr').forEach(el=>obs.observe(el));

/* ─── INIT ─── */
window.addEventListener('load',()=>{
  document.querySelectorAll('#hero .fr').forEach((el,i)=>setTimeout(()=>el.classList.add('vis'),180+i*140));
  setTimeout(animateKPIs,600);
});
</script>
</body>
</html>
