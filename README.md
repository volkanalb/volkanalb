
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Volkan Albayrak — Software Developer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --navy: #0a1628;
      --navy-mid: #112240;
      --gold: #c9a84c;
      --gold-light: #e0c070;
      --cream: #f5f0e8;
      --text: #d4cdc3;
      --text-dim: #8a8478;
      --border: rgba(201,168,76,0.18);
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--navy);
      color: var(--text);
      font-family: 'DM Sans', sans-serif;
      font-weight: 300;
      line-height: 1.7;
      overflow-x: hidden;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.4rem 4rem;
      background: rgba(10,22,40,0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
    }

    .nav-logo {
      font-family: 'Playfair Display', serif;
      font-size: 1.15rem;
      color: var(--gold);
      letter-spacing: 0.04em;
    }

    .nav-links { display: flex; gap: 2.5rem; list-style: none; }
    .nav-links a {
      text-decoration: none;
      color: var(--text-dim);
      font-size: 0.82rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      transition: color 0.3s;
    }
    .nav-links a:hover { color: var(--gold); }

    .lang-toggle {
      display: flex;
      gap: 0.4rem;
    }
    .lang-btn {
      background: none;
      border: 1px solid var(--border);
      color: var(--text-dim);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.75rem;
      letter-spacing: 0.1em;
      padding: 0.3rem 0.7rem;
      cursor: pointer;
      transition: all 0.3s;
      text-transform: uppercase;
    }
    .lang-btn.active, .lang-btn:hover {
      background: var(--gold);
      color: var(--navy);
      border-color: var(--gold);
    }

    /* ── HERO ── */
    #hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      position: relative;
      padding: 8rem 4rem 4rem;
      overflow: hidden;
    }

    .hero-bg {
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 60% 60% at 80% 50%, rgba(201,168,76,0.06) 0%, transparent 70%),
        radial-gradient(ellipse 40% 80% at 10% 80%, rgba(17,34,64,0.8) 0%, transparent 60%);
    }

    .hero-lines {
      position: absolute;
      top: 0; right: 0;
      width: 45%;
      height: 100%;
      opacity: 0.06;
      background-image: repeating-linear-gradient(
        90deg,
        var(--gold) 0px,
        var(--gold) 1px,
        transparent 1px,
        transparent 60px
      );
    }

    .hero-content {
      position: relative;
      z-index: 2;
      max-width: 780px;
    }

    .hero-eyebrow {
      font-size: 0.75rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--gold);
      margin-bottom: 1.5rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.2s forwards;
    }

    .hero-name {
      font-family: 'Playfair Display', serif;
      font-size: clamp(3rem, 6vw, 5.5rem);
      line-height: 1.1;
      color: var(--cream);
      margin-bottom: 1.2rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.4s forwards;
    }

    .hero-name span { color: var(--gold); }

    .hero-title {
      font-size: 1.05rem;
      color: var(--text-dim);
      letter-spacing: 0.06em;
      margin-bottom: 2rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.6s forwards;
    }

    .hero-desc {
      font-size: 1.05rem;
      color: var(--text);
      max-width: 560px;
      line-height: 1.85;
      margin-bottom: 3rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.8s forwards;
    }

    .hero-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 0.6rem;
      margin-bottom: 3rem;
      opacity: 0;
      animation: fadeUp 0.8s 1s forwards;
    }

    .tag {
      font-size: 0.72rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 0.4rem 1rem;
      border: 1px solid var(--border);
      color: var(--text-dim);
      transition: all 0.3s;
    }
    .tag:hover { border-color: var(--gold); color: var(--gold); }

    .tag-highlight {
      border-color: var(--gold);
      color: var(--gold);
      background: rgba(201,168,76,0.07);
      font-weight: 500;
    }

    /* ── FIX BANNER ── */
    .fix-banner {
      display: flex;
      align-items: center;
      gap: 1rem;
      margin-bottom: 2.5rem;
      padding: 1rem 1.5rem;
      border: 1px solid var(--gold);
      background: rgba(201,168,76,0.05);
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.8s 0.9s forwards;
    }

    .fix-pulse {
      width: 10px;
      height: 10px;
      border-radius: 50%;
      background: var(--gold);
      flex-shrink: 0;
      box-shadow: 0 0 0 0 rgba(201,168,76,0.6);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%   { box-shadow: 0 0 0 0 rgba(201,168,76,0.6); }
      70%  { box-shadow: 0 0 0 10px rgba(201,168,76,0); }
      100% { box-shadow: 0 0 0 0 rgba(201,168,76,0); }
    }

    .fix-label {
      font-size: 0.82rem;
      font-weight: 500;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--gold);
    }

    .fix-sub {
      font-size: 0.75rem;
      color: var(--text-dim);
      letter-spacing: 0.05em;
    }

    /* ── EXPERTISE SECTION ── */
    #expertise {
      padding: 7rem 4rem;
      border-top: 1px solid var(--border);
    }

    .expertise-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 1.5rem;
      max-width: 1000px;
      margin-top: 3rem;
    }

    .expertise-card {
      border: 1px solid var(--border);
      padding: 2rem;
      background: rgba(17,34,64,0.3);
      transition: border-color 0.3s, transform 0.3s;
      position: relative;
      overflow: hidden;
    }

    .expertise-card.featured {
      border-color: var(--gold);
      background: rgba(201,168,76,0.04);
    }

    .expertise-card.featured::before {
      content: '★ Core Specialty';
      position: absolute;
      top: 0; right: 0;
      background: var(--gold);
      color: var(--navy);
      font-size: 0.62rem;
      font-weight: 500;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      padding: 0.3rem 0.8rem;
    }

    .expertise-card.featured[data-lang="tr"]::before {
      content: '★ Ana Uzmanlık';
    }

    .expertise-card:hover {
      border-color: rgba(201,168,76,0.5);
      transform: translateY(-3px);
    }

    .expertise-card-title {
      font-family: 'Playfair Display', serif;
      font-size: 1.1rem;
      color: var(--cream);
      margin-bottom: 0.8rem;
    }

    .expertise-card.featured .expertise-card-title {
      color: var(--gold);
    }

    .expertise-card-desc {
      font-size: 0.88rem;
      color: var(--text-dim);
      line-height: 1.7;
      margin-bottom: 1.2rem;
    }

    .expertise-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 0.4rem;
    }

    .expertise-tag {
      font-size: 0.65rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      padding: 0.25rem 0.6rem;
      border: 1px solid var(--border);
      color: var(--text-dim);
    }

    .expertise-card.featured .expertise-tag {
      border-color: rgba(201,168,76,0.35);
      color: var(--gold-light);
    }

    /* ── PROJECTS SECTION ── */
    #projects {
      padding: 7rem 4rem;
      border-top: 1px solid var(--border);
    }

    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(340px, 1fr));
      gap: 1.5rem;
      max-width: 1000px;
      margin-top: 3rem;
    }

    .project-card {
      border: 1px solid var(--border);
      padding: 2.2rem;
      background: rgba(17,34,64,0.3);
      transition: border-color 0.3s, transform 0.3s;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .project-card:hover {
      border-color: var(--gold);
      transform: translateY(-4px);
      background: rgba(201,168,76,0.03);
    }

    .project-card-top {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
    }

    .project-badge {
      font-size: 0.62rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      padding: 0.25rem 0.7rem;
      border: 1px solid rgba(201,168,76,0.4);
      color: var(--gold);
    }

    .project-title {
      font-family: 'Playfair Display', serif;
      font-size: 1.15rem;
      color: var(--cream);
      font-weight: 400;
    }

    .project-desc {
      font-size: 0.88rem;
      color: var(--text-dim);
      line-height: 1.75;
    }

    .project-tech {
      display: flex;
      flex-wrap: wrap;
      gap: 0.4rem;
    }

    .project-tech-tag {
      font-size: 0.65rem;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      padding: 0.25rem 0.6rem;
      border: 1px solid var(--border);
      color: var(--text-dim);
    }

    .project-footer {
      margin-top: auto;
      padding-top: 1rem;
      border-top: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .project-gh-link {
      font-size: 0.75rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--gold);
      text-decoration: none;
      display: flex;
      align-items: center;
      gap: 0.5rem;
      transition: gap 0.3s;
    }

    .project-gh-link:hover { gap: 0.8rem; }

    .project-gh-placeholder {
      font-size: 0.72rem;
      color: var(--text-dim);
      font-style: italic;
    }

    .hero-cta {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.8s 1.2s forwards;
    }

    .btn-primary {
      display: inline-block;
      padding: 0.9rem 2.4rem;
      background: var(--gold);
      color: var(--navy);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.8rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      text-decoration: none;
      transition: all 0.3s;
    }
    .btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); }

    .btn-outline {
      display: inline-block;
      padding: 0.9rem 2.4rem;
      border: 1px solid var(--gold);
      color: var(--gold);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.8rem;
      font-weight: 400;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      text-decoration: none;
      transition: all 0.3s;
    }
    .btn-outline:hover { background: rgba(201,168,76,0.1); transform: translateY(-2px); }

    /* ── EXPERIENCE STRIP ── */
    .exp-strip {
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      padding: 2rem 4rem;
      display: flex;
      gap: 4rem;
      flex-wrap: wrap;
      opacity: 0;
      animation: fadeUp 0.8s 1.4s forwards;
    }

    .exp-item { }
    .exp-num {
      font-family: 'Playfair Display', serif;
      font-size: 2rem;
      color: var(--gold);
      line-height: 1;
    }
    .exp-label {
      font-size: 0.72rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--text-dim);
      margin-top: 0.3rem;
    }

    /* ── CONTACT ── */
    #contact {
      padding: 8rem 4rem;
      position: relative;
    }

    .section-label {
      font-size: 0.72rem;
      letter-spacing: 0.25em;
      text-transform: uppercase;
      color: var(--gold);
      margin-bottom: 1rem;
    }

    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: clamp(2rem, 4vw, 3.2rem);
      color: var(--cream);
      margin-bottom: 1rem;
      line-height: 1.2;
    }

    .section-sub {
      color: var(--text-dim);
      font-size: 1rem;
      max-width: 480px;
      margin-bottom: 4rem;
    }

    .contact-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 1.5rem;
      max-width: 860px;
    }

    .contact-card {
      border: 1px solid var(--border);
      padding: 2rem;
      position: relative;
      transition: border-color 0.3s, transform 0.3s;
      text-decoration: none;
      display: block;
      background: rgba(17,34,64,0.3);
    }
    .contact-card:hover {
      border-color: var(--gold);
      transform: translateY(-4px);
      background: rgba(201,168,76,0.04);
    }

    .contact-card-icon {
      font-size: 1.5rem;
      margin-bottom: 1rem;
      color: var(--gold);
    }

    .contact-card-label {
      font-size: 0.7rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--text-dim);
      margin-bottom: 0.4rem;
    }

    .contact-card-value {
      font-size: 0.95rem;
      color: var(--cream);
    }

    /* ── FOOTER ── */
    footer {
      border-top: 1px solid var(--border);
      padding: 2rem 4rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
    }

    .footer-copy {
      font-size: 0.75rem;
      color: var(--text-dim);
      letter-spacing: 0.06em;
    }

    .footer-logo {
      font-family: 'Playfair Display', serif;
      color: var(--gold);
      font-size: 1rem;
    }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 768px) {
      nav { padding: 1.2rem 1.5rem; }
      .nav-links { display: none; }
      #hero, #contact, #expertise, #projects { padding: 7rem 1.5rem 3rem; }
      .exp-strip { padding: 2rem 1.5rem; gap: 2rem; }
      footer { padding: 1.5rem; }
    }

    /* ── SCROLL LINE ── */
    .scroll-hint {
      position: absolute;
      bottom: 3rem;
      left: 4rem;
      display: flex;
      align-items: center;
      gap: 0.8rem;
      font-size: 0.68rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--text-dim);
      opacity: 0;
      animation: fadeUp 0.8s 1.6s forwards;
    }
    .scroll-hint::before {
      content: '';
      width: 40px;
      height: 1px;
      background: var(--gold);
    }

    /* i18n hidden */
    [data-lang] { display: none; }
    body.lang-en [data-lang="en"],
    body.lang-tr [data-lang="tr"] { display: revert; }
  </style>
</head>
<body class="lang-en">

<!-- NAV -->
<nav>
  <div class="nav-logo">VA</div>
  <ul class="nav-links">
    <li><a href="#hero" data-lang="en">About</a><a href="#hero" data-lang="tr">Hakkımda</a></li>
    <li><a href="#expertise" data-lang="en">Expertise</a><a href="#expertise" data-lang="tr">Uzmanlık</a></li>
    <li><a href="#projects" data-lang="en">Projects</a><a href="#projects" data-lang="tr">Projeler</a></li>
    <li><a href="#contact" data-lang="en">Contact</a><a href="#contact" data-lang="tr">İletişim</a></li>
  </ul>
  <div class="lang-toggle">
    <button class="lang-btn active" onclick="setLang('en')">EN</button>
    <button class="lang-btn" onclick="setLang('tr')">TR</button>
  </div>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-bg"></div>
  <div class="hero-lines"></div>

  <div class="hero-content">
    <p class="hero-eyebrow" data-lang="en">Treasury Software Engineering</p>
    <p class="hero-eyebrow" data-lang="tr">Hazine Yazılım Mühendisliği</p>

    <h1 class="hero-name">Volkan <span>Albayrak</span></h1>

    <p class="hero-title" data-lang="en">Senior Software Developer &amp; Team Leader</p>
    <p class="hero-title" data-lang="tr">Kıdemli Yazılım Geliştirici &amp; Takım Lideri</p>

    <p class="hero-desc" data-lang="en">
      13+ years of experience building mission-critical financial software for Turkey's leading banks.
      Specialised in treasury systems, Murex integration, and Java/Spring Boot backend development.
      Currently leading the Treasury Applications Team at Şekerbank.
    </p>
    <p class="hero-desc" data-lang="tr">
      Türkiye'nin önde gelen bankalarında hazine yazılımları geliştirme alanında 13+ yıl deneyim.
      Treasury sistemleri, Murex entegrasyonu ve Java/Spring Boot backend geliştirme konularında uzmanlaşmış.
      Şu anda Şekerbank Treasury Uygulamaları Takımı'nı yönetmektedir.
    </p>

    <div class="fix-banner" data-lang="en">
      <span class="fix-pulse"></span>
      <span class="fix-label">FIX Protocol Specialist</span>
      <span class="fix-sub">QuickFIX/J · Bloomberg · 360T · Reuters · TradeTools · SmartTrade · Spring Boot Gateway</span>
    </div>
    <div class="fix-banner" data-lang="tr">
      <span class="fix-pulse"></span>
      <span class="fix-label">FIX Protocol Uzmanı</span>
      <span class="fix-sub">QuickFIX/J · Bloomberg · 360T · Reuters · TradeTools · SmartTrade · Spring Boot Gateway</span>
    </div>

    <div class="hero-tags">
      <span class="tag tag-highlight">FIX Protocol</span>
      <span class="tag tag-highlight">QuickFIX/J</span>
      <span class="tag">Java &amp; Spring Boot</span>
      <span class="tag">Murex</span>
      <span class="tag">React</span>
      <span class="tag">SQL Tuning</span>
      <span class="tag">PLSQL</span>
    </div>

    <div class="hero-cta">
      <a href="#contact" class="btn-primary" data-lang="en">Get in Touch</a>
      <a href="#contact" class="btn-primary" data-lang="tr">İletişime Geç</a>
      <a href="https://www.linkedin.com/in/volkanalb" target="_blank" class="btn-outline">LinkedIn</a>
    </div>
  </div>

  <div class="scroll-hint" data-lang="en">Scroll</div>
  <div class="scroll-hint" data-lang="tr">Kaydır</div>
</section>

<!-- EXPERIENCE STRIP -->
<div class="exp-strip">
  <div class="exp-item">
    <div class="exp-num">13+</div>
    <div class="exp-label" data-lang="en">Years Experience</div>
    <div class="exp-label" data-lang="tr">Yıl Deneyim</div>
  </div>
  <div class="exp-item">
    <div class="exp-num">3</div>
    <div class="exp-label" data-lang="en">Major Banks</div>
    <div class="exp-label" data-lang="tr">Büyük Banka</div>
  </div>
  <div class="exp-item">
    <div class="exp-num">20+</div>
    <div class="exp-label" data-lang="en">Projects Delivered</div>
    <div class="exp-label" data-lang="tr">Tamamlanan Proje</div>
  </div>
  <div class="exp-item">
    <div class="exp-num">9</div>
    <div class="exp-label" data-lang="en">Key Competencies</div>
    <div class="exp-label" data-lang="tr">Temel Yetkinlik</div>
  </div>
</div>

<!-- EXPERTISE -->
<section id="expertise">
  <p class="section-label" data-lang="en">What I Do Best</p>
  <p class="section-label" data-lang="tr">Uzmanlık Alanlarım</p>

  <h2 class="section-title" data-lang="en">Core Expertise</h2>
  <h2 class="section-title" data-lang="tr">Temel Uzmanlıklar</h2>

  <div class="expertise-grid">

    <!-- FIX Protocol — FEATURED -->
    <div class="expertise-card featured" data-lang="en">
      <div class="expertise-card-title">FIX Protocol &amp; Trading Connectivity</div>
      <div class="expertise-card-desc">
        Deep expertise in FIX Protocol (4.2–4.4-5.0) and QuickFIX/J. Designed and led the development
        of Spring Boot-based FIX gateways connecting banks to major trading platforms including
        Bloomberg, 360T and Reuters — handling real-time order routing, execution reports and
        market data streams in high-availability production environments.
      </div>
      <div class="expertise-tags">
        <span class="expertise-tag">FIX 4.2 / 4.4 / 5.0</span>
        <span class="expertise-tag">QuickFIX/J</span>
        <span class="expertise-tag">Spring Boot</span>
        <span class="expertise-tag">Bloomberg</span>
        <span class="expertise-tag">360T</span>
        <span class="expertise-tag">Reuters</span>
      </div>
    </div>
    <div class="expertise-card featured" data-lang="tr">
      <div class="expertise-card-title">FIX Protocol &amp; Trading Bağlantısı</div>
      <div class="expertise-card-desc">
        FIX Protocol (4.2–4.4-5.0) ve QuickFIX/J konularında derin uzmanlık. Bloomberg, 360T ve Reuters
        gibi büyük işlem platformlarına banka bağlantısı sağlayan Spring Boot tabanlı FIX gateway'lerin
        tasarımını ve geliştirme liderliğini üstlendi — gerçek zamanlı emir yönlendirme, işlem raporları
        ve piyasa verisi akışlarını yüksek erişilebilirlik ortamında yönetiyor.
      </div>
      <div class="expertise-tags">
        <span class="expertise-tag">FIX 4.2 / 4.4 / 5.0</span>
        <span class="expertise-tag">QuickFIX/J</span>
        <span class="expertise-tag">Spring Boot</span>
        <span class="expertise-tag">Bloomberg</span>
        <span class="expertise-tag">360T</span>
        <span class="expertise-tag">Reuters</span>
      </div>
    </div>

    <!-- Murex -->
    <div class="expertise-card" data-lang="en">
      <div class="expertise-card-title">Murex Integration &amp; Architecture</div>
      <div class="expertise-card-desc">
        10+ years working with Murex across workflow design, Datamart reporting, environment
        management and multiple major version upgrades (v26→v31→v34→v40). Specialist in
        EOD/EOM automation, performance tuning and production support.
      </div>
      <div class="expertise-tags">
        <span class="expertise-tag">Murex Workflow</span>
        <span class="expertise-tag">Datamart</span>
        <span class="expertise-tag">MxML</span>
        <span class="expertise-tag">EOD Automation</span>
        <span class="expertise-tag">SQL Tuning</span>
      </div>
    </div>
    <div class="expertise-card" data-lang="tr">
      <div class="expertise-card-title">Murex Entegrasyonu &amp; Mimarisi</div>
      <div class="expertise-card-desc">
        Workflow tasarımı, Datamart raporlama, ortam yönetimi ve birden fazla büyük versiyon yükseltmesi
        (v26→v31→v34→v40) dahil olmak üzere Murex ile 10+ yıl deneyim. EOD/EOM otomasyonu, performans
        iyileştirme ve production destek konularında uzman.
      </div>
      <div class="expertise-tags">
        <span class="expertise-tag">Murex Workflow</span>
        <span class="expertise-tag">Datamart</span>
        <span class="expertise-tag">MxML</span>
        <span class="expertise-tag">EOD Otomasyonu</span>
        <span class="expertise-tag">SQL Tuning</span>
      </div>
    </div>

    <!-- Java Backend -->
    <div class="expertise-card" data-lang="en">
      <div class="expertise-card-title">Java Backend &amp; Treasury Systems</div>
      <div class="expertise-card-desc">
        End-to-end Java/Spring Boot development for treasury products: core banking integrations,
        market data pipelines, FX/commodity transaction flows, batch processes and SWIFT/EFT messaging.
        Led multiple transformation projects converting legacy PLSQL to Java.
      </div>
      <div class="expertise-tags">
        <span class="expertise-tag">Java</span>
        <span class="expertise-tag">Spring Boot</span>
        <span class="expertise-tag">PLSQL</span>
        <span class="expertise-tag">Oracle</span>
        <span class="expertise-tag">React</span>
      </div>
    </div>
    <div class="expertise-card" data-lang="tr">
      <div class="expertise-card-title">Java Backend &amp; Treasury Sistemleri</div>
      <div class="expertise-card-desc">
        Treasury ürünleri için uçtan uca Java/Spring Boot geliştirme: core banking entegrasyonları,
        piyasa verisi pipeline'ları, FX/emtia işlem akışları, batch süreçler ve SWIFT/EFT mesajlaşma.
        Legacy PLSQL'i Java'ya dönüştüren birden fazla dönüşüm projesine liderlik etti.
      </div>
      <div class="expertise-tags">
        <span class="expertise-tag">Java</span>
        <span class="expertise-tag">Spring Boot</span>
        <span class="expertise-tag">PLSQL</span>
        <span class="expertise-tag">Oracle</span>
        <span class="expertise-tag">React</span>
      </div>
    </div>

  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <p class="section-label" data-lang="en">Open Source</p>
  <p class="section-label" data-lang="tr">Açık Kaynak</p>

  <h2 class="section-title" data-lang="en">Featured Project</h2>
  <h2 class="section-title" data-lang="tr">Öne Çıkan Proje</h2>

  <div class="projects-grid">
    <div class="project-card" data-lang="en">
      <div class="project-card-top">
        <span class="project-badge">Open Source</span>
      </div>
      <div class="project-title">fix-protocol-gateway</div>
      <div class="project-desc">
        A production-grade FIX Protocol gateway built with Spring Boot and QuickFIX/J.
        Establishes and manages FIX sessions to trading platforms, handles real-time
        order routing, execution reports and market data — then forwards captured data
        to downstream systems such as Murex. Designed for high-availability banking environments.
      </div>
      <div class="project-tech">
        <span class="project-tech-tag">Java</span>
        <span class="project-tech-tag">Spring Boot</span>
        <span class="project-tech-tag">QuickFIX/J</span>
        <span class="project-tech-tag">FIX Protocol</span>
        <span class="project-tech-tag">Murex</span>
      </div>
      <div class="project-footer">
        <span class="project-gh-placeholder">GitHub link coming soon</span>
      </div>
    </div>
    <div class="project-card" data-lang="tr">
      <div class="project-card-top">
        <span class="project-badge">Açık Kaynak</span>
      </div>
      <div class="project-title">fix-protocol-gateway</div>
      <div class="project-desc">
        Spring Boot ve QuickFIX/J ile geliştirilmiş production kalitesinde bir FIX Protocol gateway.
        İşlem platformlarıyla FIX oturumlarını kurar ve yönetir; gerçek zamanlı emir yönlendirme,
        işlem raporları ve piyasa verilerini işleyerek Murex gibi downstream sistemlere iletir.
        Yüksek erişilebilirlik gerektiren bankacılık ortamları için tasarlanmıştır.
      </div>
      <div class="project-tech">
        <span class="project-tech-tag">Java</span>
        <span class="project-tech-tag">Spring Boot</span>
        <span class="project-tech-tag">QuickFIX/J</span>
        <span class="project-tech-tag">FIX Protocol</span>
        <span class="project-tech-tag">Murex</span>
      </div>
      <div class="project-footer">
        <span class="project-gh-placeholder">GitHub linki yakında eklenecek</span>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <p class="section-label" data-lang="en">Get in Touch</p>
  <p class="section-label" data-lang="tr">İletişim</p>

  <h2 class="section-title" data-lang="en">Let's work together</h2>
  <h2 class="section-title" data-lang="tr">Birlikte çalışalım</h2>

  <div class="contact-grid">
    <a class="contact-card" href="mailto:volkanalb@gmail.com">
      <div class="contact-card-icon">✉</div>
      <div class="contact-card-label" data-lang="en">Email</div>
      <div class="contact-card-label" data-lang="tr">E-posta</div>
      <div class="contact-card-value">volkanalb@gmail.com</div>
    </a>
    <a class="contact-card" href="tel:+905546784313">
      <div class="contact-card-icon">☎</div>
      <div class="contact-card-label" data-lang="en">Phone</div>
      <div class="contact-card-label" data-lang="tr">Telefon</div>
      <div class="contact-card-value">+90 (554) 678 4313</div>
    </a>
    <a class="contact-card" href="https://www.linkedin.com/in/volkanalb" target="_blank">
      <div class="contact-card-icon">in</div>
      <div class="contact-card-label">LinkedIn</div>
      <div class="contact-card-value">linkedin.com/in/volkanalb</div>
    </a>
    <div class="contact-card" style="cursor:default;">
      <div class="contact-card-icon">⌖</div>
      <div class="contact-card-label" data-lang="en">Location</div>
      <div class="contact-card-label" data-lang="tr">Konum</div>
      <div class="contact-card-value">Ankara, Türkiye</div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span class="footer-logo">Volkan Albayrak</span>
  <span class="footer-copy" data-lang="en">© 2025 — Treasury Software Engineering</span>
  <span class="footer-copy" data-lang="tr">© 2025 — Hazine Yazılım Mühendisliği</span>
</footer>

<script>
  function setLang(lang) {
    document.body.className = 'lang-' + lang;
    document.querySelectorAll('.lang-btn').forEach(b => {
      b.classList.toggle('active', b.textContent === lang.toUpperCase());
    });
  }
</script>
</body>
</html>
