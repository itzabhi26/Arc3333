<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ARC — 3333 Collection</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,500;0,9..144,600;1,9..144,400;1,9..144,500&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#E5EBD7;
    --cream:#F4F5EA;
    --ivory:#FAF9F1;
    --sage:#C8D2B5;
    --sage-deep:#8A9578;
    --olive:#5E6850;
    --ink:#20251D;
    --muted:#687060;
    --gold:#A9884F;
    --line: rgba(32,37,29,0.12);
    --radius-lg: 28px;
    --radius-md: 18px;
    --radius-sm: 10px;
    --shadow-soft: 0 20px 60px rgba(94,104,80,0.16);
    --ease: cubic-bezier(.22,.9,.32,1);
  }
  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    margin:0;
    background:var(--bg);
    color:var(--ink);
    font-family:'Space Grotesk', sans-serif;
    -webkit-font-smoothing:antialiased;
    overflow-x:hidden;
  }
  h1,h2,h3,.serif{
    font-family:'Fraunces', serif;
    font-weight:500;
    letter-spacing:-0.01em;
    margin:0;
  }
  p{margin:0;color:var(--muted); line-height:1.6;}
  a{color:inherit;}
  button{font-family:inherit; cursor:pointer;}
  ::selection{background:var(--olive); color:var(--ivory);}

  .wrap{max-width:1180px; margin:0 auto; padding:0 32px;}
  @media (max-width:640px){ .wrap{padding:0 20px;} }

  /* ---------- NAV ---------- */
  #nav{
    position:fixed; top:0; left:0; right:0; z-index:200;
    display:flex; align-items:center; justify-content:space-between;
    padding:20px 32px;
    transition: background .4s var(--ease), backdrop-filter .4s var(--ease), padding .3s var(--ease), border-color .4s var(--ease);
    border-bottom:1px solid transparent;
  }
  #nav.scrolled{
    background:rgba(244,245,234,0.72);
    backdrop-filter:blur(16px) saturate(140%);
    -webkit-backdrop-filter:blur(16px) saturate(140%);
    padding:14px 32px;
    border-color:var(--line);
  }
  .brand{display:flex; align-items:center; gap:10px; text-decoration:none;}
  .brand img{width:32px; height:32px; border-radius:8px; display:block;}
  .brand span{font-family:'Fraunces',serif; font-size:19px; letter-spacing:0.02em; font-weight:500;}
  .nav-links{display:flex; align-items:center; gap:36px; list-style:none; margin:0; padding:0;}
  .nav-links a{font-size:14px; text-decoration:none; color:var(--ink); position:relative; padding:4px 0;}
  .nav-links a::after{content:'';position:absolute;left:0;bottom:0;height:1px;width:0;background:var(--olive);transition:width .3s var(--ease);}
  .nav-links a:hover::after{width:100%;}
  .nav-cta{
    background:var(--ink); color:var(--ivory); border:none; padding:11px 22px; border-radius:100px;
    font-size:13px; letter-spacing:0.04em; font-weight:500; transition:transform .25s var(--ease), background .25s;
  }
  .nav-cta:hover{transform:translateY(-2px); background:var(--olive);}
  .nav-toggle{display:none; background:none; border:none; padding:8px;}
  .nav-toggle span{display:block; width:22px; height:2px; background:var(--ink); margin:5px 0; transition:.3s;}
  @media (max-width:860px){
    .nav-links{position:fixed; top:0; right:0; height:100vh; width:78%; max-width:320px; background:var(--ivory);
      flex-direction:column; justify-content:center; align-items:flex-start; gap:26px; padding:0 40px;
      transform:translateX(100%); transition:transform .4s var(--ease); box-shadow:-10px 0 40px rgba(0,0,0,0.08);}
    .nav-links.open{transform:translateX(0);}
    .nav-links a{font-size:20px;}
    .nav-cta{display:none;}
    .nav-toggle{display:block; z-index:210;}
  }

  /* ---------- BUBBLE / DOODLE FIELD ---------- */
  .bubble-field{position:absolute; inset:0; overflow:hidden; pointer-events:none;}
  .bubble{
    position:absolute; border-radius:50%;
    background: radial-gradient(circle at 32% 28%, rgba(255,255,255,0.85), rgba(200,210,181,0.35) 45%, rgba(94,104,80,0.12) 75%);
    box-shadow: inset 0 0 22px rgba(255,255,255,0.5), 0 18px 40px rgba(94,104,80,0.14);
    backdrop-filter: blur(1px);
    will-change: transform;
  }
  .bubble.solid{
    background: radial-gradient(circle at 30% 25%, #ffffff, var(--sage) 55%, var(--sage-deep) 100%);
  }
  .doodle{position:absolute; opacity:0.5; color:var(--olive); will-change:transform;}

  @keyframes drift{
    0%{transform:translate(0,0) rotate(0deg);}
    50%{transform:translate(var(--dx,14px),var(--dy,-18px)) rotate(6deg);}
    100%{transform:translate(0,0) rotate(0deg);}
  }
  @keyframes spin-slow{ to{ transform:rotate(360deg); } }

  /* ---------- HERO ---------- */
  #hero{position:relative; min-height:100vh; display:flex; align-items:center; padding-top:120px; padding-bottom:80px;}
  .hero-grid{display:grid; grid-template-columns:1.1fr 0.9fr; gap:40px; align-items:center; position:relative; z-index:2;}
  @media (max-width:900px){ .hero-grid{grid-template-columns:1fr;} }
  .eyebrow{font-size:13px; letter-spacing:0.14em; color:var(--olive); font-weight:600; display:flex; align-items:center; gap:10px; margin-bottom:22px;}
  .eyebrow .dot{width:7px;height:7px;border-radius:50%;background:var(--gold); box-shadow:0 0 0 5px rgba(169,136,79,0.18); animation: pulse 2.4s ease-in-out infinite;}
  @keyframes pulse{ 0%,100%{box-shadow:0 0 0 5px rgba(169,136,79,0.18);} 50%{box-shadow:0 0 0 9px rgba(169,136,79,0.06);} }
  h1.headline{font-size:clamp(44px,7vw,84px); line-height:0.98; letter-spacing:-0.02em;}
  .headline em{font-style:italic; color:var(--olive);}
  .sub{font-size:19px; margin-top:22px; max-width:480px; color:var(--muted); font-weight:400;}
  .stat-rail{display:flex; gap:0; margin-top:40px; border-top:1px solid var(--line); border-bottom:1px solid var(--line);}
  .stat{padding:18px 26px 18px 0; margin-right:26px; border-right:1px solid var(--line);}
  .stat:last-child{border-right:none;}
  .stat .num{font-family:'Fraunces',serif; font-size:26px; display:block;}
  .stat .lbl{font-size:11.5px; letter-spacing:0.08em; color:var(--muted); margin-top:3px; display:block;}
  .cta-row{display:flex; gap:16px; margin-top:38px; flex-wrap:wrap;}
  .btn-primary{
    background:var(--ink); color:var(--ivory); border:none; padding:17px 30px; border-radius:100px;
    font-size:14.5px; letter-spacing:0.03em; font-weight:500; display:inline-flex; align-items:center; gap:10px;
    transition:transform .3s var(--ease), background .3s, box-shadow .3s; box-shadow:0 14px 30px rgba(32,37,29,0.18);
  }
  .btn-primary:hover{transform:translateY(-3px); background:var(--olive);}
  .btn-secondary{
    background:transparent; color:var(--ink); border:1px solid var(--ink); padding:16px 28px; border-radius:100px;
    font-size:14.5px; letter-spacing:0.03em; font-weight:500; transition:.3s var(--ease);
  }
  .btn-secondary:hover{background:var(--ink); color:var(--ivory);}

  .hero-visual{position:relative; height:520px; display:flex; align-items:center; justify-content:center;}
  .orb-stage{position:relative; width:100%; height:100%;}
  .orb-core{
    position:absolute; top:50%; left:50%; width:230px; height:230px; border-radius:50%; transform:translate(-50%,-50%);
    background: radial-gradient(circle at 35% 30%, #ffffff 0%, var(--cream) 30%, var(--sage) 65%, var(--sage-deep) 100%);
    box-shadow: 0 40px 90px rgba(94,104,80,0.28), inset 0 0 40px rgba(255,255,255,0.6);
    display:flex; align-items:center; justify-content:center;
    animation: float-core 7s ease-in-out infinite;
  }
  @keyframes float-core{ 0%,100%{ transform:translate(-50%,-50%) translateY(0);} 50%{ transform:translate(-50%,-50%) translateY(-16px);} }
  .orb-core img{width:96px; height:96px; opacity:0.92; filter:drop-shadow(0 10px 20px rgba(0,0,0,0.15));}
  .orbit-ring{position:absolute; top:50%; left:50%; border:1px dashed rgba(94,104,80,0.35); border-radius:50%; transform:translate(-50%,-50%);}

  /* ---------- STATUS BAR ---------- */
  .status-bar{
    display:inline-flex; align-items:center; gap:10px; background:var(--ivory); border:1px solid var(--line);
    padding:9px 18px 9px 14px; border-radius:100px; font-size:12.5px; letter-spacing:0.06em; font-weight:600; color:var(--olive);
    margin-bottom:26px;
  }
  .status-bar .led{width:8px;height:8px;border-radius:50%; background:var(--olive); position:relative;}
  .status-bar .led::after{content:'';position:absolute;inset:-4px;border-radius:50%;border:1px solid var(--olive); animation:ring 1.8s ease-out infinite;}
  @keyframes ring{ 0%{transform:scale(0.6); opacity:0.9;} 100%{transform:scale(1.9); opacity:0;} }

  /* ---------- SECTIONS ---------- */
  section{position:relative; padding:110px 0;}
  @media (max-width:640px){ section{padding:70px 0;} }
  .section-head{max-width:640px; margin-bottom:56px;}
  .section-head .kicker{font-size:13px; letter-spacing:0.12em; color:var(--gold); font-weight:600; margin-bottom:14px; display:block;}
  .section-head h2{font-size:clamp(30px,4vw,46px); line-height:1.08;}
  .section-head p{margin-top:16px; font-size:17px;}

  /* Follow X + WL card */
  #waitlist{background:var(--cream); border-radius:40px; margin:0 20px; overflow:hidden;}
  @media (max-width:640px){ #waitlist{margin:0 10px; border-radius:26px;} }
  .wl-grid{display:grid; grid-template-columns:0.9fr 1.1fr; gap:0;}
  @media (max-width:900px){ .wl-grid{grid-template-columns:1fr;} }
  .wl-info{padding:64px 56px; display:flex; flex-direction:column; justify-content:center;}
  @media (max-width:640px){ .wl-info{padding:44px 26px;} }
  .wl-panel{padding:64px 56px; background:var(--ivory); position:relative;}
  @media (max-width:640px){ .wl-panel{padding:40px 26px;} }
  .step-list{list-style:none; margin:28px 0 0; padding:0; display:flex; flex-direction:column; gap:18px;}
  .step-list li{display:flex; gap:14px; font-size:14.5px; color:var(--muted); align-items:flex-start;}
  .step-num{width:26px; height:26px; border-radius:50%; border:1px solid var(--olive); color:var(--olive); font-size:12px;
    display:flex; align-items:center; justify-content:center; flex-shrink:0; font-weight:600;}
  .step-list li.done .step-num{background:var(--olive); color:var(--ivory);}

  .field{margin-bottom:20px;}
  .field label{display:block; font-size:12.5px; letter-spacing:0.05em; color:var(--olive); font-weight:600; margin-bottom:8px;}
  .field input{
    width:100%; padding:15px 17px; border-radius:14px; border:1px solid var(--line); background:var(--ivory);
    font-family:inherit; font-size:15px; color:var(--ink); transition:border-color .25s, box-shadow .25s;
  }
  #waitlist .field input{background:var(--cream);}
  .field input:focus{outline:none; border-color:var(--olive); box-shadow:0 0 0 4px rgba(138,149,120,0.18);}
  .field .hint{font-size:12px; color:var(--muted); margin-top:6px;}
  .field .err{font-size:12.5px; color:#a8493a; margin-top:6px; display:none;}
  .field.invalid input{border-color:#a8493a;}
  .field.invalid .err{display:block;}

  .btn-x{
    display:inline-flex; align-items:center; gap:10px; background:var(--ink); color:var(--ivory); border:none;
    padding:14px 24px; border-radius:100px; font-size:14px; font-weight:500; transition:.3s var(--ease); text-decoration:none;
  }
  .btn-x:hover{background:var(--olive); transform:translateY(-2px);}
  .btn-submit{
    width:100%; background:var(--ink); color:var(--ivory); border:none; padding:17px; border-radius:14px;
    font-size:15px; font-weight:600; letter-spacing:0.02em; transition:.3s var(--ease); margin-top:6px;
  }
  .btn-submit:hover:not(:disabled){background:var(--olive);}
  .btn-submit:disabled{opacity:0.45; cursor:not-allowed;}

  .form-msg{margin-top:18px; padding:16px 18px; border-radius:14px; font-size:14px; display:none; align-items:flex-start; gap:10px;}
  .form-msg.show{display:flex;}
  .form-msg.success{background:rgba(138,149,120,0.16); color:var(--olive);}
  .form-msg.error{background:rgba(168,73,58,0.1); color:#a8493a;}
  .form-msg.info{background:rgba(169,136,79,0.12); color:var(--gold);}

  .progress-wrap{margin-top:30px;}
  .progress-track{height:8px; background:var(--sage); border-radius:100px; overflow:hidden;}
  .progress-fill{height:100%; background:linear-gradient(90deg,var(--olive),var(--gold)); border-radius:100px; width:0%; transition:width 1s var(--ease);}
  .progress-label{font-size:12.5px; color:var(--muted); margin-top:8px; letter-spacing:0.02em;}

  /* spinner */
  .spin{width:16px;height:16px;border-radius:50%;border:2px solid rgba(250,249,241,0.4); border-top-color:var(--ivory); animation:spin-slow .7s linear infinite; display:inline-block;}

  /* Collection gallery */
  .gallery{display:grid; grid-template-columns:repeat(4,1fr); gap:18px;}
  @media (max-width:900px){ .gallery{grid-template-columns:repeat(2,1fr);} }
  @media (max-width:520px){ .gallery{grid-template-columns:1fr 1fr; gap:12px;} }
  .tile{
    aspect-ratio:1/1; border-radius:22px; position:relative; overflow:hidden; cursor:pointer;
    transform:perspective(700px) rotateX(0) rotateY(0); transition:transform .4s var(--ease), box-shadow .4s var(--ease);
    box-shadow:0 10px 26px rgba(94,104,80,0.14);
  }
  .tile:hover{transform:perspective(700px) rotateX(4deg) rotateY(-6deg) translateY(-6px); box-shadow:0 26px 50px rgba(94,104,80,0.24);}
  .tile-art{position:absolute; inset:0;}
  .tile-tag{position:absolute; bottom:12px; left:12px; background:rgba(250,249,241,0.85); backdrop-filter:blur(6px);
    padding:5px 12px; border-radius:100px; font-size:11px; letter-spacing:0.06em; font-weight:600; color:var(--olive);}

  /* Archive */
  .archive-grid{display:grid; grid-template-columns:repeat(6,1fr); gap:14px;}
  @media (max-width:900px){ .archive-grid{grid-template-columns:repeat(3,1fr);} }
  .archive-tile{aspect-ratio:1/1; border-radius:16px; position:relative; overflow:hidden; background:var(--sage);}
  .archive-tile.blurred .tile-art{filter:blur(9px) saturate(0.9);}
  .archive-tile.silhouette .tile-art{filter:brightness(0.15) saturate(0);}
  .archive-tile.soon{display:flex; align-items:center; justify-content:center; background:var(--cream);}
  .archive-tile.soon span{font-size:11px; letter-spacing:0.08em; color:var(--muted); font-weight:600;}
  .archive-state{position:absolute; top:8px; right:8px; font-size:9.5px; letter-spacing:0.05em; background:rgba(32,37,29,0.55);
    color:var(--ivory); padding:3px 8px; border-radius:100px; font-weight:600;}

  /* Why / Arc split */
  .split{display:grid; grid-template-columns:1fr 1fr; gap:70px; align-items:center;}
  @media (max-width:900px){ .split{grid-template-columns:1fr; gap:36px;} }
  .why-mark{font-family:'Fraunces',serif; font-size:clamp(90px,14vw,160px); line-height:0.8; color:transparent;
    -webkit-text-stroke:1.4px var(--olive); letter-spacing:-0.02em;}

  .arc-points{list-style:none; margin:26px 0 0; padding:0; display:flex; flex-direction:column; gap:16px;}
  .arc-points li{display:flex; gap:12px; font-size:15px; color:var(--muted); align-items:flex-start;}
  .arc-points svg{flex-shrink:0; margin-top:3px; color:var(--olive);}

  /* Updates */
  .updates-list{display:flex; flex-direction:column; border-top:1px solid var(--line);}
  .update-row{display:flex; gap:20px; padding:18px 0; border-bottom:1px solid var(--line); font-size:14.5px; align-items:baseline;}
  .update-row time{color:var(--muted); font-size:12.5px; min-width:110px;}

  /* FAQ */
  .faq-item{border-bottom:1px solid var(--line);}
  .faq-q{width:100%; text-align:left; background:none; border:none; padding:22px 0; display:flex; justify-content:space-between;
    align-items:center; font-family:'Fraunces',serif; font-size:18px; color:var(--ink);}
  .faq-icon{width:20px;height:20px; position:relative; flex-shrink:0;}
  .faq-icon::before,.faq-icon::after{content:'';position:absolute; background:var(--ink); top:50%; left:50%; transform:translate(-50%,-50%);}
  .faq-icon::before{width:14px;height:1.4px;}
  .faq-icon::after{width:1.4px;height:14px; transition:transform .3s var(--ease);}
  .faq-item.open .faq-icon::after{transform:translate(-50%,-50%) rotate(90deg) scaleY(0);}
  .faq-a{max-height:0; overflow:hidden; transition:max-height .35s var(--ease);}
  .faq-a p{padding:0 0 22px; font-size:15px; max-width:640px;}

  /* Links / footer */
  .link-cards{display:grid; grid-template-columns:repeat(3,1fr); gap:16px;}
  @media (max-width:760px){ .link-cards{grid-template-columns:1fr;} }
  .link-card{background:var(--ivory); border:1px solid var(--line); border-radius:20px; padding:26px; text-decoration:none;
    display:flex; flex-direction:column; gap:6px; transition:transform .3s var(--ease), box-shadow .3s var(--ease);}
  .link-card:hover{transform:translateY(-4px); box-shadow:var(--shadow-soft);}
  .link-card .lbl{font-size:11.5px; letter-spacing:0.08em; color:var(--muted); font-weight:600;}
  .link-card .name{font-family:'Fraunces',serif; font-size:19px;}
  .warn-box{margin-top:26px; background:rgba(168,73,58,0.08); border:1px solid rgba(168,73,58,0.2); border-radius:16px;
    padding:18px 20px; font-size:13.5px; color:#8a4335; display:flex; gap:10px;}

  footer{padding:60px 0 40px; border-top:1px solid var(--line); margin-top:40px;}
  .foot-grid{display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:20px;}
  .foot-security{font-size:12.5px; color:var(--muted); max-width:420px;}

  /* Eligibility */
  .elig-card{max-width:560px; margin:0 auto; background:var(--ivory); border-radius:28px; padding:52px; text-align:center; box-shadow:var(--shadow-soft);}
  @media (max-width:640px){ .elig-card{padding:34px 24px;} }
  .elig-result{margin-top:24px; display:none;}
  .elig-badge{display:inline-block; padding:12px 26px; border-radius:100px; font-family:'Fraunces',serif; font-size:22px; margin-top:10px;}
  .elig-badge.granted{background:rgba(138,149,120,0.18); color:var(--olive);}
  .elig-badge.not-selected{background:rgba(104,112,96,0.14); color:var(--muted);}

  /* Access card */
  .access-card{
    max-width:400px; margin:26px auto 0; border-radius:26px; padding:34px; position:relative; overflow:hidden;
    background: linear-gradient(155deg, var(--ivory), var(--cream) 60%, var(--sage) 130%);
    border:1px solid var(--line); box-shadow:0 30px 60px rgba(94,104,80,0.22);
    animation: card-reveal .8s var(--ease);
  }
  @keyframes card-reveal{ from{ opacity:0; transform: translateY(24px) scale(0.96) rotateX(8deg);} to{opacity:1; transform:none;} }
  .access-card .ac-top{display:flex; justify-content:space-between; align-items:center;}
  .access-card .ac-logo{width:30px;height:30px; border-radius:8px;}
  .access-card .ac-tag{font-size:10.5px; letter-spacing:0.1em; color:var(--olive); font-weight:700;}
  .access-card h3{font-size:26px; margin-top:26px;}
  .access-card .ac-user{font-size:14px; color:var(--muted); margin-top:6px;}
  .access-card .ac-status{margin-top:22px; display:inline-block; padding:8px 16px; border-radius:100px; background:var(--olive); color:var(--ivory); font-size:12px; letter-spacing:0.06em; font-weight:600;}
  .access-card .ac-id{margin-top:22px; font-size:10.5px; letter-spacing:0.08em; color:var(--muted); font-family:monospace;}

  /* Admin */
  #admin-toggle{position:fixed; bottom:18px; left:18px; z-index:150; font-size:10.5px; letter-spacing:0.06em; color:var(--muted);
    background:rgba(244,245,234,0.7); backdrop-filter:blur(6px); border:1px solid var(--line); padding:7px 12px; border-radius:100px;}
  #admin-overlay{position:fixed; inset:0; background:rgba(32,37,29,0.5); z-index:500; display:none; align-items:center; justify-content:center; padding:20px;}
  #admin-overlay.show{display:flex;}
  #admin-panel{background:var(--ivory); border-radius:26px; max-width:920px; width:100%; max-height:88vh; overflow-y:auto; padding:40px;}
  @media (max-width:640px){ #admin-panel{padding:24px;} }
  .admin-row{display:flex; justify-content:space-between; align-items:center; margin-bottom:24px;}
  .admin-section{margin-bottom:30px; padding-bottom:26px; border-bottom:1px solid var(--line);}
  .admin-section h4{font-family:'Fraunces',serif; font-size:17px; margin-bottom:14px;}
  .admin-grid{display:grid; grid-template-columns:repeat(auto-fit,minmax(160px,1fr)); gap:10px;}
  .pill-btn{padding:10px 14px; border-radius:12px; border:1px solid var(--line); background:var(--cream); font-size:12.5px; font-weight:600; text-align:left; transition:.2s;}
  .pill-btn.active{background:var(--olive); color:var(--ivory); border-color:var(--olive);}
  .admin-table{width:100%; border-collapse:collapse; font-size:12.5px;}
  .admin-table th{text-align:left; padding:8px 10px; color:var(--muted); font-weight:600; border-bottom:1px solid var(--line); font-size:11px; letter-spacing:0.04em;}
  .admin-table td{padding:9px 10px; border-bottom:1px solid var(--line); font-family:monospace; font-size:11.5px;}
  .admin-table .status-tag{font-family:'Space Grotesk',sans-serif; padding:3px 9px; border-radius:100px; font-size:10.5px; font-weight:600;}
  .st-pending{background:rgba(169,136,79,0.15); color:var(--gold);}
  .st-granted{background:rgba(138,149,120,0.2); color:var(--olive);}
  .st-not{background:rgba(104,112,96,0.14); color:var(--muted);}
  .mini-btn{font-size:10.5px; padding:4px 9px; border-radius:8px; border:1px solid var(--line); background:var(--ivory); margin-right:4px;}
  .close-admin{background:none; border:none; font-size:22px; color:var(--muted); line-height:1;}
  .admin-input{padding:10px 12px; border-radius:10px; border:1px solid var(--line); font-family:inherit; font-size:13px; width:100%;}

  .disclaimer-note{font-size:11.5px; color:var(--muted); background:rgba(169,136,79,0.1); border-radius:10px; padding:10px 12px; margin-top:16px; line-height:1.5;}

  @media (prefers-reduced-motion: reduce){
    *{animation-duration:0.001s !important; animation-iteration-count:1 !important; transition-duration:0.001s !important; scroll-behavior:auto !important;}
  }
</style>
</head>
<body>

<div class="bubble-field" id="global-bubbles"></div>

<nav id="nav">
  <a href="#hero" class="brand"><img src="data:image/jpeg;base64,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sWLFixQnxQ215v6tjGaE+RKxYsWLFixYsWLFixYsWLFixPuM5ScvMebHmsmVExkde69xKBJRI1a6IZLY/RH8CTsWIIIIIIILly5cuXLlypoWwl3TbfyN5JGyRjRO8d5ZcuXLly5cuXLly5cuXLly5cuXLk5DPlJfzF8R27n5fHpIkHkGy2Lly5cuXLly5cuXLly5fpl+9bEROJnE9UwB9DJlx4S9m+hXLly5cuXLly5cuXLly5cuXLly5cuSKEVzMmlLeqzvp7DkXLly5cuXLlixYsWLFixYsWLDRBcuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFy5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5YsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLEEFixYsWLFixYsWLEEFixBBYsWLFixYsWLFixBBYsWLFixYsWLFixcuWLFi34kAAAAAALFixYuXLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFj//Z" alt="ARC logo"><span>ARC / 3333</span></a>
  <ul class="nav-links" id="navLinks">
    <li><a href="#collection">Collection</a></li>
    <li><a href="#eligibility">Eligibility</a></li>
    <li><a href="#arc">Arc</a></li>
    <li><a href="#links" target="_self">X</a></li>
  </ul>
  <a href="#waitlist" class="nav-cta">Join Waitlist</a>
  <button class="nav-toggle" id="navToggle" aria-label="Menu"><span></span><span></span><span></span></button>
</nav>

<!-- ================= HERO ================= -->
<section id="hero">
  <div class="bubble-field" id="hero-bubbles"></div>
  <div class="wrap hero-grid">
    <div>
      <div class="status-bar" id="statusBadge"><span class="led"></span><span id="statusText">WAITLIST OPEN</span></div>
      <div class="eyebrow"><span class="dot"></span> A NEW COLLECTION ON ARC</div>
      <h1 class="headline">THE <em>ARC</em> ERA<br>BEGINS</h1>
      <p class="sub">3,333 unique digital collectibles, minted on OpenSea. Join the waitlist to be considered for early access.</p>
      <div class="stat-rail">
        <div class="stat"><span class="num">3,333</span><span class="lbl">TOTAL SUPPLY</span></div>
        <div class="stat"><span class="num" id="mintDateStat">TBA</span><span class="lbl">MINT DATE</span></div>
        <div class="stat"><span class="num">Arc</span><span class="lbl">NETWORK</span></div>
      </div>
      <div class="cta-row">
        <a href="#waitlist" class="btn-primary">Join the Waitlist →</a>
        <a href="#collection" class="btn-secondary">View Collection</a>
      </div>
    </div>
    <div class="hero-visual">
      <div class="orb-stage" id="orbStage">
        <div class="orbit-ring" style="width:420px;height:420px; animation: spin-slow 40s linear infinite;"></div>
        <div class="orbit-ring" style="width:320px;height:320px; animation: spin-slow 30s linear infinite reverse;"></div>
        <div class="orb-core"><img src="data:image/jpeg;base64,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sWLFixQnxQ215v6tjGaE+RKxYsWLFixYsWLFixYsWLFixPuM5ScvMebHmsmVExkde69xKBJRI1a6IZLY/RH8CTsWIIIIIIILly5cuXLlypoWwl3TbfyN5JGyRjRO8d5ZcuXLly5cuXLly5cuXLly5cuXLk5DPlJfzF8R27n5fHpIkHkGy2Lly5cuXLly5cuXLly5fpl+9bEROJnE9UwB9DJlx4S9m+hXLly5cuXLly5cuXLly5cuXLly5cuSKEVzMmlLeqzvp7DkXLly5cuXLlixYsWLFixYsWLDRBcuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFy5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5YsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLEEFixYsWLFixYsWLEEFixBBYsWLFixYsWLFixBBYsWLFixYsWLFixcuWLFi34kAAAAAALFixYuXLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFj//Z" alt="ARC collection mark"></div>
      </div>
    </div>
  </div>
</section>

<!-- ================= X FOLLOW + WAITLIST ================= -->
<section id="waitlist">
  <div class="wl-grid">
    <div class="wl-info">
      <span class="section-head kicker" style="display:block;margin-bottom:14px;">WAITLIST ACCESS</span>
      <h2>Two steps.<br>Then you're on the list.</h2>
      <p style="margin-top:16px;">Follow the official account, then submit your X username and wallet address. Your wallet is stored privately and locked once submitted.</p>
      <ul class="step-list" id="stepList">
        <li class="step" data-step="1"><span class="step-num">1</span><span>Follow <b id="xHandleText">@ArcCollection</b> on X</span></li>
        <li class="step" data-step="2"><span class="step-num">2</span><span>Submit your X username</span></li>
        <li class="step" data-step="3"><span class="step-num">3</span><span>Submit your wallet address</span></li>
      </ul>
      <div class="progress-wrap" id="progressWrap" style="display:none;">
        <div class="progress-track"><div class="progress-fill" id="progressFill"></div></div>
        <div class="progress-label" id="progressLabel">WL ACCESS</div>
      </div>
    </div>
    <div class="wl-panel">
      <div id="followBlock">
        <label style="display:block; font-size:12.5px; letter-spacing:0.05em; color:var(--olive); font-weight:600; margin-bottom:14px;">STEP 1 — FOLLOW ON X</label>
        <a href="https://x.com/ArcCollection" target="_blank" rel="noopener" class="btn-x" id="followXBtn">
          <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M18.9 2H22l-7.6 8.7L23.3 22h-7.2l-5.6-7.3L4 22H1l8.1-9.3L0.9 2h7.4l5 6.7L18.9 2Zm-1.3 18h2L6.5 4H4.4l13.2 16Z"/></svg>
          Follow on X
        </a>
        <button class="btn-submit" id="continueAfterFollow" style="margin-top:16px; background:transparent; color:var(--ink); border:1px solid var(--ink);">I've followed — Continue</button>
      </div>

      <form id="wlForm" style="display:none;">
        <div class="field" id="fieldX">
          <label for="xUsername">X Username</label>
          <input type="text" id="xUsername" placeholder="@username" autocomplete="off">
          <div class="err">Enter a valid X username.</div>
        </div>
        <div class="field" id="fieldWallet">
          <label for="walletAddress">Wallet Address</label>
          <input type="text" id="walletAddress" placeholder="0x..." autocomplete="off">
          <div class="hint">Double-check this address — it locks after submission.</div>
          <div class="err">Enter a valid wallet address.</div>
        </div>
        <button type="submit" class="btn-submit" id="submitWlBtn">Submit WL</button>
        <div class="form-msg" id="wlMsg"></div>
      </form>

      <div id="wlClosedBlock" style="display:none; text-align:center; padding:30px 0;">
        <h3 style="font-size:22px;">Waitlist Closed</h3>
        <p style="margin-top:10px;">Submissions are no longer being accepted. Check back for eligibility results.</p>
      </div>
    </div>
  </div>
</section>

<!-- ================= COLLECTION ================= -->
<section id="collection">
  <div class="wrap">
    <div class="section-head">
      <span class="kicker">THE COLLECTION</span>
      <h2>3,333 pieces.<br>One collection.</h2>
      <p>Total supply 3,333 · Mint date TBA · Network Arc · Minting on OpenSea</p>
    </div>
    <div class="gallery" id="gallery"></div>
  </div>
</section>

<!-- ================= ARCHIVE ================= -->
<section id="archive">
  <div class="wrap">
    <div class="section-head">
      <span class="kicker">THE ARCHIVE</span>
      <h2>Reveal states</h2>
      <p>Artwork is revealed in stages as the admin team approves each phase.</p>
    </div>
    <div class="archive-grid" id="archiveGrid"></div>
  </div>
</section>

<!-- ================= WHY 3333 / ARC ================= -->
<section id="why">
  <div class="wrap split">
    <div>
      <span class="why-mark">3333</span>
    </div>
    <div>
      <span class="kicker" style="color:var(--gold); font-size:13px; letter-spacing:0.12em; font-weight:600;">WHY 3333?</span>
      <h2 style="margin-top:12px; font-size:clamp(26px,3.4vw,36px);">The story is still being written.</h2>
      <p style="margin-top:16px; font-size:16px;">We're not in the habit of inventing meaning where none exists yet. When there's a genuine reason behind the number, it will be shared here — in full, and without embellishment.</p>
    </div>
  </div>
</section>

<section id="arc">
  <div class="wrap split">
    <div>
      <span class="kicker" style="color:var(--gold); font-size:13px; letter-spacing:0.12em; font-weight:600;">NETWORK</span>
      <h2 style="margin-top:12px;">Built for the<br>Arc era.</h2>
      <ul class="arc-points">
        <li><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M8 12l3 3 5-6"/></svg>The collection is positioned on the Arc network, with the mint itself taking place on OpenSea.</li>
        <li><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M8 12l3 3 5-6"/></svg>No wallet connection or on-site minting — everything is handled through the official OpenSea collection when it goes live.</li>
        <li><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><path d="M8 12l3 3 5-6"/></svg>Further technical detail will be shared as the mint date is confirmed.</li>
      </ul>
    </div>
    <div class="hero-visual" style="height:360px;">
      <div class="orb-stage">
        <div class="orbit-ring" style="width:280px;height:280px; animation: spin-slow 26s linear infinite;"></div>
        <div class="orb-core" style="width:170px;height:170px; animation-duration:8s;"><span class="serif" style="font-size:15px; letter-spacing:0.06em; color:var(--olive);">ARC</span></div>
      </div>
    </div>
  </div>
</section>

<!-- ================= LATEST UPDATES ================= -->
<section id="updates">
  <div class="wrap">
    <div class="section-head">
      <span class="kicker">LATEST</span>
      <h2>Updates</h2>
    </div>
    <div class="updates-list" id="updatesList"></div>
  </div>
</section>

<!-- ================= ELIGIBILITY ================= -->
<section id="eligibility">
  <div class="wrap">
    <div class="section-head" style="margin:0 auto 46px; text-align:center;">
      <span class="kicker">WL STATUS</span>
      <h2>Check your WL status</h2>
    </div>
    <div class="elig-card" id="eligCard">
      <div id="eligUnavailable">
        <p>Eligibility results open once the waitlist closes and the team finalizes the list. Check back soon.</p>
      </div>
      <form id="eligForm" style="display:none;">
        <div class="field" style="text-align:left;">
          <label for="eligUsername">X Username</label>
          <input type="text" id="eligUsername" placeholder="@username">
        </div>
        <button type="submit" class="btn-submit" id="eligBtn">Check Status</button>
      </form>
      <div class="elig-result" id="eligResult">
        <p id="eligResultText"></p>
        <div id="eligBadgeWrap"></div>
        <div id="accessCardWrap"></div>
      </div>
    </div>
  </div>
</section>

<!-- ================= FAQ ================= -->
<section id="faq">
  <div class="wrap">
    <div class="section-head">
      <span class="kicker">FAQ</span>
      <h2>Common questions</h2>
    </div>
    <div id="faqList"></div>
  </div>
</section>

<!-- ================= LINKS ================= -->
<section id="links">
  <div class="wrap">
    <div class="section-head">
      <span class="kicker">OFFICIAL LINKS</span>
      <h2>Verify before you trust</h2>
    </div>
    <div class="link-cards">
      <a class="link-card" id="linkX" href="https://x.com/ArcCollection" target="_blank" rel="noopener">
        <span class="lbl">OFFICIAL</span><span class="name">X / Twitter</span>
      </a>
      <a class="link-card" id="linkOS" href="#" target="_blank" rel="noopener">
        <span class="lbl">MINT DESTINATION</span><span class="name">OpenSea</span>
      </a>
      <a class="link-card" id="linkArc" href="#" target="_blank" rel="noopener">
        <span class="lbl">NETWORK</span><span class="name">Arc</span>
      </a>
    </div>
    <div class="warn-box">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" style="flex-shrink:0;"><path d="M12 9v4M12 17h.01M10.3 3.9 2.5 18a2 2 0 0 0 1.7 3h15.6a2 2 0 0 0 1.7-3L13.7 3.9a2 2 0 0 0-3.4 0Z"/></svg>
      <div>These are the only official links for this project. Beware of impersonators. We will never ask for your seed phrase, private key, or wallet password.</div>
    </div>
  </div>
</section>

<footer>
  <div class="wrap foot-grid">
    <a href="#hero" class="brand"><img src="data:image/jpeg;base64,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sWLFixQnxQ215v6tjGaE+RKxYsWLFixYsWLFixYsWLFixPuM5ScvMebHmsmVExkde69xKBJRI1a6IZLY/RH8CTsWIIIIIIILly5cuXLlypoWwl3TbfyN5JGyRjRO8d5ZcuXLly5cuXLly5cuXLly5cuXLk5DPlJfzF8R27n5fHpIkHkGy2Lly5cuXLly5cuXLly5fpl+9bEROJnE9UwB9DJlx4S9m+hXLly5cuXLly5cuXLly5cuXLly5cuSKEVzMmlLeqzvp7DkXLly5cuXLlixYsWLFixYsWLDRBcuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFy5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5cuXLly5YsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLEEFixYsWLFixYsWLEEFixBBYsWLFixYsWLFixBBYsWLFixYsWLFixcuWLFi34kAAAAAALFixYuXLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFixYsWLFj//Z" alt="ARC logo"><span>ARC / 3333</span></a>
    <p class="foot-security">We will never ask for your seed phrase, private key, wallet password, or X password. No wallet connect. No on-site minting — the mint happens on OpenSea.</p>
  </div>
</footer>

<button id="admin-toggle">Admin</button>

<div id="admin-overlay">
  <div id="admin-panel">
    <div class="admin-row">
      <h3 class="serif" style="font-size:22px;">Admin Panel</h3>
      <button class="close-admin" id="closeAdmin">&times;</button>
    </div>

    <div id="adminLogin">
      <div class="field"><label>Admin Passcode</label><input type="password" id="adminPass" class="admin-input" placeholder="Enter passcode"></div>
      <button class="btn-submit" id="adminLoginBtn" style="max-width:220px;">Log in</button>
      <div class="disclaimer-note">Demo passcode: <b>ARC3333</b>. This is a client-side demo gate for previewing the admin workflow — a production deployment needs a real authenticated backend.</div>
    </div>

    <div id="adminBody" style="display:none;">
      <div class="admin-section">
        <h4>Live status</h4>
        <div class="admin-grid" id="statusPills"></div>
      </div>
      <div class="admin-section">
        <h4>Mint date & links</h4>
        <div class="admin-grid" style="grid-template-columns:1fr 1fr;">
          <input class="admin-input" id="cfgMintDate" placeholder="Mint date (e.g. TBA)">
          <input class="admin-input" id="cfgWlDeadline" placeholder="WL deadline (e.g. TBA)">
          <input class="admin-input" id="cfgOpensea" placeholder="OpenSea URL">
          <input class="admin-input" id="cfgXlink" placeholder="X URL">
          <input class="admin-input" id="cfgArclink" placeholder="Arc reference URL">
          <input class="admin-input" id="cfgWlCapacity" placeholder="WL capacity (number, optional)">
        </div>
        <button class="pill-btn" id="saveCfgBtn" style="margin-top:12px;">Save configuration</button>
      </div>
      <div class="admin-section">
        <h4>Post an update</h4>
        <div style="display:flex; gap:10px;">
          <input class="admin-input" id="cfgUpdateText" placeholder="e.g. WL has closed.">
          <button class="pill-btn" id="addUpdateBtn" style="white-space:nowrap;">Post</button>
        </div>
      </div>
      <div class="admin-section">
        <h4>Waitlist submissions (<span id="submissionCount">0</span>)</h4>
        <div style="overflow-x:auto;">
          <table class="admin-table">
            <thead><tr><th>X Username</th><th>Wallet</th><th>Status</th><th>Submitted</th><th>Actions</th></tr></thead>
            <tbody id="submissionsBody"></tbody>
          </table>
        </div>
        <div class="disclaimer-note">Wallet addresses are shown here only. They are never rendered in public sections, URLs, or client-visible lists outside this gated panel.</div>
      </div>
    </div>
  </div>
</div>

<script>
(function(){

/* ================= UTIL ================= */
const $ = (s,r=document)=>r.querySelector(s);
const $$ = (s,r=document)=>Array.from(r.querySelectorAll(s));
const reducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

function normUsername(u){
  return (u||'').trim().replace(/^@/,'').toLowerCase();
}
function normWallet(w){
  return (w||'').trim().toLowerCase();
}
function isValidUsername(u){
  return /^[a-zA-Z0-9_]{1,15}$/.test((u||'').trim().replace(/^@/,''));
}
function isValidWallet(w){
  const t=(w||'').trim();
  return /^0x[a-fA-F0-9]{40}$/.test(t) || (t.length>=26 && t.length<=64 && /^[a-zA-Z0-9]+$/.test(t));
}

/* ================= STORAGE LAYER (shared, demo backend) ================= */
const DEFAULT_CONFIG = {
  liveStatus: 'WAITLIST OPEN',
  mintDate: 'TBA',
  wlDeadline: 'TBA',
  openseaUrl: '',
  xUrl: 'https://x.com/ArcCollection',
  arcUrl: 'https://arc.network',
  wlCapacity: null,
  updates: [
    {text:'Waitlist is now open.', at: Date.now()}
  ]
};

async function getConfig(){
  try{
    const r = await window.storage.get('site-config', true);
    return r ? JSON.parse(r.value) : DEFAULT_CONFIG;
  }catch(e){ return DEFAULT_CONFIG; }
}
async function setConfig(cfg){
  await window.storage.set('site-config', JSON.stringify(cfg), true);
}
async function listSubmissions(){
  try{
    const r = await window.storage.list('wl:', true);
    if(!r || !r.keys) return [];
    const out = [];
    for(const k of r.keys){
      try{
        const v = await window.storage.get(k, true);
        if(v) out.push(JSON.parse(v.value));
      }catch(e){}
    }
    return out.sort((a,b)=>b.createdAt-a.createdAt);
  }catch(e){ return []; }
}
async function getSubmission(usernameNorm){
  try{
    const r = await window.storage.get('wl:'+usernameNorm, true);
    return r ? JSON.parse(r.value) : null;
  }catch(e){ return null; }
}
async function saveSubmission(entry){
  await window.storage.set('wl:'+entry.xUsernameNorm, JSON.stringify(entry), true);
}

/* ================= BUBBLE / DOODLE GENERATION ================= */
function rand(min,max){ return Math.random()*(max-min)+min; }

function buildBubbles(container, count, opts={}){
  const frag = document.createDocumentFragment();
  for(let i=0;i<count;i++){
    const b = document.createElement('div');
    const size = rand(opts.min||16, opts.max||70);
    b.className = 'bubble' + (Math.random()>0.6?' solid':'');
    b.style.width = size+'px';
    b.style.height = size+'px';
    b.style.left = rand(0,94)+'%';
    b.style.top = rand(0,90)+'%';
    b.style.setProperty('--dx', rand(-24,24)+'px');
    b.style.setProperty('--dy', rand(-30,30)+'px');
    b.style.opacity = rand(0.35,0.9);
    if(!reducedMotion){
      b.style.animation = `drift ${rand(6,13)}s ease-in-out infinite`;
      b.style.animationDelay = rand(0,4)+'s';
    }
    b.dataset.depth = rand(6,26).toFixed(1);
    frag.appendChild(b);
  }
  container.appendChild(frag);
}

function doodleSVG(kind){
  const c = 'currentColor';
  switch(kind){
    case 'circle': return `<svg width="40" height="40" viewBox="0 0 40 40"><circle cx="20" cy="20" r="14" fill="none" stroke="${c}" stroke-width="1.4"/></svg>`;
    case 'loop': return `<svg width="46" height="30" viewBox="0 0 46 30"><path d="M2 22C10 4 20 4 23 15C26 26 36 26 44 8" fill="none" stroke="${c}" stroke-width="1.4" stroke-linecap="round"/></svg>`;
    case 'arrow': return `<svg width="40" height="40" viewBox="0 0 40 40"><path d="M6 34 L34 6 M18 6 H34 V22" fill="none" stroke="${c}" stroke-width="1.4" stroke-linecap="round" stroke-linejoin="round"/></svg>`;
    case 'sparkle': return `<svg width="30" height="30" viewBox="0 0 30 30"><path d="M15 2 L18 13 L28 15 L18 17 L15 28 L12 17 L2 15 L12 13 Z" fill="${c}"/></svg>`;
    case 'wave': return `<svg width="52" height="20" viewBox="0 0 52 20"><path d="M2 10c6-10 12-10 18 0s12 10 18 0 8-8 12-2" fill="none" stroke="${c}" stroke-width="1.4" stroke-linecap="round"/></svg>`;
    case 'cross': return `<svg width="26" height="26" viewBox="0 0 26 26"><path d="M4 4 L22 22 M22 4 L4 22" stroke="${c}" stroke-width="1.4" stroke-linecap="round"/></svg>`;
    case 'orbit': return `<svg width="44" height="44" viewBox="0 0 44 44"><ellipse cx="22" cy="22" rx="20" ry="9" fill="none" stroke="${c}" stroke-width="1.2"/><circle cx="40" cy="22" r="2.4" fill="${c}"/></svg>`;
    default: return `<svg width="30" height="30" viewBox="0 0 30 30"><circle cx="15" cy="15" r="3" fill="${c}"/></svg>`;
  }
}
function buildDoodles(container, count){
  const kinds = ['circle','loop','arrow','sparkle','wave','cross','orbit'];
  const frag = document.createDocumentFragment();
  for(let i=0;i<count;i++){
    const d = document.createElement('div');
    d.className='doodle';
    d.innerHTML = doodleSVG(kinds[Math.floor(rand(0,kinds.length))]);
    d.style.left = rand(2,92)+'%';
    d.style.top = rand(4,92)+'%';
    d.style.transform = `rotate(${rand(-20,20)}deg)`;
    if(!reducedMotion){
      d.style.animation = `drift ${rand(9,16)}s ease-in-out infinite`;
      d.style.animationDelay = rand(0,5)+'s';
    }
    frag.appendChild(d);
  }
  container.appendChild(frag);
}

buildBubbles($('#hero-bubbles'), 12, {min:14,max:60});
buildDoodles($('#hero-bubbles'), 7);
buildBubbles($('#global-bubbles'), 6, {min:10,max:34});

/* cursor-reactive parallax on hero bubbles + orb */
const heroSection = $('#hero');
if(!reducedMotion){
  heroSection.addEventListener('mousemove', (e)=>{
    const r = heroSection.getBoundingClientRect();
    const px = (e.clientX - r.left)/r.width - 0.5;
    const py = (e.clientY - r.top)/r.height - 0.5;
    $$('#hero-bubbles .bubble').forEach(b=>{
      const depth = parseFloat(b.dataset.depth||10);
      b.style.marginLeft = (px*depth)+'px';
      b.style.marginTop = (py*depth)+'px';
    });
    $('#orbStage').style.transform = `rotateY(${px*10}deg) rotateX(${-py*10}deg)`;
  });
  heroSection.addEventListener('mouseleave', ()=>{
    $('#orbStage').style.transform = '';
  });
}

/* ================= NAV ================= */
window.addEventListener('scroll', ()=>{
  $('#nav').classList.toggle('scrolled', window.scrollY > 30);
});
$('#navToggle').addEventListener('click', ()=>{
  $('#navLinks').classList.toggle('open');
});
$$('#navLinks a').forEach(a=>a.addEventListener('click',()=>$('#navLinks').classList.remove('open')));

/* ================= GALLERY (placeholder generative art tiles) ================= */
const tileGradients = [
  ['#FAF9F1','#C8D2B5'], ['#8A9578','#F4F5EA'], ['#E5EBD7','#5E6850'],
  ['#C8D2B5','#A9884F'], ['#5E6850','#FAF9F1'], ['#F4F5EA','#8A9578'],
  ['#A9884F','#E5EBD7'], ['#8A9578','#20251D']
];
function makeTileArt(idx){
  const [c1,c2] = tileGradients[idx % tileGradients.length];
  const shapes = ['circle','loop','sparkle','orbit'];
  const shape = shapes[idx % shapes.length];
  return `
    <div class="tile-art" style="background:linear-gradient(${135+idx*17}deg, ${c1}, ${c2});
      display:flex; align-items:center; justify-content:center; color:${idx%2?'#FAF9F1':'#20251D'}; opacity:0.9;">
      ${doodleSVG(shape).replace('width="40"','width="70"').replace('height="40"','height="70"').replace('width="46"','width="76"').replace('width="30"','width="60"').replace('height="30"','height="60"').replace('width="44"','width="72"').replace('height="44"','height="72"')}
    </div>`;
}
const galleryEl = $('#gallery');
for(let i=0;i<8;i++){
  const t = document.createElement('div');
  t.className='tile';
  t.innerHTML = makeTileArt(i) + `<div class="tile-tag">#${(i+1).toString().padStart(4,'0')}</div>`;
  galleryEl.appendChild(t);
}

/* ================= ARCHIVE ================= */
const archiveStates = ['revealed','revealed','blurred','silhouette','soon','soon'];
const archiveEl = $('#archiveGrid');
archiveStates.forEach((st,i)=>{
  const t = document.createElement('div');
  t.className = 'archive-tile ' + (st==='revealed'?'':st);
  if(st==='soon'){
    t.innerHTML = `<span>COMING SOON</span>`;
  }else{
    t.innerHTML = makeTileArt(i+2) + `<div class="archive-state">${st.toUpperCase()}</div>`;
  }
  archiveEl.appendChild(t);
});

/* ================= FAQ ================= */
const faqData = [
  ['What is the collection?', 'A premium 3,333-piece digital collectible collection, minting on OpenSea.'],
  ['Why 3333?', 'If there is a genuine story behind the number, it will be shared here once confirmed — we will not invent one.'],
  ['What is the total supply?', '3,333 pieces, in total.'],
  ['When is the mint?', 'The mint date is currently TBA and will be announced through official channels.'],
  ['Which blockchain is used?', 'The collection is positioned on the Arc network.'],
  ['Where will the NFT mint?', 'Minting happens on OpenSea. There is no on-site minting.'],
  ['How does the WL work?', 'Follow the official X account, then submit your X username and wallet address while the waitlist is open.'],
  ['What do I need to submit for WL?', 'Your X username and a single wallet address.'],
  ['When will eligibility be announced?', 'After the waitlist closes and the team finalizes results.'],
  ['How do I check my WL status?', 'Use the eligibility checker once it is activated, with your X username.'],
  ['Is wallet connect required?', 'No. Wallet addresses are entered manually — there is no wallet connection or signature request.'],
  ['Where is the official OpenSea collection?', 'The official link will appear in the Links section once configured.'],
  ['What are the official project links?', 'See the Official Links section for verified X, OpenSea, and Arc references.'],
];
const faqEl = $('#faqList');
faqData.forEach(([q,a],i)=>{
  const item = document.createElement('div');
  item.className='faq-item';
  item.innerHTML = `<button class="faq-q" aria-expanded="false"><span>${q}</span><span class="faq-icon"></span></button>
    <div class="faq-a"><p>${a}</p></div>`;
  faqEl.appendChild(item);
  const btn = item.querySelector('.faq-q');
  const ans = item.querySelector('.faq-a');
  btn.addEventListener('click', ()=>{
    const open = item.classList.toggle('open');
    btn.setAttribute('aria-expanded', open?'true':'false');
    ans.style.maxHeight = open ? ans.scrollHeight+'px' : '0px';
  });
});

/* ================= TILT ON SCROLL (gallery) ================= */
if(!reducedMotion && 'IntersectionObserver' in window){
  const io = new IntersectionObserver((entries)=>{
    entries.forEach(en=>{
      if(en.isIntersecting){ en.target.style.opacity='1'; en.target.style.transform+=''; }
    });
  }, {threshold:0.15});
}

/* ================= APP STATE / MAIN FLOW ================= */
let CONFIG = null;
let followed = false;

function applyLiveStatus(cfg){
  $('#statusText').textContent = cfg.liveStatus;
  $('#mintDateStat').textContent = cfg.mintDate || 'TBA';
  $('#linkOS').href = cfg.openseaUrl || '#';
  $('#linkX').href = cfg.xUrl || '#';
  $('#linkArc').href = cfg.arcUrl || '#';
  $('#followXBtn').href = cfg.xUrl || '#';

  const wlOpen = cfg.liveStatus === 'WAITLIST OPEN';
  const wlClosedShown = cfg.liveStatus !== 'WAITLIST OPEN';
  $('#followBlock').style.display = wlOpen && !followed ? 'block' : 'none';
  $('#wlForm').style.display = wlOpen && followed ? 'block' : 'none';
  $('#wlClosedBlock').style.display = wlOpen ? 'none' : 'block';

  const eligOn = cfg.liveStatus === 'CHECK WL' || cfg.liveStatus === 'MINT SOON' || cfg.liveStatus === 'MINT LIVE';
  $('#eligUnavailable').style.display = eligOn ? 'none' : 'block';
  $('#eligForm').style.display = eligOn ? 'block' : 'none';

  // updates
  const updEl = $('#updatesList');
  updEl.innerHTML = '';
  (cfg.updates||[]).slice().reverse().forEach(u=>{
    const row = document.createElement('div');
    row.className='update-row';
    row.innerHTML = `<time>${new Date(u.at).toLocaleDateString(undefined,{month:'short',day:'numeric',year:'numeric'})}</time><span>${u.text}</span>`;
    updEl.appendChild(row);
  });
}

async function refreshProgress(){
  if(!CONFIG || !CONFIG.wlCapacity){ $('#progressWrap').style.display='none'; return; }
  const subs = await listSubmissions();
  const n = subs.length;
  const cap = CONFIG.wlCapacity;
  $('#progressWrap').style.display='block';
  $('#progressFill').style.width = Math.min(100,(n/cap)*100)+'%';
  $('#progressLabel').textContent = `WL ACCESS — ${n.toLocaleString()} / ${cap.toLocaleString()}`;
}

async function boot(){
  CONFIG = await getConfig();
  applyLiveStatus(CONFIG);
  await refreshProgress();
  await renderAdminIfLoggedIn();
}
boot();

/* follow -> continue */
$('#continueAfterFollow').addEventListener('click', ()=>{
  followed = true;
  $('#stepList li[data-step="1"]').classList.add('done');
  applyLiveStatus(CONFIG);
});

/* WL form validation + submit */
const xInput = $('#xUsername');
const walletInput = $('#walletAddress');

xInput.addEventListener('input', ()=>{
  $('#fieldX').classList.toggle('invalid', xInput.value.length>0 && !isValidUsername(xInput.value));
  if(isValidUsername(xInput.value)) $('#stepList li[data-step="2"]').classList.add('done');
});
walletInput.addEventListener('input', ()=>{
  $('#fieldWallet').classList.toggle('invalid', walletInput.value.length>0 && !isValidWallet(walletInput.value));
  if(isValidWallet(walletInput.value)) $('#stepList li[data-step="3"]').classList.add('done');
});

$('#wlForm').addEventListener('submit', async (e)=>{
  e.preventDefault();
  const msg = $('#wlMsg');
  msg.className = 'form-msg'; msg.textContent='';
  const uRaw = xInput.value, wRaw = walletInput.value;

  if(!isValidUsername(uRaw)){
    $('#fieldX').classList.add('invalid'); return;
  }
  if(!isValidWallet(wRaw)){
    $('#fieldWallet').classList.add('invalid'); return;
  }

  const btn = $('#submitWlBtn');
  btn.disabled = true; btn.innerHTML = '<span class="spin"></span> Submitting…';

  try{
    const uNorm = normUsername(uRaw);
    const wNorm = normWallet(wRaw);

    const existingUser = await getSubmission(uNorm);
    if(existingUser){
      msg.classList.add('show','error');
      msg.textContent = 'This X username has already joined the waitlist.';
      return;
    }
    const all = await listSubmissions();
    if(all.some(s=>s.walletNorm === wNorm)){
      msg.classList.add('show','error');
      msg.textContent = 'This wallet has already been submitted for another waitlist entry.';
      return;
    }

    const entry = {
      xUsernameNorm: uNorm,
      xUsernameDisplay: '@'+uRaw.trim().replace(/^@/,''),
      xFollowStatus: true,
      walletAddress: wRaw.trim(),
      walletNorm: wNorm,
      walletLocked: true,
      wlStatus: 'PENDING',
      createdAt: Date.now(),
      walletSubmittedAt: Date.now()
    };
    await saveSubmission(entry);

    msg.classList.add('show','success');
    msg.textContent = "You're on the list. Your X username and wallet have been securely recorded.";
    $('#wlForm').reset();
    $('#wlForm').style.display='none';
    await refreshProgress();
    await renderAdminIfLoggedIn();
  }catch(err){
    msg.classList.add('show','error');
    msg.textContent = 'Something went wrong saving your entry. Please try again.';
  }finally{
    btn.disabled = false; btn.textContent = 'Submit WL';
  }
});

/* ================= ELIGIBILITY CHECK ================= */
$('#eligForm').addEventListener('submit', async (e)=>{
  e.preventDefault();
  const btn = $('#eligBtn');
  btn.disabled = true; btn.innerHTML = '<span class="spin"></span> Checking…';
  const uNorm = normUsername($('#eligUsername').value);
  const entry = await getSubmission(uNorm);
  const resultWrap = $('#eligResult');
  const textEl = $('#eligResultText');
  const badgeWrap = $('#eligBadgeWrap');
  const cardWrap = $('#accessCardWrap');
  resultWrap.style.display='block';
  badgeWrap.innerHTML=''; cardWrap.innerHTML='';

  if(!entry){
    textEl.textContent = "We couldn't find that X username on the waitlist.";
  }else if(entry.wlStatus === 'GRANTED'){
    textEl.textContent = 'Congratulations — your status:';
    badgeWrap.innerHTML = `<div class="elig-badge granted">WL GRANTED</div>`;
    cardWrap.innerHTML = `
      <div class="access-card">
        <div class="ac-top"><img class="ac-logo" src="data:image/jpeg;base64,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
