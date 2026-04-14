<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Interactive Cell Diagram</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    background: #1a1a2e;
    font-family: 'Georgia', serif;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 16px;
    color: #e0e0e0;
  }
  h1 {
    font-size: 1.1rem;
    color: #a8d8ea;
    margin-bottom: 4px;
    text-align: center;
    letter-spacing: 1px;
  }
  .subtitle { font-size: 0.7rem; color: #666; margin-bottom: 12px; text-align: center; font-family: Arial; }

.wrapper {
display: flex;
gap: 14px;
width: 100%;
max-width: 1100px;
align-items: flex-start;
}

/* SVG diagram */
.diagram-container {
flex: 0 0 auto;
position: relative;
width: 480px;
}
svg { width: 480px; height: 580px; }

/* Info panel */
.info-panel {
flex: 1;
background: #0f0f1a;
border: 1px solid #2a2a4a;
border-radius: 12px;
padding: 16px;
min-height: 400px;
position: sticky;
top: 16px;
}
.info-panel h2 {
font-size: 1rem;
color: #58a6ff;
margin-bottom: 4px;
font-family: Georgia;
border-bottom: 1px solid #2a2a4a;
padding-bottom: 8px;
}
.info-panel .tag {
display: inline-block;
font-size: 0.65rem;
padding: 2px 8px;
border-radius: 10px;
margin-bottom: 10px;
font-family: Arial;
font-weight: bold;
}
.info-panel .section {
margin-bottom: 10px;
}
.info-panel .section-title {
font-size: 0.75rem;
font-weight: bold;
color: #e3b341;
font-family: Arial;
margin-bottom: 3px;
text-transform: uppercase;
letter-spacing: 0.5px;
}
.info-panel .section-body {
font-size: 0.74rem;
color: #c9d1d9;
line-height: 1.6;
font-family: Arial;
}
.info-panel .section-body li {
margin-left: 14px;
margin-bottom: 2px;
}
.placeholder {
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
height: 200px;
color: #444;
font-size: 0.8rem;
font-family: Arial;
text-align: center;
gap: 8px;
}
.placeholder svg { opacity: 0.3; }

/* Clickable labels */
.label-btn {
cursor: pointer;
transition: all 0.2s;
}
.label-btn:hover rect { filter: brightness(1.3); }
.label-btn.active rect { stroke-width: 2.5 !important; filter: brightness(1.4); }
.label-btn text { pointer-events: none; }

.dot {
cursor: pointer;
transition: r 0.2s;
}
.dot:hover { r: 7; }

/* Zone labels on SVG */
.zone-label { font-family: Arial; font-weight: bold; font-size: 10px; }

/* Legend */
.legend {
display: flex;
gap: 16px;
margin-top: 10px;
flex-wrap: wrap;
justify-content: center;
}
.legend-item {
display: flex;
align-items: center;
gap: 5px;
font-size: 0.65rem;
font-family: Arial;
color: #888;
}
.legend-dot {
width: 10px; height: 10px;
border-radius: 50%;
}
</style>

</head>
<body>

<h1>Unit 7 — Interactive Cell Diagram</h1>
<p class="subtitle">Click any labeled component to view detailed information</p>

<div class="wrapper">
  <!-- DIAGRAM -->
  <div class="diagram-container">
    <svg viewBox="0 0 480 580" xmlns="http://www.w3.org/2000/svg" id="mainSvg">
      <defs>
        <linearGradient id="cellGrad" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#1e3a5f"/>
          <stop offset="100%" stop-color="#16304d"/>
        </linearGradient>
        <linearGradient id="ecmGrad" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#2d1b00"/>
          <stop offset="100%" stop-color="#1a1000"/>
        </linearGradient>
        <linearGradient id="memGrad" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#4a90a4"/>
          <stop offset="100%" stop-color="#2a6070"/>
        </linearGradient>
      </defs>

```
  <!-- ── ZONES BACKGROUNDS ── -->
  <!-- Apical zone -->
  <rect x="0" y="0" width="480" height="60" fill="#0a0a1a"/>
  <text x="8" y="14" class="zone-label" fill="#6e7daa">APICAL SURFACE (lumen side)</text>

  <!-- Cell body -->
  <rect x="30" y="60" width="420" height="310" rx="0" fill="url(#cellGrad)" stroke="#3a5f8a" stroke-width="1.2"/>

  <!-- Lateral surface label lines -->
  <text x="4" y="200" class="zone-label" fill="#4a7a6a" transform="rotate(-90,4,200)">LATERAL</text>
  <text x="468" y="200" class="zone-label" fill="#4a7a6a" transform="rotate(90,468,200)">LATERAL</text>

  <!-- Basal membrane line -->
  <rect x="30" y="370" width="420" height="10" fill="url(#memGrad)"/>
  <text x="8" y="382" class="zone-label" fill="#6e7daa">BASAL SURFACE</text>

  <!-- ECM zone -->
  <rect x="0" y="380" width="480" height="200" fill="url(#ecmGrad)"/>
  <text x="8" y="396" class="zone-label" fill="#8a6030">EXTRACELLULAR MATRIX (ECM)</text>

  <!-- Nucleus -->
  <ellipse cx="240" cy="210" rx="60" ry="40" fill="#0d1b2a" stroke="#2a4a6a" stroke-width="1.5"/>
  <text x="240" y="207" text-anchor="middle" fill="#4a7aaa" font-size="9" font-family="Arial">NUCLEUS</text>
  <text x="240" y="218" text-anchor="middle" fill="#2a5a8a" font-size="7" font-family="Arial">(DNA)</text>

  <!-- Apical membrane -->
  <rect x="30" y="58" width="420" height="8" fill="url(#memGrad)" opacity="0.8"/>

  <!-- Lateral membranes -->
  <rect x="30" y="60" width="8" height="310" fill="url(#memGrad)" opacity="0.6"/>
  <rect x="442" y="60" width="8" height="310" fill="url(#memGrad)" opacity="0.6"/>

  <!-- ── ECM FIBERS ── -->
  <!-- Collagen fibers -->
  <path d="M50 410 Q120 400 200 415 Q280 430 360 415 Q420 405 460 420" stroke="#8b6914" stroke-width="3" fill="none" opacity="0.7"/>
  <path d="M50 440 Q130 430 210 445 Q290 460 370 445 Q430 435 460 450" stroke="#8b6914" stroke-width="3" fill="none" opacity="0.7"/>
  <path d="M50 470 Q140 460 220 475 Q300 490 380 475 Q440 465 460 480" stroke="#8b6914" stroke-width="2" fill="none" opacity="0.5"/>

  <!-- Proteoglycan molecules (small branched) -->
  <line x1="100" y1="430" x2="100" y2="405" stroke="#c0392b" stroke-width="1"/>
  <line x1="100" y1="415" x2="90" y2="408" stroke="#c0392b" stroke-width="1"/>
  <line x1="100" y1="415" x2="110" y2="408" stroke="#c0392b" stroke-width="1"/>
  <circle cx="100" cy="430" r="3" fill="#c0392b"/>

  <line x1="340" y1="455" x2="340" y2="430" stroke="#c0392b" stroke-width="1"/>
  <line x1="340" y1="440" x2="330" y2="433" stroke="#c0392b" stroke-width="1"/>
  <line x1="340" y1="440" x2="350" y2="433" stroke="#c0392b" stroke-width="1"/>
  <circle cx="340" cy="455" r="3" fill="#c0392b"/>

  <!-- Fibronectin (purple flat) -->
  <rect x="155" y="420" width="35" height="8" rx="4" fill="#8e44ad" opacity="0.8"/>
  <rect x="195" y="420" width="35" height="8" rx="4" fill="#8e44ad" opacity="0.8"/>
  <line x1="190" y1="424" x2="196" y2="424" stroke="#8e44ad" stroke-width="2"/>

  <!-- Laminin (cross shape) -->
  <line x1="380" y1="460" x2="420" y2="430" stroke="#27ae60" stroke-width="2"/>
  <line x1="390" y1="430" x2="410" y2="460" stroke="#27ae60" stroke-width="2"/>
  <circle cx="380" cy="460" r="4" fill="#27ae60"/>
  <circle cx="420" cy="430" r="4" fill="#27ae60"/>
  <circle cx="390" cy="430" r="4" fill="#1e8449"/>
  <circle cx="410" cy="460" r="4" fill="#1e8449"/>

  <!-- Hyaluronic acid (wavy) -->
  <path d="M50 500 Q65 490 80 500 Q95 510 110 500 Q125 490 140 500 Q155 510 170 500" stroke="#3498db" stroke-width="1.5" fill="none" opacity="0.6"/>

  <!-- Elastin -->
  <path d="M200 510 Q215 500 230 510 Q245 520 260 510 Q275 500 290 510" stroke="#e67e22" stroke-width="1.5" fill="none" opacity="0.5" stroke-dasharray="3,2"/>

  <!-- ── INTEGRINS (transmembrane) ── -->
  <!-- Focal adhesion integrins (3 of them) -->
  <!-- Integrin 1 at ~x=120 -->
  <rect x="115" y="342" width="8" height="40" rx="4" fill="#f39c12"/>
  <rect x="126" y="342" width="8" height="40" rx="4" fill="#e67e22"/>
  <ellipse cx="121" cy="340" rx="10" ry="7" fill="#f1c40f"/>
  <!-- binds ECM below -->
  <line x1="119" y1="382" x2="115" y2="395" stroke="#f39c12" stroke-width="1"/>
  <line x1="124" y1="382" x2="128" y2="395" stroke="#e67e22" stroke-width="1"/>

  <!-- Integrin 2 at ~x=200 -->
  <rect x="195" y="342" width="8" height="40" rx="4" fill="#f39c12"/>
  <rect x="206" y="342" width="8" height="40" rx="4" fill="#e67e22"/>
  <ellipse cx="201" cy="340" rx="10" ry="7" fill="#f1c40f"/>
  <line x1="199" y1="382" x2="195" y2="395" stroke="#f39c12" stroke-width="1"/>
  <line x1="204" y1="382" x2="208" y2="395" stroke="#e67e22" stroke-width="1"/>

  <!-- Hemidesmosome integrin at x=290 -->
  <rect x="285" y="350" width="8" height="32" rx="4" fill="#9b59b6"/>
  <rect x="296" y="350" width="8" height="32" rx="4" fill="#8e44ad"/>
  <ellipse cx="291" cy="348" rx="10" ry="7" fill="#d2a8ff"/>
  <line x1="289" y1="382" x2="285" y2="395" stroke="#9b59b6" stroke-width="1"/>
  <line x1="294" y1="382" x2="298" y2="395" stroke="#8e44ad" stroke-width="1"/>

  <!-- Actin filaments (horizontal) in cell -->
  <line x1="60" y1="330" x2="165" y2="330" stroke="#27ae60" stroke-width="2" opacity="0.7"/>
  <line x1="60" y1="335" x2="165" y2="335" stroke="#27ae60" stroke-width="2" opacity="0.5"/>
  <line x1="175" y1="330" x2="265" y2="330" stroke="#27ae60" stroke-width="2" opacity="0.7"/>
  <line x1="175" y1="335" x2="265" y2="335" stroke="#27ae60" stroke-width="2" opacity="0.5"/>

  <!-- Intermediate filaments for hemidesmosome -->
  <line x1="290" y1="350" x2="240" y2="280" stroke="#e74c3c" stroke-width="1.5" opacity="0.6" stroke-dasharray="4,2"/>
  <line x1="300" y1="350" x2="350" y2="280" stroke="#e74c3c" stroke-width="1.5" opacity="0.6" stroke-dasharray="4,2"/>

  <!-- Talin/Vinculin dots at focal adhesion -->
  <circle cx="130" cy="328" r="4" fill="#f39c12" opacity="0.9"/>
  <circle cx="140" cy="328" r="4" fill="#e67e22" opacity="0.9"/>
  <circle cx="210" cy="328" r="4" fill="#f39c12" opacity="0.9"/>
  <circle cx="220" cy="328" r="4" fill="#e67e22" opacity="0.9"/>

  <!-- ── CELL-CELL JUNCTIONS (lateral surfaces) ── -->
  <!-- Tight junction (top) -->
  <rect x="22" y="75" width="16" height="12" rx="3" fill="#2ecc71"/>
  <rect x="22" y="75" width="16" height="12" rx="3" fill="none" stroke="#27ae60" stroke-width="1"/>
  <!-- zigzag sealing strand -->
  <path d="M30 75 Q26 81 30 87" stroke="#27ae60" stroke-width="1.5" fill="none"/>

  <rect x="442" y="75" width="16" height="12" rx="3" fill="#2ecc71"/>

  <!-- Adherens junction -->
  <rect x="22" y="130" width="16" height="14" rx="3" fill="#3498db"/>
  <rect x="442" y="130" width="16" height="14" rx="3" fill="#3498db"/>

  <!-- Desmosome -->
  <rect x="22" y="195" width="16" height="16" rx="2" fill="#e74c3c"/>
  <rect x="22" y="195" width="16" height="16" rx="2" fill="none" stroke="#c0392b" stroke-width="1.5"/>
  <rect x="442" y="195" width="16" height="16" rx="2" fill="#e74c3c"/>

  <!-- Gap junction -->
  <rect x="22" y="270" width="16" height="14" rx="3" fill="#f39c12"/>
  <circle cx="25" cy="277" r="2" fill="#fff" opacity="0.7"/>
  <circle cx="30" cy="277" r="2" fill="#fff" opacity="0.7"/>
  <circle cx="35" cy="277" r="2" fill="#fff" opacity="0.7"/>
  <rect x="442" y="270" width="16" height="14" rx="3" fill="#f39c12"/>

  <!-- Selectins on apical -->
  <line x1="140" y1="58" x2="140" y2="38" stroke="#16a085" stroke-width="2"/>
  <circle cx="140" cy="35" r="6" fill="#16a085"/>
  <circle cx="136" cy="28" r="3" fill="#1abc9c"/>
  <circle cx="143" cy="27" r="3" fill="#1abc9c"/>

  <!-- IgSF CAMs on lateral -->
  <line x1="30" y1="160" x2="30" y2="130" stroke="#9b59b6" stroke-width="1.5"/>
  <circle cx="30" cy="128" r="5" fill="#9b59b6"/>
  <circle cx="30" cy="120" r="5" fill="#8e44ad"/>
  <circle cx="30" cy="112" r="5" fill="#7d3c98"/>

  <!-- ══════════════════════════════════════════ -->
  <!-- CLICKABLE LABEL BUTTONS -->
  <!-- ══════════════════════════════════════════ -->

  <!-- APICAL ZONE labels -->
  <!-- Selectins -->
  <g class="label-btn" onclick="showInfo('selectins')" id="btn-selectins">
    <rect x="100" y="18" width="58" height="16" rx="8" fill="#16a085" stroke="#1abc9c" stroke-width="1.5" opacity="0.9"/>
    <text x="129" y="30" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Selectins</text>
    <line x1="140" y1="34" x2="140" y2="35" stroke="#1abc9c" stroke-width="1" stroke-dasharray="2,1"/>
  </g>

  <!-- LATERAL labels -->
  <!-- Tight junction -->
  <g class="label-btn" onclick="showInfo('tight')" id="btn-tight">
    <rect x="280" y="70" width="80" height="16" rx="8" fill="#2ecc71" stroke="#27ae60" stroke-width="1.5" opacity="0.9"/>
    <text x="320" y="82" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Tight Junction</text>
    <line x1="298" y1="78" x2="38" y2="81" stroke="#27ae60" stroke-width="0.8" stroke-dasharray="3,2"/>
  </g>

  <!-- Adherens junction -->
  <g class="label-btn" onclick="showInfo('adherens')" id="btn-adherens">
    <rect x="270" y="128" width="92" height="16" rx="8" fill="#3498db" stroke="#2980b9" stroke-width="1.5" opacity="0.9"/>
    <text x="316" y="140" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Adherens Junction</text>
    <line x1="298" y1="137" x2="38" y2="137" stroke="#2980b9" stroke-width="0.8" stroke-dasharray="3,2"/>
  </g>

  <!-- IgSF CAMs -->
  <g class="label-btn" onclick="showInfo('igsf')" id="btn-igsf">
    <rect x="270" y="155" width="80" height="16" rx="8" fill="#8e44ad" stroke="#7d3c98" stroke-width="1.5" opacity="0.9"/>
    <text x="310" y="167" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">IgSF / CAMs</text>
    <line x1="298" y1="163" x2="35" y2="120" stroke="#7d3c98" stroke-width="0.8" stroke-dasharray="3,2"/>
  </g>

  <!-- Desmosome -->
  <g class="label-btn" onclick="showInfo('desmosome')" id="btn-desmosome">
    <rect x="270" y="192" width="72" height="16" rx="8" fill="#e74c3c" stroke="#c0392b" stroke-width="1.5" opacity="0.9"/>
    <text x="306" y="204" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Desmosome</text>
    <line x1="298" y1="200" x2="38" y2="203" stroke="#c0392b" stroke-width="0.8" stroke-dasharray="3,2"/>
  </g>

  <!-- Gap junction -->
  <g class="label-btn" onclick="showInfo('gap')" id="btn-gap">
    <rect x="270" y="268" width="72" height="16" rx="8" fill="#f39c12" stroke="#e67e22" stroke-width="1.5" opacity="0.9"/>
    <text x="306" y="280" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Gap Junction</text>
    <line x1="298" y1="277" x2="38" y2="277" stroke="#e67e22" stroke-width="0.8" stroke-dasharray="3,2"/>
  </g>

  <!-- BASAL / FOCAL ADHESION labels -->
  <!-- Focal adhesion -->
  <g class="label-btn" onclick="showInfo('focal')" id="btn-focal">
    <rect x="60" y="305" width="82" height="16" rx="8" fill="#f39c12" stroke="#e67e22" stroke-width="1.5" opacity="0.9"/>
    <text x="101" y="317" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Focal Adhesion</text>
    <line x1="100" y1="321" x2="120" y2="328" stroke="#e67e22" stroke-width="0.8" stroke-dasharray="2,1"/>
  </g>

  <!-- Integrin -->
  <g class="label-btn" onclick="showInfo('integrin')" id="btn-integrin">
    <rect x="55" y="353" width="50" height="16" rx="8" fill="#f1c40f" stroke="#f39c12" stroke-width="1.5" opacity="0.9"/>
    <text x="80" y="365" text-anchor="middle" fill="#1a1a1a" font-size="8" font-family="Arial" font-weight="bold">Integrin</text>
    <line x1="98" y1="361" x2="115" y2="355" stroke="#f39c12" stroke-width="0.8" stroke-dasharray="2,1"/>
  </g>

  <!-- Hemidesmosome -->
  <g class="label-btn" onclick="showInfo('hemi')" id="btn-hemi">
    <rect x="310" y="340" width="96" height="16" rx="8" fill="#9b59b6" stroke="#8e44ad" stroke-width="1.5" opacity="0.9"/>
    <text x="358" y="352" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Hemidesmosome</text>
    <line x1="340" y1="348" x2="295" y2="356" stroke="#8e44ad" stroke-width="0.8" stroke-dasharray="2,1"/>
  </g>

  <!-- ECM LABELS -->
  <!-- Collagen -->
  <g class="label-btn" onclick="showInfo('collagen')" id="btn-collagen">
    <rect x="44" y="392" width="56" height="15" rx="7" fill="#8b6914" stroke="#d4a017" stroke-width="1.5" opacity="0.95"/>
    <text x="72" y="403" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Collagen</text>
  </g>

  <!-- Fibronectin -->
  <g class="label-btn" onclick="showInfo('fibronectin')" id="btn-fibronectin">
    <rect x="148" y="406" width="66" height="15" rx="7" fill="#8e44ad" stroke="#9b59b6" stroke-width="1.5" opacity="0.95"/>
    <text x="181" y="417" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Fibronectin</text>
  </g>

  <!-- Laminin -->
  <g class="label-btn" onclick="showInfo('laminin')" id="btn-laminin">
    <rect x="358" y="440" width="54" height="15" rx="7" fill="#27ae60" stroke="#2ecc71" stroke-width="1.5" opacity="0.95"/>
    <text x="385" y="451" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Laminin</text>
  </g>

  <!-- Proteoglycan -->
  <g class="label-btn" onclick="showInfo('proteoglycan')" id="btn-proteoglycan">
    <rect x="44" y="444" width="80" height="15" rx="7" fill="#c0392b" stroke="#e74c3c" stroke-width="1.5" opacity="0.95"/>
    <text x="84" y="455" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Proteoglycan</text>
    <line x1="100" y1="444" x2="100" y2="433" stroke="#e74c3c" stroke-width="0.8" stroke-dasharray="2,1"/>
  </g>

  <!-- Hyaluronic acid -->
  <g class="label-btn" onclick="showInfo('ha')" id="btn-ha">
    <rect x="44" y="497" width="80" height="15" rx="7" fill="#2980b9" stroke="#3498db" stroke-width="1.5" opacity="0.95"/>
    <text x="84" y="508" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Hyaluronic Acid</text>
    <line x1="130" y1="504" x2="160" y2="500" stroke="#3498db" stroke-width="0.8" stroke-dasharray="2,1"/>
  </g>

  <!-- Elastin -->
  <g class="label-btn" onclick="showInfo('elastin')" id="btn-elastin">
    <rect x="260" y="527" width="46" height="15" rx="7" fill="#e67e22" stroke="#f39c12" stroke-width="1.5" opacity="0.95"/>
    <text x="283" y="538" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Elastin</text>
    <line x1="256" y1="534" x2="240" y2="512" stroke="#f39c12" stroke-width="0.8" stroke-dasharray="2,1"/>
  </g>

  <!-- Basal lamina label -->
  <g class="label-btn" onclick="showInfo('basallamina')" id="btn-basallamina">
    <rect x="358" y="375" width="74" height="15" rx="7" fill="#4a6080" stroke="#6a80a0" stroke-width="1.5" opacity="0.95"/>
    <text x="395" y="386" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Basal Lamina</text>
  </g>

  <!-- Cadherins label -->
  <g class="label-btn" onclick="showInfo('cadherins')" id="btn-cadherins">
    <rect x="358" y="190" width="62" height="15" rx="7" fill="#3498db" stroke="#2980b9" stroke-width="1.5" opacity="0.9"/>
    <text x="389" y="201" text-anchor="middle" fill="white" font-size="8" font-family="Arial" font-weight="bold">Cadherins</text>
  </g>

</svg>

<div class="legend">
  <div class="legend-item"><div class="legend-dot" style="background:#2ecc71"></div> Tight Jn.</div>
  <div class="legend-item"><div class="legend-dot" style="background:#3498db"></div> Adherens Jn.</div>
  <div class="legend-item"><div class="legend-dot" style="background:#e74c3c"></div> Desmosome</div>
  <div class="legend-item"><div class="legend-dot" style="background:#f39c12"></div> Gap Jn. / FA</div>
  <div class="legend-item"><div class="legend-dot" style="background:#9b59b6"></div> Hemidesmosome</div>
  <div class="legend-item"><div class="legend-dot" style="background:#8b6914"></div> ECM</div>
</div>
```

  </div>

  <!-- INFO PANEL -->

  <div class="info-panel" id="infoPanel">
    <div class="placeholder">
      <svg width="40" height="40" viewBox="0 0 40 40"><circle cx="20" cy="20" r="18" stroke="#444" stroke-width="2" fill="none"/><text x="20" y="26" text-anchor="middle" fill="#444" font-size="18">👆</text></svg>
      <span>Click a component on the diagram<br>to view detailed information</span>
    </div>
  </div>
</div>

<script>
const data = {
  integrin: {
    title: "Integrins",
    color: "#f1c40f",
    tag: "Cell-ECM Receptor",
    tagColor: "#f39c12",
    sections: [
      { title: "What is it?", body: "Large family of heterodimeric, transmembrane receptors. Interface between ECM & cytosol. Found in 10–100× higher numbers than other membrane receptors." },
      { title: "Subunits", body: "<ul><li><b>α subunit</b>: extracellular globular head → ECM binding site (RGD sequence of fibronectin)</li><li><b>β subunit</b>: legs cross plasma membrane → cytoplasmic tail binds talin</li><li>18α + 8β subunits = 144 potential combos → ~24 identified</li><li>α & β held together by non-covalent interactions</li></ul>" },
      { title: "Structure", body: "<ul><li><b>Extracellular globular heads</b> = ECM binding sites</li><li><b>Legs</b> = contain transmembrane domain</li><li><b>Small cytoplasmic tails</b> = bind talin, vinculin, α-actinin</li></ul>" },
      { title: "Inactive vs Active", body: "<ul><li><b>Inactive</b>: legs together, globular head curved inward, LOW affinity for ECM (still binds loosely)</li><li><b>Active</b>: legs apart, integrin straightens, HIGH affinity → binds ligand tightly</li><li>Low affinity binding causes conformational change → legs separate</li></ul>" },
      { title: "Functions", body: "<ul><li>① Cell adhesion to ECM via focal adhesions & hemidesmosomes</li><li>② Bidirectional signal transduction (outside-in & inside-out)</li><li>③ Adhesion to other cells (leukocyte-specific)</li><li>Mechanotransduction: force → signal across membrane</li><li>Chemotransduction: chemical signals across membrane</li></ul>" },
      { title: "Binds What?", body: "Fibronectin (RGD domain), Laminin, Collagen (depending on α/β combo). Cytoplasmic: Talin, Vinculin, α-actinin → triggers actin polymerization" }
    ]
  },
  focal: {
    title: "Focal Adhesions",
    color: "#f39c12",
    tag: "Cell-ECM Junction",
    tagColor: "#e67e22",
    sections: [
      { title: "What is it?", body: "Macromolecular clusters of integrins found at POINTS along cell membrane (not entire length). Found in migratory & non-epithelial cells. Most cells adhere to ECM via focal adhesions." },
      { title: "Steps of Formation", body: "<ul><li>① Globular heads bind ECM ligand</li><li>② Conformational change activates integrin</li><li>③ Cytoplasmic proteins bind integrin<br>  (3A) Talin, Vinculin, α-actinin bind → actin polymerization → actin binds myosin → main reason for cell movement<br>  (3B) Paxillin recruits FAK → signal cascade via phosphorylation → changes gene expression</li></ul>" },
      { title: "Mechanism", body: "Binding of ECM ligand stimulates focal adhesion formation = OUTSIDE-IN signalling. ECM first → conformational change → cytoplasmic proteins bind." },
      { title: "Key Proteins", body: "<ul><li>Integrin (α+β)</li><li>Talin, Vinculin, α-Actinin (link to actin)</li><li>FAK (focal adhesion kinase) → signals to nucleus</li><li>Paxillin, Src kinase</li><li>Actin filaments + Myosin</li></ul>" },
      { title: "Signalling", body: "Signals transmitted to nucleus via FAK → Src → changes in DNA expression. Outside-in signalling (ECM → cytoplasm)." }
    ]
  },
  hemi: {
    title: "Hemidesmosomes",
    color: "#9b59b6",
    tag: "Cell-ECM Junction (Epithelial only)",
    tagColor: "#8e44ad",
    sections: [
      { title: "What is it?", body: "Multiprotein complexes that anchor epithelial cells to the basal lamina. Specific to epithelial cells. Tightest attachment of cell to ECM." },
      { title: "Cytoplasmic Side", body: "<ul><li>Dense plaques containing plakin family proteins (linkers)</li><li>BPAG1 & Plectin → bind integrin + intermediate filaments</li><li>Binds dense plaque in cytoplasm</li></ul>" },
      { title: "Extracellular", body: "Integrin (α6β4) binds Laminin 332 in basal lamina → holds cell to ECM" },
      { title: "Key Proteins", body: "<ul><li>Integrin (α6β4, α3β1)</li><li>BPAG1 (BP230), BPAG2 (BP180/Collagen XVII)</li><li>Plectin → links integrin to IF</li><li>Laminin (in ECM)</li><li>Collagen IV (in ECM)</li></ul>" },
      { title: "Associated with IF", body: "Unlike focal adhesions (actin), hemidesmosomes link to INTERMEDIATE FILAMENTS (keratin)" },
      { title: "Disease Links", body: "<ul><li><b>Epidermolysis bullosa</b>: inherited mutation in hemidesmosomal proteins → skin breakdown ('butterfly children')</li><li><b>Bullous pemphigoid</b>: autoimmune → antibodies attack BPAG proteins → blistering, fluid leaks</li></ul>" }
    ]
  },
  tight: {
    title: "Tight Junctions (Zonula Occludens)",
    color: "#2ecc71",
    tag: "Sealing Junction",
    tagColor: "#27ae60",
    sections: [
      { title: "What is it?", body: "Occluding/sealing junctions found at apical surface of epithelial cells (gut epithelium = zonula occludens). Encircle entire cell like a belt." },
      { title: "Key Proteins", body: "<ul><li>Claudins & Occludins → transmembrane proteins forming sealing strands</li><li>ZO-1, ZO-2 (Zonulins) → link claudins/occludins to actin via adaptor proteins</li><li>JAM-A → Junctional Adhesion Molecule</li></ul>" },
      { title: "Functions", body: "<ul><li>① Prevent diffusion of molecules BETWEEN cells (paracellular pathway) → allows gradients</li><li>② Prevent lateral migration of transporters in membrane (keeps SGLT apical, GLUT2 basal)</li></ul>" },
      { title: "Glucose Transport Example", body: "Tight junctions allow glucose gradient: SGLT in apical membrane takes glucose from lumen → GLUT2 in basal membrane exits to blood. Without TJ → glucose leaks back." },
      { title: "Structure", body: "Membranes joined along interlocking ridges of transmembrane proteins. Sealing strands run horizontally." }
    ]
  },
  adherens: {
    title: "Adherens Junctions (Zonula Adherens)",
    color: "#3498db",
    tag: "Adhesive/Anchoring Junction",
    tagColor: "#2980b9",
    sections: [
      { title: "What is it?", body: "Cell-cell adhesive junction common in epithelial tissues. Forms a continuous zone (belt) around the cell = 'adhesion belt'. Below the tight junction." },
      { title: "Key Proteins", body: "<ul><li>Cadherins (E-cadherin) → transmembrane, Ca²⁺-dependent adhesion</li><li>Catenins (α-catenin, β-catenin) → adaptor proteins linking cadherin to actin</li><li>Actin-binding proteins</li><li>Actin filaments (microfilaments)</li></ul>" },
      { title: "Structure", body: "Cadherins linked to actin cytoskeleton via adaptor proteins (catenins → actin-binding proteins). Cadherins from adjacent cells bind each other across intercellular space." },
      { title: "Location", body: "Just below tight junction on lateral surface. Forms the 'zonula adherens' belt around cell circumference." },
      { title: "Function", body: "Strong cell-cell adhesion. Links to actin allows contractile forces to be transmitted between cells → important in tissue morphogenesis." }
    ]
  },
  desmosome: {
    title: "Desmosomes (Macula Adherens)",
    color: "#e74c3c",
    tag: "Adhesive/Anchoring Junction",
    tagColor: "#c0392b",
    sections: [
      { title: "What is it?", body: "Disc-shaped cell-cell junctions found in epithelial tissues. Localized spot-like attachments = macula adherens. Associated with INTERMEDIATE FILAMENTS." },
      { title: "Key Proteins", body: "<ul><li><b>Desmoglein & Desmocollin</b> → desmosomal cadherins (Ca²⁺-dependent)</li><li><b>Desmoplakin</b> → plakin protein, links to IF</li><li><b>Plakoglobin</b> → in dense plaque, adaptor</li><li>Dense plaque in cytoplasm</li><li>Intermediate filaments (keratin)</li></ul>" },
      { title: "Structure", body: "Two dense plaques (one per cell) connected by desmosomal cadherins across intercellular space. IFs insert into dense plaque." },
      { title: "Difference from Adherens", body: "<ul><li>Adherens → actin (microfilaments)</li><li>Desmosome → intermediate filaments (keratin)</li></ul>" },
      { title: "Disease", body: "<b>Pemphigus vulgaris</b>: autoimmune → antibodies against desmoglein/desmocollin → blistering of skin/mucous membranes." }
    ]
  },
  gap: {
    title: "Gap Junctions",
    color: "#f39c12",
    tag: "Communicating Junction",
    tagColor: "#e67e22",
    sections: [
      { title: "What is it?", body: "Communicating junctions that allow small molecules (ions, cAMP, glucose) to pass freely between adjacent cells. Found in all mammalian cells EXCEPT skeletal muscle." },
      { title: "Structure", body: "<ul><li>Each gap junction = 2 connexons in register (one from each cell)</li><li>Each connexon = 6 connexin subunits arranged in a ring</li><li>Channel = 1.5 nm diameter, hydrophilic</li><li>Gap between cells = 2–4 nm</li><li>Annulus = channel pore</li></ul>" },
      { title: "What passes through?", body: "Ions (Na⁺, K⁺, Ca²⁺), small molecules <1 kDa: cAMP, glucose, amino acids. Large molecules (proteins, DNA) CANNOT pass." },
      { title: "Function", body: "Electrical & metabolic coupling between cells. Essential for coordinated contraction in cardiac muscle (intercalated discs)." },
      { title: "Disease", body: "Some cardiac arrhythmias → downregulation of connexin → poor electrical coupling between cardiomyocytes → uncoordinated contraction." }
    ]
  },
  selectins: {
    title: "Selectins",
    color: "#16a085",
    tag: "Cell-Cell Adhesion Molecule",
    tagColor: "#1abc9c",
    sections: [
      { title: "What is it?", body: "Cell-cell adhesion molecules that recognize & bind specific sugar groups on cell surface glycolipids & glycoproteins." },
      { title: "Types", body: "<ul><li><b>P-selectins</b> → platelets & endothelial cells</li><li><b>E-selectins</b> → surface of endothelial cells (blood vessel lining)</li><li><b>L-selectins</b> → surface of leukocytes (WBCs)</li></ul>" },
      { title: "Structure", body: "<ul><li>Lectin-like domain (binds sugar)</li><li>EGF-like domain</li><li>Structural domain</li><li>Transmembrane domain</li></ul>" },
      { title: "Binding", body: "<ul><li>Transient LOW affinity binding initially</li><li>Becomes stronger with mechanical stress (induced by blood flow)</li><li>Not specific to one membrane sugar — recognize general sugar pattern</li></ul>" },
      { title: "Function", body: "Involved in immune & inflammatory responses. Allow leukocytes to 'roll' along endothelium before extravasation (leave blood vessel into tissue)." }
    ]
  },
  igsf: {
    title: "IgSF Members (CAMs)",
    color: "#8e44ad",
    tag: "Cell-Cell Adhesion Molecule",
    tagColor: "#7d3c98",
    sections: [
      { title: "What is it?", body: "Immunoglobulin superfamily proteins including Cell Adhesion Molecules (CAMs). All have IgG domains." },
      { title: "Can bind", body: "Other CAMs (homophilic) OR integrins (heterophilic)" },
      { title: "Types of CAMs", body: "<ul><li><b>N-CAM</b> = neural CAM → nervous system development, binds its own IgG domains</li><li><b>L1-CAM</b> → also nervous system development</li><li><b>I-CAM</b> = intercellular CAM ★ → binds integrins on leukocytes (endothelial cells)</li><li><b>V-CAM</b> = vascular CAM</li></ul>" },
      { title: "Functions", body: "<ul><li>Most mediate interactions between immune cells</li><li>Some mediate adhesion between non-immune cells</li><li>Important in embryonic development</li><li>I-CAM on endothelial cells binds leukocyte integrins → allows immune cell exit from blood</li></ul>" }
    ]
  },
  cadherins: {
    title: "Cadherins",
    color: "#3498db",
    tag: "Cell-Cell Adhesion Molecule",
    tagColor: "#2980b9",
    sections: [
      { title: "What is it?", body: "Ca²⁺-dependent cell-cell adhesion molecules. Important in cell-cell recognition during embryogenesis. Bind to SIMILAR cadherins (homophilic)." },
      { title: "Structure", body: "<ul><li>5–6 repeating domains</li><li>Similar cadherins → bonded cadherins → transmembrane proteins</li><li>Ca²⁺ required for binding between domains</li></ul>" },
      { title: "Types", body: "<ul><li><b>P-cadherins</b> → placental, epidermis (skin)</li><li><b>E-cadherins</b> → epithelium</li><li><b>N-cadherins</b> → neural</li></ul>" },
      { title: "In Junctions", body: "<ul><li>Adherens junctions → E-cadherin + catenins + actin</li><li>Desmosomes → Desmoglein/Desmocollin (desmosomal cadherins) + IF</li></ul>" },
      { title: "Cancer Link", body: "Cancer cells travel & loosens around → E-cadherin loss → causes metastasis (cells detach and invade other tissues)" }
    ]
  },
  collagen: {
    title: "Collagen",
    color: "#d4a017",
    tag: "ECM Structural Protein",
    tagColor: "#8b6914",
    sections: [
      { title: "What is it?", body: "Largest family of fibrous glycoproteins. Most abundant protein in mammals (~25–30% total protein). Found only in vertebrates. 28 types (I–XXVIII)." },
      { title: "Structure", body: "<ul><li>3 α-chains twist together (triple helix = 2° structure)</li><li>α-chains have Gly-X-Y repeats (X=proline, Y=hydroxyproline*)</li><li>Hydroxylysine* also present (*rare in other proteins)</li><li>Fibrils + fibers stabilized by covalent bonds + H-bonds between hydroxylated AAs</li></ul>" },
      { title: "Key Amino Acids", body: "Glycine: small size → fits inside helix (key to triple helix). Hydroxyproline & Hydroxylysine: require Vitamin C for hydroxylation → stabilize collagen via H-bonds & covalent cross-links." },
      { title: "Types", body: "<ul><li><b>Type I</b>: most abundant (90%), skin/bone/tendon</li><li><b>Type II</b>: cartilage</li><li><b>Type III</b>: organs, smooth muscle, blood vessels</li><li><b>Type IV</b>: basal lamina (highly glycosylated, no long fibrils)</li></ul>" },
      { title: "Synthesis", body: "Precursor α-chain (soluble) → 3 chains assemble in ER (procollagen, triple helix with loose ends) → secreted → procollagen peptidase trims loose ends → tropocollagen → self-assembly → collagen fibril → collagen fiber (staggered = striated)" },
      { title: "Disease", body: "<b>Scurvy</b>: Vitamin C deficiency → can't hydroxylate → weak collagen → inflamed gums, poor wound healing, brittle bones. <b>Osteogenesis Imperfecta</b>: mutation in Gly codon → brittle bone disease." }
    ]
  },
  fibronectin: {
    title: "Fibronectin (Fn)",
    color: "#9b59b6",
    tag: "ECM Adhesive Glycoprotein",
    tagColor: "#8e44ad",
    sections: [
      { title: "What is it?", body: "Fibrous adhesive glycoprotein. 2 non-identical protein chains connected by 2 disulfide bridges at C-terminus." },
      { title: "Structure / Domains", body: "Each chain has several functional domains:<ul><li>ECM-ECM: Heparin-binding domain, Collagen-binding domain, Fibrin-binding domain</li><li>ECM-Cell: Cell-binding domain → RGD sequence → binds integrins</li><li>Heparin-binding & Fibrin-binding sites (×2)</li></ul>" },
      { title: "RGD Domain", body: "Arg-Gly-Asp (RGD) loop → the integrin binding site. Integrins on cell surface bind this loop. Key for cell adhesion to ECM." },
      { title: "Function", body: "Links ECM components to each other (ECM cohesivity) AND links ECM to cells via integrins. Important in cell migration & embryogenesis (e.g. anti-FN antibodies block salivary gland branching)." },
      { title: "Experiment", body: "Mouse salivary gland: grown 10hrs in culture → buds form. + Anti-FN antibodies → FN blocked → NO budding. Shows FN essential for morphogenesis." }
    ]
  },
  laminin: {
    title: "Laminin",
    color: "#27ae60",
    tag: "ECM Adhesive Glycoprotein",
    tagColor: "#1e8449",
    sections: [
      { title: "What is it?", body: "Adhesive glycoprotein with 3 different chains linked by disulfide bonds. Major component of basal lamina." },
      { title: "Structure", body: "<ul><li>α chain, β chain, γ chain → 3-stranded coiled coil</li><li>Functional domains: Collagen IV binding, Entactin binding, Heparin/heparan sulfate binding, Cell-surface receptor binding domain (binds integrins on cell)</li></ul>" },
      { title: "Function", body: "<ul><li>ECM-ECM cohesivity (binds collagen IV, entactin, heparin)</li><li>ECM-Cell interaction via integrins (cell-surface receptor binding domain)</li><li>Critical for basal lamina function</li></ul>" },
      { title: "In Matrigel", body: "60% of Matrigel™ is laminin → key component for organoid culture" },
      { title: "PGC Migration", body: "Primordial Germ Cells (PGCs) migrate along laminin tracks during embryogenesis (green PGCs on red laminin fibers in fluorescence image)." }
    ]
  },
  proteoglycan: {
    title: "Proteoglycans",
    color: "#c0392b",
    tag: "ECM Ground Substance",
    tagColor: "#e74c3c",
    sections: [
      { title: "What is it?", body: "Massive protein-polysaccharide complexes = core protein + GAG chains. Form the ground substance/matrix of ECM." },
      { title: "Components", body: "<ul><li><b>Core protein</b>: ~40 types; soluble (most) or transmembrane</li><li><b>GAGs</b> (Glycosaminoglycans): long, unbranched polysaccharides of disaccharide repeats; one sugar always -ve charged; made & added to core protein in Golgi (O-linked, glycosylation)</li></ul>" },
      { title: "GAG Types", body: "<ul><li>Heparan sulfate → epithelium/basal lamina</li><li>Dermatan sulfate → skin</li><li>Chondroitin sulfate → cartilage, bone</li><li>Keratan sulfate → cornea, brain</li><li>Hyaluronic acid → everywhere (special - not linked to protein)</li></ul>" },
      { title: "Function", body: "Negative charges attract cations (Na⁺) → water follows to maintain osmotic gradient → very hydrated matrix. Binds signalling molecules (ECM acts as sink for growth factors → regulates bioavailability)." },
      { title: "Hyaluronic acid backbone", body: "HA is backbone of LARGE proteoglycan complexes with many proteoglycans attached. 3 million Daltons. Not bound to core protein — freely floating in ECM." }
    ]
  },
  ha: {
    title: "Hyaluronic Acid (HA)",
    color: "#2980b9",
    tag: "Special GAG (not sulfated)",
    tagColor: "#3498db",
    sections: [
      { title: "What is it?", body: "Unique GAG — the only one NOT sulfated and NOT bound to a core protein (freely floating in ECM). Made by enzyme in PLASMA MEMBRANE (not Golgi)." },
      { title: "Properties", body: "<ul><li>Not sulfated</li><li>Not bound to core protein → freely floating</li><li>Made by enzyme in plasma membrane</li><li>~3 million Daltons</li><li>Found EVERYWHERE (ubiquitous)</li></ul>" },
      { title: "Function", body: "<ul><li>Backbone of large proteoglycan complexes (many proteoglycans attach to HA)</li><li>Provides hydration → highly viscous gel</li><li>Joint lubrication</li></ul>" },
      { title: "Aging", body: "↓ HA as we age → wrinkles, less lubrication in joints (synovial fluid reduced)" },
      { title: "Clinical use", body: "Hyaluronic acid fillers (cosmetics), joint injections for osteoarthritis" }
    ]
  },
  elastin: {
    title: "Elastin",
    color: "#e67e22",
    tag: "ECM Structural Protein",
    tagColor: "#d35400",
    sections: [
      { title: "What is it?", body: "Elastic ECM protein that allows tissues to stretch and recoil. Made as tropoelastin in ER, assembled into elastic fibers in ECM (mature elastin molecule)." },
      { title: "Structure", body: "<ul><li>No hydroxylysine, some hydroxyproline</li><li>Single elastin molecules crosslinked by COVALENT bonds in ECM</li><li>Random coil → stretches under tension → recoils when tension released</li></ul>" },
      { title: "Where found", body: "Lungs, elastic arteries, ligaments — tissues requiring repeated stretch/recoil" },
      { title: "Aging", body: "As we age: ↑ cross-linking of collagen + ↓ elasticity → wrinkles. Elastin degraded and not replaced efficiently." }
    ]
  },
  basallamina: {
    title: "Basal Lamina (Basement Membrane)",
    color: "#6a80a0",
    tag: "ECM Specialized Sheet",
    tagColor: "#4a6080",
    sections: [
      { title: "What is it?", body: "Continuous sheet of ECM containing Type IV collagen. Underlies epithelium AND surrounds muscle & fat cells." },
      { title: "Key Components", body: "<ul><li>Collagen IV (highly glycosylated, no long fibrils)</li><li>Laminin (major adhesive glycoprotein)</li><li>Entactin/Nidogen (adhesive glycoprotein)</li><li>Heparan sulfate (GAG)</li></ul>" },
      { title: "Functions", body: "Structural support for epithelial/muscle cells. Filter (kidney glomerulus). Barrier to cell migration. Guide cell migration during development." },
      { title: "Matrigel connection", body: "Matrigel™ mimics basal lamina: 60% laminin, 30% collagen IV, 8% entactin, heparan sulfate, growth factors → used to grow organoids (3D replications of organs in culture)" }
    ]
  }
};

let activeBtn = null;

function showInfo(key) {
  const d = data[key];
  if (!d) return;

  // Reset old active button
  if (activeBtn) {
    const old = document.getElementById('btn-' + activeBtn);
    if (old) old.classList.remove('active');
  }

  // Set new active
  const btn = document.getElementById('btn-' + key);
  if (btn) btn.classList.add('active');
  activeBtn = key;

  const panel = document.getElementById('infoPanel');
  let html = `<h2>${d.title}</h2>
    <span class="tag" style="background:${d.tagColor}22; color:${d.tagColor}; border:1px solid ${d.tagColor}">${d.tag}</span>`;

  d.sections.forEach(s => {
    html += `<div class="section">
      <div class="section-title">${s.title}</div>
      <div class="section-body">${s.body}</div>
    </div>`;
  });

  panel.innerHTML = html;
  panel.scrollTop = 0;
}
</script>

</body>
</html>
