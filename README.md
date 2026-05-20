<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CWC Knowledge Engine</title>
<style>
  * { margin:0; padding:0; box-sizing:border-box; }
  html, body {
    background:#0A1520;
    color:#ffffff;
    font-family:'Segoe UI',Tahoma,Geneva,Verdana,sans-serif;
    width:100%;
    min-height:100vh;
  }
  :root {
    --green:#3EAB72;
    --navy:#0A1520;
    --card:#0F2030;
    --border:#1A3045;
    --grey:#B0BBCC;
  }
  a { color:var(--green); text-decoration:none; }
  a:hover { opacity:0.85; }
  .page { padding:0 32px 40px; background:#0A1520; }

  /* ── HERO ── */
  .hero {
    display:flex;
    gap:24px;
    padding:48px 0 40px;
    align-items:stretch;
  }
  .hero-left {
    flex:0 0 62%;
    min-width:0;
    position:relative;
    overflow:hidden;
  }
  .hero-dots {
    position:absolute;
    top:0; right:0;
    width:70%; height:100%;
    pointer-events:none;
    z-index:0;
    background-image:radial-gradient(circle, rgba(62,171,114,0.18) 1px, transparent 1px);
    background-size:22px 22px;
    -webkit-mask-image:linear-gradient(to left, rgba(0,0,0,0.7) 0%, rgba(0,0,0,0.3) 50%, transparent 100%);
    mask-image:linear-gradient(to left, rgba(0,0,0,0.7) 0%, rgba(0,0,0,0.3) 50%, transparent 100%);
  }
  .hero-content { position:relative; z-index:1; }
  .hero-left h1 {
    font-size:52px;
    font-weight:700;
    color:#fff;
    margin:0 0 14px;
    line-height:1.1;
  }
  .hero-left p.tagline {
    font-size:18px;
    color:var(--grey);
    margin:0 0 28px;
  }
  .search-bar {
    display:flex;
    border-radius:8px;
    overflow:hidden;
    border:1px solid var(--border);
    margin-bottom:20px;
  }
  .search-bar input {
    flex:1;
    padding:14px 16px;
    background:var(--card);
    border:none;
    color:#fff;
    font-size:14px;
    outline:none;
    font-family:inherit;
  }
  .search-bar input::placeholder { color:var(--grey); }
  .search-bar button {
    background:var(--green);
    color:#fff;
    border:none;
    padding:14px 28px;
    font-size:14px;
    font-weight:600;
    cursor:pointer;
    font-family:inherit;
    white-space:nowrap;
  }
  .search-bar button:hover { opacity:0.9; }
  .popular {
    display:flex;
    align-items:center;
    gap:10px;
    flex-wrap:wrap;
  }
  .popular span.label { font-size:13px; color:var(--grey); }
  .pill {
    padding:5px 13px;
    border:1px solid var(--border);
    border-radius:20px;
    font-size:12px;
    color:#fff;
    background:var(--card);
    cursor:pointer;
  }
  .pill:hover { border-color:var(--green); }

  .hero-right {
    flex:1;
    background:var(--card);
    border:1px solid var(--border);
    border-radius:12px;
    padding:24px;
    display:flex;
    flex-direction:column;
    min-width:0;
  }
  .hero-right .icon { font-size:26px; margin-bottom:10px; }
  .hero-right h2 { font-size:19px; font-weight:600; color:#fff; margin:0 0 12px; }
  .hero-right p { font-size:13px; color:var(--grey); line-height:1.6; margin:0 0 20px; }
  .hub-links { display:flex; flex-direction:column; gap:10px; margin-bottom:20px; }
  .hub-links a { font-size:13px; color:var(--green); }
  .img-placeholder {
    flex:1;
    min-height:90px;
    background:linear-gradient(135deg,#0a2535,#1A3045);
    border-radius:8px;
    display:flex;
    align-items:center;
    justify-content:center;
  }
  .img-placeholder span { font-size:11px; color:#1A3045; }

  /* ── 6 TILES ── */
  .tiles {
    display:grid;
    grid-template-columns:repeat(6,1fr);
    gap:12px;
    padding:0 0 28px;
  }
  .tile {
    background:var(--card);
    border:1px solid var(--border);
    border-radius:10px;
    padding:20px 15px;
    cursor:pointer;
    transition:border-color 0.2s;
    display:flex;
    flex-direction:column;
  }
  .tile:hover { border-color:var(--green); }
  .tile .tile-icon { font-size:22px; margin-bottom:10px; }
  .tile .tile-title { font-size:13px; font-weight:600; color:#fff; margin:0 0 6px; }
  .tile .tile-sub { font-size:11px; color:var(--grey); margin:0 0 14px; line-height:1.4; flex:1; }
  .tile .arrow { color:var(--green); font-size:15px; }

  /* ── 4 PANELS ── */
  .panels {
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:16px;
    padding:0 0 28px;
  }
  .panel {
    background:var(--card);
    border:1px solid var(--border);
    border-radius:12px;
    padding:20px;
    display:flex;
    flex-direction:column;
  }
  .panel-title {
    font-size:14px;
    font-weight:600;
    color:#fff;
    margin:0 0 18px;
  }
  .panel-body { flex:1; margin-bottom:18px; }
  .view-all { color:var(--green); font-size:13px; }

  /* guidance list */
  .guide-list { display:flex; flex-direction:column; gap:13px; }
  .guide-item { display:flex; gap:9px; align-items:flex-start; }
  .dot { width:8px; height:8px; border-radius:50%; background:var(--green); margin-top:4px; flex-shrink:0; }
  .guide-item p { font-size:12px; font-weight:600; color:#fff; margin:0 0 3px; }
  .guide-item span { font-size:11px; color:var(--grey); line-height:1.4; }

  /* recently updated */
  .update-list { display:flex; flex-direction:column; gap:11px; }
  .update-row { display:flex; align-items:center; gap:8px; }
  .update-row .doc-title { font-size:11px; color:var(--grey); flex:1; line-height:1.3; }
  .badge {
    font-size:9px;
    padding:2px 6px;
    border-radius:4px;
    white-space:nowrap;
    font-weight:600;
  }
  .badge-green { background:#1A3A28; color:#3EAB72; }
  .badge-teal { background:#0F2A35; color:#4ECDC4; }
  .update-date { font-size:10px; color:var(--grey); white-space:nowrap; }

  /* onboarding */
  .panel-onboard {
    background:linear-gradient(155deg,#082818,#0F2030);
    border:1px solid var(--border);
    border-radius:12px;
    padding:20px;
    display:flex;
    flex-direction:column;
  }
  .panel-onboard .sub { font-size:11px; color:var(--grey); margin:0 0 18px; line-height:1.4; }
  .check-list { display:flex; flex-direction:column; gap:12px; flex:1; margin-bottom:20px; }
  .check-row { display:flex; align-items:center; gap:10px; }
  .check-done {
    width:20px; height:20px; border-radius:50%;
    background:var(--green);
    display:flex; align-items:center; justify-content:center;
    font-size:11px; color:#fff; flex-shrink:0;
  }
  .check-empty {
    width:20px; height:20px; border-radius:50%;
    border:1px solid var(--border);
    flex-shrink:0;
  }
  .check-row span { font-size:13px; color:#fff; }
  .check-row .grey { color:var(--grey); }
  .btn-green {
    display:inline-block;
    background:var(--green);
    color:#fff;
    padding:10px 20px;
    border-radius:8px;
    font-size:13px;
    font-weight:600;
  }
  .btn-green:hover { opacity:0.9; }

  /* expert finder */
  .expert-list { display:flex; flex-direction:column; gap:14px; }
  .expert-row { display:flex; align-items:center; gap:10px; }
  .avatar {
    width:38px; height:38px; border-radius:50%;
    background:#1A3A28;
    display:flex; align-items:center; justify-content:center;
    font-size:12px; font-weight:700; color:var(--green); flex-shrink:0;
  }
  .expert-info { flex:1; }
  .expert-info p { font-size:13px; font-weight:600; color:#fff; margin:0; }
  .expert-info span { font-size:11px; color:var(--grey); }
  .btn-outline {
    font-size:11px;
    color:var(--green);
    border:1px solid var(--green);
    border-radius:6px;
    padding:4px 9px;
    white-space:nowrap;
  }
  .btn-outline:hover { background:rgba(62,171,114,0.1); }

  /* ── LOWER ROW ── */
  .lower {
    display:grid;
    grid-template-columns:1fr 1fr 2fr;
    gap:16px;
    padding:0 0 28px;
  }
  .lower-panel {
    background:var(--card);
    border:1px solid var(--border);
    border-radius:12px;
    padding:20px;
    display:flex;
    flex-direction:column;
  }
  .lower-panel .panel-title { margin-bottom:18px; }
  .doc-list { display:flex; flex-direction:column; gap:11px; flex:1; margin-bottom:18px; }
  .doc-row { display:flex; align-items:center; gap:9px; }
  .doc-row .doc-icon { font-size:14px; flex-shrink:0; }
  .doc-row .doc-name { font-size:13px; color:var(--grey); flex:1; }
  .file-badge {
    font-size:10px;
    padding:2px 7px;
    border-radius:4px;
    font-weight:600;
  }
  .word { background:#1A3560; color:#6B9FFF; }
  .excel { background:#1A3A28; color:#3EAB72; }
  .ppt { background:#3A2010; color:#FF8C42; }

  /* insights */
  .insights-grid {
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:12px;
    margin-bottom:16px;
  }
  .insight-card {
    border:1px solid var(--border);
    border-radius:8px;
    padding:14px;
    display:flex;
    flex-direction:column;
  }
  .insight-card.green-grad { background:linear-gradient(155deg,#082818,#0F2030); }
  .insight-card.blue-grad { background:linear-gradient(155deg,#081828,#0F2030); }
  .insight-badge {
    font-size:9px;
    padding:2px 7px;
    border-radius:4px;
    display:inline-block;
    margin-bottom:9px;
    font-weight:600;
    align-self:flex-start;
  }
  .insight-card h4 { font-size:12px; font-weight:600; color:#fff; margin:0 0 7px; line-height:1.4; flex:1; }
  .insight-card p { font-size:11px; color:var(--grey); margin:0 0 12px; line-height:1.4; }
  .insight-card a { font-size:11px; color:var(--green); }
  .insights-footer {
    display:flex;
    justify-content:space-between;
    align-items:center;
  }
  .carousel-btns { display:flex; gap:8px; }
  .carousel-btn {
    background:var(--card);
    border:1px solid var(--border);
    color:#fff;
    width:30px; height:30px;
    border-radius:6px;
    cursor:pointer;
    font-size:13px;
    display:flex; align-items:center; justify-content:center;
  }
  .carousel-btn:hover { border-color:var(--green); }

  /* ── FOOTER ── */
  .footer {
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:22px 0;
    border-top:1px solid var(--border);
    flex-wrap:wrap;
    gap:16px;
  }
  .footer-logo p { font-size:16px; font-weight:600; margin:0 0 5px; }
  .footer-logo p .white { color:#fff; }
  .footer-logo p .green { color:var(--green); }
  .footer-logo small { font-size:12px; color:var(--grey); }
  .footer-links { display:flex; gap:22px; flex-wrap:wrap; }
  .footer-links a { color:var(--grey); font-size:13px; }
  .footer-links a:hover { color:#fff; }
</style>
</head>
<body>
<div class="page">

  <!-- ══ HERO ══ -->
  <div class="hero">

    <div class="hero-left">
      <div class="hero-dots"></div>
      <div class="hero-content">
        <h1>Knowledge Engine</h1>
        <p class="tagline">Find knowledge. Build capability. Deliver value.</p>
        <div class="search-bar">
          <input type="text" placeholder="Search knowledge, guidance, policies, people and more..." />
          <button>Search</button>
        </div>
        <div class="popular">
          <span class="label">Popular searches:</span>
          <span class="pill">NABERS</span>
          <span class="pill">EPC</span>
          <span class="pill">Decarbonisation</span>
          <span class="pill">Risk Management</span>
          <span class="pill">Gateway Reviews</span>
        </div>
      </div>
    </div>

    <div class="hero-right">
      <div class="icon">📚</div>
      <h2>Your knowledge hub</h2>
      <p>Centralised insights, best practice and technical expertise — curated for our people and clients.</p>
      <div class="hub-links">
        <a href="#">About Knowledge Engine &rarr;</a>
        <a href="#">How to contribute &rarr;</a>
      </div>
      <div class="img-placeholder">
        <span>[ Building image ]</span>
      </div>
    </div>

  </div>

  <!-- ══ 6 TILES ══ -->
  <div class="tiles">
    <div class="tile" onclick="window.location='#'">
      <div class="tile-icon">📄</div>
      <p class="tile-title">Technical Guidance</p>
      <p class="tile-sub">Standards, frameworks and how-to guides</p>
      <span class="arrow">&rarr;</span>
    </div>
    <div class="tile" onclick="window.location='#'">
      <div class="tile-icon">📋</div>
      <p class="tile-title">Policies &amp; Procedures</p>
      <p class="tile-sub">Governance, compliance and risk policies</p>
      <span class="arrow">&rarr;</span>
    </div>
    <div class="tile" onclick="window.location='#'">
      <div class="tile-icon">🛠</div>
      <p class="tile-title">Templates &amp; Tools</p>
      <p class="tile-sub">Documents, calculators and checklists</p>
      <span class="arrow">&rarr;</span>
    </div>
    <div class="tile" onclick="window.location='#'">
      <div class="tile-icon">💼</div>
      <p class="tile-title">Case Studies</p>
      <p class="tile-sub">Project insights and lessons learned</p>
      <span class="arrow">&rarr;</span>
    </div>
    <div class="tile" onclick="window.location='#'">
      <div class="tile-icon">🎓</div>
      <p class="tile-title">Lessons Learned</p>
      <p class="tile-sub">Knowledge from experience</p>
      <span class="arrow">&rarr;</span>
    </div>
    <div class="tile" onclick="window.location='#'">
      <div class="tile-icon">👥</div>
      <p class="tile-title">Communities</p>
      <p class="tile-sub">Connect and collaborate across teams</p>
      <span class="arrow">&rarr;</span>
    </div>
  </div>

  <!-- ══ 4 PANELS ══ -->
  <div class="panels">

    <!-- Technical Guidance Library -->
    <div class="panel">
      <p class="panel-title">⚙️ Technical Guidance Library</p>
      <div class="panel-body">
        <div class="guide-list">
          <div class="guide-item">
            <div class="dot"></div>
            <div><p>Sustainability &amp; Net Zero</p><span>Guidance on decarbonisation, net zero strategies and climate resilience.</span></div>
          </div>
          <div class="guide-item">
            <div class="dot"></div>
            <div><p>Building Performance</p><span>NABERS, EPC, energy efficiency and performance improvement.</span></div>
          </div>
          <div class="guide-item">
            <div class="dot"></div>
            <div><p>Environmental Assessment</p><span>EIA, biodiversity, planning and environmental compliance.</span></div>
          </div>
          <div class="guide-item">
            <div class="dot"></div>
            <div><p>Design &amp; Engineering</p><span>Technical design guidance and engineering best practice.</span></div>
          </div>
        </div>
      </div>
      <a href="#" class="view-all">View all guidance &rarr;</a>
    </div>

    <!-- Recently Updated -->
    <div class="panel">
      <p class="panel-title">📄 Recently Updated</p>
      <div class="panel-body">
        <div class="update-list">
          <div class="update-row">
            <span class="doc-title">NABERS UK v1.2 Technical Update</span>
            <span class="badge badge-green">UPDATED</span>
            <span class="update-date">19 May</span>
          </div>
          <div class="update-row">
            <span class="doc-title">EPC Methodology Guide</span>
            <span class="badge badge-green">UPDATED</span>
            <span class="update-date">16 May</span>
          </div>
          <div class="update-row">
            <span class="doc-title">Decarbonisation Pathways Playbook</span>
            <span class="badge badge-green">UPDATED</span>
            <span class="update-date">14 May</span>
          </div>
          <div class="update-row">
            <span class="doc-title">Climate Risk Assessment Template</span>
            <span class="badge badge-teal">NEW</span>
            <span class="update-date">12 May</span>
          </div>
          <div class="update-row">
            <span class="doc-title">Sustainability &amp; Net Zero Standard</span>
            <span class="badge badge-green">UPDATED</span>
            <span class="update-date">9 May</span>
          </div>
        </div>
      </div>
      <a href="#" class="view-all">View all recently updated &rarr;</a>
    </div>

    <!-- Onboarding Journey -->
    <div class="panel-onboard">
      <p class="panel-title">🧭 Onboarding Journey</p>
      <p class="sub">New to Crookes Walker Consulting? Start here.</p>
      <div class="check-list">
        <div class="check-row"><div class="check-done">✓</div><span>Welcome to CWC</span></div>
        <div class="check-row"><div class="check-done">✓</div><span>Our Way of Working</span></div>
        <div class="check-row"><div class="check-empty"></div><span class="grey">Systems &amp; Tools</span></div>
        <div class="check-row"><div class="check-empty"></div><span class="grey">Policies &amp; Essentials</span></div>
      </div>
      <a href="#" class="btn-green">Continue journey &rarr;</a>
    </div>

    <!-- Expert Finder -->
    <div class="panel">
      <p class="panel-title">🔍 Expert Finder</p>
      <div class="panel-body">
        <div class="expert-list">
          <div class="expert-row">
            <div class="avatar">ER</div>
            <div class="expert-info"><p>Emma Richards</p><span>Sustainability &amp; Net Zero</span></div>
            <a href="#" class="btn-outline">View profile</a>
          </div>
          <div class="expert-row">
            <div class="avatar">DM</div>
            <div class="expert-info"><p>Daniel Morgan</p><span>Building Performance</span></div>
            <a href="#" class="btn-outline">View profile</a>
          </div>
          <div class="expert-row">
            <div class="avatar">PS</div>
            <div class="expert-info"><p>Priya Shah</p><span>Environmental Assessment</span></div>
            <a href="#" class="btn-outline">View profile</a>
          </div>
        </div>
      </div>
      <a href="#" class="view-all">View all experts &rarr;</a>
    </div>

  </div>

  <!-- ══ LOWER ROW ══ -->
  <div class="lower">

    <!-- Policies & Compliance -->
    <div class="lower-panel">
      <p class="panel-title">🛡 Policies &amp; Compliance</p>
      <div class="doc-list">
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Risk Management Policy</span></div>
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Health, Safety &amp; Wellbeing Policy</span></div>
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Environmental Policy</span></div>
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Information Security Policy</span></div>
      </div>
      <a href="#" class="view-all">View all policies &rarr;</a>
    </div>

    <!-- Templates & Tools -->
    <div class="lower-panel">
      <p class="panel-title">🔧 Templates &amp; Tools</p>
      <div class="doc-list">
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Project Brief Template</span><span class="file-badge word">WORD</span></div>
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Risk Register</span><span class="file-badge excel">EXCEL</span></div>
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Stakeholder Map</span><span class="file-badge ppt">PPT</span></div>
        <div class="doc-row"><span class="doc-icon">📄</span><span class="doc-name">Site Visit Checklist</span><span class="file-badge excel">EXCEL</span></div>
      </div>
      <a href="#" class="view-all">View all templates &rarr;</a>
    </div>

    <!-- Curated Insights -->
    <div class="lower-panel">
      <p class="panel-title">💡 Curated Insights</p>
      <div class="insights-grid">
        <div class="insight-card green-grad">
          <span class="insight-badge badge-green">INSIGHT</span>
          <h4>NABERS UK: What's new in v1.2 and what it means</h4>
          <p>Key updates, compliance impacts and actions for project teams.</p>
          <a href="#">Read article &rarr;</a>
        </div>
        <div class="insight-card blue-grad">
          <span class="insight-badge badge-teal">GUIDE</span>
          <h4>EPC Reform: Preparing for the Future</h4>
          <p>Understanding upcoming changes and how to stay ahead.</p>
          <a href="#">Read guide &rarr;</a>
        </div>
        <div class="insight-card green-grad">
          <span class="insight-badge badge-green">INSIGHT</span>
          <h4>Decarbonisation Pathways that Deliver</h4>
          <p>Practical strategies for measurable emissions reduction.</p>
          <a href="#">Read article &rarr;</a>
        </div>
      </div>
      <div class="insights-footer">
        <a href="#" class="view-all">View all insights &rarr;</a>
        <div class="carousel-btns">
          <button class="carousel-btn">&#9664;</button>
          <button class="carousel-btn">&#9654;</button>
        </div>
      </div>
    </div>

  </div>

  <!-- ══ FOOTER ══ -->
  <div class="footer">
    <div class="footer-logo">
      <p><span class="white">Crookes Walker</span> <span class="green">Consulting</span></p>
      <small>Building a sustainable and resilient future.</small>
    </div>
    <div class="footer-links">
      <a href="#">About CWC</a>
      <a href="#">Our Services</a>
      <a href="#">Contact</a>
      <a href="#">Support</a>
    </div>
  </div>

</div>
</body>
</html>
