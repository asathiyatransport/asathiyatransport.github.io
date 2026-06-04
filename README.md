<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    <title>Asathiya Transports — Premium Freight Solutions</title>
    <link
        href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@300;400;500;600;700&family=Barlow+Condensed:ital,wght@0,200;0,300;0,600;0,700;1,200&display=swap"
        rel="stylesheet" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <style>
        /* ── RESET & FULLSCREEN ── */
        *,
        *::before,
        *::after {
            margin: 0;
            padding: 0;
            box-sizing: border-box
        }

        html,
        body {
            width: 100%;
            min-height: 100%;
            scroll-behavior: smooth;
            overflow-x: hidden;
        }

        :root {
            --red: #e63328;
            --deep-red: #b52820;
            --orange: #f57c2b;
            --white: #ffffff;
            --offwhite: #f7f4f0;
            --light: #edeae5;
            --lightgray: #d8d4ce;
            --dark: #111111;
            --charcoal: #222222;
            --steel: #333333;
            --muted: #777777;
            --border: #e0dbd4;
            --text: #1a1a1a;
        }

        body {
            background: var(--white);
            color: var(--text);
            font-family: 'Rajdhani', sans-serif;
            cursor: none;
        }

        /* ── CUSTOM CURSOR ── */
        #cursor {
            position: fixed;
            width: 12px;
            height: 12px;
            background: var(--red);
            border-radius: 50%;
            pointer-events: none;
            z-index: 99999;
            transform: translate(-50%, -50%);
            transition: width 0.25s, height 0.25s;
            mix-blend-mode: multiply
        }

        #cursor-ring {
            position: fixed;
            width: 40px;
            height: 40px;
            border: 1.5px solid rgba(230, 51, 40, 0.45);
            border-radius: 50%;
            pointer-events: none;
            z-index: 99998;
            transform: translate(-50%, -50%);
            transition: all 0.13s ease
        }

        /* ── LOADER ── */
        #loader {
            position: fixed;
            inset: 0;
            background: var(--dark);
            z-index: 99997;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 2rem
        }

        .loader-logo {
            font-family: 'Bebas Neue', sans-serif;
            font-size: clamp(2rem, 6vw, 5rem);
            letter-spacing: 8px;
            color: #fff;
            opacity: 0
        }

        .loader-bar-wrap {
            width: 300px;
            height: 2px;
            background: #2a2a2a;
            overflow: hidden;
            border-radius: 2px
        }

        .loader-bar {
            height: 100%;
            background: linear-gradient(90deg, var(--red), var(--orange));
            width: 0%
        }

        .loader-pct {
            font-family: 'Barlow Condensed', sans-serif;
            font-size: 0.75rem;
            letter-spacing: 4px;
            color: #555
        }

        /* ── THREE.JS ── */
        #three-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
            opacity: 0.18
        }

        /* ── PARTICLES ── */
        #particles {
            position: fixed;
            inset: 0;
            pointer-events: none;
            z-index: 1;
            opacity: 0.5
        }

        /* ── NAV ── */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 1.2rem 4rem;
            background: rgba(255, 255, 255, 0);
            backdrop-filter: blur(0px);
            border-bottom: 1px solid rgba(0, 0, 0, 0);
            transition: all 0.45s ease;
        }

        nav.scrolled {
            background: rgba(255, 255, 255, 0.97);
            backdrop-filter: blur(16px);
            border-bottom: 1px solid var(--border);
            box-shadow: 0 2px 20px rgba(0, 0, 0, 0.07);
        }

        .nav-logo {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.4rem;
            letter-spacing: 4px;
            color: var(--red);
            display: flex;
            align-items: center;
            gap: 0.6rem
        }

        .logo-img {
            height: 38px;
            width: auto;
            object-fit: contain;
            display: block;
        }

        .nav-links {
            display: flex;
            gap: 3rem;
            list-style: none
        }

        .nav-links a {
            text-decoration: none;
            color: rgba(255, 255, 255, 0.85);
            font-size: 0.72rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            transition: color 0.2s;
            position: relative
        }

        nav.scrolled .nav-links a {
            color: var(--steel)
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: 0;
            width: 0;
            height: 1.5px;
            background: var(--red);
            transition: width 0.3s
        }

        .nav-links a:hover::after {
            width: 100%
        }

        .nav-links a:hover {
            color: var(--red) !important
        }

        .nav-cta {
            padding: 0.55rem 1.4rem;
            background: var(--red);
            color: #fff;
            font-size: 0.7rem;
            font-weight: 700;
            letter-spacing: 2px;
            text-transform: uppercase;
            text-decoration: none;
            transition: all 0.25s;
            clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%)
        }

        .nav-cta:hover {
            background: var(--deep-red);
            transform: translateY(-2px);
            box-shadow: 0 6px 18px rgba(230, 51, 40, 0.35)
        }

        /* ── HERO ── */
        .hero {
            position: relative;
            width: 100%;
            height: 100vh;
            display: flex;
            align-items: center;
            overflow: hidden;
            z-index: 2;
        }

        .hero-slides {
            position: absolute;
            inset: 0;
            z-index: 0
        }

        .hero-slide {
            position: absolute;
            inset: 0;
            background-size: cover;
            background-position: center;
            opacity: 0;
            transition: opacity 1.6s ease
        }

        .hero-slide.active {
            opacity: 1
        }

        .hero-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(110deg, rgba(10, 10, 10, 0.93) 0%, rgba(10, 10, 10, 0.72) 55%, rgba(10, 10, 10, 0.25) 100%);
            z-index: 1
        }

        .hero-grid {
            position: absolute;
            inset: 0;
            z-index: 1;
            background-image: linear-gradient(rgba(230, 51, 40, 0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(230, 51, 40, 0.05) 1px, transparent 1px);
            background-size: 72px 72px;
            animation: gridDrift 22s linear infinite
        }

        @keyframes gridDrift {
            to {
                background-position: 72px 72px
            }
        }

        .hero-content {
            position: relative;
            z-index: 2;
            padding: 0 4rem;
            max-width: 950px
        }

        .hero-badge {
            display: inline-flex;
            align-items: center;
            gap: 0.6rem;
            font-size: 0.65rem;
            font-weight: 700;
            letter-spacing: 4px;
            text-transform: uppercase;
            color: var(--red);
            border: 1px solid rgba(230, 51, 40, 0.45);
            padding: 0.4rem 1rem;
            margin-bottom: 2rem;
            background: rgba(230, 51, 40, 0.08);
            backdrop-filter: blur(4px)
        }

        .badge-dot {
            width: 6px;
            height: 6px;
            background: var(--red);
            border-radius: 50%;
            animation: blink 1.6s infinite
        }

        @keyframes blink {

            0%,
            100% {
                opacity: 1
            }

            50% {
                opacity: 0.3
            }
        }

        .hero-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: clamp(4.5rem, 11vw, 10rem);
            line-height: 0.85;
            letter-spacing: 3px;
            color: #fff
        }

        .hero-title .stroke {
            -webkit-text-stroke: 1.5px #fff;
            color: transparent
        }

        .hero-title .red {
            color: var(--red)
        }

        .hero-title .line {
            display: block
        }

        .hero-subtitle {
            margin-top: 1.8rem;
            font-size: 1.05rem;
            font-weight: 300;
            color: rgba(255, 255, 255, 0.52);
            letter-spacing: 0.5px;
            line-height: 1.75;
            max-width: 480px
        }

        .hero-actions {
            margin-top: 2.5rem;
            display: flex;
            gap: 1.2rem;
            flex-wrap: wrap
        }

        .btn {
            display: inline-flex;
            align-items: center;
            gap: 0.6rem;
            padding: 0.9rem 2rem;
            font-family: 'Rajdhani', sans-serif;
            font-size: 0.78rem;
            font-weight: 700;
            letter-spacing: 2.5px;
            text-transform: uppercase;
            text-decoration: none;
            cursor: pointer;
            border: none;
            transition: all 0.3s;
            position: relative;
            overflow: hidden
        }

        .btn::before {
            content: '';
            position: absolute;
            inset: 0;
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(-100%);
            transition: transform 0.4s ease
        }

        .btn:hover::before {
            transform: translateX(0)
        }

        .btn-fire {
            background: linear-gradient(135deg, var(--red), var(--orange));
            color: #fff;
            clip-path: polygon(12px 0, 100% 0, calc(100% - 12px) 100%, 0 100%)
        }

        .btn-fire:hover {
            transform: translateY(-3px);
            box-shadow: 0 14px 32px rgba(230, 51, 40, 0.45)
        }

        .btn-ghost {
            background: transparent;
            color: #fff;
            border: 1px solid rgba(255, 255, 255, 0.25);
            clip-path: polygon(12px 0, 100% 0, calc(100% - 12px) 100%, 0 100%)
        }

        .btn-ghost:hover {
            border-color: var(--red);
            color: var(--red)
        }

        .hero-scroll {
            position: absolute;
            bottom: 2.5rem;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0.5rem;
            z-index: 2
        }

        .scroll-label {
            font-size: 0.58rem;
            letter-spacing: 4px;
            text-transform: uppercase;
            color: rgba(255, 255, 255, 0.4)
        }

        .scroll-line {
            width: 1px;
            height: 48px;
            background: linear-gradient(to bottom, var(--red), transparent);
            animation: scrollAnim 1.8s ease-in-out infinite
        }

        @keyframes scrollAnim {
            0% {
                transform: scaleY(0);
                transform-origin: top
            }

            50% {
                transform: scaleY(1);
                transform-origin: top
            }

            51% {
                transform: scaleY(1);
                transform-origin: bottom
            }

            100% {
                transform: scaleY(0);
                transform-origin: bottom
            }
        }

        /* ── MARQUEE ── */
        .marquee-wrap {
            position: relative;
            z-index: 2;
            background: var(--red);
            padding: 0.8rem 0;
            overflow: hidden
        }

        .marquee-track {
            display: flex;
            gap: 3rem;
            white-space: nowrap;
            animation: marquee 20s linear infinite
        }

        .marquee-item {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.05rem;
            letter-spacing: 4px;
            color: rgba(255, 255, 255, 0.92);
            display: flex;
            align-items: center;
            gap: 3rem
        }

        .marquee-item::after {
            content: '◆';
            color: rgba(255, 255, 255, 0.4);
            font-size: 0.45rem
        }

        @keyframes marquee {
            to {
                transform: translateX(-50%)
            }
        }

        /* ── STATS ── */
        .stats-section {
            position: relative;
            z-index: 2;
            padding: 5rem 4rem;
            background: var(--offwhite);
            border-bottom: 1px solid var(--border)
        }

        .stats-inner {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 1px;
            background: var(--border)
        }

        .stat-card {
            background: var(--white);
            padding: 3rem 2rem;
            text-align: center;
            position: relative;
            overflow: hidden;
            transition: background 0.3s
        }

        .stat-card::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--red), var(--orange));
            transform: scaleX(0);
            transition: transform 0.4s
        }

        .stat-card:hover {
            background: var(--offwhite)
        }

        .stat-card:hover::after {
            transform: scaleX(1)
        }

        .stat-num {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 4rem;
            letter-spacing: 2px;
            line-height: 1;
            background: linear-gradient(135deg, var(--red), var(--orange));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text
        }

        .stat-label {
            font-size: 0.65rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--muted);
            margin-top: 0.5rem
        }

        .stat-bar {
            width: 28px;
            height: 2px;
            background: var(--red);
            margin: 0.8rem auto 0;
            opacity: 0.4
        }

        /* ── ABOUT ── */
        .about-section {
            position: relative;
            z-index: 2;
            min-height: 90vh;
            display: grid;
            grid-template-columns: 1fr 1fr;
            overflow: hidden
        }

        .about-visual {
            position: relative;
            overflow: hidden
        }

        .about-img {
            width: 100%;
            height: 100%;
            min-height: 600px;
            object-fit: cover;
            filter: grayscale(20%) contrast(1.05);
            transition: filter 0.5s, transform 7s ease;
            display: block
        }

        .about-img:hover {
            filter: grayscale(0) contrast(1.1);
            transform: scale(1.03)
        }

        .about-img-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(to right, transparent 50%, var(--white));
            pointer-events: none
        }

        .about-tag {
            position: absolute;
            top: 2rem;
            left: 2rem;
            background: var(--red);
            color: #fff;
            padding: 0.5rem 1rem;
            font-size: 0.62rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            z-index: 2
        }

        .about-content {
            background: var(--white);
            padding: 5rem;
            display: flex;
            flex-direction: column;
            justify-content: center
        }

        .eyebrow {
            font-size: 0.63rem;
            font-weight: 700;
            letter-spacing: 5px;
            text-transform: uppercase;
            color: var(--red);
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.8rem
        }

        .eyebrow::before {
            content: '';
            display: inline-block;
            width: 24px;
            height: 1.5px;
            background: var(--red)
        }

        .section-h {
            font-family: 'Bebas Neue', sans-serif;
            font-size: clamp(2.8rem, 5vw, 4.5rem);
            letter-spacing: 2px;
            line-height: 0.92;
            margin-bottom: 1.5rem;
            color: var(--dark)
        }

        .section-h span {
            color: var(--red)
        }

        .about-body {
            font-size: 1rem;
            font-weight: 400;
            color: var(--muted);
            line-height: 1.9;
            margin-bottom: 2rem
        }

        .info-cards {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1px;
            background: var(--border);
            margin-top: 2rem
        }

        .info-card {
            background: var(--offwhite);
            padding: 1.5rem;
            transition: background 0.3s
        }

        .info-card:hover {
            background: var(--light)
        }

        .info-card-label {
            font-size: 0.58rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--red);
            margin-bottom: 0.4rem
        }

        .info-card-val {
            font-size: 0.88rem;
            line-height: 1.55;
            color: var(--dark)
        }


        /* ── FOUNDER ── */
        .founder-section {
            position: relative;
            z-index: 2;
            padding: 7rem 4rem;
            background: var(--white);
            border-bottom: 1px solid var(--border);
        }

        .founder-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1.2fr;
            gap: 6rem;
            align-items: center;
        }

        .founder-visual {
            position: relative;
            display: flex;
            justify-content: center;
        }

        .founder-img-frame {
            position: relative;
            width: 100%;
            max-width: 400px;
            aspect-ratio: 4 / 5;
        }

        .founder-img-wrap {
            position: relative;
            width: 100%;
            height: 100%;
            overflow: hidden;
            border: 1px solid var(--border);
            z-index: 1;
        }

        .founder-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: grayscale(20%) contrast(1.05);
            transition: filter 0.5s, transform 0.5s;
            z-index: 1;
            position: relative;
            transform: scale(1.18);
            opacity: 0; /* Starts hidden until curtain sweep */
        }

        .founder-img:hover {
            filter: grayscale(0) contrast(1.1);
        }

        .founder-curtain {
            position: absolute;
            inset: 0;
            background: linear-gradient(135deg, var(--red), var(--orange));
            z-index: 3;
            transform: scaleX(0);
            transform-origin: left;
        }

        .founder-sheen {
            position: absolute;
            inset: 0;
            background: radial-gradient(circle at var(--mx, 50%) var(--my, 50%), rgba(255, 255, 255, 0.45) 0%, transparent 60%);
            z-index: 2;
            pointer-events: none;
            mix-blend-mode: overlay;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        .founder-img-frame:hover .founder-sheen {
            opacity: 1;
        }

        .founder-img-accent {
            position: absolute;
            top: 1.5rem;
            left: -1.5rem;
            width: 100%;
            height: 100%;
            border: 2.5px solid var(--red);
            z-index: 0;
            transition: all 0.4s ease;
        }

        .founder-img-frame:hover .founder-img-accent {
            transform: translate(8px, -8px);
        }

        .founder-content {
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .founder-profile {
            margin-bottom: 1.5rem;
        }

        .founder-name {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2.5rem;
            letter-spacing: 2px;
            color: var(--dark);
            margin-bottom: 0.2rem;
        }

        .founder-title {
            font-size: 0.85rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--red);
        }

        .founder-quote {
            font-size: 1.1rem;
            font-style: italic;
            line-height: 1.8;
            color: var(--muted);
            border-left: 3px solid var(--red);
            padding-left: 1.5rem;
            margin-bottom: 2rem;
        }

        .founder-meta {
            display: flex;
            align-items: center;
            gap: 2rem;
        }

        .founder-experience {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .exp-num {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 3rem;
            color: var(--red);
            line-height: 1;
        }

        .exp-text {
            font-size: 0.75rem;
            font-weight: 700;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: var(--dark);
            max-width: 150px;
            line-height: 1.4;
        }

        @media(max-width:900px) {
            .founder-section {
                padding: 4rem 1.5rem;
            }
            .founder-container {
                grid-template-columns: 1fr;
                gap: 4rem;
            }
            .founder-img-accent {
                left: -1rem;
                top: 1rem;
            }
        }

        /* ── SERVICES ── */
        .services-section {
            position: relative;
            z-index: 2;
            padding: 7rem 4rem;
            background: var(--offwhite);
            overflow: hidden
        }

        .services-bg {
            position: absolute;
            inset: 0;
            background: url('https://images.unsplash.com/photo-1586528116311-ad8dd3c8310d?w=1920&q=50') center/cover no-repeat fixed;
            opacity: 0.03
        }

        .services-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            margin-bottom: 4rem;
            flex-wrap: wrap;
            gap: 2rem
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 1px;
            background: var(--border)
        }

        .svc-card {
            background: var(--white);
            overflow: hidden;
            position: relative;
            transition: transform 0.4s, box-shadow 0.4s
        }

        .svc-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.1)
        }

        .svc-img-wrap {
            width: 100%;
            height: 220px;
            overflow: hidden;
            position: relative
        }

        .svc-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: grayscale(40%) brightness(1.02);
            transition: transform 0.6s ease, filter 0.5s
        }

        .svc-card:hover .svc-img {
            transform: scale(1.07);
            filter: grayscale(0%)
        }

        .svc-img-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(to top, var(--white) 0%, rgba(255, 255, 255, 0.2) 55%, transparent 100%)
        }

        .svc-body {
            padding: 2rem
        }

        .svc-num {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 3.5rem;
            color: rgba(230, 51, 40, 0.1);
            line-height: 1;
            margin-bottom: 0.3rem
        }

        .svc-name {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.8rem;
            letter-spacing: 2px;
            margin-bottom: 0.5rem;
            color: var(--dark);
            transition: color 0.3s
        }

        .svc-card:hover .svc-name {
            color: var(--red)
        }

        .svc-desc {
            font-size: 0.88rem;
            color: var(--muted);
            line-height: 1.75;
            font-weight: 400
        }

        .svc-arrow {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            margin-top: 1.2rem;
            font-size: 0.68rem;
            font-weight: 700;
            letter-spacing: 2px;
            text-transform: uppercase;
            color: var(--red);
            opacity: 0;
            transform: translateX(-10px);
            transition: all 0.3s
        }

        .svc-card:hover .svc-arrow {
            opacity: 1;
            transform: translateX(0)
        }

        /* ── PARALLAX BANNER ── */
        .parallax-banner {
            position: relative;
            z-index: 2;
            height: 60vh;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center
        }

        .parallax-img {
            position: absolute;
            inset: -20%;
            background: url('https://images.unsplash.com/photo-1519003722824-194d4455a60c?w=1920&q=80') center/cover no-repeat;
            filter: brightness(0.28) contrast(1.3) saturate(0.5)
        }

        .parallax-content {
            position: relative;
            z-index: 2;
            text-align: center
        }

        .parallax-content h2 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: clamp(3rem, 8vw, 7rem);
            letter-spacing: 6px;
            line-height: 1;
            color: #fff
        }

        .parallax-content h2 span {
            color: var(--red)
        }

        .parallax-content p {
            font-size: 1rem;
            color: rgba(255, 255, 255, 0.45);
            letter-spacing: 2px;
            margin-top: 1rem;
            font-weight: 300
        }

        /* ── WHY US ── */
        .why-section {
            position: relative;
            z-index: 2;
            padding: 7rem 4rem;
            background: var(--white);
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 6rem;
            align-items: center
        }

        .why-visual {
            position: relative
        }

        .why-img {
            width: 100%;
            height: 500px;
            object-fit: cover;
            filter: contrast(1.05) saturate(0.85);
            display: block
        }

        .why-img-accent {
            position: absolute;
            bottom: -1.5rem;
            right: -1.5rem;
            width: 60%;
            height: 200px;
            border: 2px solid var(--red);
            z-index: -1
        }

        .why-counter {
            position: absolute;
            top: 2rem;
            right: -3rem;
            background: var(--red);
            color: #fff;
            padding: 1.5rem 2rem;
            text-align: center
        }

        .why-counter-num {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 3rem;
            line-height: 1
        }

        .why-counter-label {
            font-size: 0.58rem;
            letter-spacing: 2px;
            text-transform: uppercase;
            opacity: 0.85
        }

        .why-list {
            margin-top: 2.5rem;
            display: flex;
            flex-direction: column
        }

        .why-item {
            display: grid;
            grid-template-columns: 48px 1fr;
            gap: 1.2rem;
            align-items: start;
            padding: 1.5rem 0;
            border-bottom: 1px solid var(--border);
            cursor: pointer;
            transition: all 0.3s
        }

        .why-item:hover .why-icon {
            background: var(--red);
            color: #fff;
            border-color: var(--red)
        }

        .why-icon {
            width: 48px;
            height: 48px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.15rem;
            border: 1.5px solid var(--border);
            transition: all 0.3s;
            flex-shrink: 0;
            background: var(--offwhite)
        }

        .why-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.2rem;
            letter-spacing: 2px;
            margin-bottom: 0.2rem;
            color: var(--dark)
        }

        .why-desc {
            font-size: 0.85rem;
            color: var(--muted);
            line-height: 1.65;
            font-weight: 400
        }

        /* ── FLEET ── */
        .fleet-section {
            position: relative;
            z-index: 2;
            padding: 7rem 4rem;
            background: var(--offwhite)
        }

        .fleet-header {
            margin-bottom: 3rem
        }

        .fleet-slider {
            position: relative;
            overflow: hidden
        }

        .fleet-track {
            display: flex;
            gap: 1px;
            transition: transform 0.6s cubic-bezier(0.25, 0.46, 0.45, 0.94)
        }

        .fleet-card {
            flex: 0 0 calc(33.333% - 1px);
            background: var(--white);
            overflow: hidden;
            position: relative;
            border: 1px solid var(--border)
        }

        .fleet-img {
            width: 100%;
            height: 260px;
            object-fit: cover;
            filter: grayscale(30%) brightness(1.02);
            transition: filter 0.5s, transform 0.5s;
            display: block
        }

        .fleet-card:hover .fleet-img {
            filter: grayscale(0%);
            transform: scale(1.04)
        }

        .fleet-info {
            padding: 1.5rem
        }

        .fleet-type {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.4rem;
            letter-spacing: 2px;
            color: var(--dark)
        }

        .fleet-cap {
            font-size: 0.78rem;
            color: var(--muted);
            letter-spacing: 1px;
            font-weight: 400;
            margin-top: 0.2rem
        }

        .fleet-controls {
            display: flex;
            gap: 0.8rem;
            margin-top: 2rem
        }

        .fleet-btn {
            width: 48px;
            height: 48px;
            border: 1.5px solid var(--border);
            background: var(--white);
            color: var(--dark);
            font-size: 1rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.25s
        }

        .fleet-btn:hover {
            background: var(--red);
            border-color: var(--red);
            color: #fff
        }

        /* ── CONTACT ── */
        .contact-section {
            position: relative;
            z-index: 2;
            min-height: 100vh;
            display: grid;
            grid-template-columns: 1fr 1fr;
            overflow: hidden
        }

        .contact-visual {
            position: relative;
            overflow: hidden
        }

        .contact-bg {
            width: 100%;
            height: 100%;
            object-fit: cover;
            filter: grayscale(40%) brightness(0.38);
            position: absolute;
            inset: 0
        }

        .contact-visual-content {
            position: relative;
            z-index: 2;
            padding: 5rem;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            height: 100%
        }

        .contact-visual-content h2 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: clamp(2.5rem, 4vw, 4rem);
            letter-spacing: 3px;
            margin-bottom: 2rem;
            color: #fff;
            line-height: 1.05
        }

        .contact-details {
            display: flex;
            flex-direction: column;
            gap: 1.5rem
        }

        .contact-row {
            display: flex;
            align-items: flex-start;
            gap: 1rem
        }

        .c-icon {
            width: 40px;
            height: 40px;
            background: rgba(230, 51, 40, 0.2);
            border: 1px solid rgba(230, 51, 40, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.95rem;
            flex-shrink: 0
        }

        .c-label {
            font-size: 0.56rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--red);
            margin-bottom: 0.2rem
        }

        .c-val {
            font-size: 0.9rem;
            line-height: 1.6;
            color: rgba(255, 255, 255, 0.82)
        }

        .c-val a {
            color: rgba(255, 255, 255, 0.82);
            text-decoration: none;
            transition: color 0.2s
        }

        .c-val a:hover {
            color: var(--red)
        }

        /* form side — white */
        .contact-form-side {
            background: var(--white);
            padding: 5rem;
            display: flex;
            flex-direction: column;
            justify-content: center
        }

        .form-title {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2.2rem;
            letter-spacing: 3px;
            margin-bottom: 2rem;
            color: var(--dark)
        }

        .form-title span {
            color: var(--red)
        }

        .field {
            display: flex;
            flex-direction: column;
            gap: 0.35rem;
            margin-bottom: 1.2rem
        }

        .field label {
            font-size: 0.58rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--muted)
        }

        .field input,
        .field textarea,
        .field select {
            background: transparent;
            border: none;
            border-bottom: 1.5px solid var(--border);
            color: var(--dark);
            padding: 0.7rem 0;
            font-family: 'Rajdhani', sans-serif;
            font-size: 0.97rem;
            font-weight: 500;
            outline: none;
            transition: border-color 0.3s;
            resize: none;
            appearance: none;
            -webkit-appearance: none;
        }

        .field input:focus,
        .field textarea:focus,
        .field select:focus {
            border-bottom-color: var(--red)
        }

        .field input::placeholder,
        .field textarea::placeholder {
            color: var(--lightgray);
            font-weight: 300
        }

        .field select option {
            background: #fff;
            color: var(--dark)
        }

        .field textarea {
            height: 100px;
            padding-top: 0.7rem
        }

        .form-row-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1.5rem
        }

        .submit-btn {
            margin-top: 0.5rem;
            padding: 1rem 2.5rem;
            background: linear-gradient(135deg, var(--red), var(--orange));
            color: #fff;
            border: none;
            font-family: 'Rajdhani', sans-serif;
            font-size: 0.8rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            cursor: pointer;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
            clip-path: polygon(14px 0, 100% 0, calc(100% - 14px) 100%, 0 100%)
        }

        .submit-btn::before {
            content: '';
            position: absolute;
            inset: 0;
            background: rgba(255, 255, 255, 0.12);
            transform: translateX(-100%);
            transition: transform 0.4s ease
        }

        .submit-btn:hover::before {
            transform: translateX(0)
        }

        .submit-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 14px 32px rgba(230, 51, 40, 0.4)
        }

        /* ── GST STRIP ── */
        .gst-strip {
            position: relative;
            z-index: 2;
            background: var(--dark);
            padding: 1.3rem 4rem;
            display: flex;
            gap: 4rem;
            flex-wrap: wrap;
            align-items: center
        }

        .gst-item {
            display: flex;
            flex-direction: column;
            gap: 0.15rem
        }

        .gst-key {
            font-size: 0.53rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: #555
        }

        .gst-val {
            font-size: 0.82rem;
            font-weight: 600;
            letter-spacing: 1px;
            color: #ddd
        }

        /* ── FOOTER ── */
        footer {
            position: relative;
            z-index: 2;
            background: var(--white);
            padding: 3.5rem 4rem 2rem;
            border-top: 1.5px solid var(--border)
        }

        .footer-top {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            flex-wrap: wrap;
            gap: 2rem;
            padding-bottom: 2rem;
            border-bottom: 1px solid var(--border)
        }

        .footer-brand {
            max-width: 300px
        }

        .footer-name {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.8rem;
            letter-spacing: 4px;
            color: var(--red);
            margin-bottom: 0.7rem
        }

        .footer-tagline {
            font-size: 0.85rem;
            color: var(--muted);
            line-height: 1.75;
            font-weight: 400
        }

        .footer-links h4 {
            font-size: 0.6rem;
            font-weight: 700;
            letter-spacing: 3px;
            text-transform: uppercase;
            color: var(--red);
            margin-bottom: 1rem
        }

        .footer-links ul {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 0.5rem
        }

        .footer-links a {
            text-decoration: none;
            color: var(--muted);
            font-size: 0.9rem;
            transition: color 0.2s
        }

        .footer-links a:hover {
            color: var(--red)
        }

        .footer-bottom {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 1.5rem;
            flex-wrap: wrap;
            gap: 1rem
        }

        .footer-copy {
            font-size: 0.7rem;
            color: var(--muted);
            letter-spacing: 0.5px
        }

        /* ── TOAST ── */
        #toast {
            position: fixed;
            bottom: 2.5rem;
            right: 2.5rem;
            background: linear-gradient(135deg, var(--red), var(--orange));
            color: #fff;
            padding: 1rem 2rem;
            font-size: 0.8rem;
            font-weight: 700;
            letter-spacing: 1.5px;
            z-index: 9999;
            transform: translateY(80px);
            opacity: 0;
            transition: all 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
            pointer-events: none;
            clip-path: polygon(12px 0, 100% 0, calc(100% - 12px) 100%, 0 100%);
            box-shadow: 0 8px 24px rgba(230, 51, 40, 0.35)
        }

        #toast.show {
            transform: translateY(0);
            opacity: 1
        }

        /* ── REVEAL ── */
        .reveal {
            opacity: 0;
            transform: translateY(36px)
        }

        /* ── RESPONSIVE ── */
        @media(max-width:900px) {
            nav {
                padding: 1rem 1.5rem
            }

            .nav-links {
                display: none
            }

            .hero-content {
                padding: 0 1.5rem
            }

            .about-section,
            .why-section {
                grid-template-columns: 1fr
            }

            .services-section,
            .fleet-section {
                padding: 4rem 1.5rem
            }

            .services-grid {
                grid-template-columns: 1fr
            }

            .why-counter {
                right: 0
            }

            .fleet-card {
                flex: 0 0 82%
            }

            .contact-section {
                grid-template-columns: 1fr
            }

            .contact-visual {
                min-height: 380px
            }

            .contact-form-side {
                padding: 3rem 1.5rem
            }

            .contact-visual-content {
                padding: 3rem 1.5rem
            }

            .stats-inner {
                grid-template-columns: 1fr 1fr
            }

            .gst-strip {
                padding: 1rem 1.5rem;
                gap: 2rem
            }

            footer {
                padding: 2.5rem 1.5rem
            }

            .footer-top {
                flex-direction: column
            }

            .about-content {
                padding: 3rem 1.5rem
            }

            .why-section {
                padding: 4rem 1.5rem;
                gap: 3rem
            }

            .stats-section {
                padding: 4rem 1.5rem
            }
        }
    </style>
</head>

<body>

    <div id="cursor"></div>
    <div id="cursor-ring"></div>
    <canvas id="particles"></canvas>
    <canvas id="three-canvas"></canvas>

    <!-- LOADER -->
    <div id="loader">
        <div class="loader-logo">ASATHIYA TRANSPORTS</div>
        <div class="loader-bar-wrap">
            <div class="loader-bar" id="loaderBar"></div>
        </div>
        <div class="loader-pct" id="loaderPct">0%</div>
    </div>

    <!-- NAV -->
    <nav id="mainNav">
        <div class="nav-logo">
            <img src="logo.png" alt="Asathiya Transports Logo" class="logo-img" />
            ASATHIYA
        </div>
        <ul class="nav-links">
            <li><a href="#about">About</a></li>
            <li><a href="#founder">Founder</a></li>
            <li><a href="#services">Services</a></li>
            <li><a href="#fleet">Fleet</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
        <a href="#contact" class="nav-cta">Get Quote →</a>
    </nav>

    <!-- HERO -->
    <section class="hero" id="hero">
        <div class="hero-slides">
            <div class="hero-slide active"
                style="background-image:url('truck2.png')">
            </div>
            <div class="hero-slide"
                style="background-image:url('https://images.unsplash.com/photo-1508780709619-79562169bc64?w=1920&q=85')">
            </div>
            <div class="hero-slide"
                style="background-image:url('https://images.unsplash.com/photo-1532300964467-9be00eb5f671?w=1920&q=85')">
            </div>
        </div>
        <div class="hero-overlay"></div>
        <div class="hero-grid"></div>
        <div class="hero-content">
            <div class="hero-badge" id="heroBadge"><span class="badge-dot"></span> Tamil Nadu's Trusted Freight Partner
            </div>
            <h1 class="hero-title">
                <span class="line" id="hline1">ASATHIYA</span>
                <span class="line stroke" id="hline2">TRANS</span>
                <span class="line red" id="hline3">PORTS</span>
            </h1>
            <p class="hero-subtitle" id="heroSub">Premium road freight from Tirunelveli District — delivering cargo
                across India with precision, speed, and trust.</p>
            <div class="hero-actions" id="heroActions">
                <a href="#contact" class="btn btn-fire">🚛 Get Instant Quote</a>
                <a href="#services" class="btn btn-ghost">Explore Services</a>
            </div>
        </div>
        <div class="hero-scroll">
            <span class="scroll-label">Scroll</span>
            <div class="scroll-line"></div>
        </div>
    </section>

    <!-- MARQUEE -->
    <div class="marquee-wrap">
        <div class="marquee-track">
            <div class="marquee-item">Full Truck Load</div>
            <div class="marquee-item">Part Load LTL</div>
            <div class="marquee-item">Pan-India Freight</div>
            <div class="marquee-item">Express Delivery</div>
            <div class="marquee-item">Tirunelveli District</div>
            <div class="marquee-item">Tamil Nadu 627 110</div>
            <div class="marquee-item">GST Registered</div>
            <div class="marquee-item">24 / 7 Support</div>
            <div class="marquee-item">Full Truck Load</div>
            <div class="marquee-item">Part Load LTL</div>
            <div class="marquee-item">Pan-India Freight</div>
            <div class="marquee-item">Express Delivery</div>
            <div class="marquee-item">Tirunelveli District</div>
            <div class="marquee-item">Tamil Nadu 627 110</div>
            <div class="marquee-item">GST Registered</div>
            <div class="marquee-item">24 / 7 Support</div>
        </div>
    </div>

    <!-- STATS -->
    <div class="stats-section">
        <div class="stats-inner">
            <div class="stat-card">
                <div class="stat-num" data-target="10" data-suffix="+">0</div>
                <div class="stat-label">Years of Service</div>
                <div class="stat-bar"></div>
            </div>
            <div class="stat-card">
                <div class="stat-num" data-target="500" data-suffix="+">0</div>
                <div class="stat-label">Loads Delivered</div>
                <div class="stat-bar"></div>
            </div>
            <div class="stat-card">
                <div class="stat-num" data-target="24" data-suffix="/7">0</div>
                <div class="stat-label">Customer Support</div>
                <div class="stat-bar"></div>
            </div>
            <div class="stat-card">
                <div class="stat-num" data-target="15" data-suffix="+ States">0</div>
                <div class="stat-label">Coverage Area</div>
                <div class="stat-bar"></div>
            </div>
        </div>
    </div>

    <!-- ABOUT -->
    <section class="about-section" id="about">
        <div class="about-visual">
            <img class="about-img" src="5truck.png"
                alt="Truck on highway" loading="lazy" />
            <div class="about-img-overlay"></div>
            <div class="about-tag">Est. Nanguneri Taluk</div>
        </div>
        <div class="about-content">
            <div class="eyebrow reveal">Who We Are</div>
            <h2 class="section-h reveal">MOVING<br>INDIA'S<br><span>CARGO</span></h2>
            <p class="about-body reveal">Asathiya Transports is a GST-registered freight carrier headquartered in Anna
                Nagar, Elankulam Post, Nanguneri Taluk, Tirunelveli District. We connect businesses across Tamil Nadu
                and beyond with dependable, professional road logistics built on years of trust.</p>
            <div class="info-cards reveal">
                <div class="info-card">
                    <div class="info-card-label">Registered Address</div>
                    <div class="info-card-val">No. 184–1/3, Main Road, Anna Nagar, Elankulam Post, Nanguneri Taluk,
                        Tirunelveli Dist. TN – 627 110</div>
                </div>
                <div class="info-card">
                    <div class="info-card-label">PAN Number</div>
                    <div class="info-card-val">AWWPV7253P</div><br>
                    <div class="info-card-label">GST IN</div>
                    <div class="info-card-val">33AWWPV7253P22A</div>
                </div>
            </div>
        </div>
    </section>

    <!-- FOUNDER -->
    <section class="founder-section" id="founder">
        <div class="founder-container">
            <div class="founder-visual">
                <div class="founder-img-frame">
                    <div class="founder-img-accent"></div>
                    <div class="founder-img-wrap">
                        <div class="founder-curtain"></div>
                        <div class="founder-sheen"></div>
                        <img class="founder-img" src="founder.jpeg" alt="Asathiya Mani - Founder" loading="lazy" />
                    </div>
                </div>
            </div>
            <div class="founder-content">
                <div class="eyebrow" style="opacity: 0;">Leadership</div>
                <h2 class="section-h" style="opacity: 0;">MEET OUR <span>FOUNDER</span></h2>
                <div class="founder-profile" style="opacity: 0;">
                    <h3 class="founder-name">Asathiya Mani</h3>
                    <div class="founder-title">Founder & Managing Director</div>
                </div>
                <blockquote class="founder-quote" style="opacity: 0;">
                    "Since our inception, our mission has been simple: to deliver cargo with absolute integrity, speed, and safety. We don't just move freight; we build lasting relationships with every business we serve, ensuring that South Tamil Nadu is connected seamlessly to the rest of India."
                </blockquote>
                <div class="founder-meta" style="opacity: 0;">
                    <div class="founder-experience">
                        <span class="exp-num stat-num" data-target="30" data-suffix="+">0</span>
                        <span class="exp-text">Years of Logistics Experience</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- SERVICES -->
    <section class="services-section" id="services">
        <div class="services-bg"></div>
        <div class="services-header">
            <div>
                <div class="eyebrow reveal">What We Do</div>
                <h2 class="section-h reveal">OUR <span>SERVICES</span></h2>
            </div>
            <p class="reveal" style="max-width:340px;color:var(--muted);font-size:0.92rem;line-height:1.8">Comprehensive
                freight solutions tailored for businesses of all sizes across India.</p>
        </div>
        <div class="services-grid">
            <div class="svc-card reveal">
                <div class="svc-img-wrap"><img class="svc-img"
                        src="truck2.png" alt="FTL"
                        loading="lazy" />
                    <div class="svc-img-overlay"></div>
                </div>
                <div class="svc-body">
                    <div class="svc-num">01</div>
                    <div class="svc-name">Full Truck Load</div>
                    <p class="svc-desc">End-to-end FTL transport for large consignments. Dedicated vehicle allocation
                        with direct point-to-point delivery and real-time tracking.</p>
                    <div class="svc-arrow">Learn More →</div>
                </div>
            </div>
            <div class="svc-card reveal">
                <div class="svc-img-wrap"><img class="svc-img"
                        src="5truck.png" alt="LTL"
                        loading="lazy" />
                    <div class="svc-img-overlay"></div>
                </div>
                <div class="svc-body">
                    <div class="svc-num">02</div>
                    <div class="svc-name">Part Load / LTL</div>
                    <p class="svc-desc">Cost-effective movement for smaller shipments consolidated across routes. Ideal
                        for SMEs needing flexible, economical freight solutions.</p>
                    <div class="svc-arrow">Learn More →</div>
                </div>
            </div>
            <div class="svc-card reveal">
                <div class="svc-img-wrap"><img class="svc-img"
                        src="truck3.png" alt="Pan-India"
                        loading="lazy" />
                    <div class="svc-img-overlay"></div>
                </div>
                <div class="svc-body">
                    <div class="svc-num">03</div>
                    <div class="svc-name">Pan-India Freight</div>
                    <p class="svc-desc">Interstate logistics covering Tamil Nadu and connecting major hubs across all
                        Indian states with reliable scheduling.</p>
                    <div class="svc-arrow">Learn More →</div>
                </div>
            </div>
            <div class="svc-card reveal">
                <div class="svc-img-wrap"><img class="svc-img"
                        src="truck1.png" alt="Express"
                        loading="lazy" />
                    <div class="svc-img-overlay"></div>
                </div>
                <div class="svc-body">
                    <div class="svc-num">04</div>
                    <div class="svc-name">Express Delivery</div>
                    <p class="svc-desc">Time-critical shipments handled with priority routing. 24/7 support and
                        dedicated dispatch for urgent cargo requirements.</p>
                    <div class="svc-arrow">Learn More →</div>
                </div>
            </div>
        </div>
    </section>

    <!-- PARALLAX BANNER -->
    <div class="parallax-banner">
        <div class="parallax-img" id="parallaxImg"></div>
        <div class="parallax-content">
            <h2 class="reveal">ON TIME.<br><span>EVERY TIME.</span></h2>
            <p class="reveal">Tirunelveli · Tamil Nadu · India</p>
        </div>
    </div>

    <!-- WHY US -->
    <section class="why-section" id="why">
        <div class="why-visual reveal">
            <img class="why-img" src="truck3.png"
                alt="Logistics warehouse" loading="lazy" />
            <div class="why-img-accent"></div>
            <div class="why-counter">
                <div class="why-counter-num">100%</div>
                <div class="why-counter-label">Delivery Success</div>
            </div>
        </div>
        <div>
            <div class="eyebrow reveal">Why Choose Us</div>
            <h2 class="section-h reveal">THE ASATHIYA<br><span>ADVANTAGE</span></h2>
            <div class="why-list">
                <div class="why-item reveal">
                    <div class="why-icon">🛡️</div>
                    <div>
                        <div class="why-title">Fully GST Registered</div>
                        <p class="why-desc">Compliant with all Indian tax regulations. GST IN: 33AWWPV7253P22A —
                            seamless B2B invoicing for all clients.</p>
                    </div>
                </div>
                <div class="why-item reveal">
                    <div class="why-icon">📍</div>
                    <div>
                        <div class="why-title">Local Expertise</div>
                        <p class="why-desc">Deep knowledge of South Tamil Nadu routes, especially Tirunelveli,
                            Tuticorin, and surrounding districts.</p>
                    </div>
                </div>
                <div class="why-item reveal">
                    <div class="why-icon">⚡</div>
                    <div>
                        <div class="why-title">Fast Dispatch</div>
                        <p class="why-desc">Same-day booking confirmation with trucks dispatched within hours of order
                            placement.</p>
                    </div>
                </div>
                <div class="why-item reveal">
                    <div class="why-icon">📞</div>
                    <div>
                        <div class="why-title">24/7 Reachability</div>
                        <p class="why-desc">Two direct lines always open. Dedicated support for tracking updates and
                            urgent changes.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- FLEET -->
    <section class="fleet-section" id="fleet">
        <div class="fleet-header">
            <div class="eyebrow reveal">Our Fleet</div>
            <h2 class="section-h reveal">BUILT TO <span>DELIVER</span></h2>
        </div>
        <div class="fleet-slider">
            <div class="fleet-track" id="fleetTrack">
                <div class="fleet-card"><img class="fleet-img"
                        src="truck2.png" alt="Heavy Truck"
                        loading="lazy" />
                    <div class="fleet-info">
                        <div class="fleet-type">Heavy Trucks</div>
                        <div class="fleet-cap">20–40 Ton Capacity · FTL Specialist</div>
                    </div>
                </div>
                <div class="fleet-card"><img class="fleet-img"
                        src="truck1.png" alt="Medium"
                        loading="lazy" />
                    <div class="fleet-info">
                        <div class="fleet-type">Medium Carriers</div>
                        <div class="fleet-cap">8–15 Ton · Versatile Freight</div>
                    </div>
                </div>
                <div class="fleet-card"><img class="fleet-img"
                        src="5truck.png" alt="Light"
                        loading="lazy" />
                    <div class="fleet-info">
                        <div class="fleet-type">Light Commercial</div>
                        <div class="fleet-cap">1–5 Ton · Express & Part Load</div>
                    </div>
                </div>
                <div class="fleet-card"><img class="fleet-img"
                        src="truck3.png" alt="Refrigerated"
                        loading="lazy" />
                    <div class="fleet-info">
                        <div class="fleet-type">Refrigerated Units</div>
                        <div class="fleet-cap">Temperature Controlled · Perishables</div>
                    </div>
                </div>
            </div>
        </div>
        <div class="fleet-controls">
            <button class="fleet-btn" id="prevBtn">←</button>
            <button class="fleet-btn" id="nextBtn">→</button>
        </div>
    </section>

    <!-- CONTACT -->
    <section class="contact-section" id="contact">
        <div class="contact-visual">
            <img class="contact-bg" src="5truck.png"
                alt="Transport" loading="lazy" />
            <div class="contact-visual-content">
                <h2>LET'S<br>MOVE YOUR<br><span style="color:var(--red)">CARGO.</span></h2>
                <div class="contact-details">
                    <div class="contact-row">
                        <div class="c-icon">📍</div>
                        <div>
                            <div class="c-label">Address</div>
                            <div class="c-val">No. 184–1/3, Main Road, Anna Nagar, Elankulam Post, Nanguneri Taluk,
                                Tirunelveli District, Tamil Nadu – 627 110</div>
                        </div>
                    </div>
                    <div class="contact-row">
                        <div class="c-icon">📞</div>
                        <div>
                            <div class="c-label">Mobile</div>
                            <div class="c-val"><a href="tel:9976731444">+91 99767 31444</a><br><a
                                    href="tel:9788748900">+91 97887 48900</a></div>
                        </div>
                    </div>
                    <div class="contact-row">
                        <div class="c-icon">✉️</div>
                        <div>
                            <div class="c-label">Email</div>
                            <div class="c-val"><a href="mailto:asathiyamani1969@gmail.com"
                                    style="color:var(--red)">asathiyamani1969@gmail.com</a></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="contact-form-side">
            <div class="form-title reveal">REQUEST A<br><span>QUOTE</span></div>
            <form id="quoteForm">
                <div class="form-row-2">
                    <div class="field"><label>Your Name</label><input type="text" placeholder="Full name" required />
                    </div>
                    <div class="field"><label>Phone</label><input type="tel" placeholder="+91 XXXXX XXXXX" required />
                    </div>
                </div>
                <div class="field"><label>Email</label><input type="email" placeholder="your@email.com" /></div>
                <div class="field"><label>Service Required</label>
                    <select>
                        <option value="">— Choose Service —</option>
                        <option>Full Truck Load (FTL)</option>
                        <option>Part Load / LTL</option>
                        <option>Pan-India Freight</option>
                        <option>Express Delivery</option>
                    </select>
                </div>
                <div class="form-row-2">
                    <div class="field"><label>From (City)</label><input type="text" placeholder="Origin" /></div>
                    <div class="field"><label>To (City)</label><input type="text" placeholder="Destination" /></div>
                </div>
                <div class="field"><label>Message</label><textarea
                        placeholder="Cargo type, weight, special requirements…"></textarea></div>
                <button type="submit" class="submit-btn">Send Enquiry 🚛</button>
            </form>
        </div>
    </section>

    <!-- GST STRIP -->
    <div class="gst-strip">
        <div class="gst-item">
            <div class="gst-key">PAN Card No.</div>
            <div class="gst-val">AWWPV7253P</div>
        </div>
        <div class="gst-item">
            <div class="gst-key">GST Identification No.</div>
            <div class="gst-val">33AWWPV7253P22A</div>
        </div>
        <div class="gst-item">
            <div class="gst-key">State Code</div>
            <div class="gst-val">Tamil Nadu — 33</div>
        </div>
        <div class="gst-item">
            <div class="gst-key">District</div>
            <div class="gst-val">Tirunelveli</div>
        </div>
    </div>

    <!-- FOOTER -->
    <footer>
        <div class="footer-top">
            <div class="footer-brand">
                <div class="footer-name" style="display:flex; align-items:center; gap:0.6rem;">
                    <img src="logo.png" alt="Logo" class="logo-img" style="height:32px;" />
                    Asathiya Transports
                </div>
                <p class="footer-tagline">Premium road freight solutions from the heart of Tamil Nadu. Connecting cargo
                    to destinations across India with reliability and care.</p>
            </div>
            <div class="footer-links">
                <h4>Navigation</h4>
                <ul>
                    <li><a href="#about">About Us</a></li>
                    <li><a href="#founder">Our Founder</a></li>
                    <li><a href="#services">Our Services</a></li>
                    <li><a href="#fleet">Our Fleet</a></li>
                    <li><a href="#contact">Contact</a></li>
                </ul>
            </div>
            <div class="footer-links">
                <h4>Contact</h4>
                <ul>
                    <li><a href="tel:9976731444">+91 99767 31444</a></li>
                    <li><a href="tel:9788748900">+91 97887 48900</a></li>
                    <li><a href="mailto:asathiyamani1969@gmail.com">asathiyamani1969@gmail.com</a></li>
                </ul>
            </div>
        </div>
        <div class="footer-bottom">
            <div class="footer-copy">© 2026 Asathiya Transports. All Rights Reserved. | GST: 33AWWPV7253P22A</div>
            <div class="footer-copy">Nanguneri Taluk · Tirunelveli · Tamil Nadu 627 110</div>
        </div>
    </footer>

    <div id="toast">✔ Enquiry sent! We'll contact you shortly.</div>

    <script>
        /* ── CURSOR ── */
        const cur = document.getElementById('cursor'), ring = document.getElementById('cursor-ring');
        let mx = 0, my = 0, rx = 0, ry = 0;
        document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cur.style.left = mx + 'px'; cur.style.top = my + 'px' });
        setInterval(() => { rx += (mx - rx) * 0.13; ry += (my - ry) * 0.13; ring.style.left = rx + 'px'; ring.style.top = ry + 'px' }, 16);
        document.querySelectorAll('a,button,.svc-card,.why-item,.fleet-card,.founder-img-frame,.founder-experience').forEach(el => {
            el.addEventListener('mouseenter', () => { cur.style.width = '26px'; cur.style.height = '26px'; ring.style.width = '58px'; ring.style.height = '58px' });
            el.addEventListener('mouseleave', () => { cur.style.width = '12px'; cur.style.height = '12px'; ring.style.width = '40px'; ring.style.height = '40px' });
        });

        /* ── LOADER ── */
        const bar = document.getElementById('loaderBar'), pctEl = document.getElementById('loaderPct'), logoEl = document.querySelector('.loader-logo');
        let p = 0;
        gsap.to(logoEl, { opacity: 1, duration: 0.9, ease: 'power2.out' });
        const lt = setInterval(() => {
            p += Math.random() * 4 + 1.5; if (p >= 100) { p = 100; clearInterval(lt); setTimeout(() => { gsap.to('#loader', { opacity: 0, duration: 0.75, onComplete: () => { document.getElementById('loader').style.display = 'none'; boot() } }) }, 400) }
            bar.style.width = p + '%'; pctEl.textContent = Math.round(p) + '%';
        }, 55);

        /* ── BOOT HERO ── */
        function boot() {
            gsap.from('#heroBadge', { y: 28, opacity: 0, duration: 0.8, ease: 'power3.out' });
            gsap.from(['#hline1', '#hline2', '#hline3'], { y: 70, opacity: 0, stagger: 0.12, duration: 0.9, delay: 0.18, ease: 'power3.out' });
            gsap.from('#heroSub', { y: 18, opacity: 0, duration: 0.8, delay: 0.6, ease: 'power2.out' });
            gsap.from('#heroActions', { y: 18, opacity: 0, duration: 0.8, delay: 0.78, ease: 'power2.out' });
        }

        /* ── HERO SLIDESHOW ── */
        const slides = document.querySelectorAll('.hero-slide');
        let si = 0;
        setInterval(() => { slides[si].classList.remove('active'); si = (si + 1) % slides.length; slides[si].classList.add('active') }, 5500);

        /* ── NAV SCROLL ── */
        window.addEventListener('scroll', () => document.getElementById('mainNav').classList.toggle('scrolled', scrollY > 60));

        /* ── GSAP ── */
        gsap.registerPlugin(ScrollTrigger);
        document.querySelectorAll('.reveal').forEach(el => {
            gsap.fromTo(el, { y: 38, opacity: 0 }, { y: 0, opacity: 1, duration: 0.75, ease: 'power3.out', scrollTrigger: { trigger: el, start: 'top 88%', toggleActions: 'play none none none' } });
        });

        /* ── STAT COUNTERS ── */
        document.querySelectorAll('.stat-num[data-target]').forEach(el => {
            ScrollTrigger.create({
                trigger: el, start: 'top 85%', once: true, onEnter: () => {
                    const t = +el.dataset.target, s = el.dataset.suffix || '';
                    const o = { v: 0 };
                    gsap.to(o, { v: t, duration: 1.8, ease: 'power2.out', onUpdate: () => el.textContent = Math.round(o.v) + s });
                }
            });
        });

        /* ── PARALLAX ── */
        gsap.to('#parallaxImg', { yPercent: 26, ease: 'none', scrollTrigger: { trigger: '.parallax-banner', scrub: true } });

        /* ── FOUNDER ADVANCED ANIMATION ── */
        // Reveal elements inside founder section with custom stagger, curtains, and zooms
        gsap.timeline({
            scrollTrigger: {
                trigger: '#founder',
                start: 'top 70%',
                toggleActions: 'play none none none'
            }
        })
        .to('.founder-curtain', { scaleX: 1, duration: 0.6, ease: 'power2.inOut' })
        .set('.founder-img', { opacity: 1 })
        .to('.founder-curtain', { xPercent: 101, duration: 0.6, ease: 'power2.inOut' })
        .fromTo('.founder-img', { scale: 1.18 }, { scale: 1, duration: 1.4, ease: 'power2.out' }, '-=0.5')
        .fromTo('.founder-img-accent', { x: 50, y: -50, opacity: 0 }, { x: 0, y: 0, opacity: 1, duration: 1.2, ease: 'power3.out' }, '-=1.2')
        .fromTo('.founder-content .eyebrow', { y: 24, opacity: 0 }, { y: 0, opacity: 1, duration: 0.7, ease: 'power2.out' }, '-=0.9')
        .fromTo('.founder-content .section-h', { y: 36, opacity: 0 }, { y: 0, opacity: 1, duration: 0.9, ease: 'power3.out' }, '-=0.7')
        .fromTo('.founder-profile', { x: -24, opacity: 0 }, { x: 0, opacity: 1, duration: 0.7, ease: 'power2.out' }, '-=0.6')
        .fromTo('.founder-quote', { borderLeftWidth: 0, x: -16, opacity: 0 }, { borderLeftWidth: 3, x: 0, opacity: 1, duration: 0.9, ease: 'power2.out' }, '-=0.5')
        .fromTo('.founder-meta', { y: 20, opacity: 0 }, { y: 0, opacity: 1, duration: 0.7, ease: 'power2.out' }, '-=0.4');

        // Interactive mousemove 3D perspective and radial sheen glow
        const founderFrame = document.querySelector('.founder-img-frame');
        const founderImgWrap = document.querySelector('.founder-img-wrap');
        const founderImg = document.querySelector('.founder-img');
        const founderAccent = document.querySelector('.founder-img-accent');
        const founderSheen = document.querySelector('.founder-sheen');
        
        if (founderFrame) {
            founderFrame.addEventListener('mousemove', e => {
                const rect = founderFrame.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;
                
                const tiltX = (x - rect.width/2) * 0.08;
                const tiltY = (y - rect.height/2) * 0.08;
                
                // Track sheen coordinates
                founderSheen.style.setProperty('--mx', `${(x / rect.width) * 100}%`);
                founderSheen.style.setProperty('--my', `${(y / rect.height) * 100}%`);
                
                // 3D transform on the image wrapper
                gsap.to(founderImgWrap, {
                    rotateY: tiltX,
                    rotateX: -tiltY,
                    x: (x - rect.width/2) * 0.03,
                    y: (y - rect.height/2) * 0.03,
                    duration: 0.4,
                    ease: 'power2.out',
                    transformPerspective: 1000
                });
                
                // Parallax shift for accent borders
                gsap.to(founderAccent, {
                    x: -(x - rect.width/2) * 0.08,
                    y: -(y - rect.height/2) * 0.08,
                    duration: 0.4,
                    ease: 'power2.out'
                });
            });
            
            founderFrame.addEventListener('mouseleave', () => {
                gsap.to(founderImgWrap, {
                    rotateY: 0,
                    rotateX: 0,
                    x: 0,
                    y: 0,
                    duration: 0.8,
                    ease: 'power3.out'
                });
                gsap.to(founderAccent, {
                    x: 0,
                    y: 0,
                    duration: 0.8,
                    ease: 'power3.out'
                });
            });
        }

        /* ── FLEET SLIDER ── */
        let fp = 0;
        const ft = document.getElementById('fleetTrack');
        const cw = () => ft.children[0].offsetWidth + 1;
        document.getElementById('nextBtn').addEventListener('click', () => {
            const max = ft.children.length - Math.floor(ft.parentElement.offsetWidth / cw());
            if (fp < max) { fp++; ft.style.transform = `translateX(-${fp * cw()}px)` }
        });
        document.getElementById('prevBtn').addEventListener('click', () => {
            if (fp > 0) { fp--; ft.style.transform = `translateX(-${fp * cw()}px)` }
        });

        /* ── FORM ── */
        document.getElementById('quoteForm').addEventListener('submit', function (e) {
            e.preventDefault();
            const t = document.getElementById('toast');
            t.classList.add('show'); setTimeout(() => t.classList.remove('show'), 3800);
            this.reset();
        });

        /* ── SMOOTH SCROLL ── */
        document.querySelectorAll('a[href^="#"]').forEach(a => a.addEventListener('click', e => { e.preventDefault(); document.querySelector(a.getAttribute('href'))?.scrollIntoView({ behavior: 'smooth', block: 'start' }) }));

        /* ── PARTICLES ── */
        (function () {
            const c = document.getElementById('particles'), ctx = c.getContext('2d');
            let W, H, pts = [];
            const resize = () => { W = c.width = innerWidth; H = c.height = innerHeight };
            resize(); window.addEventListener('resize', resize);
            for (let i = 0; i < 55; i++) pts.push({ x: Math.random() * innerWidth, y: Math.random() * innerHeight, vx: (Math.random() - .5) * .35, vy: (Math.random() - .5) * .35, r: Math.random() * 1.4 + .4, a: Math.random() });
            (function draw() {
                ctx.clearRect(0, 0, W, H);
                pts.forEach(p => {
                    p.x += p.vx; p.y += p.vy;
                    if (p.x < 0) p.x = W; if (p.x > W) p.x = 0;
                    if (p.y < 0) p.y = H; if (p.y > H) p.y = 0;
                    ctx.beginPath(); ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(230,51,40,${p.a * .35})`; ctx.fill();
                });
                for (let i = 0; i < pts.length; i++) for (let j = i + 1; j < pts.length; j++) {
                    const dx = pts[i].x - pts[j].x, dy = pts[i].y - pts[j].y, d = Math.sqrt(dx * dx + dy * dy);
                    if (d < 110) { ctx.beginPath(); ctx.moveTo(pts[i].x, pts[i].y); ctx.lineTo(pts[j].x, pts[j].y); ctx.strokeStyle = `rgba(230,51,40,${(1 - d / 110) * .07})`; ctx.lineWidth = .5; ctx.stroke() }
                }
                requestAnimationFrame(draw);
            })();
        })();

        /* ── THREE.JS ── */
        (function () {
            try {
                const c = document.getElementById('three-canvas');
                const r = new THREE.WebGLRenderer({ canvas: c, alpha: true, antialias: true });
                r.setSize(innerWidth, innerHeight); r.setPixelRatio(Math.min(devicePixelRatio, 2));
                const scene = new THREE.Scene(), cam = new THREE.PerspectiveCamera(60, innerWidth / innerHeight, .1, 100);
                cam.position.z = 3;
                const m1 = new THREE.Mesh(new THREE.TorusKnotGeometry(.85, .25, 110, 14), new THREE.MeshBasicMaterial({ color: 0xe63328, wireframe: true, opacity: .1, transparent: true }));
                m1.position.set(4, -.5, 0); scene.add(m1);
                const m2 = new THREE.Mesh(new THREE.IcosahedronGeometry(1.1, 1), new THREE.MeshBasicMaterial({ color: 0xf57c2b, wireframe: true, opacity: .06, transparent: true }));
                m2.position.set(-4, 1, 0); scene.add(m2);
                window.addEventListener('resize', () => { r.setSize(innerWidth, innerHeight); cam.aspect = innerWidth / innerHeight; cam.updateProjectionMatrix() });
                (function a() { requestAnimationFrame(a); m1.rotation.x += .003; m1.rotation.y += .005; m2.rotation.x -= .002; m2.rotation.y += .003; r.render(scene, cam) })();
            } catch (e) { }
        })();
    </script>
</body>

</html>
