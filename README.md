<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Raghav Goyal | Developer & Patent Holder</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&family=Syne:wght@600;700;800&display=swap" rel="stylesheet">
    <style>
        /* CSS Variables */
        :root {
            --base-dark: #0A0E1A;
            --accent-cyan: #00F5FF;
            --highlight-amber: #FFB347;
            --text-light: #F0F4FF;
            --font-heading: 'Syne', sans-serif;
            --font-body: 'DM Sans', sans-serif;
        }

        /* Reset & Base Utilities */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        body {
            background-color: var(--base-dark);
            color: var(--text-light);
            font-family: var(--font-body);
            overflow-x: hidden;
            line-height: 1.6;
        }
        h1, h2, h3, h4, h5, h6 { font-family: var(--font-heading); font-weight: 700; }
        a { color: inherit; text-decoration: none; }
        .section { padding: 8rem 5%; max-width: 1200px; margin: 0 auto; position: relative; z-index: 10; }
        .bg-alt { background: rgba(255,255,255,0.02); }

        /* Animated Aurora Background Overlay */
        .aurora-bg {
            position: fixed;
            top: 0; left: 0; width: 100vw; height: 100vh;
            z-index: -2;
            background: var(--base-dark);
            overflow: hidden;
            pointer-events: none;
        }
        .aurora-bg::before, .aurora-bg::after {
            content: '';
            position: absolute;
            width: 200%; height: 200%;
            top: -50%; left: -50%;
            background: radial-gradient(circle at 50% 50%, rgba(0, 245, 255, 0.12), transparent 40%),
                        radial-gradient(circle at 80% 20%, rgba(255, 179, 71, 0.08), transparent 40%);
            animation: aurora-move 15s linear infinite;
            mix-blend-mode: screen;
        }
        .aurora-bg::after {
            background: radial-gradient(circle at 20% 80%, rgba(0, 245, 255, 0.08), transparent 50%);
            animation: aurora-move 20s linear infinite reverse;
        }
        @keyframes aurora-move {
            0% { transform: rotate(0deg) scale(1); }
            50% { transform: rotate(180deg) scale(1.1); }
            100% { transform: rotate(360deg) scale(1); }
        }

        /* Noise Texture */
        .noise-overlay {
            position: fixed;
            top: 0; left: 0; width: 100vw; height: 100vh;
            z-index: -1;
            opacity: 0.04;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
            pointer-events: none;
        }

        /* Scroll Fades */
        .fade-in {
            opacity: 0; transform: translateY(30px);
            transition: opacity 0.8s ease, transform 0.8s ease;
        }
        .fade-in.visible {
            opacity: 1; transform: translateY(0);
        }

        /* Navbar */
        .navbar {
            position: fixed; top: 0; width: 100%; z-index: 100;
            padding: 1.5rem 5%;
            display: flex; justify-content: space-between; align-items: center;
            transition: padding 0.3s ease, background 0.3s ease, border-bottom 0.3s ease;
        }
        .navbar.scrolled {
            padding: 1rem 5%;
            background: rgba(10, 14, 26, 0.85);
            backdrop-filter: blur(15px);
            border-bottom: 1px solid rgba(0, 245, 255, 0.1);
        }
        .logo { font-size: 1.8rem; font-family: var(--font-heading); font-weight: 800; }
        .logo span { color: var(--accent-cyan); }
        .nav-links { display: flex; gap: 2rem; list-style: none; }
        .nav-links a { font-weight: 500; transition: color 0.3s ease; }
        .nav-links a:hover { color: var(--accent-cyan); }
        .hamburger { display: none; flex-direction: column; justify-content: space-between; width: 30px; height: 21px; cursor: pointer; z-index: 1000; }
        .hamburger span { display: block; height: 3px; width: 100%; background: var(--text-light); transition: 0.3s; }

        /* Buttons */
        .btn {
            display: inline-flex; align-items: center; justify-content: center; gap: 0.5rem;
            padding: 0.8rem 2rem; font-family: var(--font-heading); font-weight: 700;
            border-radius: 8px; transition: all 0.3s ease; cursor: pointer;
            text-transform: uppercase; letter-spacing: 1px;
        }
        .btn-primary { background: var(--accent-cyan); color: var(--base-dark); border: 2px solid var(--accent-cyan); }
        .btn-primary:hover { box-shadow: 0 0 20px rgba(0, 245, 255, 0.4); transform: translateY(-3px); }
        .btn-secondary { background: transparent; color: var(--accent-cyan); border: 2px solid var(--accent-cyan); }
        .btn-secondary:hover { background: rgba(0, 245, 255, 0.1); transform: translateY(-3px); }
        .btn-sm { padding: 0.5rem 1rem; font-size: 0.85rem; }

        /* Hero */
        .hero { display: flex; align-items: center; justify-content: space-between; min-height: 100vh; padding-top: 80px; }
        .hero-left { flex: 1; padding-right: 2rem; }
        .hero-right { flex: 1; display: flex; justify-content: center; position: relative; }
        h1.hero-title { font-size: 4.5rem; line-height: 1.1; margin-bottom: 0.5rem; }
        .highlight { color: var(--accent-cyan); }
        .typewriter-container { font-size: 2rem; color: var(--highlight-amber); margin-bottom: 2rem; height: 3rem; }
        .cursor { animation: blink 1s infinite; font-weight: 400;}
        @keyframes blink { 50% { opacity: 0; } }
        .hero-bio { font-size: 1.25rem; margin-bottom: 2.5rem; color: rgba(240, 244, 255, 0.8); max-width: 600px; }
        .hero-buttons { display: flex; gap: 1.5rem; }

        /* Avatar */
        .avatar-svg { width: 100%; max-width: 500px; height: auto; animation: float 6s ease-in-out infinite; }
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }
        .spin-slow { transform-origin: center; animation: spin 30s linear infinite; }
        @keyframes spin { to { transform: rotate(360deg); } }

        /* Common Typography */
        .section-title { font-size: 3rem; margin-bottom: 0.5rem; }
        .section-subtitle { font-size: 1.2rem; margin-bottom: 0.5rem; color: rgba(240, 244, 255, 0.7); }
        .title-underline { width: 60px; height: 4px; background: var(--accent-cyan); margin-bottom: 3rem; border-radius: 2px; }

        /* Grids */
        .about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; align-items: center; margin-bottom: 4rem;}
        .stats-container {
            display: grid; grid-template-columns: repeat(2, 1fr); gap: 2rem;
            background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05);
            border-radius: 16px; padding: 3rem 2rem; backdrop-filter: blur(10px); text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        .projects-grid, .patents-grid, .client-grid {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 2rem;
        }

        /* Cards */
        .card {
            background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.05);
            border-radius: 16px; padding: 2.5rem;
            transition: transform 0.3s ease, box-shadow 0.3s ease, border-color 0.3s ease;
            backdrop-filter: blur(10px); display: flex; flex-direction: column; justify-content: space-between;
        }
        .card:hover { transform: translateY(-5px); box-shadow: 0 10px 30px rgba(0, 245, 255, 0.1); border-color: rgba(0, 245, 255, 0.4); }
        .glow-card { border-color: rgba(255, 179, 71, 0.3); }
        .glow-card:hover { box-shadow: 0 10px 30px rgba(255, 179, 71, 0.15); border-color: var(--highlight-amber); }
        
        .stat-number { font-size: 3.5rem; color: var(--accent-cyan); margin-bottom: 0.5rem; line-height: 1; font-family: var(--font-heading); font-weight: 800;}
        .stat-label { font-size: 0.9rem; text-transform: uppercase; letter-spacing: 1px; color: var(--text-light); opacity: 0.8; }

        /* Skills */
        .skills-group { margin-bottom: 2rem; }
        .skills-group h3 { margin-bottom: 1.5rem; color: var(--highlight-amber); font-family: var(--font-body); text-transform: uppercase; letter-spacing: 2px; font-size: 1rem;}
        .skill-pill {
            display: inline-block; padding: 0.6rem 1.5rem;
            background: rgba(0, 245, 255, 0.05); border: 1px solid rgba(0, 245, 255, 0.2);
            border-radius: 50px; margin: 0 0.8rem 0.8rem 0; font-size: 0.95rem; font-weight: 500;
            position: relative; overflow: hidden; transition: all 0.3s ease; cursor: default;
        }
        .skill-pill::before {
            content: ''; position: absolute; top:0; left: -100%; width: 50%; height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
            transform: skewX(-20deg); transition: left 0.5s ease;
        }
        .skill-pill:hover { background: rgba(0, 245, 255, 0.1); box-shadow: 0 0 15px rgba(0, 245, 255, 0.4); border-color: var(--accent-cyan); }
        .skill-pill:hover::before { left: 200%; }

        /* Patents */
        .badge-glow {
            display: inline-block; padding: 1.2rem 2.5rem; font-size: 1.5rem; font-family: var(--font-heading); font-weight: 800;
            color: var(--highlight-amber); background: rgba(255, 179, 71, 0.1); border: 2px solid var(--highlight-amber);
            border-radius: 12px; margin-bottom: 3rem; box-shadow: 0 0 20px rgba(255, 179, 71, 0.3);
            text-transform: uppercase; letter-spacing: 2px; animation: pulse-glow 2s infinite alternate; width: 100%; text-align: center;
        }
        @keyframes pulse-glow {
            from { box-shadow: 0 0 10px rgba(255, 179, 71, 0.1); }
            to { box-shadow: 0 0 35px rgba(255, 179, 71, 0.5); }
        }
        .patent-icon { font-size: 2rem; margin-bottom: 1rem; }
        .status-pill { display: inline-block; padding: 0.4rem 1rem; background: rgba(255, 179, 71, 0.1); color: var(--highlight-amber); border-radius: 50px; font-size: 0.85rem; margin-top: 1.5rem; border: 1px solid rgba(255, 179, 71, 0.3); font-weight: 700; text-transform: uppercase; letter-spacing: 1px; }

        /* Projects */
        .project-tags { margin-bottom: 1.5rem; }
        .tag { font-size: 0.75rem; background: rgba(255,255,255,0.08); padding: 0.3rem 0.8rem; border-radius: 4px; margin-right: 0.5rem; margin-bottom: 0.5rem; display: inline-block; color: var(--accent-cyan); text-transform: uppercase; letter-spacing: 0.5px; font-weight: 700;}
        .card-actions { display: flex; gap: 1rem; margin-top: 2rem; }
        .project-card h3 { font-size: 1.5rem; margin-bottom: 1rem; }

        /* Client Work */
        .client-card .outcome { font-size: 1.25rem; font-weight: 500; font-style: italic; color: #fff; margin: 1.5rem 0;}
        .client-card .tech-stack { color: var(--accent-cyan); font-weight: 700; font-size: 0.9rem; text-transform: uppercase; letter-spacing: 1px;}

        /* Contact */
        .contact-container { text-align: center; max-width: 700px; margin: 0 auto; background: rgba(255,255,255,0.02); padding: 4rem 2rem; border-radius: 16px; border: 1px solid rgba(255,255,255,0.05); }
        .contact-cta { font-size: 2.5rem; margin-bottom: 1.5rem; color: var(--accent-cyan); }
        .social-links { display: flex; justify-content: center; gap: 1.5rem; margin-top: 3rem; flex-wrap: wrap; }
        .social-btn { display: flex; align-items: center; gap: 0.5rem; padding: 1rem 2rem; border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; transition: all 0.3s; background: rgba(255,255,255,0.05); font-weight: 700; }
        .social-btn:hover { background: var(--accent-cyan); color: var(--base-dark); border-color: var(--accent-cyan); transform: translateY(-3px); }

        /* Footer */
        footer { padding: 3rem; text-align: center; border-top: 1px solid rgba(255,255,255,0.05); font-size: 0.9rem; opacity: 0.6; }

        /* Mobile Responsive */
        @media (max-width: 900px) {
            .hero { flex-direction: column; text-align: center; padding-top: 150px; justify-content: center; }
            .hero-left { padding-right: 0; margin-bottom: 4rem; }
            h1.hero-title { font-size: 3rem; }
            .typewriter-container { font-size: 1.5rem; height: auto; }
            .hero-buttons { justify-content: center; }
            .stats-container { grid-template-columns: 1fr; }
            .section { padding: 5rem 5%; }
            .about-grid { gap: 3rem; }
        }
        @media (max-width: 768px) {
            .hamburger { display: flex; }
            .hamburger.active span:nth-child(1) { transform: translateY(9px) rotate(45deg); }
            .hamburger.active span:nth-child(2) { opacity: 0; }
            .hamburger.active span:nth-child(3) { transform: translateY(-9px) rotate(-45deg); }

            .nav-links {
                position: fixed; top: 0; right: -100%; width: 100vw; height: 100vh;
                background: rgba(10, 14, 26, 0.98); backdrop-filter: blur(20px);
                display: flex; flex-direction: column; justify-content: center; align-items: center;
                transition: right 0.4s ease;
            }
            .nav-links.active { right: 0; }
            .nav-links li { margin: 2rem 0; font-size: 1.5rem; }
            
            .hero-buttons { flex-direction: column; gap: 1rem; width: 100%; max-width: 300px; margin: 0 auto; }
            .social-links { flex-direction: column; }
        }
    </style>
</head>
<body>
    <div class="aurora-bg"></div>
    <div class="noise-overlay"></div>

    <nav class="navbar" id="navbar">
        <a href="#" class="logo">Raghav<span>.</span></a>
        <ul class="nav-links">
            <li><a href="#about">About</a></li>
            <li><a href="#patents">Patents</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
        <div class="hamburger">
            <span></span><span></span><span></span>
        </div>
    </nav>

    <section id="home" class="hero section">
        <div class="hero-left fade-in">
            <h1 class="hero-title">I am <span class="highlight">Raghav Goyal</span></h1>
            <div class="typewriter-container">
                A <span class="typewriter-text" id="typewriter"></span><span class="cursor">|</span>
            </div>
            <p class="hero-bio">I build things that work. 10 projects, 2 patents, 2 happy clients — still in my third year.</p>
            <div class="hero-buttons">
                <a href="#projects" class="btn btn-primary">View Projects</a>
                <a href="https://github.com/snowowl69" target="_blank" class="btn btn-secondary">
                    <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg> 
                    GitHub
                </a>
            </div>
        </div>
        <div class="hero-right fade-in" style="transition-delay: 0.2s;">
            <svg class="avatar-svg" viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg">
                <defs>
                    <filter id="cyanGlow" x="-20%" y="-20%" width="140%" height="140%">
                        <feGaussianBlur stdDeviation="8" result="blur" />
                        <feComposite in="SourceGraphic" in2="blur" operator="over" />
                    </filter>
                    <linearGradient id="laptopGrad" x1="0" y1="0" x2="0" y2="1">
                        <stop offset="0%" stop-color="#00F5FF" stop-opacity="0.9"/>
                        <stop offset="100%" stop-color="transparent" />
                    </linearGradient>
                </defs>
                <!-- Abstract Rings -->
                <circle cx="200" cy="200" r="160" fill="none" stroke="rgba(0, 245, 255, 0.3)" stroke-width="2" stroke-dasharray="10 10" class="spin-slow" />
                <circle cx="200" cy="200" r="140" fill="rgba(255, 179, 71, 0.03)" />
                
                <!-- Floating geometric nodes -->
                <circle cx="80" cy="180" r="6" fill="#FFB347" filter="url(#cyanGlow)">
                    <animate attributeName="cy" values="180;150;180" dur="4s" repeatCount="indefinite"/>
                </circle>
                <circle cx="320" cy="240" r="8" fill="#00F5FF" filter="url(#cyanGlow)">
                    <animate attributeName="cy" values="240;270;240" dur="5s" repeatCount="indefinite"/>
                    <animate attributeName="cx" values="320;335;320" dur="8s" repeatCount="indefinite"/>
                </circle>
                <circle cx="100" cy="300" r="4" fill="#F0F4FF" opacity="0.6">
                    <animate attributeName="cy" values="300;280;300" dur="3s" repeatCount="indefinite"/>
                </circle>

                <!-- Torso / Hoodie Area -->
                <path d="M 110 360 C 110 240, 130 190, 200 190 C 270 190, 290 240, 290 360 Z" fill="#0E1321" stroke="#00F5FF" stroke-width="4" />
                
                <!-- Hoodie lines -->
                <path d="M 170 210 L 170 270 M 230 210 L 230 270" stroke="#00F5FF" stroke-width="2" stroke-linecap="round"/>
                
                <!-- Head -->
                <rect x="155" y="110" width="90" height="100" rx="45" fill="#1A1820" stroke="#FFB347" stroke-width="3" />
                
                <!-- Headphones -->
                <path d="M 140 150 C 140 80, 260 80, 260 150" fill="none" stroke="#F0F4FF" stroke-width="10" stroke-linecap="round"/>
                <rect x="130" y="130" width="18" height="45" rx="6" fill="#FFB347" filter="url(#cyanGlow)" />
                <rect x="252" y="130" width="18" height="45" rx="6" fill="#FFB347" filter="url(#cyanGlow)" />
            
                <!-- Edgy Visor / Glasses -->
                <path d="M 155 140 Q 200 155 245 140 L 245 160 Q 200 175 155 160 Z" fill="#00F5FF" filter="url(#cyanGlow)" opacity="0.9"/>
            
                <!-- Laptop base -->
                <path d="M 70 360 L 330 360 L 370 395 L 30 395 Z" fill="#0A0E1A" stroke="#00F5FF" stroke-width="3" stroke-linejoin="round"/>
                <!-- Laptop screen block to cast glow -->
                <polygon points="110,360 290,360 260,260 140,260" fill="url(#laptopGrad)" opacity="0.4" filter="url(#cyanGlow)"/>
            </svg>
        </div>
    </section>

    <section id="about" class="section bg-alt" style="padding-top: 6rem; padding-bottom: 6rem;">
        <div class="about-grid">
            <div class="about-text fade-in">
                <h2 class="section-title">The TL;DR</h2>
                <div class="title-underline"></div>
                <!-- Short punchy 3-line bio -->
                <p class="hero-bio" style="font-size: 1.15rem;">I build things that work. 10 projects, 2 patents, 2 happy clients — all while pursuing my B.Tech in IT at VIT Vellore (7.32 GPA). <br><br>I'm not looking for generic internships. I want to solve hard problems, optimize complex systems, and ship code that actually scales. If you need a developer who moves fast and delivers, you've found one.</p>
            </div>
            
            <div class="stats-container fade-in" id="stats">
                <div class="stat-card">
                    <h3 class="stat-number"><span class="counter" data-target="500">0</span>+</h3>
                    <p class="stat-label">GitHub Commits</p>
                </div>
                <div class="stat-card">
                    <h3 class="stat-number"><span class="counter" data-target="10">0</span>+</h3>
                    <p class="stat-label">Projects Built</p>
                </div>
                <div class="stat-card">
                    <h3 class="stat-number"><span class="counter" data-target="2">0</span></h3>
                    <p class="stat-label">Patents Filed</p>
                </div>
                <div class="stat-card">
                    <h3 class="stat-number"><span class="counter" data-target="2">0</span></h3>
                    <p class="stat-label">Live Clients</p>
                </div>
            </div>
        </div>
    </section>

    <section id="patents" class="section">
        <div class="section-header fade-in text-center" style="text-align: center; display: flex; flex-direction: column; align-items: center;">
            <h2 class="section-title">Patents</h2>
            <div class="title-underline"></div>
            
            <div class="badge-glow fade-in" style="max-width: 600px; margin: 0 auto 3rem auto;">
                🏅 2x Student Patent Holder
            </div>
        </div>
        
        <div class="patents-grid fade-in">
            <div class="card glow-card">
                <div class="patent-icon">⚡</div>
                <h3>Decentralized Distributed Logic System</h3>
                <p>A novel approach to establishing trust in computing nodes without massive consensus overhead. Filed formally at the Indian Patent Office during my academic research phase.</p>
                <div class="status-pill pending">Status: Application Filed</div>
            </div>
            <div class="card glow-card">
                <div class="patent-icon">⚡</div>
                <h3>Predictive API Resource Allocation Model</h3>
                <p>System and method utilizing proactive machine learning algorithms to scale compute environments before load spikes occur, mitigating cold starts and reducing latent lag significantly.</p>
                <div class="status-pill pending">Status: Application Filed</div>
            </div>
        </div>
    </section>

    <section id="skills" class="section bg-alt">
        <div class="section-header fade-in">
            <h2 class="section-title">Technical Arsenal</h2>
            <div class="title-underline"></div>
        </div>
        <div class="skills-wrapper fade-in">
            <div class="skills-group">
                <h3>Languages</h3>
                <div class="pill-container">
                    <span class="skill-pill">JavaScript (ES6+)</span>
                    <span class="skill-pill">TypeScript</span>
                    <span class="skill-pill">Python</span>
                    <span class="skill-pill">C++</span>
                    <span class="skill-pill">Java</span>
                </div>
            </div>
            <div class="skills-group">
                <h3>Frameworks & Libraries</h3>
                <div class="pill-container">
                    <span class="skill-pill">React.js</span>
                    <span class="skill-pill">Next.js</span>
                    <span class="skill-pill">Node.js</span>
                    <span class="skill-pill">Express</span>
                    <span class="skill-pill">TailwindCSS</span>
                </div>
            </div>
            <div class="skills-group">
                <h3>Tools & Infrastructure</h3>
                <div class="pill-container">
                    <span class="skill-pill">Git / GitHub</span>
                    <span class="skill-pill">Docker</span>
                    <span class="skill-pill">AWS Services</span>
                    <span class="skill-pill">PostgreSQL</span>
                    <span class="skill-pill">MongoDB</span>
                </div>
            </div>
        </div>
    </section>

    <section id="projects" class="section">
        <div class="section-header fade-in">
            <h2 class="section-title">Featured Projects</h2>
            <div class="title-underline"></div>
        </div>
        <div class="projects-grid fade-in">
            <div class="card project-card">
                <div class="project-tags">
                    <span class="tag">Next.js</span>
                    <span class="tag">TypeScript</span>
                    <span class="tag">Redis</span>
                </div>
                <h3>ScaleMonitor Node Engine</h3>
                <p>Real-time analytics engine processing streaming data to monitor server node health with zero perceived UI latency.</p>
                <div class="card-actions">
                    <a href="#" class="btn btn-primary btn-sm">Live Demo</a>
                    <a href="https://github.com/snowowl69" target="_blank" class="btn btn-secondary btn-sm">Code</a>
                </div>
            </div>
            <div class="card project-card">
                <div class="project-tags">
                    <span class="tag">React</span>
                    <span class="tag">WebSockets</span>
                    <span class="tag">Node.js</span>
                </div>
                <h3>Collaborative ThinkSpace</h3>
                <p>A multiplayer canvas allowing unbounded team collaboration powered by an event-driven synchronized backend architecture.</p>
                <div class="card-actions">
                    <a href="#" class="btn btn-primary btn-sm">Live Demo</a>
                    <a href="https://github.com/snowowl69" target="_blank" class="btn btn-secondary btn-sm">Code</a>
                </div>
            </div>
            <div class="card project-card">
                <div class="project-tags">
                    <span class="tag">Python</span>
                    <span class="tag">FastAPI</span>
                    <span class="tag">Docker</span>
                </div>
                <h3>Neural Predictor Service</h3>
                <p>A microservice deployed model capable of identifying anomalous network packets with 99.2% accuracy in sub-millisecond ranges.</p>
                <div class="card-actions">
                    <a href="#" class="btn btn-primary btn-sm">Live Demo</a>
                    <a href="https://github.com/snowowl69" target="_blank" class="btn btn-secondary btn-sm">Code</a>
                </div>
            </div>
        </div>
    </section>

    <section id="clients" class="section bg-alt">
        <div class="section-header fade-in">
            <h2 class="section-title">Client Work</h2>
            <p class="section-subtitle">Real clients. Real results.</p>
            <div class="title-underline"></div>
        </div>
        <div class="client-grid fade-in">
            <div class="card client-card">
                <h4>E-Commerce Platform Redesign</h4>
                <p class="outcome">"Boosted conversions by 30% with a sub-second page load."</p>
                <p class="tech-stack">Role: Lead Frontend Engineer | Next.js</p>
            </div>
            <div class="card client-card">
                <h4>SaaS Analytics Dashboard</h4>
                <p class="outcome">"Built a high-performance web dashboard handling 1M+ daily rows seamlessly."</p>
                <p class="tech-stack">Role: Full Stack Architect | React + Node.js</p>
            </div>
        </div>
    </section>

    <section id="contact" class="section">
        <div class="contact-container fade-in">
            <h2 class="contact-cta">Ready to build something extraordinary?</h2>
            <p style="font-size: 1.1rem; color: rgba(240,244,255,0.8); margin-bottom: 2rem;">Drop a line. I'm always open to discussing hard technical problems.</p>
            <div class="social-links">
                <a href="mailto:hello@raghav.com" class="social-btn">
                    <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor"><path d="M12 12.713l11.985-8.713h-23.97l11.985 8.713zm0 2.574l-12-8.727v11.44h24v-11.44l-12 8.727z"/></svg> 
                    Email Me
                </a>
                <a href="https://github.com/snowowl69" target="_blank" class="social-btn">
                    <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg> 
                    GitHub
                </a>
                <a href="#" target="_blank" class="social-btn">
                    <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
                    LinkedIn
                </a>
            </div>
        </div>
    </section>

    <footer>
        <p>Built by a human. Designed to ship. &copy; 2026 Raghav Goyal. All rights reserved.</p>
    </footer>

    <!-- Animations, Interactions and Functionality -->
    <script>
        // 1. Typewriter Effect
        const words = ["Developer", "Patent Holder", "Problem Solver", "VIT'er"];
        let wordIndex = 0;
        let charIndex = 0;
        let isDeleting = false;
        const typewriterEl = document.getElementById("typewriter");

        function type() {
            const currentWord = words[wordIndex];
            
            if (isDeleting) {
                typewriterEl.textContent = currentWord.substring(0, charIndex - 1);
                charIndex--;
            } else {
                typewriterEl.textContent = currentWord.substring(0, charIndex + 1);
                charIndex++;
            }

            let typeSpeed = 100;
            if (isDeleting) typeSpeed /= 2;

            if (!isDeleting && charIndex === currentWord.length) {
                typeSpeed = 2000;
                isDeleting = true;
            } else if (isDeleting && charIndex === 0) {
                isDeleting = false;
                wordIndex = (wordIndex + 1) % words.length;
                typeSpeed = 500;
            }
            setTimeout(type, typeSpeed);
        }
        setTimeout(type, 1000);

        // 2. Navbar Shrink & Hamburger
        const navbar = document.getElementById('navbar');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
        });

        const hamburger = document.querySelector('.hamburger');
        const navLinks = document.querySelector('.nav-links');
        hamburger.addEventListener('click', () => {
            hamburger.classList.toggle('active');
            navLinks.classList.toggle('active');
        });
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', () => {
                hamburger.classList.remove('active');
                navLinks.classList.remove('active');
            });
        });

        // 3. Intersection Observer (Fade in on scroll & Trigger counters)
        const observerOptions = { threshold: 0.1, rootMargin: '0px 0px -50px 0px' };
        let countersActivated = false;

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                    
                    // Trigger counters if stats section is visible
                    if (entry.target.id === 'stats' && !countersActivated) {
                        runCounters();
                        countersActivated = true;
                    }
                }
            });
        }, observerOptions);

        document.querySelectorAll('.fade-in').forEach(element => {
            observer.observe(element);
        });

        // 4. Counter Animation
        function runCounters() {
            const counters = document.querySelectorAll('.counter');
            
            counters.forEach(counter => {
                const target = +counter.getAttribute('data-target');
                const duration = 2000; // Total ms to finish counter
                
                // frames -> approx 60Hz = 16ms delay. 
                const delay = 30; // smooth enough
                const steps = duration / delay;
                const inc = target / steps;
                
                let count = 0;
                
                const updateCount = () => {
                    count += inc;
                    if (count < target) {
                        counter.innerText = Math.floor(count);
                        setTimeout(updateCount, delay);
                    } else {
                        counter.innerText = target;
                    }
                };
                updateCount();
            });
        }
    </script>
</body>
</html>
