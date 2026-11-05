<!DOCTYPE html>
<html lang="pt-BR">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SiteLab — Sistemas e sites sob medida</title>
    <meta name="description"
        content="A SiteLab projeta e constrói sites, lojas virtuais e sistemas sob medida para empresas que querem crescer com tecnologia confiável.">

    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link
        href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap"
        rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

    <style>
        :root {
            --bg: #080B14;
            --bg-panel: #0F1526;
            --bg-panel-2: #131B31;
            --primary: #00D9C0;
            --primary-dark: #06231F;
            --secondary: #FFB454;
            --text: #E8ECF4;
            --text-dim: #8B95AC;
            --text-faint: #5C6478;
            --border: rgba(232, 236, 244, 0.09);
            --border-strong: rgba(232, 236, 244, 0.16);
            --radius-sm: 8px;
            --radius-md: 14px;
            --radius-lg: 22px;
            --container: 1180px;
            --shadow-glow: 0 0 40px rgba(0, 217, 192, 0.18);
        }

        *,
        *::before,
        *::after {
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
        }

        @media (prefers-reduced-motion: reduce) {
            html {
                scroll-behavior: auto;
            }

            *,
            *::before,
            *::after {
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
            }
        }

        body {
            margin: 0;
            background: var(--bg);
            color: var(--text);
            font-family: 'Inter', system-ui, sans-serif;
            line-height: 1.6;
            -webkit-font-smoothing: antialiased;
            overflow-x: hidden;
        }

        img {
            max-width: 100%;
            display: block;
        }

        a {
            color: inherit;
            text-decoration: none;
        }

        button {
            font-family: inherit;
            cursor: pointer;
        }

        ul {
            margin: 0;
            padding: 0;
            list-style: none;
        }

        h1,
        h2,
        h3,
        h4 {
            font-family: 'Space Grotesk', sans-serif;
            margin: 0;
            font-weight: 600;
            letter-spacing: -0.01em;
        }

        p {
            margin: 0;
        }

        :focus-visible {
            outline: 2px solid var(--primary);
            outline-offset: 3px;
            border-radius: 4px;
        }

        .skip-link {
            position: absolute;
            left: 1rem;
            top: -60px;
            z-index: 200;
            background: var(--primary);
            color: var(--primary-dark);
            padding: .7rem 1.2rem;
            border-radius: var(--radius-sm);
            font-weight: 600;
            transition: top .25s ease;
        }

        .skip-link:focus {
            top: 1rem;
        }

        .container {
            max-width: var(--container);
            margin: 0 auto;
            padding: 0 1.25rem;
        }

        .eyebrow {
            font-family: 'IBM Plex Mono', monospace;
            font-size: 0.78rem;
            letter-spacing: 0.14em;
            text-transform: uppercase;
            color: var(--primary);
            display: inline-flex;
            align-items: center;
            gap: .5rem;
        }

        .eyebrow::before {
            content: '';
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: var(--primary);
            box-shadow: 0 0 8px var(--primary);
        }

        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: .6rem;
            padding: .9rem 1.7rem;
            border-radius: 999px;
            font-weight: 600;
            font-size: .95rem;
            border: 1px solid transparent;
            transition: transform .25s ease, box-shadow .25s ease, background .25s ease, border-color .25s ease;
            white-space: nowrap;
        }

        .btn-primary {
            background: var(--primary);
            color: var(--primary-dark);
            box-shadow: 0 8px 24px rgba(0, 217, 192, 0.22);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(0, 217, 192, 0.32);
        }

        .btn-ghost {
            background: transparent;
            color: var(--text);
            border-color: var(--border-strong);
        }

        .btn-ghost:hover {
            border-color: var(--primary);
            color: var(--primary);
            transform: translateY(-2px);
        }

        .btn-sm {
            padding: .6rem 1.1rem;
            font-size: .85rem;
        }

        /* ---------- HEADER ---------- */
        header.site-header {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 100;
            padding: 1.15rem 0;
            background: transparent;
            border-bottom: 1px solid transparent;
            transition: background .35s ease, border-color .35s ease, padding .35s ease, backdrop-filter .35s ease;
        }

        header.site-header.scrolled {
            background: rgba(8, 11, 20, 0.82);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border-bottom: 1px solid var(--border);
            padding: .8rem 0;
        }

        .nav-inner {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 1rem;
        }

        .header-actions {
            display: flex;
            align-items: center;
            gap: .75rem;
        }

        .user-pill {
            display: inline-flex;
            align-items: center;
            gap: .55rem;
            padding: .5rem .8rem;
            border-radius: 999px;
            background: rgba(0, 217, 192, 0.08);
            border: 1px solid rgba(0, 217, 192, 0.18);
            color: var(--text);
            font-size: .8rem;
            font-weight: 600;
            white-space: nowrap;
        }

        .user-pill i {
            color: var(--primary);
        }

        .logout-btn {
            padding: .65rem 1rem;
            font-size: .8rem;
        }

        .logo {
            font-family: 'Space Grotesk', sans-serif;
            font-weight: 700;
            font-size: 1.3rem;
            display: flex;
            align-items: center;
            gap: .55rem;
            color: var(--text);
        }

        .logo-mark {
            width: 34px;
            height: 34px;
            border-radius: 9px;
            background: linear-gradient(135deg, var(--primary), #00A78F);
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--primary-dark);
            font-weight: 700;
            font-size: 1rem;
            font-family: 'IBM Plex Mono', monospace;
        }

        .logo span {
            color: var(--primary);
        }

        nav.main-nav {
            display: none;
        }

        nav.main-nav ul {
            display: flex;
            align-items: center;
            gap: 2.1rem;
        }

        nav.main-nav a {
            font-size: .94rem;
            color: var(--text-dim);
            font-weight: 500;
            position: relative;
            padding: .3rem 0;
            transition: color .2s ease;
        }

        nav.main-nav a::after {
            content: '';
            position: absolute;
            left: 0;
            bottom: -2px;
            height: 1.5px;
            width: 0;
            background: var(--primary);
            transition: width .25s ease;
        }

        nav.main-nav a:hover {
            color: var(--text);
        }

        nav.main-nav a:hover::after {
            width: 100%;
        }

        .header-actions {
            display: flex;
            align-items: center;
            gap: .75rem;
        }

        .header-actions .btn-primary {
            display: none;
        }

        .header-actions .btn-ghost {
            display: none;
        }

        .hamburger {
            background: none;
            border: 1px solid var(--border-strong);
            border-radius: var(--radius-sm);
            width: 44px;
            height: 44px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text);
            font-size: 1.1rem;
        }

        .mobile-panel {
            position: fixed;
            inset: 0 0 0 auto;
            width: min(84vw, 340px);
            background: var(--bg-panel);
            border-left: 1px solid var(--border);
            z-index: 150;
            padding: 1.6rem 1.5rem;
            transform: translateX(100%);
            transition: transform .35s ease;
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        .mobile-panel.open {
            transform: translateX(0);
        }

        .mobile-panel-top {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .mobile-panel ul {
            display: flex;
            flex-direction: column;
            gap: 1.4rem;
        }

        .mobile-panel a {
            font-size: 1.15rem;
            font-weight: 600;
        }

        .mobile-backdrop {
            position: fixed;
            inset: 0;
            background: rgba(3, 5, 10, 0.6);
            z-index: 140;
            opacity: 0;
            pointer-events: none;
            transition: opacity .35s ease;
        }

        .mobile-backdrop.open {
            opacity: 1;
            pointer-events: auto;
        }

        section {
            position: relative;
        }

        .section-pad {
            padding: 6rem 0;
        }

        .section-head {
            max-width: 620px;
            margin-bottom: 3rem;
        }

        .section-head h2 {
            font-size: clamp(1.8rem, 3.4vw, 2.6rem);
            margin-top: .9rem;
        }

        .section-head p {
            color: var(--text-dim);
            margin-top: 1rem;
            font-size: 1.02rem;
        }

        /* ---------- HERO ---------- */
        .hero {
            padding: 9.5rem 0 5rem;
            position: relative;
            overflow: hidden;
        }

        .hero::before {
            content: '';
            position: absolute;
            top: -180px;
            right: -160px;
            width: 520px;
            height: 520px;
            background: radial-gradient(circle, rgba(0, 217, 192, 0.16), transparent 70%);
            filter: blur(10px);
            pointer-events: none;
        }

        .hero::after {
            content: '';
            position: absolute;
            bottom: -220px;
            left: -180px;
            width: 480px;
            height: 480px;
            background: radial-gradient(circle, rgba(255, 180, 84, 0.09), transparent 70%);
            pointer-events: none;
        }

        .hero-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 3.5rem;
            align-items: center;
            position: relative;
            z-index: 2;
        }

        .hero-copy h1 {
            font-size: clamp(2.15rem, 5.2vw, 3.6rem);
            line-height: 1.08;
            margin-top: 1.1rem;
        }

        .hero-copy h1 .line {
            display: block;
            overflow: hidden;
        }

        .hero-copy h1 .accent {
            color: var(--primary);
        }

        .hero-copy p.lead {
            color: var(--text-dim);
            font-size: 1.08rem;
            margin-top: 1.4rem;
            max-width: 480px;
        }

        .hero-actions {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-top: 2.2rem;
        }

        .hero-trust {
            display: flex;
            gap: 1.8rem;
            margin-top: 2.6rem;
            flex-wrap: wrap;
        }

        .hero-trust div {
            font-family: 'IBM Plex Mono', monospace;
        }

        .hero-trust strong {
            display: block;
            font-size: 1.3rem;
            color: var(--text);
            font-family: 'Space Grotesk', sans-serif;
        }

        .hero-trust span {
            font-size: .78rem;
            color: var(--text-faint);
            text-transform: uppercase;
            letter-spacing: .06em;
        }

        /* terminal / compile visual */
        .compile-wrap {
            position: relative;
            z-index: 2;
        }

        .compile-card {
            background: var(--bg-panel);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            overflow: hidden;
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.45);
        }

        .compile-topbar {
            display: flex;
            align-items: center;
            gap: .5rem;
            padding: .85rem 1rem;
            border-bottom: 1px solid var(--border);
            background: var(--bg-panel-2);
        }

        .compile-topbar i.dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
        }

        .dot.red {
            background: #FF5F57;
        }

        .dot.yellow {
            background: #FEBC2E;
        }

        .dot.green {
            background: #28C840;
        }

        .compile-topbar span {
            margin-left: .6rem;
            font-family: 'IBM Plex Mono', monospace;
            font-size: .75rem;
            color: var(--text-faint);
        }

        .compile-body {
            padding: 1.5rem 1.6rem 1.7rem;
            font-family: 'IBM Plex Mono', monospace;
            font-size: .86rem;
            min-height: 230px;
        }

        .code-line {
            white-space: pre;
            color: var(--text-dim);
            margin-bottom: .55rem;
            opacity: 0;
            transform: translateY(6px);
        }

        .code-line .kw {
            color: var(--primary);
        }

        .code-line .str {
            color: var(--secondary);
        }

        .compile-cursor {
            display: inline-block;
            width: 7px;
            height: 1rem;
            background: var(--primary);
            vertical-align: middle;
            margin-left: 2px;
        }

        .preview-panel {
            margin-top: 1.1rem;
            border-radius: var(--radius-sm);
            overflow: hidden;
            border: 1px solid var(--border);
            opacity: 0;
            transform: translateY(10px) scale(.98);
        }

        .preview-bar {
            height: 22px;
            background: var(--bg-panel-2);
            display: flex;
            align-items: center;
            padding: 0 .6rem;
            gap: 4px;
        }

        .preview-bar span {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: rgba(232, 236, 244, 0.25);
        }

        .preview-body {
            padding: .9rem;
            background: #0C1424;
        }

        .preview-hero {
            height: 36px;
            border-radius: 6px;
            background: linear-gradient(90deg, rgba(0, 217, 192, .28), rgba(0, 217, 192, .06));
            margin-bottom: .6rem;
        }

        .preview-row {
            display: flex;
            gap: .5rem;
        }

        .preview-row div {
            flex: 1;
            height: 44px;
            border-radius: 6px;
            background: rgba(232, 236, 244, 0.06);
        }

        /* ---------- SERVICES ---------- */
        .services-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.25rem;
        }

        .service-card {
            background: var(--bg-panel);
            border: 1px solid var(--border);
            border-radius: var(--radius-md);
            padding: 1.9rem 1.7rem;
            transition: transform .3s ease, border-color .3s ease, background .3s ease;
        }

        .service-card:hover {
            transform: translateY(-6px);
            border-color: rgba(0, 217, 192, 0.4);
            background: var(--bg-panel-2);
        }

        .service-icon {
            width: 48px;
            height: 48px;
            border-radius: var(--radius-sm);
            background: rgba(0, 217, 192, 0.12);
            color: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
            margin-bottom: 1.2rem;
        }

        .service-card h3 {
            font-size: 1.12rem;
            margin-bottom: .6rem;
        }

        .service-card p {
            color: var(--text-dim);
            font-size: .92rem;
        }

        /* ---------- ABOUT ---------- */
        .about-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 3rem;
            align-items: center;
        }

        .about-media {
            position: relative;
            border-radius: var(--radius-lg);
            overflow: hidden;
            border: 1px solid var(--border);
        }

        .about-media img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            aspect-ratio: 4/3;
        }

        .about-badge {
            position: absolute;
            bottom: 1rem;
            left: 1rem;
            right: 1rem;
            background: rgba(8, 11, 20, 0.78);
            backdrop-filter: blur(8px);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm);
            padding: .9rem 1.1rem;
            display: flex;
            gap: .9rem;
            align-items: center;
        }

        .about-badge i {
            color: var(--primary);
            font-size: 1.3rem;
        }

        .about-badge strong {
            display: block;
            font-size: .95rem;
        }

        .about-badge span {
            font-size: .78rem;
            color: var(--text-dim);
        }

        .about-copy p {
            color: var(--text-dim);
            margin-top: 1.1rem;
        }

        .about-list {
            margin-top: 1.6rem;
            display: flex;
            flex-direction: column;
            gap: .9rem;
        }

        .about-list li {
            display: flex;
            gap: .7rem;
            align-items: flex-start;
            color: var(--text);
            font-size: .95rem;
        }

        .about-list i {
            color: var(--primary);
            margin-top: .2rem;
        }

        /* ---------- STATS ---------- */
        .stats-section {
            background: var(--bg-panel);
            border-top: 1px solid var(--border);
            border-bottom: 1px solid var(--border);
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 2rem;
            text-align: center;
        }

        .stat-num {
            font-family: 'Space Grotesk', sans-serif;
            font-weight: 700;
            font-size: clamp(2rem, 4.5vw, 2.9rem);
            color: var(--primary);
        }

        .stat-label {
            color: var(--text-dim);
            font-size: .85rem;
            margin-top: .4rem;
        }

        /* ---------- PROJECTS ---------- */
        .projects-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.5rem;
        }

        .project-card {
            position: relative;
            border-radius: var(--radius-md);
            overflow: hidden;
            border: 1px solid var(--border);
            aspect-ratio: 4/3;
        }

        .project-card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform .5s ease;
        }

        .project-card:hover img {
            transform: scale(1.07);
        }

        .project-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(180deg, transparent 40%, rgba(6, 9, 17, 0.92) 100%);
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 1.3rem;
        }

        .project-tag {
            font-family: 'IBM Plex Mono', monospace;
            font-size: .72rem;
            color: var(--primary);
            text-transform: uppercase;
            letter-spacing: .08em;
        }

        .project-overlay h3 {
            font-size: 1.15rem;
            margin-top: .4rem;
        }

        /* ---------- TESTIMONIALS ---------- */
        .testi-wrap {
            position: relative;
            max-width: 760px;
            margin: 0 auto;
        }

        .testi-card {
            background: var(--bg-panel);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            padding: 2.4rem 2.2rem;
            text-align: center;
        }

        .testi-card i.fa-quote-left {
            color: var(--primary);
            font-size: 1.4rem;
            opacity: .7;
        }

        .testi-quote {
            font-size: 1.15rem;
            margin-top: 1.2rem;
            line-height: 1.65;
        }

        .testi-person {
            margin-top: 1.6rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: .2rem;
        }

        .testi-avatar {
            width: 52px;
            height: 52px;
            border-radius: 50%;
            overflow: hidden;
            margin-bottom: .6rem;
            border: 2px solid var(--border-strong);
        }

        .testi-avatar img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .testi-person strong {
            font-family: 'Space Grotesk', sans-serif;
        }

        .testi-person span {
            font-size: .82rem;
            color: var(--text-dim);
        }

        .testi-nav {
            display: flex;
            justify-content: center;
            gap: .6rem;
            margin-top: 1.8rem;
        }

        .testi-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--border-strong);
            border: none;
            padding: 0;
            transition: background .25s ease, width .25s ease;
        }

        .testi-dot.active {
            background: var(--primary);
            width: 22px;
            border-radius: 5px;
        }

        .testi-arrow {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            width: 42px;
            height: 42px;
            border-radius: 50%;
            background: var(--bg-panel);
            border: 1px solid var(--border-strong);
            color: var(--text);
            display: none;
            align-items: center;
            justify-content: center;
        }

        .testi-arrow:hover {
            border-color: var(--primary);
            color: var(--primary);
        }

        .testi-arrow.left {
            left: -60px;
        }

        .testi-arrow.right {
            right: -60px;
        }

        /* ---------- CTA ---------- */
        .login-section {
            padding-top: 2rem;
        }

        .login-shell {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.5rem;
            background: var(--bg-panel);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            overflow: hidden;
            box-shadow: var(--shadow-glow);
        }

        .login-visual {
            background: linear-gradient(135deg, rgba(0, 217, 192, 0.12), rgba(255, 180, 84, 0.08));
            padding: 2rem;
            display: flex;
            flex-direction: column;
            justify-content: center;
            border-bottom: 1px solid var(--border);
        }

        .login-visual .eyebrow {
            margin-bottom: 1rem;
        }

        .login-visual h3 {
            font-size: clamp(1.5rem, 3vw, 2.2rem);
            margin-bottom: .9rem;
        }

        .login-visual p {
            color: var(--text-dim);
            max-width: 480px;
        }

        .login-badges {
            display: flex;
            flex-wrap: wrap;
            gap: .7rem;
            margin-top: 1.5rem;
        }

        .login-badges span {
            display: inline-flex;
            align-items: center;
            gap: .5rem;
            border: 1px solid var(--border-strong);
            border-radius: 999px;
            padding: .55rem .8rem;
            color: var(--text-dim);
            font-size: .8rem;
            background: rgba(255, 255, 255, 0.02);
        }

        .login-form-wrap {
            padding: 2rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .login-form {
            width: min(100%, 400px);
            display: grid;
            gap: 1rem;
        }

        .login-form h3 {
            font-size: 1.5rem;
            margin-bottom: .1rem;
        }

        .login-form p {
            color: var(--text-dim);
            font-size: .92rem;
        }

        .input-group {
            display: grid;
            gap: .45rem;
        }

        .input-group label {
            font-size: .8rem;
            color: var(--text-dim);
            font-weight: 600;
        }

        .input-group input {
            width: 100%;
            background: rgba(255, 255, 255, 0.02);
            border: 1px solid var(--border-strong);
            border-radius: 12px;
            padding: .9rem 1rem;
            font: inherit;
            color: var(--text);
        }

        .input-group input:focus {
            border-color: rgba(0, 217, 192, 0.8);
            box-shadow: 0 0 0 3px rgba(0, 217, 192, 0.12);
            outline: none;
        }

        .login-options {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 1rem;
            font-size: .82rem;
            color: var(--text-dim);
        }

        .login-options a {
            color: var(--primary);
        }

        .checkbox {
            display: inline-flex;
            align-items: center;
            gap: .55rem;
        }

        .checkbox input {
            accent-color: var(--primary);
        }

        .login-submit {
            width: 100%;
            margin-top: .3rem;
        }

        .signup-link {
            text-align: center;
            color: var(--text-dim);
            font-size: .88rem;
        }

        .signup-link a {
            color: var(--primary);
            font-weight: 600;
        }

        .cta-section {
            margin: 2rem auto 0;
            max-width: var(--container);
            border-radius: var(--radius-lg);
            background: radial-gradient(circle at 20% 20%, rgba(0, 217, 192, 0.16), transparent 60%), var(--bg-panel);
            border: 1px solid var(--border);
            padding: 4rem 2rem;
            text-align: center;
            position: relative;
            overflow: hidden;
        }

        .cta-section h2 {
            font-size: clamp(1.7rem, 4vw, 2.5rem);
        }

        .cta-section p {
            color: var(--text-dim);
            max-width: 520px;
            margin: 1rem auto 0;
        }

        .cta-actions {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-top: 2rem;
            flex-wrap: wrap;
        }

        /* ---------- FOOTER ---------- */
        footer {
            padding: 4.5rem 0 2rem;
            border-top: 1px solid var(--border);
            margin-top: 3rem;
        }

        .footer-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 2.5rem;
        }

        .footer-brand p {
            color: var(--text-dim);
            margin-top: 1rem;
            max-width: 320px;
            font-size: .92rem;
        }

        .footer-social {
            display: flex;
            gap: .7rem;
            margin-top: 1.3rem;
        }

        .footer-social a {
            width: 38px;
            height: 38px;
            border-radius: 50%;
            border: 1px solid var(--border-strong);
            display: flex;
            align-items: center;
            justify-content: center;
            transition: border-color .2s ease, color .2s ease;
        }

        .footer-social a:hover {
            border-color: var(--primary);
            color: var(--primary);
        }

        .footer-col h4 {
            font-size: .85rem;
            text-transform: uppercase;
            letter-spacing: .08em;
            color: var(--text-dim);
            margin-bottom: 1.1rem;
        }

        .footer-col ul {
            display: flex;
            flex-direction: column;
            gap: .8rem;
        }

        .footer-col a {
            color: var(--text-dim);
            font-size: .92rem;
            transition: color .2s ease;
        }

        .footer-col a:hover {
            color: var(--primary);
        }

        .footer-col li.contact-item {
            display: flex;
            gap: .6rem;
            align-items: flex-start;
            color: var(--text-dim);
            font-size: .92rem;
        }

        .footer-col li.contact-item i {
            color: var(--primary);
            margin-top: .2rem;
        }

        .footer-bottom {
            margin-top: 3rem;
            padding-top: 1.6rem;
            border-top: 1px solid var(--border);
            display: flex;
            flex-direction: column;
            gap: .8rem;
            align-items: center;
            text-align: center;
            color: var(--text-faint);
            font-size: .82rem;
        }

        /* ---------- RESPONSIVE ---------- */
        @media (min-width: 640px) {
            .stats-grid {
                grid-template-columns: repeat(4, 1fr);
            }

            .services-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .projects-grid {
                grid-template-columns: repeat(2, 1fr);
            }

            .footer-grid {
                grid-template-columns: 1.4fr 1fr 1fr;
            }
        }

        @media (min-width: 900px) {
            nav.main-nav {
                display: block;
            }

            .hamburger {
                display: none;
            }

            .header-actions .btn-primary {
                display: inline-flex;
            }

            .header-actions .btn-ghost {
                display: inline-flex;
            }

            .hero-grid {
                grid-template-columns: 1.05fr 0.95fr;
            }

            .about-grid {
                grid-template-columns: 1fr 1fr;
            }

            .about-grid.reverse .about-media {
                order: 2;
            }

            .testi-arrow {
                display: flex;
            }
        }

        @media (min-width: 1040px) {
            .services-grid {
                grid-template-columns: repeat(3, 1fr);
            }

            .projects-grid {
                grid-template-columns: repeat(3, 1fr);
            }
        }
    </style>
</head>

<body>

    <a href="#main" class="skip-link">Pular para o conteúdo principal</a>

    <div id="root"></div>

    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>

    <script type="text/babel" data-type="module">
        const { useState, useEffect, useRef, useCallback } = React;

        gsap.registerPlugin(ScrollTrigger);
        const REDUCED = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

        function getDemoSession() {
            try {
                const raw = localStorage.getItem('sitelab-demo-session');
                return raw ? JSON.parse(raw) : null;
            } catch (error) {
                return null;
            }
        }

        function getDisplayName(user) {
            if (!user) return null;
            if (user.full_name) return user.full_name;
            if (user.user_metadata?.full_name) return user.user_metadata.full_name;
            if (user.email) return user.email.split('@')[0];
            return 'Usuário';
        }

        /* ---------------- ICONS (Font Awesome) ---------------- */
        const Icon = ({ name, className = '' }) => <i className={`fa-solid ${name} ${className}`} aria-hidden="true"></i>;

        /* ---------------- DATA ---------------- */
        const NAV_LINKS = [
            { href: '#servicos', label: 'Serviços' },
            { href: '#sobre', label: 'Sobre' },
            { href: '#projetos', label: 'Projetos' },
            { href: '#depoimentos', label: 'Depoimentos' },
            { href: '#contato', label: 'Contato' },
        ];

        const SERVICES = [
            { icon: 'fa-window-maximize', title: 'Sites institucionais', desc: 'Páginas rápidas e responsivas que apresentam sua empresa com clareza e credibilidade.' },
            { icon: 'fa-cart-shopping', title: 'Lojas virtuais', desc: 'E-commerces completos, com catálogo, pagamento e gestão de pedidos integrados.' },
            { icon: 'fa-diagram-project', title: 'Sistemas sob medida', desc: 'Plataformas e painéis desenvolvidos para resolver o processo específico do seu negócio.' },
            { icon: 'fa-gears', title: 'Automação de processos', desc: 'Fluxos que eliminam tarefas manuais repetitivas e reduzem erros operacionais.' },
            { icon: 'fa-chart-line', title: 'Painéis administrativos', desc: 'Dashboards com dados em tempo real para decisões mais rápidas e seguras.' },
            { icon: 'fa-headset', title: 'Manutenção & suporte', desc: 'Acompanhamento contínuo, correções e evoluções após o lançamento do projeto.' },
        ];

        const STATS = [
            { end: 120, suffix: '+', label: 'Projetos entregues' },
            { end: 98, suffix: '%', label: 'Clientes satisfeitos' },
            { end: 7, suffix: ' anos', label: 'De experiência' },
            { end: 24, suffix: 'h', label: 'Tempo médio de resposta' },
        ];

        const PROJECTS = [
            { tag: 'Sistema', title: 'Painel de gestão para clínicas', img: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&w=900&q=80' },
            { tag: 'E-commerce', title: 'Loja virtual de cosméticos', img: 'https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?auto=format&fit=crop&w=900&q=80' },
            { tag: 'Institucional', title: 'Site para escritório de advocacia', img: 'https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?auto=format&fit=crop&w=900&q=80' },
            { tag: 'Sistema', title: 'Automação de pedidos por WhatsApp', img: 'https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=900&q=80' },
            { tag: 'Dashboard', title: 'Painel financeiro para franquias', img: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=900&q=80' },
            { tag: 'E-commerce', title: 'Marketplace de produtos artesanais', img: 'https://images.unsplash.com/photo-1519389950473-47ba0277781c?auto=format&fit=crop&w=900&q=80' },
        ];

        const TESTIMONIALS = [
            { name: 'Renata Costa', role: 'Diretora, Clínica Vitalis', quote: 'A SiteLab entendeu nosso processo interno antes de escrever qualquer linha de código. O painel entregue reduziu pela metade o tempo de agendamento.', avatar: 'https://images.unsplash.com/photo-1487412720507-e7ab37603c6f?auto=format&fit=crop&w=200&q=80' },
            { name: 'Diego Almeida', role: 'Fundador, Loja Terra Boa', quote: 'Migramos para a loja virtual construída pela equipe e as vendas online triplicaram em três meses. Suporte rápido em cada ajuste que pedimos.', avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?auto=format&fit=crop&w=200&q=80' },
            { name: 'Camila Torres', role: 'Sócia, Torres Advocacia', quote: 'O site ficou exatamente como imaginávamos: sério, rápido e fácil de atualizar. O processo todo foi transparente do início ao fim.', avatar: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?auto=format&fit=crop&w=200&q=80' },
        ];

        /* ---------------- HEADER ---------------- */
        function Header() {
            const [scrolled, setScrolled] = useState(false);
            const [open, setOpen] = useState(false);
            const [userName, setUserName] = useState('');

            useEffect(() => {
                const onScroll = () => setScrolled(window.scrollY > 40);
                onScroll();
                window.addEventListener('scroll', onScroll, { passive: true });
                return () => window.removeEventListener('scroll', onScroll);
            }, []);

            useEffect(() => {
                document.body.style.overflow = open ? 'hidden' : '';
            }, [open]);

            useEffect(() => {
                const demoSession = getDemoSession();

                if (demoSession?.full_name) {
                    setUserName(demoSession.full_name);
                } else if (demoSession?.user_metadata?.full_name) {
                    setUserName(demoSession.user_metadata.full_name);
                } else if (demoSession?.email) {
                    setUserName(demoSession.email.split('@')[0]);
                } else {
                    setUserName('');
                }
            }, []);

            const close = useCallback(() => setOpen(false), []);

            const handleSignOut = () => {
                localStorage.removeItem('sitelab-demo-session');
                setUserName('');
            };

            return (
                <React.Fragment>
                    <header className={`site-header ${scrolled ? 'scrolled' : ''}`}>
                        <div className="container nav-inner">
                            <a href="#main" className="logo" aria-label="SiteLab, ir para o início">
                                <span className="logo-mark">S</span>
                                Site<span>Lab</span>
                            </a>
                            <nav className="main-nav" aria-label="Navegação principal">
                                <ul>
                                    {NAV_LINKS.map(l => (
                                        <li key={l.href}><a href={l.href}>{l.label}</a></li>
                                    ))}
                                </ul>
                            </nav>
                            <div className="header-actions">
                                {userName ? (
                                    <>
                                        <span className="user-pill"><Icon name="fa-user" /> Olá, {userName}</span>
                                        <button type="button" className="btn btn-ghost btn-sm logout-btn" onClick={handleSignOut}>Sair</button>
                                    </>
                                ) : (
                                    <a href="loginsitelab.html" className="btn btn-primary btn-sm">Iniciar projeto</a>
                                )}
                            </div>
                            <button
                                className="hamburger"
                                aria-label="Abrir menu"
                                aria-expanded={open}
                                aria-controls="mobile-menu"
                                onClick={() => setOpen(true)}
                            >
                                <Icon name="fa-bars" />
                            </button>
                        </div>
                    </header>

                    <div className={`mobile-backdrop ${open ? 'open' : ''}`} onClick={close}></div>
                    <div id="mobile-menu" className={`mobile-panel ${open ? 'open' : ''}`} role="dialog" aria-modal={open} aria-label="Menu de navegação">
                        <div className="mobile-panel-top">
                            <span className="logo"><span className="logo-mark">S</span>Site<span>Lab</span></span>
                            <button className="hamburger" aria-label="Fechar menu" onClick={close}>
                                <Icon name="fa-xmark" />
                            </button>
                        </div>
                        <nav aria-label="Navegação mobile">
                            <ul>
                                {NAV_LINKS.map(l => (
                                    <li key={l.href}><a href={l.href} onClick={close}>{l.label}</a></li>
                                ))}
                            </ul>
                        </nav>
                        {userName ? (
                            <>
                                <div className="user-pill" style={{ marginBottom: '0.8rem', justifyContent: 'center' }}><Icon name="fa-user" /> {userName}</div>
                                <button type="button" className="btn btn-ghost" onClick={() => { localStorage.removeItem('sitelab-demo-session'); setUserName(''); close(); }}>Sair</button>
                            </>
                        ) : (
                            <a href="login.html" className="btn btn-primary" onClick={close}>Iniciar projeto</a>
                        )}
                    </div>
                </React.Fragment>
            );
        }

        /* ---------------- HERO ---------------- */
        const CODE_LINES = [
            <React.Fragment key="1"><span className="kw">const</span> projeto = sitelab.<span className="kw">criar</span>({'{'}</React.Fragment>,
            <React.Fragment key="2">&nbsp;&nbsp;tipo: <span className="str">'loja-virtual'</span>,</React.Fragment>,
            <React.Fragment key="3">&nbsp;&nbsp;design: <span className="str">'sob medida'</span>,</React.Fragment>,
            <React.Fragment key="4">&nbsp;&nbsp;entrega: <span className="str">'no prazo'</span></React.Fragment>,
            <React.Fragment key="5">{'}'});</React.Fragment>,
        ];

        function Hero() {
            const rootRef = useRef(null);

            useEffect(() => {
                const ctx = gsap.context(() => {
                    const tl = gsap.timeline({ defaults: { ease: 'power3.out' } });
                    tl.from('.hero-eyebrow', { opacity: 0, y: 14, duration: REDUCED ? 0.01 : 0.6 })
                        .from('.hero-line', { yPercent: 110, duration: REDUCED ? 0.01 : 0.8, stagger: 0.1 }, '-=0.3')
                        .from('.hero-lead', { opacity: 0, y: 16, duration: REDUCED ? 0.01 : 0.6 }, '-=0.35')
                        .from('.hero-actions .btn', { opacity: 0, y: 14, duration: REDUCED ? 0.01 : 0.5, stagger: 0.1 }, '-=0.3')
                        .from('.hero-trust > div', { opacity: 0, y: 10, duration: REDUCED ? 0.01 : 0.5, stagger: 0.08 }, '-=0.25')
                        .from('.compile-card', { opacity: 0, y: 24, scale: 0.97, duration: REDUCED ? 0.01 : 0.7 }, '-=0.6')
                        .to('.code-line', { opacity: 1, y: 0, duration: REDUCED ? 0.01 : 0.35, stagger: 0.28 }, '-=0.2')
                        .to('.preview-panel', { opacity: 1, y: 0, scale: 1, duration: REDUCED ? 0.01 : 0.5 }, '+=0.1');

                    if (!REDUCED) {
                        gsap.to('.hero::before', {});
                        gsap.to('.compile-wrap', {
                            y: -12,
                            ease: 'none',
                            scrollTrigger: { trigger: '.hero', start: 'top top', end: 'bottom top', scrub: 0.6 },
                        });
                    }
                }, rootRef);
                return () => ctx.revert();
            }, []);

            return (
                <section className="hero" id="main" ref={rootRef}>
                    <div className="container hero-grid">
                        <div className="hero-copy">
                            <span className="eyebrow hero-eyebrow">Estúdio de sistemas e sites</span>
                            <h1 aria-label="Sistemas e sites que colocam sua empresa no próximo nível">
                                <span className="line"><span className="hero-line" style={{ display: 'inline-block' }}>Sistemas e sites que</span></span>
                                <span className="line"><span className="hero-line accent" style={{ display: 'inline-block' }}>colocam sua empresa</span></span>
                                <span className="line"><span className="hero-line" style={{ display: 'inline-block' }}>no próximo nível</span></span>
                            </h1>
                            <p className="lead hero-lead">
                                Projetamos e construímos sites, lojas virtuais e sistemas sob medida — do primeiro esboço ao deploy — para negócios que não podem esperar meses para colocar tecnologia no ar.
                            </p>
                            <div className="hero-actions">
                                <a href="login.html" className="btn btn-primary">
                                    Iniciar projeto <Icon name="fa-arrow-right" />
                                </a>
                                <a href="#projetos" className="btn btn-ghost">Ver projetos</a>
                            </div>
                            <div className="hero-trust">
                                <div><strong>120+</strong><span>Projetos entregues</span></div>
                                <div><strong>98%</strong><span>Satisfação</span></div>
                                <div><strong>7 anos</strong><span>De mercado</span></div>
                            </div>
                        </div>

                        <div className="compile-wrap">
                            <div className="compile-card">
                                <div className="compile-topbar">
                                    <i className="dot red"></i><i className="dot yellow"></i><i className="dot green"></i>
                                    <span>build.js — sitelab</span>
                                </div>
                                <div className="compile-body">
                                    {CODE_LINES.map((line, i) => (
                                        <div className="code-line" key={i}>{line}{i === CODE_LINES.length - 1 && <span className="compile-cursor"></span>}</div>
                                    ))}
                                    <div className="preview-panel">
                                        <div className="preview-bar"><span></span><span></span><span></span></div>
                                        <div className="preview-body">
                                            <div className="preview-hero"></div>
                                            <div className="preview-row">
                                                <div></div><div></div><div></div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </section>
            );
        }

        /* ---------------- SERVICES ---------------- */
        function Services() {
            const ref = useRef(null);
            useEffect(() => {
                const ctx = gsap.context(() => {
                    gsap.from('.service-card', {
                        opacity: 0, y: 30, duration: REDUCED ? 0.01 : 0.6, stagger: 0.1,
                        scrollTrigger: { trigger: ref.current, start: 'top 78%' },
                    });
                }, ref);
                return () => ctx.revert();
            }, []);

            return (
                <section className="section-pad" id="servicos" ref={ref}>
                    <div className="container">
                        <div className="section-head">
                            <span className="eyebrow">O que fazemos</span>
                            <h2>Serviços pensados para cada etapa do seu negócio digital</h2>
                            <p>Da primeira página ao sistema mais complexo, cada entrega é construída sob medida para o seu processo — não o contrário.</p>
                        </div>
                        <div className="services-grid">
                            {SERVICES.map((s, i) => (
                                <div className="service-card" key={i}>
                                    <div className="service-icon"><Icon name={s.icon} /></div>
                                    <h3>{s.title}</h3>
                                    <p>{s.desc}</p>
                                </div>
                            ))}
                        </div>
                    </div>
                </section>
            );
        }

        /* ---------------- ABOUT ---------------- */
        function About() {
            const ref = useRef(null);
            useEffect(() => {
                const ctx = gsap.context(() => {
                    gsap.from('.about-media', { opacity: 0, x: -30, duration: REDUCED ? 0.01 : 0.7, scrollTrigger: { trigger: ref.current, start: 'top 75%' } });
                    gsap.from('.about-copy > *', { opacity: 0, y: 20, duration: REDUCED ? 0.01 : 0.6, stagger: 0.12, scrollTrigger: { trigger: ref.current, start: 'top 75%' } });
                }, ref);
                return () => ctx.revert();
            }, []);

            return (
                <section className="section-pad" id="sobre" ref={ref}>
                    <div className="container about-grid">
                        <div className="about-media">
                            <img
                                src="https://images.unsplash.com/photo-1522071820081-009f0129c71c?auto=format&fit=crop&w=900&q=80"
                                alt="Equipe da SiteLab reunida em frente a um monitor discutindo o layout de um sistema"
                                loading="lazy"
                            />
                            <div className="about-badge">
                                <Icon name="fa-code-branch" />
                                <div>
                                    <strong>Processo transparente</strong>
                                    <span>Você acompanha cada etapa do desenvolvimento</span>
                                </div>
                            </div>
                        </div>
                        <div className="about-copy">
                            <span className="eyebrow">Quem somos</span>
                            <h2>Uma equipe que trata seu sistema como o produto que ele é</h2>
                            <p>A SiteLab nasceu para resolver um problema comum: empresas que precisam de tecnologia sob medida, mas recebem soluções genéricas demoradas demais para lançar. Reunimos design, desenvolvimento e automação em um único fluxo de trabalho.</p>
                            <p>Trabalhamos lado a lado com cada cliente, do mapeamento do processo até o suporte pós-lançamento, sempre com prazos e escopo definidos com clareza desde a primeira conversa.</p>
                            <ul className="about-list">
                                <li><Icon name="fa-circle-check" /> Reuniões de alinhamento em cada etapa</li>
                                <li><Icon name="fa-circle-check" /> Código documentado e de fácil manutenção</li>
                                <li><Icon name="fa-circle-check" /> Suporte contínuo após a entrega</li>
                            </ul>
                        </div>
                    </div>
                </section>
            );
        }

        /* ---------------- STATS ---------------- */
        function Stats() {
            const ref = useRef(null);
            const numRefs = useRef([]);

            useEffect(() => {
                const ctx = gsap.context(() => {
                    const trigger = {
                        trigger: ref.current, start: 'top 80%', once: true,
                        onEnter: () => {
                            STATS.forEach((s, i) => {
                                const el = numRefs.current[i];
                                if (!el) return;
                                const obj = { val: 0 };
                                gsap.to(obj, {
                                    val: s.end,
                                    duration: REDUCED ? 0.01 : 1.6,
                                    ease: 'power2.out',
                                    onUpdate: () => { el.textContent = Math.round(obj.val) + s.suffix; },
                                });
                            });
                        },
                    };
                    gsap.from('.stat-item', { opacity: 0, y: 20, duration: REDUCED ? 0.01 : 0.6, stagger: 0.1, scrollTrigger: trigger });
                }, ref);
                return () => ctx.revert();
            }, []);

            return (
                <section className="stats-section section-pad" ref={ref}>
                    <div className="container stats-grid">
                        {STATS.map((s, i) => (
                            <div className="stat-item" key={i}>
                                <div className="stat-num" ref={el => numRefs.current[i] = el}>0{s.suffix}</div>
                                <div className="stat-label">{s.label}</div>
                            </div>
                        ))}
                    </div>
                </section>
            );
        }

        /* ---------------- PROJECTS ---------------- */
        function Projects() {
            const ref = useRef(null);
            useEffect(() => {
                const ctx = gsap.context(() => {
                    gsap.from('.project-card', {
                        opacity: 0, y: 34, duration: REDUCED ? 0.01 : 0.6, stagger: 0.1,
                        scrollTrigger: { trigger: ref.current, start: 'top 78%' },
                    });
                }, ref);
                return () => ctx.revert();
            }, []);

            return (
                <section className="section-pad" id="projetos" ref={ref}>
                    <div className="container">
                        <div className="section-head">
                            <span className="eyebrow">Projetos</span>
                            <h2>Alguns sistemas e sites que já colocamos no ar</h2>
                            <p>Cada projeto começa com um problema de negócio real — o design e o código vêm depois, moldados por ele.</p>
                        </div>
                        <div className="projects-grid">
                            {PROJECTS.map((p, i) => (
                                <div className="project-card" key={i}>
                                    <img src={p.img} alt={`Tela do projeto ${p.title}`} loading="lazy" />
                                    <div className="project-overlay">
                                        <span className="project-tag">{p.tag}</span>
                                        <h3>{p.title}</h3>
                                    </div>
                                </div>
                            ))}
                        </div>
                    </div>
                </section>
            );
        }

        /* ---------------- TESTIMONIALS ---------------- */
        function Testimonials() {
            const [index, setIndex] = useState(0);
            const ref = useRef(null);
            const total = TESTIMONIALS.length;

            const go = useCallback((i) => setIndex(((i % total) + total) % total), [total]);

            useEffect(() => {
                if (REDUCED) return;
                const id = setInterval(() => setIndex(i => (i + 1) % total), 6500);
                return () => clearInterval(id);
            }, [total]);

            useEffect(() => {
                const ctx = gsap.context(() => {
                    gsap.from('.testi-wrap', { opacity: 0, y: 24, duration: REDUCED ? 0.01 : 0.6, scrollTrigger: { trigger: ref.current, start: 'top 80%' } });
                }, ref);
                return () => ctx.revert();
            }, []);

            useEffect(() => {
                if (REDUCED) return;
                gsap.fromTo('.testi-card', { opacity: 0, y: 10 }, { opacity: 1, y: 0, duration: 0.45, ease: 'power2.out' });
            }, [index]);

            const t = TESTIMONIALS[index];

            return (
                <section className="section-pad" id="depoimentos" ref={ref}>
                    <div className="container">
                        <div className="section-head" style={{ margin: '0 auto 3rem', textAlign: 'center' }}>
                            <span className="eyebrow" style={{ justifyContent: 'center' }}>Depoimentos</span>
                            <h2>Quem já construiu com a SiteLab</h2>
                        </div>
                        <div className="testi-wrap">
                            <button className="testi-arrow left" aria-label="Depoimento anterior" onClick={() => go(index - 1)}>
                                <Icon name="fa-chevron-left" />
                            </button>
                            <div className="testi-card">
                                <Icon name="fa-quote-left" />
                                <p className="testi-quote">{t.quote}</p>
                                <div className="testi-person">
                                    <div className="testi-avatar"><img src={t.avatar} alt={`Foto de ${t.name}`} loading="lazy" /></div>
                                    <strong>{t.name}</strong>
                                    <span>{t.role}</span>
                                </div>
                            </div>
                            <button className="testi-arrow right" aria-label="Próximo depoimento" onClick={() => go(index + 1)}>
                                <Icon name="fa-chevron-right" />
                            </button>
                            <div className="testi-nav" role="tablist" aria-label="Selecionar depoimento">
                                {TESTIMONIALS.map((_, i) => (
                                    <button
                                        key={i}
                                        className={`testi-dot ${i === index ? 'active' : ''}`}
                                        role="tab"
                                        aria-selected={i === index}
                                        aria-label={`Ver depoimento ${i + 1}`}
                                        onClick={() => go(i)}
                                    ></button>
                                ))}
                            </div>
                        </div>
                    </div>
                </section>
            );
        }

        /* ---------------- CTA ---------------- */
        function CTA() {
            const ref = useRef(null);
            useEffect(() => {
                const ctx = gsap.context(() => {
                    gsap.from('.cta-section > *', {
                        opacity: 0, y: 20, duration: REDUCED ? 0.01 : 0.6, stagger: 0.1,
                        scrollTrigger: { trigger: ref.current, start: 'top 82%' },
                    });
                }, ref);
                return () => ctx.revert();
            }, []);

            return (
                <section id="contato" ref={ref}>
                    <div className="container">
                        <div className="cta-section">
                            <span className="eyebrow" style={{ justifyContent: 'center' }}>Vamos conversar</span>
                            <h2>Pronto para tirar o seu sistema do papel?</h2>
                            <p>Conte um pouco sobre o seu projeto e retornamos com uma proposta de escopo e prazo em até 1 dia útil.</p>
                            <div className="cta-actions">
                                <a className="btn btn-primary" href="mailto:contato@sitelab.dev">
                                    <Icon name="fa-envelope" /> Falar com a SiteLab
                                </a>
                                <a className="btn btn-ghost" href="https://wa.me/5585999999999" target="_blank" rel="noopener noreferrer">
                                    <Icon name="fa-brands fa-whatsapp" /> Chamar no WhatsApp
                                </a>
                            </div>
                        </div>
                    </div>
                </section>
            );
        }

        /* ---------------- FOOTER ---------------- */
        function Footer() {
            return (
                <footer>
                    <div className="container">
                        <div className="footer-grid">
                            <div className="footer-brand">
                                <span className="logo"><span className="logo-mark">S</span>Site<span>Lab</span></span>
                                <p>Estúdio de desenvolvimento especializado em sites, lojas virtuais e sistemas sob medida para pequenas e médias empresas.</p>
                                <div className="footer-social">
                                    <a href="https://www.instagram.com/site_lab_criativo/" aria-label="SiteLab no Instagram" target="_blank" rel="noopener noreferrer"><Icon name="fa-brands fa-instagram" /></a>
                                    <a href="https://github.com/samuel-freire-romao/projeto" aria-label="SiteLab no GitHub" target="_blank" rel="noopener noreferrer"><Icon name="fa-brands fa-github" /></a>
                                </div>
                            </div>
                            <div className="footer-col">
                                <h4>Navegação</h4>
                                <ul>
                                    {NAV_LINKS.map(l => <li key={l.href}><a href={l.href}>{l.label}</a></li>)}
                                </ul>
                            </div>
                            <div className="footer-col">
                                <h4>Contato</h4>
                                <ul>
                                    <li className="contact-item"><Icon name="fa-envelope" /> samuelfreire2527@gmail.com</li>
                                    <li className="contact-item"><Icon name="fa-phone" /> (85) 99669-4355</li>
                                    <li className="contact-item"><Icon name="fa-location-dot" /> Fortaleza, CE — Brasil</li>
                                </ul>
                            </div>
                        </div>
                        <div className="footer-bottom">
                            <span>© {new Date().getFullYear()} SiteLab. Todos os direitos reservados.</span>
                        </div>
                    </div>
                </footer>
            );
        }

        /* ---------------- APP ---------------- */
        function App() {
            return (
                <React.Fragment>
                    <Header />
                    <main>
                        <Hero />
                        <Services />
                        <About />
                        <Stats />
                        <Projects />
                        <Testimonials />
                        <CTA />
                    </main>
                    <Footer />
                </React.Fragment>
            );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>

</html>
