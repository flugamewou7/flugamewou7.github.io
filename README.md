<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>FlugameMMA | Football Legacy</title>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#07070a;--s1:#0d0d14;--s2:#13131e;--s3:#1a1a28;
  --border:#1f1f32;--border2:#2a2a42;
  --gold:#e8b84b;--gold2:#c49a2a;--gold3:rgba(232,184,75,.08);
  --green:#00c853;--red:#f44336;--blue:#2979ff;--cyan:#00b4d8;
  --text:#f0f0f8;--muted:#8888aa;--faint:#222238;
  --radius:10px;
}
*{box-sizing:border-box;margin:0;padding:0;}
html,body{font-family:'Inter',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;overflow-x:hidden;}
::-webkit-scrollbar{width:4px;}::-webkit-scrollbar-track{background:var(--bg);}::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px;}

/* NAV */
nav{display:flex;align-items:center;justify-content:space-between;padding:0 28px;height:52px;background:rgba(7,7,10,.97);border-bottom:1px solid var(--border);position:sticky;top:0;z-index:300;}
.nav-logo{font-family:'Oswald',sans-serif;font-size:1.3rem;letter-spacing:2px;color:var(--text);text-decoration:none;font-weight:600;}
.nav-logo span{color:var(--gold);}
.nav-links{display:flex;gap:4px;}
.nav-links a{font-family:'DM Mono',monospace;font-size:.68rem;letter-spacing:1px;text-transform:uppercase;color:var(--muted);text-decoration:none;padding:5px 12px;border-radius:4px;border:1px solid transparent;transition:all .2s;}
.nav-links a:hover{color:var(--text);border-color:var(--border);}
.nav-links a.active{color:var(--gold);border-color:var(--gold2);}

/* SCREENS */
.screen{display:none;min-height:calc(100vh - 52px);}
.screen.active{display:block;}
#screen-menu{display:none;align-items:center;justify-content:center;flex-direction:column;}
#screen-menu.active{display:flex;}

/* MENU */
.menu-wrap{position:relative;width:100%;min-height:calc(100vh - 52px);display:flex;flex-direction:column;align-items:center;justify-content:center;overflow:hidden;padding:40px 20px;text-align:center;}
.menu-pitch{position:absolute;inset:0;background:radial-gradient(ellipse at 50% 60%,rgba(0,200,83,.07) 0%,transparent 60%),repeating-linear-gradient(90deg,transparent,transparent 79px,rgba(0,200,83,.03) 79px,rgba(0,200,83,.03) 80px),repeating-linear-gradient(0deg,transparent,transparent 79px,rgba(0,200,83,.03) 79px,rgba(0,200,83,.03) 80px);pointer-events:none;}
.menu-ring{position:absolute;border-radius:50%;border:1px solid rgba(232,184,75,.06);animation:rp 5s ease-in-out infinite;}
@keyframes rp{0%,100%{transform:scale(1);opacity:.5;}50%{transform:scale(1.04);opacity:1;}}
.menu-eyebrow{font-family:'DM Mono',monospace;font-size:.7rem;letter-spacing:3px;text-transform:uppercase;color:var(--gold2);margin-bottom:12px;position:relative;z-index:1;}
.menu-title{font-family:'Oswald',sans-serif;font-size:clamp(3.5rem,10vw,7.5rem);font-weight:700;letter-spacing:3px;line-height:.95;position:relative;z-index:1;}
.menu-title .t1{display:block;color:var(--text);}
.menu-title .t2{display:block;color:var(--gold);}
.menu-subtitle{font-family:'DM Mono',monospace;font-size:.72rem;letter-spacing:2px;color:var(--muted);margin:18px 0 48px;position:relative;z-index:1;}
.menu-btns{display:flex;flex-direction:column;gap:12px;width:100%;max-width:300px;position:relative;z-index:1;}
.mbtn{font-family:'Oswald',sans-serif;font-size:1.2rem;letter-spacing:2px;padding:15px 24px;border-radius:6px;border:2px solid;cursor:pointer;transition:all .2s;font-weight:500;}
.mbtn.gold{background:var(--gold);border-color:var(--gold);color:#000;}
.mbtn.gold:hover{background:#f5c85a;}
.mbtn.outline{background:transparent;border-color:var(--border2);color:var(--text);}
.mbtn.outline:hover{border-color:var(--muted);}

/* WIZARD */
#screen-create{padding:0;}
.wizard-wrap{max-width:820px;margin:0 auto;padding:36px 20px;}
.wiz-step{display:none;animation:fadeUp .3s ease;}
.wiz-step.active{display:block;}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}}
.wiz-title{font-family:'Oswald',sans-serif;font-size:2.2rem;letter-spacing:2px;color:var(--gold);font-weight:600;}
.wiz-sub{font-family:'DM Mono',monospace;font-size:.68rem;letter-spacing:2px;color:var(--muted);text-transform:uppercase;margin-top:4px;margin-bottom:28px;}
.wiz-progress{display:flex;gap:5px;margin-bottom:32px;}
.wdot{height:3px;flex:1;background:var(--border2);border-radius:2px;transition:background .3s;}
.wdot.done{background:var(--gold);}
.wdot.act{background:var(--gold2);}

/* Forms */
.fg{margin-bottom:20px;}
.fl{font-family:'DM Mono',monospace;font-size:.65rem;letter-spacing:2px;text-transform:uppercase;color:var(--muted);display:block;margin-bottom:7px;}
.fi{width:100%;background:var(--s2);border:1px solid var(--border2);border-radius:6px;padding:11px 14px;font-family:'Inter',sans-serif;font-size:.95rem;color:var(--text);outline:none;transition:border-color .2s;}
.fi:focus{border-color:var(--gold);}
.fi::placeholder{color:var(--faint);}
select.fi{cursor:pointer;}select.fi option{background:var(--s2);}
.two-col{display:grid;grid-template-columns:1fr 1fr;gap:16px;}
.three-col{display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;}
@media(max-width:580px){.two-col,.three-col{grid-template-columns:1fr;}}

/* Card pickers */
.card-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px;}
.cp{background:var(--s2);border:2px solid var(--border);border-radius:var(--radius);padding:14px 10px;cursor:pointer;transition:all .2s;text-align:center;}
.cp:hover{border-color:var(--border2);}
.cp.sel{border-color:var(--gold);background:var(--gold3);}
.cp .cpi{font-size:1.8rem;margin-bottom:7px;}
.cp .cpn{font-family:'Oswald',sans-serif;font-size:.95rem;letter-spacing:1px;color:var(--text);}
.cp .cps{font-size:.7rem;color:var(--muted);margin-top:3px;line-height:1.35;}
.cp.sel .cpn{color:var(--gold);}

/* Stat bars */
.sr{display:flex;align-items:center;gap:10px;margin-bottom:8px;}
.sl{font-family:'DM Mono',monospace;font-size:.63rem;letter-spacing:1px;text-transform:uppercase;color:var(--muted);width:82px;flex-shrink:0;}
.sb{flex:1;height:5px;background:var(--border);border-radius:3px;overflow:hidden;}
.sf{height:100%;border-radius:3px;transition:width .4s ease;}
.sf.g{background:var(--green);}
.sf.gd{background:var(--gold);}
.sf.b{background:var(--blue);}
.sv{font-family:'DM Mono',monospace;font-size:.68rem;color:var(--text);width:24px;text-align:right;}

/* Avatar builder */
.av-layout{display:grid;grid-template-columns:200px 1fr;gap:24px;align-items:start;}
@media(max-width:600px){.av-layout{grid-template-columns:1fr;}}
.av-preview{display:flex;flex-direction:column;align-items:center;gap:10px;position:sticky;top:60px;}
.av-canvas-bg{background:linear-gradient(160deg,#141428,#0a0a18);border:1px solid var(--border2);border-radius:14px;padding:16px 14px;display:inline-flex;align-items:center;justify-content:center;}
.av-opts{display:flex;flex-direction:column;gap:16px;}
.sw-row{display:flex;gap:7px;flex-wrap:wrap;margin-top:5px;}
.sw{width:26px;height:26px;border-radius:50%;border:2px solid transparent;cursor:pointer;transition:all .15s;}
.sw:hover{transform:scale(1.15);}
.sw.sel{border-color:var(--gold);box-shadow:0 0 0 2px rgba(232,184,75,.4);}
.gb-row{display:flex;gap:6px;flex-wrap:wrap;margin-top:5px;}
.gBtn{font-family:'DM Mono',monospace;font-size:.6rem;letter-spacing:.5px;padding:5px 9px;border:1px solid var(--border2);border-radius:4px;background:transparent;color:var(--muted);cursor:pointer;transition:all .15s;}
.gBtn:hover{border-color:var(--text);color:var(--text);}
.gBtn.sel{border-color:var(--gold);color:var(--gold);background:var(--gold3);}

/* Model preview cards (premade) */
.model-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(110px,1fr));gap:12px;margin-bottom:20px;}
.model-card{background:var(--s2);border:2px solid var(--border);border-radius:10px;padding:10px 6px;cursor:pointer;transition:all .2s;text-align:center;}
.model-card:hover{border-color:var(--border2);}
.model-card.sel{border-color:var(--gold);background:var(--gold3);}
.model-card .mn{font-family:'Oswald',sans-serif;font-size:.78rem;letter-spacing:1px;margin-top:6px;color:var(--text);}
.model-card.sel .mn{color:var(--gold);}

/* Club picker */
.ltabs{display:flex;gap:5px;flex-wrap:wrap;margin-bottom:14px;}
.ltab{font-family:'DM Mono',monospace;font-size:.6rem;letter-spacing:1px;text-transform:uppercase;padding:5px 11px;border:1px solid var(--border2);border-radius:4px;background:transparent;color:var(--muted);cursor:pointer;transition:all .15s;}
.ltab:hover{color:var(--text);}
.ltab.sel{border-color:var(--gold);color:var(--gold);background:var(--gold3);}
.club-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:8px;max-height:320px;overflow-y:auto;padding-right:4px;}
.club-card{background:var(--s2);border:2px solid var(--border);border-radius:8px;padding:10px;cursor:pointer;transition:all .15s;display:flex;align-items:center;gap:8px;}
.club-card:hover{border-color:var(--border2);}
.club-card.sel{border-color:var(--gold);background:var(--gold3);}
.cbadge{width:30px;height:30px;border-radius:5px;display:flex;align-items:center;justify-content:center;font-size:.65rem;font-weight:700;font-family:'Oswald',sans-serif;flex-shrink:0;}
.cn{font-size:.78rem;font-weight:500;line-height:1.2;}
.cl{font-family:'DM Mono',monospace;font-size:.56rem;color:var(--muted);}

/* Wiz nav */
.wiz-nav{display:flex;gap:10px;margin-top:28px;}
.wbtn{font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:2px;padding:12px 24px;border-radius:6px;border:2px solid;cursor:pointer;transition:all .2s;font-weight:500;}
.wbtn.back{background:transparent;border-color:var(--border2);color:var(--muted);}
.wbtn.back:hover{border-color:var(--text);color:var(--text);}
.wbtn.nxt{background:var(--gold);border-color:var(--gold);color:#000;flex:1;}
.wbtn.nxt:hover{background:#f5c85a;}

/* CAREER HUB */
#screen-career{padding:0;}
.career-wrap{max-width:980px;margin:0 auto;padding:24px 20px;}
.career-topbar{display:grid;grid-template-columns:auto 1fr auto;gap:16px;align-items:center;padding-bottom:18px;border-bottom:1px solid var(--border);margin-bottom:20px;}
.player-badge{display:flex;align-items:center;gap:14px;}
.pb-canvas{width:60px;height:82px;background:var(--s2);border-radius:8px;overflow:hidden;display:flex;align-items:center;justify-content:center;}
.pb-name{font-family:'Oswald',sans-serif;font-size:1.5rem;letter-spacing:1px;line-height:1;}
.pb-club{font-size:.78rem;color:var(--muted);margin-top:2px;}
.pb-stats{display:flex;gap:14px;}
.pbs{text-align:center;}
.pbs .n{font-family:'Oswald',sans-serif;font-size:1.4rem;color:var(--gold);line-height:1;}
.pbs .l{font-family:'DM Mono',monospace;font-size:.54rem;color:var(--muted);letter-spacing:1px;margin-top:1px;}
.ovr-box{background:linear-gradient(135deg,var(--gold),var(--gold2));border-radius:8px;padding:10px 16px;text-align:center;}
.ovr-n{font-family:'Oswald',sans-serif;font-size:2rem;font-weight:700;color:#000;line-height:1;}
.ovr-l{font-family:'DM Mono',monospace;font-size:.54rem;color:rgba(0,0,0,.7);letter-spacing:1px;}
.sbar{background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:12px 16px;margin-bottom:18px;display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap;}
.sbi{}
.sbi .lbl{font-family:'DM Mono',monospace;font-size:.58rem;color:var(--muted);letter-spacing:1px;text-transform:uppercase;}
.sbi .val{font-family:'Oswald',sans-serif;font-size:1rem;margin-top:2px;}
.sbi .val.g{color:var(--gold);}
.fav-wrap{flex:1;min-width:140px;}
.fav-bg{height:7px;background:var(--border);border-radius:4px;overflow:hidden;margin-top:4px;}
.fav-fill{height:100%;border-radius:4px;transition:width .5s ease;}
.career-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:12px;margin-bottom:18px;}
.cc{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:16px;cursor:pointer;transition:all .2s;position:relative;overflow:hidden;}
.cc::before{content:'';position:absolute;left:0;top:0;bottom:0;width:3px;background:var(--gold);transform:scaleY(0);transition:transform .2s;transform-origin:bottom;}
.cc:hover{border-color:var(--border2);transform:translateY(-2px);}
.cc:hover::before{transform:scaleY(1);}
.cc .ci{font-size:1.6rem;margin-bottom:8px;}
.cc .ct{font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:1px;margin-bottom:3px;}
.cc .cd{font-size:.75rem;color:var(--muted);}
.ndot{position:absolute;top:10px;right:10px;width:7px;height:7px;border-radius:50%;background:var(--gold);animation:blink 1.5s infinite;}
@keyframes blink{0%,100%{opacity:1;}50%{opacity:.3;}}

/* MATCH SCREEN */
.match-wrap{max-width:900px;margin:0 auto;padding:24px 20px;}
.match-comp-bar{font-family:'DM Mono',monospace;font-size:.65rem;letter-spacing:2px;text-transform:uppercase;color:var(--muted);margin-bottom:12px;}
.match-header{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;gap:12px;background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:18px 20px;margin-bottom:16px;}
.mh-team{display:flex;flex-direction:column;align-items:center;gap:8px;}
.mh-team.right{align-items:flex-end;text-align:right;}
.mh-badge{width:52px;height:52px;border-radius:10px;display:flex;align-items:center;justify-content:center;font-family:'Oswald',sans-serif;font-size:.9rem;font-weight:700;}
.mh-name{font-family:'Oswald',sans-serif;font-size:1.1rem;letter-spacing:1px;}
.mh-cen{text-align:center;}
.score-disp{font-family:'Oswald',sans-serif;font-size:2.8rem;font-weight:700;letter-spacing:4px;line-height:1;}
.match-minute{font-family:'DM Mono',monospace;font-size:.65rem;color:var(--gold);letter-spacing:2px;margin-top:4px;}
.comp-tag{font-family:'DM Mono',monospace;font-size:.6rem;color:var(--muted);letter-spacing:1px;margin-top:2px;}

/* Pitch visual */
.pitch-wrap{background:#1a3a1a;border:2px solid #2a5a2a;border-radius:10px;overflow:hidden;margin-bottom:14px;position:relative;}
.pitch-canvas{width:100%;display:block;}

/* Event log */
.elog{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:14px;max-height:220px;overflow-y:auto;margin-bottom:14px;}
.elog-entry{font-size:.83rem;padding:4px 0;border-bottom:1px solid rgba(255,255,255,.04);animation:logIn .25s ease;}
@keyframes logIn{from{opacity:0;transform:translateY(4px);}to{opacity:1;transform:translateY(0);}}
.eg{color:var(--green);}
.er{color:#ef5350;}
.ee{color:var(--gold);font-weight:600;}
.en{color:var(--muted);}

/* Decision panel */
.decision-panel{background:var(--s1);border:2px solid var(--gold2);border-radius:var(--radius);padding:18px;margin-bottom:14px;animation:fadeUp .3s ease;}
.dp-title{font-family:'Oswald',sans-serif;font-size:1.1rem;letter-spacing:1px;color:var(--gold);margin-bottom:6px;}
.dp-situation{font-size:.84rem;line-height:1.6;color:var(--text);margin-bottom:12px;border-left:3px solid var(--gold2);padding-left:12px;font-style:italic;}
.dp-choices{display:flex;flex-direction:column;gap:8px;}
.dp-choice{background:var(--s2);border:1px solid var(--border2);border-radius:7px;padding:12px 14px;cursor:pointer;transition:all .2s;display:flex;align-items:center;justify-content:space-between;gap:10px;}
.dp-choice:hover{border-color:var(--gold);background:var(--gold3);}
.dp-choice .dct{font-family:'Oswald',sans-serif;font-size:.95rem;letter-spacing:.5px;}
.dp-choice .dcs{font-size:.75rem;color:var(--muted);margin-top:2px;}
.dp-choice .dco{font-family:'DM Mono',monospace;font-size:.6rem;padding:3px 8px;border-radius:3px;white-space:nowrap;}
.outcome-great{background:rgba(0,200,83,.15);color:var(--green);border:1px solid var(--green);}
.outcome-ok{background:rgba(232,184,75,.12);color:var(--gold);border:1px solid var(--gold2);}
.outcome-poor{background:rgba(244,67,54,.12);color:#ef5350;border:1px solid #c62828;}

.match-acts{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:10px;}
.mact{font-family:'Oswald',sans-serif;font-size:.9rem;letter-spacing:1px;padding:10px 18px;border-radius:6px;border:2px solid;cursor:pointer;transition:all .2s;font-weight:500;}
.mact.primary{background:var(--green);border-color:var(--green);color:#000;}
.mact.primary:hover{background:#00e060;}
.mact.secondary{background:transparent;border-color:var(--border2);color:var(--text);}
.mact.secondary:hover{border-color:var(--muted);}
.mact.danger{background:transparent;border-color:#c62828;color:#ef5350;}

/* CUTSCENE */
.cs-overlay{position:fixed;inset:0;background:rgba(0,0,0,.92);z-index:500;display:none;align-items:center;justify-content:center;padding:16px;}
.cs-overlay.open{display:flex;animation:csIn .35s ease;}
@keyframes csIn{from{opacity:0;}to{opacity:1;}}
.cs-box{background:var(--s1);border:1px solid var(--border2);border-radius:14px;width:min(600px,95vw);overflow:hidden;box-shadow:0 30px 80px rgba(0,0,0,.8);}
.cs-head{background:linear-gradient(135deg,var(--s2),var(--s3));padding:18px 22px;border-bottom:1px solid var(--border2);display:flex;align-items:center;gap:12px;}
.cs-icon{font-size:2rem;}
.cs-htitle{font-family:'Oswald',sans-serif;font-size:1.5rem;letter-spacing:2px;color:var(--gold);}
.cs-hsub{font-family:'DM Mono',monospace;font-size:.62rem;color:var(--muted);letter-spacing:1px;margin-top:2px;}
.cs-body{padding:22px;}
.cs-scene{font-size:.9rem;line-height:1.7;color:var(--text);margin-bottom:16px;font-style:italic;border-left:3px solid var(--gold2);padding-left:12px;}
.cs-q{font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:1px;color:var(--text);margin-bottom:14px;}
.cs-choices{display:flex;flex-direction:column;gap:8px;}
.cs-ch{background:var(--s2);border:2px solid var(--border2);border-radius:8px;padding:12px 16px;cursor:pointer;transition:all .2s;text-align:left;}
.cs-ch:hover{border-color:var(--gold);background:var(--gold3);}
.cs-ch .cht{font-family:'Oswald',sans-serif;font-size:.95rem;letter-spacing:1px;color:var(--text);}
.cs-ch .chs{font-size:.76rem;color:var(--muted);margin-top:2px;}
.cs-ch:hover .cht{color:var(--gold);}

/* PANEL */
.panel{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:18px;margin-bottom:14px;}
.ph{font-family:'Oswald',sans-serif;font-size:.85rem;letter-spacing:2px;color:var(--muted);text-transform:uppercase;margin-bottom:14px;}
.back-btn{font-family:'DM Mono',monospace;font-size:.65rem;letter-spacing:1px;text-transform:uppercase;padding:7px 14px;background:transparent;border:1px solid var(--border2);border-radius:4px;color:var(--muted);cursor:pointer;transition:all .2s;margin-bottom:20px;display:inline-block;}
.back-btn:hover{border-color:var(--text);color:var(--text);}
.sh{font-family:'Oswald',sans-serif;font-size:1.9rem;letter-spacing:2px;color:var(--gold);margin-bottom:4px;}
.ss{font-family:'DM Mono',monospace;font-size:.63rem;letter-spacing:2px;color:var(--muted);text-transform:uppercase;margin-bottom:22px;}

/* Playstyle chips */
.ps-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(120px,1fr));gap:8px;}
.ps-chip{background:var(--s2);border:1px solid var(--border2);border-radius:6px;padding:8px 10px;text-align:center;}
.ps-chip .psi{font-size:1.2rem;}
.ps-chip .psn{font-family:'Oswald',sans-serif;font-size:.75rem;letter-spacing:.5px;margin-top:3px;}
.ps-chip .psd{font-size:.6rem;color:var(--muted);margin-top:2px;}
.ps-chip.gold{border-color:var(--gold2);background:var(--gold3);}
.ps-chip.gold .psn{color:var(--gold);}

/* Transfer card */
.tc{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:14px 18px;margin-bottom:10px;display:flex;align-items:center;justify-content:space-between;gap:14px;transition:border-color .2s;}
.tc:hover{border-color:var(--border2);}
.tc-l{display:flex;align-items:center;gap:12px;}
.tc-b{width:42px;height:42px;border-radius:7px;display:flex;align-items:center;justify-content:center;font-family:'Oswald',sans-serif;font-size:.82rem;font-weight:700;}
.tc-n{font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:1px;}
.tc-s{font-size:.75rem;color:var(--muted);margin-top:2px;}
.tc-w{font-family:'DM Mono',monospace;font-size:.65rem;color:var(--gold);margin-top:2px;}
.tc-r{display:flex;flex-direction:column;align-items:flex-end;gap:5px;}
.tc-fee{font-family:'Oswald',sans-serif;font-size:1.1rem;color:var(--gold);}
.act-btn{font-family:'Oswald',sans-serif;font-size:.8rem;letter-spacing:1px;padding:6px 14px;border-radius:5px;border:2px solid;cursor:pointer;transition:all .2s;}
.act-btn.acc{border-color:var(--green);color:var(--green);}
.act-btn.acc:hover{background:var(--green);color:#000;}
.act-btn.rej{border-color:#c62828;color:#ef5350;}
.act-btn.rej:hover{background:#c62828;color:#fff;}

/* Comp entry */
.comp-entry{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:12px 16px;display:flex;align-items:center;justify-content:space-between;gap:12px;cursor:pointer;transition:all .2s;margin-bottom:8px;}
.comp-entry:hover{border-color:var(--border2);transform:translateX(3px);}
.ce-l{display:flex;align-items:center;gap:10px;}
.ce-ic{font-size:1.5rem;}
.ce-nm{font-family:'Oswald',sans-serif;font-size:.95rem;letter-spacing:1px;}
.ce-rd{font-family:'DM Mono',monospace;font-size:.6rem;color:var(--muted);}
.ce-st{font-family:'DM Mono',monospace;font-size:.62rem;letter-spacing:1px;padding:3px 8px;border-radius:3px;}
.st-active{background:rgba(0,200,83,.15);color:var(--green);border:1px solid var(--green);}
.st-upcoming{background:rgba(232,184,75,.1);color:var(--gold);border:1px solid var(--gold2);}
.st-elim{background:rgba(244,67,54,.1);color:#ef5350;border:1px solid #c62828;}
.st-won{background:rgba(41,121,255,.15);color:var(--blue);border:1px solid var(--blue);}

/* Toast */
.toast-wrap{position:fixed;bottom:24px;right:24px;display:flex;flex-direction:column;gap:8px;z-index:400;}
.toast{background:var(--s2);border:1px solid var(--border2);border-radius:8px;padding:10px 16px;font-family:'DM Mono',monospace;font-size:.72rem;letter-spacing:.5px;transform:translateX(120px);opacity:0;transition:all .3s;max-width:280px;pointer-events:none;}
.toast.show{transform:translateX(0);opacity:1;}
.toast.tg{border-color:var(--gold2);color:var(--gold);}
.toast.tgr{border-color:var(--green);color:var(--green);}
.toast.tr{border-color:#c62828;color:#ef5350;}
.divider{height:1px;background:var(--border);margin:16px 0;}
.info-box{background:rgba(0,229,255,.05);border:1px solid rgba(0,229,255,.2);border-radius:6px;padding:10px 14px;font-family:'DM Mono',monospace;font-size:.68rem;color:var(--cyan);margin-bottom:14px;}
.warn-box{background:rgba(232,184,75,.05);border:1px solid rgba(232,184,75,.2);border-radius:6px;padding:10px 14px;font-family:'DM Mono',monospace;font-size:.68rem;color:var(--gold);margin-bottom:14px;}

/* ── DRILL CARDS ── */
.drill-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:14px 16px;display:flex;align-items:center;gap:14px;margin-bottom:10px;cursor:pointer;transition:all .2s;}
.drill-card:hover{border-color:var(--gold);transform:translateX(3px);}
.drill-card.locked{opacity:.4;cursor:not-allowed;}
.drill-card.locked:hover{border-color:var(--border);transform:none;}
.drill-icon{font-size:1.8rem;flex-shrink:0;}
.drill-info{}
.drill-name{font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:1px;color:var(--text);}
.drill-desc{font-size:.75rem;color:var(--muted);margin-top:2px;}
.drill-reward{font-family:'DM Mono',monospace;font-size:.65rem;color:var(--gold);margin-top:4px;}
.fatigue-wrap{background:var(--s2);border:1px solid var(--border);border-radius:8px;padding:12px 16px;margin-bottom:16px;display:flex;align-items:center;gap:16px;}
.fatigue-bar-bg{flex:1;height:8px;background:var(--border);border-radius:4px;overflow:hidden;}
/* ── CALENDAR ── */
.cal-month{margin-bottom:20px;}
.cal-month-head{font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:2px;color:var(--gold);padding-bottom:8px;border-bottom:1px solid var(--border);margin-bottom:8px;}
.cal-entry{display:flex;align-items:center;gap:12px;padding:7px 0;border-bottom:1px solid rgba(255,255,255,.04);font-size:.82rem;}
.cal-day{font-family:'DM Mono',monospace;font-size:.7rem;color:var(--muted);width:22px;flex-shrink:0;}
.cal-type{font-family:'DM Mono',monospace;font-size:.68rem;letter-spacing:1px;width:90px;flex-shrink:0;}
.cal-comp{color:var(--muted);font-size:.78rem;}
/* ── AGENT ── */
.agent-card{background:var(--s1);border:1px solid var(--border);border-radius:var(--radius);padding:20px;}
.agent-header{display:flex;align-items:center;gap:14px;margin-bottom:18px;padding-bottom:14px;border-bottom:1px solid var(--border);}
.agent-icon{font-size:2.2rem;}
.agent-name{font-family:'Oswald',sans-serif;font-size:1.3rem;letter-spacing:1px;color:var(--text);}
.agent-title{font-family:'DM Mono',monospace;font-size:.62rem;color:var(--muted);letter-spacing:1px;margin-top:2px;}
.agent-body{display:flex;flex-direction:column;gap:0;}
.agent-row{display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid var(--border);font-family:'DM Mono',monospace;font-size:.72rem;color:var(--muted);}
.agent-row:last-child{border-bottom:none;}
.agent-val{color:var(--text);}
.agent-actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:16px;}
/* ── SIM BUTTON ── */
.sim-btn{font-family:'Oswald',sans-serif;font-size:.95rem;letter-spacing:2px;padding:12px 20px;border-radius:6px;border:2px solid var(--muted);color:var(--text);background:transparent;cursor:pointer;transition:all .2s;}
.sim-btn:hover{border-color:var(--text);background:var(--s2);}
/* ── LEAGUE TABLE ── */
.league-table{width:100%;border-collapse:collapse;font-size:.78rem;}
.league-table th{font-family:'DM Mono',monospace;font-size:.6rem;letter-spacing:1px;text-transform:uppercase;color:var(--muted);padding:6px 8px;text-align:left;border-bottom:1px solid var(--border);}
.league-table td{padding:6px 8px;border-bottom:1px solid rgba(255,255,255,.04);}
.league-table tr.you-row{background:var(--gold3);font-weight:600;}
.league-table tr.you-row td{color:var(--gold);}
.pos-dot{width:8px;height:8px;border-radius:50%;display:inline-block;margin-right:6px;}

/* Training upgrade row */
.tr-row{display:flex;align-items:center;gap:10px;margin-bottom:8px;}
.tr-l{font-family:'DM Mono',monospace;font-size:.62rem;letter-spacing:1px;color:var(--muted);text-transform:uppercase;width:100px;flex-shrink:0;}
.tr-bg{flex:1;height:5px;background:var(--border);border-radius:3px;overflow:hidden;}
.tr-fill{height:100%;border-radius:3px;background:var(--gold);transition:width .3s;}
.tr-v{font-family:'DM Mono',monospace;font-size:.67rem;color:var(--text);width:24px;text-align:right;}
.tr-btn{font-family:'DM Mono',monospace;font-size:.58rem;padding:3px 8px;border:1px solid var(--border2);border-radius:3px;background:transparent;color:var(--gold);cursor:pointer;white-space:nowrap;transition:all .15s;}
.tr-btn:hover{border-color:var(--gold);background:var(--gold3);}
</style>
</head>
<body>

<nav>
  <a class="nav-logo" href="index.html">Flugame<span class="slash">/</span>MMA</a>
  <div class="nav-links">
    <a href="index.html"
    <a href="Rankings.html">Rankings</a>
    <a href="streaming.html">notes</a>
    <a href="Predictions.html">Predictions</a>
    <a href="forum.html">Forum</a>
    <a href="Game.html">game</a>
    <a href="football.html" class="active">footy</a>
  </div>
</nav>

<div class="toast-wrap" id="toastWrap"></div>

<!-- CUTSCENE -->
<div class="cs-overlay" id="csOverlay">
  <div class="cs-box">
    <div class="cs-head">
      <div class="cs-icon" id="csIcon">⚽</div>
      <div>
        <div class="cs-htitle" id="csTitle">Decision</div>
        <div class="cs-hsub" id="csSub">Your move</div>
      </div>
    </div>
    <div class="cs-body">
      <div class="cs-scene" id="csScene"></div>
      <div class="cs-q" id="csQ"></div>
      <div class="cs-choices" id="csChoices"></div>
    </div>
  </div>
</div>

<!-- ═══════════════════ MENU ═══════════════════ -->
<div class="screen" id="screen-menu">
  <div class="menu-wrap">
    <div class="menu-pitch"></div>
    <div class="menu-ring" style="width:700px;height:700px;top:50%;left:50%;transform:translate(-50%,-50%)"></div>
    <div class="menu-ring" style="width:1100px;height:1100px;top:50%;left:50%;transform:translate(-50%,-50%);animation-delay:2.5s"></div>
    <div class="menu-eyebrow">FlugameMMA presents</div>
    <div class="menu-title"><span class="t1">FOOTBALL</span><span class="t2">LEGACY</span></div>
    <div class="menu-subtitle">Build your career. Write your legend.</div>
    <div class="menu-btns" id="menuBtns"></div>
  </div>
</div>

<!-- ═══════════════════ CREATE ═══════════════════ -->
<div class="screen" id="screen-create">
  <div class="wizard-wrap">
    <div class="wiz-progress" id="wizProg"></div>

    <!-- Step 1: Identity -->
    <div class="wiz-step active" id="step-1">
      <div class="wiz-title">Create Your Player</div>
      <div class="wiz-sub">Step 1 of 6 — Identity</div>
      <div class="two-col"><div class="fg"><label class="fl">First Name</label><input class="fi" id="firstName" type="text" placeholder="First name..." maxlength="16"/></div><div class="fg"><label class="fl">Last Name</label><input class="fi" id="lastName" type="text" placeholder="Last name..." maxlength="16"/></div></div>
      <div class="three-col">
        <div class="fg"><label class="fl">Starting Age</label><select class="fi" id="startAge"><option value="16">16 — Wonderkid</option><option value="18" selected>18 — Young Pro</option><option value="20">20 — Developing</option><option value="22">22 — Late Bloomer</option></select></div>
        <div class="fg"><label class="fl">Nationality</label><select class="fi" id="natSel"></select></div>
        <div class="fg"><label class="fl">Position</label><select class="fi" id="posSel">
          <optgroup label="Goalkeeper"><option value="GK">GK — Goalkeeper</option></optgroup>
          <optgroup label="Defenders">
            <option value="CB">CB — Centre-Back</option><option value="LB">LB — Left-Back</option><option value="RB">RB — Right-Back</option>
            <option value="LWB">LWB — Left Wing-Back</option><option value="RWB">RWB — Right Wing-Back</option>
          </optgroup>
          <optgroup label="Midfielders">
            <option value="CDM">CDM — Defensive Mid</option><option value="CM" selected>CM — Central Mid</option>
            <option value="CAM">CAM — Attacking Mid</option><option value="LM">LM — Left Mid</option><option value="RM">RM — Right Mid</option>
          </optgroup>
          <optgroup label="Forwards">
            <option value="LW">LW — Left Wing</option><option value="RW">RW — Right Wing</option>
            <option value="CF">CF — Centre-Forward</option><option value="ST">ST — Striker</option>
          </optgroup>
        </select></div>
      </div>
      <div class="fg"><label class="fl">Preferred Foot</label>
        <div class="card-grid" style="grid-template-columns:1fr 1fr 1fr;">
          <div class="cp sel" data-foot="right"><div class="cpi">🦵</div><div class="cpn">Right</div><div class="cps">Standard</div></div>
          <div class="cp" data-foot="left"><div class="cpi">🦵</div><div class="cpn">Left</div><div class="cps">Rare</div></div>
          <div class="cp" data-foot="both"><div class="cpi">⚡</div><div class="cpn">Both</div><div class="cps">Elite</div></div>
        </div>
      </div>
      <div class="two-col">
        <div class="fg"><label class="fl">Height (cm)</label><select class="fi" id="heightSel"><option value="165">5'5" (165cm)</option><option value="168">5'6" (168cm)</option><option value="170">5'7" (170cm)</option><option value="172">5'8" (172cm)</option><option value="175" selected>5'9" (175cm)</option><option value="178">5'10" (178cm)</option><option value="180">5'11" (180cm)</option><option value="183">6'0" (183cm)</option><option value="185">6'1" (185cm)</option><option value="188">6'2" (188cm)</option><option value="191">6'3" (191cm)</option><option value="196">6'5" (196cm)</option></select></div>
        <div class="fg"><label class="fl">Body Type</label><select class="fi" id="bodySel"><option value="lean">Lean — Fast & Low Weight</option><option value="normal" selected>Normal — Balanced</option><option value="stocky">Stocky — Strong & Physical</option><option value="tall">Tall & Lean — Aerial Threat</option></select></div>
      </div>
      <div class="wiz-nav"><button class="wbtn nxt" onclick="wizNext()">Continue →</button></div>
    </div>

    <!-- Step 2: Look -->
    <div class="wiz-step" id="step-2">
      <div class="wiz-title">Appearance</div>
      <div class="wiz-sub">Step 2 of 6 — Choose your look</div>
      <label class="fl">Choose a Base Model</label>
      <div class="model-grid" id="modelGrid"></div>
      <div class="av-layout">
        <div class="av-preview">
          <div class="av-canvas-bg"><canvas id="playerCanvas" width="120" height="172"></canvas></div>
          <div style="font-family:'DM Mono',monospace;font-size:.58rem;color:var(--muted);letter-spacing:1px;margin-top:6px;text-align:center;">LIVE PREVIEW</div>
        </div>
        <div class="av-opts">
          <div class="fg"><label class="fl">Hair Style</label><div class="gb-row" id="hairStyleRow"></div></div>
          <div class="fg"><label class="fl">Hair Color</label><div class="sw-row" id="hairColorRow"></div></div>
          <div class="fg"><label class="fl">Skin Tone</label><div class="sw-row" id="skinRow"></div></div>
          <div class="fg"><label class="fl">Kit Color</label><div class="sw-row" id="kitRow"></div></div>
          <div class="fg"><label class="fl">Boots</label><div class="sw-row" id="bootRow"></div></div>
        </div>
      </div>
      <div class="wiz-nav"><button class="wbtn back" onclick="wizBack()">← Back</button><button class="wbtn nxt" onclick="wizNext()">Continue →</button></div>
    </div>

    <!-- Step 3: Playstyle -->
    <div class="wiz-step" id="step-3">
      <div class="wiz-title">Play Style</div>
      <div class="wiz-sub">Step 3 of 6 — FC26 PlayStyles</div>
      <div class="card-grid" id="archGrid"></div>
      <div class="panel" id="statPrev" style="margin-top:16px;"></div>
      <div class="wiz-nav"><button class="wbtn back" onclick="wizBack()">← Back</button><button class="wbtn nxt" onclick="wizNext()">Continue →</button></div>
    </div>

    <!-- Step 4: Academy -->
    <div class="wiz-step" id="step-4">
      <div class="wiz-title">Academy</div>
      <div class="wiz-sub">Step 4 of 6 — Your background</div>
      <div class="card-grid" id="acadGrid"></div>
      <div class="wiz-nav"><button class="wbtn back" onclick="wizBack()">← Back</button><button class="wbtn nxt" onclick="wizNext()">Continue →</button></div>
    </div>

    <!-- Step 5: Starting Club -->
    <div class="wiz-step" id="step-5">
      <div class="wiz-title">Starting Club</div>
      <div class="wiz-sub">Step 5 of 6 — Where you begin</div>
      <div class="ltabs" id="leagueTabs"></div>
      <div class="fg"><input class="fi" id="clubSearch" type="text" placeholder="Search clubs..."/></div>
      <div class="club-grid" id="clubGrid"></div>
      <div class="wiz-nav"><button class="wbtn back" onclick="wizBack()">← Back</button><button class="wbtn nxt" onclick="beginCareer()">Begin Career ⚽</button></div>
    </div>
  </div>
</div>

<!-- ═══════════════════ CAREER HUB ═══════════════════ -->
<div class="screen" id="screen-career">
  <div class="career-wrap">
    <div class="career-topbar">
      <div class="player-badge">
        <div class="pb-canvas"><canvas id="careerCanvas" width="60" height="82"></canvas></div>
        <div>
          <div class="pb-name" id="pbName">—</div>
          <div class="pb-club" id="pbClub">—</div>
          <div style="display:flex;gap:5px;margin-top:5px;flex-wrap:wrap;" id="pbPills"></div>
        </div>
      </div>
      <div class="pb-stats" id="pbStats"></div>
      <div class="ovr-box"><div class="ovr-n" id="ovrNum">60</div><div class="ovr-l">OVR</div></div>
    </div>
    <div class="sbar">
      <div class="sbi"><div class="lbl">Season</div><div class="val g" id="sbSeason">2024/25</div></div>
      <div class="sbi"><div class="lbl">Age</div><div class="val" id="sbAge">18</div></div>
      <div class="sbi"><div class="lbl">Matches Left</div><div class="val" id="sbMatchLeft">—</div></div>
      <div class="sbi"><div class="lbl">Salary</div><div class="val g" id="sbSalary">—</div></div>
      <div class="fav-wrap">
        <div class="lbl">Manager Favor</div>
        <div class="fav-bg"><div class="fav-fill" id="favFill"></div></div>
        <div id="favLabel" style="font-family:'DM Mono',monospace;font-size:.58rem;color:var(--muted);margin-top:3px;"></div>
      </div>
    </div>
    <div id="champBanner" style="display:none;background:linear-gradient(135deg,var(--gold3),transparent);border:1px solid var(--gold2);border-radius:8px;padding:10px 16px;text-align:center;font-family:'Oswald',sans-serif;font-size:1rem;letter-spacing:3px;color:var(--gold);margin-bottom:14px;">🏆 &nbsp; CHAMPION &nbsp; 🏆</div>
    <div class="career-grid" id="careerGrid"></div>
    <button class="back-btn" onclick="confirmReset()">⚠ Reset Career</button>
  </div>
</div>

<!-- ═══════════════════ MATCH ═══════════════════ -->
<div class="screen" id="screen-match">
  <div class="match-wrap">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="match-comp-bar" id="matchCompBar">League Match</div>
    <div class="match-header" id="matchHeader"></div>
    <canvas class="pitch-canvas" id="pitchCanvas" height="220"></canvas>
    <div class="match-acts" id="matchActs"></div>
    <div class="decision-panel" id="decisionPanel" style="display:none;"></div>
    <div class="elog" id="elog"></div>
  </div>
</div>

<!-- ═══════════════════ TRANSFERS ═══════════════════ -->
<div class="screen" id="screen-transfers">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="sh">Transfer Market</div>
    <div class="ss" id="transSub">Market overview</div>
    <div id="transContent"></div>
  </div>
</div>

<!-- ═══════════════════ COMPETITIONS ═══════════════════ -->
<div class="screen" id="screen-comps">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="sh">Competitions</div>
    <div class="ss" id="compSub">Active this season</div>
    <div id="compList"></div>
  </div>
</div>

<!-- ═══════════════════ PROFILE ═══════════════════ -->
<div class="screen" id="screen-profile">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div style="display:grid;grid-template-columns:180px 1fr;gap:20px;align-items:start;">
      <div class="panel" style="text-align:center;">
        <canvas id="profileCanvas" width="120" height="172"></canvas>
        <div style="font-family:'Oswald',sans-serif;font-size:1.3rem;letter-spacing:1px;margin-top:8px;" id="pcName">—</div>
        <div style="font-family:'DM Mono',monospace;font-size:.62rem;color:var(--gold);letter-spacing:2px;margin-top:3px;" id="pcPos">—</div>
        <div style="font-size:.75rem;color:var(--muted);margin-top:3px;" id="pcClub">—</div>
        <div style="display:inline-flex;align-items:center;justify-content:center;width:60px;height:60px;border-radius:50%;border:3px solid var(--gold);font-family:'Oswald',sans-serif;font-size:1.6rem;font-weight:700;color:var(--gold);margin:10px auto;" id="pcOvr">60</div>
      </div>
      <div>
        <div class="panel" id="profileStats"></div>
        <div class="panel" id="profilePlaystyles"></div>
        <div class="panel" id="profileHistory"></div>
      </div>
    </div>
  </div>
</div>


<!-- ═══════════════════ TRAINING DRILLS ═══════════════════ -->
<div class="screen" id="screen-training">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="sh">Training Ground</div>
    <div class="ss">Train to earn SP. Spend SP to upgrade stats.</div>
    <div class="fatigue-wrap">
      <span style="font-family:'DM Mono',monospace;font-size:.65rem;color:var(--muted);letter-spacing:1px;">FATIGUE</span>
      <div class="fatigue-bar-bg"><div id="fatigueBar" style="height:100%;border-radius:4px;transition:width .4s;"></div></div>
      <span id="fatigueLabel" style="font-family:'DM Mono',monospace;font-size:.65rem;color:var(--muted);white-space:nowrap;width:140px;text-align:right;"></span>
      <span style="font-family:'DM Mono',monospace;font-size:.65rem;color:var(--muted);">SP: <b id="tSpVal" style="color:var(--gold);font-size:.9rem;"></b></span>
    </div>
    <div class="panel">
      <div class="ph">Training Drills — Earn SP</div>
      <div id="drillGrid"></div>
    </div>
    <div class="panel">
      <div class="ph">Spend SP on Attributes</div>
      <div id="trainStats"></div>
    </div>
    <div class="panel">
      <div class="ph">Switch Position <span style="font-family:'DM Mono',monospace;font-size:.6rem;color:var(--muted);">(Costs 3 SP)</span></div>
      <div id="posSwitch"></div>
    </div>
  </div>
</div>

<!-- ═══════════════════ CALENDAR ═══════════════════ -->
<div class="screen" id="screen-calendar">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="sh">Season Calendar</div>
    <div class="ss" id="calSub">All fixtures this season</div>
    <div id="calendarContent"></div>
  </div>
</div>

<!-- ═══════════════════ AGENT / CONTRACTS ═══════════════════ -->
<div class="screen" id="screen-agent">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="sh">My Agent</div>
    <div class="ss" id="agentSub">Manage your career and contracts</div>
    <div id="agentContent"></div>
  </div>
</div>

<!-- ═══════════════════ LEAGUE TABLE ═══════════════════ -->
<div class="screen" id="screen-table">
  <div style="max-width:860px;margin:0 auto;padding:24px 20px;">
    <button class="back-btn" onclick="showScreen('career')">← Hub</button>
    <div class="sh">League Table</div>
    <div class="ss" id="tableSub">Current standings</div>
    <div class="panel" id="tableContent"></div>
  </div>
</div>



<script>
// ══════════════════════════════════════════════════════════════
// CONSTANTS & DATA
// ══════════════════════════════════════════════════════════════

const NATIONS=['Afghanistan','Albania','Algeria','Argentina','Armenia','Australia','Austria','Azerbaijan','Belgium','Bolivia','Bosnia','Brazil','Bulgaria','Cameroon','Canada','Chile','China','Colombia','Congo DR','Costa Rica','Croatia','Czech Republic','Denmark','Ecuador','Egypt','El Salvador','England','Estonia','Ethiopia','Finland','France','Gabon','Gambia','Georgia','Germany','Ghana','Greece','Guatemala','Guinea','Honduras','Hungary','Iceland','India','Iran','Iraq','Ireland','Israel','Italy','Ivory Coast','Jamaica','Japan','Jordan','Kazakhstan','Kenya','Kosovo','Latvia','Lebanon','Lithuania','Luxembourg','Mali','Morocco','Mexico','Moldova','Montenegro','Netherlands','New Zealand','Nigeria','North Macedonia','Northern Ireland','Norway','Pakistan','Palestine','Panama','Paraguay','Peru','Philippines','Poland','Portugal','Romania','Russia','Rwanda','Saudi Arabia','Scotland','Senegal','Serbia','Slovakia','Slovenia','South Africa','South Korea','Spain','Sweden','Switzerland','Syria','Tanzania','Thailand','Trinidad & Tobago','Tunisia','Turkey','Uganda','Ukraine','United States','Uruguay','Uzbekistan','Venezuela','Wales','Zambia','Zimbabwe'];

// FC26 exact playstyles per role
const PLAYSTYLES_DEF={
  magician:{icon:'🎩',name:'Magician',desc:'Finesse Shot',plus:'Finesse Shot+',cat:'forward'},
  finisher:{icon:'🎯',name:'Finisher',desc:'Low Driven Shot',plus:'Low Driven Shot+',cat:'forward'},
  target:{icon:'✈️',name:'Target',desc:'Precision Header',plus:'Precision Header+',cat:'forward'},
  recycler:{icon:'♻️',name:'Recycler',desc:'Intercept',plus:'Intercept+',cat:'mid'},
  maestro:{icon:'🎼',name:'Maestro',desc:'Pinged Pass',plus:'Pinged Pass+',cat:'mid'},
  creator:{icon:'🔑',name:'Creator',desc:'Incisive Pass',plus:'Incisive Pass+',cat:'mid'},
  spark:{icon:'⚡',name:'Spark',desc:'Trickster',plus:'Trickster+',cat:'mid'},
  progressor:{icon:'📈',name:'Progressor',desc:'Anticipate',plus:'Anticipate+',cat:'def'},
  boss:{icon:'💪',name:'Boss (Capitano)',desc:'Slide Tackle',plus:'Slide Tackle+',cat:'def'},
  engine:{icon:'🔋',name:'Engine',desc:'Relentless',plus:'Relentless+',cat:'def'},
  marauder:{icon:'🏃',name:'Marauder',desc:'Quick Step',plus:'Quick Step+',cat:'def'},
};

const ARCHETYPES=[
  {id:'magician',name:'Magician',icon:'🎩',pos:['LW','RW','CAM','CF'],desc:'Finesse curled shots',playstyle:'magician',stats:{pace:76,shooting:82,passing:78,dribbling:85,defending:34,physical:62}},
  {id:'finisher',name:'Finisher',icon:'🎯',pos:['ST','CF'],desc:'Clinical low-driven goals',playstyle:'finisher',stats:{pace:74,shooting:88,passing:64,dribbling:72,defending:30,physical:70}},
  {id:'target',name:'Target Man',icon:'✈️',pos:['ST','CF'],desc:'Dominant aerial striker',playstyle:'target',stats:{pace:62,shooting:80,passing:66,dribbling:58,defending:38,physical:88}},
  {id:'recycler',name:'Recycler',icon:'♻️',pos:['CDM','CM','LM','RM'],desc:'Win the ball, restart attacks',playstyle:'recycler',stats:{pace:72,shooting:54,passing:74,dribbling:68,defending:82,physical:76}},
  {id:'maestro',name:'Maestro',icon:'🎼',pos:['CM','CDM','CAM'],desc:'Dictates play with long passes',playstyle:'maestro',stats:{pace:64,shooting:62,passing:90,dribbling:72,defending:68,physical:66}},
  {id:'creator',name:'Creator',icon:'🔑',pos:['CAM','CM','LM','RM'],desc:'Incisive through balls',playstyle:'creator',stats:{pace:70,shooting:72,passing:86,dribbling:80,defending:46,physical:62}},
  {id:'spark',name:'Spark',icon:'⚡',pos:['LW','RW','LM','RM','CAM'],desc:'Skilful dribbler, flair player',playstyle:'spark',stats:{pace:82,shooting:72,passing:72,dribbling:88,defending:36,physical:66}},
  {id:'progressor',name:'Progressor',icon:'📈',pos:['CB','LB','RB','CDM'],desc:'Ball-playing defender',playstyle:'progressor',stats:{pace:70,shooting:44,passing:78,dribbling:66,defending:84,physical:78}},
  {id:'boss',name:'Boss',icon:'💪',pos:['CB','CDM','CM'],desc:'Aggressive slide tackler',playstyle:'boss',stats:{pace:68,shooting:46,passing:64,dribbling:58,defending:88,physical:86}},
  {id:'engine',name:'Engine',icon:'🔋',pos:['LB','RB','LWB','RWB','CM'],desc:'Tireless pressing runner',playstyle:'engine',stats:{pace:78,shooting:52,passing:72,dribbling:72,defending:76,physical:80}},
  {id:'marauder',name:'Marauder',icon:'🏃',pos:['LB','RB','LWB','RWB'],desc:'Overlapping full-back',playstyle:'marauder',stats:{pace:84,shooting:60,passing:74,dribbling:76,defending:74,physical:70}},
];

// Full stat list — outfield only
const OUTFIELD_STATS=['acceleration','sprint_speed','agility','balance','reactions','composure','aggression','jumping','stamina','strength','ball_control','dribbling','curve','finishing','free_kick','heading','long_shots','penalties','positioning','shot_power','volleys','crossing','long_passing','short_passing','vision','defensive_awareness','interceptions','sliding_tackle','standing_tackle'];
const GK_STATS=['gk_diving','gk_handling','gk_kicking','gk_positioning','gk_reflexes','gk_speed'];
const STAT_LABELS={acceleration:'Acceleration',sprint_speed:'Sprint Speed',agility:'Agility',balance:'Balance',reactions:'Reactions',composure:'Composure',aggression:'Aggression',jumping:'Jumping',stamina:'Stamina',strength:'Strength',ball_control:'Ball Control',dribbling:'Dribbling',curve:'Curve',finishing:'Finishing',free_kick:'Free Kick Acc.',heading:'Heading Acc.',long_shots:'Long Shots',penalties:'Penalties',positioning:'Positioning',shot_power:'Shot Power',volleys:'Volleys',crossing:'Crossing',long_passing:'Long Passing',short_passing:'Short Passing',vision:'Vision',defensive_awareness:'Def. Awareness',interceptions:'Interceptions',sliding_tackle:'Sliding Tackle',standing_tackle:'Standing Tackle',gk_diving:'GK Diving',gk_handling:'GK Handling',gk_kicking:'GK Kicking',gk_positioning:'GK Positioning',gk_reflexes:'GK Reflexes',gk_speed:'GK Speed'};
const STAT_GROUPS={pace:['acceleration','sprint_speed'],mental:['agility','balance','reactions','composure','aggression'],physical:['jumping','stamina','strength'],technical:['ball_control','dribbling','curve','finishing','free_kick','heading','long_shots','penalties','positioning','shot_power','volleys'],passing:['crossing','long_passing','short_passing','vision'],defending:['defensive_awareness','interceptions','sliding_tackle','standing_tackle'],gk:['gk_diving','gk_handling','gk_kicking','gk_positioning','gk_reflexes','gk_speed']};

const ACADEMIES=[
  {id:'la_masia',name:'La Masía',icon:'🟦',club:'Barcelona',desc:'Total technical football',boost:{ball_control:6,short_passing:6,vision:4},ps:'creator'},
  {id:'ajax',name:'Ajax Academy',icon:'⭕',club:'Ajax',desc:'Total Football',boost:{short_passing:5,defensive_awareness:4,dribbling:4},ps:'maestro'},
  {id:'chelsea',name:'Chelsea Academy',icon:'🔵',club:'Chelsea',desc:'Physical & modern',boost:{sprint_speed:5,stamina:5},ps:'engine'},
  {id:'real_madrid',name:'RM Cantera',icon:'⚪',club:'Real Madrid',desc:'Elite professionalism',boost:{finishing:5,composure:5},ps:'finisher'},
  {id:'dortmund',name:'BVB Academy',icon:'🟡',club:'Dortmund',desc:'High intensity pressing',boost:{acceleration:6,sprint_speed:4},ps:'marauder'},
  {id:'street',name:'Street Football',icon:'🏚️',club:'None',desc:'Raw unorthodox flair',boost:{dribbling:8,agility:4},ps:'spark'},
  {id:'southampton',name:'Southampton',icon:'🔴',club:'Southampton',desc:'World-class youth dev.',boost:{short_passing:6,vision:5},ps:'creator'},
  {id:'atalanta',name:'Atalanta',icon:'⚫',club:'Atalanta',desc:'Pressing specialists',boost:{defensive_awareness:5,stamina:5},ps:'recycler'},
];

// League fixture counts
const LEAGUE_FIXTURES={'Premier League':38,'Championship':46,'League One':46,'League Two':46,'National League':46,'Bundesliga':34,'Bundesliga 2':34,'3. Liga':38,'La Liga':38,'La Liga 2':42,'Serie A':38,'Serie B':38,'Ligue 1':34,'Ligue 2':38,'Eredivisie':34,'Primeira Liga':34,'Pro League':30,'Scottish Prem':38,'Süper Lig':38,'Russian Premier':30,'Super League':36,'MLS':34,'J-League':34,'K-League':38,'Saudi Pro League':30,'Chinese SL':30,'Argentine Primera':38,'Brasileirão':38,'default':38};

// League hierarchy for relegation/promotion
const LEAGUE_HIERARCHY={
  England:['Premier League','Championship','League One','League Two','National League'],
  Germany:['Bundesliga','Bundesliga 2','3. Liga'],
  Spain:['La Liga','La Liga 2'],
  Italy:['Serie A','Serie B'],
  France:['Ligue 1','Ligue 2'],
};

// Manager names pool
const MANAGER_NAMES=['Carlos Mendez','Jurgen Bauer','Roberto Silva','Erik Andersen','Marco Rossi','Philippe Dumont','David Walsh','Aleksei Petrov','Hiroshi Tanaka','Mohammed Al-Rashid','Seamus O Brien','Lars Bergstrom']

// Calendar months
const CALENDAR_MONTHS=['July','August','September','October','November','December','January','February','March','April','May','June'];
const MATCH_DAYS_PER_MONTH=[2,4,4,4,4,3,4,4,4,4,2,0]; // approx matchdays per month


// Salary tiers (£/week) by league prestige
const SALARY_TIERS={5:{min:80000,max:500000},4:{min:20000,max:150000},3:{min:5000,max:50000},2:{min:1000,max:15000},1:{min:500,max:8000}};
const LEAGUE_PRESTIGE={'Premier League':5,'Bundesliga':5,'La Liga':5,'Serie A':5,'Ligue 1':4,'Eredivisie':4,'Primeira Liga':4,'Süper Lig':4,'Scottish Prem':3,'Championship':3,'Bundesliga 2':3,'La Liga 2':3,'Serie B':3,'Ligue 2':3,'MLS':3,'Russian Premier':3,'default':2};

const CLUBS=[
  // Premier League
  {name:'Arsenal',league:'Premier League',country:'England',p:'#EF0107',s:'#FFFFFF',abbr:'ARS',tier:5},
  {name:'Aston Villa',league:'Premier League',country:'England',p:'#670E36',s:'#95BFE5',abbr:'AVL',tier:4},
  {name:'AFC Bournemouth',league:'Premier League',country:'England',p:'#DA291C',s:'#000000',abbr:'BOU',tier:3},
  {name:'Brentford',league:'Premier League',country:'England',p:'#E30613',s:'#FFE500',abbr:'BRE',tier:3},
  {name:'Brighton & Hove Albion',league:'Premier League',country:'England',p:'#0057B8',s:'#FFFFFF',abbr:'BHA',tier:3},
  {name:'Chelsea',league:'Premier League',country:'England',p:'#034694',s:'#FFFFFF',abbr:'CHE',tier:5},
  {name:'Crystal Palace',league:'Premier League',country:'England',p:'#1B458F',s:'#C4122E',abbr:'CRY',tier:3},
  {name:'Everton',league:'Premier League',country:'England',p:'#003399',s:'#FFFFFF',abbr:'EVE',tier:3},
  {name:'Fulham',league:'Premier League',country:'England',p:'#CC0000',s:'#FFFFFF',abbr:'FUL',tier:3},
  {name:'Liverpool',league:'Premier League',country:'England',p:'#C8102E',s:'#F6EB61',abbr:'LIV',tier:5},
  {name:'Manchester City',league:'Premier League',country:'England',p:'#6CABDD',s:'#FFFFFF',abbr:'MCI',tier:5},
  {name:'Manchester United',league:'Premier League',country:'England',p:'#DA291C',s:'#FBE122',abbr:'MUN',tier:5},
  {name:'Newcastle United',league:'Premier League',country:'England',p:'#241F20',s:'#FFFFFF',abbr:'NEW',tier:4},
  {name:'Nottingham Forest',league:'Premier League',country:'England',p:'#DD0000',s:'#FFFFFF',abbr:'NFO',tier:3},
  {name:'Southampton',league:'Premier League',country:'England',p:'#D71920',s:'#130C0E',abbr:'SOU',tier:2},
  {name:'Tottenham Hotspur',league:'Premier League',country:'England',p:'#132257',s:'#FFFFFF',abbr:'TOT',tier:5},
  {name:'West Ham United',league:'Premier League',country:'England',p:'#7A263A',s:'#1BB1E7',abbr:'WHU',tier:3},
  {name:'Wolverhampton Wanderers',league:'Premier League',country:'England',p:'#FDB913',s:'#231F20',abbr:'WOL',tier:3},
  // Championship
  {name:'Leeds United',league:'Championship',country:'England',p:'#FFCD00',s:'#1D428A',abbr:'LEE',tier:3},
  {name:'Sunderland',league:'Championship',country:'England',p:'#EB172B',s:'#FFFFFF',abbr:'SUN',tier:2},
  {name:'Burnley',league:'Championship',country:'England',p:'#6C1D45',s:'#99D6EA',abbr:'BUR',tier:2},
  {name:'Derby County',league:'Championship',country:'England',p:'#FFFFFF',s:'#000000',abbr:'DER',tier:2},
  {name:'Sheffield United',league:'Championship',country:'England',p:'#EE2737',s:'#000000',abbr:'SHU',tier:3},
  {name:'Middlesbrough',league:'Championship',country:'England',p:'#E21A24',s:'#FFFFFF',abbr:'MID',tier:2},
  {name:'Watford',league:'Championship',country:'England',p:'#FBEE23',s:'#ED2127',abbr:'WAT',tier:2},
  {name:'Coventry City',league:'Championship',country:'England',p:'#59CBBF',s:'#FFFFFF',abbr:'COV',tier:2},
  {name:'Hull City',league:'Championship',country:'England',p:'#F5A12D',s:'#000000',abbr:'HUL',tier:2},
  {name:'Norwich City',league:'Championship',country:'England',p:'#00A650',s:'#FFF200',abbr:'NOR',tier:2},
  {name:'QPR',league:'Championship',country:'England',p:'#1D5BA4',s:'#FFFFFF',abbr:'QPR',tier:2},
  {name:'Cardiff City',league:'Championship',country:'England',p:'#0070B5',s:'#D11524',abbr:'CAR',tier:2},
  {name:'West Bromwich Albion',league:'Championship',country:'England',p:'#003090',s:'#FFFFFF',abbr:'WBA',tier:2},
  {name:'Swansea City',league:'Championship',country:'England',p:'#FFFFFF',s:'#000000',abbr:'SWA',tier:2},
  {name:'Huddersfield',league:'Championship',country:'England',p:'#0E63AD',s:'#FFFFFF',abbr:'HTF',tier:2},
  // League One
  {name:'Portsmouth',league:'League One',country:'England',p:'#003399',s:'#FFFFFF',abbr:'POM',tier:2},
  {name:'Charlton Athletic',league:'League One',country:'England',p:'#CC0000',s:'#FFFFFF',abbr:'CHA',tier:2},
  {name:'Bolton Wanderers',league:'League One',country:'England',p:'#263B7E',s:'#FFFFFF',abbr:'BOL',tier:2},
  {name:'Plymouth Argyle',league:'League One',country:'England',p:'#007A53',s:'#FFFFFF',abbr:'PLY',tier:2},
  {name:'Birmingham City',league:'League One',country:'England',p:'#0000FF',s:'#FFFFFF',abbr:'BIR',tier:2},
  {name:'Millwall',league:'League One',country:'England',p:'#001D5E',s:'#FFFFFF',abbr:'MIL',tier:2},
  {name:'Exeter City',league:'League One',country:'England',p:'#CC0000',s:'#FFFFFF',abbr:'EXE',tier:1},
  {name:'Accrington Stanley',league:'League Two',country:'England',p:'#CC0000',s:'#FFFFFF',abbr:'ACC',tier:1},
  {name:'Newport County',league:'League Two',country:'England',p:'#F7A600',s:'#000000',abbr:'NPC',tier:1},
  {name:'Yeovil Town',league:'National League',country:'England',p:'#119728',s:'#FFFFFF',abbr:'YEO',tier:1},
  {name:'Kettering Town',league:'National League',country:'England',p:'#CC0000',s:'#FFFFFF',abbr:'KET',tier:1},
  // Bundesliga
  {name:'Bayern Munich',league:'Bundesliga',country:'Germany',p:'#DC052D',s:'#FFFFFF',abbr:'FCB',tier:5},
  {name:'Borussia Dortmund',league:'Bundesliga',country:'Germany',p:'#FDE100',s:'#000000',abbr:'BVB',tier:5},
  {name:'Bayer Leverkusen',league:'Bundesliga',country:'Germany',p:'#E32221',s:'#000000',abbr:'B04',tier:4},
  {name:'RB Leipzig',league:'Bundesliga',country:'Germany',p:'#DD0741',s:'#FFFFFF',abbr:'RBL',tier:4},
  {name:'Eintracht Frankfurt',league:'Bundesliga',country:'Germany',p:'#E1000F',s:'#000000',abbr:'SGE',tier:3},
  {name:'VfL Wolfsburg',league:'Bundesliga',country:'Germany',p:'#65B32E',s:'#FFFFFF',abbr:'WOB',tier:3},
  {name:'Hoffenheim',league:'Bundesliga',country:'Germany',p:'#1964B0',s:'#FFFFFF',abbr:'TSG',tier:3},
  {name:'VfB Stuttgart',league:'Bundesliga',country:'Germany',p:'#E32221',s:'#FFFFFF',abbr:'VFB',tier:3},
  {name:'Werder Bremen',league:'Bundesliga',country:'Germany',p:'#1D9053',s:'#FFFFFF',abbr:'SVW',tier:3},
  {name:'Borussia MGB',league:'Bundesliga',country:'Germany',p:'#000000',s:'#FFFFFF',abbr:'BMG',tier:3},
  {name:'Schalke 04',league:'Bundesliga 2',country:'Germany',p:'#004D9D',s:'#FFFFFF',abbr:'S04',tier:3},
  {name:'Hamburg SV',league:'Bundesliga 2',country:'Germany',p:'#0A1F60',s:'#FFFFFF',abbr:'HSV',tier:3},
  {name:'Hannover 96',league:'Bundesliga 2',country:'Germany',p:'#009A44',s:'#FFFFFF',abbr:'H96',tier:2},
  {name:'1. FC Köln',league:'Bundesliga 2',country:'Germany',p:'#FC4F00',s:'#FFFFFF',abbr:'KOE',tier:2},
  {name:'Kaiserslautern',league:'Bundesliga 2',country:'Germany',p:'#C8102E',s:'#FFFFFF',abbr:'FCK',tier:2},
  {name:'St. Pauli',league:'Bundesliga',country:'Germany',p:'#8B0000',s:'#FFFFFF',abbr:'STP',tier:2},
  {name:'Dynamo Dresden',league:'3. Liga',country:'Germany',p:'#FBD600',s:'#000000',abbr:'SGD',tier:1},
  // La Liga
  {name:'Real Madrid',league:'La Liga',country:'Spain',p:'#FEBE10',s:'#FFFFFF',abbr:'RMA',tier:5},
  {name:'Barcelona',league:'La Liga',country:'Spain',p:'#A50044',s:'#004D98',abbr:'BAR',tier:5},
  {name:'Atletico Madrid',league:'La Liga',country:'Spain',p:'#CB3524',s:'#FFFFFF',abbr:'ATM',tier:5},
  {name:'Sevilla',league:'La Liga',country:'Spain',p:'#D4282D',s:'#FFFFFF',abbr:'SEV',tier:4},
  {name:'Real Betis',league:'La Liga',country:'Spain',p:'#00954C',s:'#FFFFFF',abbr:'BET',tier:3},
  {name:'Athletic Bilbao',league:'La Liga',country:'Spain',p:'#EE2523',s:'#FFFFFF',abbr:'ATH',tier:3},
  {name:'Real Sociedad',league:'La Liga',country:'Spain',p:'#003DA5',s:'#FFFFFF',abbr:'RSO',tier:3},
  {name:'Valencia',league:'La Liga',country:'Spain',p:'#FE6600',s:'#FFFFFF',abbr:'VAL',tier:3},
  {name:'Villarreal',league:'La Liga',country:'Spain',p:'#F7D000',s:'#009900',abbr:'VIL',tier:3},
  {name:'Celta Vigo',league:'La Liga',country:'Spain',p:'#97C0DB',s:'#FFFFFF',abbr:'CEL',tier:2},
  {name:'Espanyol',league:'La Liga',country:'Spain',p:'#002D62',s:'#FFFFFF',abbr:'ESP',tier:2},
  {name:'Malaga',league:'La Liga 2',country:'Spain',p:'#003DA5',s:'#FFFFFF',abbr:'MAL',tier:2},
  {name:'Sporting Gijon',league:'La Liga 2',country:'Spain',p:'#CC0000',s:'#FFFFFF',abbr:'SPG',tier:2},
  // Serie A
  {name:'Inter Milan',league:'Serie A',country:'Italy',p:'#010E80',s:'#000000',abbr:'INT',tier:5},
  {name:'AC Milan',league:'Serie A',country:'Italy',p:'#FB090B',s:'#000000',abbr:'ACM',tier:5},
  {name:'Juventus',league:'Serie A',country:'Italy',p:'#000000',s:'#FFFFFF',abbr:'JUV',tier:5},
  {name:'Napoli',league:'Serie A',country:'Italy',p:'#12A0C3',s:'#FFFFFF',abbr:'NAP',tier:4},
  {name:'AS Roma',league:'Serie A',country:'Italy',p:'#8B0000',s:'#F7A600',abbr:'ROM',tier:4},
  {name:'Lazio',league:'Serie A',country:'Italy',p:'#9BCEE4',s:'#FFFFFF',abbr:'LAZ',tier:4},
  {name:'Atalanta',league:'Serie A',country:'Italy',p:'#1E3888',s:'#000000',abbr:'ATA',tier:4},
  {name:'Fiorentina',league:'Serie A',country:'Italy',p:'#4B0082',s:'#FFFFFF',abbr:'FIO',tier:3},
  {name:'Torino',league:'Serie A',country:'Italy',p:'#8B0000',s:'#FFFFFF',abbr:'TOR',tier:3},
  {name:'Bologna',league:'Serie A',country:'Italy',p:'#CC0000',s:'#0000CC',abbr:'BOL',tier:3},
  {name:'Hellas Verona',league:'Serie A',country:'Italy',p:'#FFD700',s:'#003DA5',abbr:'HEL',tier:2},
  {name:'Sampdoria',league:'Serie B',country:'Italy',p:'#003DA5',s:'#FFFFFF',abbr:'SAM',tier:2},
  {name:'Parma',league:'Serie A',country:'Italy',p:'#FFF200',s:'#003DA5',abbr:'PAR',tier:3},
  // Ligue 1
  {name:'Paris Saint Germain',league:'Ligue 1',country:'France',p:'#004170',s:'#DA291C',abbr:'PSG',tier:5},
  {name:'Olympique Marseille',league:'Ligue 1',country:'France',p:'#009BD8',s:'#FFFFFF',abbr:'OM',tier:4},
  {name:'Olympique Lyonnais',league:'Ligue 1',country:'France',p:'#0046AD',s:'#FFFFFF',abbr:'OL',tier:4},
  {name:'AS Monaco',league:'Ligue 1',country:'France',p:'#D4021D',s:'#FFFFFF',abbr:'ASM',tier:4},
  {name:'Lille OSC',league:'Ligue 1',country:'France',p:'#DA291C',s:'#003DA5',abbr:'LOS',tier:3},
  {name:'Nice',league:'Ligue 1',country:'France',p:'#CC0000',s:'#000000',abbr:'OGC',tier:3},
  {name:'Nantes',league:'Ligue 1',country:'France',p:'#F7D000',s:'#119728',abbr:'FCN',tier:2},
  {name:'Saint Etienne',league:'Ligue 1',country:'France',p:'#119728',s:'#FFFFFF',abbr:'ASS',tier:2},
  // Eredivisie
  {name:'Ajax',league:'Eredivisie',country:'Netherlands',p:'#CC0000',s:'#FFFFFF',abbr:'AFC',tier:4},
  {name:'PSV Eindhoven',league:'Eredivisie',country:'Netherlands',p:'#CC0000',s:'#FFFFFF',abbr:'PSV',tier:4},
  {name:'Feyenoord',league:'Eredivisie',country:'Netherlands',p:'#CC0000',s:'#FFFFFF',abbr:'FEY',tier:4},
  {name:'AZ Alkmaar',league:'Eredivisie',country:'Netherlands',p:'#CC0000',s:'#FFFFFF',abbr:'AZA',tier:3},
  {name:'FC Twente',league:'Eredivisie',country:'Netherlands',p:'#CC0000',s:'#FFFFFF',abbr:'FCT',tier:3},
  // Portugal
  {name:'Benfica',league:'Primeira Liga',country:'Portugal',p:'#CC0000',s:'#FFFFFF',abbr:'SLB',tier:4},
  {name:'FC Porto',league:'Primeira Liga',country:'Portugal',p:'#003DA5',s:'#FFFFFF',abbr:'FCP',tier:4},
  {name:'Sporting Lisbon',league:'Primeira Liga',country:'Portugal',p:'#119728',s:'#FFFFFF',abbr:'SCP',tier:4},
  // Scotland
  {name:'Celtic FC',league:'Scottish Prem',country:'Scotland',p:'#119728',s:'#FFFFFF',abbr:'CEL',tier:3},
  {name:'Rangers',league:'Scottish Prem',country:'Scotland',p:'#003DA5',s:'#FFFFFF',abbr:'RAN',tier:3},
  // Turkey
  {name:'Galatasaray',league:'Süper Lig',country:'Turkey',p:'#CC0000',s:'#FFD700',abbr:'GS',tier:4},
  {name:'Fenerbahce',league:'Süper Lig',country:'Turkey',p:'#003DA5',s:'#FFD700',abbr:'FB',tier:3},
  {name:'Besiktas',league:'Süper Lig',country:'Turkey',p:'#000000',s:'#FFFFFF',abbr:'BJK',tier:3},
  // South America
  {name:'River Plate',league:'Argentine Primera',country:'Argentina',p:'#CC0000',s:'#FFFFFF',abbr:'RIV',tier:4},
  {name:'Boca Juniors',league:'Argentine Primera',country:'Argentina',p:'#003DA5',s:'#FFD700',abbr:'BOC',tier:4},
  {name:'Flamengo',league:'Brasileirão',country:'Brazil',p:'#CC0000',s:'#000000',abbr:'FLA',tier:4},
  {name:'Corinthians',league:'Brasileirão',country:'Brazil',p:'#000000',s:'#FFFFFF',abbr:'SCO',tier:3},
  {name:'Santos FC',league:'Brasileirão',country:'Brazil',p:'#FFFFFF',s:'#000000',abbr:'SAN',tier:3},
  {name:'Sao Paulo',league:'Brasileirão',country:'Brazil',p:'#CC0000',s:'#FFFFFF',abbr:'SAO',tier:3},
  {name:'Club America',league:'Liga MX',country:'Mexico',p:'#FFD700',s:'#003DA5',abbr:'AME',tier:3},
  // MLS
  {name:'New York City FC',league:'MLS',country:'USA',p:'#6CABDD',s:'#FFFFFF',abbr:'NYC',tier:2},
  {name:'LA Galaxy',league:'MLS',country:'USA',p:'#00245D',s:'#FFFFFF',abbr:'LAG',tier:2},
  {name:'Chicago Fire',league:'MLS',country:'USA',p:'#CC0000',s:'#FFFFFF',abbr:'CHI',tier:2},
  {name:'Toronto FC',league:'MLS',country:'Canada',p:'#CC0000',s:'#FFFFFF',abbr:'TOR',tier:2},
  // Saudi
  {name:'Al-Hilal',league:'Saudi Pro League',country:'Saudi Arabia',p:'#003DA5',s:'#FFFFFF',abbr:'ALH',tier:3},
  {name:'Al-Nassr',league:'Saudi Pro League',country:'Saudi Arabia',p:'#FFD700',s:'#003DA5',abbr:'ALN',tier:3},
  {name:'Al-Ittihad',league:'Saudi Pro League',country:'Saudi Arabia',p:'#000000',s:'#FFD700',abbr:'ALI',tier:3},
];

const HAIR_STYLES=['Short Fade','Buzz Cut','Textured Crop','Curly Top','Afro','Spiked Dreads','Cornrows','Slick Back','Quiff','Mohawk','Side Part','Long Flow'];
const SKIN_TONES=['#FDBCB4','#F1C27D','#E0AC69','#C68642','#8D5524','#4A2912'];
const HAIR_COLS=['#1a1a1a','#3B2314','#7B3F00','#C09A6B','#D4A017','#F0E0A0','#808080','#CC0000','#4B0082'];
const KIT_COLS=['#CC0000','#003DA5','#119728','#000000','#FFFFFF','#FFD700','#8B0082','#FF8C00'];
const BOOT_COLS=['#CC0000','#FFD700','#119728','#003DA5','#FFFFFF','#000000','#FF69B4','#FF8C00'];

// Premade models
const MODELS=[
  {id:'euro',name:'European',skin:SKIN_TONES[1],hair:'Short Fade',hairCol:HAIR_COLS[0],kit:KIT_COLS[0],boot:BOOT_COLS[0]},
  {id:'afro',name:'African',skin:SKIN_TONES[4],hair:'Afro',hairCol:HAIR_COLS[0],kit:KIT_COLS[1],boot:BOOT_COLS[1]},
  {id:'latin',name:'Latin',skin:SKIN_TONES[2],hair:'Textured Crop',hairCol:HAIR_COLS[1],kit:KIT_COLS[2],boot:BOOT_COLS[0]},
  {id:'dreads',name:'Dreads',skin:SKIN_TONES[3],hair:'Spiked Dreads',hairCol:HAIR_COLS[0],kit:KIT_COLS[3],boot:BOOT_COLS[3]},
  {id:'nordic',name:'Nordic',skin:SKIN_TONES[0],hair:'Slick Back',hairCol:HAIR_COLS[5],kit:KIT_COLS[1],boot:BOOT_COLS[4]},
  {id:'quiff',name:'Quiff',skin:SKIN_TONES[1],hair:'Quiff',hairCol:HAIR_COLS[2],kit:KIT_COLS[0],boot:BOOT_COLS[1]},
  {id:'corn',name:'Cornrows',skin:SKIN_TONES[3],hair:'Cornrows',hairCol:HAIR_COLS[0],kit:KIT_COLS[4],boot:BOOT_COLS[0]},
  {id:'mohk',name:'Mohawk',skin:SKIN_TONES[1],hair:'Mohawk',hairCol:HAIR_COLS[6],kit:KIT_COLS[5],boot:BOOT_COLS[7]},
];

// Competition calendar (matchdays in season)
const COMP_CALENDAR={
  'FA Cup':       {icon:'🏆',md_start:10,md_end:42,country:'England'},
  'Carabao Cup':  {icon:'🥛',md_start:2,md_end:28,country:'England'},
  'Community Shield':{icon:'🛡️',md_start:0,md_end:0,country:'England'},
  'Champions League':{icon:'⭐',md_start:6,md_end:38,country:'Europe',minLeaguePos:4},
  'Europa League':{icon:'🌙',md_start:6,md_end:38,country:'Europe',minLeaguePos:7},
  'Conference League':{icon:'🌐',md_start:6,md_end:38,country:'Europe',minLeaguePos:10},
  'Club World Cup':{icon:'🌍',md_start:0,md_end:0,country:'International'},
  'DFB Pokal':    {icon:'🏆',md_start:6,md_end:36,country:'Germany'},
  'Copa del Rey': {icon:'👑',md_start:8,md_end:38,country:'Spain'},
  'Coppa Italia': {icon:'🏆',md_start:6,md_end:36,country:'Italy'},
  'Coupe de France':{icon:'🇫🇷',md_start:8,md_end:34,country:'France'},
};

// ══════════════════════════════════════════════════════════════
// STATE
// ══════════════════════════════════════════════════════════════
let career=null;
let wizStep=1;
let selFoot='right';
let selArch=null;
let selAcad=null;
let selClub=null;
let activeLeagueTab='ALL';
let selModel='euro';
let av={skin:SKIN_TONES[1],hair:'Short Fade',hairCol:HAIR_COLS[0],kit:KIT_COLS[0],boot:BOOT_COLS[0]};
let matchState=null;
let pitchBalls=[]; // animated balls on pitch
let pitchAnim=null;

function rng(a,b){return Math.floor(Math.random()*(b-a+1))+a;}
function save(){try{localStorage.setItem('fl_v3',JSON.stringify({career,av}));}catch(e){}}
function load(){try{const d=localStorage.getItem('fl_v3');if(d){const p=JSON.parse(d);career=p.career;if(p.av)av={...av,...p.av};}}catch(e){}}

// ══════════════════════════════════════════════════════════════
// AVATAR DRAWING — realistic 2D solid figures
// ══════════════════════════════════════════════════════════════
function drawPlayer(canvas,cfg,mini=false){
  const ctx=canvas.getContext('2d');
  const W=canvas.width,H=canvas.height;
  ctx.clearRect(0,0,W,H);
  const cx=W/2;
  const skin=cfg.skin||SKIN_TONES[1];
  const hairCol=cfg.hairCol||HAIR_COLS[0];
  const kit=cfg.kit||'#CC0000';
  const boot=cfg.boot||'#000000';
  const hs=cfg.hair||'Short Fade';
  const sc=darken(skin,20);

  const s=(sz)=>mini?sz*0.7:sz; // scale helper

  // === BOOTS ===
  ctx.fillStyle=boot;
  roundRect(ctx,cx-s(17),H-s(24),s(14),s(10),s(4));ctx.fill();
  roundRect(ctx,cx+s(3),H-s(24),s(14),s(10),s(4));ctx.fill();
  ctx.fillStyle='rgba(255,255,255,0.25)';
  ctx.fillRect(cx-s(17),H-s(24),s(6),s(3));
  ctx.fillRect(cx+s(3),H-s(24),s(6),s(3));

  // === SOCKS ===
  ctx.fillStyle='#fff';
  ctx.fillRect(cx-s(17),H-s(34),s(14),s(12));
  ctx.fillRect(cx+s(3),H-s(34),s(14),s(12));
  // Sock detail
  ctx.fillStyle='rgba(0,0,0,0.1)';
  ctx.fillRect(cx-s(17),H-s(28),s(14),s(2));
  ctx.fillRect(cx+s(3),H-s(28),s(14),s(2));

  // === SKIN — LOWER LEGS ===
  ctx.fillStyle=skin;
  ctx.fillRect(cx-s(16),H-s(42),s(12),s(10));
  ctx.fillRect(cx+s(4),H-s(42),s(12),s(10));

  // === SHORTS ===
  const kitDark=darken(kit,25);
  ctx.fillStyle=kit;
  roundRect(ctx,cx-s(18),H*0.54,s(15),H*0.18,s(3));ctx.fill();
  roundRect(ctx,cx+s(3),H*0.54,s(15),H*0.18,s(3));ctx.fill();
  // Shorts highlight
  ctx.fillStyle='rgba(255,255,255,0.1)';
  ctx.fillRect(cx-s(18),H*0.54,s(6),H*0.06);
  ctx.fillRect(cx+s(3),H*0.54,s(6),H*0.06);

  // === TORSO/SHIRT ===
  ctx.fillStyle=kit;
  // Main body shape
  ctx.beginPath();
  ctx.moveTo(cx-s(20),H*0.54);
  ctx.bezierCurveTo(cx-s(22),H*0.44,cx-s(24),H*0.34,cx-s(20),H*0.28);
  ctx.lineTo(cx+s(20),H*0.28);
  ctx.bezierCurveTo(cx+s(24),H*0.34,cx+s(22),H*0.44,cx+s(20),H*0.54);
  ctx.closePath();ctx.fill();
  // Shirt highlight
  ctx.fillStyle='rgba(255,255,255,0.08)';
  ctx.beginPath();
  ctx.moveTo(cx-s(10),H*0.28);ctx.bezierCurveTo(cx-s(12),H*0.34,cx-s(12),H*0.42,cx-s(8),H*0.5);
  ctx.lineTo(cx,H*0.5);ctx.lineTo(cx,H*0.28);ctx.closePath();ctx.fill();
  // Number badge
  ctx.fillStyle='rgba(255,255,255,0.2)';
  ctx.beginPath();ctx.ellipse(cx,H*0.4,s(8),s(8),0,0,Math.PI*2);ctx.fill();

  // === COLLAR ===
  ctx.fillStyle=darken(kit,30);
  ctx.beginPath();ctx.ellipse(cx,H*0.28,s(6),s(4),0,0,Math.PI*2);ctx.fill();
  ctx.fillStyle='rgba(255,255,255,0.3)';
  ctx.beginPath();ctx.ellipse(cx,H*0.27,s(3),s(2),0,0,Math.PI*2);ctx.fill();

  // === ARMS ===
  ctx.fillStyle=kit;
  // Left arm
  ctx.beginPath();
  ctx.moveTo(cx-s(20),H*0.29);
  ctx.bezierCurveTo(cx-s(28),H*0.32,cx-s(32),H*0.4,cx-s(30),H*0.5);
  ctx.bezierCurveTo(cx-s(28),H*0.52,cx-s(24),H*0.52,cx-s(22),H*0.5);
  ctx.bezierCurveTo(cx-s(22),H*0.42,cx-s(22),H*0.33,cx-s(18),H*0.3);
  ctx.closePath();ctx.fill();
  // Right arm
  ctx.beginPath();
  ctx.moveTo(cx+s(20),H*0.29);
  ctx.bezierCurveTo(cx+s(28),H*0.32,cx+s(32),H*0.4,cx+s(30),H*0.5);
  ctx.bezierCurveTo(cx+s(28),H*0.52,cx+s(24),H*0.52,cx+s(22),H*0.5);
  ctx.bezierCurveTo(cx+s(22),H*0.42,cx+s(22),H*0.33,cx+s(18),H*0.3);
  ctx.closePath();ctx.fill();

  // === HANDS ===
  ctx.fillStyle=skin;
  ctx.beginPath();ctx.ellipse(cx-s(28),H*0.51,s(5),s(6),0.2,0,Math.PI*2);ctx.fill();
  ctx.beginPath();ctx.ellipse(cx+s(28),H*0.51,s(5),s(6),-0.2,0,Math.PI*2);ctx.fill();

  // === NECK ===
  ctx.fillStyle=skin;
  ctx.fillRect(cx-s(5),H*0.23,s(10),H*0.07);

  // === HEAD ===
  ctx.fillStyle=skin;
  ctx.beginPath();ctx.ellipse(cx,H*0.165,s(17),s(20),0,0,Math.PI*2);ctx.fill();
  // Head shading
  ctx.fillStyle='rgba(0,0,0,0.07)';
  ctx.beginPath();ctx.ellipse(cx+s(4),H*0.19,s(10),s(14),0.2,0,Math.PI*2);ctx.fill();

  // === EARS ===
  ctx.fillStyle=skin;
  ctx.beginPath();ctx.ellipse(cx-s(17),H*0.165,s(4.5),s(6.5),0,0,Math.PI*2);ctx.fill();
  ctx.fillStyle=sc;ctx.beginPath();ctx.ellipse(cx-s(17),H*0.165,s(2.5),s(4),0,0,Math.PI*2);ctx.fill();
  ctx.fillStyle=skin;
  ctx.beginPath();ctx.ellipse(cx+s(17),H*0.165,s(4.5),s(6.5),0,0,Math.PI*2);ctx.fill();
  ctx.fillStyle=sc;ctx.beginPath();ctx.ellipse(cx+s(17),H*0.165,s(2.5),s(4),0,0,Math.PI*2);ctx.fill();

  // === HAIR ===
  drawHair(ctx,cx,H,hs,hairCol,s);

  // === EYES ===
  ctx.fillStyle='#fff';
  ctx.beginPath();ctx.ellipse(cx-s(5.5),H*0.148,s(4.5),s(3.2),0,0,Math.PI*2);ctx.fill();
  ctx.beginPath();ctx.ellipse(cx+s(5.5),H*0.148,s(4.5),s(3.2),0,0,Math.PI*2);ctx.fill();
  const irisCol=skin<'#C'?'#3D2B1F':'#1a1a2e';
  ctx.fillStyle=irisCol;
  ctx.beginPath();ctx.arc(cx-s(5.5),H*0.15,s(2.5),0,Math.PI*2);ctx.fill();
  ctx.beginPath();ctx.arc(cx+s(5.5),H*0.15,s(2.5),0,Math.PI*2);ctx.fill();
  ctx.fillStyle='#000';
  ctx.beginPath();ctx.arc(cx-s(5.5),H*0.15,s(1.4),0,Math.PI*2);ctx.fill();
  ctx.beginPath();ctx.arc(cx+s(5.5),H*0.15,s(1.4),0,Math.PI*2);ctx.fill();
  ctx.fillStyle='rgba(255,255,255,0.75)';
  ctx.beginPath();ctx.arc(cx-s(4.5),H*0.146,s(0.9),0,Math.PI*2);ctx.fill();
  ctx.beginPath();ctx.arc(cx+s(6.5),H*0.146,s(0.9),0,Math.PI*2);ctx.fill();
  // Eyelids
  ctx.strokeStyle='rgba(0,0,0,0.5)';ctx.lineWidth=s(1);ctx.lineCap='round';
  ctx.beginPath();ctx.moveTo(cx-s(10),H*0.146);ctx.quadraticCurveTo(cx-s(5.5),H*0.138,cx-s(1),H*0.146);ctx.stroke();
  ctx.beginPath();ctx.moveTo(cx+s(1),H*0.146);ctx.quadraticCurveTo(cx+s(5.5),H*0.138,cx+s(10),H*0.146);ctx.stroke();

  // === EYEBROWS ===
  ctx.strokeStyle=hairCol;ctx.lineWidth=s(1.8);ctx.lineCap='round';
  ctx.beginPath();ctx.moveTo(cx-s(10),H*0.126);ctx.quadraticCurveTo(cx-s(5.5),H*0.118,cx-s(1),H*0.123);ctx.stroke();
  ctx.beginPath();ctx.moveTo(cx+s(1),H*0.123);ctx.quadraticCurveTo(cx+s(5.5),H*0.118,cx+s(10),H*0.126);ctx.stroke();

  // === NOSE ===
  ctx.strokeStyle=sc;ctx.lineWidth=s(1.2);ctx.fillStyle=sc;
  ctx.beginPath();ctx.moveTo(cx,H*0.155);ctx.quadraticCurveTo(cx-s(2.5),H*0.175,cx-s(2),H*0.182);ctx.stroke();
  ctx.beginPath();ctx.moveTo(cx,H*0.155);ctx.quadraticCurveTo(cx+s(2.5),H*0.175,cx+s(2),H*0.182);ctx.stroke();
  ctx.fillStyle=darken(skin,35);
  ctx.beginPath();ctx.ellipse(cx-s(2.8),H*0.182,s(2),s(1.5),-0.3,0,Math.PI*2);ctx.fill();
  ctx.beginPath();ctx.ellipse(cx+s(2.8),H*0.182,s(2),s(1.5),0.3,0,Math.PI*2);ctx.fill();

  // === MOUTH ===
  ctx.strokeStyle=darken(skin,42);ctx.lineWidth=s(1.4);
  ctx.beginPath();ctx.moveTo(cx-s(4.5),H*0.197);ctx.quadraticCurveTo(cx,H*0.205,cx+s(4.5),H*0.197);ctx.stroke();
  ctx.fillStyle=darken(skin,10);
  ctx.beginPath();ctx.ellipse(cx,H*0.207,s(3),s(1.6),0,0,Math.PI);ctx.fill();
}

function drawHair(ctx,cx,H,style,col,s){
  // Pre-compute colors once — no random inside draw loop
  const dark=darken(col,24);
  const vdark=darken(col,45);
  const hi='rgba(255,255,255,0.14)';
  ctx.fillStyle=col;

  if(style==='Short Fade'){
    // Smooth bezier cap
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(20),H*0.09,cx-s(7),H*0.048,cx,H*0.044);
    ctx.bezierCurveTo(cx+s(7),H*0.048,cx+s(20),H*0.09,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Soft fade on sides using gradient
    const gL=ctx.createLinearGradient(cx-s(17),0,cx-s(5),0);
    gL.addColorStop(0,'rgba(0,0,0,0)');gL.addColorStop(1,col+'cc');
    ctx.fillStyle=gL;ctx.fillRect(cx-s(17),H*0.11,s(12),H*0.05);ctx.fillStyle=col;
    const gR=ctx.createLinearGradient(cx+s(5),0,cx+s(17),0);
    gR.addColorStop(0,col+'cc');gR.addColorStop(1,'rgba(0,0,0,0)');
    ctx.fillStyle=gR;ctx.fillRect(cx+s(5),H*0.11,s(12),H*0.05);ctx.fillStyle=col;
    // Sheen highlight
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx-s(2),H*0.079,s(7),s(3.5),-0.3,0,Math.PI*2);ctx.fill();

  } else if(style==='Buzz Cut'){
    // Solid smooth stubble cap — NO random, smooth ellipse with texture lines
    ctx.beginPath();ctx.ellipse(cx,H*0.1,s(17),s(12),0,0,Math.PI*2);ctx.fill();
    // Fine lines suggest short hair texture
    ctx.strokeStyle=dark;ctx.lineWidth=s(0.8);
    for(let i=-4;i<=4;i++){
      const lx=cx+s(i*3.5);
      ctx.beginPath();ctx.moveTo(lx,H*0.052);ctx.lineTo(lx+s(0.5),H*0.1);ctx.stroke();
    }
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx-s(3),H*0.08,s(6),s(3),-0.2,0,Math.PI*2);ctx.fill();

  } else if(style==='Textured Crop'){
    // Clean base
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(19),H*0.085,cx-s(6),H*0.042,cx,H*0.04);
    ctx.bezierCurveTo(cx+s(6),H*0.042,cx+s(19),H*0.085,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Smooth texture strands — bezier strokes only
    ctx.strokeStyle=dark;ctx.lineWidth=s(2.2);ctx.lineCap='round';
    for(let i=-4;i<=4;i++){
      const tx=cx+s(i*2.6);
      ctx.beginPath();ctx.moveTo(tx,H*0.05);ctx.bezierCurveTo(tx+s(1),H*0.07,tx-s(0.5),H*0.09,tx+s(0.5),H*0.105);ctx.stroke();
    }
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx,H*0.068,s(5),s(2.5),0,0,Math.PI*2);ctx.fill();

  } else if(style==='Curly Top'){
    // Base cap
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(19),H*0.1,cx-s(10),H*0.07,cx,H*0.065);
    ctx.bezierCurveTo(cx+s(10),H*0.07,cx+s(19),H*0.1,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Chunky smooth curls on top
    const cXs=[cx-s(11),cx-s(5.5),cx,cx+s(5.5),cx+s(11)];
    cXs.forEach((bx,i)=>{
      ctx.fillStyle=i%2===0?col:dark;
      ctx.beginPath();ctx.arc(bx,H*0.054+Math.sin(i*1.2)*H*0.008,s(5.8),0,Math.PI*2);ctx.fill();
    });
    // Dark ring details
    ctx.fillStyle=vdark;
    cXs.forEach((bx,i)=>{
      ctx.beginPath();ctx.arc(bx+s(1.5),H*0.05+Math.sin(i*1.2)*H*0.008,s(2.2),0,Math.PI*2);ctx.fill();
    });

  } else if(style==='Afro'){
    // Smooth cloud silhouette
    ctx.beginPath();
    ctx.moveTo(cx,H*0.02);
    ctx.bezierCurveTo(cx+s(6),H*0.015,cx+s(14),H*0.03,cx+s(19),H*0.062);
    ctx.bezierCurveTo(cx+s(23),H*0.095,cx+s(22),H*0.13,cx+s(17),H*0.155);
    ctx.lineTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(22),H*0.13,cx-s(23),H*0.095,cx-s(19),H*0.062);
    ctx.bezierCurveTo(cx-s(14),H*0.03,cx-s(6),H*0.015,cx,H*0.02);
    ctx.closePath();ctx.fill();
    // Smooth depth blobs — fixed positions, no random
    ctx.fillStyle=dark;
    [[cx-s(10),H*0.045,s(5)],[cx+s(8),H*0.038,s(6)],[cx-s(2),H*0.03,s(5)],
     [cx+s(16),H*0.09,s(4)],[cx-s(15),H*0.1,s(4)]].forEach(([x,y,r])=>{
      ctx.beginPath();ctx.arc(x,y,r,0,Math.PI*2);ctx.fill();
    });
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx-s(3),H*0.065,s(8),s(4),-0.2,0,Math.PI*2);ctx.fill();

  } else if(style==='Spiked Dreads'||style==='Dreadlocks'){
    // === SPIKED DREADS — upward spikes, never cover face ===
    // Tight base cap
    ctx.fillStyle=col;
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(18),H*0.1,cx-s(6),H*0.055,cx,H*0.052);
    ctx.bezierCurveTo(cx+s(6),H*0.055,cx+s(18),H*0.1,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Spiked dreads — angled UPWARD and outward, never forward over face
    var spikeData=[
      // [baseX offset, baseY, tipX offset, tipY, width, colorAlt]
      [-s(14), H*0.09, -s(22), H*0.01, s(4.5), false],
      [-s(9),  H*0.07, -s(16), H*0.0,  s(4.5), true],
      [-s(4),  H*0.06, -s(7),  H*-0.01, s(4),  false],
      [s(0),   H*0.055, s(1),  H*-0.02, s(3.8), true],
      [s(4),   H*0.06, s(7),   H*-0.01, s(4),  false],
      [s(9),   H*0.07, s(16),  H*0.0,  s(4.5), true],
      [s(14),  H*0.09, s(22),  H*0.01, s(4.5), false],
      // shorter ones between
      [-s(11.5),H*0.08, -s(18),H*0.04, s(3.5), true],
      [s(11.5), H*0.08, s(18), H*0.04, s(3.5), false],
    ];
    spikeData.forEach(function(sp){
      var bx=cx+sp[0], by=sp[1], tx=cx+sp[2], ty=sp[3], hw=sp[4], alt=sp[5];
      ctx.fillStyle=alt?dark:col;
      // Tapered spike shape
      ctx.beginPath();
      ctx.moveTo(bx-hw, by);
      ctx.quadraticCurveTo(tx-hw*0.3, (by+ty)/2, tx, ty);
      ctx.quadraticCurveTo(tx+hw*0.3, (by+ty)/2, bx+hw, by);
      ctx.closePath();
      ctx.fill();
      // Band marks on spike
      ctx.fillStyle='rgba(0,0,0,0.22)';
      var steps=3;
      for(var b=1;b<=steps;b++){
        var t=b/(steps+1);
        var mx=bx+(tx-bx)*t, my=by+(ty-by)*t;
        var mw=hw*(1-t*0.7);
        ctx.fillRect(mx-mw, my-s(0.8), mw*2, s(1.6));
      }
    });
    // Highlight on cap top
    ctx.fillStyle='rgba(255,255,255,0.12)';
    ctx.beginPath();ctx.ellipse(cx-s(2),H*0.085,s(7),s(3),-0.2,0,Math.PI*2);ctx.fill();

} else if(style==='Cornrows'){
    // Tight-cropped base
    ctx.fillStyle=col+'55';
    ctx.beginPath();ctx.ellipse(cx,H*0.1,s(17),s(10.5),0,0,Math.PI*2);ctx.fill();
    // Clean parallel braid rows
    const rowXs=[cx-s(12),cx-s(6),cx,cx+s(6),cx+s(12)];
    rowXs.forEach((rx,ri)=>{
      // Braid path
      ctx.strokeStyle=ri%2===0?col:dark;ctx.lineWidth=s(4);ctx.lineCap='round';
      ctx.beginPath();ctx.moveTo(rx,H*0.058);ctx.lineTo(rx,H*0.155);ctx.stroke();
      // Over-under weave marks
      ctx.strokeStyle=vdark;ctx.lineWidth=s(1.2);
      for(let k=0;k<8;k++){
        ctx.beginPath();
        ctx.moveTo(rx-s(2),H*0.062+k*H*0.012);
        ctx.bezierCurveTo(rx,H*0.066+k*H*0.012,rx,H*0.066+k*H*0.012,rx+s(2),H*0.062+k*H*0.012);
        ctx.stroke();
      }
    });

  } else if(style==='Slick Back'){
    // Smooth swept-back shape
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(16),H*0.12,cx-s(14),H*0.08,cx-s(5),H*0.055);
    ctx.bezierCurveTo(cx+s(4),H*0.05,cx+s(14),H*0.07,cx+s(17),H*0.11);
    ctx.bezierCurveTo(cx+s(18),H*0.13,cx+s(17),H*0.155,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Comb lines following direction
    ctx.strokeStyle=dark;ctx.lineWidth=s(1);ctx.lineCap='round';
    for(let i=0;i<6;i++){
      const t=i/5;
      const y1=H*(0.06+t*0.04);const y2=H*(0.08+t*0.04);
      ctx.beginPath();ctx.moveTo(cx-s(12+t*4),y1);ctx.bezierCurveTo(cx-s(2),y1+H*0.01,cx+s(8),y2-H*0.01,cx+s(15),y2);ctx.stroke();
    }
    // Glossy highlight
    ctx.fillStyle='rgba(255,255,255,0.18)';
    ctx.beginPath();ctx.moveTo(cx-s(8),H*0.065);ctx.bezierCurveTo(cx,H*0.052,cx+s(10),H*0.065,cx+s(12),H*0.08);ctx.lineTo(cx+s(8),H*0.088);ctx.bezierCurveTo(cx,H*0.074,cx-s(5),H*0.078,cx-s(4),H*0.085);ctx.closePath();ctx.fill();

  } else if(style==='Quiff'){
    // Base sides
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(19),H*0.1,cx-s(14),H*0.075,cx-s(7),H*0.07);
    ctx.lineTo(cx+s(7),H*0.07);
    ctx.bezierCurveTo(cx+s(14),H*0.075,cx+s(19),H*0.1,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Quiff volume — prominent smooth mound
    ctx.beginPath();
    ctx.moveTo(cx-s(8),H*0.072);
    ctx.bezierCurveTo(cx-s(7),H*0.025,cx+s(7),H*0.025,cx+s(8),H*0.072);
    ctx.bezierCurveTo(cx+s(4),H*0.066,cx-s(4),H*0.066,cx-s(8),H*0.072);
    ctx.closePath();ctx.fill();
    // Shadow crease on quiff
    ctx.fillStyle=dark;
    ctx.beginPath();ctx.moveTo(cx-s(5),H*0.062);ctx.bezierCurveTo(cx,H*0.04,cx+s(5),H*0.062,cx+s(3),H*0.065);ctx.bezierCurveTo(cx,H*0.048,cx-s(3),H*0.065,cx-s(5),H*0.062);ctx.closePath();ctx.fill();
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx-s(1),H*0.045,s(4),s(2),-0.2,0,Math.PI*2);ctx.fill();

  } else if(style==='Mohawk'){
    // Shaved sides — semi-transparent
    ctx.fillStyle=col+'33';
    ctx.beginPath();ctx.ellipse(cx,H*0.11,s(17),s(10),0,0,Math.PI*2);ctx.fill();
    // The strip — clean rectangle with rounded top
    ctx.fillStyle=col;
    roundRect(ctx,cx-s(5),H*0.03,s(10),H*0.13,s(4));ctx.fill();
    // Shadow crease down centre
    ctx.fillStyle=dark;
    roundRect(ctx,cx-s(1.5),H*0.03,s(3),H*0.13,s(1));ctx.fill();
    // Highlight
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx-s(2),H*0.065,s(3),s(6),0,0,Math.PI*2);ctx.fill();

  } else if(style==='Side Part'){
    // Main cap
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(19),H*0.09,cx-s(8),H*0.048,cx-s(2),H*0.046);
    ctx.bezierCurveTo(cx+s(6),H*0.048,cx+s(19),H*0.09,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Part line — clean
    ctx.strokeStyle=vdark;ctx.lineWidth=s(1.5);ctx.lineCap='butt';
    ctx.beginPath();ctx.moveTo(cx-s(2),H*0.048);ctx.lineTo(cx-s(3),H*0.15);ctx.stroke();
    // Comb direction
    ctx.strokeStyle=dark;ctx.lineWidth=s(1);
    for(let i=0;i<5;i++){
      ctx.beginPath();ctx.moveTo(cx-s(1)+s(i*3),H*0.06+i*H*0.012);ctx.lineTo(cx+s(10),H*0.07+i*H*0.012);ctx.stroke();
    }
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx+s(4),H*0.08,s(6),s(2.5),0.1,0,Math.PI*2);ctx.fill();

  } else if(style==='Long Flow'){
    // Head cap
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.155);
    ctx.bezierCurveTo(cx-s(19),H*0.085,cx-s(6),H*0.042,cx,H*0.04);
    ctx.bezierCurveTo(cx+s(6),H*0.042,cx+s(19),H*0.085,cx+s(17),H*0.155);
    ctx.closePath();ctx.fill();
    // Long flowing sides — smooth bezier
    ctx.beginPath();
    ctx.moveTo(cx-s(17),H*0.14);
    ctx.bezierCurveTo(cx-s(21),H*0.22,cx-s(22),H*0.38,cx-s(18),H*0.56);
    ctx.lineTo(cx-s(12),H*0.56);
    ctx.bezierCurveTo(cx-s(16),H*0.38,cx-s(15),H*0.22,cx-s(13),H*0.14);
    ctx.closePath();ctx.fill();
    ctx.beginPath();
    ctx.moveTo(cx+s(17),H*0.14);
    ctx.bezierCurveTo(cx+s(21),H*0.22,cx+s(22),H*0.38,cx+s(18),H*0.56);
    ctx.lineTo(cx+s(12),H*0.56);
    ctx.bezierCurveTo(cx+s(16),H*0.38,cx+s(15),H*0.22,cx+s(13),H*0.14);
    ctx.closePath();ctx.fill();
    // Centre parting stripe
    ctx.fillStyle=dark;ctx.fillRect(cx-s(1.5),H*0.04,s(3),H*0.12);
    ctx.fillStyle=hi;ctx.beginPath();ctx.ellipse(cx-s(2),H*0.075,s(6),s(2.5),-0.2,0,Math.PI*2);ctx.fill();
  }
}

function roundRect(ctx,x,y,w,h,r){ctx.beginPath();ctx.moveTo(x+r,y);ctx.lineTo(x+w-r,y);ctx.quadraticCurveTo(x+w,y,x+w,y+r);ctx.lineTo(x+w,y+h-r);ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);ctx.lineTo(x+r,y+h);ctx.quadraticCurveTo(x,y+h,x,y+h-r);ctx.lineTo(x,y+r);ctx.quadraticCurveTo(x,y,x+r,y);ctx.closePath();}
function darken(hex,a){const r=Math.max(0,parseInt((hex||'#888888').slice(1,3)||'88',16)-a),g=Math.max(0,parseInt((hex||'#888888').slice(3,5)||'88',16)-a),b=Math.max(0,parseInt((hex||'#888888').slice(5,7)||'88',16)-a);return '#'+[r,g,b].map(v=>v.toString(16).padStart(2,'0')).join('');}
function isLight(h){const r=parseInt((h||'#000').slice(1,3),16),g=parseInt((h||'#000').slice(3,5),16),b=parseInt((h||'#000').slice(5,7),16);return(r*299+g*587+b*114)/1000>140;}

function redrawAll(){
  ['playerCanvas','careerCanvas','profileCanvas'].forEach(id=>{const c=document.getElementById(id);if(c)drawPlayer(c,av,id!=='playerCanvas');});
}

// ══════════════════════════════════════════════════════════════
// PITCH CANVAS ANIMATION
// ══════════════════════════════════════════════════════════════
function drawPitch(canvas,state){
  const ctx=canvas.getContext('2d');
  const W=canvas.width=canvas.offsetWidth||500;
  const H=canvas.height;
  // Pitch surface
  ctx.fillStyle='#1d4a1d';ctx.fillRect(0,0,W,H);
  // Stripes
  for(let i=0;i<8;i++){ctx.fillStyle=i%2===0?'#204e20':'#1d4a1d';ctx.fillRect(i*(W/8),0,W/8,H);}
  // Lines
  ctx.strokeStyle='rgba(255,255,255,0.6)';ctx.lineWidth=2;
  // Perimeter
  ctx.strokeRect(12,8,W-24,H-16);
  // Halfway
  ctx.beginPath();ctx.moveTo(W/2,8);ctx.lineTo(W/2,H-8);ctx.stroke();
  // Centre circle
  ctx.beginPath();ctx.arc(W/2,H/2,40,0,Math.PI*2);ctx.stroke();
  ctx.fillStyle='rgba(255,255,255,0.6)';ctx.beginPath();ctx.arc(W/2,H/2,3,0,Math.PI*2);ctx.fill();
  // Left penalty box
  ctx.strokeRect(12,H/2-50,80,100);ctx.strokeRect(12,H/2-28,40,56);
  ctx.beginPath();ctx.arc(92,H/2,30,Math.PI*0.75,Math.PI*1.25);ctx.stroke();
  // Right penalty box
  ctx.strokeRect(W-92,H/2-50,80,100);ctx.strokeRect(W-52,H/2-28,40,56);
  ctx.beginPath();ctx.arc(W-92,H/2,30,-Math.PI*0.25,Math.PI*0.25);ctx.stroke();
  // Corner arcs
  [[14,10],[W-14,10],[14,H-10],[W-14,H-10]].forEach(([x,y])=>{ctx.beginPath();ctx.arc(x,y,8,0,Math.PI/2*((x>W/2?-1:1)+(y>H/2?2:0)+1));ctx.stroke();});

  if(!state)return;
  // Draw player dot (you)
  ctx.fillStyle='#00e5ff';ctx.shadowColor='#00e5ff';ctx.shadowBlur=10;
  ctx.beginPath();ctx.arc(state.px,state.py,8,0,Math.PI*2);ctx.fill();
  ctx.shadowBlur=0;
  // Draw opponents
  ctx.fillStyle='#ff3b5c';
  (state.opp||[]).forEach(o=>{ctx.beginPath();ctx.arc(o.x,o.y,6,0,Math.PI*2);ctx.fill();});
  // Draw teammates
  ctx.fillStyle='#2ecc71';
  (state.team||[]).forEach(t=>{ctx.beginPath();ctx.arc(t.x,t.y,6,0,Math.PI*2);ctx.fill();});
  // Ball
  if(state.ball){
    ctx.fillStyle='#fff';ctx.beginPath();ctx.arc(state.ball.x,state.ball.y,6,0,Math.PI*2);ctx.fill();
    ctx.strokeStyle='#ccc';ctx.lineWidth=1;ctx.stroke();
  }
}

// ══════════════════════════════════════════════════════════════
// WIZARD
// ══════════════════════════════════════════════════════════════
function updateWizProg(){
  const el=document.getElementById('wizProg');el.innerHTML='';
  for(let i=1;i<=5;i++){const d=document.createElement('div');d.className='wdot'+(i<wizStep?' done':i===wizStep?' act':'');el.appendChild(d);}
}

function wizNext(){
  if(wizStep===1){
    if(!document.getElementById('firstName').value.trim()||!document.getElementById('lastName').value.trim()){toast('Enter your full name!','r');return;}
  }
  if(wizStep===3&&!selArch){toast('Choose a play style!','r');return;}
  if(wizStep===4&&!selAcad){toast('Choose your academy!','r');return;}
  document.getElementById(`step-${wizStep}`).classList.remove('active');
  wizStep++;
  document.getElementById(`step-${wizStep}`).classList.add('active');
  updateWizProg();
  if(wizStep===2)initAvatarBuilder();
  if(wizStep===3)renderArchs();
  if(wizStep===4)renderAcads();
  if(wizStep===5){renderLeagueTabs();renderClubs();}
}
function wizBack(){
  if(wizStep<=1)return;
  document.getElementById(`step-${wizStep}`).classList.remove('active');
  wizStep--;
  document.getElementById(`step-${wizStep}`).classList.add('active');
  updateWizProg();
}

// Foot picker
document.querySelectorAll('[data-foot]').forEach(el=>{
  el.addEventListener('click',()=>{
    document.querySelectorAll('[data-foot]').forEach(x=>x.classList.remove('sel'));
    el.classList.add('sel');selFoot=el.dataset.foot;
  });
});

// AVATAR BUILDER
function initAvatarBuilder(){
  // Premade models
  const mg=document.getElementById('modelGrid');mg.innerHTML='';
  MODELS.forEach(m=>{
    const el=document.createElement('div');el.className='model-card'+(selModel===m.id?' sel':'');
    const c=document.createElement('canvas');c.width=80;c.height=110;c.style.borderRadius='6px';
    drawPlayer(c,m,true);
    el.appendChild(c);
    const nm=document.createElement('div');nm.className='mn';nm.textContent=m.name;el.appendChild(nm);
    el.addEventListener('click',()=>{
      selModel=m.id;av={...m};
      document.querySelectorAll('.model-card').forEach(x=>x.classList.remove('sel'));el.classList.add('sel');
      syncAvatarControls();redrawAll();
    });
    mg.appendChild(el);
  });
  initControls();redrawAll();
}

function initControls(){
  mkSwatches('skinRow',SKIN_TONES,'skin');
  mkSwatches('hairColorRow',HAIR_COLS,'hairCol');
  mkGear('hairStyleRow',HAIR_STYLES,'hair');
  mkSwatches('kitRow',KIT_COLS,'kit');
  mkSwatches('bootRow',BOOT_COLS,'boot');
}
function syncAvatarControls(){
  ['skinRow','hairColorRow','kitRow','bootRow'].forEach(id=>{const row=document.getElementById(id);if(row)row.querySelectorAll('.sw').forEach(s=>s.classList.remove('sel'));});
  document.getElementById('hairStyleRow')?.querySelectorAll('.gBtn').forEach(b=>b.classList.remove('sel'));
  initControls();
}
function mkSwatches(id,arr,key){
  const row=document.getElementById(id);if(!row)return;row.innerHTML='';
  arr.forEach(c=>{
    const s=document.createElement('div');s.className='sw'+(av[key]===c?' sel':'');
    s.style.background=c;if(c==='#FFFFFF')s.style.border='2px solid #aaa';
    s.addEventListener('click',()=>{av[key]=c;row.querySelectorAll('.sw').forEach(x=>x.classList.remove('sel'));s.classList.add('sel');redrawAll();});
    row.appendChild(s);
  });
}
function mkGear(id,arr,key){
  const row=document.getElementById(id);if(!row)return;row.innerHTML='';
  arr.forEach(o=>{
    const b=document.createElement('button');b.className='gBtn'+(av[key]===o?' sel':'');b.textContent=o;
    b.addEventListener('click',()=>{av[key]=o;row.querySelectorAll('.gBtn').forEach(x=>x.classList.remove('sel'));b.classList.add('sel');redrawAll();});
    row.appendChild(b);
  });
}

// ARCHETYPES
function renderArchs(){
  const pos=document.getElementById('posSel').value;
  const grid=document.getElementById('archGrid');grid.innerHTML='';
  ARCHETYPES.forEach(a=>{
    const card=document.createElement('div');card.className='cp'+(selArch===a.id?' sel':'');
    card.innerHTML=`<div class="cpi">${a.icon}</div><div class="cpn">${a.name}</div><div class="cps">${a.desc}</div>`;
    card.addEventListener('click',()=>{
      selArch=a.id;document.querySelectorAll('#archGrid .cp').forEach(x=>x.classList.remove('sel'));card.classList.add('sel');
      renderStatPrev();
    });
    grid.appendChild(card);
  });
}

function renderStatPrev(){
  const a=ARCHETYPES.find(x=>x.id===selArch);if(!a)return;
  const ps=PLAYSTYLES_DEF[a.playstyle];
  const prev=document.getElementById('statPrev');
  prev.innerHTML=`<div class="ph">Base Stats + PlayStyle</div>
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;background:var(--s2);border:1px solid var(--gold2);border-radius:6px;padding:10px;">
      <span style="font-size:1.6rem;">${ps?.icon||'⚽'}</span>
      <div><div style="font-family:'Oswald',sans-serif;font-size:1rem;color:var(--gold);">${ps?.name||''} <span style="font-family:'DM Mono',monospace;font-size:.6rem;color:var(--cyan);">${ps?.plus||''}</span></div><div style="font-size:.72rem;color:var(--muted);">${ps?.desc||''}</div></div>
    </div>
    ${Object.entries(a.stats).map(([k,v])=>`<div class="sr"><div class="sl">${k}</div><div class="sb"><div class="sf gd" style="width:${v}%"></div></div><div class="sv">${v}</div></div>`).join('')}`;
}

// ACADEMIES
function renderAcads(){
  const grid=document.getElementById('acadGrid');grid.innerHTML='';
  ACADEMIES.forEach(a=>{
    const card=document.createElement('div');card.className='cp'+(selAcad===a.id?' sel':'');
    card.innerHTML=`<div class="cpi">${a.icon}</div><div class="cpn">${a.name}</div><div class="cps">${a.club}<br>${a.desc}</div>`;
    card.addEventListener('click',()=>{selAcad=a.id;document.querySelectorAll('#acadGrid .cp').forEach(x=>x.classList.remove('sel'));card.classList.add('sel');});
    grid.appendChild(card);
  });
}

// CLUBS
function renderLeagueTabs(){
  const leagues=['ALL',...new Set(CLUBS.map(c=>c.league)).values()].sort();
  const tabs=document.getElementById('leagueTabs');tabs.innerHTML='';
  leagues.forEach(l=>{const b=document.createElement('button');b.className='ltab'+(activeLeagueTab===l?' sel':'');b.textContent=l;b.addEventListener('click',()=>{activeLeagueTab=l;renderLeagueTabs();renderClubs();});tabs.appendChild(b);});
  document.getElementById('clubSearch').oninput=()=>renderClubs();
}
function renderClubs(){
  const q=(document.getElementById('clubSearch')?.value||'').toLowerCase();
  const grid=document.getElementById('clubGrid');
  const filtered=CLUBS.filter(c=>(activeLeagueTab==='ALL'||c.league===activeLeagueTab)&&(!q||c.name.toLowerCase().includes(q)||c.league.toLowerCase().includes(q)));
  grid.innerHTML=filtered.map(c=>`<div class="club-card${selClub===c.name?' sel':''}" onclick="selectClub('${c.name.replace(/'/g,"\\'")}')">
    <div class="cbadge" style="background:${c.p};color:${isLight(c.p)?'#000':'#fff'};">${c.abbr}</div>
    <div><div class="cn">${c.name}</div><div class="cl">${c.league}</div></div>
  </div>`).join('');
}
function selectClub(n){selClub=n;renderClubs();}

// ══════════════════════════════════════════════════════════════
// BEGIN CAREER
// ══════════════════════════════════════════════════════════════
function buildStats(archId,acadId,pos){
  const arch=ARCHETYPES.find(a=>a.id===archId)||ARCHETYPES[0];
  const acad=ACADEMIES.find(a=>a.id===acadId)||ACADEMIES[0];
  const isGK=pos==='GK';
  let stats={};
  if(isGK){
    GK_STATS.forEach(k=>stats[k]=rng(55,70));
  } else {
    OUTFIELD_STATS.forEach(k=>{
      const grp=Object.entries(STAT_GROUPS).find(([g,arr])=>arr.includes(k));
      const grpName=grp?grp[0]:'technical';
      // Map archetype simple stats to full attribute groups
      const archMap={pace:['acceleration','sprint_speed'],shooting:['finishing','shot_power','long_shots','positioning','volleys','penalties','free_kick'],passing:['short_passing','long_passing','vision','crossing'],dribbling:['dribbling','ball_control','agility','balance','reactions','curve'],defending:['defensive_awareness','interceptions','sliding_tackle','standing_tackle'],physical:['strength','stamina','jumping','aggression','composure']};
      let base=58;
      for(const[cat,keys] of Object.entries(archMap)){if(keys.includes(k)&&arch.stats[cat]){base=arch.stats[cat]+rng(-6,4);break;}}
      // Academy boost
      if(acad.boost[k])base+=acad.boost[k];
      stats[k]=Math.min(99,Math.max(40,base));
    });
  }
  return stats;
}

function calcOvr(stats,pos){
  const isGK=pos==='GK';
  if(isGK)return Math.round(Object.values(stats).reduce((a,b)=>a+b,0)/GK_STATS.length);
  const weights={pace:1.2,shooting:1.1,passing:1.1,dribbling:1.0,defending:0.8,physical:1.0};
  let tot=0,w=0;
  const archMap={pace:['acceleration','sprint_speed'],shooting:['finishing','shot_power','long_shots','positioning'],passing:['short_passing','long_passing','vision','crossing'],dribbling:['dribbling','ball_control','agility'],defending:['defensive_awareness','interceptions','sliding_tackle','standing_tackle'],physical:['strength','stamina','jumping']};
  for(const[cat,keys] of Object.entries(archMap)){
    const wt=weights[cat]||1;
    const vals=keys.map(k=>stats[k]||60);
    const avg=vals.reduce((a,b)=>a+b,0)/vals.length;
    tot+=avg*wt;w+=wt;
  }
  return Math.round(tot/w);
}

function calcSalary(tier,ovr){
  const p=SALARY_TIERS[tier]||SALARY_TIERS[2];
  const pct=(ovr-50)/50;
  const base=p.min+pct*(p.max-p.min);
  return Math.max(p.min,Math.round(base/500)*500);
}

function buildComps(club,leaguePos=10){
  const cl=CLUBS.find(c=>c.name===club);
  const country=cl?.country||'England';
  const league=cl?.league||'Premier League';
  const tier=cl?.tier||3;
  const comps=[{id:'league',name:league,icon:'🏴',round:'Matchday 1',status:'active',md:1,W:0,D:0,L:0,GF:0,GA:0}];
  // National cups
  if(country==='England'){comps.push({id:'fa_cup',name:'FA Cup',icon:'🏆',round:'3rd Round',status:'upcoming',md:0,W:0,D:0,L:0});comps.push({id:'carabao',name:'Carabao Cup',icon:'🥛',round:'Round 1',status:'active',md:0,W:0,D:0,L:0});}
  if(country==='Germany')comps.push({id:'dfb',name:'DFB Pokal',icon:'🏆',round:'Round 1',status:'upcoming',md:0,W:0,D:0,L:0});
  if(country==='Spain')comps.push({id:'copa',name:'Copa del Rey',icon:'👑',round:'Round 1',status:'upcoming',md:0,W:0,D:0,L:0});
  if(country==='Italy')comps.push({id:'coppa',name:'Coppa Italia',icon:'🏆',round:'Round 1',status:'upcoming',md:0,W:0,D:0,L:0});
  if(country==='France')comps.push({id:'coupe',name:'Coupe de France',icon:'🇫🇷',round:'Round 1',status:'upcoming',md:0,W:0,D:0,L:0});
  // Community Shield (England, start of season)
  if(country==='England'&&tier>=4)comps.push({id:'cs',name:'Community Shield',icon:'🛡️',round:'Final',status:'upcoming',md:0,W:0,D:0,L:0});
  // Europe — based on tier/leaguePos
  if(tier>=4&&leaguePos<=4)comps.push({id:'ucl',name:'Champions League',icon:'⭐',round:'Group Stage',status:'upcoming',md:0,W:0,D:0,L:0});
  else if(tier>=3&&leaguePos<=7)comps.push({id:'uel',name:'Europa League',icon:'🌙',round:'Group Stage',status:'upcoming',md:0,W:0,D:0,L:0});
  else if(tier>=2&&leaguePos<=10)comps.push({id:'uecl',name:'Conference League',icon:'🌐',round:'Qualifying',status:'upcoming',md:0,W:0,D:0,L:0});
  // Club World Cup (top tier)
  if(tier>=5)comps.push({id:'cwc',name:'Club World Cup',icon:'🌍',round:'Group Stage',status:'upcoming',md:0,W:0,D:0,L:0});
  return comps;
}

function beginCareer(){
  if(!selClub){toast('Choose a club!','r');return;}
  const fn=document.getElementById('firstName').value.trim();
  const ln=document.getElementById('lastName').value.trim();
  const arch=ARCHETYPES.find(a=>a.id===selArch)||ARCHETYPES[4];
  const acad=ACADEMIES.find(a=>a.id===selAcad)||ACADEMIES[0];
  const club=CLUBS.find(c=>c.name===selClub)||CLUBS[0];
  const pos=document.getElementById('posSel').value;
  const age=parseInt(document.getElementById('startAge').value)||18;
  const nat=document.getElementById('natSel').value;
  const ht=parseInt(document.getElementById('heightSel').value)||175;
  const body=document.getElementById('bodySel').value;
  const stats=buildStats(arch.id,acad.id,pos);
  const ovr=calcOvr(stats,pos);
  const leagueTot=LEAGUE_FIXTURES[club.league]||38;
  const pres=LEAGUE_PRESTIGE[club.league]||2;
  const salary=calcSalary(pres,ovr);

  career={
    firstName:fn,lastName:ln,name:`${fn} ${ln}`,
    pos,age,nat,height:ht,body,foot:selFoot,
    archetype:arch.id,academy:acad.id,
    club:club.name,league:club.league,
    stats,ovr,sp:3,xp:0,level:1,
    salary,
    season:1,year:2025,
    goals:0,assists:0,apps:0,
    seasonGoals:0,seasonAssists:0,seasonApps:0,
    managerFavor:50,
    history:[],trophies:[],achievements:[],
    offers:[],
    comps:buildComps(club.name),
    leaguePos:10,
    leagueTotal:leagueTot,
    matchdayLeft:leagueTot,
    loan:false,loanClub:null,
    retirementAge:45,
    playstyle:arch.playstyle,
    additionalPS:[acad.ps],
  };
  career.clubManager=MANAGER_NAMES[rng(0,MANAGER_NAMES.length-1)];
  career.agentName=MANAGER_NAMES[rng(0,MANAGER_NAMES.length-1)];
  while(career.agentName===career.clubManager)career.agentName=MANAGER_NAMES[rng(0,MANAGER_NAMES.length-1)];
  career.contractEnd=career.year+3;
  career.leaguePos=rng(8,16);
  playerFatigue=0;
  save();
  toast('Career started! Welcome to '+club.name+'!','gr');
  showScreen('career');
  setTimeout(()=>triggerCS({
    icon:'⚽',title:`Welcome to ${club.name}`,sub:'First day',
    scene:`The dressing room buzzes with chatter. Your new manager stops you in the corridor, a clipboard under his arm. "${career.name}. I've seen your work. Now I want to see you prove it on this pitch."`,
    q:'How do you respond?',
    choices:[
      {t:'Confident',s:'I\'m ready. Just give me the ball.',ef:()=>{career.managerFavor+=10;toast('+10 Manager Favor','gr');}},
      {t:'Humble',s:'I\'ll work my hardest for this club.',ef:()=>{career.managerFavor+=6;career.stats.composure=Math.min(99,(career.stats.composure||60)+3);toast('+6 Favor +3 Composure','gr');}},
      {t:'Focused',s:'*You nod and head straight to training.*',ef:()=>{career.stats.ball_control=Math.min(99,(career.stats.ball_control||60)+4);toast('+4 Ball Control','g');}},
    ]
  }),900);
}

// ══════════════════════════════════════════════════════════════
// CAREER HUB
// ══════════════════════════════════════════════════════════════
function showScreen(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  const el=document.getElementById('screen-'+id);if(el)el.classList.add('active');
  if(id==='career'){refreshCareer();checkManagerCutscenes();}
  if(id==='match')refreshMatch();
  if(id==='transfers')refreshTransfers();
  if(id==='comps')refreshComps();
  if(id==='profile')refreshProfile();
  if(id==='training')refreshTrainingDrills();
  if(id==='calendar'){refreshCalendar();if(career)document.getElementById('calSub').textContent=career.league+' Season '+career.year+'/'+(career.year+1);}
  if(id==='agent'){refreshAgent();if(career)document.getElementById('agentSub').textContent='Agent: '+(career.agentName||getManagerName());}
  if(id==='table')refreshLeagueTable();
  if(id==='menu')refreshMenu();
  if(pitchAnim&&id!=='match'){cancelAnimationFrame(pitchAnim);pitchAnim=null;}
}

function refreshCareer(){
  if(!career)return;
  const club=CLUBS.find(c=>c.name===career.club)||{p:'#333',abbr:'?'};
  const tc=isLight(club.p)?'#000':'#fff';
  document.getElementById('pbName').textContent=career.name;
  document.getElementById('pbClub').innerHTML=`<span style="background:${club.p};color:${tc};padding:2px 6px;border-radius:3px;font-family:'Oswald',sans-serif;font-size:.7rem;margin-right:5px;">${club.abbr}</span>${career.club} · ${career.league}`;
  document.getElementById('pbPills').innerHTML=`<span style="font-family:'DM Mono',monospace;font-size:.6rem;letter-spacing:1px;padding:3px 8px;border-radius:3px;border:1px solid var(--gold2);color:var(--gold);background:var(--gold3);">${career.pos}</span><span style="font-family:'DM Mono',monospace;font-size:.6rem;padding:3px 8px;border-radius:3px;border:1px solid var(--border2);color:var(--muted);">Age ${career.age}</span><span style="font-family:'DM Mono',monospace;font-size:.6rem;padding:3px 8px;border-radius:3px;border:1px solid var(--border2);color:var(--muted);">${career.nat}</span>`;
  document.getElementById('pbStats').innerHTML=`<div class="pbs"><div class="n">${career.seasonGoals}</div><div class="l">Goals</div></div><div class="pbs"><div class="n">${career.seasonAssists}</div><div class="l">Assists</div></div><div class="pbs"><div class="n">${career.seasonApps}</div><div class="l">Apps</div></div><div class="pbs"><div class="n">${career.sp}</div><div class="l">SP</div></div>`;
  document.getElementById('ovrNum').textContent=career.ovr;
  document.getElementById('sbSeason').textContent=`${career.year}/${String(career.year+1).slice(2)}`;
  document.getElementById('sbAge').textContent=career.age;
  document.getElementById('sbMatchLeft').textContent=career.matchdayLeft<=0?'Season done — End Season!':career.matchdayLeft;
  document.getElementById('sbSalary').textContent=`£${(career.salary||0).toLocaleString()}/wk`;
  const f=career.managerFavor;
  document.getElementById('favFill').style.width=f+'%';
  document.getElementById('favFill').style.background=f>65?'var(--green)':f>35?'var(--gold)':'var(--red)';
  document.getElementById('favLabel').textContent=f>75?'🟢 Trusted Star':f>50?'🟡 Good Books':f>30?'🟠 Fringe':'🔴 Falling Out';
  document.getElementById('champBanner').style.display=career.trophies.length?'block':'none';
  const cc=document.getElementById('careerCanvas');if(cc)drawPlayer(cc,av,true);
  var offerBadge=career.offers.length?'<div class="ndot"></div>':'';
  var simLeft=career.matchdayLeft;
  var gridHTML='';
  var gridItems=[
    ['match','⚽','Play Match','Matchday '+(career.seasonApps+1),true],
    ['sim','⚡','Simulate','Auto-play next match',false],
    ['training','💪','Training','Earn SP · Upgrade stats',false],
    ['transfers','💰','Transfers',career.offers.length+' offer(s)',career.offers.length>0],
    ['agent','🤵','Agent','Contracts · Loans',false],
    ['calendar','📅','Calendar','Season fixtures',false],
    ['table','📊','League Table','Pos: #'+career.leaguePos,false],
    ['comps','🏆','Competitions',(career.comps||[]).length+' active',false],
    ['profile','🎖️','Profile','Stats & playstyles',false],
    ['endsz','🔄','End Season',simLeft+' games left',false],
  ];
  gridItems.forEach(function(item){
    var id=item[0];var ic=item[1];var ct=item[2];var cd=item[3];var dot=item[4];
    var onclick=id==='sim'?'simulateMatchFromHub()':id==='endsz'?'nextSeason()':"showScreen('"+id+"')";
    gridHTML+='<div class="cc" onclick="'+onclick+'"><div class="ci">'+ic+'</div><div class="ct">'+ct+'</div><div class="cd">'+cd+'</div>'+(dot?'<div class="ndot"></div>':'')+'</div>';
  });
  document.getElementById('careerGrid').innerHTML=gridHTML;  '';
}
function xpNeeded(l){return 100+(l-1)*60;}

// ══════════════════════════════════════════════════════════════
// MATCH ENGINE WITH DECISIONS & PITCH
// ══════════════════════════════════════════════════════════════
function refreshMatch(){
  if(!career)return;
  const club=CLUBS.find(c=>c.name===career.club)||{p:'#333',abbr:'?',s:'#fff'};
  const opponents=CLUBS.filter(c=>c.league===career.league&&c.name!==career.club);
  const opp=opponents[rng(0,opponents.length-1)]||CLUBS[0];
  const home=Math.random()>.5;
  matchState={opp,home,yourScore:0,oppScore:0,minute:0,log:[],played:false,pendingDecision:false,decisionCount:0,goals:0,assists:0,rating:6.0};
  document.getElementById('matchCompBar').textContent=`${career.league} — Matchday ${career.seasonApps+1} of ${career.leagueTotal}`;
  renderMatchHeader(club,opp,home,0,0);
  document.getElementById('elog').innerHTML='';
  document.getElementById('decisionPanel').style.display='none';
  drawPitch(document.getElementById('pitchCanvas'),null);
  document.getElementById('matchActs').innerHTML=`
    <button class="mact primary" onclick="startMatch()">▶ Kick Off</button>
    <button class="mact secondary" onclick="showScreen('career')">← Hub</button>`;
}

function renderMatchHeader(club,opp,home,ys,os){
  const a=home?club:opp,b=home?opp:club;
  const taA=isLight(a.p)?'#000':'#fff',taB=isLight(b.p)?'#000':'#fff';
  const min=matchState?matchState.minute:0;
  document.getElementById('matchHeader').innerHTML=`
    <div class="mh-team">
      <div class="mh-badge" style="background:${a.p};color:${taA};">${a.abbr}</div>
      <div class="mh-name">${a.name}</div>
    </div>
    <div class="mh-cen">
      <div class="score-disp">${ys} – ${os}</div>
      <div class="match-minute">${min>0?min+"'":'PRE-MATCH'}</div>
      <div class="comp-tag">${career.league} ${home?'· HOME':'· AWAY'}</div>
    </div>
    <div class="mh-team right">
      <div class="mh-badge" style="background:${b.p};color:${taB};">${b.abbr}</div>
      <div class="mh-name">${b.name}</div>
    </div>`;
}

function startMatch(isCup){
  if(matchState)matchState.isCup=isCup||false;
  document.getElementById('matchActs').innerHTML='<button class="mact danger" onclick="abandonMatch()">Abandon Match</button>';
  if(career&&career.seasonApps===0&&!career.firstMatchDone){
    triggerFirstMatchCS();
    setTimeout(runMatchMinutes, 400);
  } else {
    runMatchMinutes();
  }
}

function abandonMatch(){
  if(matchState)matchState.played=true;
  if(window._decisionCallback){window._decisionCallback=null;window._currentSit=null;}
  document.getElementById('decisionPanel').style.display='none';
  showScreen('career');
}

function runMatchMinutes(){
  if(!matchState||matchState.played)return;
  // Key moment minutes spread across a real 90min match
  const allMinutes=[4,8,12,16,20,24,28,31,34,37,40,44,45,
    48,52,56,60,63,67,70,73,76,79,82,85,88,90];
  const isCup=matchState.isCup||false;
  // League: 6-8 decisions. Cup/Trophy: 12-15 decisions (every big moment)
  const totalDecisions=isCup?rng(12,15):rng(6,8);
  const shuffled=[...allMinutes].sort(()=>Math.random()-0.5);
  matchState.pendingDecisions=new Set(shuffled.slice(0,totalDecisions));
  matchState.gameMinuteIdx=0;
  runNextMinute();
}

function runNextMinute(){
  if(!matchState||matchState.played)return;
  const allMinutes=[1,3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,
    47,49,51,53,55,57,59,61,63,65,67,69,71,73,75,77,79,81,83,85,87,89,90];
  const idx=matchState.gameMinuteIdx;
  if(idx>=allMinutes.length){endMatch();return;}
  const minute=allMinutes[idx];
  matchState.minute=minute;
  const club=CLUBS.find(c=>c.name===career.club)||{p:'#333',abbr:'?'};
  renderMatchHeader(club,matchState.opp,matchState.home,matchState.yourScore,matchState.oppScore);
  // Update pitch
  updatePitchFrame(minute);
  // Background events — balanced so player isn't punished passively
  const r=Math.random();
  const oppStrength=matchState.opp.tier||2;
  const playerStr=career.ovr||60;
  const oppGoalChance=0.04+(oppStrength*0.01)-(playerStr*0.001);
  const yourGoalChance=0.05+(playerStr*0.001)-(oppStrength*0.01);
  if(r<Math.max(0.02,oppGoalChance)){
    matchState.oppScore++;
    logEv('⚽ '+minute+"' — "+matchState.opp.name+' score from a set piece!','r');
    matchState.rating=Math.max(3,matchState.rating-0.1);
    renderMatchHeader(club,matchState.opp,matchState.home,matchState.yourScore,matchState.oppScore);
  } else if(r<Math.max(0.02,oppGoalChance)+Math.max(0.02,yourGoalChance)){
    matchState.yourScore++;
    matchState.rating=Math.min(10,matchState.rating+0.15);
    logEv('⚽ '+minute+"' — "+career.club+' GOAL! Great team move!','g');
    renderMatchHeader(club,matchState.opp,matchState.home,matchState.yourScore,matchState.oppScore);
  } else if(r<0.22){
    logEv(minute+"' — "+matchState.opp.name+' win a corner. Pressure building.','n');
  } else if(r<0.30){
    logEv(minute+"' — "+career.club+' work the ball forward. Good build-up.','n');
    matchState.rating=Math.min(10,matchState.rating+0.05);
  } else if(r<0.36){
    logEv(minute+"' — Free kick "+career.club+'. Good position.','n');
  }
  // Halftime break
  if(minute===45&&idx<allMinutes.length-1){
    logEv('--- HALF TIME: '+career.club+' '+matchState.yourScore+' – '+matchState.oppScore+' '+matchState.opp.name+' ---','e');
  }
  // Check if this minute has a decision
  if(matchState.pendingDecisions&&matchState.pendingDecisions.has(minute)){
    triggerDecision(minute, idx, ()=>{
      matchState.gameMinuteIdx++;
      setTimeout(runNextMinute, 220);
    });
    return; // pause tick until player decides
  }
  matchState.gameMinuteIdx++;
  setTimeout(runNextMinute, 120);
}

function updatePitchFrame(minute){
  const canvas=document.getElementById('pitchCanvas');
  if(!canvas)return;
  const W=canvas.offsetWidth||500;const H=220;
  const progress=minute/90;
  const pitchState={
    px: W*(0.15+progress*0.3+Math.sin(minute)*0.12),
    py: H*(0.2+Math.cos(minute*0.7)*0.35+0.3),
    ball:{x:W*(0.1+Math.random()*0.8), y:H*(0.15+Math.random()*0.7)},
    opp:Array.from({length:4},(_,i)=>({x:W*(0.5+Math.random()*0.45),y:H*(0.1+i*0.2+Math.random()*0.1)})),
    team:Array.from({length:3},(_,i)=>({x:W*(0.1+Math.random()*0.4),y:H*(0.15+i*0.22+Math.random()*0.1)})),
  };
  drawPitch(canvas,pitchState);
}

function triggerDecision(minute, sitIdx, onChoiceMade){
  const arch=ARCHETYPES.find(a=>a.id===career.archetype)||ARCHETYPES[4];
  const stats=career.stats;
  const situations=buildSituations(arch,stats);
  const sit=situations[rng(0,situations.length-1)];
  // Store current situation globally so makeDecision can access it
  window._currentSit=sit;
  window._decisionCallback=onChoiceMade;
  const panel=document.getElementById('decisionPanel');
  panel.style.display='block';
  // Build choices HTML without nested template literals
  let choicesHTML='';
  for(let ci=0;ci<sit.choices.length;ci++){
    const c=sit.choices[ci];
    const cls=c.outcome==='great'?'outcome-great':c.outcome==='ok'?'outcome-ok':'outcome-poor';
    const risk=c.outcome==='great'?'HIGH RISK':c.outcome==='ok'?'MED RISK':'LOW RISK';
    choicesHTML+='<div class="dp-choice" onclick="makeDecision('+ci+')">'+
      '<div><div class="dct">'+c.label+'</div><div class="dcs">'+c.desc+'</div></div>'+
      '<span class="dco '+cls+'">'+risk+'</span></div>';
  }
  panel.innerHTML=
    '<div class="dp-title">⚡ '+minute+"' — Decision Time</div>"+
    '<div class="dp-situation">'+sit.situation+'</div>'+
    '<div class="dp-choices">'+choicesHTML+'</div>';
}

window.makeDecision=function(ci){
  const sit=window._currentSit;
  const cb=window._decisionCallback;
  window._currentSit=null;window._decisionCallback=null;
  const panel=document.getElementById('decisionPanel');
  panel.style.display='none';
  if(!sit||!sit.choices[ci])return;
  const choice=sit.choices[ci];
  const result=resolveDecisionOutcome(choice);
  logEv('Decision: '+choice.label+' → '+result.msg,result.type);
  if(result.goal){matchState.yourScore++;matchState.goals++;matchState.rating+=0.6;
    const club=CLUBS.find(c=>c.name===career.club)||{p:'#333',abbr:'?'};
    renderMatchHeader(club,matchState.opp,matchState.home,matchState.yourScore,matchState.oppScore);
    logEv('⚽ GOAL! '+career.name+' scores!','e');
  }
  if(result.assist){matchState.assists++;matchState.rating+=0.35;logEv('🎯 ASSIST! Teammate finishes!','e');}
  if(result.miss)logEv('😤 Chance wasted — shot goes wide.','r');
  if(result.foul)logEv('🟡 Foul conceded — referee books you!','r');
  if(cb)cb();
}

function resolveDecisionOutcome(choice){
  const r=Math.random();
  if(choice.outcome==='great'){
    if(r<0.45){matchState.rating=Math.min(10,matchState.rating+0.5);return{msg:'Brilliant execution!',type:'g',goal:choice.action==='shoot',assist:choice.action==='pass'};}
    if(r<0.75){matchState.rating=Math.min(10,matchState.rating+0.2);return{msg:'Good play, held possession.',type:'n'};}
    matchState.rating=Math.max(3,matchState.rating-0.1);return{msg:'Overambitious — possession lost.',type:'r'};
  }
  if(choice.outcome==='ok'){
    if(r<0.38){matchState.rating=Math.min(10,matchState.rating+0.35);return{msg:'Well played!',type:'g',goal:choice.action==='shoot',assist:choice.action==='pass'};}
    if(r<0.72){matchState.rating=Math.min(10,matchState.rating+0.1);return{msg:'Safe option — team resets.',type:'n'};}
    matchState.rating=Math.max(3,matchState.rating-0.15);return{msg:'Poor execution — pressure mounts.',type:'r'};
  }
  // poor outcome choice
  if(r<0.20){matchState.rating=Math.min(10,matchState.rating+0.4);return{msg:'Against all odds — it worked!',type:'g',goal:choice.action==='shoot'};}
  if(r<0.52){matchState.rating=Math.max(3,matchState.rating-0.1);return{msg:'Predictable — snuffed out.',type:'n'};}
  matchState.rating=Math.max(3,matchState.rating-0.35);return{msg:'Costly mistake! Opposition break!',type:'r',foul:Math.random()<0.3};
}

function buildSituations(arch,stats){
  const pace=(stats.acceleration||60);
  const finish=(stats.finishing||60);
  const drbl=(stats.dribbling||60);
  const pass=(stats.short_passing||60);
  const vision=(stats.vision||60);
  const comp=(stats.composure||60);
  const lpass=(stats.long_passing||60);
  const inter=(stats.interceptions||60);
  const defw=(stats.defensive_awareness||60);
  const cross=(stats.crossing||60);
  const shot=(stats.shot_power||60);
  const head=(stats.heading||60);
  const bal=(stats.balance||60);
  const str=(stats.strength||60);

  const situations=[
    // 1. Intercept + run
    {situation:'You win the ball in midfield and burst forward. Your striker is making a run to the right — closely tracked. Your winger is free wide left. You have pace ('+pace+') but your finishing is '+finish+'. What do you do?',
     choices:[
      {label:'A. Through ball — Striker right',desc:'Thread it into space where the striker will run. (Vision '+vision+')',action:'pass',outcome:vision>72?'great':'ok'},
      {label:'B. Drive forward and shoot',desc:'Use your pace ('+pace+') and try to finish ('+finish+').',action:'shoot',outcome:finish>78?'great':finish>65?'ok':'poor'},
      {label:'C. Switch play — Left winger',desc:'Spread it wide to the free winger.',action:'pass',outcome:'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 2. 1v1 with keeper
    {situation:'You beat the last defender and are in on goal. 1v1 with the keeper rushing out. (Finishing: '+finish+' | Dribbling: '+drbl+' | Composure: '+comp+')',
     choices:[
      {label:'A. Chip the keeper',desc:'Delicate lob over the rushing GK. High risk, high reward.',action:'shoot',outcome:(finish>80&&comp>75)?'great':'ok'},
      {label:'B. Shoot low to far post',desc:'Driven low shot — keeper diving.',action:'shoot',outcome:shot>74?'great':'ok'},
      {label:'C. Cut inside — create angle',desc:'Take one more touch before shooting (Dribbling '+drbl+').',action:'dribble',outcome:drbl>78?'great':'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 3. Pressed in own half
    {situation:'You receive under pressure in your own half. CB is free left. Striker has run in behind the line. (Short pass: '+pass+' | Long pass: '+lpass+' | Vision: '+vision+')',
     choices:[
      {label:'A. Long ball — striker run',desc:'Launch over the top. (Long Pass: '+lpass+')',action:'pass',outcome:lpass>74?'great':'ok'},
      {label:'B. Short back to CB',desc:'Reset and build again. Safe option.',action:'pass',outcome:'ok'},
      {label:'C. Dribble through the press',desc:'Hold off the pressure (Dribble: '+drbl+' | Balance: '+bal+').',action:'dribble',outcome:(drbl>78&&bal>70)?'great':drbl>65?'ok':'poor'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 4. Corner kick delivery
    {situation:'Corner kick. You are taking it. Three teammates are in the box making runs — tall striker at near post, fast attacker at far post, midfielder ghosting in from outside the box. (Crossing: '+cross+' | Vision: '+vision+')',
     choices:[
      {label:'A. Near post — flick-on',desc:'Inswing to the near post for a flick. (Cross: '+cross+')',action:'pass',outcome:cross>75?'great':'ok'},
      {label:'B. Far post — flight',desc:'Float to the far post for the free runner.',action:'pass',outcome:vision>72?'great':'ok'},
      {label:'C. Short corner — build up',desc:'Play short and work a better angle.',action:'pass',outcome:'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 5. Free kick 25 yards
    {situation:'Free kick 25 yards from goal. Wall up. You can see the top corner. (Shot Power: '+shot+' | Curve: '+(stats.curve||60)+' | Free Kick: '+(stats.free_kick||60)+')',
     choices:[
      {label:'A. Curl top corner',desc:'Bend it over the wall and into the top corner.',action:'shoot',outcome:((stats.curve||60)>74&&(stats.free_kick||60)>74)?'great':'ok'},
      {label:'B. Blast through the wall',desc:'Pure power at the wall — try to go through or under.',action:'shoot',outcome:shot>78?'great':'ok'},
      {label:'C. Dummy — let teammate run',desc:'Dummied over for a teammate to strike.',action:'pass',outcome:vision>70?'great':'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 6. Counter attack 3v2
    {situation:'3v2 counter attack. You have the ball in the middle. Right runner is ahead of their defender. Left runner is level. You could go alone. (Vision: '+vision+' | Sprint: '+pace+' | Pass: '+pass+')',
     choices:[
      {label:'A. Right run — give and go',desc:'Release to the right — they are in a better position.',action:'pass',outcome:vision>70?'great':'ok'},
      {label:'B. Sprint and shoot',desc:'Use your pace ('+pace+') and go alone.',action:'shoot',outcome:(pace>82&&finish>74)?'great':'ok'},
      {label:'C. Wait — draw defenders',desc:'Hold the ball and wait for both to commit.',action:'pass',outcome:comp>72?'great':'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 7. Late tackle decision
    {situation:'Opposition striker is breaking through 1v1. You are the last defender — sliding could stop him but you might concede a penalty. (Def. Awareness: '+defw+' | Interceptions: '+inter+' | Strength: '+str+')',
     choices:[
      {label:'A. Slide tackle — clear it',desc:'Go to ground and try to win the ball clean.',action:'defend',outcome:(inter>74)?'great':'ok'},
      {label:'B. Stand off — jockey',desc:'Stay on your feet and force him wide.',action:'defend',outcome:'ok'},
      {label:'C. Foul intentionally',desc:'Take the yellow, stop the run — tactical foul.',action:'defend',outcome:'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 8. Penalty kick
    {situation:'PENALTY! You have been given a spot kick. The goalkeeper is watching your body language. (Penalties: '+(stats.penalties||60)+' | Composure: '+comp+' | Shot Power: '+shot+')',
     choices:[
      {label:'A. Wait and place it — goalkeeper dives',desc:'Read the GK dive and place opposite. High technique.',action:'shoot',outcome:((stats.penalties||60)>74&&comp>72)?'great':'ok'},
      {label:'B. Hard and down the middle',desc:'Pure power — nowhere GK can go if struck hard enough.',action:'shoot',outcome:shot>78?'great':'ok'},
      {label:'C. Panenka chip',desc:'The audacious chip down the middle.',action:'shoot',outcome:((stats.penalties||60)>85&&comp>80)?'great':'poor'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 9. Header challenge
    {situation:'Cross coming in from the right. You have made a good run to the far post. Defender is behind you. (Heading: '+head+' | Jumping: '+(stats.jumping||60)+' | Positioning: '+(stats.positioning||60)+')',
     choices:[
      {label:'A. Glance it near post',desc:'Redirect header near post — pure technique.',action:'shoot',outcome:head>74?'great':'ok'},
      {label:'B. Power header far post',desc:'Bully the defender and power it far corner.',action:'shoot',outcome:(head>70&&(stats.jumping||60)>70)?'great':'ok'},
      {label:'C. Lay it off — better angle',desc:'Nod it down for an oncoming runner.',action:'pass',outcome:vision>68?'great':'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
    // 10. Defensive header clearing
    {situation:'Opposition cross into the box. You are first to it at the edge of the six-yard box. Striker is behind you. (Heading: '+head+' | Strength: '+str+' | Defensive Awareness: '+defw+')',
     choices:[
      {label:'A. Headed clearance — distance',desc:'Get it as far as possible, row Z if needed.',action:'defend',outcome:head>68?'great':'ok'},
      {label:'B. Control and play out',desc:'Bring it down and play from the back.',action:'defend',outcome:(stats.ball_control||60)>72?'great':'ok'},
      {label:'C. Flick-on to goalkeeper',desc:'Head it back to the keeper.',action:'defend',outcome:'ok'},
      {label:randD(),desc:randDDesc(),action:pickAction(),outcome:randOutcome()},
    ]},
  ];
  return situations;
}

function pickAction(){return['shoot','pass','dribble','defend'][rng(0,3)];}
function randOutcome(){return['great','ok','poor'][rng(0,2)];}

function randD(){const opts=['D. Nutmeg the last defender','D. Attempt a rabona flick','D. Backheel to yourself','D. Shoulder barge through','D. Step over and cut inside','D. Burst into the box and improvise'];return opts[rng(0,opts.length-1)];}
function randDDesc(){const d=['A high-risk flashy move.','Unconventional but sometimes it works.','Unpredictable — could go either way.','Pure instinct, no plan.','The crowd will love it or hate it.'];return d[rng(0,d.length-1)];}

function endMatch(){
  if(!matchState)return;
  matchState.played=true;
  const won=matchState.yourScore>matchState.oppScore;
  const draw=matchState.yourScore===matchState.oppScore;
  career.goals+=matchState.goals;career.assists+=matchState.assists;
  career.apps++;career.seasonGoals+=matchState.goals;career.seasonAssists+=matchState.assists;career.seasonApps++;
  career.matchdayLeft=Math.max(0,career.matchdayLeft-1);
  // Rating-based favor
  // Rating: base from decisions + match result bonus
  const decisionBonus = matchState.goals*0.4 + matchState.assists*0.25;
  const resultBonus = won ? 0.8 : draw ? 0.2 : -0.3;
  const rat=Math.min(10,Math.max(4.5,matchState.rating + decisionBonus + resultBonus));
  if(rat>7.5)career.managerFavor=Math.min(100,career.managerFavor+6);
  else if(rat<5.5)career.managerFavor=Math.max(0,career.managerFavor-8);
  if(won)career.managerFavor=Math.min(100,career.managerFavor+rng(3,7));
  else if(!draw)career.managerFavor=Math.max(0,career.managerFavor+rng(-7,-2));
  // XP
  const xp=25+(won?20:draw?10:0)+matchState.goals*20+matchState.assists*12;
  career.xp+=xp;
  while(career.xp>=xpNeeded(career.level)){career.xp-=xpNeeded(career.level);career.level++;career.sp+=5;toast(`🎉 Level ${career.level}! +3 SP`,'g');}
  // Update comps
  const lc=career.comps.find(c=>c.id==='league');if(lc){lc.md++;lc.round=`Matchday ${lc.md}`;if(won)lc.W++;else if(draw)lc.D++;else lc.L++;lc.GF+=matchState.yourScore;lc.GA+=matchState.oppScore;}
  // Post match offer
  if(career.seasonApps>=5&&matchState.goals+matchState.assists>=4&&Math.random()<.3)generateOffer();
  save();
  const res=won?'WIN 🏆':draw?'DRAW 🤝':'DEFEAT';
  logEv(`Full Time: ${career.club} ${matchState.yourScore}–${matchState.oppScore} ${matchState.opp.name} | You: ${matchState.goals}G ${matchState.assists}A | Rating: ${rat.toFixed(1)} | ${res}`,'e');
  document.getElementById('matchActs').innerHTML=`<button class="mact primary" onclick="showScreen('career')">← Back to Hub</button><button class="mact secondary" onclick="refreshMatch();startMatch()">Next Match</button>`;
  // Post-match cutscene
  if(Math.random()<0.25){
    const cs=getPostMatchCS(won,matchState.goals,rat);
    if(cs)setTimeout(()=>triggerCS(cs),700);
  }
  // Generate Europe comp if doing well
  if(career.seasonApps>=10&&won){
    career.leaguePos=Math.max(1,career.leaguePos-1);
    if(career.leaguePos<=4&&!career.comps.find(c=>c.id==='ucl')){
      career.comps.push({id:'ucl',name:'Champions League',icon:'⭐',round:'Group Stage',status:'active',md:0,W:0,D:0,L:0});
      toast('🌟 Champions League qualification!','g');
    }
  }
}

function logEv(msg,type){
  const el=document.getElementById('elog');
  const d=document.createElement('div');d.className='elog-entry '+(type==='g'?'eg':type==='r'?'er':type==='e'?'ee':'en');
  d.textContent=msg;el.appendChild(d);el.scrollTop=el.scrollHeight;
}

// ══════════════════════════════════════════════════════════════
// POST-MATCH CUTSCENES
// ══════════════════════════════════════════════════════════════
function getPostMatchCS(won,goals,rat){
  const nm=career.firstName;
  if(goals>=2)return{icon:'🌟',title:'Brace!',sub:'Dressing room',scene:`The gaffer embraces you as you come off the pitch. "${nm}, that was something else. Two goals — exactly what this club needed." Your teammates bang the lockers in celebration.`,q:'How do you react?',choices:[
    {t:'Leader',s:'This is what we\'re capable of.',ef:()=>{career.managerFavor+=10;toast('+10 Favor','gr');}},
    {t:'Focus',s:'We take nothing for granted. Next game.',ef:()=>{career.stats.composure=Math.min(99,(career.stats.composure||60)+3);toast('+3 Composure','g');}},
  ]};
  if(!won&&rat<5.5)return{icon:'😤',title:'The Hair Dryer',sub:'Post-match debrief',scene:`Silence in the dressing room. The manager paces. "${nm}. I didn't bring you here to disappear in the big moments. That performance is not acceptable."`,q:'How do you respond?',choices:[
    {t:'Apologise',s:'You\'re right. I\'ll be better.',ef:()=>{career.managerFavor+=5;toast('+5 Favor','gr');}},
    {t:'Stand your ground',s:'The system didn\'t suit me.',ef:()=>{career.managerFavor-=10;career.stats.dribbling=Math.min(99,(career.stats.dribbling||60)+4);toast('-10 Favor but +4 Dribbling','g');}},
  ]};
  if(career.managerFavor<30)return{icon:'🚨',title:'Ultimatum',sub:'Manager\'s office',scene:`"${nm}, I'll be straight with you. You're not in my plans. There's interest from other clubs. I think a fresh start might be best for everyone."`,q:'Your decision?',choices:[
    {t:'Fight for your place',s:'I\'m not going anywhere. Watch me.',ef:()=>{career.stats.sprint_speed=Math.min(99,(career.stats.sprint_speed||60)+3);career.stats.stamina=Math.min(99,(career.stats.stamina||60)+3);toast('Chip on the shoulder: +3 Sprint +3 Stamina','g');}},
    {t:'Request a loan',s:'A fresh start would do me good.',ef:()=>{generateLoanOffer();toast('Loan offer arranged.','gr');}},
  ]};
  return null;
}

// ══════════════════════════════════════════════════════════════
// TRANSFERS
// ══════════════════════════════════════════════════════════════
function calcValue(){
  const ovr=career.ovr||60;const age=career.age||22;
  const base=Math.pow(Math.max(0,(ovr-50)/50),2.2)*80;
  const af=age<24?1.3:age<27?1.15:age<30?1:age<33?.75:.4;
  return Math.round(base*af*2)/2;
}

function generateOffer(){
  const tier=CLUBS.find(c=>c.name===career.club)?.tier||2;
  const higher=CLUBS.filter(c=>c.tier>=tier&&c.name!==career.club);
  const opp=higher[rng(0,higher.length-1)];if(!opp)return;
  const val=calcValue();
  const pres=LEAGUE_PRESTIGE[opp.league]||2;
  const salary=calcSalary(pres,career.ovr);
  const fee=Math.round((val*(0.85+Math.random()*.3))*2)/2;
  if(career.offers.find(o=>o.clubName===opp.name))return;
  career.offers.push({clubName:opp.name,league:opp.league,clubData:opp,fee,wage:salary,type:'transfer'});
  save();toast(`💰 Transfer offer from ${opp.name}!`,'g');
}

function generateLoanOffer(){
  const opp=CLUBS[rng(0,CLUBS.length-1)];
  const pres=LEAGUE_PRESTIGE[opp.league]||2;
  const salary=Math.round(calcSalary(pres,career.ovr)*0.6/500)*500;
  career.offers.push({clubName:opp.name,league:opp.league,clubData:opp,fee:0,wage:salary,type:'loan'});
  save();toast(`📋 Loan offer from ${opp.name}!`,'b');
}

function refreshTransfers(){
  if(!career)return;
  const val=calcValue();
  document.getElementById('transSub').textContent=`Market value: ~£${val}M · ${career.offers.length} offer(s)`;
  const el=document.getElementById('transContent');
  if(!career.offers.length){el.innerHTML=`<div style="text-align:center;padding:60px;font-family:'DM Mono',monospace;font-size:.75rem;color:var(--muted);">No offers yet. Perform well to attract interest.</div>`;return;}
  el.innerHTML=career.offers.map((o,i)=>{
    const cd=o.clubData||CLUBS.find(c=>c.name===o.clubName)||{p:'#333',abbr:'?'};
    const tc=isLight(cd.p)?'#000':'#fff';
    return `<div class="tc">
      <div class="tc-l">
        <div class="tc-b" style="background:${cd.p};color:${tc};">${cd.abbr||'?'}</div>
        <div><div class="tc-n">${o.clubName}</div><div class="tc-s">${o.league} · ${o.type==='loan'?'Season Loan':'Transfer'}</div><div class="tc-w">£${(o.wage||0).toLocaleString()}/wk</div></div>
      </div>
      <div class="tc-r">
        <div class="tc-fee">£${o.fee}M</div>
        <button class="act-btn acc" onclick="acceptOffer(${i})">Accept</button>
        <button class="act-btn rej" onclick="rejectOffer(${i})">Reject</button>
      </div>
    </div>`;
  }).join('');
}

function acceptOffer(i){
  const o=career.offers[i];if(!o)return;
  const cd=o.clubData||CLUBS.find(c=>c.name===o.clubName)||{p:'#333'};
  if(o.type==='loan'){
    career.loan=true;career.loanClub=o.clubName;career.loanLeague=o.league;
    toast(`Loan to ${o.clubName} confirmed.`,'gr');
  } else {
    career.club=o.clubName;career.league=o.league;
    career.salary=o.wage;career.managerFavor=50;
    career.seasonGoals=0;career.seasonAssists=0;career.seasonApps=0;
    career.matchdayLeft=LEAGUE_FIXTURES[o.league]||38;
    career.comps=buildComps(o.clubName);
    toast(`Transferred to ${o.clubName}! New chapter.`,'gr');
    triggerCS({icon:'✍️',title:`Signing Day`,sub:o.clubName,scene:`The cameras flash. A new shirt, a new city. The manager grips your hand firmly. "You're exactly what we've been missing."`,q:'Set your ambition:',choices:[
      {t:'Hungry',s:'I\'ll be your best player.',ef:()=>{career.stats.finishing=Math.min(99,(career.stats.finishing||60)+4);toast('+4 Finishing','g');}},
      {t:'Grateful',s:'This is a dream club for me.',ef:()=>{career.managerFavor+=18;toast('+18 Manager Favor','gr');}},
    ]});
  }
  career.offers.splice(i,1);save();showScreen('career');
}

function rejectOffer(i){
  career.offers.splice(i,1);career.managerFavor=Math.min(100,career.managerFavor+3);save();
  toast('Offer rejected. Manager appreciates your commitment.','g');refreshTransfers();
}

// ══════════════════════════════════════════════════════════════
// COMPETITIONS
// ══════════════════════════════════════════════════════════════
function refreshComps(){
  if(!career)return;
  document.getElementById('compSub').textContent=`${career.name} · ${career.club} · Season ${career.season}`;
  const list=document.getElementById('compList');
  list.innerHTML=(career.comps||[]).map(c=>`<div class="comp-entry">
    <div class="ce-l"><div class="ce-ic">${c.icon}</div><div><div class="ce-nm">${c.name}</div><div class="ce-rd">${c.round} · ${c.W}W ${c.D}D ${c.L}L</div></div></div>
    <div><span class="ce-st ${{active:'st-active',upcoming:'st-upcoming',won:'st-won',eliminated:'st-elim'}[c.status]||'st-upcoming'}">${c.status.toUpperCase()}</span></div>
  </div>`).join('');
}

// ══════════════════════════════════════════════════════════════
// PROFILE
// ══════════════════════════════════════════════════════════════
function refreshProfile(){
  if(!career)return;
  document.getElementById('pcName').textContent=career.name;
  document.getElementById('pcPos').textContent=career.pos;
  document.getElementById('pcClub').textContent=career.club;
  document.getElementById('pcOvr').textContent=career.ovr;
  const pc=document.getElementById('profileCanvas');if(pc)drawPlayer(pc,av,false);
  const isGK=career.pos==='GK';
  const statKeys=isGK?GK_STATS:OUTFIELD_STATS;
  document.getElementById('profileStats').innerHTML=`<div class="ph">Attributes</div>${statKeys.map(k=>`<div class="sr"><div class="sl">${STAT_LABELS[k]||k}</div><div class="sb"><div class="sf gd" style="width:${Math.min(100,career.stats[k]||0)}%"></div></div><div class="sv">${career.stats[k]||0}</div></div>`).join('')}<div class="divider"></div><div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;font-family:'DM Mono',monospace;font-size:.7rem;"><div>Goals: <b style="color:var(--gold)">${career.goals}</b></div><div>Assists: <b style="color:var(--gold)">${career.assists}</b></div><div>Apps: <b style="color:var(--gold)">${career.apps}</b></div><div>Level: <b style="color:var(--gold)">${career.level}</b></div><div>Height: <b style="color:var(--gold)">${career.height}cm</b></div><div>Salary: <b style="color:var(--gold)">£${(career.salary||0).toLocaleString()}/wk</b></div></div>`;
  const allPS=[career.playstyle,...(career.additionalPS||[])].filter(Boolean);
  document.getElementById('profilePlaystyles').innerHTML=`<div class="ph">PlayStyles</div><div class="ps-grid">${allPS.map(pid=>{const ps=PLAYSTYLES_DEF[pid];if(!ps)return '';return `<div class="ps-chip gold"><div class="psi">${ps.icon}</div><div class="psn">${ps.name}</div><div class="psd">${ps.plus}</div></div>`;}).join('')}</div>`;
  document.getElementById('profileHistory').innerHTML=`<div class="ph">Trophies & Career</div>${career.trophies.length?career.trophies.map(t=>`<div style="padding:5px 0;font-size:.83rem;">🏆 ${t}</div>`).join(''):'<div style="color:var(--muted);font-family:DM Mono,monospace;font-size:.7rem;">No trophies yet.</div>'}<div class="divider"></div>${(career.history||[]).slice(-5).reverse().map(h=>`<div style="font-size:.78rem;padding:4px 0;border-bottom:1px solid var(--border);">${h.year}/${String(h.year+1).slice(2)} · ${h.club} · ${h.goals}G ${h.assists}A · OVR ${h.ovr}</div>`).join('')}`;
}

// ══════════════════════════════════════════════════════════════
// TRAINING
// ══════════════════════════════════════════════════════════════
function refreshTraining(){refreshTrainingDrills();}

function trainStat(elOrKey){
  var k=typeof elOrKey==='string'?elOrKey:elOrKey.dataset.stat;
  if(!k)return;
  if(!career.sp||career.sp<1){toast('No SP!','r');return;}
  if((career.stats[k]||0)>=99){toast('Maxed!','r');return;}
  career.sp--;career.stats[k]=Math.min(99,(career.stats[k]||50)+rng(2,5));
  career.ovr=calcOvr(career.stats,career.pos);save();
  toast((STAT_LABELS[k]||k)+' upgraded! SP left: '+career.sp,'gr');
  refreshTraining();
}

function switchPos(elOrStr){
  var p=typeof elOrStr==='string'?elOrStr:elOrStr.dataset.pos;
  if(!p)return;
  if(career.sp<3){toast('Need 3 SP to switch position!','r');return;}
  if(p===career.pos){toast('Already playing there!','r');return;}
  career.sp-=3;
  const wasGK=career.pos==='GK';const toGK=p==='GK';
  if(!wasGK&&toGK){GK_STATS.forEach(k=>{if(!career.stats[k])career.stats[k]=55;});}
  career.pos=p;career.ovr=calcOvr(career.stats,p);save();toast(`Position changed to ${p}!`,'gr');refreshTraining();
}

// ══════════════════════════════════════════════════════════════
// NEXT SEASON
// ══════════════════════════════════════════════════════════════
function nextSeason(){
  if(!career)return;
  career.history.push({season:career.season,year:career.year,club:career.club,league:career.league,goals:career.seasonGoals,assists:career.seasonAssists,apps:career.seasonApps,ovr:career.ovr});
  career.season++;career.year++;career.age++;
  career.seasonGoals=0;career.seasonAssists=0;career.seasonApps=0;
  career.matchdayLeft=LEAGUE_FIXTURES[career.league]||38;
  career.managerFavor=Math.min(100,Math.max(20,career.managerFavor+rng(-5,12)));
  career.offers=[];
  playerFatigue=0;
  // Relegation/promotion check before season ends
  checkRelegationPromotion();
  career.comps=buildComps(career.club,career.leaguePos);
  // Natural progression / decline
  const isGK=career.pos==='GK';
  const keys=isGK?GK_STATS:OUTFIELD_STATS;
  if(career.age<25)keys.forEach(k=>{career.stats[k]=Math.min(99,(career.stats[k]||50)+rng(0,3));});
  else if(career.age<30)keys.forEach(k=>{career.stats[k]=Math.min(99,(career.stats[k]||50)+rng(0,1));});
  else if(career.age>32)keys.forEach(k=>{career.stats[k]=Math.max(30,(career.stats[k]||50)-rng(0,2));});
  career.ovr=calcOvr(career.stats,career.pos);
  // Salary renegotiation
  const pres=LEAGUE_PRESTIGE[career.league]||2;
  career.salary=calcSalary(pres,career.ovr);
  save();toast(`Season ${career.season-1} complete! Now ${career.age}. OVR ${career.ovr}. Salary £${career.salary.toLocaleString()}/wk`,'g');
  if(career.age>=45){
    triggerCS({icon:'👟',title:'Hanging Up The Boots',sub:'Career over',scene:`The empty stadium echoes as you do your last lap. ${career.goals} goals across ${career.apps} appearances. A journey that defined a generation.`,q:'Final words?',choices:[
      {t:'Graceful exit',s:'It\'s been the privilege of my life.',ef:()=>{career.trophies.push('Career Completed');save();}},
      {t:'One last year',s:'I\'ve got one more season in me.',ef:()=>{career.retirementAge+=2;career.age-=1;toast('Career extended 2 more seasons!','g');}},
    ]});
  } else {
    triggerCS({icon:'📅',title:`Season ${career.season} Begins`,sub:`${career.year}/${String(career.year+1).slice(2)}`,scene:`Pre-season. The manager gathers the squad. "Last year was the foundation. This year, we push for silverware." All eyes on you.`,q:'This season I will...',choices:[
      {t:'Attack record',s:'I\'m going to be top scorer.',ef:()=>{career.stats.finishing=Math.min(99,(career.stats.finishing||60)+4);career.stats.positioning=Math.min(99,(career.stats.positioning||60)+3);toast('+4 Finishing +3 Positioning','g');}},
      {t:'Captain material',s:'I want the armband.',ef:()=>{career.managerFavor=Math.min(100,career.managerFavor+18);toast('+18 Favor','gr');}},
      {t:'All-rounder',s:'I\'ll be everywhere on the pitch.',ef:()=>{career.stats.stamina=Math.min(99,(career.stats.stamina||60)+5);career.stats.composure=Math.min(99,(career.stats.composure||60)+3);toast('+5 Stamina +3 Composure','g');}},
    ]});
  }
}

// ══════════════════════════════════════════════════════════════
// CUTSCENE ENGINE
// ══════════════════════════════════════════════════════════════
function triggerCS(cs){
  document.getElementById('csIcon').textContent=cs.icon;
  document.getElementById('csTitle').textContent=cs.title;
  document.getElementById('csSub').textContent=cs.sub;
  document.getElementById('csScene').textContent=cs.scene;
  document.getElementById('csQ').textContent=cs.q;
  const el=document.getElementById('csChoices');el.innerHTML='';
  cs.choices.forEach(c=>{
    const btn=document.createElement('div');btn.className='cs-ch';
    btn.innerHTML=`<div class="cht">${c.t}</div><div class="chs">${c.s}</div>`;
    btn.addEventListener('click',()=>{if(c.ef)c.ef();closeCS();save();});
    el.appendChild(btn);
  });
  document.getElementById('csOverlay').classList.add('open');
}
function closeCS(){document.getElementById('csOverlay').classList.remove('open');}

// ══════════════════════════════════════════════════════════════
// TOAST
// ══════════════════════════════════════════════════════════════
function toast(msg,type=''){
  const wrap=document.getElementById('toastWrap');
  const t=document.createElement('div');
  t.className=`toast${type==='g'?' tg':type==='gr'?' tgr':type==='r'?' tr':type==='b'?' tg':''}`;
  t.textContent=msg;wrap.appendChild(t);
  requestAnimationFrame(()=>t.classList.add('show'));
  setTimeout(()=>{t.classList.remove('show');setTimeout(()=>t.remove(),400);},3200);
}

// ══════════════════════════════════════════════════════════════
// MENU
// ══════════════════════════════════════════════════════════════

// ══════════════════════════════════════════════════════════════
// TRAINING DRILLS — Earn SP through practice
// ══════════════════════════════════════════════════════════════
const DRILLS=[
  {id:'fitness',name:'Fitness Run',icon:'🏃',desc:'Sprint sessions improve stamina and pace',time:15,sp:1,boost:{stamina:1,acceleration:1},fatigue:20},
  {id:'shooting',name:'Finishing Drills',icon:'⚽',desc:'Shooting practice at various angles',time:20,sp:1,boost:{finishing:1,shot_power:1,positioning:1},fatigue:25},
  {id:'passing',name:'Passing Circuits',icon:'🎯',desc:'One-touch and long-range passing',time:20,sp:1,boost:{short_passing:1,vision:1,long_passing:1},fatigue:20},
  {id:'dribbling',name:'Dribbling Course',icon:'💨',desc:'Cone drills and close control',time:20,sp:1,boost:{dribbling:1,agility:1,ball_control:1},fatigue:25},
  {id:'defense',name:'Defensive Shape',icon:'🛡️',desc:'Tactical shape and interception timing',time:20,sp:1,boost:{defensive_awareness:1,interceptions:1,standing_tackle:1},fatigue:20},
  {id:'gym',name:'Gym Session',icon:'💪',desc:'Weight training — strength and physicality',time:25,sp:1,boost:{strength:1,jumping:1,aggression:1},fatigue:35},
  {id:'video',name:'Video Analysis',icon:'📹',desc:'Study opponents and positions',time:10,sp:1,boost:{composure:1,reactions:1},fatigue:5,managerFavor:3},
  {id:'double',name:'Double Session',icon:'⚡',desc:'Full day training — high SP gain',time:60,sp:3,boost:{},fatigue:70,allBoost:1},
];

let playerFatigue=0; // 0-100, resets each matchday

function refreshTrainingDrills(){
  if(!career)return;
  document.getElementById('tSpVal').textContent=career.sp;
  const fbar=document.getElementById('fatigueBar');
  if(fbar){fbar.style.width=playerFatigue+'%';fbar.style.background=playerFatigue>70?'var(--red)':playerFatigue>40?'var(--gold)':'var(--green)';}
  const fl=document.getElementById('fatigueLabel');
  if(fl)fl.textContent=playerFatigue>70?'Exhausted - risk of injury':playerFatigue>40?'Tired':'Fresh';
  
  const grid=document.getElementById('drillGrid');
  if(!grid)return;
  grid.innerHTML=DRILLS.map((d,i)=>{
    const canDo=playerFatigue+d.fatigue<=100;
    return '<div class="drill-card'+(canDo?'':' locked')+'" onclick="'+(canDo?'doDrill('+i+')':'')+'">'+
      '<span class="drill-icon">'+d.icon+'</span>'+
      '<div class="drill-info">'+
        '<div class="drill-name">'+d.name+'</div>'+
        '<div class="drill-desc">'+d.desc+'</div>'+
        '<div class="drill-reward">+'+d.sp+' SP &nbsp;·&nbsp; ⏱ '+d.time+' min &nbsp;·&nbsp; 😓 '+d.fatigue+'%</div>'+
      '</div>'+
    '</div>';
  }).join('');

  // Attribute upgrade section
  const isGK=career.pos==='GK';
  const keys=isGK?GK_STATS:OUTFIELD_STATS;
  document.getElementById('trainStats').innerHTML=keys.map(function(k){
    var v=career.stats[k]||0;
    return '<div class="tr-row">'+
    '<div class="tr-l">'+(STAT_LABELS[k]||k)+'</div>'+
    '<div class="tr-bg"><div class="tr-fill" style="width:'+Math.min(100,v)+'%"></div></div>'+
    '<div class="tr-v">'+v+'</div>'+
    '<button class="tr-btn" onclick="trainStat(this)" data-stat="'+k+'">'+(v>=99?'MAX':'+ 1SP')+'</button>'+
    '</div>';
  }).join('');
  // Position switch
  var ALL_POS_LIST=['GK','CB','LB','RB','LWB','RWB','CDM','CM','CAM','LM','RM','LW','RW','CF','ST'];
  var psEl=document.getElementById('posSwitch');
  if(psEl){
    var pb=ALL_POS_LIST.map(function(p){
      var a=p===career.pos;
      return '<button onclick="switchPos(this)" data-pos="'+p+'" style="font-family:DM Mono,monospace;font-size:.6rem;padding:4px 9px;border-radius:4px;border:1px solid '+(a?'var(--gold)':'var(--border2)')+';background:'+(a?'var(--gold3)':'transparent')+';color:'+(a?'var(--gold)':'var(--muted)')+';cursor:pointer;margin:2px;">'+p+'</button>';
    }).join('');
    psEl.innerHTML='<div style="display:flex;gap:4px;flex-wrap:wrap;">'+pb+'</div><div style="font-family:DM Mono,monospace;font-size:.62rem;color:var(--muted);margin-top:8px;">Costs 3 SP · stats adjust next season</div>';
  }
}

function doDrill(idx){
  const d=DRILLS[idx];
  if(!d)return;
  if(playerFatigue+d.fatigue>100){toast('Too tired! Rest after a match.','r');return;}
  if(career.sp<0)career.sp=0;
  playerFatigue+=d.fatigue;
  career.sp+=d.sp;
  // Apply small stat boost
  if(d.allBoost){
    const isGK=career.pos==='GK';
    const keys=isGK?GK_STATS:OUTFIELD_STATS;
    keys.forEach(k=>{career.stats[k]=Math.min(99,(career.stats[k]||50)+1);});
  } else {
    Object.entries(d.boost).forEach(([k,v])=>{career.stats[k]=Math.min(99,(career.stats[k]||50)+v);});
  }
  if(d.managerFavor)career.managerFavor=Math.min(100,career.managerFavor+d.managerFavor);
  career.ovr=calcOvr(career.stats,career.pos);
  save();
  toast(d.icon+' '+d.name+' done! +'+d.sp+' SP earned','gr');
  refreshTrainingDrills();
}

// ══════════════════════════════════════════════════════════════
// SIMULATE MATCH
// ══════════════════════════════════════════════════════════════
function simulateMatchFromHub(){
  if(!career)return;
  if(career.matchdayLeft<=0){toast('No league matches left this season!','r');return;}
  simulateMatch();
}

function simulateMatch(){
  if(!career)return;
  const opponents=CLUBS.filter(c=>c.league===career.league&&c.name!==career.club);
  const opp=opponents[rng(0,opponents.length-1)]||CLUBS[0];
  const oppTier=opp.tier||2;
  const myOvr=career.ovr||60;
  // Simulate result based on OVR diff
  const diff=(myOvr-60)/10 + career.managerFavor/100*2;
  const winChance=0.35+diff*0.08;
  const drawChance=0.25;
  const r=Math.random();
  let ys,os;
  if(r<winChance){ys=rng(1,4);os=rng(0,ys-1);}
  else if(r<winChance+drawChance){const g=rng(0,2);ys=g;os=g;}
  else{os=rng(1,3);ys=rng(0,os-1);}
  
  const won=ys>os,draw=ys===os;
  const myGoals=Math.random()<0.3?rng(0,Math.min(2,ys)):0;
  const myAssists=myGoals<ys&&Math.random()<0.3?rng(0,1):0;
  const rat=Math.min(10,Math.max(4.5,6.0+(won?0.8:draw?0.1:-0.5)+(myGoals*0.5)+(myAssists*0.3)));
  
  career.goals+=myGoals;career.assists+=myAssists;career.apps++;
  career.seasonGoals+=myGoals;career.seasonAssists+=myAssists;career.seasonApps++;
  career.matchdayLeft=Math.max(0,career.matchdayLeft-1);
  if(won)career.managerFavor=Math.min(100,career.managerFavor+rng(3,7));
  else if(!draw)career.managerFavor=Math.max(0,career.managerFavor+rng(-5,-1));
  const lc=career.comps.find(c=>c.id==='league');
  if(lc){lc.md++;lc.round='Matchday '+lc.md;if(won)lc.W++;else if(draw)lc.D++;else lc.L++;lc.GF+=ys;lc.GA+=os;}
  // Update league position estimate
  if(won)career.leaguePos=Math.max(1,career.leaguePos-1);
  else if(!draw)career.leaguePos=Math.min(20,career.leaguePos+1);
  
  const xp=20+(won?15:draw?7:0)+myGoals*15+myAssists*10;
  career.xp+=xp;
  while(career.xp>=xpNeeded(career.level)){career.xp-=xpNeeded(career.level);career.level++;career.sp+=5;toast('Level '+career.level+'! +4 SP','g');}
  
  playerFatigue=Math.min(100,playerFatigue+30); // matches tire you
  save();
  const res=won?'WIN':draw?'DRAW':'DEFEAT';
  toast(career.club+' '+ys+'-'+os+' '+opp.name+' | You: '+myGoals+'G '+myAssists+'A | Rating '+rat.toFixed(1)+' | SIM','g');
  refreshCareer();
  // Check relegation/promotion near season end
  if(career.matchdayLeft<=5)checkRelegationPromotion();
}

// ══════════════════════════════════════════════════════════════
// RELEGATION / PROMOTION
// ══════════════════════════════════════════════════════════════
function checkRelegationPromotion(){
  if(!career)return;
  const currentLeague=career.league;
  let hierarchy=null;let tierIdx=-1;
  for(const [country,tiers] of Object.entries(LEAGUE_HIERARCHY)){
    const idx=tiers.indexOf(currentLeague);
    if(idx>=0){hierarchy=tiers;tierIdx=idx;break;}
  }
  if(!hierarchy)return;
  const pos=career.leaguePos;
  // Promoted: top 2 in tier (not top tier)
  if(tierIdx>0&&pos<=2){
    const upperLeague=hierarchy[tierIdx-1];
    triggerCS({icon:'🚀',title:'PROMOTION!',sub:upperLeague,
      scene:'The final whistle blows. Your teammates pile on. You have won promotion to the '+upperLeague+'! The fans are streaming onto the pitch. The manager lifts you onto his shoulders.',
      q:'How do you feel?',choices:[
        {t:'Ecstatic',s:'This is the greatest moment of my life!',ef:()=>{career.managerFavor=Math.min(100,career.managerFavor+15);career.trophies.push('Promoted to '+upperLeague+' ('+career.year+')');career.league=upperLeague;career.matchdayLeft=LEAGUE_FIXTURES[upperLeague]||38;career.leaguePos=18;save();toast('Promoted to '+upperLeague+'!','gr');}},
        {t:'Focused',s:'Now the real work begins.',ef:()=>{career.stats.composure=Math.min(99,(career.stats.composure||60)+5);career.trophies.push('Promoted to '+upperLeague+' ('+career.year+')');career.league=upperLeague;career.matchdayLeft=LEAGUE_FIXTURES[upperLeague]||38;career.leaguePos=18;save();toast('Promoted to '+upperLeague+'!','gr');}},
      ]
    });
  }
  // Relegated: bottom 3 in a non-bottom tier
  else if(tierIdx<hierarchy.length-1&&pos>=18){
    const lowerLeague=hierarchy[tierIdx+1];
    triggerCS({icon:'😢',title:'RELEGATED',sub:lowerLeague,
      scene:'The season ends in disappointment. The club is relegated to the '+lowerLeague+'. The dressing room is silent. The manager stares at the floor.',
      q:'What do you do?',choices:[
        {t:'Stay and fight back',s:'We will bounce straight back up.',ef:()=>{career.trophies.push('Relegated to '+lowerLeague+' ('+career.year+')');career.league=lowerLeague;career.matchdayLeft=LEAGUE_FIXTURES[lowerLeague]||38;career.leaguePos=3;save();toast('Relegated to '+lowerLeague,'r');}},
        {t:'Request transfer out',s:'I need to play at a higher level.',ef:()=>{career.trophies.push('Relegated to '+lowerLeague+' ('+career.year+')');career.league=lowerLeague;career.matchdayLeft=LEAGUE_FIXTURES[lowerLeague]||38;career.leaguePos=3;generateOffer();save();toast('Transfer request submitted.','g');}},
      ]
    });
  }
}

// ══════════════════════════════════════════════════════════════
// CALENDAR
// ══════════════════════════════════════════════════════════════
function generateCalendar(){
  if(!career)return;
  const year=career.year;
  const totalGames=LEAGUE_FIXTURES[career.league]||38;
  const months=CALENDAR_MONTHS;
  const days=MATCH_DAYS_PER_MONTH;
  let entries=[];
  let matchNum=0;
  let cupNum=0;
  months.forEach((month,mi)=>{
    const mYear=mi<6?year:year+1;
    const matchesThisMonth=Math.min(days[mi],totalGames-matchNum);
    for(let d=0;d<matchesThisMonth;d++){
      matchNum++;
      const day=5+d*7+rng(0,2);
      entries.push({month,mYear,day:Math.min(day,28),type:'league',comp:career.league,matchday:matchNum,done:matchNum<=career.seasonApps});
    }
    // Cup entries
    if([0,1,2,3,4,5].includes(mi)){
      if(mi===0&&career.comps.some(c=>c.id==='cs'))entries.push({month,mYear,day:7,type:'cup',comp:'Community Shield',done:false});
      if(mi===1||mi===2)entries.push({month,mYear,day:19,type:'cup',comp:'Cup Round',done:false});
      if(mi>=3&&mi<=5&&career.comps.some(c=>['ucl','uel','uecl'].includes(c.id)))
        entries.push({month,mYear,day:22,type:'euro',comp:'European Night',done:false});
    }
  });
  return entries;
}

function refreshCalendar(){
  if(!career)return;
  const entries=generateCalendar();
  const el=document.getElementById('calendarContent');
  if(!el)return;
  let currentMonth='';
  let html='';
  entries.forEach(e=>{
    if(e.month!==currentMonth){
      if(currentMonth)html+='</div>';
      html+='<div class="cal-month"><div class="cal-month-head">'+e.month+' '+e.mYear+'</div>';
      currentMonth=e.month;
    }
    const typeColor=e.type==='league'?'var(--gold)':e.type==='cup'?'var(--green)':'var(--cyan)';
    const doneStyle=e.done?'opacity:.4;text-decoration:line-through;':'';
    html+='<div class="cal-entry" style="'+doneStyle+'">'+
      '<span class="cal-day">'+e.day+'</span>'+
      '<span class="cal-type" style="color:'+typeColor+'">'+
        (e.type==='league'?'⚽ MD '+e.matchday:e.type==='cup'?'🏆 Cup':'⭐ Euro')+
      '</span>'+
      '<span class="cal-comp">'+e.comp+'</span>'+
    '</div>';
  });
  if(currentMonth)html+='</div>';
  el.innerHTML=html||'<div style="color:var(--muted);padding:20px;font-family:DM Mono,monospace;font-size:.72rem;">No calendar generated.</div>';
}

// ══════════════════════════════════════════════════════════════
// PERSONAL MANAGER / AGENT
// ══════════════════════════════════════════════════════════════
function getManagerName(){
  if(!career.agentName){
    career.agentName=MANAGER_NAMES[rng(0,MANAGER_NAMES.length-1)];
  }
  return career.agentName;
}

function refreshAgent(){
  if(!career)return;
  const agent=getManagerName();
  const el=document.getElementById('agentContent');
  if(!el)return;
  const val=calcValue();
  const curSalary=(career.salary||0).toLocaleString();
  const fav=career.managerFavor;
  const favText=fav>70?'Excellent — manager trusts you fully':fav>50?'Good standing':fav>30?'Needs improvement':'Critical — action required';
  el.innerHTML=
    '<div class="agent-card">'+
      '<div class="agent-header">'+
        '<span class="agent-icon">🤵</span>'+
        '<div>'+
          '<div class="agent-name">'+agent+'</div>'+
          '<div class="agent-title">Your Personal Agent</div>'+
        '</div>'+
      '</div>'+
      '<div class="agent-body">'+
        '<div class="agent-row"><span>Market Value</span><span class="agent-val">£'+val+'M</span></div>'+
        '<div class="agent-row"><span>Current Salary</span><span class="agent-val">£'+curSalary+'/wk</span></div>'+
        '<div class="agent-row"><span>Contract Until</span><span class="agent-val">'+(career.contractEnd||career.year+3)+'</span></div>'+
        '<div class="agent-row"><span>Manager Favor</span><span class="agent-val">'+fav+'% — '+favText+'</span></div>'+
        '<div class="agent-row"><span>Club</span><span class="agent-val">'+career.club+'</span></div>'+
      '</div>'+
      '<div class="agent-actions">'+
        '<button class="act-btn acc" onclick="negotiateContract()">Negotiate Contract</button>'+
        '<button class="act-btn" style="border-color:var(--cyan);color:var(--cyan);" onclick="requestLoan()">Request Loan</button>'+
        '<button class="act-btn" style="border-color:var(--gold);color:var(--gold);" onclick="requestTransfer()">Request Transfer</button>'+
      '</div>'+
    '</div>'+
    // Manager cutscene button if favor is bad
    (fav<35?'<div class="warn-box" style="margin-top:12px;">⚠ Manager favor is critical. Consider requesting a loan or having a meeting.</div>'+
      '<button class="act-btn" style="border-color:var(--red);color:var(--red);margin-top:8px;width:100%;" onclick="managerMeeting()">Request Manager Meeting</button>':'');
}

function negotiateContract(){
  const val=calcValue();
  const fav=career.managerFavor;
  const pres=LEAGUE_PRESTIGE[career.league]||2;
  const baseSal=calcSalary(pres,career.ovr);
  const raise=Math.round(baseSal*1.25/500)*500;
  
  triggerCS({icon:'📋',title:'Contract Negotiation',sub:career.club,
    scene:career.agentName+' walks into the boardroom. "We believe '+career.name+' is worth more to this club than the current contract reflects. His market value stands at £'+val+'M, and comparable players in this league are earning significantly more."',
    q:'Choose your approach:',choices:[
      {t:'Demand top wages',s:'£'+raise.toLocaleString()+'/wk or I walk.',ef:()=>{
        if(fav>60){career.salary=raise;career.contractEnd=(career.contractEnd||career.year+2)+3;save();toast('Contract renewed! £'+raise.toLocaleString()+'/wk x3 years','gr');}
        else{career.managerFavor=Math.max(0,career.managerFavor-15);toast('Club rejected demands. Favor -15.','r');}
      }},
      {t:'Accept fair offer',s:'Reasonable increase, happy to stay.',ef:()=>{
        const fairSal=Math.round(baseSal*1.1/500)*500;
        career.salary=fairSal;career.contractEnd=(career.contractEnd||career.year+2)+2;
        career.managerFavor=Math.min(100,career.managerFavor+8);
        save();toast('Contract extended! £'+fairSal.toLocaleString()+'/wk +8 Favor','gr');
      }},
      {t:'Short-term deal',s:'1 year deal — reassess next season.',ef:()=>{
        career.contractEnd=(career.year+1);
        career.managerFavor=Math.min(100,career.managerFavor+3);
        save();toast('1-year deal signed. More freedom next summer.','g');
      }},
    ]
  });
}

function requestLoan(){
  triggerCS({icon:'📋',title:'Loan Request',sub:'Agent Meeting',
    scene:career.agentName+' sits across from the sporting director. "'+career.name+' would benefit enormously from a season-long loan. He needs consistent minutes at a high level to reach his full potential."',
    q:'Your preference:',choices:[
      {t:'Same league',s:'Stay in '+career.league+' with more game time.',ef:()=>{
        const sameLeague=CLUBS.filter(c=>c.league===career.league&&c.name!==career.club);
        const dest=sameLeague[rng(0,sameLeague.length-1)];
        if(dest){career.offers.push({clubName:dest.name,league:dest.league,clubData:dest,fee:0,wage:Math.round((career.salary||5000)*0.9/500)*500,type:'loan'});save();toast('Loan offer from '+dest.name+' incoming!','g');}
      }},
      {t:'Higher league',s:'I want to prove myself at a higher level.',ef:()=>{
        const higher=CLUBS.filter(c=>(c.tier||2)>=(CLUBS.find(x=>x.name===career.club)?.tier||2));
        const dest=higher[rng(0,higher.length-1)];
        if(dest){career.offers.push({clubName:dest.name,league:dest.league,clubData:dest,fee:0,wage:Math.round((career.salary||5000)*1.1/500)*500,type:'loan'});save();toast('Loan offer from '+dest.name+'!','g');}
      }},
      {t:'Cancel request',s:'Actually, I want to fight for my place.',ef:()=>{career.managerFavor=Math.min(100,career.managerFavor+5);toast('Stayed. Manager pleased. +5 Favor','gr');}},
    ]
  });
}

function requestTransfer(){
  const fav=career.managerFavor;
  triggerCS({icon:'🚪',title:'Transfer Request',sub:'Sporting Director',
    scene:career.agentName+' places the formal written transfer request on the desk. "'+career.name+' feels the time is right to move on and explore new opportunities. We trust the club will act professionally."',
    q:'How formal do you go?',choices:[
      {t:'Public request',s:'I formally request a transfer.',ef:()=>{
        if(fav<40)career.managerFavor=Math.max(0,career.managerFavor-20);
        generateOffer();save();toast('Transfer request submitted. Offer expected.','g');
      }},
      {t:'Private conversation',s:'I would like to discuss my future, boss.',ef:()=>{
        if(fav>50){generateOffer();career.managerFavor=Math.max(0,career.managerFavor-5);save();toast('Manager understood. Listening for offers. -5 Favor','g');}
        else{toast('Manager rejected quiet approach. Try again.','r');}
      }},
      {t:'Stay loyal',s:'Actually, I will honour my contract.',ef:()=>{
        career.managerFavor=Math.min(100,career.managerFavor+12);save();toast('Loyal decision! +12 Manager Favor','gr');
      }},
    ]
  });
}

function managerMeeting(){
  const mgrFav=career.managerFavor;
  const mgr=career.clubManager||'the manager';
  triggerCS({icon:'🤝',title:'Manager Meeting',sub:career.club,
    scene:mgr+' gestures for you to sit. "I appreciate you coming to see me. Let me be direct - your performances recently have not been at the level I expect. I need to know if your head is still here." He waits for your response.',
    q:'How do you respond?',choices:[
      {t:'Fully committed',s:'My head is 100% here. I will turn this around.',ef:()=>{
        career.managerFavor=Math.min(100,career.managerFavor+20);
        career.stats.composure=Math.min(99,(career.stats.composure||60)+3);
        save();toast('Manager meeting helped! +20 Favor +3 Composure','gr');
      }},
      {t:'Honest concern',s:'I have been struggling mentally. I need game time.',ef:()=>{
        career.managerFavor=Math.min(100,career.managerFavor+10);
        toast('+10 Favor. Manager will monitor situation.','g');save();
      }},
      {t:'Challenge back',s:'Give me a run of games and I will show you.',ef:()=>{
        if(mgrFav>25){career.managerFavor=Math.min(100,career.managerFavor+8);toast('Bold! Manager respected the confidence. +8 Favor','gr');}
        else{career.managerFavor=Math.max(0,career.managerFavor-10);toast('Manager did not appreciate that. -10 Favor','r');}
        save();
      }},
    ]
  });
}

// Manager cutscene triggers based on favor thresholds
function checkManagerCutscenes(){
  if(!career)return;
  const fav=career.managerFavor;
  const mgr=career.clubManager||'The manager';
  // Only trigger if not recently triggered
  if(career._lastManagerCS&&career.seasonApps-career._lastManagerCS<3)return;
  
  if(fav<20&&Math.random()<0.4){
    career._lastManagerCS=career.seasonApps;
    triggerCS({icon:'😡',title:'You Are Dropped',sub:career.club,
      scene:mgr+' calls you into his office before training. "I am leaving you out of the squad this weekend. Your form and attitude have not met the standards of this club. Take the time to reflect." He does not look up from his desk.',
      q:'What do you do?',choices:[
        {t:'Accept and train harder',s:'I understand. I will prove you wrong in training.',ef:()=>{career.managerFavor=Math.min(100,career.managerFavor+10);doDrill(7);toast('Extra training helped. +10 Favor','gr');}},
        {t:'Request to leave',s:'If I am not wanted here, let me go.',ef:()=>{generateOffer();toast('Transfer request submitted.','g');}},
      ]
    });
  } else if(fav>85&&Math.random()<0.3&&career.seasonApps>5){
    career._lastManagerCS=career.seasonApps;
    triggerCS({icon:'⭐',title:'Captain Offer',sub:career.club,
      scene:mgr+' stops you after training. "I want to talk to you about the armband. The squad respects you. You lead by example every single day. I want you to captain this club." He holds out the captain armband.',
      q:'Do you accept?',choices:[
        {t:'Accept with pride',s:'It would be an honour.',ef:()=>{career.isCaptain=true;career.managerFavor=Math.min(100,career.managerFavor+10);career.trophies.push('Club Captain ('+career.year+')');save();toast('You are the captain! +10 Favor','gr');}},
        {t:'Focus on playing',s:'I lead best on the pitch, not off it.',ef:()=>{career.stats.dribbling=Math.min(99,(career.stats.dribbling||60)+3);toast('Respect. +3 Dribbling — focus on game.','g');}},
      ]
    });
  }
}

// First match cutscene
function triggerFirstMatchCS(){
  if(career.firstMatchDone)return;
  career.firstMatchDone=true;
  save();
  triggerCS({icon:'🔔',title:'Debut Day',sub:career.club,
    scene:'The tunnel is louder than you expected. The smell of fresh grass hits you as you walk out. Thousands of fans are chanting. You pull your shirt — your name on the back. This is it. Your first competitive match for '+career.club+'. The referee blows his whistle.',
    q:'What is your mindset?',choices:[
      {t:'Controlled',s:'Play your game. Trust the training.',ef:()=>{career.stats.composure=Math.min(99,(career.stats.composure||60)+4);career.stats.reactions=Math.min(99,(career.stats.reactions||60)+3);toast('+4 Composure +3 Reactions','gr');}},
      {t:'Fearless',s:'This is your stage. Take it.',ef:()=>{career.stats.finishing=Math.min(99,(career.stats.finishing||60)+3);career.stats.acceleration=Math.min(99,(career.stats.acceleration||60)+4);toast('+3 Finishing +4 Acceleration','gr');}},
      {t:'Grounded',s:'Just another game. One step at a time.',ef:()=>{career.stats.stamina=Math.min(99,(career.stats.stamina||60)+5);career.managerFavor=Math.min(100,career.managerFavor+5);toast('+5 Stamina +5 Favor — grounded approach','gr');}},
    ]
  });
}


function refreshLeagueTable(){
  if(!career)return;
  document.getElementById('tableSub').textContent=career.league+' — Season '+career.year;
  const opponents=CLUBS.filter(c=>c.league===career.league&&c.name!==career.club);
  // Generate fake table
  const rows=[{name:career.name,club:career.club,isYou:true,pos:career.leaguePos,W:0,D:0,L:0,GF:0,GA:0}];
  const lc=career.comps.find(c=>c.id==='league');
  if(lc){rows[0].W=lc.W;rows[0].D=lc.D;rows[0].L=lc.L;rows[0].GF=lc.GF;rows[0].GA=lc.GA;}
  opponents.slice(0,19).forEach((c,i)=>{
    const tier=c.tier||2;
    const w=rng(2,tier*3);const d=rng(1,4);const l=rng(1,tier*2);
    rows.push({name:c.name,club:c.name,isYou:false,pos:i+1+(i>=career.leaguePos-1?1:0),W:w,D:d,L:l,GF:w*2+d,GA:l*2+d});
  });
  // Sort by points
  rows.forEach(r=>{r.pts=r.W*3+r.D;r.gd=r.GF-r.GA;});
  rows.sort((a,b)=>b.pts-a.pts||b.gd-a.gd);
  
  const totalTeams=rows.length;
  let html='<table class="league-table"><thead><tr><th>#</th><th>Club</th><th>W</th><th>D</th><th>L</th><th>GD</th><th>Pts</th></tr></thead><tbody>';
  rows.forEach((r,i)=>{
    const pos=i+1;
    const dot=pos<=4?'var(--blue)':pos<=7?'var(--cyan)':pos>=totalTeams-2?'var(--red)':'transparent';
    html+='<tr'+(r.isYou?' class="you-row"':'')+'>';
    html+='<td><span class="pos-dot" style="background:'+dot+'"></span>'+pos+'</td>';
    html+='<td>'+(r.isYou?'⭐ ':'')+r.club+'</td>';
    html+='<td>'+r.W+'</td><td>'+r.D+'</td><td>'+r.L+'</td>';
    html+='<td>'+(r.gd>0?'+':'')+r.gd+'</td>';
    html+='<td style="font-weight:600;color:var(--gold)">'+r.pts+'</td>';
    html+='</tr>';
  });
  html+='</tbody></table>';
  html+='<div style="display:flex;gap:16px;margin-top:12px;font-family:DM Mono,monospace;font-size:.6rem;color:var(--muted);">'+
    '<span><span class="pos-dot" style="background:var(--blue);display:inline-block;"></span>Champions League</span>'+
    '<span><span class="pos-dot" style="background:var(--cyan);display:inline-block;"></span>Europa League</span>'+
    '<span><span class="pos-dot" style="background:var(--red);display:inline-block;"></span>Relegation</span>'+
  '</div>';
  document.getElementById('tableContent').innerHTML=html;
}
function refreshMenu(){
  load();
  const b=document.getElementById('menuBtns');
  b.innerHTML=career?`<button class="mbtn gold" onclick="showScreen('career')">Continue Career</button><button class="mbtn outline" onclick="newCareerConfirm()">New Career</button>`:`<button class="mbtn gold" onclick="showScreen('create')">Start Career</button>`;
}
function newCareerConfirm(){
  if(!confirm('Start new career? Progress lost.'))return;
  career=null;try{localStorage.removeItem('fl_v3');}catch(e){}
  wizStep=1;selArch=null;selAcad=null;selClub=null;
  document.querySelectorAll('.wiz-step').forEach(s=>s.classList.remove('active'));
  document.getElementById('step-1').classList.add('active');
  updateWizProg();showScreen('create');
}
function confirmReset(){
  var nm=career&&career.name?career.name:'this career';
  if(!confirm('Delete '+nm+'s career? All progress will be lost permanently.'))return;
  // Clear everything
  career=null;av={skin:SKIN_TONES[1],hair:'Short Fade',hairCol:HAIR_COLS[0],kit:KIT_COLS[0],boot:BOOT_COLS[0]};
  matchState=null;
  window._currentSit=null;window._decisionCallback=null;
  try{localStorage.removeItem('fl_v3');}catch(e){}
  // Reset wizard
  wizStep=1;selArch=null;selAcad=null;selClub=null;selModel='euro';activeLeagueTab='ALL';
  document.querySelectorAll('.wiz-step').forEach(function(s){s.classList.remove('active');});
  var s1=document.getElementById('step-1');if(s1)s1.classList.add('active');
  updateWizProg();
  // Go to menu
  document.querySelectorAll('.screen').forEach(function(s){s.classList.remove('active');});
  var menuEl=document.getElementById('screen-menu');
  if(menuEl)menuEl.classList.add('active');
  // Force re-render menu buttons
  var b=document.getElementById('menuBtns');
  if(b)b.innerHTML=`<button class="mbtn gold" onclick="showScreen('create')">Start Career</button>`;
  toast('Career deleted.','gr');
}

// ══════════════════════════════════════════════════════════════
// BOOT
// ══════════════════════════════════════════════════════════════
const ns=document.getElementById('natSel');
NATIONS.forEach(n=>{const o=document.createElement('option');o.value=n;o.textContent=n;if(n==='England')o.selected=true;ns.appendChild(o);});
load();updateWizProg();showScreen('menu');
</script>
</body>
</html>
