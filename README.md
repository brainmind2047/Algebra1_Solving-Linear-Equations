<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Sopaan · Solving Linear Equations</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Source+Sans+3:wght@400;600;700&family=IBM+Plex+Mono:wght@500;600&display=swap">
<style>
  html,body{margin:0;} img{max-width:100%;} [hidden]{display:none !important;}
  :root{
    --navy:#16264A; --navy-2:#1F3B6B; --gold:#C79A3E; --gold-soft:#F3E7C9;
    --paper:#FBF9F4; --paper-2:#F1EAD8; --card:#FFFFFF;
    --ink:#211E1A; --ink-soft:#655D4C; --rule:#E4DCC8;
    --success:#2E8B57; --success-soft:#E1F2E7;
    --danger:#BF4B45; --danger-soft:#FAE3E1;
    --locked:#C7BEA9;
    --focus:#1F3B6B;
    --accent-text:#1F3B6B; --retry-text:#8A661F;
    color-scheme:light;
  }
  @media (prefers-color-scheme: dark){
    :root:not([data-theme="light"]){
      --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
      --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
      --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
      --success:#7BC79A; --success-soft:#1B2E22;
      --danger:#E38884; --danger-soft:#331D1B;
      --locked:#4A4436;
      --focus:#E0B75B;
      --accent-text:#E0B75B; --retry-text:#E0B75B;
      color-scheme:dark;
    }
  }
  :root[data-theme="dark"]{
    --navy:#0E1830; --navy-2:#16264A; --gold:#E0B75B; --gold-soft:#3A2F16;
    --paper:#141210; --paper-2:#1C1914; --card:#1C1914;
    --ink:#EDE7DA; --ink-soft:#B2A996; --rule:#3A342A;
    --success:#7BC79A; --success-soft:#1B2E22;
    --danger:#E38884; --danger-soft:#331D1B;
    --locked:#4A4436;
    --focus:#E0B75B;
    --accent-text:#E0B75B; --retry-text:#E0B75B;
    color-scheme:dark;
  }

  *{box-sizing:border-box;}
  body{background:var(--paper); color:var(--ink); font-family:'Source Sans 3',-apple-system,'Segoe UI',sans-serif; padding-inline:0; padding-block:0;}
  h1,h2,h3{font-family:'Fraunces',Georgia,serif; text-wrap:balance; margin:0;}
  .num{font-family:'IBM Plex Mono',ui-monospace,monospace; font-variant-numeric:tabular-nums;}

  header.brand{
    background:linear-gradient(155deg,var(--navy) 0%, var(--navy-2) 100%);
    color:#F4EFDF; padding-block:calc(20px + env(safe-area-inset-top,0px)) 18px; padding-inline:20px;
  }
  .brand-row{display:flex; align-items:center; gap:12px; max-width:900px; margin:0 auto;}
  .crest{
    width:42px; height:42px; border-radius:10px; background:var(--gold); color:var(--navy);
    display:flex; align-items:center; justify-content:center; font-family:'Fraunces',serif; font-weight:700; font-size:18px; flex-shrink:0;
  }
  .brand-name{font-size:12px; letter-spacing:.08em; text-transform:uppercase; color:var(--gold); font-weight:700;}
  .series-name{font-size:19px; font-weight:700; font-family:'Fraunces',serif;}
  .chapter-eyebrow{max-width:900px; margin:14px auto 0; font-size:12px; letter-spacing:.06em; text-transform:uppercase; color:#AEB9D6;}
  .chapter-title{font-size:28px; max-width:900px; margin:2px auto 0;}
  .chapter-sub{font-size:14.5px; color:var(--gold); font-weight:700; max-width:900px; margin:3px auto 0;}

  .chapter-progress{max-width:900px; margin:14px auto 0; display:flex; align-items:center; gap:10px;}
  .cp-track{flex:1; height:6px; border-radius:99px; background:rgba(255,255,255,.18); overflow:hidden;}
  .cp-fill{height:100%; background:var(--gold); border-radius:99px; transition:width .3s ease;}
  .cp-label{font-size:11.5px; color:#CFD7EA; white-space:nowrap;}

  .tabbar{position:sticky; top:env(safe-area-inset-top,0px); z-index:15; background:var(--paper); border-bottom:1px solid var(--rule); overflow-x:auto; white-space:nowrap;}
  .tabbar-inner{max-width:900px; margin:0 auto; display:flex; padding-inline:16px;}
  .tab-btn{font-family:inherit; font-size:14px; font-weight:600; color:var(--ink-soft); background:none; border:none; padding:13px 16px; cursor:pointer; position:relative; flex-shrink:0;}
  .tab-btn.active{color:var(--accent-text);}
  .tab-btn.active::after{content:''; position:absolute; left:12px; right:12px; bottom:0; height:3px; background:var(--gold); border-radius:3px 3px 0 0;}
  .tab-count{font-size:11px; color:var(--ink-soft); margin-left:5px;}

  .slide-progress{max-width:900px; margin:0 auto; padding:10px 16px 0; display:flex; align-items:center; gap:10px;}
  .sp-track{flex:1; height:5px; border-radius:99px; background:var(--rule); overflow:hidden;}
  .sp-fill{height:100%; background:var(--accent-text); border-radius:99px; transition:width .3s ease;}
  .sp-label{font-size:12px; color:var(--ink-soft); white-space:nowrap; font-weight:600;}

  .wrap{max-width:900px; margin:0 auto; padding:16px 16px calc(110px + env(safe-area-inset-bottom,0px));}

  .qcard{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px;}
  .qhead{display:flex; align-items:flex-start; gap:10px; margin-bottom:10px;}
  .qnum{width:32px; height:32px; border-radius:8px; background:var(--gold-soft); color:var(--accent-text); display:flex; align-items:center; justify-content:center; font-weight:700; font-family:'Fraunces',serif; flex-shrink:0; font-size:14px;}
  .qtext{font-size:16px; line-height:1.55; flex:1;}
  .qtag{font-size:10.5px; color:var(--gold); background:var(--gold-soft); padding:2px 7px; border-radius:99px; font-weight:700; margin-left:6px; white-space:nowrap;}
  .marks-pill{font-size:11px; font-weight:700; color:var(--ink-soft); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; margin-left:auto; flex-shrink:0; white-space:nowrap;}
  .step-badge{font-size:11px; font-weight:700; color:var(--accent-text); background:var(--paper-2); border:1px solid var(--rule); padding:3px 9px; border-radius:99px; display:inline-block; margin-bottom:12px;}

  .options{display:flex; flex-direction:column; gap:8px; margin-top:10px;}
  .opt{display:flex; align-items:center; gap:10px; padding:11px 12px; border:1.5px solid var(--rule); border-radius:10px; cursor:pointer; font-size:15px; background:var(--paper);}
  .opt input{accent-color:var(--navy-2);}
  .opt.is-correct{border-color:var(--success); background:var(--success-soft);}
  .opt.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .opt.locked{cursor:not-allowed;}

  .subpart-label{font-weight:700; font-size:12.5px; color:var(--accent-text); text-transform:uppercase; letter-spacing:.03em; margin:14px 0 6px;}
  .or-divider{text-align:center; font-size:11px; font-weight:700; letter-spacing:.08em; color:var(--ink-soft); margin:8px 0;}

  .steps{display:flex; flex-direction:column; gap:10px;}
  .step-line{font-size:14.5px; line-height:1.9; background:var(--paper); border:1px dashed var(--rule); border-radius:10px; padding:9px 12px;}
  .step-line.resolved{opacity:.9;}
  .blank-input{font-family:'IBM Plex Mono',monospace; font-size:14px; border:1.5px solid var(--rule); border-radius:6px; padding:3px 8px; width:120px; background:var(--card); color:var(--ink); margin:0 2px;}
  .blank-input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .blank-input.is-correct{border-color:var(--success); background:var(--success-soft);}
  .blank-input.is-wrong{border-color:var(--danger); background:var(--danger-soft);}
  .blank-input[disabled]{opacity:.85;}
  .reveal-note{font-size:12px; color:var(--danger); padding-left:2px; margin-top:-2px;}

  .feedback{font-size:13.5px; padding:10px 12px; border-radius:9px; margin-top:14px; display:none;}
  .feedback.show{display:block;}
  .feedback.ok{background:var(--success-soft); color:var(--success);}
  .feedback.retry{background:var(--gold-soft); color:var(--retry-text);}
  .feedback.reveal{background:var(--danger-soft); color:var(--danger);}
  .feedback.err{background:var(--danger-soft); color:var(--danger);}
  .attempts-dots{display:inline-flex; gap:4px; margin-left:2px;}
  .attempts-dots span{width:6px; height:6px; border-radius:50%; background:var(--ink-soft); opacity:.3; display:inline-block;}
  .attempts-dots span.used{opacity:1; background:var(--danger);}

  .ar-box{background:var(--paper-2); border-radius:10px; padding:10px 12px; margin-bottom:12px; font-size:13px; color:var(--ink-soft);}

  .navbar{
    position:fixed; left:0; right:0; bottom:0; z-index:30; background:var(--paper);
    border-top:1px solid var(--rule); padding:10px 16px calc(10px + env(safe-area-inset-bottom,0px));
  }
  .navbar-inner{max-width:900px; margin:0 auto; display:flex; gap:8px; flex-wrap:wrap; align-items:center;}
  .btn{font-family:inherit; font-size:13.5px; font-weight:700; padding:10px 14px; border-radius:9px; border:1.5px solid var(--rule); background:var(--card); color:var(--ink); cursor:pointer;}
  .btn:hover{border-color:var(--navy-2);}
  .btn:disabled{opacity:.4; cursor:not-allowed;}
  .btn-primary{background:var(--navy-2); color:#fff; border-color:var(--navy-2);}
  .navbar .spacer{flex:1;}

  .fab{position:fixed; right:16px; bottom:calc(74px + env(safe-area-inset-bottom,0px)); background:var(--gold); color:var(--navy); border:none; border-radius:999px; padding:11px 16px; font-family:inherit; font-weight:700; font-size:13px; display:flex; align-items:center; gap:7px; cursor:pointer; box-shadow:0 6px 16px rgba(0,0,0,.18); z-index:35;}
  .fab-badge{background:rgba(255,255,255,.55); border-radius:99px; padding:1px 7px; font-size:11px;}

  .overlay{position:fixed; inset:0; background:rgba(20,18,14,.45); z-index:50; display:none; align-items:flex-end; justify-content:center;}
  .overlay.show{display:flex;}
  .palette{background:var(--card); width:min(480px,100%); max-height:78vh; overflow-y:auto; border-radius:18px 18px 0 0; padding:18px 18px calc(18px + env(safe-area-inset-bottom,0px)); border:1px solid var(--rule); border-bottom:none;}
  @media (min-width:640px){ .overlay{align-items:center;} .palette{border-radius:18px; border-bottom:1px solid var(--rule); max-height:74vh;} }
  .palette-head{display:flex; align-items:center; justify-content:space-between; margin-bottom:6px;}
  .palette-head h2{font-size:16px;}
  .palette-close{background:none; border:none; font-size:20px; color:var(--ink-soft); cursor:pointer; padding:4px;}
  .palette-legend{display:flex; gap:12px; flex-wrap:wrap; font-size:11px; color:var(--ink-soft); margin:10px 0 14px;}
  .palette-legend span{display:inline-flex; align-items:center; gap:5px;}
  .dot{width:9px; height:9px; border-radius:50%; display:inline-block;}
  .dot.correct{background:var(--success);} .dot.revealed{background:var(--danger);}
  .dot.skipped{background:var(--gold);} .dot.locked{background:var(--locked);}
  .dot.current{background:var(--navy-2);}
  .chip-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(48px,1fr)); gap:8px;}
  .chip{border:1.5px solid var(--rule); border-radius:9px; padding:8px 4px; text-align:center; font-family:'IBM Plex Mono',monospace; font-size:12.5px; font-weight:600; cursor:pointer; background:var(--paper); color:var(--ink);}
  .chip[data-status="correct"]{border-color:var(--success); background:var(--success-soft); color:var(--success);}
  .chip[data-status="revealed"]{border-color:var(--danger); background:var(--danger-soft); color:var(--danger);}
  .chip[data-status="skipped"]{border-color:var(--gold); background:var(--gold-soft); color:var(--retry-text);}
  .chip[data-status="locked"]{border-color:var(--rule); color:var(--locked); cursor:not-allowed; background:var(--paper-2);}
  .chip[data-status="current"]{outline:2px solid var(--navy-2); outline-offset:1px;}

  .toast{position:fixed; left:50%; bottom:calc(140px + env(safe-area-inset-bottom,0px)); transform:translateX(-50%); background:var(--ink); color:var(--paper); padding:9px 16px; border-radius:99px; font-size:13px; opacity:0; pointer-events:none; transition:opacity .25s ease; z-index:60;}
  .toast.show{opacity:1;}

  .done-card{text-align:center; padding:36px 20px;}
  .done-card .big{font-size:38px; margin-bottom:6px;}
  .score-pills{display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin:16px 0;}
  .score-pill{padding:8px 16px; border-radius:99px; font-size:13px; font-weight:700;}

  footer.brandfoot{max-width:900px; margin:14px auto 0; padding:0 16px calc(110px + env(safe-area-inset-bottom,0px)); text-align:center; font-size:12px; color:var(--ink-soft);}

  .mode-pill{font-family:inherit; font-size:12.5px; font-weight:700; color:var(--navy); background:var(--gold); border:none; border-radius:99px; padding:6px 14px; cursor:pointer; margin-top:12px; display:inline-flex; align-items:center; gap:6px;}
  .mode-pick{display:flex; flex-direction:column; gap:14px; padding:8px 0 24px;}
  .mode-card{background:var(--card); border:1.5px solid var(--rule); border-radius:16px; padding:22px; cursor:pointer; text-align:left;}
  .mode-card:hover{border-color:var(--navy-2);}
  .mode-card .mode-icon{font-size:26px; margin-bottom:8px;}
  .mode-card h3{font-size:18px; margin-bottom:6px;}
  .mode-card p{font-size:13.5px; color:var(--ink-soft); line-height:1.5; margin:0;}
  .quiz-hint{font-size:12.5px; color:var(--ink-soft); background:var(--paper-2); border-radius:9px; padding:8px 12px; margin-bottom:14px;}
  .review-row{border:1px solid var(--rule); border-radius:10px; padding:11px 13px; margin-bottom:10px;}
  .review-tag{font-size:11.5px; font-weight:700; margin-bottom:4px; display:block;}
  .review-tag.ok{color:var(--success);} .review-tag.bad{color:var(--danger);} .review-tag.na{color:var(--ink-soft);}
  .review-q{font-size:13.5px; margin-bottom:6px; color:var(--ink-soft);}
  .review-ans{font-size:13px; margin-bottom:2px;}

  .who-row{max-width:900px; margin:12px auto 0; display:flex; flex-wrap:wrap; gap:8px; align-items:center;}
  .who-row .mode-pill{margin-top:0;}
  .who{display:inline-flex; flex-wrap:wrap; align-items:center; gap:6px; font-size:12.5px; color:#CFD7EA;}
  .who b{color:#F4EFDF;}
  .who button{font-family:inherit; font-size:12px; font-weight:700; color:#F4EFDF; background:rgba(255,255,255,.12); border:1px solid rgba(255,255,255,.22); border-radius:99px; padding:5px 11px; cursor:pointer;}
  .who button:hover{background:rgba(255,255,255,.2);}
  .login-card{max-width:460px; margin:8px auto 0; background:var(--card); border:1px solid var(--rule); border-radius:16px; padding:22px;}
  .login-card h2{font-size:21px; margin-bottom:4px;}
  .login-card p.lead{font-size:13.5px; color:var(--ink-soft); margin:0 0 16px; line-height:1.5;}
  .fld{display:flex; flex-direction:column; gap:5px; margin-bottom:12px;}
  .fld label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .fld input{font-family:inherit; font-size:15px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:9px; background:var(--paper); color:var(--ink);}
  .fld input:focus{outline:none; border-color:var(--focus); box-shadow:0 0 0 3px var(--gold-soft);}
  .fld-row{display:grid; grid-template-columns:1fr 1fr; gap:10px;}
  .login-err{font-size:13px; color:var(--danger); background:var(--danger-soft); border-radius:8px; padding:8px 10px; margin-bottom:12px;}
  .login-note{font-size:12px; color:var(--ink-soft); margin-top:12px; line-height:1.5;}
  .known{margin:0 0 16px; display:flex; flex-direction:column; gap:6px;}
  .known-label{font-size:12px; font-weight:700; letter-spacing:.04em; text-transform:uppercase; color:var(--ink-soft);}
  .known-btn{display:flex; justify-content:space-between; align-items:center; gap:10px; text-align:left; font-family:inherit; font-size:14.5px; padding:10px 12px; border:1.5px solid var(--rule); border-radius:10px; background:var(--paper); color:var(--ink); cursor:pointer;}
  .known-btn:hover{border-color:var(--navy-2);}
  .known-btn small{font-size:12px; color:var(--ink-soft);}
  .rec-card{background:var(--card); border:1px solid var(--rule); border-radius:14px; padding:18px; margin-bottom:14px;}
  .rec-card h2{font-size:19px; margin-bottom:10px;}
  .rec-card h3{font-size:15px; margin:4px 0 8px;}
  .rec-table-wrap{overflow-x:auto;}
  .rec-table{width:100%; border-collapse:collapse; font-size:13.5px; font-variant-numeric:tabular-nums;}
  .rec-table th{text-align:left; font-size:11.5px; text-transform:uppercase; letter-spacing:.04em; color:var(--ink-soft); padding:6px 8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-table td{padding:8px; border-bottom:1px solid var(--rule); white-space:nowrap;}
  .rec-bar{display:inline-block; width:70px; height:6px; border-radius:99px; background:var(--rule); overflow:hidden; vertical-align:middle; margin-right:6px;}
  .rec-bar i{display:block; height:100%; background:var(--success);}
  .rec-empty{font-size:13.5px; color:var(--ink-soft);}
  .sec-sub{max-width:900px; margin:0 auto; padding:10px 16px 0; font-size:12.5px; font-weight:700; color:var(--accent-text); letter-spacing:.02em;}
  .opt{flex-wrap:wrap;}
  .opt-l{font-family:'IBM Plex Mono',monospace; font-size:13px; font-weight:600; color:var(--ink-soft);}
  .opt-t{flex:1; min-width:0;}
  .opt.is-chosen:not(.is-correct):not(.is-wrong){border-color:var(--navy-2); background:var(--gold-soft);}
  .opt-tag{font-size:11px; font-weight:700; padding:2px 8px; border-radius:99px; background:var(--card); border:1px solid currentColor; white-space:nowrap;}
  .opt.is-correct .opt-tag{color:var(--success);} .opt.is-wrong .opt-tag{color:var(--danger);} .opt.is-chosen:not(.is-correct):not(.is-wrong) .opt-tag{color:var(--accent-text);}
  .chosen{font-size:13.5px; margin-top:10px; padding:8px 12px; border-radius:9px;}
  .chosen.ok{background:var(--success-soft); color:var(--success);} .chosen.bad{background:var(--danger-soft); color:var(--danger);}
  .chosen + .chosen{margin-top:6px;}
  .solution{margin-top:14px; border:1px solid var(--rule); border-left:4px solid var(--gold); background:var(--paper-2); border-radius:10px; padding:12px 14px;}
  .sol-h{font-family:'Fraunces',Georgia,serif; font-weight:700; font-size:14px; color:var(--accent-text); margin-bottom:6px;}
  .sol-line{font-size:14.5px; line-height:1.7;}
  .rev-sol summary{cursor:pointer; font-size:12.5px; font-weight:700; color:var(--accent-text); margin-top:6px;}
  .rev-sol .solution{margin-top:8px;}
  .chapter-credit{max-width:900px; margin:4px auto 0; font-size:12px; color:#CFD7EA;}
  footer.brandfoot a{color:inherit;}
  .blank-input.wide{width:260px; max-width:100%; font-family:'Source Sans 3',sans-serif;}
  .blank-input.expr{width:170px; max-width:100%;}
  /*fix-layout*/ .cp-fill,.sp-fill{width:0;} .fld{min-width:0;} .fld input{width:100%; min-width:0; box-sizing:border-box;}
  .fig{margin:6px 0 10px; display:flex; justify-content:center;}
  .figsvg{width:100%; max-width:340px; height:auto; overflow:visible;}
  .figsvg .ln,.figsvg .arm{stroke:var(--ink); stroke-width:1.6; fill:none;}
  .figsvg .arm{stroke:var(--accent-text); stroke-width:2;}
  .figsvg .pt{fill:var(--ink);}
  .figsvg .lb{fill:var(--ink); font:600 13px 'Source Sans 3',sans-serif;}
  .figsvg .al{fill:var(--accent-text); font:700 12px 'Source Sans 3',sans-serif;}
  .figsvg .wg{fill:var(--gold-soft); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .wg2{fill:rgba(199,154,62,.35); stroke:var(--gold); stroke-width:1.2;}
  .figsvg .ra{fill:none; stroke:var(--ink); stroke-width:1.2;}
  .figsvg .ahd{fill:var(--ink);}
  .figsvg .pr{fill:var(--paper-2); stroke:var(--ink-soft); stroke-width:1.2;}
  .figsvg .tk{stroke:var(--ink-soft); stroke-width:.8;}
  .figsvg .po{fill:var(--ink); font:600 8.5px 'IBM Plex Mono',monospace;}
  .figsvg .pi{fill:var(--danger); font:600 7.5px 'IBM Plex Mono',monospace;}
  .figsvg .sh{fill:var(--gold-soft); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh2{fill:rgba(199,154,62,.38); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .sh3{fill:rgba(199,154,62,.22); stroke:var(--ink); stroke-width:1.5; stroke-linejoin:round;}
  .figsvg .none{fill:none;}
  .figsvg .hid{stroke-dasharray:5 4; fill:none;}
  .figsvg .tick{stroke:var(--ink); stroke-width:1.4; fill:none;}
  .figsvg .shd{fill:var(--accent-text); fill-opacity:.55;}
  .figsvg .cell{fill:var(--card); stroke:var(--ink); stroke-width:1.1;}
  .figsvg .dr{fill:var(--danger);} .figsvg .dw{fill:var(--card); stroke:var(--ink); stroke-width:1.2;}
  .figsvg .dotfill{fill:var(--danger);}
  .tt{border-collapse:collapse; font-size:13.5px; margin:4px auto; font-variant-numeric:tabular-nums;} .tt th,.tt td{border:1px solid var(--rule); padding:4px 9px; text-align:left;} .tt th{background:var(--paper-2); font-weight:700;} .ttw{overflow-x:auto; max-width:100%;}
  .fq{display:inline-flex; flex-direction:column; vertical-align:middle; text-align:center; font-size:.82em; line-height:1.12; margin:0 2px;}
  .fq>span:first-child{border-bottom:1.5px solid currentColor; padding:0 2px;}
  .fq>span:last-child{padding:0 2px;}
  .mx{white-space:nowrap;}
  .blank-input.fr{width:110px;}
  @media (prefers-reduced-motion:reduce){ *{transition:none !important;} }
.datline{display:block;margin-top:8px;padding:8px 10px;border-radius:8px;background:var(--paper-2);font:500 14px/1.7 'IBM Plex Mono',monospace;word-spacing:2px;overflow-wrap:anywhere;}

  .theory{display:flex;flex-direction:column;gap:16px;padding-bottom:40px;}
  .hub{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .hub{grid-template-columns:repeat(3,1fr);} }
  .hub-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:16px;display:flex;flex-direction:column;gap:8px;}
  .hub-card h3{font-family:'Fraunces',serif;font-size:18px;margin:0;color:var(--accent-text);}
  .hub-card p{margin:0;font-size:14px;color:var(--ink-soft);line-height:1.5;}
  .hub-btns{display:flex;flex-wrap:wrap;gap:8px;margin-top:auto;}
  .hub-btn{min-height:40px;border:1.5px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:10px;padding:8px 12px;font:600 14px 'Source Sans 3',sans-serif;cursor:pointer;text-align:left;}
  .hub-btn:hover{border-color:var(--gold);}
  .hub-btn.primary{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .note{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:18px;scroll-margin-top:120px;}
  .note h2{font-family:'Fraunces',serif;font-size:22px;margin:0 0 4px;color:var(--ink);}
  .note .lt{font-size:13.5px;color:var(--ink-soft);margin:0 0 12px;}
  .note .lt b{color:var(--accent-text);}
  .note h4{font:700 15px 'Source Sans 3',sans-serif;margin:16px 0 6px;color:var(--accent-text);}
  .note p,.note li{font-size:15.5px;line-height:1.6;}
  .note ul{padding-left:20px;margin:6px 0;}
  .keybox{background:var(--gold-soft);border-left:4px solid var(--gold);border-radius:8px;padding:10px 12px;margin:10px 0;font-size:15px;line-height:1.6;}
  .keybox b{color:var(--ink);}
  .ex{background:var(--paper-2);border-radius:10px;padding:12px;margin:10px 0;}
  .ex .exh{font-family:'Fraunces',serif;font-weight:700;color:var(--accent-text);margin-bottom:4px;}
  .ex .exl{font-size:15px;line-height:1.7;}
  .ttab{width:100%;border-collapse:collapse;font-size:14.5px;margin:8px 0;}
  .ttab th,.ttab td{border:1px solid var(--rule);padding:7px 8px;text-align:left;vertical-align:top;}
  .ttab th{background:var(--paper-2);}
  .tscroll{overflow-x:auto;}
  .mono{font-family:'IBM Plex Mono',monospace;font-size:.92em;}
  @media (max-width:480px){ .ttab{font-size:13.5px;} .ttab th,.ttab td{padding:6px;} }
  .note .figsvg{max-width:100%;height:auto;display:block;margin:8px auto;}


  .rep-top{display:flex;flex-wrap:wrap;gap:18px;align-items:center;justify-content:center;margin-top:8px;}
  .rep-legend{flex:1;min-width:220px;display:flex;flex-direction:column;gap:8px;}
  .rep-cap{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.05em;}
  .rep-li{display:flex;align-items:center;gap:6px;font-size:15px;}
  .rep-n{margin-left:auto;white-space:nowrap;padding-left:8px;font-family:'IBM Plex Mono',monospace;font-weight:600;}
  .sw{display:inline-block;width:12px;height:12px;border-radius:3px;flex:none;}
  .rep-grid{display:grid;grid-template-columns:1fr;gap:12px;}
  @media (min-width:640px){ .rep-grid{grid-template-columns:1fr 1fr;} }
  .rep-card{background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:14px;display:flex;flex-direction:column;gap:10px;}
  .rep-h{display:flex;align-items:center;gap:8px;font:700 16px 'Source Sans 3',sans-serif;}
  .crit{display:inline-grid;place-items:center;width:28px;height:28px;border-radius:50%;color:var(--card);font:700 15px Fraunces,serif;flex:none;}
  .rep-row{display:flex;gap:14px;align-items:center;}
  .rep-stats{display:flex;flex-direction:column;gap:5px;font-size:14.5px;}
  .rep-stats div{display:flex;align-items:center;gap:6px;}
  .rep-lvl{margin-top:4px;color:var(--accent-text);} .rep-lvl span{color:var(--ink-soft);font-size:13px;}
  .rep-note{font-size:13px;color:var(--ink-soft);}


  .skip-chips{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin:12px 0;}
  .skip-chips .chip{min-width:48px;min-height:40px;cursor:pointer;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--retry-text);border-radius:10px;font:600 14px 'IBM Plex Mono',monospace;}
  .skip-btns{display:flex;flex-wrap:wrap;gap:10px;justify-content:center;margin-top:12px;}


  .kb-toggle{border:none;background:transparent;font-size:15px;cursor:pointer;padding:0 2px;vertical-align:middle;opacity:.7;}
  .vkb{position:fixed;left:0;right:0;bottom:0;z-index:80;background:var(--paper-2);border-top:1px solid var(--rule);box-shadow:0 -6px 20px rgba(0,0,0,.12);padding:6px 6px 8px;display:none;}
  .vkb.show{display:block;}
  .vkb-top{display:flex;justify-content:space-between;align-items:center;max-width:640px;margin:0 auto 4px;font:600 12px 'Source Sans 3',sans-serif;color:var(--ink-soft);}
  .vkb-link{border:none;background:none;color:var(--accent-text);font:600 12px 'Source Sans 3',sans-serif;cursor:pointer;text-decoration:underline;}
  .vkb-row{display:flex;gap:5px;max-width:640px;margin:0 auto 5px;}
  .vkb-k{flex:1;min-height:42px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 17px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .vkb-k.fn{font:600 13px 'Source Sans 3',sans-serif;background:var(--gold-soft);}
  .vkb-k.done{background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .vkb-k:active{transform:scale(.96);}
  body.kb-open .wrap{padding-bottom:360px;}
  body.kb-open .fab{display:none;}
  .tool-bar{display:flex;gap:8px;flex-wrap:wrap;margin:-4px 0 10px;}
  .tool-btn{min-height:36px;border:1.5px solid var(--gold);background:var(--gold-soft);color:var(--ink);border-radius:18px;padding:4px 12px;font:600 13.5px 'Source Sans 3',sans-serif;cursor:pointer;}
  .tool-panel{position:fixed;z-index:85;background:var(--card);border:1px solid var(--rule);border-radius:14px;box-shadow:0 10px 30px rgba(0,0,0,.25);display:none;}
  .tool-panel.show{display:block;}
  .tp-head{display:flex;align-items:center;gap:8px;padding:8px 10px;border-bottom:1px solid var(--rule);font:600 14px 'Source Sans 3',sans-serif;}
  .tp-note{font-size:12px;color:var(--ink-soft);font-weight:500;}
  .tp-x{margin-left:auto;border:1px solid var(--rule);background:var(--paper-2);color:var(--ink);border-radius:8px;min-height:32px;padding:2px 10px;cursor:pointer;font:600 13px 'Source Sans 3',sans-serif;}
  .tp-x + .tp-x{margin-left:0;}
  .calc{right:12px;bottom:84px;width:min(330px,calc(100vw - 24px));}
  body.calc-open .wrap{padding-bottom:440px;}
  body.calc-open .fab{display:none;}
  @media (max-width:640px){ .calc{left:6px;right:6px;width:auto;} .calc-keys button{min-height:36px;} }
  .calc-disp{padding:8px 12px;text-align:right;background:var(--paper-2);}
  .calc-expr{font:500 13px 'IBM Plex Mono',monospace;color:var(--ink-soft);min-height:18px;word-break:break-all;}
  .calc-res{font:600 24px 'IBM Plex Mono',monospace;color:var(--ink);word-break:break-all;}
  .calc-keys{display:grid;grid-template-columns:repeat(6,1fr);gap:5px;padding:8px;}
  .calc-keys button{min-height:40px;border:1px solid var(--rule);border-radius:8px;background:var(--card);color:var(--ink);font:600 14px 'IBM Plex Mono',monospace;cursor:pointer;padding:0;}
  .calc-keys button.fn{background:var(--gold-soft);font-family:'Source Sans 3',sans-serif;font-size:13px;}
  .calc-keys button.eq{grid-column:span 2;background:var(--navy);color:#F4EFDF;border-color:var(--navy);}
  .desmos{left:50%;top:50%;transform:translate(-50%,-50%);width:min(760px,calc(100vw - 16px));height:min(560px,calc(100vh - 90px));flex-direction:column;}
  .desmos.show{display:flex;}
  #desmosBox{flex:1;min-height:0;border-radius:0 0 14px 14px;overflow:hidden;}
  .desmos-msg{padding:24px;text-align:center;color:var(--ink-soft);}
  .chip[data-status="skipped"]{cursor:pointer;}
  .chip[data-status="answered"]{border-color:var(--accent-text);color:var(--accent-text);}


  button.crest-home{border:none;padding:0;position:relative;cursor:pointer;transition:transform .15s ease;}
  button.crest-home:hover,button.crest-home:focus-visible{transform:scale(1.06);outline:2px solid var(--gold);outline-offset:2px;}
  .crest-h{position:absolute;right:-7px;bottom:-7px;width:18px;height:18px;border-radius:50%;background:#F4EFDF;color:var(--navy);font:700 12px/18px 'Source Sans 3',sans-serif;text-align:center;box-shadow:0 1px 3px rgba(0,0,0,.3);}
  .brand .brand-row{position:relative;}
  .bmasw{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);display:flex;flex-shrink:0;white-space:nowrap;align-items:center;gap:6px;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.25);border-radius:99px;padding:5px 14px;color:#F4EFDF;}
  .bmasw-ic{font-size:16px;} .bmasw-t{font:600 20px 'IBM Plex Mono',monospace;letter-spacing:.02em;min-width:62px;text-align:center;}
  .bmasw-b{border:none;background:rgba(255,255,255,.18);color:#F4EFDF;border-radius:50%;width:30px;height:30px;cursor:pointer;font-size:13px;}
  .bmasw.off{display:none;}
  @media (max-width:560px){ .bmasw{position:static;transform:none;margin-left:auto;padding:4px 5px 4px 8px;gap:4px;} .bmasw-ic{display:none;} .bmasw-t{font-size:16px;min-width:48px;} .bmasw-b{width:26px;height:26px;} .brand .series-name{font-size:15px;} .brand .brand-name{font-size:10.5px;} .brand .brand-row>div:not(.bmasw){min-width:0;} }
  .bmasw-done{font:600 15px 'IBM Plex Mono',monospace;color:var(--accent-text);margin:4px 0 8px;}
  .sp-fab{position:fixed;left:14px;bottom:84px;z-index:60;border:1.5px solid var(--navy-2);background:var(--card);color:var(--ink);border-radius:99px;padding:9px 14px;font:700 14px 'Source Sans 3',sans-serif;box-shadow:0 4px 14px rgba(0,0,0,.15);cursor:pointer;}
  .sp-fab.on{background:var(--navy);color:#F4EFDF;}
  body.kb-open .sp-fab{display:none;}
  .sp-canvas{position:absolute;z-index:55;display:none;touch-action:none;cursor:crosshair;}
  .sp-canvas.passive{pointer-events:none;cursor:default;}
  .sp-bar{position:fixed;top:8px;left:8px;right:8px;margin:0 auto;width:max-content;z-index:90;display:none;align-items:center;gap:6px;background:var(--card);border:1px solid var(--rule);border-radius:14px;padding:6px 8px;box-shadow:0 6px 20px rgba(0,0,0,.2);max-width:calc(100vw - 16px);flex-wrap:wrap;justify-content:center;}
  .sp-lbl{font:700 13px 'Source Sans 3',sans-serif;color:var(--ink-soft);margin-right:2px;}
  .sp-pen,.sp-tool{width:38px;height:38px;border-radius:10px;border:1.5px solid var(--rule);background:var(--paper);cursor:pointer;display:inline-flex;align-items:center;justify-content:center;font-size:17px;padding:0;color:var(--ink);}
  .sp-pen i{width:20px;height:20px;border-radius:50%;display:block;}
  .sp-pen.on,.sp-tool.on{border-color:var(--navy-2);box-shadow:0 0 0 3px var(--gold-soft);}
  @media (max-width:560px){ .sp-lbl{display:none;} .sp-pen,.sp-tool{width:34px;height:34px;} .sp-fab span{display:none;} }

  /* larger reading sizes */
  .chapter-eyebrow{font-size:13.5px;}
  .chapter-title{font-size:36px;line-height:1.15;}
  .chapter-sub{font-size:16.5px;}
  .tab-btn{font-size:15.5px;}
  .sec-sub{font-size:15px;}
  .qtext{font-size:19px;line-height:1.55;}
  .qnum{width:36px;height:36px;font-size:16px;}
  .opt{font-size:17.5px;padding:12px 14px;}
  .step-line{font-size:17.5px;line-height:2;}
  .blank-input{font-size:16px;}
  .sol-line{font-size:16.5px;}
  .feedback{font-size:15px;}
  .note h2{font-size:28px;}
  .note h4{font-size:19px;}
  .note p,.note li{font-size:17.5px;line-height:1.65;}
  .note .lt{font-size:15.5px;}
  .ex .exh{font-size:18px;} .ex .exl{font-size:16.5px;}
  .keybox{font-size:16.5px;}
  .ttab{font-size:15.5px;}
  .hub-card h3{font-size:21px;} .hub-card p{font-size:15.5px;} .hub-btn{font-size:15px;}
  @media (max-width:480px){ .chapter-title{font-size:30px;} .qtext{font-size:18px;} .opt,.step-line{font-size:16.5px;} .note h2{font-size:24px;} .note p,.note li{font-size:16.5px;} }

  /* v4 celebration */
  .v4conf{position:fixed;inset:0;width:100vw;height:100vh;pointer-events:none;z-index:9999;}
  .v4ban{background:linear-gradient(135deg,var(--gold-soft),var(--card));border:2px solid var(--gold);border-radius:18px;padding:18px 14px 16px;margin:-4px 0 18px;text-align:center;animation:v4pop .55s cubic-bezier(.2,1.6,.4,1);}
  @keyframes v4pop{0%{transform:scale(.6);opacity:0}100%{transform:scale(1);opacity:1}}
  .v4trophy{font-size:54px;line-height:1;animation:v4bob 1.4s ease-in-out infinite;}
  @keyframes v4bob{0%,100%{transform:translateY(0) rotate(-6deg)}50%{transform:translateY(-6px) rotate(6deg)}}
  .v4h{font-size:28px;font-weight:800;color:var(--accent-text);margin-top:6px;}
  .v4m{font-size:19px;color:var(--ink);margin-top:4px;}
  .v4pills{display:flex;flex-wrap:wrap;gap:8px;justify-content:center;margin-top:12px;}
  .v4p{font-size:16px;font-weight:700;border-radius:999px;padding:6px 12px;}
  .v4p.g{background:var(--success-soft);color:var(--success);} .v4p.o{background:var(--gold-soft);color:var(--retry-text);}
  .v4p.r{background:var(--danger-soft);color:var(--danger);} .v4p.s{background:var(--rule);color:var(--ink);}
  .v4next{margin-top:14px;} .v4go{font-size:18px !important;padding:13px 20px !important;}
  .v4rec td.v4g{color:var(--success);font-weight:700;} .v4rec td.v4o{color:var(--retry-text);font-weight:700;} .v4rec td.v4r{color:var(--danger);font-weight:700;}
  .v4rec tr.v4tot td{font-weight:800;border-top:2px solid var(--rule);}
  .v4rec th{font-size:12.5px;padding:6px 3px !important;white-space:nowrap;} .v4rec td{font-size:15px;padding:7px 3px !important;text-align:center;}
  .v4rec td:first-child,.v4rec th:first-child{text-align:left;white-space:normal;min-width:92px;max-width:150px;font-size:14.5px;}
  @media(max-width:460px){ .v4left{display:none;} }
  .v4leg{font-size:14.5px;color:var(--ink-soft);margin:2px 0 8px;line-height:1.5;}
  body.v4done .fab-q,body.v4done #qFab{display:none;}
  .v4sum{font-size:16px;margin-top:10px;}
  /* v4 larger reading sizes */
  body{font-size:18px;}
  .chapter-title{font-size:38px !important;line-height:1.15;}
  .chapter-sub{font-size:17px !important;}
  .tab-btn{font-size:16.5px !important;}
  .sec-sub{font-size:16.5px !important;}
  .qtext{font-size:21px !important;line-height:1.6 !important;}
  .qnum{width:38px !important;height:38px !important;font-size:17px !important;}
  .opt{font-size:19.5px !important;padding:13px 15px !important;}
  .step-line{font-size:19.5px !important;line-height:2.1 !important;}
  .blank-input{font-size:18px !important;min-height:40px;}
  .sol-line{font-size:18px !important;line-height:1.6;}
  .feedback{font-size:16.5px !important;}
  .note h2{font-size:29px !important;}
  .note h3{font-size:22px !important;}
  .note h4{font-size:20px !important;}
  .note p,.note li,.note td,.note th{font-size:18.5px !important;line-height:1.7 !important;}
  .ex .exh{font-size:19px !important;} .ex .exl{font-size:18px !important;}
  .keybox{font-size:18px !important;}
  .hub-card p{font-size:17.5px !important;} .hub-btn{font-size:16.5px !important;}
  .review-q,.review-ans{font-size:17.5px !important;}
  .rec-table td{font-size:16px;}
  .vkb-k{font-size:19px !important;}
  .fq{font-size:0.95em;}
</style>
</head>
<body>
<header class="brand">
  <div class="brand-row">
    <div class="crest">BM</div>
    <div>
      <div class="brand-name">Brain &amp; Mind Academy</div>
      <div class="series-name">Sopaan <span style="font-weight:400;font-size:14px;color:#CFD7EA;">Practice Series</span></div>
    </div>
  </div>
  <div class="chapter-eyebrow">Algebra 1 · Chapter 1</div>
  <div class="chapter-title">Solving Linear Equations</div>
  <div class="chapter-sub">Theory Notes · Practice by Section · Learning Assessment</div><div class="chapter-credit">Follows the sections of Big Ideas Math Algebra 1, Chapter 1</div>
  <div class="chapter-progress">
    <div class="cp-track"><div class="cp-fill" id="cpFill"></div></div>
    <div class="cp-label" id="cpLabel">0% complete</div>
  </div>
  <div class="who-row"><button class="mode-pill" id="modePill" hidden>Choose a mode</button><span class="who" id="whoBar" hidden></span></div>
</header>

<nav class="tabbar"><div class="tabbar-inner" id="tabbar"></div></nav>
<div class="sec-sub" id="secSub"></div><div class="slide-progress"><div class="sp-track"><div class="sp-fill" id="spFill"></div></div><div class="sp-label" id="spLabel">Question 1 of 49</div></div>
<div class="wrap" id="wrap"></div>
<footer class="brandfoot">Brain &amp; Mind Academy · Sopaan Practice Series · Algebra 1 · Chapter 1<br>Lessons follow the chapter and section structure of <i>Big Ideas Math Algebra 1</i> (2015), Chapter 1. Theory notes, questions, learning assessments and worked solutions are written by Brain &amp; Mind Academy.</footer>

<div class="navbar"><div class="navbar-inner" id="navbarInner"></div></div>
<button class="fab" id="paletteFab"><span>Questions</span><span class="fab-badge" id="fabBadge">0/49</span></button>

<div class="overlay" id="overlay">
  <div class="palette" role="dialog" aria-label="Question palette">
    <div class="palette-head"><h2 id="paletteTitle">Question palette</h2><button class="palette-close" id="paletteClose">&times;</button></div>
    <div class="palette-legend">
      <span><i class="dot current"></i>Current</span><span><i class="dot correct"></i>Correct</span>
      <span><i class="dot revealed"></i>Revealed</span><span><i class="dot skipped"></i>Skipped</span>
      <span><i class="dot locked"></i>Locked</span>
    </div>
    <div class="chip-grid" id="paletteBody"></div>
  </div>
</div>
<div class="toast" id="toast"></div>

<script>
(function(){
"use strict";

/* ================= audio ================= */
var audioCtx=null;
function ensureAudio(){ if(!audioCtx){ try{ audioCtx=new (window.AudioContext||window.webkitAudioContext)(); }catch(e){} } return audioCtx; }
function playTone(freqs,dur,type){
  var ctx=ensureAudio(); if(!ctx) return;
  try{
    var t0=ctx.currentTime;
    freqs.forEach(function(f,i){
      var o=ctx.createOscillator(), g=ctx.createGain();
      o.type=type||'sine'; o.frequency.value=f;
      var start=t0+i*dur;
      g.gain.setValueAtTime(0.0001,start);
      g.gain.exponentialRampToValueAtTime(0.16,start+0.02);
      g.gain.exponentialRampToValueAtTime(0.0001,start+dur);
      o.connect(g); g.connect(ctx.destination);
      o.start(start); o.stop(start+dur+0.02);
    });
  }catch(e){}
}
function playSuccess(){ playTone([523.25,659.25,783.99],0.11,'sine'); }
function playWrong(){ playTone([220,185],0.14,'square'); }
function playReveal(){ playTone([300,220],0.16,'triangle'); }

/* ================= helpers ================= */
function norm(s){
  return String(s===undefined||s===null?'':s).trim().toLowerCase().replace(/\s+/g,'')
    .replace(/[×∗*·]/g,'x').replace(/÷/g,'/').replace(/–|—|−/g,'-')
    .replace(/[²]/g,'^2').replace(/[³]/g,'^3').replace(/[⁴]/g,'^4').replace(/[⁵]/g,'^5')
    .replace(/[⁶]/g,'^6').replace(/[⁷]/g,'^7').replace(/[⁸]/g,'^8').replace(/[⁹]/g,'^9')
    .replace(/\^/g,'');
}
function parseNum(s){
  if(s===undefined||s===null) return null;
  var t=String(s).trim().replace(/,/g,'').replace(/[−–—]/g,'-').replace(/\s+/g,''); if(t==='') return null;
  var neg=false; if(t[0]==='-'){neg=true;t=t.slice(1);}
  var m=t.match(/^(\d+)\/(\d+)$/);
  if(m){ var v=parseInt(m[1],10)/parseInt(m[2],10); return neg?-v:v; }
  if(/^\d+(\.\d+)?$/.test(t)){ var v2=parseFloat(t); return neg?-v2:v2; }
  return null;
}
/* ---- expression checker: compares answers like (P-2w)/2 and P/2-w at random values ---- */
function exprPrep(s){
  return String(s).toLowerCase().replace(/\s+/g,'').replace(/^[a-z]\(x\)=/i,'').replace(/^[a-z]=/i,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^2').replace(/³/g,'^3').replace(/⁴/g,'^4').replace(/⁵/g,'^5').replace(/⁶/g,'^6').replace(/⁷/g,'^7').replace(/⁸/g,'^8').replace(/⁹/g,'^9').replace(/π/g,'#').replace(/pi/gi,'#').replace(/½/g,'(1/2)');
}
function exprCompile(src){
  var s=exprPrep(src), i=0, toks=[], absDepth=0;
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length && /[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(/[a-zA-Z#]/.test(ch)){ toks.push({k:'v',v:ch}); i++; continue; }
    if(ch==='|'){ var pv=toks[toks.length-1]; var opn=(absDepth===0)||!pv||('+-*/^(['.indexOf(pv.k)>=0); if(opn){ absDepth++; toks.push({k:'['}); } else { absDepth--; toks.push({k:']'}); } i++; continue; }
    if('+-*/^()'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  var out=[];
  for(var t=0;t<toks.length;t++){
    var a=toks[t], b=out[out.length-1];
    if(b && (b.k==='n'||b.k==='v'||b.k===')'||b.k===']') && (a.k==='n'||a.k==='v'||a.k==='('||a.k==='[')) out.push({k:'&'});
    out.push(a);
  }
  var p=0;
  function peek(){ return out[p]; }
  function parseE(){ var n=parseT(); while(peek() && (peek().k==='+'||peek().k==='-')){ var o=out[p++].k, r=parseT(); n=(function(l,r,o){return function(e){ return o==='+'?l(e)+r(e):l(e)-r(e); };})(n,r,o); } return n; }
  function parseI(){ var n=parseU(); while(peek() && peek().k==='&'){ p++; var r=parseP(); n=(function(l,r){return function(e){ return l(e)*r(e); };})(n,r); } return n; }
  function parseT(){ var n=parseI(); while(peek() && (peek().k==='*'||peek().k==='/')){ var o=out[p++].k, r=parseI(); n=(function(l,r,o){return function(e){ return o==='*'?l(e)*r(e):l(e)/r(e); };})(n,r,o); } return n; }
  function parseU(){ if(peek() && peek().k==='-'){ p++; var u=parseU(); return function(e){ return -u(e); }; } if(peek() && peek().k==='+'){ p++; return parseU(); } return parseP(); }
  function parseP(){ var b=parseA(); if(peek() && peek().k==='^'){ p++; var x=parseU(); return function(e){ return Math.pow(b(e),x(e)); }; } return b; }
  function parseA(){
    var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){ return t.v; };
    if(t.k==='v') return t.v==='#' ? function(){ return Math.PI; } : function(e){ return e[t.v]; };
    if(t.k==='('){ var n=parseE(); if(!peek()||peek().k!==')') throw 0; p++; return n; }
    if(t.k==='['){ var m=parseE(); if(!peek()||peek().k!==']') throw 0; p++; return function(e){ return Math.abs(m(e)); }; }
    throw 0;
  }
  try{ var f=parseE(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function exprEqual(input,answer){
  var f=exprCompile(input), g=exprCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<8;trial++){
    var env={}; 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=1.3+Math.random()*4.1; });
    var x=f(env), y=g(env);
    if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-7*Math.max(1,Math.abs(x),Math.abs(y))) return false;
    hits++;
  }
  return hits>=3;
}
function wordsNorm(s){ return String(s||'').toLowerCase().replace(/\band\b/g,' ').replace(/[^a-z]/g,''); }
function listNorm(s){ return (String(s||'').replace(/[−–—]/g,'-').replace(/(\d) (?=\d{3}\b)/g,'$1').match(/-?\d+(\.\d+)?/g)||[]).join(','); }
function powNorm(s){ return String(s||'').toLowerCase().replace(/\s+/g,'').replace(/[×∗*·.]/g,'x').replace(/[⁰¹²³⁴⁵⁶⁷⁸⁹]+/g,function(m){ return '^'+m.split('').map(function(c){ return '⁰¹²³⁴⁵⁶⁷⁸⁹'.indexOf(c); }).join(''); }).replace(/\^1(?!\d)/g,''); }
function fr(s){ return String(s).replace(/\{(\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>').replace(/\{(\d+)\/(\d+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); }
function gcdI(a,b){ a=Math.abs(a); b=Math.abs(b); while(b){ var t=a%b; a=b; b=t; } return a; }
function fracParse(s){ s=String(s===undefined||s===null?'':s).trim().replace(/[\u2044\u2215\u00f7]/g,'/').replace(/\s+/g,' ').replace(/\s*\/\s*/g,'/'); var m;
  if((m=s.match(/^(-?\d+)$/))) return {v:+m[1],form:'int',n:+m[1],d:1};
  if((m=s.match(/^(-?\d+)\/(\d+)$/))){ if(+m[2]===0) return null; return {v:m[1]/m[2],form:'frac',n:+m[1],d:+m[2]}; }
  if((m=s.match(/^(-?)(\d+)(?: |\+)(\d+)\/(\d+)$/))){ if(+m[4]===0) return null; var sg=m[1]?-1:1; return {v:sg*(+m[2]+m[3]/m[4]),form:'mixed',w:sg*m[2],n:+m[3],d:+m[4]}; }
  if((m=s.match(/^-?\d*\.\d+$/))) return {v:parseFloat(s),form:'dec'};
  return null; }
function fracOK(mode,input,answer){
  if(mode==='flist'){ var A=String(input).split(/[,;]/).map(function(x){return x.trim();}).filter(Boolean), K=String(answer).split(/[,;]/).map(function(x){return x.trim();});
    if(A.length!==K.length) return false; return A.every(function(x,i){ var a=fracParse(x), k=fracParse(K[i]); return a&&k&&Math.abs(a.v-k.v)<1e-9; }); }
  var a=fracParse(input), k=fracParse(answer); if(!a||!k) return false;
  var same=Math.abs(a.v-k.v)<1e-9; if(!same) return false;
  if(mode==='fv') return true;
  if(mode==='dec') return a.form==='dec'||a.form==='int';
  if(mode==='fe') return (a.form==='frac'&&k.form==='frac'&&a.n===k.n&&a.d===k.d)||(a.form==='int'&&k.form==='int');
  if(mode==='fi') return a.form==='frac'||(a.form==='int'&&k.form==='int');
  if(mode==='fl') return a.form==='int'||(a.form==='frac'&&gcdI(a.n,a.d)===1)||(a.form==='mixed'&&a.n<a.d&&gcdI(a.n,a.d)===1);
  if(mode==='fm') return a.form==='int'||(a.form==='mixed'&&a.n>0&&a.n<a.d&&gcdI(a.n,a.d)===1);
  return false; }
function answerMatches(input,answer,accept,expr){
  if(expr==='dec'||expr==='fv'||expr==='fe'||expr==='fl'||expr==='fm'||expr==='fi'||expr==='flist'){ if(input===undefined||input===null||String(input).trim()==='') return false; return fracOK(expr,input,answer); }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  if(expr==='words'){ return [answer].concat(accept||[]).some(function(a){ if(/\d/.test(a)) return norm(a)===norm(input); var w=wordsNorm(a); return w!=='' && w===wordsNorm(input); }); }
  if(expr==='list'){ return [answer].concat(accept||[]).some(function(a){ return listNorm(a)===listNorm(input); }); }
  if(expr==='pow'){ return [answer].concat(accept||[]).some(function(a){ return powNorm(a)===powNorm(input); }); }
  if(expr==='time'){ var tn=function(x){ var t=String(x).toLowerCase().replace(/[\s.]/g,'').replace(/[:h]/g,''); if(/^\d{3}(am|pm)?$/.test(t)) t='0'+t; return t; }; return [answer].concat(accept||[]).some(function(a){ return tn(a)===tn(input); }); }
  if(expr==='glist'){ var gn=function(x){ return String(x).toUpperCase().split(/[\s,;]+/).filter(Boolean).sort().join(','); }; return [answer].concat(accept||[]).some(function(a){ return gn(a)===gn(input); }); }
  if(expr==='coord'){ var cn=function(x){ return String(x).replace(/[\u2212\u2013\u2014]/g,'-').replace(/[\s()\[\]]/g,''); }; return [answer].concat(accept||[]).some(function(a){ return cn(a)===cn(input); }); }
  if(expr==='dlist'){ var dn=function(x){ return (String(x).replace(/[−–—]/g,'-').match(/-?\d*\.?\d+/g)||[]).map(Number).join(','); }; return [answer].concat(accept||[]).some(function(a){ return dn(a)===dn(input); }); }
  if(expr==='set'){ var sn=function(x){ return (String(x).match(/-?\d+/g)||[]).map(Number).sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return sn(a)===sn(input); }); }
  if(expr==='primes'){ var pn=function(x){ var t=powNorm(x).replace(/[^0-9x^]/g,''); var out=[]; t.split('x').forEach(function(tok){ if(!tok) return; var m=tok.split('^'); var b=+m[0], e=m[1]?+m[1]:1; for(var i=0;i<e;i++) out.push(b); }); return out.sort(function(a,b){return a-b;}).join(','); }; return [answer].concat(accept||[]).some(function(a){ return pn(a)===pn(input); }); }
  if(expr==='angle'){ var an=function(x){ return String(x).toUpperCase().replace(/[^A-Z]/g,''); }; var k=an(answer), v=an(input); return v===k || v===k.split('').reverse().join(''); }
  if(expr==='trans'){ var tv=function(x){ var s=String(x).toLowerCase().replace(/[−–—]/g,'-').replace(/\b(units?|squares?|and|then|steps?|to|the|a)\b/g,' ').replace(/[,;.]/g,' '); var re=/(\d+)\s*(right|left|up|down|r|l|u|d)\b/g, m, dx=0, dy=0, n=0; while((m=re.exec(s))){ var v=+m[1], d=m[2][0]; if(d==='r')dx+=v; else if(d==='l')dx-=v; else if(d==='u')dy+=v; else dy-=v; n++; } if(!n||s.replace(re,'').replace(/\s+/g,'')!=='') return null; return dx+','+dy; }; var ti=tv(input); return ti!==null && [answer].concat(accept||[]).some(function(a){ return tv(a)===ti; }); }
  if(expr==='rot'){ var rv=function(x){ var s=String(x).toLowerCase().replace(/quarter[\s-]*turn/g,'90').replace(/half[\s-]*turn/g,'180').replace(/three[\s-]*quarter[\s-]*turn/g,'270'); var m=s.match(/\b(90|180|270)\b/); if(!m) return null; var a=+m[1]; if(a===180) return '180'; var dir=/anti|counter|acw|ccw/.test(s)?-1:(/clockwise|\bcw\b/.test(s)?1:0); if(!dir) return null; return String(((a*dir)%360+360)%360); }; var ri=rv(input); return ri!==null && ri===rv(answer); }
  if(expr==='expanded'){ var f=function(x){ return String(x).replace(/\s+/g,'').replace(/,/g,''); }; return [answer].concat(accept||[]).some(function(a){ return f(a)===f(input); }); }
  if(expr===true && input!==undefined && input!==null && String(input).trim()!==''){
    if(exprEqual(input,answer)) return true;
    var alt=String(input).replace(/\/\s*(\d+(?:\.\d+)?)\s*([a-zA-Z(])/g,'/$1*$2'); if(alt!==String(input) && exprEqual(alt,answer)) return true;
    return (accept||[]).some(function(a){ return exprEqual(input,a); });
  }
  if(input===undefined||input===null||String(input).trim()==='') return false;
  var n1=parseNum(input), n2=parseNum(answer);
  if(n1!==null && n2!==null){ if(Math.abs(n1-n2)<1e-3) return true; return (accept||[]).some(function(a){ var n3=parseNum(a); return n3!==null && Math.abs(n1-n3)<1e-3; }); }
  var cands=[answer].concat(accept||[]); var ni=norm(input);
  for(var i=0;i<cands.length;i++){ if(norm(cands[i])===ni) return true; }
  return false;
}
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;'); }

/* ================= DATA ================= */
var AR_OPTIONS = ["Both A and R are true, and R is the correct explanation of A","Both A and R are true, but R is NOT the correct explanation of A","A is true but R is false","A is false but R is true"];
var THEORY = "<div class=\"hub\"><div class=\"hub-card\"><h3>📖 Theory notes</h3><p>Explained notes for every section of the chapter, with rules in boxes, number lines, common mistakes and worked examples.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-jump=\"n11\">1.1 notes</button><button class=\"hub-btn\" data-jump=\"n12\">1.2 notes</button><button class=\"hub-btn\" data-jump=\"n13\">1.3 notes</button><button class=\"hub-btn\" data-jump=\"n14\">1.4 notes</button><button class=\"hub-btn\" data-jump=\"n15\">1.5 notes</button></div></div><div class=\"hub-card\"><h3>🎯 Practice by section</h3><p>One practice sheet for each section, easy to hard, mixing multiple-choice and fill-in-the-blank questions, with real-life problems and error-analysis items.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s1\">1.1 · Solving Simple Equations</button><button class=\"hub-btn\" data-go=\"s2\">1.2 · Solving Multi-Step Equations</button><button class=\"hub-btn\" data-go=\"s3\">1.3 · Solving Equations with Variables on Both Sides</button><button class=\"hub-btn\" data-go=\"s4\">1.4 · Solving Absolute Value Equations</button><button class=\"hub-btn\" data-go=\"s5\">1.5 · Rewriting Equations and Formulas</button></div></div><div class=\"hub-card\"><h3>📝 Learning assessment</h3><p>Four short assessments mixing all five sections, one per skill area. Take them in Quiz mode and open the report to see your results as pie charts.</p><div class=\"hub-btns\"><button class=\"hub-btn\" data-go=\"s6\">A · Knowing and understanding</button><button class=\"hub-btn\" data-go=\"s7\">B · Investigating patterns</button><button class=\"hub-btn\" data-go=\"s8\">C · Communicating</button><button class=\"hub-btn\" data-go=\"s9\">D · Applying mathematics in real-life contexts</button><button class=\"hub-btn primary\" data-go=\"report\">📊 View my report</button></div></div></div><section class=\"note\" id=\"nintro\"><h2>About this chapter</h2><p>An <b>equation</b> is a statement that two expressions are equal. <b>Solving</b> an equation means finding the value(s) of the variable that make it true. In this chapter you solve one-step, multi-step and absolute value equations, and you learn to rearrange formulas so that any variable can be the subject.</p><h4>Maintaining mathematical proficiency</h4><p>These skills from earlier grades are used on every page. Check that each example makes sense before you start 1.1.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Skill</th><th>Key idea</th><th>Example</th></tr><tr><td>Adding and subtracting integers</td><td>Subtracting a number is adding its opposite.</td><td class=\"mono\">−4 − (−9) = −4 + 9 = 5</td></tr><tr><td>Multiplying and dividing integers</td><td>Same signs → positive; different signs → negative.</td><td class=\"mono\">−6 × (−3) = 18 ;  24 ÷ (−8) = −3</td></tr><tr><td>Order of operations</td><td>Parentheses, exponents, × and ÷ left to right, + and − left to right.</td><td class=\"mono\">5 + 2(7 − 3)<sup>2</sup> = 5 + 32 = 37</td></tr><tr><td>Distributive Property</td><td>a(b + c) = ab + ac; the sign in front goes with the number.</td><td class=\"mono\">−3(x − 4) = −3x + 12</td></tr><tr><td>Combining like terms</td><td>Add the coefficients of terms with the same variable part.</td><td class=\"mono\">5y + 8 − 2y − 3 = 3y + 5</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Warm-up example · Simplify −2(3n − 5) + 4n</div><div class=\"exl\">Distribute: −6n + 10 + 4n.<br>Combine like terms: <b>−2n + 10</b>.</div></div><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Sheet</th><th>Section</th><th>Learning target</th></tr><tr><td>1.1</td><td>Solving Simple Equations</td><td>I can solve one-step linear equations using inverse operations and the properties of equality, and check my answer.</td></tr><tr><td>1.2</td><td>Solving Multi-Step Equations</td><td>I can solve equations that need several steps, including combining like terms and using the Distributive Property.</td></tr><tr><td>1.3</td><td>Solving Equations with Variables on Both Sides</td><td>I can solve equations with the variable on both sides and recognize identities and equations with no solution.</td></tr><tr><td>1.4</td><td>Solving Absolute Value Equations</td><td>I can solve absolute value equations, including equations with two absolute values, and identify extraneous solutions.</td></tr><tr><td>1.5</td><td>Rewriting Equations and Formulas</td><td>I can solve literal equations and formulas for a given variable and use them to find unknown values.</td></tr></table></div><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Assessment</th><th>Skill area</th><th>What it checks</th></tr><tr><td>A</td><td>Knowing and understanding</td><td>Solving each type of equation correctly.</td></tr><tr><td>B</td><td>Investigating patterns</td><td>How solutions change when numbers in an equation change.</td></tr><tr><td>C</td><td>Communicating</td><td>Vocabulary, explaining steps, spotting and correcting errors.</td></tr><tr><td>D</td><td>Applying mathematics in real-life contexts</td><td>Money, travel, measurement and tolerance problems.</td></tr></table></div><p><b>Tools:</b> ⏱ at the top times each tab (pause or reset it). ✏️ opens a scratchpad for rough work. Some questions have a 🧮 calculator or 📈 Desmos button. Tap the BM badge to go back to the home page.</p><p><b>Typing answers:</b> type numbers like <span class=\"mono\">-7</span>, <span class=\"mono\">2.5</span> or <span class=\"mono\">-3/4</span>. When an expression is asked for, type it like <span class=\"mono\">(P-2w)/2</span> or <span class=\"mono\">2x-7</span>; put a fraction coefficient in parentheses, e.g. <span class=\"mono\">(3/4)x</span>.</p></section><section class=\"note\" id=\"n11\"><h2>1.1 Solving Simple Equations</h2><p class=\"lt\"><b>Learning target:</b> I can solve one-step linear equations using inverse operations and the properties of equality, and check my answer.</p><h4>Key vocabulary</h4><ul><li><b>Equation:</b> a statement that two expressions are equal, such as x + 3 = 8.</li><li><b>Solution:</b> a value that makes the equation true. <b>Equivalent equations</b> have the same solutions.</li><li><b>Inverse operations:</b> operations that undo each other: + and −, × and ÷.</li></ul><p>Think of an equation as a balance. Whatever you do to one side you must do to the other, or it tips.</p><svg class=\"figsvg\" viewBox=\"0 0 300 150\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><text class=\"lb\" x=\"150.0\" y=\"10.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">x + 3 = 8 : take 3 from both pans</text><path d=\"M150,76 L130,136 L170,136 Z\" style=\"fill:var(--accent-text);opacity:.35\"/><line x1=\"40\" y1=\"76\" x2=\"260\" y2=\"76\" style=\"stroke:var(--ink);stroke-width:3\"/><line x1=\"70\" y1=\"76\" x2=\"70\" y2=\"52\" style=\"stroke:var(--ink-soft);stroke-width:1.4\"/><rect x=\"22\" y=\"24\" width=\"96\" height=\"28\" rx=\"6\" style=\"fill:var(--card);stroke:var(--accent-text);stroke-width:2\"/><text class=\"lb\" x=\"70.0\" y=\"38.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">x + 3</text><line x1=\"230\" y1=\"76\" x2=\"230\" y2=\"52\" style=\"stroke:var(--ink-soft);stroke-width:1.4\"/><rect x=\"182\" y=\"24\" width=\"96\" height=\"28\" rx=\"6\" style=\"fill:var(--card);stroke:var(--accent-text);stroke-width:2\"/><text class=\"lb\" x=\"230.0\" y=\"38.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">8</text></svg><h4>Properties of equality</h4><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Property</th><th>In words</th><th>Use it to solve</th></tr><tr><td>Addition Property of Equality</td><td>Add the same number to both sides.</td><td class=\"mono\">x − 6 = 2 → x = 8</td></tr><tr><td>Subtraction Property of Equality</td><td>Subtract the same number from both sides.</td><td class=\"mono\">x + 3 = 8 → x = 5</td></tr><tr><td>Multiplication Property of Equality</td><td>Multiply both sides by the same non-zero number.</td><td class=\"mono\">{x/4} = −2 → x = −8</td></tr><tr><td>Division Property of Equality</td><td>Divide both sides by the same non-zero number.</td><td class=\"mono\">5x = −35 → x = −7</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Worked example 1 · Add to both sides</div><div class=\"exl\">Solve n − 9 = −4.<br>Add 9 to both sides: n = −4 + 9.<br><b>n = 5</b>. Check: 5 − 9 = −4 ✓</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Divide by a negative</div><div class=\"exl\">Solve −7w = 56.<br>Divide both sides by −7: w = {56/−7}.<br><b>w = −8</b>. Check: −7(−8) = 56 ✓</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Fraction coefficient</div><div class=\"exl\">Solve {2/5}k = 6.<br>Multiply both sides by the reciprocal {5/2}: k = 6 × {5/2}.<br><b>k = 15</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 4 · Real life</div><div class=\"exl\">A hiker is 1,340 ft higher after climbing, now at 5,120 ft. Where did she start?<br>Let s be the start height: s + 1340 = 5120.<br>Subtract 1340: <b>s = 3,780 ft</b>.</div></div><div class=\"keybox\"><b>Common mistake.</b> To undo “− 9” you <b>add</b> 9; to undo “× (−7)” you divide by <b>−7</b>, not by 7. Always check by substituting your answer into the <b>original</b> equation.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s1\">Practise 1.1 →</button></div></section><section class=\"note\" id=\"n12\"><h2>1.2 Solving Multi-Step Equations</h2><p class=\"lt\"><b>Learning target:</b> I can solve equations that need several steps, including combining like terms and using the Distributive Property.</p><p>A multi-step equation is solved by <b>undoing the operations in reverse order</b>. First simplify each side, then undo addition or subtraction, then undo multiplication or division.</p><div class=\"keybox\"><b>Steps for a multi-step equation</b><br>1. Use the Distributive Property to remove parentheses.<br>2. Combine like terms on each side.<br>3. Add or subtract to get the variable term alone.<br>4. Multiply or divide to get the variable alone.<br>5. Check the solution in the original equation.</div><div class=\"ex\"><div class=\"exh\">Worked example 1 · Two steps</div><div class=\"exl\">Solve 4x − 7 = 21.<br>Add 7: 4x = 28.<br>Divide by 4: <b>x = 7</b>. Check: 4(7) − 7 = 21 ✓</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Like terms and parentheses</div><div class=\"exl\">Solve 3(y + 2) − 5y = 14.<br>Distribute: 3y + 6 − 5y = 14.<br>Combine: −2y + 6 = 14. Subtract 6: −2y = 8. Divide by −2: <b>y = −4</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Angles of a triangle</div><div class=\"exl\">The angles of a triangle are x°, 2x° and (x + 20)°.<br>x + 2x + x + 20 = 180, so 4x + 20 = 180.<br>4x = 160, <b>x = 40</b>. The angles are 40°, 80° and 60°.</div></div><h4>Consecutive integers</h4><p>Consecutive integers follow each other: n, n + 1, n + 2, … Consecutive <b>even</b> (or odd) integers go up by 2: n, n + 2, n + 4, …</p><div class=\"keybox\"><b>Common mistake.</b> Distribute a negative to <b>every</b> term: −2(x − 5) = −2x <b>+ 10</b>, not −2x − 10. Also, 3(x + 4) is 3x + 12, not 3x + 4.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s2\">Practise 1.2 →</button></div></section><section class=\"note\" id=\"n13\"><h2>1.3 Solving Equations with Variables on Both Sides</h2><p class=\"lt\"><b>Learning target:</b> I can solve equations with the variable on both sides and recognize identities and equations with no solution.</p><p>When the variable appears on both sides, use the Addition or Subtraction Property of Equality to <b>collect the variable terms on one side</b> and the numbers on the other. It is usually easiest to move the smaller variable term.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · Collect the variables</div><div class=\"exl\">Solve 8x + 3 = 5x − 12.<br>Subtract 5x: 3x + 3 = −12.<br>Subtract 3: 3x = −15. Divide by 3: <b>x = −5</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Parentheses on both sides</div><div class=\"exl\">Solve 2(m − 4) = 6(m + 2).<br>Distribute: 2m − 8 = 6m + 12.<br>Subtract 2m: −8 = 4m + 12. Subtract 12: −20 = 4m, so <b>m = −5</b>.</div></div><h4>Special cases</h4><p>Sometimes the variable terms cancel out, leaving a statement with only numbers.</p><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Left-over statement</th><th>Meaning</th><th>Example</th></tr><tr><td>always true, e.g. 6 = 6</td><td><b>identity</b>: every real number is a solution (infinitely many solutions)</td><td class=\"mono\">3(x + 2) = 3x + 6</td></tr><tr><td>always false, e.g. 6 = −1</td><td><b>no solution</b></td><td class=\"mono\">3x + 6 = 3x − 1</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Real life</div><div class=\"exl\">Gym A charges $40 to join plus $25 a month. Gym B charges $35 a month and nothing to join. When do they cost the same?<br>40 + 25m = 35m → 40 = 10m → m = 4.<br>After <b>4 months</b> both cost $140.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 4 · Mixture</div><div class=\"exl\">How many litres of a 10% salt solution must be added to 4 L of a 25% solution to make a 15% solution?<br>Salt in = salt out: 0.10x + 0.25(4) = 0.15(x + 4).<br>0.10x + 1 = 0.15x + 0.6 → 0.4 = 0.05x → <b>x = 8 L</b>.</div></div><div class=\"keybox\"><b>Common mistake.</b> When you see 0 = 0 or 5 = 5, the answer is <b>not</b> “x = 0”. It means every value works. When you see a false statement such as 0 = 7, write “no solution”.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s3\">Practise 1.3 →</button></div></section><section class=\"note\" id=\"n14\"><h2>1.4 Solving Absolute Value Equations</h2><p class=\"lt\"><b>Learning target:</b> I can solve absolute value equations, including equations with two absolute values, and identify extraneous solutions.</p><p>The <b>absolute value</b> |a| is the distance between a and 0 on a number line, so it is never negative. An <b>absolute value equation</b> has a variable inside absolute value bars. |x − 2| = 3 means “x is 3 units from 2”, so there are two answers.</p><svg class=\"figsvg\" viewBox=\"0 0 330 112\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><text class=\"lb\" x=\"165.0\" y=\"10.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">|x − 2| = 3 : the points 3 units from 2</text><line class=\"ln\" x1=\"10.0\" y1=\"72.0\" x2=\"320.0\" y2=\"72.0\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><line x1=\"22.0\" y1=\"66\" x2=\"22.0\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"22.0\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">−3</text><line x1=\"50.6\" y1=\"66\" x2=\"50.6\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"50.6\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">−2</text><line x1=\"79.2\" y1=\"66\" x2=\"79.2\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"79.2\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">−1</text><line x1=\"107.8\" y1=\"66\" x2=\"107.8\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"107.8\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">0</text><line x1=\"136.4\" y1=\"66\" x2=\"136.4\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"136.4\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">1</text><line x1=\"165.0\" y1=\"66\" x2=\"165.0\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"165.0\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text><line x1=\"193.6\" y1=\"66\" x2=\"193.6\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"193.6\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">3</text><line x1=\"222.2\" y1=\"66\" x2=\"222.2\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"222.2\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">4</text><line x1=\"250.8\" y1=\"66\" x2=\"250.8\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"250.8\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">5</text><line x1=\"279.4\" y1=\"66\" x2=\"279.4\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"279.4\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">6</text><line x1=\"308.0\" y1=\"66\" x2=\"308.0\" y2=\"78\" style=\"stroke:var(--ink);stroke-width:1.3\"/><text class=\"lb\" x=\"308.0\" y=\"91.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">7</text><path d=\"M79.2,64 Q122.1,34 165.0,64\" style=\"fill:none;stroke:var(--accent-text);stroke-width:1.8\"/><text class=\"al\" x=\"122.1\" y=\"40.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">3 units</text><path d=\"M165.0,64 Q207.9,34 250.8,64\" style=\"fill:none;stroke:var(--accent-text);stroke-width:1.8\"/><text class=\"al\" x=\"207.9\" y=\"40.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">3 units</text><circle cx=\"165.0\" cy=\"72\" r=\"5\" style=\"fill:var(--danger)\"/><text class=\"al\" x=\"165.0\" y=\"57.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2</text></svg><div class=\"keybox\"><b>Solving |ax + b| = c</b><br>1. Isolate the absolute value expression.<br>2. If c &gt; 0, write two equations: ax + b = c <b>or</b> ax + b = −c. If c = 0 there is one solution; if c &lt; 0 there is <b>no solution</b>.<br>3. Solve both equations and check.</div><div class=\"ex\"><div class=\"exh\">Worked example 1 · Isolate first</div><div class=\"exl\">Solve 2|x + 1| − 5 = 7.<br>Add 5: 2|x + 1| = 12. Divide by 2: |x + 1| = 6.<br>x + 1 = 6 or x + 1 = −6, so <b>x = 5 or x = −7</b>.</div></div><h4>Two absolute values</h4><p>|a| = |b| means a and b are equal or opposite: solve a = b <b>and</b> a = −b.</p><div class=\"ex\"><div class=\"exh\">Worked example 2 · |x − 4| = |2x + 1|</div><div class=\"exl\">Case 1: x − 4 = 2x + 1 → x = −5.<br>Case 2: x − 4 = −(2x + 1) → 3x = 3 → x = 1.<br><b>x = −5 or x = 1</b>. Check: |−9| = |−9| ✓ and |−3| = |3| ✓</div></div><h4>Extraneous solutions</h4><p>An <b>extraneous solution</b> is a value found while solving that does <b>not</b> make the original equation true. When the right side contains the variable, as in |x + 3| = 2x, you must check every answer.</p><div class=\"ex\"><div class=\"exh\">Worked example 3 · Check for extraneous solutions</div><div class=\"exl\">Solve |x + 3| = 2x.<br>Case 1: x + 3 = 2x → x = 3. Case 2: x + 3 = −2x → x = −1.<br>Check x = −1: |2| = 2 but 2(−1) = −2 ✗. The only solution is <b>x = 3</b>.</div></div><h4>Absolute deviation</h4><p>The <b>absolute deviation</b> of a value x from a given value (often the mean) is |x − mean|: how far x is from the mean, ignoring direction. If you know the deviation d, then |x − mean| = d gives the two possible values: mean − d and mean + d.</p><div class=\"ex\"><div class=\"exh\">Worked example 4 · Tolerance</div><div class=\"exl\">A 500 g bag of rice may differ from 500 g by at most 6 g. Find the extreme weights.<br>|w − 500| = 6.<br>w − 500 = −6 or 6, so <b>w = 494 g or w = 506 g</b>.</div></div><div class=\"keybox\"><b>Common mistake.</b> Do not split into two equations until the absolute value is alone. In 3|x| + 4 = 10, first get |x| = 2; writing 3x + 4 = ±10 gives wrong answers.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s4\">Practise 1.4 →</button></div></section><section class=\"note\" id=\"n15\"><h2>1.5 Rewriting Equations and Formulas</h2><p class=\"lt\"><b>Learning target:</b> I can solve literal equations and formulas for a given variable and use them to find unknown values.</p><p>A <b>literal equation</b> has two or more variables. A <b>formula</b> is a literal equation that shows how quantities are related, such as d = rt. To <b>solve for a variable</b>, use the same inverse operations as before, treating every other letter like a number.</p><div class=\"ex\"><div class=\"exh\">Worked example 1 · Solve for y</div><div class=\"exl\">Solve 5x + 2y = 8 for y.<br>Subtract 5x: 2y = 8 − 5x.<br>Divide by 2: <b>y = 4 − {5/2}x</b>.</div></div><div class=\"ex\"><div class=\"exh\">Worked example 2 · Solve for a variable that appears twice</div><div class=\"exl\">Solve y = 3x + ax for x.<br>Factor out x: y = x(3 + a).<br>Divide by (3 + a): <b>x = y ÷ (3 + a)</b>, for a ≠ −3.</div></div><h4>Useful formulas</h4><div class=\"tscroll\"><table class=\"ttab\"><tr><th>Formula</th><th>Meaning</th><th>Solved for another variable</th></tr><tr><td class=\"mono\">d = rt</td><td>distance = rate × time</td><td class=\"mono\">t = d ÷ r</td></tr><tr><td class=\"mono\">A = ℓw</td><td>area of a rectangle</td><td class=\"mono\">w = A ÷ ℓ</td></tr><tr><td class=\"mono\">P = 2ℓ + 2w</td><td>perimeter of a rectangle</td><td class=\"mono\">ℓ = (P − 2w) ÷ 2</td></tr><tr><td class=\"mono\">I = Prt</td><td>simple interest</td><td class=\"mono\">r = I ÷ (Pt)</td></tr><tr><td class=\"mono\">C = {5/9}(F − 32)</td><td>Fahrenheit to Celsius</td><td class=\"mono\">F = {9/5}C + 32</td></tr></table></div><div class=\"ex\"><div class=\"exh\">Worked example 3 · Use the rewritten formula</div><div class=\"exl\">A cyclist rides 54 miles at 12 mi/h. How long does it take?<br>t = d ÷ r = 54 ÷ 12.<br><b>t = 4.5 hours</b>.</div></div><div class=\"keybox\"><b>Common mistake.</b> Undo operations in the right order. In y = mx + b, solving for x: subtract b <b>first</b>, then divide by m: x = (y − b) ÷ m, not y ÷ m − b.</div><div class=\"hub-btns\" style=\"margin-top:12px\"><button class=\"hub-btn primary\" data-go=\"s5\">Practise 1.5 →</button></div></section><section class=\"note\" id=\"nsum\"><h2>Chapter checklist</h2><ul><li>I can solve one-step linear equations using inverse operations and the properties of equality, and check my answer.</li><li>I can solve equations that need several steps, including combining like terms and using the Distributive Property.</li><li>I can solve equations with the variable on both sides and recognize identities and equations with no solution.</li><li>I can solve absolute value equations, including equations with two absolute values, and identify extraneous solutions.</li><li>I can solve literal equations and formulas for a given variable and use them to find unknown values.</li></ul><div class=\"hub-btns\" style=\"margin-top:10px\"><button class=\"hub-btn\" data-go=\"s6\">Assessment A</button><button class=\"hub-btn\" data-go=\"s7\">Assessment B</button><button class=\"hub-btn\" data-go=\"s8\">Assessment C</button><button class=\"hub-btn\" data-go=\"s9\">Assessment D</button><button class=\"hub-btn primary\" data-go=\"report\">📊 Report</button></div></section>";
var REPORT = [["s6", "A", "Knowing and understanding"], ["s7", "B", "Investigating patterns"], ["s8", "C", "Communicating"], ["s9", "D", "Applying mathematics in real-life contexts"]];
var SECTIONS = [{"id": "s1", "label": "1.1 Solving Simple Equations", "sub": "I can solve one-step linear equations using inverse operations and the properties of equality, and check my answer.", "slides": [{"kind": "mcq", "text": "Solve x + 9 = 4.", "opts": ["x = −5", "x = 5", "x = 13", "x = −13"], "correct": 0, "tag": "", "sol": "Subtract 9 from both sides: x = 4 − 9 = −5. Check: −5 + 9 = 4 ✓ (x = 13 comes from adding 9 instead of subtracting.)"}, {"kind": "blank", "p": "Solve each equation.", "tag": "", "marks": "", "flat": [{"t": "a) y − 6 = −11: y = __B1__", "a": {"B1": "-5"}}, {"t": "b) −8 = t + 3: t = __B1__", "a": {"B1": "-11"}}, {"t": "c) 14 = p − 2.5: p = __B1__", "a": {"B1": "16.5"}}], "sol": "Add 6: y = −11 + 6 = −5.\nSubtract 3: t = −8 − 3 = −11.\nAdd 2.5: p = 14 + 2.5 = 16.5."}, {"kind": "mcq", "text": "Solve −6k = 42.", "opts": ["k = 48", "k = 7", "k = −7", "k = 36"], "correct": 2, "tag": "", "sol": "Divide both sides by −6: k = 42 ÷ (−6) = −7. Check: −6(−7) = 42 ✓"}, {"kind": "blank", "p": "Solve each equation.", "tag": "", "marks": "", "flat": [{"t": "a) {m/5} = −3: m = __B1__", "a": {"B1": "-15"}}, {"t": "b) 4.5 = 0.9r: r = __B1__", "a": {"B1": "5"}}, {"t": "c) −{2/3}z = 10: z = __B1__", "a": {"B1": "-15"}}], "sol": "Multiply both sides by 5: m = −15.\nDivide both sides by 0.9: r = 4.5 ÷ 0.9 = 5.\nMultiply both sides by −{3/2}: z = 10 × (−{3/2}) = −15."}, {"kind": "mcq", "text": "Which step solves {w/−4} = 3 in one move?", "opts": ["Multiply both sides by 4, so w = 12", "Multiply both sides by −4, so w = −12", "Add 4 to both sides, so w = 7", "Divide both sides by −4, so w = −{3/4}"], "correct": 1, "tag": "", "sol": "w is divided by −4, so undo it with the Multiplication Property of Equality: multiply both sides by −4. w = 3 × (−4) = −12. Check: −12 ÷ (−4) = 3 ✓"}, {"kind": "blank", "p": "Solve {3/4}x = −9.", "tag": "", "marks": "", "flat": [{"t": "Multiply both sides by the reciprocal of {3/4}, which is __B1__", "a": {"B1": "4/3"}, "expr": "fv"}, {"t": "x = __B1__", "a": {"B1": "-12"}}], "sol": "The reciprocal of {3/4} is {4/3}, because {3/4} × {4/3} = 1.\nx = −9 × {4/3} = −12."}, {"kind": "mcq", "text": "<b>Error analysis.</b> Jordan solved −12 = x − 5 and wrote x = −17. Which is correct?", "opts": ["Subtract 5 from both sides: x = −17 is right", "Add 12 to both sides: x = 7", "Divide both sides by −5: x = {12/5}", "Add 5 to both sides: x = −7"], "correct": 3, "tag": "", "sol": "x has 5 subtracted from it, so add 5 to both sides: −12 + 5 = x, so x = −7. Jordan subtracted 5 instead. Check: −7 − 5 = −12 ✓"}, {"kind": "blank", "p": "Solve 7 − x = 10.", "tag": "", "marks": "", "flat": [{"t": "Subtract 7 from both sides: −x = __B1__", "a": {"B1": "3"}}, {"t": "x = __B1__", "a": {"B1": "-3"}}], "sol": "10 − 7 = 3, so −x = 3.\nMultiply (or divide) both sides by −1: x = −3. Check: 7 − (−3) = 10 ✓"}, {"kind": "mcq", "text": "After spending $38 on sneakers, Maya has $67 left. Which equation and solution give the amount s she had at first?", "opts": ["s − 38 = 67; s = $29", "38 − s = 67; s = −$29", "s + 38 = 67; s = $29", "s − 38 = 67; s = $105"], "correct": 3, "tag": "", "sol": "Starting money minus $38 leaves $67: s − 38 = 67. Add 38: s = 105. She had $105."}, {"kind": "blank", "p": "A car travels at a steady 58 miles per hour. How long does it take to travel 203 miles? Use 58t = 203.", "tag": "", "marks": "", "flat": [{"t": "t = __B1__ hours", "a": {"B1": "3.5"}}], "sol": "Divide both sides by 58: t = 203 ÷ 58 = 3.5 hours.", "tools": ["calc"], "desmos": []}, {"kind": "mcq", "text": "<b>Reasoning.</b> Which equation has a negative solution?", "opts": ["{x/2} = 6", "−3x = 12", "x − 4 = 1", "x + 7 = 9"], "correct": 1, "tag": "", "sol": "−3x = 12 gives x = −4. The others give x = 5, x = 12 and x = 2, all positive."}, {"kind": "blank", "p": "At 6 a.m. the temperature in Fargo was −4 °F. By noon it was 23 °F. Let c be the change in temperature: −4 + c = 23.", "tag": "", "marks": "", "flat": [{"t": "c = __B1__ °F", "a": {"B1": "27"}}, {"t": "The temperature __B1__ (rose / fell).", "a": {"B1": "rose"}, "expr": "words", "accept": ["increased", "went up", "risen"]}], "sol": "Add 4 to both sides: c = 23 + 4 = 27.\nc is positive, so the temperature rose by 27 °F."}, {"kind": "mcq", "text": "<b>Properties of equality.</b> Which property justifies the step from {x/6} = −3 to x = −18?", "opts": ["Addition Property of Equality", "Division Property of Equality", "Subtraction Property of Equality", "Multiplication Property of Equality"], "correct": 3, "tag": "", "sol": "Both sides were multiplied by 6: {x/6} × 6 = −3 × 6. Multiplying both sides by the same non-zero number is the Multiplication Property of Equality."}, {"kind": "blank", "p": "Five friends split a restaurant bill equally. Each pays $14.60. Let b be the total bill: {b/5} = 14.60.", "tag": "", "marks": "", "flat": [{"t": "b = $__B1__", "a": {"B1": "73"}}, {"t": "To solve, you __B1__ both sides by 5 (multiply / divide).", "a": {"B1": "multiply"}, "expr": "words", "accept": ["multiplied", "times"]}], "sol": "Multiply both sides by 5: b = 14.60 × 5 = 73. Check: 73 ÷ 5 = 14.60 ✓\nb is divided by 5, so the inverse operation is multiplying by 5."}]}, {"id": "s2", "label": "1.2 Solving Multi-Step Equations", "sub": "I can solve equations that need several steps, including combining like terms and using the Distributive Property.", "slides": [{"kind": "mcq", "text": "Solve 3x + 5 = 20.", "opts": ["x = {25/3}", "x = 5", "x = −5", "x = 15"], "correct": 1, "tag": "", "sol": "Subtract 5: 3x = 15. Divide by 3: x = 5. (x = {25/3} comes from adding 5 instead of subtracting.)"}, {"kind": "blank", "p": "Solve {n/4} − 7 = −2.", "tag": "", "marks": "", "flat": [{"t": "Add 7 to both sides: {n/4} = __B1__", "a": {"B1": "5"}}, {"t": "n = __B1__", "a": {"B1": "20"}}], "sol": "−2 + 7 = 5.\nMultiply both sides by 4: n = 20. Check: 20 ÷ 4 − 7 = −2 ✓"}, {"kind": "mcq", "text": "Solve 12 − 5y = −8.", "opts": ["y = {4/5}", "y = −4", "y = 4", "y = −{4/5}"], "correct": 2, "tag": "", "sol": "Subtract 12: −5y = −20. Divide by −5: y = 4. Check: 12 − 20 = −8 ✓"}, {"kind": "blank", "p": "Solve 4x − 9 + 2x = 27.", "tag": "", "marks": "", "flat": [{"t": "Combine like terms: 6x − 9 = 27, so 6x = __B1__", "a": {"B1": "36"}}, {"t": "x = __B1__", "a": {"B1": "6"}}], "sol": "4x + 2x = 6x; add 9 to both sides: 6x = 36.\nDivide by 6: x = 6."}, {"kind": "mcq", "text": "Solve 2(x − 3) + 4 = 14.", "opts": ["x = 2", "x = {13/2}", "x = 5", "x = 8"], "correct": 3, "tag": "", "sol": "Distribute: 2x − 6 + 4 = 14, so 2x − 2 = 14. Add 2: 2x = 16, x = 8. ({13/2} comes from 2x − 3 + 4, forgetting to multiply the 3.)"}, {"kind": "blank", "p": "Solve −3(2w + 1) = 21.", "tag": "", "marks": "", "flat": [{"t": "Distribute: −6w − __B1__ = 21", "a": {"B1": "3"}}, {"t": "−6w = __B1__", "a": {"B1": "24"}}, {"t": "w = __B1__", "a": {"B1": "-4"}}], "sol": "−3 × 1 = −3, so −6w − 3 = 21.\nAdd 3: −6w = 24.\nDivide by −6: w = −4. Check: −3(−8 + 1) = −3(−7) = 21 ✓"}, {"kind": "mcq", "text": "<b>Error analysis.</b> Priya solved 5 − 2(x + 1) = 11 like this: 5 − 2x + 2 = 11, so −2x = 4 and x = −2. What is her mistake?", "opts": ["She should divide by 2, not −2; the answer is x = 2", "−2(x + 1) is −2x − 2, not −2x + 2; the answer is x = −4", "She should have subtracted 2 from 5 first; the answer is x = −8", "There is no mistake; x = −2 is correct"], "correct": 1, "tag": "", "sol": "Distribute −2 to both terms: −2x − 2. Then 5 − 2x − 2 = 11 → 3 − 2x = 11 → −2x = 8 → x = −4. Check: 5 − 2(−3) = 11 ✓"}, {"kind": "blank", "p": "Solve {2/3}(x + 6) = 10.", "tag": "", "marks": "", "flat": [{"t": "Multiply both sides by {3/2}: x + 6 = __B1__", "a": {"B1": "15"}}, {"t": "x = __B1__", "a": {"B1": "9"}}], "sol": "10 × {3/2} = 15.\nSubtract 6: x = 9. Check: {2/3}(15) = 10 ✓"}, {"kind": "mcq", "text": "The sum of three consecutive integers is 96. What are the integers?", "opts": ["30, 32, 34", "31, 32, 33", "32, 33, 34", "31, 33, 35"], "correct": 1, "tag": "", "sol": "n + (n + 1) + (n + 2) = 96 → 3n + 3 = 96 → 3n = 93 → n = 31. The integers are 31, 32 and 33. (30, 32, 34 are even, not consecutive; 31 + 33 + 35 = 99.)"}, {"kind": "blank", "p": "The angles of the triangle are x°, (2x + 15)° and (3x − 3)°. The angles of a triangle add to 180°.", "tag": "", "marks": "", "flat": [{"t": "6x + 12 = 180, so x = __B1__", "a": {"B1": "28"}}, {"t": "The largest angle is __B1__°", "a": {"B1": "81"}}], "sol": "x + 2x + 3x = 6x and 15 − 3 = 12. Subtract 12: 6x = 168, x = 28.\nThe angles are 28°, 2(28) + 15 = 71° and 3(28) − 3 = 81°. Check: 28 + 71 + 81 = 180 ✓", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 170\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><path d=\"M40,145 L262,145 L118,22 Z\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><text class=\"al\" x=\"70.0\" y=\"131.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">x°</text><text class=\"al\" x=\"200.0\" y=\"133.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">(2x + 15)°</text><text class=\"al\" x=\"122.0\" y=\"54.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">(3x − 3)°</text></svg>"}, {"kind": "mcq", "text": "A gym charges a $45 sign-up fee plus $28 per month. Liam has paid $297 in all. For how many months has he been a member?", "opts": ["9", "10", "8", "12"], "correct": 0, "tag": "", "sol": "45 + 28m = 297. Subtract 45: 28m = 252. Divide by 28: m = 9 months."}, {"kind": "blank", "p": "The length of a rectangular poster is 4 inches more than twice its width. The perimeter is 62 inches.", "tag": "", "marks": "", "flat": [{"t": "2w + 2(2w + 4) = 62 simplifies to 6w + 8 = 62, so w = __B1__ in.", "a": {"B1": "9"}}, {"t": "Length = __B1__ in.", "a": {"B1": "22"}}], "sol": "2w + 4w + 8 = 6w + 8. Subtract 8: 6w = 54, w = 9.\n2(9) + 4 = 22 in. Check: 2(9) + 2(22) = 62 ✓", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 134\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><rect x=\"70\" y=\"18\" width=\"160\" height=\"86\" style=\"fill:none;stroke:var(--ink);stroke-width:2\"/><text class=\"al\" x=\"150.0\" y=\"120.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">2w + 4</text><text class=\"al\" x=\"62.0\" y=\"61.0\" text-anchor=\"end\" dominant-baseline=\"middle\">w</text></svg>"}, {"kind": "mcq", "text": "<b>Reasoning.</b> Which of these is NOT a correct first step for solving 4(x − 2) = 20?", "opts": ["Distribute the 4 on the left side", "Multiply both sides by {1/4}", "Add 2 to both sides", "Divide both sides by 4"], "correct": 2, "tag": "", "sol": "The 2 is inside the parentheses and is multiplied by 4, so adding 2 does not undo it. Dividing by 4 (or multiplying by {1/4}) gives x − 2 = 5, and distributing gives 4x − 8 = 20; both lead to x = 7."}, {"kind": "blank", "p": "Two angles form a straight line (a linear pair), so they add to 180°. One angle is (3x − 5)° and the other is (2x + 10)°.", "tag": "", "marks": "", "flat": [{"t": "5x + 5 = 180, so x = __B1__", "a": {"B1": "35"}}, {"t": "The larger angle is __B1__°", "a": {"B1": "100"}}], "sol": "3x + 2x = 5x and −5 + 10 = 5. Subtract 5: 5x = 175, so x = 35.\n3(35) − 5 = 100° and 2(35) + 10 = 80°. Check: 100 + 80 = 180 ✓", "fig": "<svg class=\"figsvg\" viewBox=\"0 0 300 130\" role=\"img\"><defs><marker id=\"ah\" viewBox=\"0 0 10 10\" refX=\"9\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M0,1 L10,5 L0,9 z\" class=\"ahd\"/></marker><marker id=\"ahs\" viewBox=\"0 0 10 10\" refX=\"1\" refY=\"5\" markerWidth=\"7\" markerHeight=\"7\" orient=\"auto\"><path d=\"M10,1 L0,5 L10,9 z\" class=\"ahd\"/></marker></defs><line class=\"ln\" x1=\"20.0\" y1=\"100.0\" x2=\"280.0\" y2=\"100.0\" marker-end=\"url(#ah)\" marker-start=\"url(#ahs)\"/><line x1=\"150\" y1=\"100\" x2=\"166\" y2=\"14\" style=\"stroke:var(--ink);stroke-width:2\"/><path d=\"M178,100 A28,28 0 0 0 154.9,72.4\" style=\"fill:none;stroke:var(--accent-text);stroke-width:1.6\"/><path d=\"M122,100 A28,28 0 0 1 154.9,72.4\" style=\"fill:none;stroke:var(--danger);stroke-width:1.6\"/><text class=\"al\" x=\"212.0\" y=\"70.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">(2x + 10)°</text><text class=\"al\" x=\"92.0\" y=\"70.0\" text-anchor=\"middle\" dominant-baseline=\"middle\">(3x − 5)°</text></svg>"}]}, {"id": "s3", "label": "1.3 Variables on Both Sides", "sub": "I can solve equations with the variable on both sides and recognize identities and equations with no solution.", "slides": [{"kind": "mcq", "text": "Solve 7x − 4 = 3x + 12.", "opts": ["x = 4", "x = −4", "x = 1.6", "x = 2"], "correct": 0, "tag": "", "sol": "Subtract 3x: 4x − 4 = 12. Add 4: 4x = 16. x = 4. (1.6 comes from adding 3x to the left instead of subtracting.)"}, {"kind": "blank", "p": "Solve 5y + 9 = 2y − 6.", "tag": "", "marks": "", "flat": [{"t": "Subtract 2y and 9 from both sides: 3y = __B1__", "a": {"B1": "-15"}}, {"t": "y = __B1__", "a": {"B1": "-5"}}], "sol": "5y − 2y = 3y and −6 − 9 = −15.\nDivide by 3: y = −5. Check: 5(−5) + 9 = −16 and 2(−5) − 6 = −16 ✓"}, {"kind": "mcq", "text": "Solve 4(n − 3) = 2(n + 5).", "opts": ["n = −1", "n = 8.5", "n = 11", "n = 4"], "correct": 2, "tag": "", "sol": "Distribute: 4n − 12 = 2n + 10. Subtract 2n: 2n − 12 = 10. Add 12: 2n = 22, n = 11. (n = 4 comes from not distributing at all: 4n − 3 = 2n + 5.)"}, {"kind": "blank", "p": "Decide how many solutions each equation has. Type <i>one</i>, <i>no solution</i> or <i>infinitely many</i>.", "tag": "", "marks": "", "flat": [{"t": "a) 3(2x − 4) = 6x − 12: __B1__", "a": {"B1": "infinitely many"}, "expr": "words", "accept": ["infinitely many solutions", "all real numbers", "all reals", "every real number", "identity", "infinite", "infinitely many", "infinitelymany"]}, {"t": "b) 5x + 7 = 5x − 2: __B1__", "a": {"B1": "no solution"}, "expr": "words", "accept": ["no solution", "no solutions", "none", "zero", "nosolution", "empty set"]}, {"t": "c) 2x + 7 = 5x − 2: __B1__", "a": {"B1": "one"}, "expr": "words", "accept": ["one solution", "exactly one", "just one"]}], "sol": "6x − 12 = 6x − 12 is always true: an identity with infinitely many solutions.\nSubtract 5x: 7 = −2, which is false: no solution.\n3x = 9 gives exactly one solution, x = 3."}, {"kind": "mcq", "text": "Which equation is an identity?", "opts": ["2(x + 3) = 2x + 3", "2x + 3 = 2x − 3", "2(x + 3) = 2x + 6", "2x + 6 = 3x + 6"], "correct": 2, "tag": "", "sol": "2(x + 3) = 2x + 6 is true for every x. 2x + 6 = 2x + 3 and 2x + 3 = 2x − 3 have no solution; 2x + 6 = 3x + 6 has one solution (x = 0)."}, {"kind": "blank", "p": "Solve {1/2}(8x − 6) = 3x + 5.", "tag": "", "marks": "", "flat": [{"t": "Distribute: 4x − __B1__ = 3x + 5", "a": {"B1": "3"}}, {"t": "x = __B1__", "a": {"B1": "8"}}], "sol": "{1/2} × 8x = 4x and {1/2} × 6 = 3.\nSubtract 3x and add 3: x = 8. Check: {1/2}(58) = 29 and 3(8) + 5 = 29 ✓"}, {"kind": "mcq", "text": "<b>Error analysis.</b> Noah solved 6x − 5 = 2x + 11: “Add 2x to both sides: 8x − 5 = 11, so 8x = 16 and x = 2.” What should he have done?", "opts": ["Nothing; x = 2 is correct", "Divide both sides by 2 first, giving x = 2", "Add 5 first, giving 6x = 2x + 6 and x = 1.5", "Subtract 2x from both sides, giving 4x = 16 and x = 4"], "correct": 3, "tag": "", "sol": "To remove 2x from the right side you subtract 2x from both sides: 4x − 5 = 11, 4x = 16, x = 4. Check: 6(4) − 5 = 19 and 2(4) + 11 = 19 ✓"}, {"kind": "blank", "p": "Solve 0.4m + 3.2 = 1.2m − 0.8.", "tag": "", "marks": "", "flat": [{"t": "Subtract 0.4m and add 0.8: 4 = __B1__m", "a": {"B1": "0.8"}}, {"t": "m = __B1__", "a": {"B1": "5"}}], "sol": "1.2m − 0.4m = 0.8m and 3.2 + 0.8 = 4.\nDivide by 0.8: m = 5. Check: 2 + 3.2 = 5.2 and 6 − 0.8 = 5.2 ✓", "tools": ["calc"], "desmos": []}, {"kind": "mcq", "text": "<b>Reasoning.</b> For which value of a does 3x + a = 3x + 7 have infinitely many solutions?", "opts": ["a = −7", "a = 3", "a = 7", "a = 0"], "correct": 2, "tag": "", "sol": "Subtract 3x from both sides: a = 7. If a = 7 the equation is always true; for any other a it is never true (no solution)."}, {"kind": "blank", "p": "Phone plan A costs $30 a month plus $0.10 per text. Plan B costs $18 a month plus $0.25 per text. For how many texts t do they cost the same?", "tag": "", "marks": "", "flat": [{"t": "30 + 0.10t = 18 + 0.25t gives t = __B1__", "a": {"B1": "80"}}, {"t": "The cost is then $__B1__", "a": {"B1": "38"}}], "sol": "Subtract 0.10t and 18: 12 = 0.15t, so t = 12 ÷ 0.15 = 80.\n30 + 0.10(80) = 38 and 18 + 0.25(80) = 38.", "tools": ["calc"], "desmos": []}, {"kind": "mcq", "text": "A 12-inch candle burns 0.5 inch per hour. A 9-inch candle burns 0.25 inch per hour. Both are lit at the same time. When are they the same height?", "opts": ["Never", "After 6 hours", "After 4 hours", "After 12 hours"], "correct": 3, "tag": "", "sol": "12 − 0.5h = 9 − 0.25h → 3 = 0.25h → h = 12. Both are then 6 inches tall. On Desmos the two lines meet at (12, 6).", "tools": ["desmos"], "desmos": ["y=12-0.5x", "y=9-0.25x"]}, {"kind": "blank", "p": "<b>Reasoning.</b> Look at 4(x + k) = 4x + 10.", "tag": "", "marks": "", "flat": [{"t": "It has infinitely many solutions when k = __B1__", "a": {"B1": "5/2"}, "expr": "fv"}, {"t": "When k = 3, the equation has __B1__.", "a": {"B1": "no solution"}, "expr": "words", "accept": ["no solution", "no solutions", "none", "zero", "nosolution", "empty set"]}], "sol": "4x + 4k = 4x + 10 is always true when 4k = 10, so k = 2.5.\nk = 3 gives 4x + 12 = 4x + 10, so 12 = 10, which is false: no solution."}, {"kind": "mcq", "text": "<b>Mixture.</b> How many litres of a 20% juice drink must be mixed with 6 litres of a 50% juice drink to make a 30% juice drink? (0.2x + 0.5(6) = 0.3(x + 6))", "opts": ["12 litres", "18 litres", "9 litres", "3 litres"], "correct": 0, "tag": "", "sol": "0.2x + 3 = 0.3x + 1.8. Subtract 0.2x and 1.8: 1.2 = 0.1x, so x = 12 litres. Check: 2.4 + 3 = 5.4 L of juice in 18 L, and 5.4 ÷ 18 = 0.3 ✓", "tools": ["calc"], "desmos": []}, {"kind": "blank", "p": "A café mixes x pounds of coffee worth $8 per pound with 5 pounds of coffee worth $14 per pound. The blend is worth $10 per pound: 8x + 14(5) = 10(x + 5).", "tag": "", "marks": "", "flat": [{"t": "8x + 70 = 10x + 50 gives x = __B1__ pounds", "a": {"B1": "10"}}, {"t": "The blend weighs __B1__ pounds", "a": {"B1": "15"}}], "sol": "Subtract 8x and 50: 20 = 2x, so x = 10.\n10 + 5 = 15 lb. Check: 80 + 70 = 150 = 10 × 15 ✓"}]}, {"id": "s4", "label": "1.4 Absolute Value Equations", "sub": "I can solve absolute value equations, including equations with two absolute values, and identify extraneous solutions.", "slides": [{"kind": "mcq", "text": "Solve |x| = 9.", "opts": ["x = −9 only", "No solution", "x = 9 or x = −9", "x = 9 only"], "correct": 2, "tag": "", "sol": "Both 9 and −9 are 9 units from 0, so there are two solutions."}, {"kind": "blank", "p": "Solve |x − 4| = 7.", "tag": "", "marks": "", "flat": [{"t": "Smaller solution: x = __B1__", "a": {"B1": "-3"}}, {"t": "Larger solution: x = __B1__", "a": {"B1": "11"}}], "sol": "x − 4 = −7 gives x = −3.\nx − 4 = 7 gives x = 11. Both are 7 units from 4."}, {"kind": "mcq", "text": "Solve |x + 3| = 5.", "opts": ["x = 2 or x = −8", "x = 8 or x = −2", "x = 2 or x = −2", "x = 8 or x = −8"], "correct": 0, "tag": "", "sol": "x + 3 = 5 gives x = 2; x + 3 = −5 gives x = −8. (|x + 3| is the distance from −3, not from 3.)"}, {"kind": "blank", "p": "Solve 3|2y − 1| + 4 = 25.", "tag": "", "marks": "", "flat": [{"t": "Isolate the absolute value: |2y − 1| = __B1__", "a": {"B1": "7"}}, {"t": "Smaller solution: y = __B1__", "a": {"B1": "-3"}}, {"t": "Larger solution: y = __B1__", "a": {"B1": "4"}}], "sol": "Subtract 4: 3|2y − 1| = 21. Divide by 3: |2y − 1| = 7.\n2y − 1 = −7 → 2y = −6 → y = −3.\n2y − 1 = 7 → 2y = 8 → y = 4."}, {"kind": "mcq", "text": "Which equation has no solution?", "opts": ["−|x| = −4", "|x + 2| = 0", "|x − 2| + 6 = 1", "|x − 2| − 6 = 1"], "correct": 2, "tag": "", "sol": "|x − 2| + 6 = 1 gives |x − 2| = −5, and an absolute value is never negative. The others give |x − 2| = 7 (two solutions), x = −2 (one solution) and |x| = 4 (two solutions)."}, {"kind": "blank", "p": "Solve −2|m + 1| + 3 = −9.", "tag": "", "marks": "", "flat": [{"t": "|m + 1| = __B1__", "a": {"B1": "6"}}, {"t": "Smaller solution: m = __B1__", "a": {"B1": "-7"}}, {"t": "Larger solution: m = __B1__", "a": {"B1": "5"}}], "sol": "Subtract 3: −2|m + 1| = −12. Divide by −2: |m + 1| = 6.\nm + 1 = −6 → m = −7.\nm + 1 = 6 → m = 5."}, {"kind": "mcq", "text": "<b>Error analysis.</b> Ava solved |3x + 2| + 5 = 12 by writing 3x + 2 + 5 = 12 or 3x + 2 + 5 = −12. What is correct?", "opts": ["Drop the bars: 3x + 7 = 12, so x = {5/3} only", "Isolate first: |3x + 2| = 7, so x = {5/3} or x = 3", "Isolate first: |3x + 2| = 7, so x = {5/3} or x = −3", "Her work is right: x = {5/3} or x = −{19/3}"], "correct": 2, "tag": "", "sol": "Subtract 5 first: |3x + 2| = 7. Then 3x + 2 = 7 → x = {5/3}, or 3x + 2 = −7 → 3x = −9 → x = −3. Ava's second equation wrongly made the +5 negative too."}, {"kind": "blank", "p": "Solve |x − 2| = |x + 6|.", "tag": "", "marks": "", "flat": [{"t": "x − 2 = −(x + 6) gives x = __B1__", "a": {"B1": "-2"}}, {"t": "How many solutions does the equation have? __B1__", "a": {"B1": "1"}, "accept": ["one", "one solution"]}], "sol": "x − 2 = −x − 6 → 2x = −4 → x = −2. Check: |−4| = |4| ✓\nThe other case x − 2 = x + 6 gives −2 = 6, which is false, so there is only 1 solution."}, {"kind": "mcq", "text": "Solve |2x − 1| = |x + 4|.", "opts": ["x = 5 or x = 1", "x = −5 or x = 1", "x = 5 or x = −1", "x = 5 only"], "correct": 2, "tag": "", "sol": "Case 1: 2x − 1 = x + 4 → x = 5. Case 2: 2x − 1 = −(x + 4) → 3x = −3 → x = −1. Check: |9| = |9| and |−3| = |3| ✓"}, {"kind": "blank", "p": "Solve |x + 2| = 3x and check for extraneous solutions.", "tag": "", "marks": "", "flat": [{"t": "Case x + 2 = 3x gives x = __B1__", "a": {"B1": "1"}}, {"t": "Case x + 2 = −3x gives x = __B1__", "a": {"B1": "-1/2"}, "expr": "fv"}, {"t": "The only true solution is x = __B1__", "a": {"B1": "1"}}], "sol": "2 = 2x → x = 1. Check: |3| = 3 ✓\n2 = −4x → x = −{1/2}.\nCheck −{1/2}: |{3/2}| = {3/2} but 3(−{1/2}) = −{3/2}, so −{1/2} is extraneous. Only x = 1 works."}, {"kind": "mcq", "text": "A thermostat is set to 68 °F. The actual temperature can differ from the setting by 3 °F: |t − 68| = 3. What are the lowest and highest temperatures?", "opts": ["68 °F and 71 °F", "62 °F and 74 °F", "−65 °F and 71 °F", "65 °F and 71 °F"], "correct": 3, "tag": "", "sol": "t − 68 = −3 gives t = 65; t − 68 = 3 gives t = 71."}, {"kind": "blank", "p": "A box of cereal is labeled 16 ounces. The actual weight w may differ from the label by 0.4 ounce: |w − 16| = 0.4.", "tag": "", "marks": "", "flat": [{"t": "Minimum weight = __B1__ oz", "a": {"B1": "15.6"}}, {"t": "Maximum weight = __B1__ oz", "a": {"B1": "16.4"}}], "sol": "w − 16 = −0.4 → w = 15.6.\nw − 16 = 0.4 → w = 16.4."}, {"kind": "mcq", "text": "<b>Reasoning.</b> For which value of c does |x − 3| = c have exactly one solution?", "opts": ["c = −3", "c = 1", "c = 3", "c = 0"], "correct": 3, "tag": "", "sol": "|x − 3| = 0 only when x = 3. A positive c gives two solutions and a negative c gives none."}, {"kind": "blank", "p": "<b>Absolute deviation.</b> The mean of a set of test scores is 72. A score x has an absolute deviation of 9 from the mean, so |x − 72| = 9.", "tag": "", "marks": "", "flat": [{"t": "The possible scores are x = __B1__ (separate with a comma)", "a": {"B1": "63, 81"}, "expr": "set"}, {"t": "The mean absolute deviation of the two scores 63 and 81 from 72 is __B1__", "a": {"B1": "9"}}], "sol": "x − 72 = −9 gives x = 63; x − 72 = 9 gives x = 81.\n|63 − 72| = 9 and |81 − 72| = 9, so their mean is (9 + 9) ÷ 2 = 9."}]}, {"id": "s5", "label": "1.5 Rewriting Equations and Formulas", "sub": "I can solve literal equations and formulas for a given variable and use them to find unknown values.", "slides": [{"kind": "mcq", "text": "Solve 3x + 4y = 12 for y.", "opts": ["y = 3 − {3/4}x", "y = 12 − 3x", "y = 4 − {3/4}x", "y = 3 − {4/3}x"], "correct": 0, "tag": "", "sol": "Subtract 3x: 4y = 12 − 3x. Divide every term by 4: y = 3 − {3/4}x."}, {"kind": "blank", "p": "Solve 2x − y = 7 for y.", "tag": "", "marks": "", "flat": [{"t": "Subtract 2x: −y = __B1__", "a": {"B1": "7-2x"}, "expr": true, "accept": ["-2x+7"]}, {"t": "y = __B1__", "a": {"B1": "2x-7"}, "expr": true, "accept": ["-7+2x"]}], "sol": "2x − y − 2x = 7 − 2x.\nMultiply both sides by −1: y = 2x − 7."}, {"kind": "mcq", "text": "Solve A = ℓw for w.", "opts": ["w = Aℓ", "w = A − ℓ", "w = {ℓ/A}", "w = {A/ℓ}"], "correct": 3, "tag": "", "sol": "w is multiplied by ℓ, so divide both sides by ℓ: w = A ÷ ℓ."}, {"kind": "blank", "p": "Solve the perimeter formula P = 2l + 2w for l.", "tag": "", "marks": "", "flat": [{"t": "2l = __B1__", "a": {"B1": "P-2w"}, "expr": true, "accept": ["-2w+P"]}, {"t": "l = __B1__", "a": {"B1": "(P-2w)/2"}, "expr": true, "accept": ["P/2-w"]}], "sol": "Subtract 2w from both sides.\nDivide both sides by 2: l = (P − 2w) ÷ 2, which is also P ÷ 2 − w."}, {"kind": "mcq", "text": "Solve d = rt for t. Then find the time for a 150-mile trip at 60 miles per hour.", "opts": ["t = dr; 9,000 hours", "t = {d/r}; 2.5 hours", "t = {r/d}; 0.4 hour", "t = d − r; 90 hours"], "correct": 1, "tag": "", "sol": "Divide both sides by r: t = d ÷ r = 150 ÷ 60 = 2.5 hours."}, {"kind": "blank", "p": "The formula C = {5/9}(F − 32) converts Fahrenheit to Celsius.", "tag": "", "marks": "", "flat": [{"t": "Solve for F: F = __B1__", "a": {"B1": "9C/5+32"}, "expr": true, "accept": ["(9/5)C+32", "1.8C+32", "32+9C/5", "32+1.8C"]}, {"t": "A day in Houston reaches 35 °C. In Fahrenheit this is __B1__ °F", "a": {"B1": "95"}}], "sol": "Multiply by {9/5}: {9/5}C = F − 32. Add 32: F = {9/5}C + 32.\nF = {9/5}(35) + 32 = 63 + 32 = 95 °F."}, {"kind": "mcq", "text": "<b>Error analysis.</b> Diego solved y = mx + b for x and wrote x = y ÷ m − b. What is correct?", "opts": ["x = (y − b) ÷ m: subtract b before dividing by m", "x = m(y − b): multiply by m after subtracting b", "x = y ÷ m − b is correct", "x = (y + b) ÷ m: add b before dividing"], "correct": 0, "tag": "", "sol": "Undo + b first: y − b = mx. Then divide both sides by m: x = (y − b) ÷ m. Diego divided only y by m. (Test m = 2, b = 1, x = 3: y = 7, and (7 − 1) ÷ 2 = 3 ✓ but 7 ÷ 2 − 1 = 2.5 ✗.)"}, {"kind": "blank", "p": "The simple interest formula is I = Prt.", "tag": "", "marks": "", "flat": [{"t": "Solve for r: r = __B1__", "a": {"B1": "I/(Pt)"}, "expr": true, "accept": ["I/(P*t)", "I/P/t"]}, {"t": "Aisha earned $180 interest on $1,500 in 3 years. The rate is __B1__% per year", "a": {"B1": "4"}}], "sol": "Divide both sides by Pt: r = I ÷ (Pt).\nr = 180 ÷ (1500 × 3) = 180 ÷ 4500 = 0.04 = 4%.", "tools": ["calc"], "desmos": []}, {"kind": "mcq", "text": "Solve ax + b = c for x (a ≠ 0).", "opts": ["x = (c − b) ÷ a", "x = c ÷ a − b", "x = (c + b) ÷ a", "x = a(c − b)"], "correct": 0, "tag": "", "sol": "Subtract b: ax = c − b. Divide by a: x = (c − b) ÷ a. This works for every equation of the form ax + b = c."}, {"kind": "blank", "p": "The area of a triangle is A = {1/2}bh.", "tag": "", "marks": "", "flat": [{"t": "Solve for h: h = __B1__", "a": {"B1": "2A/b"}, "expr": true, "accept": ["2*A/b", "(2A)/b"]}, {"t": "A triangular sail has area 36 ft² and base 9 ft. Its height is __B1__ ft", "a": {"B1": "8"}}], "sol": "Multiply both sides by 2: 2A = bh. Divide by b: h = 2A ÷ b.\nh = 2(36) ÷ 9 = 72 ÷ 9 = 8 ft."}, {"kind": "mcq", "text": "Pens cost $4 and notebooks $5. Kai spends $60: 4x + 5y = 60, where x is pens and y is notebooks. Solve for y and find y when x = 5.", "opts": ["y = 12 − {4/5}x; 8 notebooks", "y = 12 − 4x; −8 notebooks", "y = 15 − {5/4}x; 8.75 notebooks", "y = 60 − 4x; 40 notebooks"], "correct": 0, "tag": "", "sol": "5y = 60 − 4x, so y = 12 − {4/5}x. When x = 5: y = 12 − 4 = 8 notebooks."}, {"kind": "blank", "p": "<b>Reasoning.</b> Solve 3x − 2y = 6 for x.", "tag": "", "marks": "", "flat": [{"t": "x = __B1__", "a": {"B1": "(6+2y)/3"}, "expr": true, "accept": ["2+(2/3)y", "2+2y/3"]}, {"t": "When y = 6, x = __B1__", "a": {"B1": "6"}}], "sol": "Add 2y: 3x = 6 + 2y. Divide by 3: x = (6 + 2y) ÷ 3 = 2 + {2/3}y.\nx = (6 + 12) ÷ 3 = 6. Check: 3(6) − 2(6) = 6 ✓"}, {"kind": "mcq", "text": "Solve the circumference formula C = 2πr for r.", "opts": ["r = C − 2π", "r = 2πC", "r = C ÷ 2 × π", "r = C ÷ (2π)"], "correct": 3, "tag": "", "sol": "r is multiplied by 2π, so divide both sides by 2π: r = C ÷ (2π). (C ÷ 2 × π means (C ÷ 2) × π, which multiplies by π instead of dividing.)"}, {"kind": "blank", "p": "The area of a trapezoid with parallel sides p and q and height h is A = {1/2}h(p + q).", "tag": "", "marks": "", "flat": [{"t": "Solve for h: h = __B1__", "a": {"B1": "2A/(p+q)"}, "expr": true, "accept": ["(2A)/(p+q)", "2*A/(p+q)"]}, {"t": "A trapezoid-shaped garden bed has area 60 m² and parallel sides 7 m and 13 m. Its height is __B1__ m", "a": {"B1": "6"}}], "sol": "Multiply both sides by 2: 2A = h(p + q). Divide by (p + q): h = 2A ÷ (p + q).\nh = 2(60) ÷ (7 + 13) = 120 ÷ 20 = 6 m."}]}, {"id": "s6", "label": "Assessment A", "sub": "Knowing and understanding", "slides": [{"kind": "mcq", "text": "Solve x − 12 = −5.", "opts": ["x = −7", "x = 7", "x = 17", "x = −17"], "correct": 1, "tag": "", "sol": "Add 12: x = −5 + 12 = 7."}, {"kind": "blank", "p": "Solve −4a + 9 = 29.", "tag": "", "marks": "", "flat": [{"t": "−4a = __B1__", "a": {"B1": "20"}}, {"t": "a = __B1__", "a": {"B1": "-5"}}], "sol": "Subtract 9: −4a = 20.\nDivide by −4: a = −5."}, {"kind": "mcq", "text": "Solve 3(x + 2) = x − 8.", "opts": ["x = −7", "x = −1", "x = 7", "x = −5"], "correct": 0, "tag": "", "sol": "3x + 6 = x − 8 → 2x = −14 → x = −7. (x = −5 comes from 3x + 2 = x − 8.)"}, {"kind": "blank", "p": "Solve |x + 1| = 6.", "tag": "", "marks": "", "flat": [{"t": "Smaller solution: x = __B1__", "a": {"B1": "-7"}}, {"t": "Larger solution: x = __B1__", "a": {"B1": "5"}}], "sol": "x + 1 = −6 → x = −7.\nx + 1 = 6 → x = 5."}, {"kind": "mcq", "text": "Solve V = ℓwh for ℓ.", "opts": ["ℓ = V ÷ (wh)", "ℓ = V − wh", "ℓ = (wh) ÷ V", "ℓ = Vwh"], "correct": 0, "tag": "", "sol": "Divide both sides by wh: ℓ = V ÷ (wh)."}, {"kind": "blank", "p": "Solve {x/3} + 4 = 1.", "tag": "", "marks": "", "flat": [{"t": "{x/3} = __B1__", "a": {"B1": "-3"}}, {"t": "x = __B1__", "a": {"B1": "-9"}}], "sol": "Subtract 4: {x/3} = −3.\nMultiply by 3: x = −9."}, {"kind": "mcq", "text": "Which equation has infinitely many solutions?", "opts": ["4x + 8 = 4(x − 2)", "4x − 8 = 4(x − 2)", "4x − 8 = 2(x − 4)", "4x − 8 = 4(x − 8)"], "correct": 1, "tag": "", "sol": "4(x − 2) = 4x − 8, so both sides are the same. 4x − 8 = 4x − 32 and 4x + 8 = 4x − 8 have no solution; 4x − 8 = 2x − 8 has one (x = 0)."}, {"kind": "blank", "p": "Solve 2(3y − 1) = 4y + 10.", "tag": "", "marks": "", "flat": [{"t": "6y − 2 = 4y + 10, so 2y = __B1__", "a": {"B1": "12"}}, {"t": "y = __B1__", "a": {"B1": "6"}}], "sol": "Subtract 4y and add 2: 2y = 12.\ny = 6."}, {"kind": "mcq", "text": "Solve |4x| = 20.", "opts": ["x = 5 only", "x = 5 or x = −5", "x = 16 or x = −16", "x = 80 or x = −80"], "correct": 1, "tag": "", "sol": "4x = 20 or 4x = −20, so x = 5 or x = −5."}]}, {"id": "s7", "label": "Assessment B", "sub": "Investigating patterns", "slides": [{"kind": "blank", "p": "Solve ax + 4 = 16 for different values of a and look for a pattern.", "tag": "", "marks": "", "flat": [{"t": "a = 1: x = __B1__", "a": {"B1": "12"}}, {"t": "a = 2: x = __B1__", "a": {"B1": "6"}}, {"t": "a = 3: x = __B1__", "a": {"B1": "4"}}, {"t": "In general, x = __B1__ (in terms of a)", "a": {"B1": "12/a"}, "expr": true}], "sol": "x = 12.\n2x = 12, x = 6.\n3x = 12, x = 4.\nax = 12, so x = 12 ÷ a."}, {"kind": "mcq", "text": "How many solutions does |x − 5| = c have?", "opts": ["None if c = 0, two otherwise", "One if c < 0, two if c ≥ 0", "None if c < 0, one if c = 0, two if c > 0", "Two for every value of c"], "correct": 2, "tag": "", "sol": "An absolute value cannot be negative (no solution for c < 0); |x − 5| = 0 only at x = 5; a positive c gives 5 − c and 5 + c."}, {"kind": "blank", "p": "The sum of three consecutive integers is always 3 times the middle one.", "tag": "", "marks": "", "flat": [{"t": "If the sum is 75, the middle integer is __B1__", "a": {"B1": "25"}}, {"t": "If the sum is −42, the middle integer is __B1__", "a": {"B1": "-14"}}], "sol": "(m − 1) + m + (m + 1) = 3m = 75, so m = 25 (24 + 25 + 26 = 75).\n3m = −42, m = −14 (−15 − 14 − 13 = −42)."}, {"kind": "mcq", "text": "If 2x + 5 = 17, what is the value of 6x + 15?", "opts": ["6", "51", "17", "36"], "correct": 1, "tag": "", "sol": "6x + 15 = 3(2x + 5) = 3 × 17 = 51. (Or: x = 6, and 6(6) + 15 = 51.)"}, {"kind": "blank", "p": "The solutions of |x − c| = 3 are c − 3 and c + 3.", "tag": "", "marks": "", "flat": [{"t": "For c = 10, the smaller solution is __B1__", "a": {"B1": "7"}}, {"t": "and the larger solution is __B1__", "a": {"B1": "13"}}, {"t": "The midpoint of the two solutions is __B1__", "a": {"B1": "10"}}], "sol": "10 − 3 = 7.\n10 + 3 = 13.\n(7 + 13) ÷ 2 = 10: the midpoint is always c."}, {"kind": "mcq", "text": "The solution of 4(x − k) = 12 is x = 5. What is k?", "opts": ["k = 3", "k = 2", "k = 8", "k = −2"], "correct": 1, "tag": "", "sol": "Substitute x = 5: 4(5 − k) = 12 → 5 − k = 3 → k = 2."}, {"kind": "blank", "p": "Use the rule x = (c − b) ÷ a for equations of the form ax + b = c.", "tag": "", "marks": "", "flat": [{"t": "5x + 3 = 38: x = __B1__", "a": {"B1": "7"}}, {"t": "−2x + 3 = 11: x = __B1__", "a": {"B1": "-4"}}], "sol": "(38 − 3) ÷ 5 = 35 ÷ 5 = 7.\n(11 − 3) ÷ (−2) = 8 ÷ (−2) = −4."}, {"kind": "mcq", "text": "For which value of k does 5x + 2 = 5x + k have infinitely many solutions?", "opts": ["k = 0", "k = 5", "k = −2", "k = 2"], "correct": 3, "tag": "", "sol": "Subtract 5x: 2 = k. With k = 2 the equation is an identity; any other k gives no solution."}, {"kind": "blank", "p": "A rectangle's length is twice its width, so its perimeter is P = 6w.", "tag": "", "marks": "", "flat": [{"t": "P = 36 gives w = __B1__", "a": {"B1": "6"}}, {"t": "P = 54 gives w = __B1__", "a": {"B1": "9"}}, {"t": "In general, w = __B1__", "a": {"B1": "P/6"}, "expr": true}], "sol": "36 ÷ 6 = 6.\n54 ÷ 6 = 9.\nDivide both sides of P = 6w by 6: w = P ÷ 6."}]}, {"id": "s8", "label": "Assessment C", "sub": "Communicating", "slides": [{"kind": "mcq", "text": "An equation that is true for every value of the variable is called", "opts": ["an absolute value equation", "an inverse operation", "an identity", "a literal equation"], "correct": 2, "tag": "", "sol": "An identity, such as 2(x + 1) = 2x + 2, has infinitely many solutions."}, {"kind": "blank", "p": "Explain how to solve {x/−3} = 5.", "tag": "", "marks": "", "flat": [{"t": "Multiply both sides by __B1__", "a": {"B1": "-3"}}, {"t": "x = __B1__", "a": {"B1": "-15"}}], "sol": "x is divided by −3, so multiply by −3.\n5 × (−3) = −15."}, {"kind": "mcq", "text": "<b>Error analysis.</b> Sophia wrote: “|x| = −4, so x = 4 or x = −4.” Which reply is correct?", "opts": ["There is no solution, because an absolute value is never negative", "Only x = −4 works", "She is right; both 4 and −4 work", "Only x = 4 works"], "correct": 0, "tag": "", "sol": "|4| = 4 and |−4| = 4, never −4. An absolute value is a distance, so |x| = −4 has no solution."}, {"kind": "blank", "p": "Complete the definition.", "tag": "", "marks": "", "flat": [{"t": "A literal equation is an equation that has two or more __B1__.", "a": {"B1": "variables"}, "expr": "words", "accept": ["letters", "variable"]}], "sol": "For example, 2x + 3y = 6 and d = rt are literal equations."}, {"kind": "mcq", "text": "Which sentence describes the solution of 2(x + 1) = 2x + 5?", "opts": ["Infinitely many solutions, because both sides contain 2x", "No solution, because it simplifies to 2 = 5", "One solution, x = 0", "One solution, x = 3"], "correct": 1, "tag": "", "sol": "2x + 2 = 2x + 5 → 2 = 5, a false statement. No value of x works."}, {"kind": "blank", "p": "“Five more than three times a number n is 26.”", "tag": "", "marks": "", "flat": [{"t": "Left side of the equation: __B1__ = 26", "a": {"B1": "3n+5"}, "expr": true, "accept": ["5+3n"]}, {"t": "n = __B1__", "a": {"B1": "7"}}], "sol": "Three times n is 3n; five more than that is 3n + 5.\n3n = 21, so n = 7."}, {"kind": "mcq", "text": "<b>Error analysis.</b> Ethan solved 8 = −2(x − 3) by writing 8 = −2x − 6 and x = −7. What is correct?", "opts": ["His work is right, x = −7", "−2(x − 3) = −2x + 6, so x = −1", "−2(x − 3) = −2x − 3, so x = −5.5", "−2(x − 3) = 2x + 6, so x = 1"], "correct": 1, "tag": "", "sol": "−2 × (−3) = +6: 8 = −2x + 6 → 2 = −2x → x = −1. Check: −2(−1 − 3) = −2(−4) = 8 ✓"}, {"kind": "blank", "p": "Describe the steps for solving 3x − 4 = 11.", "tag": "", "marks": "", "flat": [{"t": "First __B1__ 4 to both sides (add / subtract).", "a": {"B1": "add"}, "expr": "words", "accept": ["adding"]}, {"t": "Then divide both sides by __B1__", "a": {"B1": "3"}}, {"t": "x = __B1__", "a": {"B1": "5"}}], "sol": "Adding 4 undoes subtracting 4: 3x = 15.\nDividing by 3 undoes multiplying by 3.\n15 ÷ 3 = 5."}, {"kind": "mcq", "text": "What is an extraneous solution?", "opts": ["The second solution of an absolute value equation", "A value found while solving that does not satisfy the original equation", "A solution that is a very large number", "A solution that is a fraction or decimal"], "correct": 1, "tag": "", "sol": "Extraneous solutions appear, for example, when an equation like |x + 3| = 2x is split into cases; checking in the original equation removes them."}]}, {"id": "s9", "label": "Assessment D", "sub": "Applying mathematics in real-life contexts", "slides": [{"kind": "mcq", "text": "A taxi charges $3.50 plus $2.25 per mile. Carla's fare was $26. How many miles did she ride?", "opts": ["11.6", "12", "10", "9"], "correct": 2, "tag": "", "sol": "3.50 + 2.25m = 26 → 2.25m = 22.50 → m = 10 miles."}, {"kind": "blank", "p": "Gym A charges a $60 joining fee plus $20 a month. Gym B charges $30 a month with no fee.", "tag": "", "marks": "", "flat": [{"t": "60 + 20m = 30m gives m = __B1__ months", "a": {"B1": "6"}}, {"t": "The cost at either gym is then $__B1__", "a": {"B1": "180"}}], "sol": "Subtract 20m: 60 = 10m, so m = 6.\n30 × 6 = 180 and 60 + 20 × 6 = 180."}, {"kind": "mcq", "text": "A bolt should be 25 mm long. A length is acceptable if it differs from 25 mm by at most 0.2 mm. What are the shortest and longest acceptable lengths? (Solve |x − 25| = 0.2.)", "opts": ["25 mm and 25.2 mm", "24.98 mm and 25.02 mm", "24.2 mm and 25.2 mm", "24.8 mm and 25.2 mm"], "correct": 3, "tag": "", "sol": "x − 25 = −0.2 → x = 24.8; x − 25 = 0.2 → x = 25.2."}, {"kind": "blank", "p": "Use C = {5/9}(F − 32). On a summer day in Phoenix it is 95 °F.", "tag": "", "marks": "", "flat": [{"t": "C = __B1__ °C", "a": {"B1": "35"}}], "sol": "C = {5/9}(95 − 32) = {5/9}(63) = 35 °C."}, {"kind": "mcq", "text": "A school sold 150 tickets for a play: adults $8, students $5. Ticket sales were $975. How many adult tickets were sold? (8a + 5(150 − a) = 975)", "opts": ["50", "105", "75", "45"], "correct": 2, "tag": "", "sol": "8a + 750 − 5a = 975 → 3a = 225 → a = 75 adult tickets (and 75 student tickets: 600 + 375 = 975)."}, {"kind": "blank", "p": "A car leaves Denver at 50 mph. A second car leaves the same place 1.5 hours later at 65 mph on the same road. Let t be the first car's travel time: 50t = 65(t − 1.5).", "tag": "", "marks": "", "flat": [{"t": "t = __B1__ hours", "a": {"B1": "6.5"}}, {"t": "They meet __B1__ miles from Denver", "a": {"B1": "325"}}], "sol": "50t = 65t − 97.5 → 97.5 = 15t → t = 6.5.\n50 × 6.5 = 325 miles (and 65 × 5 = 325).", "tools": ["calc"], "desmos": []}, {"kind": "mcq", "text": "Marcus earned $252 simple interest on $2,400 at 3.5% per year. For how many years was it invested? (I = Prt)", "opts": ["7", "2", "3", "3.5"], "correct": 2, "tag": "", "sol": "t = I ÷ (Pr) = 252 ÷ (2400 × 0.035) = 252 ÷ 84 = 3 years.", "tools": ["calc"], "desmos": []}, {"kind": "blank", "p": "Phone X is at 100% charge and loses 8% per hour. Phone Y is at 80% and loses 4% per hour.", "tag": "", "marks": "", "flat": [{"t": "100 − 8h = 80 − 4h gives h = __B1__ hours", "a": {"B1": "5"}}, {"t": "Both phones then show __B1__% charge", "a": {"B1": "60"}}], "sol": "20 = 4h, so h = 5.\n100 − 40 = 60 and 80 − 20 = 60. On Desmos the lines meet at (5, 60).", "tools": ["desmos"], "desmos": ["y=100-8x", "y=80-4x"]}, {"kind": "mcq", "text": "A rectangular garden is 3 ft longer than it is wide. It takes 38 ft of fencing to go around it. What are its dimensions?", "opts": ["17.5 ft by 20.5 ft", "7 ft by 10 ft", "8 ft by 11 ft", "9 ft by 12 ft"], "correct": 2, "tag": "", "sol": "2w + 2(w + 3) = 38 → 4w + 6 = 38 → w = 8, length 11. (17.5 by 20.5 comes from w + (w + 3) = 38, using only half the perimeter formula.)"}, {"kind": "mcq", "text": "<b>Is this reasonable?</b> Tara compares two streaming plans: 12 + 9m = 30 + 6m, where m is the number of months. She solves it and says, “The plans cost the same after m = −6 months.” What should she conclude?", "opts": ["Her answer is reasonable: the plans cost the same 6 months ago", "Her algebra is wrong: m = 6, so the plans cost the same after 6 months", "Her answer is reasonable, because −6 months means 6 months from now", "The plans can never cost the same, because 9 ≠ 6"], "correct": 1, "tag": "", "sol": "Subtract 6m and 12: 3m = 18, so m = 6, not −6. A negative number of months would not make sense for a plan that starts now, which is a warning sign to recheck. After 6 months: 12 + 54 = 66 and 30 + 36 = 66 ✓"}]}];
/* ================= build slide lists ================= */
var SLIDES = {}; SECTIONS.forEach(function(sec){ SLIDES[sec.id]=sec.slides; });
var TAB_DEFS = SECTIONS.map(function(sec){ return {id:sec.id, label:sec.label, sub:sec.sub}; });

/* ================= state ================= */
function blankItem(slide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    return {status:'unanswered', attempts:0, choice:undefined};
  }
  return {status:'unanswered', curStep:0, stepStates: slide.flat.map(function(){ return {status:'unanswered', attempts:0, inputs:{}}; })};
}
function defaultState(){
  var s={tabs:{}};
  TAB_DEFS.forEach(function(td){
    s.tabs[td.id] = { idx:0, maxReached:0, items: SLIDES[td.id].map(function(sl){ return blankItem(sl); }) };
  });
  return s;
}
var appState = {mode:null, learning:null, quiz:null};
var state = null;      // alias for appState[appState.mode]
var MODE = null;
var activeTab=TAB_DEFS[0].id;

function setMode(m){
  appState.mode = m;
  if(!appState[m]) appState[m] = defaultState();
  state = appState[m];
  MODE = m;
}
/* ================= student accounts (saved on this device) ================= */
var SHEET_KEY='sopaan-bim-ch1';
var ACC_KEY='sopaan-students-v1';
var storageOK=true;
var MEM={};
function lsGet(k){ var r=null; try{ r=localStorage.getItem(k); }catch(e){ storageOK=false; }
  if(r===null||r===undefined) r=MEM[k]||null; try{ return r?JSON.parse(r):null; }catch(e){ return null; } }
function lsSet(k,v){ var j=JSON.stringify(v); MEM[k]=j; try{ localStorage.setItem(k,j); return true; }catch(e){ storageOK=false; return false; } }
try{ localStorage.setItem('sopaan-probe','1'); localStorage.removeItem('sopaan-probe'); }catch(e){ storageOK=false; }
function hashPin(pin,salt){ var h=2166136261, str=salt+'|'+pin; for(var i=0;i<str.length;i++){ h^=str.charCodeAt(i); h=Math.imul(h,16777619)>>>0; } return h.toString(36); }
function accKey(name,roll){ return (name.trim().toLowerCase().replace(/\s+/g,' ')+'#'+roll.trim().toLowerCase()); }
function accounts(){ return lsGet(ACC_KEY)||{students:{}}; }
var student=null; // {key,name,roll}
var records=[];   // finished-tab history for this student on this sheet
function progKey(){ return SHEET_KEY+'::'+student.key; }

function loadState(){
  appState = {mode:null, learning:null, quiz:null}; records=[]; activeTab=TAB_DEFS[0].id;
  var saved=lsGet(progKey());
  if(!saved) return;
  try{
    ['learning','quiz'].forEach(function(m){
      if(saved[m] && saved[m].tabs){
        var fresh = defaultState();
        TAB_DEFS.forEach(function(td){
          if(saved[m].tabs[td.id] && saved[m].tabs[td.id].items && saved[m].tabs[td.id].items.length===SLIDES[td.id].length){
            fresh.tabs[td.id] = saved[m].tabs[td.id];
          }
        });
        appState[m] = fresh;
      }
    });
    if(saved.mode==='learning' || saved.mode==='quiz') appState.mode = saved.mode;
    if(saved.activeTab && TAB_DEFS.some(function(t){ return t.id===saved.activeTab; })) activeTab = saved.activeTab;
    if(Array.isArray(saved.records)) records = saved.records;
  }catch(e){}
}
function saveState(){
  if(!student) return;
  lsSet(progKey(), {mode:appState.mode, learning:appState.learning, quiz:appState.quiz, activeTab:activeTab, records:records, updated:Date.now()});
  var acc=accounts(); if(acc.students[student.key]){ acc.students[student.key].last=Date.now(); lsSet(ACC_KEY,acc); }
}
function addRecord(mode, tabId, correct, revealed, skipped, total){
  records.unshift({at:Date.now(), mode:mode, tab:tabId, correct:correct, revealed:revealed, skipped:skipped, total:total});
  if(records.length>60) records.length=60;
  saveState();
}
function fmtDate(ms){ try{ return new Date(ms).toLocaleString(undefined,{day:'numeric',month:'short',hour:'2-digit',minute:'2-digit'}); }catch(e){ return ''; } }

function renderWho(){
  var el=document.getElementById('whoBar');
  if(!student){ el.hidden=true; el.innerHTML=''; return; }
  el.hidden=false;
  el.innerHTML='Signed in as <b>'+esc(student.name)+'</b> · Roll '+esc(student.roll)+
    ' <button id="btnRecord">My record</button> <button id="btnSignOut">Sign out</button>';
  document.getElementById('btnRecord').addEventListener('click', renderRecord);
  document.getElementById('btnSignOut').addEventListener('click', signOut);
}
function signOut(){
  saveState(); student=null; state=null; MODE=null;
  var acc=accounts(); delete acc.current; lsSet(ACC_KEY,acc);
  document.getElementById('modePill').hidden=true;
  renderWho(); renderLogin();
}
function signIn(key){
  var acc=accounts(); var st=acc.students[key]; if(!st) return;
  student={key:key, name:st.name, roll:st.roll};
  acc.current=key; st.last=Date.now(); lsSet(ACC_KEY,acc);
  loadState(); renderWho();
  if(appState.mode==='learning' || appState.mode==='quiz'){
    setMode(appState.mode); document.getElementById('modePill').hidden=false; updateModePill();
    showChrome(true); buildTabbar(); renderSlide();
    showToast('Welcome back, '+st.name.split(' ')[0]+'. Picking up where you left off.');
  } else {
    renderModePicker();
  }
}
function renderLogin(msg){
  showChrome(false);
  var acc=accounts(); var keys=Object.keys(acc.students).sort(function(a,b){ return (acc.students[b].last||0)-(acc.students[a].last||0); });
  var h='<div class="login-card"><h2>Student sign-in</h2>'+
    '<p class="lead">Sign in to save your answers, see your record and continue where you left off next time.</p>';
  if(!storageOK) h+='<div class="login-err">This browser is blocking saved data (for example, a private window). You can still practise, but progress will not be kept after you close the page.</div>';
  if(msg) h+='<div class="login-err">'+esc(msg)+'</div>';
  if(keys.length){
    h+='<div class="known"><span class="known-label">Continue as</span>';
    keys.slice(0,6).forEach(function(k){ var st=acc.students[k];
      h+='<button class="known-btn" data-k="'+esc(k)+'"><span>'+esc(st.name)+' <small>· Roll '+esc(st.roll)+'</small></span><small>'+(st.last?'Last active '+fmtDate(st.last):'')+'</small></button>'; });
    h+='</div>';
  }
  h+='<form id="loginForm" novalidate>'+
    '<div class="fld"><label for="lgName">Full name</label><input id="lgName" autocomplete="name" required></div>'+
    '<div class="fld-row"><div class="fld"><label for="lgRoll">Roll no.</label><input id="lgRoll" required></div>'+
    '<div class="fld"><label for="lgPin">4-digit PIN</label><input id="lgPin" type="password" inputmode="numeric" maxlength="4" autocomplete="off" required></div></div>'+
    '<button class="btn btn-primary" type="submit" style="width:100%;">Sign in</button>'+
    '<p class="login-note">New here? Enter your name, roll no. and a PIN you will remember, and your profile is created. Progress is saved on this device, so use the same device and browser to continue.</p>'+
    '</form></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  wrap.querySelectorAll('.known-btn').forEach(function(b){
    b.addEventListener('click', function(){
      var st=accounts().students[b.dataset.k];
      document.getElementById('lgName').value=st.name; document.getElementById('lgRoll').value=st.roll;
      document.getElementById('lgPin').focus();
    });
  });
  document.getElementById('loginForm').addEventListener('submit', function(e){
    e.preventDefault();
    var name=document.getElementById('lgName').value.trim(), roll=document.getElementById('lgRoll').value.trim(), pin=document.getElementById('lgPin').value.trim();
    if(!name||!roll){ renderLoginErr('Enter your name and roll no.'); return; }
    if(!/^\d{4}$/.test(pin)){ renderLoginErr('Your PIN must be exactly 4 digits.'); return; }
    var k=accKey(name,roll); var acc=accounts();
    if(acc.students[k]){
      if(acc.students[k].pin!==hashPin(pin,k)){ renderLoginErr('That PIN does not match this name and roll no. Try again.'); return; }
    } else {
      acc.students[k]={name:name.replace(/\s+/g,' '), roll:roll, pin:hashPin(pin,k), created:Date.now()};
      lsSet(ACC_KEY,acc);
    }
    signIn(k);
  });
}
function renderLoginErr(m){
  var n=document.getElementById('lgName').value, r=document.getElementById('lgRoll').value;
  renderLogin(m); document.getElementById('lgName').value=n; document.getElementById('lgRoll').value=r; document.getElementById('lgPin').focus();
}
function tabSummary(m){
  var st=appState[m]; if(!st) return null;
  return TAB_DEFS.map(function(td){
    var items=st.tabs[td.id].items, n=items.length;
    var c=items.filter(function(i){return i.status==='correct';}).length;
    var done=items.filter(function(i){return i.status!=='unanswered';}).length;
    return {label:td.label, n:n, done:done, correct:c};
  });
}
function renderRecord(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+' · Solving Linear Equations</p>';
  ['learning','quiz'].forEach(function(m){
    var sum=tabSummary(m);
    h+='<h3>'+(m==='learning'?'📘 Learning Sheet':'📝 Quiz Mode')+'</h3>';
    if(!sum){ h+='<p class="rec-empty">Not started yet.</p>'; return; }
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>Section</th><th>Progress</th><th>Correct first time</th></tr></thead><tbody>';
    sum.forEach(function(r){ var pct=Math.round(r.done/r.n*100);
      h+='<tr><td>'+r.label+'</td><td><span class="rec-bar"><i style="width:'+pct+'%"></i></span>'+r.done+' / '+r.n+'</td><td>'+(m==='quiz'?'—':r.correct+' / '+r.n)+'</td></tr>'; });
    h+='</tbody></table></div>';
  });
  h+='</div><div class="rec-card"><h3>Finished sections</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sections finished yet. Each time you finish a tab, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table"><thead><tr><th>When</th><th>Mode</th><th>Section</th><th>Score</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+(r.mode==='learning'?' <span class="rec-empty">('+r.revealed+' revealed, '+r.skipped+' skipped)</span>':'')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){
    if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker();
  });
  window.scrollTo({top:0});
}

/* ================= tab bar ================= */
function buildTabbar(){
  var el=document.getElementById('tabbar');
  el.innerHTML = '<button class="tab-btn'+(activeTab==='theory'?' active':'')+'" data-tab="theory">Theory<span class="tab-count">notes</span></button>' + TAB_DEFS.map(function(t){
    return '<button class="tab-btn'+(t.id===activeTab?' active':'')+'" data-tab="'+t.id+'">'+t.label+'<span class="tab-count">'+SLIDES[t.id].length+'</span></button>';
  }).join('') + '<button class="tab-btn'+(activeTab==='report'?' active':'')+'" data-tab="report">📊 Report<span class="tab-count">pie</span></button>';
  el.querySelectorAll('.tab-btn').forEach(function(btn){
    btn.addEventListener('click', function(){ activeTab=btn.dataset.tab; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  });
}

/* ================= rendering ================= */
function canProceed(item){ return item.status==='correct'||item.status==='revealed'||item.status==='skipped'; }

function renderSlide(){
  if(!state.tabs[activeTab]){ activeTab=TAB_DEFS[0].id; }
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  if(ts.idx>=slides.length||ts.idx<0) ts.idx=0;
  var idx = ts.idx;
  var slide = slides[idx];
  var item = ts.items[idx];

  var tdef=TAB_DEFS.find(function(t){return t.id===activeTab;});
  document.getElementById('spLabel').textContent = tdef.label+' · Question '+(idx+1)+' of '+slides.length;
  document.getElementById('secSub').textContent = tdef.label+' — '+tdef.sub;
  document.getElementById('spFill').style.width = Math.round(((idx)/(Math.max(slides.length-1,1)))*100)+'%';

  var h='<div class="qcard">';
  if(slide.kind==='mcq' || slide.kind==='ar'){
    h += renderChoiceBody(slide, item, idx);
  } else {
    h += renderBlankBody(slide, item, idx);
  }
  h += '<div class="feedback" id="feedbackBox"></div>';
  if(MODE==='learning' && (item.status==='correct'||item.status==='revealed')) h += solutionHTML(slide);
  h += '</div>';

  document.getElementById('wrap').innerHTML = h;
  wireSlideEvents(slide, item, idx);
  restoreFeedback(item);
  renderNavbar(item);
  updateFab();
  saveState();
}

function solutionHTML(slide){
  if(!slide.sol) return '';
  return '<div class="solution"><div class="sol-h">Solution</div>'+slide.sol.split('\n').map(function(l){ return '<div class="sol-line">'+fr(esc(l))+'</div>'; }).join('')+'</div>';
}
var LETTERS=['a','b','c','d','e','f'];
function chosenHTML(slide,item){
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(item.choice===undefined) return '';
  var ok=item.choice===slide.correct;
  var h='<div class="chosen '+(ok?'ok':'bad')+'"><b>Your answer:</b> ('+LETTERS[item.choice]+') '+fr(esc(opts[item.choice]))+(ok?' ✓':' ✗')+'</div>';
  if(!ok) h+='<div class="chosen ok"><b>Correct answer:</b> ('+LETTERS[slide.correct]+') '+fr(esc(opts[slide.correct]))+'</div>';
  return h;
}
function renderChoiceBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div>';
  if(slide.kind==='mcq'){
    h += '<div class="qtext">'+fr(esc(slide.text))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  } else {
    h += '<div class="qtext"><span class="qtag" style="margin-left:0;margin-right:6px;">A / R</span>Assertion (A): '+fr(esc(slide.a))+'<br>Reason (R): '+fr(esc(slide.r))+(slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  }
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';
  var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
  if(MODE==='quiz') h += '<div class="quiz-hint">Quiz mode — pick an option. The correct answer is revealed once you finish this tab.</div>';
  var locked = MODE==='learning' && (item.status==='correct' || item.status==='revealed');
  h += '<div class="options">';
  opts.forEach(function(opt,i){
    var cls='opt';
    if(locked){
      if(i===slide.correct) cls+=' is-correct';
      else if(item.choice===i) cls+=' is-wrong';
      cls+=' locked';
    }
    if(item.choice===i) cls+=' is-chosen';
    h += '<label class="'+cls+'"><input type="radio" name="choice" value="'+i+'" '+(item.choice===i?'checked':'')+' '+(locked?'disabled':'')+'> <span class="opt-l">('+LETTERS[i]+')</span> <span class="opt-t">'+fr(esc(opt))+'</span>'+(item.choice===i?'<span class="opt-tag">'+(locked?(i===slide.correct?'Your answer ✓':'Your answer ✗'):'Selected')+'</span>':'')+'</label>';
  });
  h += '</div>';
  if(locked) h += chosenHTML(slide,item);
  return h;
}

function renderBlankBody(slide, item, idx){
  var h='<div class="qhead"><div class="qnum">'+(idx+1)+'</div><div class="qtext">';
  if(slide.kind==='case'){ h += '<b>'+esc(slide.title)+'.</b> '+esc(slide.body); }
  else { var pp=fr(esc(slide.p)).split('\n'); h += pp[0]+pp.slice(1).map(function(x){return '<span class="datline">'+x+'</span>';}).join(''); }
  h += (slide.tag?'<span class="qtag">'+esc(slide.tag)+'</span>':'')+'</div>';
  if(slide.marks) h += '<div class="marks-pill">'+slide.marks+'</div>';
  h += '</div>';
  if(slide.fig) h += '<div class="fig">'+slide.fig+'</div>';

  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  var blankCount=0; slide.flat.forEach(function(s){ blankCount+=Object.keys(s.a).length; });

  if(MODE==='quiz'){
    h += '<div class="step-badge">'+blankCount+' blank'+(blankCount===1?'':'s')+' in this question</div>';
    h += '<div class="quiz-hint">Quiz mode — fill in what you can. Correct answers are revealed once you finish this tab.</div>';
    if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
    if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
    h += '<div class="steps">';
    for(var qi=0; qi<total; qi++){
      var qstep = slide.flat[qi];
      var qss = item.stepStates[qi];
      if(qstep.partLabel) h += '<div class="subpart-label">'+esc(qstep.partLabel)+'</div>';
      if(qstep.orDivider) h += '<div class="or-divider">OR</div>';
      var qline = fr(qstep.t);
      Object.keys(qstep.a).forEach(function(bkey){
        var val = qss.inputs[bkey]||'';
        var inp='<input class="blank-input'+(['fv','fe','fl','fm','fi','dec'].indexOf(qstep.expr)>=0?' fr':(qstep.expr==='flist'||qstep.expr==='dlist'||qstep.expr==='glist')?' wide':qstep.expr===true?' expr':(qstep.expr==='words'||qstep.expr==='list'||qstep.expr==='expanded'||qstep.expr==='set'||qstep.expr==='primes'||qstep.expr==='trans'||qstep.expr==='rot'?' wide':''))+'" data-step="'+qi+'" data-bkey="'+bkey+'" value="'+esc(val)+'">';
        qline = qline.replace('__'+bkey+'__', inp);
      });
      if(qstep.fig) h += '<div class="fig">'+qstep.fig+'</div>';
      h += '<div class="step-line">'+qline+'</div>';
    }
    h += '</div>';
    return h;
  }

  if(hasFrac) h += '<div class="quiz-hint">Type fractions like <b>3/4</b> and mixed numbers like <b>2 3/4</b> (whole number, space, fraction).</div>';
  if(hasExpr) h += '<div class="quiz-hint">Type answers like <b>2x-5</b>, <b>x^2-4</b> or <b>3+2i</b>. Use ^ for powers, | | for absolute value and pi for π. Any equivalent form is accepted.</div>';
  var locked = item.status==='correct' || item.status==='revealed';
  var upto = locked ? total-1 : item.curStep;
  h += '<div class="step-badge">Step '+(Math.min(item.curStep,total-1)+1)+' of '+total+'</div>';
  h += '<div class="steps">';
  for(var i=0;i<=upto;i++){
    var step = slide.flat[i];
    var ss = item.stepStates[i];
    if(step.partLabel) h += '<div class="subpart-label">'+esc(step.partLabel)+'</div>';
    if(step.orDivider) h += '<div class="or-divider">OR</div>';
    var resolved = ss.status==='correct' || ss.status==='revealed';
    var line = fr(step.t);
    Object.keys(step.a).forEach(function(bkey){
      var fs = ss.inputs['fs_'+bkey];
      var cls = fs==='correct'?'is-correct':(fs==='wrong'?'is-wrong':'');
      var val = ss.inputs[bkey]||'';
      var dis = resolved ? 'disabled':'';
      var inp='<input class="blank-input '+cls+(['fv','fe','fl','fm','fi','dec'].indexOf(step.expr)>=0?' fr':(step.expr==='flist'||step.expr==='dlist'||step.expr==='glist')?' wide':step.expr===true?' expr':(step.expr==='words'||step.expr==='list'||step.expr==='expanded'||step.expr==='set'||step.expr==='primes'||step.expr==='trans'||step.expr==='rot'?' wide':''))+'" data-step="'+i+'" data-bkey="'+bkey+'" value="'+esc(val)+'" '+dis+'>';
      line = line.replace('__'+bkey+'__', inp);
    });
    if(step.fig) h += '<div class="fig">'+step.fig+'</div>';
    h += '<div class="step-line'+(resolved?' resolved':'')+'">'+line+'</div>';
    if(ss.status==='revealed'){
      var reveals=[];
      Object.keys(step.a).forEach(function(bkey){ reveals.push(bkey+' = '+esc(step.a[bkey])); });
      h += '<div class="reveal-note">correct: '+reveals.join(', ')+'</div>';
    }
  }
  h += '</div>';
  return h;
}

var __flash=null;
function restoreFeedback(item){
  var fb=document.getElementById('feedbackBox'); if(!fb) return;
  if(__flash){ fb.className='feedback show '+__flash.c; fb.innerHTML=__flash.h; __flash=null; return; }
  if(MODE==='quiz'){ fb.className='feedback'; fb.innerHTML=''; return; }
  if(item.status==='correct'){ fb.className='feedback show ok'; fb.innerHTML='<b>All done — correct!</b>'; }
  else if(item.status==='revealed'){ fb.className='feedback show reveal'; fb.innerHTML='<b>Answer revealed above.</b> Move on whenever you’re ready.'; }
  else if(item.status==='skipped'){ fb.className='feedback show retry'; fb.innerHTML='Skipped — you can answer it now and press <b>Check</b>, or come back later from the Question Palette.'; }
  else { fb.className='feedback'; fb.innerHTML=''; }
}

function slideIsAnswered(slide,item){
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return item.stepStates.some(function(ss){ return Object.keys(ss.inputs).some(function(k){ return k.indexOf('fs_')!==0 && ss.inputs[k] && String(ss.inputs[k]).trim()!==''; }); });
}
function renderNavbar(item){
  var ts = state.tabs[activeTab];
  var slides = SLIDES[activeTab];
  var slide = slides[ts.idx];
  var isLast = ts.idx === slides.length-1;
  var h='';
  h += '<button class="btn" id="btnPrev" '+(ts.idx===0?'disabled':'')+'>&larr; Previous</button>';

  if(MODE==='quiz'){
    h += '<button class="btn" id="btnSkip">Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnNext">'+(isLast?'Finish':'Next →')+'</button>';
  } else {
    h += '<button class="btn" id="btnSkip" '+(item.status!=='unanswered'?'disabled':'')+'>Skip</button>';
    h += '<span class="spacer"></span>';
    h += '<button class="btn btn-primary" id="btnCheck" '+((item.status!=='unanswered'&&item.status!=='skipped')?'disabled':'')+'>Check</button>';
    h += '<button class="btn btn-primary" id="btnNext" '+(canProceed(item)?'':'disabled')+'>'+(isLast?'Finish':'Next →')+'</button>';
  }
  document.getElementById('navbarInner').innerHTML = h;

  document.getElementById('btnPrev').addEventListener('click', function(){ if(ts.idx>0){ ts.idx--; renderSlide(); } });

  if(MODE==='quiz'){
    document.getElementById('btnSkip').addEventListener('click', function(){
      item.status='skipped';
      advanceQuiz(ts, slides);
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      item.status = slideIsAnswered(slide,item) ? 'answered' : 'unanswered';
      advanceQuiz(ts, slides);
    });
  } else {
    document.getElementById('btnSkip').addEventListener('click', function(){
      if(item.status==='unanswered'){ item.status='skipped'; renderSlide(); }
    });
    document.getElementById('btnNext').addEventListener('click', function(){
      if(!canProceed(item)) return;
      if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
      else { renderFinished(); }
    });
    document.getElementById('btnCheck').addEventListener('click', function(){ handleCheck(); });
  }
}
function advanceQuiz(ts, slides){
  if(ts.idx < slides.length-1){ ts.idx++; ts.maxReached=Math.max(ts.maxReached, ts.idx); renderSlide(); }
  else { renderFinished(); }
}

function wireSlideEvents(slide, item, idx){
  document.querySelectorAll('input[type="radio"][name="choice"]').forEach(function(r){
    r.addEventListener('change', function(){ item.choice=parseInt(r.value,10); saveState();
      document.querySelectorAll('.opt').forEach(function(l){ l.classList.remove('is-chosen'); var t=l.querySelector('.opt-tag'); if(t) t.remove(); });
      var lab=r.closest('.opt'); lab.classList.add('is-chosen'); var tg=document.createElement('span'); tg.className='opt-tag'; tg.textContent='Selected'; lab.appendChild(tg); });
  });
  document.querySelectorAll('.blank-input').forEach(function(inp){
    inp.addEventListener('input', function(){
      var si=parseInt(inp.dataset.step,10), bk=inp.dataset.bkey;
      item.stepStates[si].inputs[bk]=inp.value;
      saveState();
    });
  });
}

function handleCheck(){
  var ts = state.tabs[activeTab];
  var slide = SLIDES[activeTab][ts.idx];
  var item = ts.items[ts.idx];
  if(item.status==='skipped') item.status='unanswered';
  var fb = document.getElementById('feedbackBox');

  if(slide.kind==='mcq' || slide.kind==='ar'){
    if(item.choice===undefined){ fb.className='feedback show err'; fb.innerHTML='Please choose an option first.'; return; }
    var ok = item.choice===slide.correct;
    if(ok){
      item.status='correct'; playSuccess();
      fb.className='feedback show ok'; fb.innerHTML='<b>Correct!</b>';
    } else {
      item.attempts=(item.attempts||0)+1;
      if(item.attempts>=2){ item.status='revealed'; playReveal(); }
      else { playWrong(); fb.className='feedback show retry'; fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'}; }
    }
    renderSlide();
    return;
  }

  // blank / case
  var step = slide.flat[item.curStep];
  var ss = item.stepStates[item.curStep];
  var blanks = Object.keys(step.a);
  var missing = blanks.some(function(k){ return !ss.inputs[k] || String(ss.inputs[k]).trim()===''; });
  if(missing){ fb.className='feedback show err'; fb.innerHTML='Fill in every blank in this step before checking.'; return; }

  var allGood=true;
  blanks.forEach(function(k){
    var good=answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr);
    ss.inputs['fs_'+k]=good?'correct':'wrong';
    if(!good) allGood=false;
  });

  if(allGood){
    ss.status='correct'; playSuccess();
    advanceStepOrFinish(item, slide);
  } else {
    ss.attempts=(ss.attempts||0)+1;
    if(ss.attempts>=2){
      ss.status='revealed'; playReveal();
      advanceStepOrFinish(item, slide);
    } else {
      playWrong();
      fb.className='feedback show retry';
      fb.innerHTML='<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'; __flash={c:'retry',h:'<b>Not quite — try again</b> (attempt 1 of 2) <span class="attempts-dots"><span class="used"></span><span></span></span>'};
      renderSlide();
      return;
    }
  }
  renderSlide();
}

function advanceStepOrFinish(item, slide){
  var total = slide.flat.length;
  var hasExpr = slide.flat.some(function(s){ return s.expr===true; });
  var hasFrac = slide.flat.some(function(s){ return ['fv','fe','fl','fm','fi','flist'].indexOf(s.expr)>=0; });
  if(item.curStep < total-1){
    item.curStep++;
  } else {
    var anyRevealed = item.stepStates.some(function(ss){ return ss.status==='revealed'; });
    item.status = anyRevealed ? 'revealed' : 'correct';
  }
}

/* ================= palette ================= */
var overlay=document.getElementById('overlay');
function statusOf(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  return ts.items[i].status==='unanswered' ? 'locked' : ts.items[i].status;
}
function buildPalette(){
  var slides=SLIDES[activeTab];
  document.getElementById('paletteTitle').textContent = TAB_DEFS.find(function(t){return t.id===activeTab;}).label+' · Question palette';
  var body=document.getElementById('paletteBody');
  var html='';
  for(var i=0;i<slides.length;i++){
    html += '<div class="chip" data-status="'+statusOf(activeTab,i)+'" data-idx="'+i+'">'+(i+1)+'</div>';
  }
  body.innerHTML = html;
  body.querySelectorAll('.chip').forEach(function(chip){
    chip.addEventListener('click', function(){
      var i=parseInt(chip.dataset.idx,10);
      var ts=state.tabs[activeTab];
      if(i>ts.maxReached){ showToast('Finish the earlier questions to unlock this one.'); return; }
      ts.idx=i; closePalette(); renderSlide();
    });
  });
}
function openPalette(){ buildPalette(); overlay.classList.add('show'); }
function closePalette(){ overlay.classList.remove('show'); }
var toastTimer;
function showToast(msg){
  var t=document.getElementById('toast'); t.textContent=msg; t.classList.add('show');
  clearTimeout(toastTimer); toastTimer=setTimeout(function(){ t.classList.remove('show'); },2200);
}
document.getElementById('paletteFab').addEventListener('click', openPalette);
document.getElementById('paletteClose').addEventListener('click', closePalette);
overlay.addEventListener('click', function(e){ if(e.target===overlay) closePalette(); });

function updateFab(){
  var slides=SLIDES[activeTab];
  var done=state.tabs[activeTab].items.filter(function(it){ return it.status==='correct'||it.status==='revealed'||it.status==='skipped'; }).length;
  document.getElementById('fabBadge').textContent = done+'/'+slides.length;
}

/* ================= overall progress + finish ================= */
function updateChapterProgress(){
  var total=0, done=0;
  TAB_DEFS.forEach(function(td){
    state.tabs[td.id].items.forEach(function(it){
      total++;
      if(it.status==='correct'||it.status==='revealed'||it.status==='skipped') done++;
    });
  });
  var pct = total>0 ? Math.round((done/total)*100) : 0;
  document.getElementById('cpFill').style.width=pct+'%';
  document.getElementById('cpLabel').textContent=pct+'% complete';
}
function isSlideCorrect(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice===slide.correct;
  return slide.flat.every(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).every(function(k){ return answerMatches(ss.inputs[k], step.a[k], step.accept, step.expr); });
  });
}
function isSlideAttempted(tabId,i){
  var slide=SLIDES[tabId][i], item=state.tabs[tabId].items[i];
  if(slide.kind==='mcq'||slide.kind==='ar') return item.choice!==undefined;
  return slide.flat.some(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).some(function(k){ return ss.inputs[k] && String(ss.inputs[k]).trim()!==''; });
  });
}
function slideLabel(slide){
  var t = slide.kind==='case' ? slide.title : (slide.kind==='ar' ? slide.a : (slide.p||slide.text||''));
  t = String(t);
  return t.length>90 ? t.slice(0,90)+'…' : t;
}
function slideAnswerText(slide, item, correctSide){
  if(slide.kind==='mcq'||slide.kind==='ar'){
    var opts = slide.kind==='mcq' ? slide.opts : AR_OPTIONS;
    if(correctSide) return '('+LETTERS[slide.correct]+') '+opts[slide.correct];
    return item.choice!==undefined ? '('+LETTERS[item.choice]+') '+opts[item.choice] : '— not attempted —';
  }
  return slide.flat.map(function(step,si){
    var ss=item.stepStates[si];
    return Object.keys(step.a).map(function(k){
      return correctSide ? step.a[k] : (ss.inputs[k] || '—');
    }).join(', ');
  }).join('  |  ');
}

function renderFinished(){
  if(MODE==='quiz'){ renderQuizResults(); return; }
  var ts=state.tabs[activeTab];
  var correct=ts.items.filter(function(i){return i.status==='correct';}).length;
  var revealed=ts.items.filter(function(i){return i.status==='revealed';}).length;
  var skipped=ts.items.filter(function(i){return i.status==='skipped';}).length;
  var h='<div class="qcard done-card"><div class="big">✨</div><h2>Tab complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">You worked through all '+ts.items.length+' questions in this tab.</p>';
  if(!ts.recorded){ ts.recorded=true; addRecord('learning', activeTab, correct, revealed, skipped, ts.items.length); }
  h+='<div class="score-pills">'+
     '<span class="score-pill" style="background:var(--success-soft);color:var(--success);">'+correct+' correct</span>'+
     '<span class="score-pill" style="background:var(--danger-soft);color:var(--danger);">'+revealed+' revealed</span>'+
     '<span class="score-pill" style="background:var(--gold-soft);color:var(--retry-text);">'+skipped+' skipped</span></div>'+
     '<button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; ts.recorded=false; renderSlide(); });
  updateChapterProgress(); saveState();
}

function renderQuizResults(){
  var ts=state.tabs[activeTab];
  var slides=SLIDES[activeTab];
  var correctCount=0, attemptedCount=0;
  var rowsHtml = slides.map(function(slide,i){
    var item=ts.items[i];
    var ok=isSlideCorrect(activeTab,i);
    var att=isSlideAttempted(activeTab,i);
    if(ok) correctCount++;
    if(att) attemptedCount++;
    var tagCls = ok?'ok':(att?'bad':'na');
    var tagText = ok?'Correct':(att?'Incorrect':'Not attempted');
    var row='<div class="review-row">';
    row+='<span class="review-tag '+tagCls+'">Q'+(i+1)+' · '+tagText+'</span>';
    row+='<div class="review-q">'+fr(esc(slideLabel(slide)))+'</div>';
    row+='<div class="review-ans"><b>Your answer:</b> '+fr(esc(slideAnswerText(slide,item,false)))+'</div>';
    if(!ok) row+='<div class="review-ans" style="color:var(--success);"><b>Correct answer:</b> '+fr(esc(slideAnswerText(slide,item,true)))+'</div>';
    if(slide.sol) row+='<details class="rev-sol"><summary>Show solution</summary>'+solutionHTML(slide)+'</details>';
    row+='</div>';
    return row;
  }).join('');

  addRecord('quiz', activeTab, correctCount, 0, 0, slides.length);
  var h='<div class="qcard done-card" style="text-align:left;">';
  h+='<div style="text-align:center;"><div class="big">🏁</div><h2>Quiz complete</h2>';
  h+='<p style="color:var(--ink-soft);font-size:14px;">'+correctCount+' / '+slides.length+' correct · '+attemptedCount+' attempted</p></div>';
  h+='<div style="margin-top:16px;">'+rowsHtml+'</div>';
  h+='<div style="text-align:center;margin-top:6px;"><button class="btn btn-primary" id="btnReview">Review from question 1</button></div>';
  h+='</div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  document.getElementById('btnReview').addEventListener('click', function(){ ts.idx=0; renderSlide(); });
  playSuccess();
  updateChapterProgress(); saveState();
}

/* ================= mode picker ================= */
function updateModePill(){
  var btn=document.getElementById('modePill');
  if(!btn) return;
  btn.textContent = MODE==='quiz' ? '📝 Quiz Mode · switch' : '📘 Learning Sheet · switch';
}
function showChrome(show){
  document.querySelector('.tabbar').style.display = show?'':'none';
  document.querySelector('.slide-progress').style.display = show?'':'none';
  document.querySelector('.navbar').style.display = show?'':'none';
  document.getElementById('paletteFab').style.display = show?'':'none';
}
function renderModePicker(){
  showChrome(false);
  var wrap=document.getElementById('wrap');
  wrap.innerHTML =
    '<div class="mode-pick">'+
      '<div class="mode-card" data-pick="learning"><div class="mode-icon">📘</div><h3>Learning Sheet</h3>'+
      '<p>Work through each question step by step with instant feedback — two tries, then the correct value is revealed right there so you can keep moving.</p></div>'+
      '<div class="mode-card" data-pick="quiz"><div class="mode-icon">📝</div><h3>Quiz Mode</h3>'+
      '<p>Attempt every question with no hints along the way. Your score and the full answer key are shown together once you finish the tab — just like the real exam.</p></div>'+
    '</div>';
  wrap.querySelectorAll('[data-pick]').forEach(function(card){
    card.addEventListener('click', function(){
      setMode(card.dataset.pick); activeTab='theory';
      document.getElementById('modePill').hidden=false;
      updateModePill();
      showChrome(true);
      buildTabbar();
      renderSlide();
    });
  });
}
document.getElementById('modePill').addEventListener('click', function(){
  if(!appState.mode){ return; }
  setMode(appState.mode==='quiz' ? 'learning' : 'quiz');
  updateModePill();
  showChrome(true);
  buildTabbar();
  renderSlide();
});

/* ================= boot ================= */
var _origRenderSlide = renderSlide;
renderSlide = function(){ _origRenderSlide(); updateChapterProgress(); updateModePill(); };


/* ================= theory tab ================= */
function renderTheory(){
  var wrap=document.getElementById('wrap');
  wrap.innerHTML='<div class="theory">'+fr(THEORY)+'</div>';
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Theory — notes, key ideas and worked examples';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
  wrap.querySelectorAll('[data-jump]').forEach(function(b){ b.addEventListener('click',function(){ var t=document.getElementById(b.dataset.jump); if(t) t.scrollIntoView({behavior:'smooth',block:'start'}); }); });
}
var _rsTheory = renderSlide;
renderSlide = function(){
  if(activeTab==='theory'){ renderTheory(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  document.querySelector('.slide-progress').style.display='';
  document.querySelector('.navbar').style.display='';
  document.getElementById('paletteFab').style.display='';
  _rsTheory();
};


/* ================= MYP criterion report ================= */
var CRIT_COL={A:'var(--accent-text)',B:'var(--gold)',C:'#8A6FC4',D:'#2F9AA0'};
function critStats(){
  return REPORT.map(function(r){
    var tabId=r[0], slides=SLIDES[tabId], ts=state&&state.tabs[tabId];
    var c=0,w=0,n=0;
    slides.forEach(function(sl,i){
      if(!ts||!ts.items[i]){ n++; return; }
      var it=ts.items[i];
      if(MODE==='learning'){
        if(it.status==='correct') c++; else if(it.status==='revealed') w++; else n++;
      } else {
        if(isSlideCorrect(tabId,i)) c++; else if(isSlideAttempted(tabId,i)) w++; else n++;
      }
    });
    var tot=slides.length, pct=tot?Math.round(c/tot*100):0;
    var lvl=Math.round(c/Math.max(tot,1)*8);
    return {tab:tabId,letter:r[1],name:r[2],c:c,w:w,n:n,tot:tot,pct:pct,lvl:lvl};
  });
}
function arcPath(cx,cy,r,a0,a1){
  if(a1-a0>=Math.PI*2-1e-6){ return 'M'+(cx-r)+','+cy+' a'+r+','+r+' 0 1,0 '+(2*r)+',0 a'+r+','+r+' 0 1,0 '+(-2*r)+',0 Z'; }
  var x0=cx+r*Math.sin(a0), y0=cy-r*Math.cos(a0), x1=cx+r*Math.sin(a1), y1=cy-r*Math.cos(a1);
  return 'M'+cx+','+cy+' L'+x0.toFixed(2)+','+y0.toFixed(2)+' A'+r+','+r+' 0 '+((a1-a0)>Math.PI?1:0)+',1 '+x1.toFixed(2)+','+y1.toFixed(2)+' Z';
}
function pieSVG(parts,size,hole,center,sub){
  var tot=parts.reduce(function(s,p){return s+p.v;},0), cx=size/2, cy=size/2, r=size/2-4, a=0, h='';
  if(!tot){ h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+r+'" style="fill:var(--paper-2);stroke:var(--rule)"/>'; }
  parts.forEach(function(p){ if(!p.v) return; var b=a+p.v/tot*Math.PI*2; h+='<path d="'+arcPath(cx,cy,r,a,b)+'" style="fill:'+p.col+';stroke:var(--card);stroke-width:2"><title>'+esc(p.label)+': '+p.v+'</title></path>'; a=b; });
  if(hole) h+='<circle cx="'+cx+'" cy="'+cy+'" r="'+(r*hole)+'" style="fill:var(--card)"/>';
  if(center) h+='<text x="'+cx+'" y="'+(cy-(sub?4:0))+'" text-anchor="middle" dominant-baseline="middle" style="fill:var(--ink);font:700 '+(size>150?22:15)+'px Fraunces,serif">'+center+'</text>';
  if(sub) h+='<text x="'+cx+'" y="'+(cy+16)+'" text-anchor="middle" style="fill:var(--ink-soft);font:600 11px \'Source Sans 3\',sans-serif">'+sub+'</text>';
  return '<svg viewBox="0 0 '+size+' '+size+'" width="'+size+'" height="'+size+'" role="img">'+h+'</svg>';
}
function band(l){ return l===0?'0':(l<=2?'1–2':(l<=4?'3–4':(l<=6?'5–6':'7–8'))); }
function renderReport(){
  var st=critStats(), totC=0, totQ=0;
  st.forEach(function(s){ totC+=s.c; totQ+=s.tot; });
  var h='<div class="theory">';
  h+='<section class="note"><h2>Chapter test report</h2><p class="lt">'+(MODE==='quiz'?'<b>Quiz mode</b> results: answers are marked when you finish each test tab.':'<b>Learning mode</b> results: a question counts as correct only if you got it without the answer being revealed. Switch to Quiz mode for an exam-style score.')+'</p>';
  h+='<div class="rep-top"><div class="rep-pie">'+pieSVG(st.map(function(s){return {v:s.c,col:CRIT_COL[s.letter],label:'Criterion '+s.letter};}),200,0.55,totC+'/'+totQ,'correct')+'</div>';
  h+='<div class="rep-legend"><div class="rep-cap">Marks earned, by criterion</div>'+st.map(function(s){ return '<div class="rep-li"><span class="sw" style="background:'+CRIT_COL[s.letter]+'"></span><b>'+s.letter+'</b>&nbsp;'+esc(s.name)+'<span class="rep-n">'+s.c+' / '+s.tot+'</span></div>'; }).join('')+'</div></div></section>';
  h+='<div class="rep-grid">'+st.map(function(s){
    return '<div class="rep-card"><div class="rep-h"><span class="crit" style="background:'+CRIT_COL[s.letter]+'">'+s.letter+'</span>'+esc(s.name)+'</div>'+
      '<div class="rep-row">'+pieSVG([{v:s.c,col:'var(--success)',label:'Correct'},{v:s.w,col:'var(--danger)',label:'Incorrect'},{v:s.n,col:'var(--locked)',label:'Not attempted'}],120,0.5,s.pct+'%')+
      '<div class="rep-stats"><div><span class="sw" style="background:var(--success)"></span>Correct <b>'+s.c+'</b></div><div><span class="sw" style="background:var(--danger)"></span>Incorrect <b>'+s.w+'</b></div><div><span class="sw" style="background:var(--locked)"></span>Not attempted <b>'+s.n+'</b></div>'+
      '<div class="rep-lvl">Indicative level <b>'+s.lvl+'</b> / 8 <span>(band '+band(s.lvl)+')</span></div></div></div>'+
      '<button class="hub-btn" data-go="'+s.tab+'">Open Test '+s.letter+' →</button></div>';
  }).join('')+'</div>';
  h+='<p class="rep-note">Indicative level = fraction of questions correct × 8, rounded. It is a practice guide only; your teacher awards the real MYP criterion levels.</p></div>';
  var wrap=document.getElementById('wrap'); wrap.innerHTML=h;
  document.querySelector('.slide-progress').style.display='none';
  document.querySelector('.navbar').style.display='none';
  document.getElementById('paletteFab').style.display='none';
  document.getElementById('secSub').textContent='Report — chapter test results by MYP criterion';
  wrap.querySelectorAll('[data-go]').forEach(function(b){ b.addEventListener('click',function(){ activeTab=b.dataset.go; buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); });
}
var _rsReport = renderSlide;
renderSlide = function(){
  if(activeTab==='report'){ renderReport(); buildTabbar(); updateChapterProgress(); updateModePill(); saveState(); return; }
  _rsReport();
};


/* ================= skipped-question return ================= */
function firstSkippedIdx(ts){
  for(var i=0;i<ts.items.length;i++){
    var it=ts.items[i];
    if(MODE==='quiz'){ if(!isSlideAttempted(activeTab,i)) return i; }
    else if(it.status==='skipped'||it.status==='unanswered') return i;
  }
  return -1;
}
function skippedList(ts){
  var out=[]; for(var i=0;i<ts.items.length;i++){ var it=ts.items[i];
    if(MODE==='quiz' ? !isSlideAttempted(activeTab,i) : (it.status==='skipped'||it.status==='unanswered')) out.push(i); }
  return out;
}
function renderSkipGate(ts){
  var list=skippedList(ts);
  var h='<div class="qcard done-card"><div class="big">⏭️</div><h2>You skipped '+list.length+' question'+(list.length>1?'s':'')+'</h2>'+
    '<p style="color:var(--ink-soft);font-size:14px;">Answer them now, or submit the tab as it is. Answers are marked only when you submit.</p>'+
    '<div class="skip-chips">'+list.map(function(i){ return '<button class="chip skip-go" data-i="'+i+'">Q'+(i+1)+'</button>'; }).join('')+'</div>'+
    '<div class="skip-btns"><button class="btn btn-primary" id="btnGoSkipped">Answer skipped questions</button><button class="btn" id="btnSubmitAnyway">Submit anyway</button></div></div>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('navbarInner').innerHTML='';
  var go=function(i){ ts.idx=i; ts.maxReached=Math.max(ts.maxReached,i); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); };
  document.getElementById('btnGoSkipped').addEventListener('click',function(){ go(list[0]); });
  document.querySelectorAll('.skip-go').forEach(function(b){ b.addEventListener('click',function(){ go(parseInt(b.dataset.i,10)); }); });
  document.getElementById('btnSubmitAnyway').addEventListener('click',function(){ ts.submitOK=true; renderFinished(); ts.submitOK=false; });
  saveState();
}
var _rfSkip = renderFinished;
renderFinished = function(){
  var ts=state.tabs[activeTab];
  if(MODE==='quiz' && !ts.submitOK && skippedList(ts).length){ renderSkipGate(ts); return; }
  _rfSkip();
  if(MODE==='learning'){
    var list=skippedList(ts);
    if(list.length){
      var card=document.querySelector('.done-card');
      if(card){ var d=document.createElement('div'); d.className='skip-btns';
        d.innerHTML='<button class="btn btn-primary" id="btnGoSkipped">Attempt skipped questions ('+list.length+')</button>';
        card.appendChild(d);
        document.getElementById('btnGoSkipped').addEventListener('click',function(){ ts.idx=list[0]; ts.recorded=false; renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); }); }
    }
  }
};


/* ================= approx answers (physics: within 1%) ================= */
var _amTools = answerMatches;
answerMatches = function(input,answer,accept,expr){
  if(expr==='approx'){
    var n1=parseNum(input); if(n1===null) return false;
    return [answer].concat(accept||[]).some(function(a){ var n2=parseNum(a); if(n2===null) return false; return Math.abs(n1-n2) <= Math.max(0.011*Math.abs(n2), 1e-9); });
  }
  return _amTools(input,answer,accept,expr);
};

/* ================= palette: every question already reached can be opened ================= */
statusOf = function(tabId,i){
  var ts=state.tabs[tabId];
  if(i>ts.maxReached) return 'locked';
  if(i===ts.idx) return 'current';
  var s=ts.items[i].status;
  if(s==='unanswered') return 'skipped';
  return s;
};

/* ================= on-screen keyboard ================= */
var KB={on:true, page:'num', target:null};
try{ var kbp=localStorage.getItem('sopaan-kb-pref'); if(kbp==='off') KB.on=false; }catch(e){}
function kbSave(){ try{ localStorage.setItem('sopaan-kb-pref', KB.on?'on':'off'); }catch(e){} }
var KEYS_NUM=[['7','8','9','(',')'],['4','5','6','−','/'],['1','2','3','.',','],['0',':','%','°','⌫'],['abc','←','→','Clear','Done']];
var KEYS_FRAC=[['7','8','9','/'],['4','5','6','−'],['1','2','3','space'],['0',',','⌫','Clear'],['abc','←','→','Done']];
var KEYS_ALG=[['7','8','9','x','y','n'],['4','5','6','+','−','a'],['1','2','3','×','÷','b'],['0','.','(',')','^','²'],['/','π','|','t','⌫','Clear'],['abc','←','→','Done']];
function kbLayoutFor(inp){ try{ var ts=state.tabs[activeTab], sl=SLIDES[activeTab][ts.idx], stp=sl.flat[parseInt(inp.dataset.step,10)]; var m=stp.expr, key=String(stp.a[inp.dataset.bkey]||'');
  if(m==='words'||m==='glist'||m==='angle') return 'abc'; if(m===true||m==='pow'||m==='primes') return 'alg';
  if(['fv','fe','fl','fm','fi','flist'].indexOf(m)>=0) return 'frac'; if(m==='dec'||m==='approx'||m==='dlist'||m==='set'||m==='coord'||m==='list'||m==='time') return 'num';
  if(/^[\-−]?\d+ \d+\/\d+$/.test(key)||/^[\-−]?\d+\/\d+$/.test(key)) return 'frac'; if(/[a-df-z]/i.test(key.replace(/pi/gi,''))) return /\d/.test(key)?'alg':'abc'; return 'num'; }catch(e){ return 'num'; } }
var KEYS_CALC=[['7','8','9','x','(',')'],['4','5','6','+','−','^'],['1','2','3','×','/','²'],['0','.','e','eˣ','√','ln'],['sin','cos','tan','t','⌫','Clear'],['abc','←','→','Done']];
var KEYS_ABC=[['q','w','e','r','t','y','u','i','o','p'],['a','s','d','f','g','h','j','k','l','-'],['z','x','c','v','b','n','m',',',':','/'],['123','space','←','→','⌫','Done']];
function kbBuild(){
  var el=document.getElementById('vkb'); if(!el){ el=document.createElement('div'); el.id='vkb'; el.className='vkb'; document.body.appendChild(el);
    el.addEventListener('pointerdown',function(e){ var b=e.target.closest('button[data-k]'); e.preventDefault(); if(b) kbPress(b.dataset.k); });
    el.addEventListener('mousedown',function(e){ e.preventDefault(); }); }
  var rows={num:KEYS_NUM,frac:KEYS_FRAC,alg:KEYS_ALG,abc:KEYS_ABC,calc:KEYS_CALC}[KB.page]||KEYS_NUM;
  el.innerHTML='<div class="vkb-top"><span>⌨️ Keyboard</span><button data-k="device" class="vkb-link">Use device keyboard</button></div>'+
    rows.map(function(r){ return '<div class="vkb-row">'+r.map(function(k){
      var cls='vkb-k'+(/^(abc|123|Done|Clear|⌫|←|→|space)$/.test(k)?' fn':'')+(k==='Done'?' done':'');
      return '<button type="button" class="'+cls+'" data-k="'+k+'">'+(k==='space'?'space':k)+'</button>'; }).join('')+'</div>'; }).join('');
  return el;
}
function kbShow(inp){ KB.target=inp; KB.home=kbLayoutFor(inp); KB.page=KB.home; if(!KB.on) return; var cp=document.getElementById('calcPanel'); if(cp&&cp.classList.contains('show')) return; var el=kbBuild(); var nb=document.querySelector('.navbar'); el.style.bottom=(nb?nb.getBoundingClientRect().height:0)+'px'; el.classList.add('show'); document.body.classList.add('kb-open'); setTimeout(function(){ var r=inp.getBoundingClientRect(), top=el.getBoundingClientRect().top; if(r.bottom>top-12) window.scrollBy({top:r.bottom-top+60,behavior:'smooth'}); else if(r.top<60) window.scrollBy({top:r.top-80,behavior:'smooth'}); },30); }
function kbHide(){ var el=document.getElementById('vkb'); if(el) el.classList.remove('show'); document.body.classList.remove('kb-open'); }
function kbInsert(s){
  var t=KB.target; if(!t||t.disabled) return;
  var a=t.selectionStart==null?t.value.length:t.selectionStart, b=t.selectionEnd==null?a:t.selectionEnd;
  t.value=t.value.slice(0,a)+s+t.value.slice(b); var p=a+s.length; try{ t.setSelectionRange(p,p); }catch(e){}
  t.dispatchEvent(new Event('input',{bubbles:true}));
}
function kbPress(k){
  var t=KB.target; if(k==='device'){ KB.on=false; kbSave(); kbHide(); document.querySelectorAll('.blank-input').forEach(function(i){ i.removeAttribute('inputmode'); }); if(t){ t.blur(); setTimeout(function(){ t.focus(); },50); } showToast('Device keyboard on. Tap ⌨️ on any blank to bring the on-screen keyboard back.'); return; }
  if(k==='Done'){ kbHide(); if(t) t.blur(); return; }
  if(k==='abc'||k==='123'){ KB.page=(k==='abc')?'abc':(KB.home&&KB.home!=='abc'?KB.home:'num'); kbBuild(); return; }
  if(!t) return;
  if(k==='⌫'){ var a=t.selectionStart, b=t.selectionEnd; if(a===b&&a>0){ t.value=t.value.slice(0,a-1)+t.value.slice(b); try{t.setSelectionRange(a-1,a-1);}catch(e){} } else { t.value=t.value.slice(0,a)+t.value.slice(b); try{t.setSelectionRange(a,a);}catch(e){} } t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='Clear'){ t.value=''; t.dispatchEvent(new Event('input',{bubbles:true})); return; }
  if(k==='←'||k==='→'){ var p=(t.selectionStart||0)+(k==='←'?-1:1); p=Math.max(0,Math.min(t.value.length,p)); try{t.setSelectionRange(p,p);}catch(e){} return; }
  var map={'−':'-','space':' '}; kbInsert(map[k]!==undefined?map[k]:k);
}
function kbWire(){
  document.querySelectorAll('.blank-input').forEach(function(inp){
    if(inp.dataset.kb) return; inp.dataset.kb='1';
    if(KB.on) inp.setAttribute('inputmode','none');
    inp.addEventListener('focus',function(){ kbShow(inp); });
    var btn=document.createElement('button'); btn.type='button'; btn.className='kb-toggle'; btn.title='On-screen keyboard'; btn.textContent='⌨️'; btn.tabIndex=-1;
    btn.addEventListener('mousedown',function(e){ e.preventDefault(); });
    btn.addEventListener('click',function(){ KB.on=true; kbSave(); document.querySelectorAll('.blank-input').forEach(function(i){ i.setAttribute('inputmode','none'); }); inp.focus(); kbShow(inp); });
    if(!inp.disabled) inp.insertAdjacentElement('afterend',btn);
  });
}
document.addEventListener('focusout',function(e){ setTimeout(function(){ var a=document.activeElement; if(!a||!a.classList||!a.classList.contains('blank-input')){ if(!document.querySelector('#vkb:hover')) kbHide(); } },120); });

/* ================= calculator ================= */
var CALC={expr:'', ans:0};
function calcEval(src){
  var s=String(src).replace(/×/g,'*').replace(/÷/g,'/').replace(/−/g,'-').replace(/π/g,'(PI)').replace(/Ans/g,'('+CALC.ans+')').replace(/\^/g,'**').replace(/√\(/g,'sqrt(').replace(/²/g,'**2').replace(/E/g,'*10**');
  s=s.replace(/(^|[(*\/+\-,])-/g,'$1(-1)*');
  if(/[^0-9+\-*/().,a-z A-Z]/.test(s)) throw 0;
  var ok=s.replace(/sin|cos|tan|asin|acos|atan|sqrt|log|ln|PI|abs/g,''); if(/[a-zA-Z]/.test(ok)) throw 0;
  var f=new Function('sin','cos','tan','asin','acos','atan','sqrt','log','ln','PI','abs','return ('+s+');');
  var d=Math.PI/180;
  var v=f(function(x){return Math.sin(x*d);},function(x){return Math.cos(x*d);},function(x){return Math.tan(x*d);},
    function(x){return Math.asin(x)/d;},function(x){return Math.acos(x)/d;},function(x){return Math.atan(x)/d;},Math.sqrt,Math.log10,Math.log,Math.PI,Math.abs);
  if(typeof v!=='number'||!isFinite(v)) throw 0; return v;
}
function fmtNum(v){ if(Math.abs(v)>=1e10||(Math.abs(v)<1e-6&&v!==0)) return v.toExponential(6).replace(/\.?0+e/,'e'); return String(parseFloat(v.toPrecision(10))); }
var CKEYS=[['sin(','cos(','tan(','√(','^','²'],['asin(','acos(','atan(','(',')','π'],['7','8','9','÷','⌫','AC'],['4','5','6','×','E','Ans'],['1','2','3','−','(−)','Insert'],['0','.','=','+']];
function openCalc(){
  var p=document.getElementById('calcPanel');
  if(!p){ p=document.createElement('div'); p.id='calcPanel'; p.className='tool-panel calc';
    p.innerHTML='<div class="tp-head"><b>🧮 Calculator</b><span class="tp-note">degrees · tap a blank, then Insert</span><button class="tp-x" data-c="close">✕</button></div>'+
      '<div class="calc-disp"><div class="calc-expr" id="calcExpr"></div><div class="calc-res" id="calcRes">0</div></div>'+
      '<div class="calc-keys">'+CKEYS.map(function(r){ return r.map(function(k){ return '<button type="button" data-c="'+k+'" class="'+(k==='='?'eq':(/^(AC|⌫|Insert)$/.test(k)?'fn':''))+'">'+({'sin(':'sin','cos(':'cos','tan(':'tan','asin(':'sin⁻¹','acos(':'cos⁻¹','atan(':'tan⁻¹','√(':'√'}[k]||k)+'</button>'; }).join(''); }).join('')+'</div>';
    document.body.appendChild(p);
    p.addEventListener('mousedown',function(e){ if(e.target.closest('button')) e.preventDefault(); });
    p.addEventListener('click',function(e){ var b=e.target.closest('button[data-c]'); if(!b) return; calcKey(b.dataset.c); });
  }
  kbHide(); var nb=document.querySelector('.navbar'); p.style.bottom=((nb?nb.getBoundingClientRect().height:0)+8)+'px'; p.classList.add('show'); document.body.classList.add('calc-open'); calcShow();
}
function calcShow(res){ document.getElementById('calcExpr').textContent=CALC.expr||' '; if(res!==undefined) document.getElementById('calcRes').textContent=res; }
function calcKey(k){
  if(k==='close'){ document.getElementById('calcPanel').classList.remove('show'); document.body.classList.remove('calc-open'); return; }
  if(k==='AC'){ CALC.expr=''; calcShow('0'); return; }
  if(k==='⌫'){ CALC.expr=CALC.expr.replace(/(asin\(|acos\(|atan\(|sin\(|cos\(|tan\(|√\(|Ans|.)$/,''); calcShow(); return; }
  if(k==='='){ try{ var v=calcEval(CALC.expr); CALC.ans=v; calcShow(fmtNum(v)); }catch(e){ calcShow('Error'); } return; }
  if(k==='(−)'){ CALC.expr+='−'; calcShow(); return; }
  if(k==='Insert'){ var r=document.getElementById('calcRes').textContent; if(KB.target && !KB.target.disabled && r!=='Error'){ KB.target.value=r; KB.target.dispatchEvent(new Event('input',{bubbles:true})); showToast('Inserted '+r+' into the blank.'); } else showToast('Tap a blank first, then press Insert.'); return; }
  CALC.expr+=k; calcShow();
}

/* ================= Desmos ================= */
var DESMOS_KEY='dcb31709b452b1cf9dc26972add0fda6', desmosCalc=null, desmosLoading=false;
function openDesmos(exprs){
  var p=document.getElementById('desmosPanel');
  if(!p){ p=document.createElement('div'); p.id='desmosPanel'; p.className='tool-panel desmos';
    p.innerHTML='<div class="tp-head"><b>📈 Desmos graphing calculator</b><button class="tp-x" id="desmosReset">Reset graph</button><button class="tp-x" id="desmosClose">✕</button></div><div id="desmosBox"><div class="desmos-msg">Loading Desmos…</div></div>';
    document.body.appendChild(p);
    document.getElementById('desmosClose').addEventListener('click',function(){ p.classList.remove('show'); });
    document.getElementById('desmosReset').addEventListener('click',function(){ if(desmosCalc) desmosSet(p._exprs||[]); });
  }
  p._exprs=exprs||[]; p.classList.add('show');
  if(window.Desmos){ desmosInit(); desmosSet(p._exprs); return; }
  if(desmosLoading) return; desmosLoading=true;
  var sc=document.createElement('script'); sc.src='https://www.desmos.com/api/v1.9/calculator.js?apiKey='+DESMOS_KEY;
  sc.onload=function(){ desmosInit(); desmosSet(p._exprs); };
  sc.onerror=function(){ desmosLoading=false; document.getElementById('desmosBox').innerHTML='<div class="desmos-msg">Desmos needs an internet connection. <a href="https://www.desmos.com/calculator" target="_blank" rel="noopener">Open Desmos in a new tab</a>.</div>'; };
  document.head.appendChild(sc);
}
function desmosInit(){ if(desmosCalc) return; var box=document.getElementById('desmosBox'); box.innerHTML=''; desmosCalc=Desmos.GraphingCalculator(box,{expressionsCollapsed:false,settingsMenu:false,border:false,degreeMode:true}); }
function desmosSet(exprs){ if(!desmosCalc) return; desmosCalc.setBlank(); (exprs||[]).forEach(function(e,i){ if(typeof e==='string') desmosCalc.setExpression({id:'e'+i,latex:e}); else desmosCalc.setExpression(Object.assign({id:'e'+i},e)); }); }

/* ================= toolbar on each question ================= */
var _rsTools = renderSlide;
renderSlide = function(){
  _rsTools();
  kbHide();
  if(activeTab==='theory'||activeTab==='report') return;
  var ts=state.tabs[activeTab]; if(!ts) return;
  var slide=SLIDES[activeTab][ts.idx], card=document.querySelector('#wrap .qcard');
  if(card && slide && slide.tools && slide.tools.length && !card.querySelector('.tool-bar')){
    var bar=document.createElement('div'); bar.className='tool-bar';
    bar.innerHTML=(slide.tools.indexOf('calc')>=0?'<button type="button" class="tool-btn" data-t="calc">🧮 Calculator</button>':'')+
                  (slide.tools.indexOf('desmos')>=0?'<button type="button" class="tool-btn" data-t="desmos">📈 Desmos graph</button>':'');
    card.insertBefore(bar, card.firstChild);
    bar.addEventListener('click',function(e){ var b=e.target.closest('[data-t]'); if(!b) return; if(b.dataset.t==='calc') openCalc(); else openDesmos(slide.desmos||[]); });
  }
  kbWire();
};



/* ================= signed fractions in text: {−3/4}, {3/−4}, {−2 1/3}, {p/q} ================= */
fr = function(s){ return String(s).replace(/&lt;(\/?)(b|sup|sub|i)>/g,'<$1$2>')
  .replace(/\{([−-]?\d+) (\d+)\/(\d+)\}/g,'<span class="mx">$1<span class="fq"><span>$2</span><span>$3</span></span></span>')
  .replace(/\{([−-]?[A-Za-z0-9]+)\/([−-]?[A-Za-z0-9]+)\}/g,'<span class="fq"><span>$1</span><span>$2</span></span>'); };
/* ================= BMA badge → main page of this sheet (theory hub) ================= */
(function(){
  var c=document.querySelector('.brand .crest'); if(!c) return;
  var a=document.createElement('button'); a.type='button'; a.className='crest crest-home'; a.title='Back to the main page (theory notes)'; a.setAttribute('aria-label','Main page');
  a.innerHTML='BM<span class="crest-h">⌂</span>'; c.parentNode.replaceChild(a,c);
  a.addEventListener('click',function(){
    if(!student||!MODE){ window.scrollTo({top:0,behavior:'smooth'}); return; }
    if(typeof kbHide==='function') kbHide(); if(typeof SP!=='undefined'&&SP.on) spToggle(false);
    var cp=document.getElementById('calcPanel'); if(cp) cp.classList.remove('show'); document.body.classList.remove('calc-open');
    activeTab = (typeof THEORY!=='undefined') ? 'theory' : TAB_DEFS[0].id;
    buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'});
  });
})();

/* ================= session clock: starts at sign-in and keeps running ================= */
var CLK={t0:null};
(function(){
  var row=document.querySelector('.brand .brand-row'); if(!row) return;
  var d=document.createElement('div'); d.className='bmasw off'; d.id='swBox'; d.title='Time since you signed in';
  d.innerHTML='<span class="bmasw-ic">⏱</span><span class="bmasw-t" id="swT">00:00</span>';
  row.appendChild(d); setInterval(swTick,1000);
})();
function swFmt(s){ s=Math.floor(s||0); var h=Math.floor(s/3600), m=Math.floor(s%3600/60), x=s%60; return (h?h+':'+String(m).padStart(2,'0'):String(m).padStart(2,'0'))+':'+String(x).padStart(2,'0'); }
function swTick(){
  var box=document.getElementById('swBox'); if(!box) return;
  if(student && !CLK.t0) CLK.t0=Date.now();
  if(!student) CLK.t0=null;
  box.classList.toggle('off',!CLK.t0);
  document.getElementById('swT').textContent = CLK.t0 ? swFmt((Date.now()-CLK.t0)/1000) : '00:00';
}
function swTab(){ try{ if(!state||!state.tabs||activeTab==='theory'||activeTab==='report') return null; return state.tabs[activeTab]||null; }catch(e){ return null; } }
var _rsSW = renderSlide;
renderSlide = function(){ _rsSW(); swTick(); };
var _rfSW = renderFinished;
renderFinished = function(){ _rfSW(); var done=document.querySelector('#wrap .done-card'); if(CLK.t0 && done && !done.querySelector('.bmasw-done')){ var p=document.createElement('p'); p.className='bmasw-done'; p.textContent='⏱ Time since sign-in: '+swFmt((Date.now()-CLK.t0)/1000); var h2=done.querySelector('h2'); if(h2) h2.insertAdjacentElement('afterend',p); else done.appendChild(p); } };

/* ================= scratchpad (Khan-style, 4 pens) ================= */
var SP={on:false, draw:true, color:'ink', size:3, erase:false, store:{}, key:null, cv:null, ctx:null, down:false, last:null};
var SP_COL={ink:null, blue:'#2563EB', red:'#DC2626', green:'#16A34A'};
function spInk(){ return getComputedStyle(document.documentElement).getPropertyValue('--ink').trim()||'#211E1A'; }
function spKey(){ var ts=swTab(); return ts ? (MODE+'|'+activeTab+'|'+ts.idx) : null; }
function spBuild(){
  if(SP.cv) return;
  var cv=document.createElement('canvas'); cv.id='spCanvas'; cv.className='sp-canvas'; document.body.appendChild(cv);
  var bar=document.createElement('div'); bar.id='spBar'; bar.className='sp-bar';
  bar.innerHTML='<span class="sp-lbl">✏️ Scratchpad</span>'+
    ['ink','blue','red','green'].map(function(c){ return '<button type="button" class="sp-pen" data-c="'+c+'" title="'+(c==='ink'?'black':c)+' pen"><i style="background:'+(c==='ink'?'var(--ink)':SP_COL[c])+'"></i></button>'; }).join('')+
    '<button type="button" class="sp-tool" data-t="erase" title="Eraser">🧽</button><button type="button" class="sp-tool" data-t="size" title="Pen size">●</button><button type="button" class="sp-tool" data-t="scroll" title="Pause drawing to scroll or answer">✋</button>'+
    '<button type="button" class="sp-tool" data-t="clear" title="Clear page">🗑</button><button type="button" class="sp-tool" data-t="close" title="Close scratchpad">✕</button>';
  document.body.appendChild(bar);
  bar.addEventListener('click',function(e){ var b=e.target.closest('button'); if(!b) return;
    if(b.dataset.c){ SP.color=b.dataset.c; SP.erase=false; SP.draw=true; }
    else if(b.dataset.t==='erase'){ SP.erase=true; SP.draw=true; }
    else if(b.dataset.t==='size'){ SP.size = SP.size===3?6:(SP.size===6?1.5:3); b.textContent = SP.size===6?'⬤':(SP.size===1.5?'·':'●'); }
    else if(b.dataset.t==='scroll'){ SP.draw=!SP.draw; }
    else if(b.dataset.t==='clear'){ spClear(); }
    else if(b.dataset.t==='close'){ spToggle(false); return; }
    spUI(); });
  SP.cv=cv; SP.ctx=cv.getContext('2d');
  cv.addEventListener('pointerdown',function(e){ if(!SP.draw) return; e.preventDefault(); cv.setPointerCapture(e.pointerId); SP.down=true; SP.last=spPt(e); spDot(SP.last); });
  cv.addEventListener('pointermove',function(e){ if(!SP.down) return; e.preventDefault(); var p=spPt(e); spLine(SP.last,p); SP.last=p; });
  var up=function(){ if(SP.down){ SP.down=false; spSave(); } };
  cv.addEventListener('pointerup',up); cv.addEventListener('pointercancel',up); cv.addEventListener('pointerleave',up);
  window.addEventListener('resize',function(){ if(SP.on) spFit(true); });
}
function spPt(e){ var r=SP.cv.getBoundingClientRect(); return {x:e.clientX-r.left, y:e.clientY-r.top}; }
function spStyle(){ var c=SP.ctx; c.lineCap='round'; c.lineJoin='round'; c.globalCompositeOperation=SP.erase?'destination-out':'source-over'; c.strokeStyle=c.fillStyle=(SP.color==='ink'?spInk():SP_COL[SP.color]); c.lineWidth=SP.erase?22:SP.size; }
function spDot(p){ spStyle(); var c=SP.ctx; c.beginPath(); c.arc(p.x,p.y,(SP.erase?11:SP.size/2),0,Math.PI*2); c.fill(); }
function spLine(a,b){ spStyle(); var c=SP.ctx; c.beginPath(); c.moveTo(a.x,a.y); c.lineTo(b.x,b.y); c.stroke(); }
function spSave(){ if(SP.key&&SP.cv){ try{ SP.store[SP.key]=SP.cv.toDataURL(); }catch(e){} } }
function spClear(){ if(!SP.ctx) return; SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.clearRect(0,0,SP.cv.width,SP.cv.height); SP.ctx.restore(); if(SP.key) delete SP.store[SP.key]; }
function spFit(keep){
  var wrap=document.getElementById('wrap'); if(!wrap||!SP.cv) return;
  var r=wrap.getBoundingClientRect(), top=r.top+window.scrollY, h=Math.max(wrap.scrollHeight, window.innerHeight-r.top)+40, w=document.documentElement.clientWidth;
  var old=keep&&SP.key?SP.store[SP.key]:null, dpr=window.devicePixelRatio||1;
  SP.cv.style.top=top+'px'; SP.cv.style.left='0px'; SP.cv.style.width=w+'px'; SP.cv.style.height=h+'px';
  SP.cv.width=Math.round(w*dpr); SP.cv.height=Math.round(h*dpr); SP.ctx.setTransform(dpr,0,0,dpr,0,0);
  if(old){ var im=new Image(); im.onload=function(){ SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.drawImage(im,0,0); SP.ctx.restore(); }; im.src=old; }
}
function spLoad(){ spSave(); SP.key=spKey(); spFit(false); var d=SP.key&&SP.store[SP.key]; if(d){ var im=new Image(); im.onload=function(){ SP.ctx.save(); SP.ctx.setTransform(1,0,0,1,0,0); SP.ctx.drawImage(im,0,0); SP.ctx.restore(); }; im.src=d; } }
function spUI(){
  var bar=document.getElementById('spBar'); if(!bar) return;
  bar.querySelectorAll('.sp-pen').forEach(function(b){ b.classList.toggle('on', !SP.erase && SP.draw && b.dataset.c===SP.color); });
  bar.querySelector('[data-t=erase]').classList.toggle('on', SP.erase && SP.draw);
  bar.querySelector('[data-t=scroll]').classList.toggle('on', !SP.draw);
  SP.cv.classList.toggle('passive', !SP.draw);
  var fb=document.getElementById('spFab'); if(fb) fb.classList.toggle('on',SP.on);
}
function spToggle(on){
  spBuild(); SP.on=(on===undefined)?!SP.on:on;
  document.body.classList.toggle('sp-open',SP.on); SP.cv.style.display=SP.on?'block':'none'; document.getElementById('spBar').style.display=SP.on?'flex':'none';
  if(SP.on){ SP.draw=true; SP.erase=false; spLoad(); if(typeof kbHide==='function') kbHide(); } else { spSave(); }
  spUI();
}
(function(){ var f=document.createElement('button'); f.type='button'; f.id='spFab'; f.className='sp-fab'; f.innerHTML='✏️ <span>Scratchpad</span>'; f.title='Open a scratchpad to write your working'; f.addEventListener('click',function(){ spToggle(); }); document.body.appendChild(f); })();
var _rsSP = renderSlide;
renderSlide = function(){ _rsSP(); var fab=document.getElementById('spFab'); var q=!!swTab(); if(fab) fab.style.display=q?'':'none'; if(!q && SP.on) spToggle(false); if(SP.on) setTimeout(spLoad,30); };


/* ================= v4: attempt classification ================= */
function v4Class(item){
  if(!item) return 'un';
  if(item.status==='skipped') return 'sk';
  if(item.status==='unanswered') return 'un';
  if(item.stepStates){ // step question
    if(item.status!=='correct' && item.status!=='revealed') return 'un';
    if(item.status==='revealed' || item.stepStates.some(function(s){return s.status==='revealed';})) return 'w';
    return item.stepStates.some(function(s){return (s.attempts||0)>0;}) ? 'c2' : 'c1';
  }
  if(item.status==='revealed') return 'w';
  if(item.status==='correct') return (item.attempts||0)>0 ? 'c2' : 'c1';
  if(item.status==='wrong'||item.status==='incorrect') return 'w';
  return 'un';
}
function v4Counts(items){ var c={n:items.length,c1:0,c2:0,w:0,sk:0,un:0}; items.forEach(function(it){ c[v4Class(it)]++; }); return c; }

/* ================= v4: My record with attempt columns ================= */
renderRecord = function(){
  showChrome(false);
  var tabLabel=function(id){ var t=TAB_DEFS.find(function(x){return x.id===id;}); return t?t.label:id; };
  var title=(document.querySelector('.chapter-title')||{}).textContent||'';
  var h='<div class="rec-card"><h2>'+esc(student.name)+'’s record</h2><p class="rec-empty" style="margin:0 0 12px;">Roll '+esc(student.roll)+(title?' · '+esc(title):'')+'</p>';
  var st=appState.learning;
  h+='<h3>📘 Learning Sheet — attempts</h3><p class="v4leg"><b>1st ✓</b> correct on the first attempt · <b>2nd ✓</b> correct on the second attempt · <b>Wrong</b> still wrong after two attempts (answer revealed) · <b>Skip</b> skipped<span class="v4left"> · <b>Left</b> not done yet</span></p>';
  if(!st){ h+='<p class="rec-empty">Not started yet.</p>'; }
  else {
    var T={n:0,c1:0,c2:0,w:0,sk:0,un:0};
    h+='<div class="rec-table-wrap"><table class="rec-table v4rec"><thead><tr><th>Sheet</th><th>Qs</th><th>1st ✓</th><th>2nd ✓</th><th>Wrong</th><th>Skip</th><th class="v4left">Left</th></tr></thead><tbody>';
    TAB_DEFS.forEach(function(td){ var tt=st.tabs[td.id]; if(!tt||!tt.items||!tt.items.length) return; var c=v4Counts(tt.items);
      ['n','c1','c2','w','sk','un'].forEach(function(k){ T[k]+=c[k]; });
      h+='<tr><td>'+td.label+'</td><td>'+c.n+'</td><td class="v4g">'+c.c1+'</td><td class="v4o">'+c.c2+'</td><td class="v4r">'+c.w+'</td><td>'+c.sk+'</td><td class="v4left">'+c.un+'</td></tr>'; });
    h+='<tr class="v4tot"><td>Total</td><td>'+T.n+'</td><td class="v4g">'+T.c1+'</td><td class="v4o">'+T.c2+'</td><td class="v4r">'+T.w+'</td><td>'+T.sk+'</td><td class="v4left">'+T.un+'</td></tr>';
    h+='</tbody></table></div>';
    var doneN=T.c1+T.c2+T.w; if(doneN){ h+='<p class="v4sum">Of '+doneN+' questions answered: <b>'+Math.round(T.c1/doneN*100)+'%</b> right first time, <b>'+Math.round(T.c2/doneN*100)+'%</b> right on the second try, <b>'+Math.round(T.w/doneN*100)+'%</b> still wrong after two tries.</p>'; }
  }
  var q=appState.quiz;
  h+='<h3>📝 Quiz Mode</h3>';
  if(!q){ h+='<p class="rec-empty">Not started yet.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table v4rec"><thead><tr><th>Sheet</th><th>Qs</th><th>Status</th><th>Correct</th><th>Wrong</th></tr></thead><tbody>';
    TAB_DEFS.forEach(function(td){ var tt=q.tabs[td.id]; if(!tt||!tt.items||!tt.items.length) return; var n=tt.items.length, cor=0, att=0;
      tt.items.forEach(function(it){ if(it.status!=='unanswered'||it.choice!==undefined) att++; });
      var rec=records.filter(function(r){ return r.mode==='quiz'&&r.tab===td.id; })[0];
      if(rec){ cor=rec.correct; att=Math.max(att,rec.total); }
      h+='<tr><td>'+td.label+'</td><td>'+n+'</td><td>'+(rec?'Finished':att+' / '+n)+'</td><td class="v4g">'+(rec?cor:'—')+'</td><td class="v4r">'+(rec?(rec.total-cor):'—')+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><div class="rec-card"><h3>Finished sheets (latest first)</h3>';
  if(!records.length){ h+='<p class="rec-empty">No sheets finished yet. Each time you finish a sheet, your score is recorded here.</p>'; }
  else {
    h+='<div class="rec-table-wrap"><table class="rec-table v4rec"><thead><tr><th>When</th><th>Mode</th><th>Sheet</th><th>Score</th><th>1st ✓</th><th>2nd ✓</th><th>Wrong</th></tr></thead><tbody>';
    records.forEach(function(r){ h+='<tr><td>'+fmtDate(r.at)+'</td><td>'+(r.mode==='quiz'?'Quiz':'Learning')+'</td><td>'+tabLabel(r.tab)+'</td><td>'+r.correct+' / '+r.total+'</td><td>'+(r.c1!=null?r.c1:'—')+'</td><td>'+(r.c2!=null?r.c2:'—')+'</td><td>'+(r.w!=null?r.w:(r.mode==='quiz'?r.total-r.correct:'—'))+'</td></tr>'; });
    h+='</tbody></table></div>';
  }
  h+='</div><button class="btn btn-primary" id="btnBack">'+(MODE?'Back to practice':'Choose a mode')+'</button>';
  document.getElementById('wrap').innerHTML=h;
  document.getElementById('btnBack').addEventListener('click', function(){ if(MODE){ showChrome(true); buildTabbar(); renderSlide(); } else renderModePicker(); });
  window.scrollTo({top:0});
};
var _v4add = addRecord;
addRecord = function(mode, tabId, correct, revealed, skipped, total){
  _v4add(mode, tabId, correct, revealed, skipped, total);
  try{ if(mode==='learning'&&records[0]){ var c=v4Counts(state.tabs[tabId].items); records[0].c1=c.c1; records[0].c2=c.c2; records[0].w=c.w; saveState(); } }catch(e){}
};

/* ================= v4: celebration ================= */
function v4Cracker(){
  var ctx=ensureAudio(); if(!ctx) return; try{ if(ctx.state==='suspended') ctx.resume(); }catch(e){}
  var now=ctx.currentTime;
  function pop(t, vol, dur, hp){
    var len=Math.floor(ctx.sampleRate*dur), buf=ctx.createBuffer(1,len,ctx.sampleRate), d=buf.getChannelData(0);
    for(var i=0;i<len;i++){ d[i]=(Math.random()*2-1)*Math.pow(1-i/len,3); }
    var src=ctx.createBufferSource(); src.buffer=buf;
    var f=ctx.createBiquadFilter(); f.type='highpass'; f.frequency.value=hp;
    var g=ctx.createGain(); g.gain.setValueAtTime(vol,t); g.gain.exponentialRampToValueAtTime(0.001,t+dur);
    src.connect(f); f.connect(g); g.connect(ctx.destination); src.start(t); src.stop(t+dur+0.02);
  }
  pop(now,0.9,0.35,300);                                   // big bang
  for(var k=0;k<14;k++){ pop(now+0.35+Math.random()*1.3, 0.25+Math.random()*0.35, 0.05+Math.random()*0.08, 1500+Math.random()*2500); } // crackles
  [523.25,659.25,783.99,1046.5].forEach(function(fq,i){ var o=ctx.createOscillator(), g=ctx.createGain(); o.type='triangle'; o.frequency.value=fq;
    var t=now+0.15+i*0.12; g.gain.setValueAtTime(0.0001,t); g.gain.exponentialRampToValueAtTime(0.18,t+0.03); g.gain.exponentialRampToValueAtTime(0.001,t+0.5);
    o.connect(g); g.connect(ctx.destination); o.start(t); o.stop(t+0.55); });
}
function v4Confetti(){
  var cv=document.createElement('canvas'); cv.className='v4conf'; document.body.appendChild(cv);
  var W=cv.width=window.innerWidth*(window.devicePixelRatio||1), H=cv.height=window.innerHeight*(window.devicePixelRatio||1), s=(window.devicePixelRatio||1);
  var ctx=cv.getContext('2d'), cols=['#e8b13a','#d9534f','#2e86de','#27ae60','#9b59b6','#f39c12','#1abc9c','#ff6b9a'], P=[];
  function burst(x,y,n){ for(var i=0;i<n;i++){ var a=Math.random()*Math.PI*2, v=(4+Math.random()*9)*s;
    P.push({x:x,y:y,vx:Math.cos(a)*v,vy:Math.sin(a)*v-6*s,w:(6+Math.random()*7)*s,h:(4+Math.random()*5)*s,r:Math.random()*6,vr:(Math.random()-.5)*.4,c:cols[i%cols.length],life:0,flyer:Math.random()<.25}); } }
  burst(W*0.2,H*0.35,90); burst(W*0.8,H*0.35,90); setTimeout(function(){ burst(W*0.5,H*0.25,120); },380); setTimeout(function(){ burst(W*0.35,H*0.3,70); burst(W*0.65,H*0.3,70); },800);
  var t0=performance.now();
  (function frame(t){
    ctx.clearRect(0,0,W,H);
    P.forEach(function(p){ p.vy+=0.22*s; p.vx*=0.985; p.vy*=0.985; p.x+=p.vx; p.y+=p.vy; p.r+=p.vr; p.life++;
      ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.r); ctx.fillStyle=p.c;
      if(p.flyer){ ctx.fillRect(-p.w*1.4,-1.5*s,p.w*2.8,3*s); } else { ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h*Math.abs(Math.cos(p.life/6))); }
      ctx.restore(); });
    if(t-t0<4200) requestAnimationFrame(frame); else cv.remove();
  })(t0);
}
function v4NextTab(){
  var i=TAB_DEFS.findIndex(function(t){return t.id===activeTab;});
  for(var j=i+1;j<TAB_DEFS.length;j++){ var id=TAB_DEFS[j].id; if(id!=='theory' && SLIDES[id] && SLIDES[id].length) return TAB_DEFS[j]; }
  return null;
}
function v4Celebrate(){
  var done=document.querySelector('#wrap .done-card'); if(!done || done.dataset.v4) return; done.dataset.v4='1';
  var ts=state.tabs[activeTab], c=v4Counts(ts.items), n=ts.items.length;
  var first=(student&&student.name)?String(student.name).split(' ')[0]:'';
  var pct=MODE==='quiz'?null:Math.round((c.c1+c.c2)/Math.max(n,1)*100);
  var msg = pct===null ? 'You finished this sheet!' : (pct>=90?'Outstanding work!':pct>=75?'Excellent effort!':pct>=50?'Well done — keep going!':'Great persistence — every try makes you stronger!');
  var banner=document.createElement('div'); banner.className='v4ban';
  banner.innerHTML='<div class="v4trophy">🏆</div><div class="v4h">Congratulations'+(first?', '+esc(first):'')+'!</div><div class="v4m">'+msg+'</div>'+
    (MODE==='quiz'?'':'<div class="v4pills"><span class="v4p g">✅ '+c.c1+' first attempt</span><span class="v4p o">🔁 '+c.c2+' second attempt</span><span class="v4p r">❌ '+c.w+' finally wrong</span>'+(c.sk?'<span class="v4p s">⏭ '+c.sk+' skipped</span>':'')+'</div>');
  done.insertBefore(banner, done.firstChild);
  var nx=v4NextTab(), wrapB=document.createElement('div'); wrapB.className='v4next';
  if(nx){ wrapB.innerHTML='<button class="btn btn-primary v4go" id="v4Next">Next sheet: '+nx.label+' →</button>'; }
  else if(SLIDES.report!==undefined || TAB_DEFS.some(function(t){return t.id==='report';})){ wrapB.innerHTML='<button class="btn btn-primary v4go" id="v4Next">📊 View my report →</button>'; }
  else { wrapB.innerHTML='<button class="btn btn-primary v4go" id="v4Next">⌂ Back to the home page</button>'; }
  banner.appendChild(wrapB);
  document.getElementById('v4Next').addEventListener('click',function(){
    var t=nx?nx.id:(TAB_DEFS.some(function(x){return x.id==='report';})?'report':(TAB_DEFS[0]&&TAB_DEFS[0].id));
    activeTab=t; showChrome(true); buildTabbar(); renderSlide(); window.scrollTo({top:0,behavior:'smooth'}); });
  setTimeout(function(){ var r=banner.getBoundingClientRect(); window.scrollBy({top:r.top-110,behavior:'smooth'}); },60);
  v4Confetti(); v4Cracker();
}
var _v4rf = renderFinished;
renderFinished = function(){ _v4rf.apply(this,arguments); try{ v4Celebrate(); }catch(e){ console.log('v4',e); } };


/* ================= calculus answer mode ================= */
function calcCompile(src){
  var s=String(src).replace(/\s+/g,'').replace(/[×∗·]/g,'*').replace(/÷/g,'/').replace(/[−–—]/g,'-')
    .replace(/²/g,'^2').replace(/³/g,'^3').replace(/π/g,'#').replace(/eˣ/g,'e^x');
  if(s.indexOf('=')>=0) s=s.slice(s.lastIndexOf('=')+1);
  var FN=['sqrt','abs','ln','log','exp','sin','cos','tan','sec','csc','cot','pi'];
  var i=0,toks=[];
  while(i<s.length){
    var ch=s[i];
    if(/[0-9.]/.test(ch)){ var j=i; while(j<s.length&&/[0-9.]/.test(s[j])) j++; toks.push({k:'n',v:parseFloat(s.slice(i,j))}); i=j; continue; }
    if(ch==='√'){ toks.push({k:'f',v:'sqrt'}); i++; continue; }
    if(/[a-zA-Z#]/.test(ch)){
      var hit=null; for(var q=0;q<FN.length;q++){ if(s.substr(i,FN[q].length).toLowerCase()===FN[q]){ hit=FN[q]; break; } }
      if(hit==='pi'){ toks.push({k:'v',v:'#'}); i+=2; continue; }
      if(hit){ toks.push({k:'f',v:hit}); i+=hit.length; continue; }
      toks.push({k:'v',v:ch}); i++; continue; }
    if('+-*/^()|'.indexOf(ch)>=0){ toks.push({k:ch}); i++; continue; }
    return null;
  }
  // absolute value bars -> abs( )
  var t2=[],open=false; for(var a=0;a<toks.length;a++){ var tk=toks[a]; if(tk.k==='|'){ if(!open){ t2.push({k:'f',v:'abs'}); t2.push({k:'('}); open=true; } else { t2.push({k:')'}); open=false; } } else t2.push(tk); }
  toks=t2;
  var out=[];
  for(var t=0;t<toks.length;t++){ var A=toks[t], B=out[out.length-1];
    if(B&&(B.k==='n'||B.k==='v'||B.k===')')&&(A.k==='n'||A.k==='v'||A.k==='('||A.k==='f')) out.push({k:'&'});
    out.push(A); }
  var p=0; function pk(){ return out[p]; }
  var F={sqrt:Math.sqrt,ln:Math.log,log:function(x){return Math.log(x)/Math.LN10;},exp:Math.exp,sin:Math.sin,cos:Math.cos,tan:Math.tan,
    sec:function(x){return 1/Math.cos(x);},csc:function(x){return 1/Math.sin(x);},cot:function(x){return 1/Math.tan(x);},abs:Math.abs};
  function E(){ var n=T(); while(pk()&&(pk().k==='+'||pk().k==='-')){ var o=out[p++].k,r=T(); n=(function(l,r,o){return function(e){return o==='+'?l(e)+r(e):l(e)-r(e);};})(n,r,o);} return n; }
  function T(){ var n=I(); while(pk()&&(pk().k==='*'||pk().k==='/')){ var o=out[p++].k,r=I(); n=(function(l,r,o){return function(e){return o==='*'?l(e)*r(e):l(e)/r(e);};})(n,r,o);} return n; }
  function I(){ var n=U(); while(pk()&&pk().k==='&'){ p++; var r=P(); n=(function(l,r){return function(e){return l(e)*r(e);};})(n,r);} return n; }
  function U(){ if(pk()&&pk().k==='-'){ p++; var u=U(); return function(e){return -u(e);}; } if(pk()&&pk().k==='+'){ p++; return U(); } return P(); }
  function P(){ var b=Aa(); if(pk()&&pk().k==='^'){ p++; var x=U(); return function(e){return Math.pow(b(e),x(e));}; } return b; }
  function Aa(){ var t=out[p++]; if(!t) throw 0;
    if(t.k==='n') return function(){return t.v;};
    if(t.k==='v'){ if(t.v==='#') return function(){return Math.PI;}; if(t.v==='e') return function(){return Math.E;}; return function(e){return e[t.v];}; }
    if(t.k==='('){ var n=E(); if(!pk()||pk().k!==')') throw 0; p++; return n; }
    if(t.k==='f'){ var fn=F[t.v]; var ex=null;
      if(pk()&&pk().k==='^'){ p++; ex=Aa(); if(pk()&&pk().k==='&') p++; }            // sin^2(x)
      var arg; if(pk()&&pk().k==='('){ p++; arg=E(); if(!pk()||pk().k!==')') throw 0; p++; } else arg=P();
      return ex? function(e){ return Math.pow(fn(arg(e)),ex(e)); } : function(e){ return fn(arg(e)); }; }
    throw 0; }
  try{ var f=E(); if(p!==out.length) return null; return f; }catch(e){ return null; }
}
function calcEqual(input,answer){
  var f=calcCompile(input), g=calcCompile(answer); if(!f||!g) return false;
  var hits=0;
  for(var trial=0;trial<14;trial++){
    var env={}; 'abcdfghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'.split('').forEach(function(c){ env[c]=0.35+Math.random()*2.3; });
    var x=f(env), y=g(env); if(!isFinite(x)||!isFinite(y)) continue;
    if(Math.abs(x-y)>1e-6*Math.max(1,Math.abs(x),Math.abs(y))) return false; hits++;
  }
  return hits>=4;
}
(function(){
  var _am=answerMatches;
  answerMatches=function(input,answer,accept,expr){
    if(expr==='calc'){ if(input===undefined||input===null||String(input).trim()==='') return false;
      if(calcEqual(input,answer)) return true; return (accept||[]).some(function(a){ return calcEqual(input,a); }); }
    return _am.apply(this,arguments); };
  var _kl=kbLayoutFor;
  kbLayoutFor=function(inp){ try{ var ts=state.tabs[activeTab], sl=SLIDES[activeTab][ts.idx], stp=sl.flat[parseInt(inp.dataset.step,10)]; if(stp.expr==='calc') return 'calc'; }catch(e){} return _kl(inp); };
  var _kp=kbPress;
  kbPress=function(k){ var m={'eˣ':'e^(','√':'√(','ln':'ln(','sin':'sin(','cos':'cos(','tan':'tan('}; if(KB.page==='calc'&&m[k]){ kbInsert(m[k]); return; } return _kp(k); };
})();

renderLogin();
})();
</script>
</body>
</html>
