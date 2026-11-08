# sky-shield-app
# this is simulation app build for understanding the concept of cybersecurity in drones-on-ground-handshake
 # file:///C:/Users/Gex/Desktop/app%20cyber/index.html

 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#0b0f19">
  <meta name="description" content="SkyShield is a client-side drone IoT blockchain security simulator.">
  <title>SkyShield — Drone IoT Blockchain Simulator</title>
  <style>
    :root {
      color-scheme: dark;
      --bg: #0b0f19;
      --panel: #111827;
      --panel-deep: #0c131f;
      --line: rgba(149, 176, 211, .14);
      --muted: #8291a9;
      --text: #e8f0fc;
      --cyan: #00e5ff;
      --green: #00e676;
      --red: #ff1744;
      --amber: #ffc400;
      --shadow: 0 18px 55px rgba(0, 0, 0, .28);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      min-height: 100vh;
      background:
        radial-gradient(ellipse at 16% -14%, rgba(0, 229, 255, .10), transparent 38%),
        radial-gradient(ellipse at 95% 8%, rgba(0, 230, 118, .055), transparent 30%),
        var(--bg);
      color: var(--text);
    }
    button, input, textarea { font: inherit; }
    button { cursor: pointer; }
    button:disabled { cursor: not-allowed; opacity: .48; transform: none !important; }
    button:focus-visible, input:focus-visible, textarea:focus-visible {
      outline: 2px solid var(--cyan);
      outline-offset: 3px;
    }
    .shell { width: min(1540px, 100%); margin: auto; padding: 26px 28px 44px; }
    .topbar { display: flex; justify-content: space-between; align-items: center; gap: 20px; margin-bottom: 23px; }
    .brand { display: flex; align-items: center; gap: 14px; min-width: 0; }
    .brand-mark {
      width: 46px; height: 46px; display: grid; place-items: center; border-radius: 14px;
      color: var(--cyan); border: 1px solid rgba(0,229,255,.34); background: rgba(0,229,255,.08);
      box-shadow: 0 0 24px rgba(0,229,255,.1); font-size: 21px;
    }
    h1 { font-size: clamp(19px, 2.2vw, 27px); margin: 0; letter-spacing: -.04em; }
    .subtitle { color: var(--muted); font-size: 11px; margin-top: 5px; letter-spacing: .04em; }
    .top-meta { display: flex; align-items: center; gap: 9px; flex-wrap: wrap; justify-content: flex-end; }
    .chip, .live-pill {
      border: 1px solid var(--line); color: #b8c5d8; border-radius: 999px;
      padding: 8px 11px; font: 9px ui-monospace, SFMono-Regular, Menlo, monospace;
      letter-spacing: .08em; background: rgba(255,255,255,.025);
    }
    .live-pill { color: var(--green); border-color: rgba(0,230,118,.28); display: flex; gap: 8px; align-items: center; }
    .live-dot { width: 7px; height: 7px; background: var(--green); border-radius: 50%; box-shadow: 0 0 12px var(--green); animation: pulse 1.6s infinite; }
    .demo-badge { color: var(--amber); border-color: rgba(255,196,0,.24); }

    .overview { display: grid; grid-template-columns: minmax(255px, .82fr) minmax(390px, 1.3fr) minmax(310px, 1fr); gap: 16px; align-items: start; }
    .panel {
      background: linear-gradient(145deg, rgba(18,26,41,.96), rgba(13,19,31,.97));
      border: 1px solid var(--line); border-radius: 17px; box-shadow: var(--shadow); overflow: hidden; min-width: 0;
    }
    .panel-head { padding: 18px 18px 14px; border-bottom: 1px solid var(--line); display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; }
    .eyebrow { color: var(--cyan); font: 9px ui-monospace, SFMono-Regular, Menlo, monospace; letter-spacing: .14em; text-transform: uppercase; }
    .panel h2 { font-size: 14px; margin: 6px 0 0; letter-spacing: -.02em; }
    .panel-body { padding: 17px 18px 19px; }
    .section-note { color: var(--muted); font-size: 10px; line-height: 1.6; margin: 7px 0 0; }
    .small-stat { font: 9px ui-monospace, monospace; color: var(--muted); white-space: nowrap; }

    .fleet-summary { display: flex; gap: 8px; margin-bottom: 14px; }
    .mini-stat { flex: 1; border: 1px solid var(--line); background: rgba(255,255,255,.025); padding: 10px; border-radius: 11px; }
    .mini-stat strong { display: block; font: 17px ui-monospace, monospace; margin-bottom: 3px; }
    .mini-stat span { color: var(--muted); text-transform: uppercase; font-size: 8px; letter-spacing: .1em; }
    .drone-list { display: grid; gap: 8px; }
    .drone-card { border: 1px solid var(--line); padding: 10px; border-radius: 12px; background: rgba(255,255,255,.018); transition: .25s; }
    .drone-card.compromised { border-color: rgba(255,23,68,.55); background: rgba(255,23,68,.07); box-shadow: 0 0 22px rgba(255,23,68,.08); }
    .drone-top { display: flex; justify-content: space-between; align-items: center; gap: 8px; }
    .drone-name { display: flex; align-items: center; gap: 8px; font-size: 11px; font-weight: 650; }
    .drone-icon { font-size: 15px; color: var(--cyan); }
    .status { font: 8px ui-monospace, monospace; letter-spacing: .06em; color: var(--green); text-align: right; }
    .status.bad { color: var(--red); }
    .drone-meta { color: var(--muted); font: 8px ui-monospace, monospace; margin-top: 7px; line-height: 1.7; overflow-wrap: anywhere; }
    .key { color: #b4c6db; }
    .fleet-footer { display: flex; justify-content: space-between; gap: 10px; padding-top: 12px; margin-top: 12px; border-top: 1px solid var(--line); color: var(--muted); font: 8px ui-monospace, monospace; }

    .ledger-topline { display: flex; align-items: center; justify-content: space-between; gap: 10px; margin-bottom: 13px; }
    .ledger-topline strong { font: 10px ui-monospace, monospace; color: var(--green); }
    .consensus { font: 8px ui-monospace, monospace; color: var(--amber); }
    .peer-row { display: flex; gap: 7px; margin-bottom: 16px; }
    .peer { flex: 1; text-align: center; padding: 8px 4px; border: 1px solid var(--line); border-radius: 9px; color: var(--muted); font: 8px ui-monospace, monospace; transition: .25s; }
    .peer.active { color: var(--amber); border-color: rgba(255,196,0,.55); box-shadow: 0 0 14px rgba(255,196,0,.12); }
    .peer.done { color: var(--green); border-color: rgba(0,230,118,.35); }
    .chain { display: flex; gap: 9px; align-items: stretch; overflow-x: auto; padding: 2px 1px 10px; scrollbar-color: #34445a transparent; }
    .block {
      min-width: 136px; flex: 1; border: 1px solid rgba(0,230,118,.25); border-radius: 11px;
      background: rgba(0,230,118,.055); padding: 11px; position: relative; transition: .35s;
    }
    .block:not(:last-child)::after { content: ""; height: 1px; width: 10px; background: rgba(0,230,118,.42); position: absolute; right: -10px; top: 50%; z-index: 2; }
    .block.proposing { border-color: rgba(255,196,0,.8); background: rgba(255,196,0,.13); box-shadow: 0 0 25px rgba(255,196,0,.13); animation: blockPulse .8s infinite alternate; }
    .block h3 { font: 9px ui-monospace, monospace; margin: 0 0 8px; color: var(--green); }
    .block.proposing h3 { color: var(--amber); }
    .block p { color: var(--muted); font: 8px/1.55 ui-monospace, monospace; margin: 4px 0; overflow-wrap: anywhere; }
    .block .hash { color: #a8bdd2; }
    .empty-chain { padding: 18px; text-align: center; color: var(--muted); font-size: 10px; border: 1px dashed var(--line); border-radius: 10px; width: 100%; }
    .ledger-caption { display: flex; justify-content: space-between; color: var(--muted); font: 8px ui-monospace, monospace; margin-top: 2px; }
    .chain-note { display: flex; align-items: center; gap: 7px; margin-top: 9px; color: var(--muted); font: 8px ui-monospace, monospace; }
    .chain-note::before { content: ""; width: 6px; height: 6px; border-radius: 50%; background: var(--green); box-shadow: 0 0 9px var(--green); }

    .form-label { display: block; color: #bfcbda; font-size: 9px; letter-spacing: .07em; margin: 13px 0 7px; text-transform: uppercase; }
    input, textarea {
      width: 100%; border: 1px solid var(--line); background: #0a101b; color: var(--text);
      border-radius: 9px; padding: 10px 11px; outline: none; transition: .2s; font-size: 10px;
    }
    input:focus, textarea:focus { border-color: rgba(0,229,255,.6); box-shadow: 0 0 0 3px rgba(0,229,255,.08); }
    textarea { min-height: 70px; resize: vertical; font-family: ui-monospace, monospace; line-height: 1.5; }
    .btn {
      border: 1px solid rgba(0,229,255,.35); border-radius: 9px; background: rgba(0,229,255,.10);
      color: var(--cyan); padding: 10px 13px; font-size: 9px; font-weight: 700; letter-spacing: .04em;
      transition: transform .18s, box-shadow .18s, background .18s; display: inline-flex; align-items: center; justify-content: center; gap: 8px;
    }
    .btn:hover { transform: translateY(-1px); background: rgba(0,229,255,.16); box-shadow: 0 0 18px rgba(0,229,255,.13); }
    .btn.primary { width: 100%; margin-top: 12px; }
    .btn.green { color: var(--green); border-color: rgba(0,230,118,.38); background: rgba(0,230,118,.08); }
    .btn.red { color: #fff; border-color: rgba(255,23,68,.5); background: linear-gradient(135deg, rgba(255,23,68,.9), rgba(196,0,48,.9)); }
    .btn.red:hover { box-shadow: 0 0 22px rgba(255,23,68,.3); }
    .form-feedback { color: var(--muted); min-height: 15px; margin-top: 8px; font: 8px ui-monospace, monospace; }
    .simulator { margin-top: 16px; }
    .sim-actions { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 14px; }
    .sim-actions .btn { min-height: 46px; line-height: 1.35; }
    .sim-result { margin-top: 12px; padding: 12px; border-radius: 10px; border: 1px solid var(--line); background: rgba(255,255,255,.025); min-height: 79px; transition: .2s; }
    .sim-result.safe { border-color: rgba(0,230,118,.32); background: rgba(0,230,118,.045); }
    .sim-result.danger { border-color: rgba(255,23,68,.48); background: rgba(255,23,68,.065); }
    .result-title { font-size: 10px; font-weight: 750; margin-bottom: 6px; }
    .result-detail { color: var(--muted); font: 8px/1.7 ui-monospace, monospace; overflow-wrap: anywhere; }
    .hash-compare { display: grid; gap: 6px; margin-top: 7px; }
    .hash-line { padding: 7px; border-radius: 6px; background: rgba(0,0,0,.2); color: #b8c7da; overflow-wrap: anywhere; }
    .alert-banner { display: none; margin-top: 10px; padding: 11px; border: 1px solid rgba(255,23,68,.6); border-radius: 9px; color: #ff8b9e; background: rgba(255,23,68,.09); font: 9px ui-monospace, monospace; animation: alertFlash .75s infinite alternate; }
    .alert-banner.show { display: block; }
    .reset-row { display: flex; justify-content: space-between; align-items: center; gap: 8px; margin-top: 9px; }
    .reset-btn { border: 0; background: transparent; padding: 5px 0; color: var(--muted); font: 8px ui-monospace, monospace; text-decoration: underline; text-underline-offset: 3px; }
    .reset-btn:hover { color: var(--cyan); }

    .tabs { display: flex; gap: 8px; border-bottom: 1px solid var(--line); margin: 23px 0 15px; }
    .tab {
      border: 0; background: transparent; color: var(--muted); padding: 11px 15px;
      border-bottom: 2px solid transparent; font-size: 10px; font-weight: 650; transition: .2s;
    }
    .tab:hover { color: var(--text); }
    .tab.active { color: var(--cyan); border-color: var(--cyan); }
    .game-panel { display: none; }
    .game-panel.active { display: block; }
    .game-layout { display: grid; grid-template-columns: minmax(0, 1.6fr) minmax(265px, .75fr); gap: 16px; }
    .arena-wrap { position: relative; }
    .arena {
      min-height: 335px; position: relative; overflow: hidden; border: 1px solid var(--line); border-radius: 14px;
      background-color: #0a111c;
      background-image: linear-gradient(rgba(0,229,255,.045) 1px, transparent 1px), linear-gradient(90deg, rgba(0,229,255,.045) 1px, transparent 1px);
      background-size: 28px 28px; isolation: isolate;
    }
    .arena::before { content: ""; position: absolute; inset: 0; pointer-events: none; background: radial-gradient(ellipse at center, transparent 15%, rgba(10,17,28,.32) 100%); }
    .arena-hud { position: absolute; z-index: 2; inset: 13px 14px auto; display: flex; justify-content: space-between; color: #a9bad0; font: 8px ui-monospace, monospace; letter-spacing: .08em; }
    .arena-center { position: absolute; width: 136px; height: 136px; border-radius: 50%; border: 1px solid rgba(0,229,255,.16); left: 50%; top: 52%; transform: translate(-50%,-50%); display: grid; place-items: center; }
    .arena-center::before, .arena-center::after { content: ""; position: absolute; border: 1px solid rgba(0,229,255,.11); border-radius: 50%; inset: 15px; }
    .arena-center::after { inset: -18px; border-style: dashed; animation: orbit 25s linear infinite; }
    .rescue-zone { font: 8px ui-monospace, monospace; color: rgba(0,229,255,.68); text-align: center; z-index: 1; letter-spacing: .12em; }
    .rescue-zone b { display: block; font-size: 23px; font-weight: 400; margin-bottom: 4px; }
    .game-drone {
      position: absolute; z-index: 3; width: 32px; height: 32px; display: grid; place-items: center;
      border: 1px solid rgba(0,229,255,.3); border-radius: 10px; background: rgba(0,229,255,.1);
      color: var(--cyan); font-size: 14px; box-shadow: 0 0 14px rgba(0,229,255,.08); animation: hover 2.3s ease-in-out infinite;
      transition: left .65s ease, top .65s ease, opacity .3s;
    }
    .game-drone.candidate { border-color: rgba(255,196,0,.8); color: var(--amber); background: rgba(255,196,0,.12); box-shadow: 0 0 19px rgba(255,196,0,.23); animation: candidatePulse .65s infinite alternate; }
    .game-drone.candidate.rogue { color: var(--red); border-color: rgba(255,23,68,.8); background: rgba(255,23,68,.12); box-shadow: 0 0 20px rgba(255,23,68,.2); }
    .arena-toast { position: absolute; z-index: 4; left: 50%; top: 15%; transform: translateX(-50%); border: 1px solid var(--line); background: rgba(8,13,22,.92); padding: 9px 13px; border-radius: 9px; color: var(--text); font: 8px ui-monospace, monospace; opacity: 0; transition: opacity .25s; white-space: nowrap; pointer-events: none; }
    .arena-toast.show { opacity: 1; }
    .arena-toast.alert { border-color: rgba(255,23,68,.55); color: #ff8799; }
    .arena-status { display: flex; justify-content: space-between; align-items: center; gap: 10px; margin-top: 10px; color: var(--muted); font: 8px ui-monospace, monospace; }
    .status-led { display: flex; align-items: center; gap: 7px; }
    .status-led::before { content: ""; width: 7px; height: 7px; border-radius: 50%; background: var(--muted); }
    .status-led.running { color: var(--green); }
    .status-led.running::before { background: var(--green); box-shadow: 0 0 10px var(--green); }
    .arena-legend { display: flex; gap: 13px; flex-wrap: wrap; margin-top: 8px; color: var(--muted); font: 8px ui-monospace, monospace; }
    .legend-item { display: flex; align-items: center; gap: 5px; }
    .legend-dot { width: 7px; height: 7px; border-radius: 2px; background: var(--cyan); }
    .legend-dot.pending { background: var(--amber); }
    .legend-dot.rogue { background: var(--red); }

    .game-side { display: grid; gap: 12px; align-content: start; }
    .game-card { border: 1px solid var(--line); border-radius: 13px; padding: 14px; background: rgba(255,255,255,.02); }
    .game-card h3 { margin: 0 0 10px; font-size: 11px; }
    .game-intro { color: var(--muted); font-size: 9px; line-height: 1.6; margin: 0 0 12px; }
    .game-stats { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
    .game-stat { padding: 10px; border: 1px solid var(--line); background: rgba(0,0,0,.15); border-radius: 9px; }
    .game-stat strong { display: block; color: var(--cyan); font: 18px ui-monospace, monospace; }
    .game-stat span { display: block; color: var(--muted); font: 7px ui-monospace, monospace; letter-spacing: .08em; text-transform: uppercase; margin-top: 4px; }
    .timer-track { height: 5px; margin-top: 10px; background: rgba(255,255,255,.07); border-radius: 9px; overflow: hidden; }
    .timer-fill { height: 100%; background: linear-gradient(90deg, var(--cyan), var(--green)); width: 100%; transition: width 1s linear; }
    .timer-fill.low { background: linear-gradient(90deg, var(--amber), var(--red)); }
    .game-actions { display: grid; gap: 8px; margin-top: 11px; }
    .game-actions .btn { width: 100%; min-height: 40px; }
    .candidate-callout { min-height: 49px; padding: 9px; border: 1px dashed var(--line); border-radius: 9px; color: var(--muted); font: 8px/1.6 ui-monospace, monospace; }
    .candidate-callout.pending { border-color: rgba(255,196,0,.45); color: var(--amber); background: rgba(255,196,0,.04); }
    .candidate-callout.rogue { border-color: rgba(255,23,68,.5); color: #ff8296; background: rgba(255,23,68,.05); }
    .game-message { color: var(--muted); font: 8px/1.65 ui-monospace, monospace; margin: 10px 0 0; min-height: 27px; }
    .game-summary { display: none; padding: 10px; margin-top: 10px; border-radius: 9px; border: 1px solid rgba(0,230,118,.28); color: #adffd0; background: rgba(0,230,118,.055); font-size: 9px; line-height: 1.6; }
    .game-summary.show { display: block; }
    .game-summary.failed { border-color: rgba(255,23,68,.35); color: #ff9aab; background: rgba(255,23,68,.06); }
    .rules-list { list-style: none; padding: 0; margin: 0; display: grid; gap: 8px; color: var(--muted); font: 8px/1.5 ui-monospace, monospace; }
    .rules-list li { display: flex; gap: 8px; }
    .rules-list b { color: var(--green); font-weight: 500; }
    .rules-list .rule-red { color: var(--red); }
    .footer-note { color: #65748c; text-align: center; font: 8px ui-monospace, monospace; padding: 19px 0 0; }

    @keyframes pulse { 50% { opacity: .45; box-shadow: 0 0 3px var(--green); } }
    @keyframes blockPulse { to { filter: brightness(1.35); } }
    @keyframes alertFlash { to { box-shadow: 0 0 17px rgba(255,23,68,.19); } }
    @keyframes orbit { to { transform: rotate(360deg); } }
    @keyframes hover { 50% { transform: translateY(-5px); } }
    @keyframes candidatePulse { to { filter: brightness(1.5); transform: scale(1.08); } }
    @media (max-width: 1120px) {
      .overview { grid-template-columns: minmax(250px, .8fr) minmax(380px, 1.2fr); }
      .sim-panel { grid-column: 1 / -1; }
      .sim-panel .panel-body { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
      .sim-panel .panel-body > div + div { border-left: 1px solid var(--line); padding-left: 20px; }
      .simulator { margin-top: 0; }
    }
    @media (max-width: 760px) {
      .shell { padding: 18px 14px 30px; }
      .topbar { align-items: flex-start; flex-direction: column; }
      .top-meta { justify-content: flex-start; }
      .overview { grid-template-columns: 1fr; }
      .sim-panel { grid-column: auto; }
      .sim-panel .panel-body { display: block; }
      .sim-panel .panel-body > div + div { border-left: 0; padding-left: 0; margin-top: 18px; border-top: 1px solid var(--line); padding-top: 14px; }
      .simulator { margin-top: 14px; }
      .game-layout { grid-template-columns: 1fr; }
      .arena { min-height: 300px; }
    }
    @media (max-width: 430px) {
      .sim-actions { grid-template-columns: 1fr; }
      .tabs { gap: 0; }
      .tab { flex: 1; padding-inline: 8px; }
      .peer { font-size: 7px; }
      .arena { min-height: 275px; }
    }
    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after { animation-duration: .01ms !important; animation-iteration-count: 1 !important; scroll-behavior: auto !important; transition-duration: .01ms !important; }
    }
  </style>
</head>
<body>
  <main class="shell">
    <header class="topbar">
      <div class="brand">
        <div class="brand-mark" aria-hidden="true">✦</div>
        <div>
          <h1>SkyShield <span style="color:var(--muted);font-weight:450">/ Drone IoT Blockchain Simulator</span></h1>
          <div class="subtitle">PERMISSIONED NETWORK SECURITY · FABRIC-INSPIRED COMMAND DECK</div>
        </div>
      </div>
      <div class="top-meta">
        <span class="chip demo-badge">SIMULATION MODE</span>
        <span class="chip">CHANNEL: SKY-FLEET-01</span>
        <span class="live-pill"><i class="live-dot" aria-hidden="true"></i> NETWORK NOMINAL</span>
      </div>
    </header>

    <section class="overview" aria-label="Fleet, ledger, and simulator">
      <section class="panel" aria-labelledby="fleet-heading">
        <div class="panel-head">
          <div><div class="eyebrow">01 / Fleet Control Deck</div><h2 id="fleet-heading">Registered drone assets</h2></div>
          <span class="small-stat">X.509 IDENTITY</span>
        </div>
        <div class="panel-body">
          <div class="fleet-summary">
            <div class="mini-stat"><strong id="fleet-count">05</strong><span>Enrolled</span></div>
            <div class="mini-stat"><strong id="fleet-safe">05</strong><span>Operational</span></div>
            <div class="mini-stat"><strong id="fleet-grounded" style="color:var(--green)">00</strong><span>Grounded</span></div>
          </div>
          <div class="drone-list" id="drone-list" aria-live="polite"></div>
          <div class="fleet-footer"><span>IDENTITY PROVIDER: SKY-CA-01</span><span id="firmware-tag">FLEET FW · —</span></div>
        </div>
      </section>

      <section class="panel" aria-labelledby="ledger-heading">
        <div class="panel-head">
          <div><div class="eyebrow">02 / Ledger State</div><h2 id="ledger-heading">Permissioned blockchain grid</h2></div>
          <span class="small-stat" id="ledger-height">HEIGHT · 000</span>
        </div>
        <div class="panel-body">
          <div class="ledger-topline">
            <strong><span aria-hidden="true">◈</span> SKY-FLEET-01 / IMMUTABLE LOG</strong>
            <span class="consensus" id="consensus-state">● CONSENSUS IDLE</span>
          </div>
          <div class="peer-row" id="peer-row" aria-label="Peer endorsements">
            <div class="peer" data-peer="0">PEER 01</div><div class="peer" data-peer="1">PEER 02</div><div class="peer" data-peer="2">PEER 03</div>
          </div>
          <div class="chain" id="chain" aria-live="polite"><div class="empty-chain">Initializing genesis block…</div></div>
          <div class="ledger-caption"><span>SEQUENTIAL · HASH-LINKED · APPEND-ONLY</span><span id="latest-commit">AWAITING GENESIS</span></div>
          <div class="chain-note">Simulated Fabric-style endorsement policy: 2 of 3 peers</div>
        </div>
      </section>

      <section class="panel sim-panel" aria-labelledby="sim-heading">
        <div class="panel-head">
          <div><div class="eyebrow">03 / Interactive Testing Ground</div><h2 id="sim-heading">Firmware integrity simulator</h2></div>
          <span class="small-stat">OPERATOR / RED TEAM</span>
        </div>
        <div class="panel-body">
          <div>
            <div class="eyebrow">Manufacturer Genesis</div>
            <p class="section-note">Release a signed firmware payload to the permissioned ledger. Its SHA-256 fingerprint becomes the fleet's trusted reference.</p>
            <form id="publish-form">
              <label class="form-label" for="fw-version">Firmware version</label>
              <input id="fw-version" name="version" value="v2.0.4" maxlength="24" autocomplete="off" required>
              <label class="form-label" for="fw-binary">Firmware binary code <span style="color:var(--muted)">(simulated text payload)</span></label>
              <textarea id="fw-binary" name="binary" maxlength="4000" required>SKYSHIELD_FW_v2.0.4::manufacturer_signature=SS-CA-01</textarea>
              <button class="btn primary" id="publish-button" type="submit"><span aria-hidden="true">＋</span> Publish to Blockchain</button>
              <div class="form-feedback" id="publish-feedback" role="status">Ready to propose a firmware transaction.</div>
            </form>
          </div>
          <div class="simulator">
            <div class="eyebrow">Firmware Check & Detection</div>
            <p class="section-note">Test the fleet's latest committed release against a normal sync or an intercepted cellular link.</p>
            <div class="sim-actions">
              <button class="btn green" id="sync-button" type="button"><span aria-hidden="true">↻</span> Standard Deployment Sync</button>
              <button class="btn red" id="attack-button" type="button"><span aria-hidden="true">⚠</span> Man-In-The-Middle Attack</button>
            </div>
            <div class="sim-result" id="sim-result" aria-live="polite">
              <div class="result-title">SYSTEM READY</div>
              <div class="result-detail">Select a deployment path to verify the current firmware against the ledger.</div>
            </div>
            <div class="alert-banner" id="alert-banner" role="alert">TAMPER DETECTED: CRYPTOGRAPHIC SIGNATURE MISMATCH!</div>
            <div class="reset-row">
              <span class="small-stat" id="grounding-note">ALL ASSETS AIRBORNE</span>
              <button class="reset-btn" id="restore-button" type="button">Restore fleet / clear incident</button>
            </div>
          </div>
        </div>
      </section>
    </section>

    <nav class="tabs" aria-label="Simulator modes">
      <button class="tab active" id="dashboard-tab" type="button" aria-selected="true">Command Deck</button>
      <button class="tab" id="game-tab" type="button" aria-selected="false">▶ Play Demo Game</button>
    </nav>

    <section class="game-panel" id="game-panel" aria-labelledby="game-title">
      <div class="game-layout">
        <section class="panel">
          <div class="panel-head">
            <div><div class="eyebrow">Search & Rescue / Live Simulation</div><h2 id="game-title">Drone Swarm Intrusion Game</h2></div>
            <span class="small-stat">60-SECOND MISSION</span>
          </div>
          <div class="panel-body">
            <div class="arena-wrap">
              <div class="arena" id="arena" aria-label="Drone swarm simulation field">
                <div class="arena-hud"><span>SECTOR 07 / SEARCH GRID</span><span id="arena-clock">READY</span></div>
                <div class="arena-center"><div class="rescue-zone"><b>⌖</b>RESCUE ZONE</div></div>
                <div class="arena-toast" id="arena-toast" role="status"></div>
              </div>
            </div>
            <div class="arena-status">
              <span class="status-led" id="game-status">MISSION STANDBY</span>
              <span id="swarm-status">5 AUTHENTICATED NODES</span>
            </div>
            <div class="arena-legend">
              <span class="legend-item"><i class="legend-dot"></i> VERIFIED SWARM</span>
              <span class="legend-item"><i class="legend-dot pending"></i> HANDSHAKE REQUEST</span>
              <span class="legend-item"><i class="legend-dot rogue"></i> ROGUE / SPOOFED</span>
            </div>
          </div>
        </section>
        <aside class="game-side">
          <section class="panel">
            <div class="panel-head">
              <div><div class="eyebrow">Mission Control</div><h2>Handshake console</h2></div>
              <span class="small-stat">BEST · <span id="best-score">0000</span></span>
            </div>
            <div class="panel-body">
              <p class="game-intro">Five certified drones are searching for survivors. Authenticate every join request before its timer expires. The ledger rejects impostors before they can enter the swarm.</p>
              <div class="game-stats">
                <div class="game-stat"><strong id="game-score">0000</strong><span>Integrity score</span></div>
                <div class="game-stat"><strong id="game-time">60<span style="font-size:10px">s</span></strong><span>Mission time</span></div>
              </div>
              <div class="timer-track" aria-label="Mission time remaining"><div class="timer-fill" id="timer-fill"></div></div>
              <div class="game-actions">
                <button class="btn green" id="start-game" type="button">▶ Start 60s mission</button>
                <div class="candidate-callout" id="candidate-callout">Awaiting mission start. Incoming identities will appear here.</div>
                <button class="btn" id="handshake-button" type="button" disabled>◈ Trigger Blockchain Handshake</button>
              </div>
              <p class="game-message" id="game-message" role="status">Secure the swarm. Every authenticated join strengthens its rescue signal.</p>
              <div class="game-summary" id="game-summary" aria-live="polite"></div>
            </div>
          </section>
          <section class="panel">
            <div class="panel-body">
              <div class="eyebrow">How to play</div>
              <h2 style="margin:6px 0 12px">Consensus is your shield</h2>
              <ul class="rules-list">
                <li><b>01</b><span>Wait for an identity to request access.</span></li>
                <li><b>02</b><span>Trigger a handshake before the request expires.</span></li>
                <li><b>03</b><span>Valid certificates join; rogue payloads are isolated.</span></li>
                <li><b class="rule-red">!</b><span>Miss a rogue request and the network is compromised.</span></li>
              </ul>
            </div>
          </section>
        </aside>
      </div>
    </section>
    <div class="footer-note">CLIENT-SIDE SIMULATION · NO LIVE BLOCKCHAIN, CLOUD ENDPOINT, OR EXTERNAL DATABASE CONNECTED</div>
  </main>

  <script>
    (() => {
      "use strict";

      const $ = (selector) => document.querySelector(selector);
      const sleep = (ms) => new Promise((resolve) => window.setTimeout(resolve, ms));
      const encoder = new TextEncoder();
      const drones = [
        { id: "SKY-01", key: "9A:4F:2D:88:10:C7", status: "OPERATIONAL" },
        { id: "SKY-02", key: "71:CC:03:B2:5E:19", status: "OPERATIONAL" },
        { id: "SKY-03", key: "A6:21:EF:47:9B:32", status: "OPERATIONAL" },
        { id: "SKY-04", key: "3D:80:CA:14:6F:E1", status: "OPERATIONAL" },
        { id: "SKY-05", key: "F2:6B:91:0A:DC:73", status: "OPERATIONAL" }
      ];
      const state = {
        blocks: [],
        firmware: [],
        activeFirmware: null,
        busy: false,
        compromised: false,
        game: { running: false, time: 60, score: 0, best: 0, authenticated: 5, candidate: null, requestId: 0, interval: null, spawnTimeout: null, nodes: [] }
      };
      const gamePositions = [
        [24, 31], [39, 67], [57, 28], [72, 63], [81, 40],
        [17, 58], [31, 44], [47, 76], [66, 48], [84, 70],
        [22, 75], [57, 57], [75, 24], [43, 21], [91, 52]
      ];

      async function sha256(value) {
        if (!window.crypto || !window.crypto.subtle) {
          throw new Error("Web Crypto is unavailable. Use a secure browser context (HTTPS or localhost) to calculate SHA-256.");
        }
        const digest = await window.crypto.subtle.digest("SHA-256", encoder.encode(value));
        return Array.from(new Uint8Array(digest), (byte) => byte.toString(16).padStart(2, "0")).join("");
      }

      function makeElement(tag, className, text) {
        const element = document.createElement(tag);
        if (className) element.className = className;
        if (text !== undefined) element.textContent = text;
        return element;
      }

      function renderFleet() {
        const list = $("#drone-list");
        list.replaceChildren();
        drones.forEach((drone) => {
          const compromised = drone.status !== "OPERATIONAL";
          const card = makeElement("article", `drone-card${compromised ? " compromised" : ""}`);
          const top = makeElement("div", "drone-top");
          const name = makeElement("div", "drone-name");
          name.append(makeElement("span", "drone-icon", "⌁"), document.createTextNode(drone.id));
          top.append(name, makeElement("span", `status${compromised ? " bad" : ""}`, drone.status));
          const meta = makeElement("div", "drone-meta");
          const identity = makeElement("div");
          identity.append(document.createTextNode("CERT FP  "), makeElement("span", "key", drone.key));
          const version = makeElement("div");
          version.append(document.createTextNode("FIRMWARE  "), makeElement("span", "key", state.activeFirmware ? state.activeFirmware.version : "INITIALIZING"));
          meta.append(identity, version);
          card.append(top, meta);
          list.append(card);
        });
        const grounded = drones.filter((drone) => drone.status !== "OPERATIONAL").length;
        $("#fleet-count").textContent = String(drones.length).padStart(2, "0");
        $("#fleet-grounded").textContent = String(grounded).padStart(2, "0");
        $("#fleet-grounded").style.color = grounded ? "var(--red)" : "var(--green)";
        $("#fleet-safe").textContent = String(drones.length - grounded).padStart(2, "0");
        $("#firmware-tag").textContent = `FLEET FW · ${state.activeFirmware ? state.activeFirmware.version : "—"}`;
      }

      function renderLedger(proposingIndex = -1) {
        const chain = $("#chain");
        chain.replaceChildren();
        if (!state.blocks.length) {
          chain.append(makeElement("div", "empty-chain", "Initializing genesis block…"));
        } else {
          state.blocks.forEach((block, index) => {
            const card = makeElement("article", `block${index === proposingIndex ? " proposing" : ""}`);
            card.append(makeElement("h3", "", `${index === proposingIndex ? "◌ PROPOSAL" : "◆ BLOCK"} · ${String(block.index).padStart(3, "0")}`));
            const version = makeElement("p", "", `TX: ${block.version}`);
            const payload = makeElement("p", "", block.kind === "genesis" ? "TYPE: CHANNEL GENESIS" : "TYPE: FIRMWARE RELEASE");
            const hash = makeElement("p", "hash", `SHA-256: ${block.hash.slice(0, 18)}…`);
            const previous = makeElement("p", "", `PREV: ${block.previousHash.slice(0, 14)}…`);
            card.append(version, payload, hash, previous);
            chain.append(card);
          });
        }
        $("#ledger-height").textContent = `HEIGHT · ${String(state.blocks.length).padStart(3, "0")}`;
        $("#latest-commit").textContent = state.blocks.length ? `COMMITTED ${state.blocks[state.blocks.length - 1].time}` : "AWAITING GENESIS";
        chain.scrollLeft = chain.scrollWidth;
      }

      function resetPeers() {
        document.querySelectorAll(".peer").forEach((peer, index) => {
          peer.classList.remove("active", "done");
          peer.textContent = `PEER 0${index + 1}`;
        });
      }

      async function createBlock({ version, binary, kind }) {
        const payloadHash = await sha256(binary);
        const previousHash = state.blocks.length ? state.blocks[state.blocks.length - 1].hash : "0".repeat(64);
        const index = state.blocks.length;
        const time = new Date().toLocaleTimeString([], { hour: "2-digit", minute: "2-digit", second: "2-digit" });
        const hash = await sha256(`${index}|${version}|${payloadHash}|${previousHash}|${kind}`);
        return { index, version, binary, payloadHash, previousHash, hash, kind, time };
      }

      async function initialize() {
        try {
          const binary = "SKYSHIELD_FW_v2.0.3::manufacturer_signature=SS-CA-01";
          const genesis = await createBlock({ version: "v2.0.3", binary, kind: "genesis" });
          state.blocks.push(genesis);
          state.firmware.push({ version: genesis.version, binary: genesis.binary, hash: genesis.payloadHash, block: genesis.index });
          state.activeFirmware = state.firmware[state.firmware.length - 1];
          renderFleet();
          renderLedger();
          $("#consensus-state").textContent = "● GENESIS COMMITTED";
          $("#consensus-state").style.color = "var(--green)";
          $("#publish-feedback").textContent = "Genesis channel online. Ready for firmware proposals.";
        } catch (error) {
          $("#chain").replaceChildren(makeElement("div", "empty-chain", error.message));
          $("#consensus-state").textContent = "● CRYPTO API UNAVAILABLE";
          $("#consensus-state").style.color = "var(--red)";
          $("#publish-feedback").textContent = error.message;
          $("#publish-button").disabled = true;
          $("#sync-button").disabled = true;
          $("#attack-button").disabled = true;
        }
      }

      async function publishFirmware(event) {
        event.preventDefault();
        if (state.busy) return;
        const version = $("#fw-version").value.trim();
        const binary = $("#fw-binary").value;
        if (!version || !binary.trim()) {
          $("#publish-feedback").textContent = "Version and firmware payload are both required.";
          return;
        }
        if (state.firmware.some((firmware) => firmware.version.toLowerCase() === version.toLowerCase())) {
          $("#publish-feedback").textContent = "That version is already committed. Choose a new version number.";
          return;
        }
        state.busy = true;
        $("#publish-button").disabled = true;
        $("#publish-feedback").textContent = "Hashing firmware payload with SHA-256…";
        $("#consensus-state").textContent = "● PROPOSAL IN FLIGHT";
        $("#consensus-state").style.color = "var(--amber)";
        resetPeers();
        try {
          const proposal = await createBlock({ version, binary, kind: "firmware" });
          const card = makeElement("article", "block proposing");
          card.append(makeElement("h3", "", `◌ PROPOSAL · ${String(proposal.index).padStart(3, "0")}`));
          card.append(makeElement("p", "", `TX: ${proposal.version}`));
          card.append(makeElement("p", "hash", `SHA-256: ${proposal.hash.slice(0, 18)}…`));
          card.append(makeElement("p", "", "AWAITING ENDORSEMENT…"));
          $("#chain").append(card);
          $("#chain").scrollLeft = $("#chain").scrollWidth;
          $("#publish-feedback").textContent = "Proposal submitted. Waiting for peer endorsements…";
          for (let index = 0; index < 3; index += 1) {
            await sleep(600);
            const peer = document.querySelector(`[data-peer="${index}"]`);
            peer.classList.add(index < 2 ? "done" : "active");
            peer.textContent = index < 2 ? `PEER 0${index + 1} ✓` : "PEER 03 · VALIDATING";
          }
          await sleep(450);
          resetPeers();
          state.blocks.push(proposal);
          state.firmware.push({ version, binary, hash: proposal.payloadHash, block: proposal.index });
          state.activeFirmware = state.firmware[state.firmware.length - 1];
          renderFleet();
          renderLedger();
          $("#consensus-state").textContent = "● CONSENSUS VERIFIED";
          $("#consensus-state").style.color = "var(--green)";
          $("#publish-feedback").textContent = `${version} committed to block ${String(proposal.index).padStart(3, "0")} · 2/3 peers endorsed.`;
        } catch (error) {
          $("#publish-feedback").textContent = `Proposal failed: ${error.message}`;
          $("#consensus-state").textContent = "● PROPOSAL FAILED";
          $("#consensus-state").style.color = "var(--red)";
          renderLedger();
        } finally {
          state.busy = false;
          $("#publish-button").disabled = false;
        }
      }

      async function runIntegrityCheck(isAttack) {
        if (state.busy || !state.activeFirmware) return;
        state.busy = true;
        $("#sync-button").disabled = true;
        $("#attack-button").disabled = true;
        $("#alert-banner").classList.remove("show");
        const result = $("#sim-result");
        result.className = "sim-result";
        result.replaceChildren(makeElement("div", "result-title", isAttack ? "CELLULAR LINK INTERCEPTED" : "DEPLOYMENT SYNC IN PROGRESS"));
        const detail = makeElement("div", "result-detail");
        result.append(detail);
        detail.textContent = "1 / 3  Hashing binary with SHA-256…";
        $("#consensus-state").textContent = "● VERIFYING FIRMWARE";
        $("#consensus-state").style.color = "var(--amber)";
        try {
          await sleep(650);
          let deliveredBinary = state.activeFirmware.binary;
          if (isAttack) {
            const index = Math.floor(deliveredBinary.length / 2);
            const original = deliveredBinary[index];
            const replacement = original === "X" ? "Y" : "X";
            deliveredBinary = `${deliveredBinary.slice(0, index)}${replacement}${deliveredBinary.slice(index + 1)}`;
          }
          const deliveredHash = await sha256(deliveredBinary);
          detail.textContent = "2 / 3  Comparing firmware fingerprint against ledger matrix…";
          await sleep(700);
          result.replaceChildren();
          result.className = `sim-result ${deliveredHash === state.activeFirmware.hash ? "safe" : "danger"}`;
          const title = deliveredHash === state.activeFirmware.hash ? "HANDSHAKE SECURE · SYSTEM NOMINAL" : "HANDSHAKE REJECTED · TAMPER DETECTED";
          result.append(makeElement("div", "result-title", title));
          result.append(makeElement("div", "result-detail", `3 / 3  ${deliveredHash === state.activeFirmware.hash ? "Consensus verified" : "Ledger mismatch"} · release ${state.activeFirmware.version}`));
          const compare = makeElement("div", "hash-compare");
          const ledgerHash = makeElement("div", "hash-line", `LEDGER SHA-256  ${state.activeFirmware.hash}`);
          const suppliedHash = makeElement("div", "hash-line", `${isAttack ? "SPOOFED" : "DEPLOYED"} SHA-256  ${deliveredHash}`);
          suppliedHash.style.color = deliveredHash === state.activeFirmware.hash ? "var(--green)" : "var(--red)";
          compare.append(ledgerHash, suppliedHash);
          result.append(compare);
          if (deliveredHash !== state.activeFirmware.hash) {
            state.compromised = true;
            drones.forEach((drone) => { drone.status = "GROUNDED / COMPROMISED"; });
            renderFleet();
            $("#grounding-note").textContent = "SECURITY INCIDENT · FLEET GROUNDED";
            $("#grounding-note").style.color = "var(--red)";
            $("#alert-banner").classList.add("show");
            $("#consensus-state").textContent = "● INVALID PAYLOAD REJECTED";
            $("#consensus-state").style.color = "var(--red)";
          } else {
            state.compromised = false;
            drones.forEach((drone) => { drone.status = "OPERATIONAL"; });
            renderFleet();
            $("#grounding-note").textContent = "ALL ASSETS AIRBORNE";
            $("#grounding-note").style.color = "var(--muted)";
            $("#consensus-state").textContent = "● CONSENSUS VERIFIED";
            $("#consensus-state").style.color = "var(--green)";
          }
        } catch (error) {
          result.replaceChildren(makeElement("div", "result-title", "CRYPTOGRAPHIC CHECK FAILED"));
          result.append(makeElement("div", "result-detail", error.message));
          $("#consensus-state").textContent = "● VERIFICATION ERROR";
          $("#consensus-state").style.color = "var(--red)";
        } finally {
          state.busy = false;
          $("#sync-button").disabled = false;
          $("#attack-button").disabled = false;
        }
      }

      function restoreFleet() {
        state.compromised = false;
        drones.forEach((drone) => { drone.status = "OPERATIONAL"; });
        renderFleet();
        $("#alert-banner").classList.remove("show");
        $("#grounding-note").textContent = "ALL ASSETS AIRBORNE";
        $("#grounding-note").style.color = "var(--muted)";
        const result = $("#sim-result");
        result.className = "sim-result";
        result.replaceChildren(makeElement("div", "result-title", "FLEET RESTORED"));
        result.append(makeElement("div", "result-detail", "Drone assets are operational. The immutable ledger remains unchanged."));
        $("#consensus-state").textContent = "● CONSENSUS IDLE";
        $("#consensus-state").style.color = "var(--amber)";
      }

      function renderGameNodes() {
        const arena = $("#arena");
        arena.querySelectorAll(".game-drone").forEach((node) => node.remove());
        state.game.nodes.forEach((node, index) => {
          const position = gamePositions[index % gamePositions.length];
          const icon = makeElement("div", "game-drone", "⌁");
          icon.setAttribute("aria-label", `Authenticated swarm drone ${node}`);
          icon.style.left = `${position[0]}%`;
          icon.style.top = `${position[1]}%`;
          icon.style.animationDelay = `${(index % 5) * -0.3}s`;
          arena.append(icon);
        });
        if (state.game.candidate) {
          const candidate = makeElement("div", `game-drone candidate${state.game.candidate.rogue ? " rogue" : ""}`, "⌁");
          candidate.setAttribute("aria-label", state.game.candidate.rogue ? "Rogue drone requesting access" : "Certified drone requesting access");
          candidate.style.left = "50%";
          candidate.style.top = "52%";
          candidate.style.transform = "translate(-50%, -50%)";
          arena.append(candidate);
        }
        $("#swarm-status").textContent = `${String(state.game.authenticated).padStart(2, "0")} AUTHENTICATED NODES`;
      }

      function showToast(message, alert = false) {
        const toast = $("#arena-toast");
        toast.textContent = message;
        toast.classList.toggle("alert", alert);
        toast.classList.add("show");
        window.setTimeout(() => toast.classList.remove("show"), 1800);
      }

      function updateGameHud() {
        $("#game-score").textContent = String(state.game.score).padStart(4, "0");
        $("#best-score").textContent = String(state.game.best).padStart(4, "0");
        $("#game-time").innerHTML = `${state.game.time}<span style="font-size:10px">s</span>`;
        $("#arena-clock").textContent = state.game.running ? `T−${String(state.game.time).padStart(2, "0")}s` : (state.game.time === 0 ? "MISSION END" : "READY");
        $("#timer-fill").style.width = `${(state.game.time / 60) * 100}%`;
        $("#timer-fill").classList.toggle("low", state.game.time <= 15);
        $("#game-status").textContent = state.game.running ? "MISSION ACTIVE" : (state.game.time === 0 ? "MISSION COMPLETE" : "MISSION STANDBY");
        $("#game-status").classList.toggle("running", state.game.running);
        $("#start-game").textContent = state.game.running ? "Mission in progress…" : "▶ Start 60s mission";
        $("#start-game").disabled = state.game.running;
        $("#handshake-button").disabled = !state.game.running || !state.game.candidate;
      }

      function spawnCandidate() {
        if (!state.game.running || state.game.candidate) return;
        const rogue = Math.random() < 0.38;
        state.game.requestId += 1;
        state.game.candidate = { id: rogue ? `ROGUE-${String(state.game.requestId).padStart(2, "0")}` : `SKY-R${String(state.game.requestId).padStart(2, "0")}`, rogue, timeLeft: 5 };
        renderGameNodes();
        updateGameHud();
        $("#candidate-callout").className = `candidate-callout pending${rogue ? " rogue" : ""}`;
        $("#candidate-callout").textContent = `${rogue ? "⚠ UNTRUSTED IDENTITY" : "◈ CERTIFICATE PRESENT"} · ${state.game.candidate.id} · ${rogue ? "SPOOFED CERT / PAYLOAD" : "SKY-CA SIGNED"} · 5s`;
        $("#game-message").textContent = rogue ? "An unknown identity is approaching. Trigger consensus to isolate it." : "A certified rescue drone is requesting to join the swarm.";
        if (rogue) showToast("ROGUE IDENTITY DETECTED · AUTHENTICATE NOW", true);
        else showToast("NEW DRONE REQUEST · CERTIFICATE PRESENT");
      }

      function endGame(won) {
        state.game.running = false;
        state.game.candidate = null;
        window.clearInterval(state.game.interval);
        window.clearTimeout(state.game.spawnTimeout);
        renderGameNodes();
        updateGameHud();
        const summary = $("#game-summary");
        summary.className = `game-summary show${won ? "" : " failed"}`;
        summary.textContent = won
          ? `MISSION COMPLETE · Integrity score ${String(state.game.score).padStart(4, "0")}. You won because the consensus protocol rejected the rogue nodes before they could write to the state database!`
          : `NETWORK COMPROMISED · A rogue node passed its handshake window. Mission score: ${String(state.game.score).padStart(4, "0")}. Restart and authenticate every join request before it expires.`;
        $("#game-message").textContent = won ? "All identities checked. Rescue swarm stayed protected for the full mission." : "An unauthenticated payload reached the swarm topology.";
        $("#start-game").disabled = false;
      }

      function scheduleNextCandidate() {
        window.clearTimeout(state.game.spawnTimeout);
        const delay = 3500 + Math.floor(Math.random() * 1700);
        state.game.spawnTimeout = window.setTimeout(spawnCandidate, delay);
      }

      function startGame() {
        if (state.game.running) return;
        window.clearInterval(state.game.interval);
        window.clearTimeout(state.game.spawnTimeout);
        state.game.running = true;
        state.game.time = 60;
        state.game.score = 0;
        state.game.authenticated = 5;
        state.game.candidate = null;
        state.game.requestId = 0;
        state.game.nodes = ["SKY-01", "SKY-02", "SKY-03", "SKY-04", "SKY-05"];
        $("#game-summary").className = "game-summary";
        $("#candidate-callout").className = "candidate-callout";
        $("#candidate-callout").textContent = "Scanning for incoming network identities…";
        $("#game-message").textContent = "Mission live. Stand by for the first join request.";
        renderGameNodes();
        updateGameHud();
        scheduleNextCandidate();
        state.game.interval = window.setInterval(() => {
          state.game.time -= 1;
          if (state.game.candidate) {
            state.game.candidate.timeLeft -= 1;
            const candidate = state.game.candidate;
            $("#candidate-callout").textContent = `${candidate.rogue ? "⚠ UNTRUSTED IDENTITY" : "◈ CERTIFICATE PRESENT"} · ${candidate.id} · ${candidate.rogue ? "SPOOFED CERT / PAYLOAD" : "SKY-CA SIGNED"} · ${candidate.timeLeft}s`;
            if (candidate.timeLeft <= 0) {
              if (candidate.rogue) {
                state.game.score = Math.max(0, state.game.score - 100);
                endGame(false);
                return;
              }
              state.game.candidate = null;
              state.game.score = Math.max(0, state.game.score - 25);
              $("#candidate-callout").className = "candidate-callout";
              $("#candidate-callout").textContent = "Valid request timed out. Integrity penalty applied; scanning continues.";
              $("#game-message").textContent = "A trusted drone timed out and was not admitted. Keep watching for the next request.";
              renderGameNodes();
              scheduleNextCandidate();
            }
          }
          updateGameHud();
          if (state.game.time <= 0) {
            state.game.time = 0;
            state.game.best = Math.max(state.game.best, state.game.score);
            updateGameHud();
            endGame(true);
          }
        }, 1000);
      }

      function triggerHandshake() {
        const candidate = state.game.candidate;
        if (!state.game.running || !candidate) return;
        if (candidate.rogue) {
          state.game.score += 75;
          $("#game-message").textContent = `${candidate.id} rejected by 2/3 peers. Crypto Shield isolated the spoofed payload.`;
          $("#candidate-callout").className = "candidate-callout";
          $("#candidate-callout").textContent = `BLOCKED · ${candidate.id} rejected by consensus.`;
          showToast("CRYPTO SHIELD · ROGUE ISOLATED", true);
        } else {
          state.game.score += 100;
          state.game.authenticated += 1;
          state.game.nodes.push(candidate.id);
          $("#game-message").textContent = `${candidate.id} certificate matched the ledger. Node admitted; swarm processing power increased.`;
          $("#candidate-callout").className = "candidate-callout";
          $("#candidate-callout").textContent = `VERIFIED · ${candidate.id} certificate matches ledger.`;
          showToast("CONSENSUS VERIFIED · DRONE ADMITTED");
        }
        state.game.candidate = null;
        state.game.best = Math.max(state.game.best, state.game.score);
        renderGameNodes();
        updateGameHud();
        scheduleNextCandidate();
      }

      $("#publish-form").addEventListener("submit", publishFirmware);
      $("#sync-button").addEventListener("click", () => runIntegrityCheck(false));
      $("#attack-button").addEventListener("click", () => runIntegrityCheck(true));
      $("#restore-button").addEventListener("click", restoreFleet);
      $("#start-game").addEventListener("click", startGame);
      $("#handshake-button").addEventListener("click", triggerHandshake);
      $("#dashboard-tab").addEventListener("click", () => {
        $("#dashboard-tab").classList.add("active");
        $("#game-tab").classList.remove("active");
        $("#dashboard-tab").setAttribute("aria-selected", "true");
        $("#game-tab").setAttribute("aria-selected", "false");
        $("#game-panel").classList.remove("active");
      });
      $("#game-tab").addEventListener("click", () => {
        $("#game-tab").classList.add("active");
        $("#dashboard-tab").classList.remove("active");
        $("#game-tab").setAttribute("aria-selected", "true");
        $("#dashboard-tab").setAttribute("aria-selected", "false");
        $("#game-panel").classList.add("active");
      });
      renderFleet();
      renderGameNodes();
      updateGameHud();
      initialize();
    })();
  </script>
</body>
</html>

