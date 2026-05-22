<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mehul Jambukiya — Unity Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;500;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>

  :root {
    --bg: #050a0f;
    --bg2: #080f18;
    --panel: #0a1520;
    --border: #0f2a40;
    --accent: #00e5ff;
    --accent2: #ff6b35;
    --accent3: #7fff00;
    --text: #c8e6f0;
    --muted: #4a7a96;
    --glow: 0 0 20px rgba(0,229,255,0.4);
    --glow2: 0 0 20px rgba(255,107,53,0.4);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Rajdhani', sans-serif;
    font-size: 16px;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom Cursor */
  .cursor {
    position: fixed;
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s;
    box-shadow: 0 0 10px var(--accent), 0 0 20px var(--accent);
  }
  .cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid rgba(0,229,255,0.5);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s, width 0.2s, height 0.2s;
  }
  .hero-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
  position: relative;
  z-index: 2;
  width: 100%;
}


@media (max-width: 1000px) {
  .hero-container {
    flex-direction: column-reverse;
    text-align: center;
  }

  .hero-content {
    max-width: 100%;
  }

  .hero-desc {
    margin-inline: auto;
  }

  .hero-stats,
  .hero-buttons {
    justify-content: center;
  }

  .hero-image {
    width: 300px;
  }

  .hero-image img {
    height: 400px;
  }
}

@media (max-width: 600px) {
  .hero-image {
    width: 240px;
  }

  .hero-image img {
    height: 320px;
  }
}

  /* Scanlines overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.08) 2px, rgba(0,0,0,0.08) 4px);
    pointer-events: none;
    z-index: 100;
  }

  /* Noise texture */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 99;
    opacity: 0.4;
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 50;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 18px 48px;
    background: linear-gradient(180deg, rgba(5,10,15,0.95) 0%, transparent 100%);
    border-bottom: 1px solid rgba(0,229,255,0.1);
  }
  .nav-logo {
    font-family: 'Orbitron', monospace;
    font-size: 14px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 3px;
    text-transform: uppercase;
  }
  .nav-links { display: flex; gap: 32px; list-style: none; }
  .nav-links a {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 2px;
    text-transform: uppercase;
    transition: color 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0; right: 0;
    height: 1px;
    background: var(--accent);
    transform: scaleX(0);
    transition: transform 0.3s;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { transform: scaleX(1); }

  /* HERO */
  #hero {
    min-height: 100vh;
    display: flex;
    align-items: center;
    position: relative;
    padding: 120px 48px 80px;
    overflow: hidden;
  }

  /* Animated grid background */
  .grid-bg {
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,229,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridMove 20s linear infinite;
  }
  @keyframes gridMove {
    0% { background-position: 0 0; }
    100% { background-position: 60px 60px; }
  }

  /* Floating geometric shapes */
  .shape {
    position: absolute;
    border: 1px solid;
    opacity: 0.15;
    animation: float 8s ease-in-out infinite;
  }
  .shape-1 { width: 120px; height: 120px; top: 15%; right: 15%; border-color: var(--accent); transform: rotate(45deg); animation-delay: 0s; }
  .shape-2 { width: 60px; height: 60px; top: 60%; right: 25%; border-color: var(--accent2); border-radius: 50%; animation-delay: 2s; }
  .shape-3 { width: 200px; height: 200px; top: 30%; right: 8%; border-color: var(--accent3); opacity: 0.06; animation-delay: 4s; }
  .shape-4 { width: 40px; height: 40px; bottom: 20%; right: 35%; border-color: var(--accent); animation-delay: 1s; }

  @keyframes float {
    0%, 100% { transform: translateY(0) rotate(0deg); }
    50% { transform: translateY(-20px) rotate(10deg); }
  }

  .hero-content { position: relative; z-index: 2; max-width: 700px; }

  .hero-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .hero-tag::before {
    content: '';
    display: inline-block;
    width: 32px; height: 1px;
    background: var(--accent);
  }

  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(40px, 7vw, 80px);
    font-weight: 900;
    line-height: 1;
    letter-spacing: -1px;
    margin-bottom: 12px;
    background: linear-gradient(135deg, #ffffff 0%, var(--accent) 50%, #ffffff 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: shimmer 4s ease-in-out infinite;
    background-size: 200% auto;
  }
  @keyframes shimmer {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }

  .hero-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(14px, 2vw, 18px);
    font-weight: 400;
    color: var(--accent2);
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 28px;
  }

  .hero-desc {
    font-size: 17px;
    font-weight: 300;
    line-height: 1.7;
    color: rgba(200,230,240,0.7);
    max-width: 520px;
    margin-bottom: 40px;
  }

  .hero-stats {
    display: flex;
    gap: 40px;
    margin-bottom: 48px;
    flex-wrap: wrap;
  }
  .stat-item { text-align: center; }
  .stat-num {
    font-family: 'Orbitron', monospace;
    font-size: 28px;
    font-weight: 700;
    color: var(--accent);
    display: block;
  }
  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  .hero-buttons { display: flex; gap: 16px; flex-wrap: wrap; }

  .btn {
    font-family: 'Orbitron', monospace;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 14px 32px;
    border: none;
    cursor: pointer;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .btn-primary {
    background: var(--accent);
    color: #000;
    clip-path: polygon(12px 0%, 100% 0%, calc(100% - 12px) 100%, 0% 100%);
  }
  .btn-primary:hover {
    background: #fff;
    box-shadow: var(--glow);
    transform: translateY(-2px);
  }
  .btn-outline {
    background: transparent;
    color: var(--accent);
    border: 1px solid var(--accent);
    clip-path: polygon(12px 0%, 100% 0%, calc(100% - 12px) 100%, 0% 100%);
  }
  .btn-outline:hover {
    background: rgba(0,229,255,0.1);
    box-shadow: var(--glow);
    transform: translateY(-2px);
  }

  /* SECTIONS */
  section { padding: 100px 48px; position: relative; }

  .section-header {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 64px;
  }
  .section-num {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    opacity: 0.6;
    letter-spacing: 2px;
  }
  .section-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(22px, 3vw, 32px);
    font-weight: 700;
    color: #fff;
    letter-spacing: 2px;
    text-transform: uppercase;
  }
  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
  }

  /* ABOUT */
  #about { background: var(--bg2); }
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: start;
  }
  .about-text p {
    font-size: 16px;
    line-height: 1.8;
    color: rgba(200,230,240,0.75);
    margin-bottom: 20px;
  }
  .about-text p strong { color: var(--accent); font-weight: 600; }

  .info-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-top: 32px; }
  .info-item {
    background: var(--panel);
    border: 1px solid var(--border);
    padding: 16px 20px;
    position: relative;
    overflow: hidden;
  }
  .info-item::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 3px; height: 100%;
    background: var(--accent);
  }
  .info-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 9px;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 4px;
  }
  .info-value {
    font-family: 'Rajdhani', sans-serif;
    font-size: 14px;
    font-weight: 600;
    color: var(--text);
  }

  /* Contact panel in about */
  .contact-panel {
    background: var(--panel);
    border: 1px solid var(--border);
    padding: 32px;
    position: relative;
  }
  .contact-panel::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }
  .contact-title {
    font-family: 'Orbitron', monospace;
    font-size: 13px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 28px;
  }
  .contact-item {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 14px 0;
    border-bottom: 1px solid var(--border);
  }
  .contact-item:last-child { border-bottom: none; }
  .contact-icon {
    width: 36px; height: 36px;
    background: rgba(0,229,255,0.1);
    border: 1px solid rgba(0,229,255,0.2);
    display: flex; align-items: center; justify-content: center;
    font-size: 14px;
    flex-shrink: 0;
  }
  .contact-info-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 9px;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
  }
  .contact-info-val {
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
    margin-top: 2px;
  }

  /* SKILLS */
  #skills { background: var(--bg); }
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
  }
  .skill-card {
    background: var(--panel);
    border: 1px solid var(--border);
    padding: 28px;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
  }
  .skill-card:hover {
    transform: translateY(-4px);
    border-color: rgba(0,229,255,0.4);
  }
  .skill-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(0,229,255,0.05) 0%, transparent 60%);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .skill-card:hover::after { opacity: 1; }

  .skill-card-icon {
    font-size: 28px;
    margin-bottom: 16px;
    display: block;
  }
  .skill-card-title {
    font-family: 'Orbitron', monospace;
    font-size: 12px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 16px;
  }
  .skill-tags { display: flex; flex-wrap: wrap; gap: 8px; }
  .tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    padding: 4px 10px;
    border: 1px solid;
    letter-spacing: 1px;
    text-transform: uppercase;
  }
  .tag-cyan { border-color: rgba(0,229,255,0.4); color: var(--accent); background: rgba(0,229,255,0.05); }
  .tag-orange { border-color: rgba(255,107,53,0.4); color: var(--accent2); background: rgba(255,107,53,0.05); }
  .tag-green { border-color: rgba(127,255,0,0.4); color: var(--accent3); background: rgba(127,255,0,0.05); }

  /* Skill bars */
  .skill-bar-list { margin-top: 16px; }
  .skill-bar-item { margin-bottom: 14px; }
  .skill-bar-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 6px;
  }
  .skill-bar-name {
    font-family: 'Rajdhani', sans-serif;
    font-size: 13px;
    font-weight: 600;
    color: var(--text);
    letter-spacing: 1px;
  }
  .skill-bar-pct {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--accent);
  }
  .skill-bar-track {
    height: 4px;
    background: rgba(255,255,255,0.05);
    border: 1px solid var(--border);
    position: relative;
    overflow: hidden;
  }
  .skill-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    position: relative;
    animation: barFill 1.5s ease-out forwards;
    transform-origin: left;
  }
  @keyframes barFill {
    from { transform: scaleX(0); }
    to { transform: scaleX(1); }
  }

  /* PROJECT PLACEHOLDER */
  #projects { background: var(--bg2); }
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 28px;
  }
  .project-card {
    background: var(--panel);
    border: 1px solid var(--border);
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s;
  }
  .project-card:hover {
    transform: translateY(-6px);
    border-color: rgba(0,229,255,0.4);
    box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 30px rgba(0,229,255,0.1);
  }

  .project-img {
    height: 200px;
    position: relative;
    overflow: hidden;
    background: linear-gradient(135deg, #0a1a28 0%, #0f2540 100%);
    display: flex; align-items: center; justify-content: center;
  }
  .project-img-text {
    font-family: 'Orbitron', monospace;
    font-size: 40px;
    font-weight: 900;
    color: rgba(0,229,255,0.08);
    letter-spacing: 4px;
    text-transform: uppercase;
    user-select: none;
    position: relative;
    z-index: 1;
  }
  .project-img::before {
    content: '';
    position: absolute;
    inset: 0;
    background-image: 
      linear-gradient(rgba(0,229,255,0.06) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.06) 1px, transparent 1px);
    background-size: 30px 30px;
  }

  .project-badge {
    position: absolute;
    top: 16px; right: 16px;
    font-family: 'Share Tech Mono', monospace;
    font-size: 9px;
    padding: 4px 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
  }
  .badge-live { background: rgba(127,255,0,0.15); border: 1px solid var(--accent3); color: var(--accent3); }
  .badge-wip { background: rgba(255,107,53,0.15); border: 1px solid var(--accent2); color: var(--accent2); }
  .badge-fresher { background: rgba(0,229,255,0.15); border: 1px solid var(--accent); color: var(--accent); }

  .project-body { padding: 24px; }
  .project-name {
    font-family: 'Orbitron', monospace;
    font-size: 15px;
    font-weight: 700;
    color: #fff;
    letter-spacing: 1px;
    margin-bottom: 8px;
  }
  .project-desc {
    font-size: 14px;
    line-height: 1.65;
    color: rgba(200,230,240,0.65);
    margin-bottom: 20px;
  }
  .project-tech { display: flex; flex-wrap: wrap; gap: 6px; }

  /* Coming soon card */
  .coming-soon {
    background: var(--panel);
    border: 1px dashed var(--border);
    display: flex; align-items: center; justify-content: center;
    min-height: 360px;
    text-align: center;
    flex-direction: column;
    gap: 16px;
    padding: 32px;
    transition: border-color 0.3s;
  }
  .coming-soon:hover { border-color: rgba(255,107,53,0.4); }
  .coming-soon-icon { font-size: 48px; opacity: 0.3; }
  .coming-soon-text {
    font-family: 'Orbitron', monospace;
    font-size: 13px;
    font-weight: 700;
    color: var(--muted);
    letter-spacing: 3px;
    text-transform: uppercase;
  }
  .coming-soon-sub {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: rgba(74,122,150,0.6);
    letter-spacing: 1px;
  }

  /* EDUCATION */
  #education { background: var(--bg); }
  .timeline { position: relative; }
  .timeline::before {
    content: '';
    position: absolute;
    left: 20px; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(180deg, var(--accent), var(--border), transparent);
  }
  .timeline-item {
    display: flex;
    gap: 40px;
    padding-bottom: 48px;
    position: relative;
  }
  .timeline-dot {
    width: 40px; height: 40px;
    background: var(--panel);
    border: 1px solid var(--accent);
    display: flex; align-items: center; justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
    position: relative;
    z-index: 1;
    box-shadow: var(--glow);
  }
  .timeline-card {
    flex: 1;
    background: var(--panel);
    border: 1px solid var(--border);
    padding: 24px 28px;
    position: relative;
    transition: border-color 0.3s;
  }
  .timeline-card:hover { border-color: rgba(0,229,255,0.3); }
  .timeline-card::before {
    content: '';
    position: absolute;
    left: -8px; top: 12px;
    width: 8px; height: 1px;
    background: var(--border);
  }
  .edu-title {
    font-family: 'Orbitron', monospace;
    font-size: 14px;
    font-weight: 700;
    color: #fff;
    letter-spacing: 1px;
    margin-bottom: 4px;
  }
  .edu-school {
    font-size: 13px;
    color: var(--accent);
    margin-bottom: 8px;
  }
  .edu-meta {
    display: flex; gap: 20px; flex-wrap: wrap;
    margin-bottom: 16px;
  }
  .edu-meta span {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 1px;
  }
  .edu-points { list-style: none; }
  .edu-points li {
    font-size: 13px;
    color: rgba(200,230,240,0.65);
    padding: 4px 0;
    display: flex; align-items: flex-start; gap: 10px;
    line-height: 1.5;
  }
  .edu-points li::before {
    content: '▸';
    color: var(--accent);
    flex-shrink: 0;
    font-size: 10px;
    margin-top: 3px;
  }

  /* SOFT SKILLS */
  #soft-skills { background: var(--bg2); }
  .soft-skills-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; }
  .soft-card {
    background: var(--panel);
    border: 1px solid var(--border);
    padding: 32px 20px;
    text-align: center;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .soft-card:hover {
    border-color: rgba(0,229,255,0.4);
    transform: translateY(-4px);
  }
  .soft-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at center bottom, rgba(0,229,255,0.06) 0%, transparent 70%);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .soft-card:hover::before { opacity: 1; }
  .soft-icon { font-size: 32px; margin-bottom: 16px; display: block; }
  .soft-name {
    font-family: 'Orbitron', monospace;
    font-size: 10px;
    font-weight: 700;
    color: var(--accent);
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  /* FOOTER */
  footer {
    background: #020609;
    border-top: 1px solid var(--border);
    padding: 48px;
    text-align: center;
  }
  .footer-logo {
    font-family: 'Orbitron', monospace;
    font-size: 22px;
    font-weight: 900;
    color: #fff;
    letter-spacing: 4px;
    margin-bottom: 8px;
  }
  .footer-sub {
    font-family: 'Share Tech Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 32px;
  }
  .footer-cta {
    font-size: 15px;
    color: rgba(200,230,240,0.5);
    margin-bottom: 32px;
  }
  .footer-cta a {
    color: var(--accent);
    text-decoration: none;
    font-weight: 600;
  }
  .footer-copy {
    font-family: 'Share Tech Mono', monospace;
    font-size: 10px;
    color: rgba(74,122,150,0.4);
    letter-spacing: 2px;
    text-transform: uppercase;
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* Responsive */
  @media (max-width: 900px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    section { padding: 80px 24px; }
    #hero { padding: 120px 24px 60px; }
    .about-grid { grid-template-columns: 1fr; }
    .skills-grid { grid-template-columns: 1fr 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    .soft-skills-grid { grid-template-columns: repeat(2, 1fr); }
  }
  @media (max-width: 560px) {
    .skills-grid { grid-template-columns: 1fr; }
    .hero-stats { gap: 24px; }
    .info-grid { grid-template-columns: 1fr; }
    .soft-skills-grid { grid-template-columns: repeat(2, 1fr); }
  }

  /* HERO IMAGE DESIGN */
  .hero-image {
    position: relative;
    z-index: 2;
    flex-shrink: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .hero-img-wrapper {
    position: relative;
    width: 340px;
    height: 340px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .hero-img-ring {
    position: absolute;
    border-radius: 50%;
    border: 1px solid rgba(0,229,255,0.25);
  }
  .ring-1 { width: 340px; height: 340px; animation: spinRing 18s linear infinite; border-color: rgba(0,229,255,0.3); border-style: dashed; }
  .ring-2 { width: 300px; height: 300px; animation: spinRing 12s linear infinite reverse; border-color: rgba(255,107,53,0.2); }
  .ring-3 { width: 260px; height: 260px; animation: spinRing 8s linear infinite; border-color: rgba(127,255,0,0.15); border-style: dotted; }

  @keyframes spinRing {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }

  .hero-img-circle {
    width: 220px;
    height: 220px;
    border-radius: 50%;
    overflow: hidden;
    border: 3px solid var(--accent);
    box-shadow: 0 0 0 6px rgba(0,229,255,0.08), 0 0 40px rgba(0,229,255,0.35), inset 0 0 30px rgba(0,229,255,0.1);
    position: relative;
    z-index: 2;
  }

  .hero-img-circle img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: top center;
    display: block;
  }

  .hero-img-badge {
    position: absolute;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    background: linear-gradient(135deg, rgba(0,229,255,0.15), rgba(0,229,255,0.05));
    border: 1px solid rgba(0,229,255,0.5);
    color: var(--accent);
    font-family: 'Orbitron', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 3px;
    padding: 6px 16px;
    white-space: nowrap;
    backdrop-filter: blur(10px);
    z-index: 3;
    box-shadow: 0 0 12px rgba(0,229,255,0.2);
  }

  .corner-br {
    position: absolute;
    width: 12px; height: 12px;
    border-color: var(--accent);
    border-style: solid;
    opacity: 0.6;
    z-index: 3;
  }
  .c1 { top: 20px; left: 20px; border-width: 2px 0 0 2px; }
  .c2 { top: 20px; right: 20px; border-width: 2px 2px 0 0; }
  .c3 { bottom: 20px; left: 20px; border-width: 0 0 2px 2px; }
  .c4 { bottom: 20px; right: 20px; border-width: 0 2px 2px 0; }

  @media (max-width: 1000px) {
    .hero-img-wrapper { width: 280px; height: 280px; }
    .ring-1 { width: 280px; height: 280px; }
    .ring-2 { width: 248px; height: 248px; }
    .ring-3 { width: 216px; height: 216px; }
    .hero-img-circle { width: 180px; height: 180px; }
  }
  @media (max-width: 600px) {
    .hero-img-wrapper { width: 220px; height: 220px; }
    .ring-1 { width: 220px; height: 220px; }
    .ring-2 { width: 192px; height: 192px; }
    .ring-3 { width: 164px; height: 164px; }
    .hero-img-circle { width: 140px; height: 140px; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">MJ.DEV</div>
  <ul class="nav-links">
    <li><a href="#about">Profile</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="mailto:jamukiyamehul23@gmail.com">Contact</a></li>
  </ul>
</nav>


<!-- HERO -->
<section id="hero">
  <div class="grid-bg"></div>
  <div class="shape shape-1"></div>
  <div class="shape shape-2"></div>
  <div class="shape shape-3"></div>
  <div class="shape shape-4"></div>

  <div class="hero-container">

    <div class="hero-content">
      <div class="hero-tag">Unity Developer &amp; App Builder</div>
      <h1 class="hero-name">MEHUL<br>JAMBUKIYA</h1>
      <p class="hero-title">BCA Graduate &nbsp;|&nbsp; Game Dev &nbsp;|&nbsp; C# / Java</p>
      <p class="hero-desc">
        Crafting interactive experiences with <strong style="color:var(--accent)">Unity Engine</strong> and building
        robust mobile apps with <strong style="color:var(--accent2)">Android Studio</strong>.
        Fresh graduate, ready to level up the game dev world.
      </p>

      <div class="hero-stats">
        <div class="stat-item">
          <span class="stat-num">8.32</span>
          <span class="stat-label">CGPA</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">5+</span>
          <span class="stat-label">Tech Skills</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">2026</span>
          <span class="stat-label">Graduate</span>
        </div>
      </div>

      <div class="hero-buttons">
        <a href="mailto:jamukiyamehul23@gmail.com" class="btn btn-primary">⚡ Hire Me</a>
        <a href="#projects" class="btn btn-outline">▶ View Work</a>
      </div>
    </div>

    <!-- RIGHT SIDE IMAGE -->
    <div class="hero-image">
      <div class="hero-img-wrapper">
        <div class="hero-img-ring ring-1"></div>
        <div class="hero-img-ring ring-2"></div>
        <div class="hero-img-ring ring-3"></div>
        <div class="hero-img-circle">
            <img src="mehul.jpeg">
        </div>
        <div class="hero-img-badge">⚡ UNITY DEV</div>
        <div class="corner-br c1"></div>
        <div class="corner-br c2"></div>
        <div class="corner-br c3"></div>
        <div class="corner-br c4"></div>
      </div>
    </div>

  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="section-header reveal">
    <span class="section-num">01</span>
    <h2 class="section-title">Player Profile</h2>
    <div class="section-line"></div>
  </div>
  <div class="about-grid">
    <div class="about-text reveal">
      <p>I'm a <strong>BCA graduate from Gujarat University</strong> with a passion for building engaging, interactive applications. My journey spans game development with <strong>Unity Engine</strong>, Android app development, and modern web technologies.</p>
      <p>I developed a <strong>Firebase-backed E-Attendance System</strong> — a role-based Android application supporting both Student and Faculty workflows with real-time data synchronization. It demonstrates my ability to build practical, production-quality apps.</p>
      <p>As a self-driven learner, I'm actively expanding into <strong> Unity game development</strong>, always pushing to level up my technical stack. I'm eager to join a forward-thinking team where I can create, contribute, and grow.</p>

      <div class="info-grid">
        <div class="info-item">
          <div class="info-label">Location</div>
          <div class="info-value">Ahmedabad, Gujarat</div>
        </div>
        <div class="info-item">
          <div class="info-label">Status</div>
          <div class="info-value" style="color:var(--accent3)">Open to Work ✓</div>
        </div>
        <div class="info-item">
          <div class="info-label">Degree</div>
          <div class="info-value">BCA — Gujarat University</div>
        </div>
        <div class="info-item">
          <div class="info-label">CGPA</div>
          <div class="info-value" style="color:var(--accent)">8.32 / 10.0</div>
        </div>
      </div>
    </div>

    <div class="contact-panel reveal">
      <div class="contact-title">Contact Info</div>
      <div class="contact-item">
        <div class="contact-icon">📱</div>
        <div>
          <div class="contact-info-label">Phone</div>
          <div class="contact-info-val">+91 92651 46063</div>
        </div>
      </div>
      <div class="contact-item">
        <div class="contact-icon">✉️</div>
        <div>
          <div class="contact-info-label">Email</div>
          <div class="contact-info-val">jamukiyamehul23@gmail.com</div>
        </div>
      </div>
      <div class="contact-item">
        <div class="contact-icon">💼</div>
        <div>
          <div class="contact-info-label">LinkedIn</div>
          <div class="contact-info-val">Jambukiya Mehul</div>
        </div>
      </div>
      <div class="contact-item">
        <div class="contact-icon">🦊</div>
        <div>
          <div class="contact-info-label">GitLab</div>
          <div class="contact-info-val">Jambukiya Mehul</div>
        </div>
      </div>
      <div style="margin-top: 28px;">
        <a href="mailto:jamukiyamehul23@gmail.com" class="btn btn-primary" style="width:100%; justify-content:center;">Send Message ➜</a>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-header reveal">
    <span class="section-num">02</span>
    <h2 class="section-title">Skill Tree</h2>
    <div class="section-line"></div>
  </div>
  <div class="skills-grid">

    <div class="skill-card reveal">
      <span class="skill-card-icon">🎮</span>
      <div class="skill-card-title">Game Dev</div>
      <div class="skill-tags">
        <span class="tag tag-cyan">Unity Engine</span>
        <span class="tag tag-cyan">C# Scripting</span>
        <span class="tag tag-cyan">Game Logic</span>
        <span class="tag tag-cyan">2D / 3D</span>
      </div>
    </div>

    <div class="skill-card reveal">
      <span class="skill-card-icon">📱</span>
      <div class="skill-card-title">Mobile Dev</div>
      <div class="skill-tags">
        <span class="tag tag-orange">Android Studio</span>
        <span class="tag tag-orange">Java</span>
        <span class="tag tag-orange">XML Layouts</span>
        <span class="tag tag-orange">Firebase Auth</span>
        <span class="tag tag-orange">Realtime DB</span>
      </div>
    </div>

    <div class="skill-card reveal">
      <span class="skill-card-icon">🌐</span>
      <div class="skill-card-title">Web Dev</div>
      <div class="skill-tags">
        <span class="tag tag-green">HTML5</span>
        <span class="tag tag-green">CSS3</span>
        <span class="tag tag-green">JavaScript</span>
        <span class="tag tag-green">Laravel</span>
        <span class="tag tag-green">ASP.NET</span>
      </div>
    </div>

    <div class="skill-card reveal" style="grid-column: span 2;">
      <span class="skill-card-icon">💻</span>
      <div class="skill-card-title">Programming Languages</div>
      <div class="skill-bar-list">
        <div class="skill-bar-item">
          <div class="skill-bar-header">
            <span class="skill-bar-name">C# (Unity / .NET)</span>
            <span class="skill-bar-pct">80%</span>
          </div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="width:80%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-header">
            <span class="skill-bar-name">Java (Android)</span>
            <span class="skill-bar-pct">75%</span>
          </div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="width:75%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-header">
            <span class="skill-bar-name">Python</span>
            <span class="skill-bar-pct">65%</span>
          </div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="width:65%"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-header">
            <span class="skill-bar-name">JavaScript / HTML / CSS</span>
            <span class="skill-bar-pct">70%</span>
          </div>
          <div class="skill-bar-track"><div class="skill-bar-fill" style="width:70%"></div></div>
        </div>
      </div>
    </div>

    <div class="skill-card reveal">
      <span class="skill-card-icon">🛠️</span>
      <div class="skill-card-title">Tools &amp; IDEs</div>
      <div class="skill-tags">
        <span class="tag tag-cyan">Visual Studio</span>
        <span class="tag tag-cyan">Android Studio</span>
        <span class="tag tag-cyan">Git</span>
        <span class="tag tag-cyan">GitLab</span>
        <span class="tag tag-cyan">Firebase</span>
        <span class="tag tag-cyan">Unity Engine</span>
      </div>
    </div>

  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-header reveal">
    <span class="section-num">03</span>
    <h2 class="section-title">Project Log</h2>
    <div class="section-line"></div>
  </div>
  <div class="projects-grid">

    <!-- E-Attendance System -->
    <div class="project-card reveal">
      <div class="project-img">
        <div class="project-img-text">APP</div>
        <span class="project-badge badge-live">Completed</span>
      </div>
      <div class="project-body">
        <div class="project-name">E-Attendance System</div>
        <p class="project-desc">
          A role-based Android attendance application supporting Student and Faculty users with separate login flows, live data sync via Firebase Realtime Database, and responsive XML layouts compatible across screen sizes.
        </p>
        <div class="project-tech">
          <span class="tag tag-orange">Android Studio</span>
          <span class="tag tag-orange">Java</span>
          <span class="tag tag-cyan">Firebase Auth</span>
          <span class="tag tag-cyan">Realtime DB</span>
          <span class="tag tag-green">XML</span>
        </div>
      </div>
    </div>

    <!-- Coming Soon -->
    <div class="coming-soon reveal">
      <span class="coming-soon-icon">🎮</span>
      <div class="coming-soon-text">Unity Game — Coming Soon</div>
      <div class="coming-soon-sub">Currently in development. Check back soon!</div>
    </div>

    <div class="coming-soon reveal">
      <span class="coming-soon-icon">🌐</span>
      <div class="coming-soon-text">Laravel Web App — In Progress</div>
      <div class="coming-soon-sub">Expanding web dev expertise with Laravel.</div>
    </div>

    <div class="coming-soon reveal">
      <span class="coming-soon-icon">🚀</span>
      <div class="coming-soon-text">Next Project Loading...</div>
      <div class="coming-soon-sub">More exciting builds on the way. Stay tuned!</div>
    </div>

  </div>
</section>

<!-- EDUCATION -->
<section id="education">
  <div class="section-header reveal">
    <span class="section-num">04</span>
    <h2 class="section-title">XP Log</h2>
    <div class="section-line"></div>
  </div>
  <div class="timeline">

    <div class="timeline-item reveal">
      <div class="timeline-dot">🎓</div>
      <div class="timeline-card">
        <div class="edu-title">Bachelor of Computer Applications (BCA)</div>
        <div class="edu-school">Gujarat University, Ahmedabad, Gujarat</div>
        <div class="edu-meta">
          <span>📅 Aug 2023 – Sep 2026</span>
          <span>⭐ CGPA: 8.32 / 10.0</span>
        </div>
        <ul class="edu-points">
          <li>Specialization in software programming, mobile application development, and game development.</li>
          <li>Developed strong foundations in data structures, object-oriented programming, and database management.</li>
          <li>Active self-learner — independently pursuing Unity game development alongside formal studies.</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item reveal">
      <div class="timeline-dot">📘</div>
      <div class="timeline-card">
        <div class="edu-title">Higher Secondary Certificate (HSC)</div>
        <div class="edu-school">Chanakya Vidhya Sankul, Ahmedabad, Gujarat</div>
        <div class="edu-meta">
          <span>📅 Jun 2021 – Mar 2023</span>
          <span>⭐ 81.57%</span>
        </div>
      </div>
    </div>

    <div class="timeline-item reveal">
      <div class="timeline-dot">📗</div>
      <div class="timeline-card">
        <div class="edu-title">Secondary School Certificate (SSC)</div>
        <div class="edu-school">Vrajendra Vidhya Vihar Madhyamik Shala, Ahmedabad, Gujarat</div>
        <div class="edu-meta">
          <span>📅 Jun 2019 – May 2021</span>
          <span>⭐ 77.33%</span>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- SOFT SKILLS -->
<section id="soft-skills">
  <div class="section-header reveal">
    <span class="section-num">05</span>
    <h2 class="section-title">Character Traits</h2>
    <div class="section-line"></div>
  </div>
  <div class="soft-skills-grid">
    <div class="soft-card reveal">
      <span class="soft-icon">🧩</span>
      <div class="soft-name">Problem Solving</div>
    </div>
    <div class="soft-card reveal">
      <span class="soft-icon">📚</span>
      <div class="soft-name">Self-Learning</div>
    </div>
    <div class="soft-card reveal">
      <span class="soft-icon">🤝</span>
      <div class="soft-name">Teamwork</div>
    </div>
    <div class="soft-card reveal">
      <span class="soft-icon">🔍</span>
      <div class="soft-name">Attention to Detail</div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">MEHUL JAMBUKIYA</div>
  <div class="footer-sub">Unity Developer · Android · Web</div>
  <p class="footer-cta">Looking for a dedicated developer? <a href="mailto:jamukiyamehul23@gmail.com">Let's connect →</a></p>
  <div class="footer-copy">© 2026 Mehul Jambukiya · Ahmedabad, Gujarat · All Systems Go</div>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animateCursor() {
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12;
    ry += (my - ry) *.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateCursor);
  }
  animateCursor();

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => observer.observe(el));

  // Skill bar animation on visibility
  const bars = document.querySelectorAll('.skill-bar-fill');
  bars.forEach(bar => {
    const targetWidth = bar.style.width;
    bar.style.width = '0%';
    const barObserver = new IntersectionObserver(entries => {
      if (entries[0].isIntersecting) {
        setTimeout(() => { bar.style.transition = 'width 1.2s cubic-bezier(0.4,0,0.2,1)'; bar.style.width = targetWidth; }, 300);
        barObserver.disconnect();
      }
    }, { threshold: 0.5 });
    barObserver.observe(bar);
  });
</script>
</body>
</html>
