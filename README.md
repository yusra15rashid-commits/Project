<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0" />
  <title>HFC - Healthy Fry-chicks</title>
  <style>
    :root {
      --bg-black: #0a0a0c;
      --bg-dark: #141417;
      --card-bg: #1e1e24;
      --brand-red: #e62e2d;
      --brand-orange: #ff7b00;
      --brand-green: #22c55e;
      --brand-yellow: #ffd000;
      --text-light: #f8fafc;
      --text-muted: #94a3b8;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      background-color: var(--bg-black);
      color: var(--text-light);
      overflow-x: hidden;
    }

    /* ================= 1. INTRO SPLASH SCREEN ================= */
    #intro-screen {
      position: fixed;
      inset: 0;
      background-color: #000000;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 9999;
      padding: 20px;
      transition: opacity 0.8s ease, visibility 0.8s ease;
    }

    #intro-screen.fade-out {
      opacity: 0;
      visibility: hidden;
      pointer-events: none;
    }

    .intro-hint {
      color: var(--text-muted);
      font-size: 0.9rem;
      letter-spacing: 2.5px;
      text-transform: uppercase;
      margin-bottom: 10px;
      animation: pulseHint 2s infinite;
      text-align: center;
    }

    .intro-sub-legend {
      color: var(--brand-green);
      font-size: 0.8rem;
      letter-spacing: 1.2px;
      margin-bottom: 24px;
      text-transform: uppercase;
      font-weight: 700;
      text-align: center;
      line-height: 1.5;
    }

    @keyframes pulseHint {
      0%, 100% { opacity: 0.45; }
      50% { opacity: 1; }
    }

    .logo-selector {
      display: flex;
      gap: 22px;
      align-items: center;
      justify-content: center;
      user-select: none;
    }

    .letter-wrapper {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 8px;
    }

    .letter-label {
      font-size: 0.72rem;
      font-weight: 800;
      letter-spacing: 1.2px;
      text-transform: uppercase;
      color: var(--text-muted);
      transition: color 0.3s;
    }

    .letter-wrapper:hover .letter-label {
      color: var(--brand-orange);
    }

    .letter-box {
      position: relative;
      font-size: clamp(3.6rem, 11vw, 8.5rem);
      font-weight: 900;
      color: #ffffff;
      padding: 10px 22px;
      cursor: pointer;
      border: 3px solid transparent;
      border-radius: 16px;
      transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
      letter-spacing: 2px;
    }

    .letter-box::after {
      content: '';
      position: absolute;
      bottom: 8px;
      left: 50%;
      width: 0%;
      height: 5px;
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange), var(--brand-green));
      border-radius: 4px;
      transform: translateX(-50%);
      transition: width 0.3s ease;
    }

    .letter-box:hover,
    .letter-box:active {
      color: var(--brand-yellow);
      border-color: var(--brand-orange);
      box-shadow: 0 0 25px rgba(255, 123, 0, 0.55), inset 0 0 15px rgba(230, 46, 45, 0.35);
      transform: translateY(-4px) scale(1.04);
    }

    .letter-box:hover::after {
      width: 75%;
    }

    /* ================= 2. BIG WIDE YELLOW WOBBLE ANIMATION ================= */
    #yellow-animation-stage {
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at center, #1a1500 0%, #000000 85%);
      display: none;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 10000;
      overflow: hidden;
      padding: 20px;
      text-align: center;
    }

    #yellow-animation-stage.active {
      display: flex;
    }

    .big-yellow-hfc {
      font-size: clamp(4.5rem, 18vw, 15rem);
      font-weight: 900;
      color: var(--brand-yellow);
      letter-spacing: 0.16em;
      transform: scaleX(1.3);
      text-transform: uppercase;
      text-shadow:
        0 6px 0 #b8860b,
        0 12px 25px rgba(255, 208, 0, 0.6),
        0 0 60px rgba(255, 123, 0, 0.45);
      animation: slideFromRightWobble 1.6s cubic-bezier(0.22, 1, 0.36, 1) forwards;
    }

    .big-yellow-sub {
      margin-top: 18px;
      font-size: clamp(0.95rem, 2.5vw, 1.7rem);
      font-weight: 700;
      letter-spacing: 4px;
      color: var(--brand-green);
      text-transform: uppercase;
      opacity: 0;
      animation: fadeUpSub 0.6s ease 0.9s forwards;
    }

    .enter-now-btn {
      margin-top: 30px;
      padding: 13px 30px;
      font-size: 1rem;
      font-weight: 800;
      color: #000;
      background: var(--brand-yellow);
      border: none;
      border-radius: 50px;
      cursor: pointer;
      opacity: 0;
      animation: fadeUpSub 0.5s ease 1.2s forwards;
      transition: transform 0.2s ease, background 0.2s ease;
    }

    .enter-now-btn:hover {
      transform: scale(1.06);
      background: var(--brand-orange);
      color: #fff;
    }

    @keyframes slideFromRightWobble {
      0% { opacity: 0; transform: translateX(110vw) scaleX(1.5) skewX(-18deg); }
      50% { opacity: 1; transform: translateX(-30px) scaleX(1.22) skewX(10deg); }
      68% { transform: translateX(18px) scaleX(1.36) skewX(-7deg); }
      82% { transform: translateX(-8px) scaleX(1.28) skewX(4deg); }
      92% { transform: translateX(4px) scaleX(1.31) skewX(-2deg); }
      100% { opacity: 1; transform: translateX(0) scaleX(1.3) skewX(0deg); }
    }

    @keyframes fadeUpSub {
      from { opacity: 0; transform: translateY(15px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* ================= SHARED HEADER ================= */
    header {
      position: sticky;
      top: 0;
      z-index: 100;
      background: rgba(15, 15, 18, 0.96);
      backdrop-filter: blur(10px);
      border-bottom: 3px solid var(--brand-orange);
      padding: 11px 5%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
    }

    .brand-lockup {
      display: flex;
      align-items: center;
      gap: 10px;
      text-decoration: none;
      cursor: pointer;
      min-width: 0;
    }

    .brand-title h1 {
      font-size: 1.5rem;
      font-weight: 900;
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      line-height: 1;
    }

    .brand-title span {
      font-size: 0.72rem;
      font-weight: 700;
      color: var(--brand-green);
      letter-spacing: 1.2px;
      text-transform: uppercase;
      display: block;
      margin-top: 2px;
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 9px;
      margin-left: auto;
    }

    .replay-btn {
      background: transparent;
      border: 1.5px solid var(--brand-green);
      color: var(--brand-green);
      padding: 8px 12px;
      border-radius: 8px;
      font-weight: 700;
      cursor: pointer;
      font-size: 0.82rem;
      transition: all 0.2s;
      white-space: nowrap;
    }

    .replay-btn:hover {
      background: var(--brand-green);
      color: #000;
    }

    .cart-btn {
      background: linear-gradient(135deg, var(--brand-red), var(--brand-orange));
      color: #fff;
      border: none;
      padding: 9px 14px;
      border-radius: 8px;
      font-weight: 800;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 7px;
      box-shadow: 0 4px 14px rgba(230, 46, 45, 0.4);
      transition: transform 0.2s;
      white-space: nowrap;
      font-size: 0.88rem;
    }

    .cart-btn:hover {
      transform: translateY(-2px);
    }

    .cart-count {
      background: var(--brand-green);
      color: #000;
      font-weight: 900;
      padding: 2px 7px;
      border-radius: 50px;
      font-size: 0.78rem;
    }

    /* Top-Right Three-Line Menu Button */
    .three-line-btn {
      background: #1e1e26;
      color: var(--brand-yellow);
      border: 2px solid var(--brand-orange);
      width: 42px;
      height: 40px;
      border-radius: 9px;
      cursor: pointer;
      display: inline-flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      gap: 5px;
      transition: background 0.2s, transform 0.15s;
      flex-shrink: 0;
    }

    .three-line-btn:hover {
      background: var(--brand-orange);
      transform: translateY(-1px);
    }

    .three-line-btn span {
      display: block;
      width: 20px;
      height: 2.5px;
      background: var(--brand-yellow);
      border-radius: 2px;
      transition: background 0.2s;
    }

    .three-line-btn:hover span {
      background: #000000;
    }

    /* Side Category Menu Drawer (Opened via Three-Line Button) */
    .side-menu-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.7);
      backdrop-filter: blur(3px);
      display: none;
      z-index: 550;
    }

    .side-menu-backdrop.open {
      display: block;
    }

    .side-menu-drawer {
      position: fixed;
      top: 0;
      right: -350px;
      width: 320px;
      max-width: 88vw;
      height: 100dvh;
      background: #15151b;
      border-left: 3px solid var(--brand-orange);
      z-index: 600;
      padding: 20px 16px;
      display: flex;
      flex-direction: column;
      transition: right 0.3s ease;
      box-shadow: -12px 0 32px rgba(0, 0, 0, 0.85);
      overflow-y: auto;
    }

    .side-menu-drawer.open {
      right: 0;
    }

    .side-menu-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-bottom: 14px;
      margin-bottom: 14px;
      border-bottom: 1px solid #2c2c38;
    }

    .side-menu-header h3 {
      font-size: 1.12rem;
      font-weight: 900;
      color: var(--brand-yellow);
    }

    .close-side-menu {
      background: none;
      border: none;
      color: var(--brand-red);
      font-size: 1.5rem;
      font-weight: 900;
      cursor: pointer;
      line-height: 1;
      padding: 4px;
    }

    .side-menu-list {
      display: flex;
      flex-direction: column;
      gap: 9px;
    }

    .side-menu-item {
      width: 100%;
      text-align: left;
      background: #1f1f28;
      border: 1.5px solid #2e2e3b;
      color: var(--text-light);
      padding: 13px 14px;
      border-radius: 11px;
      font-size: 0.95rem;
      font-weight: 700;
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      align-items: center;
      transition: all 0.18s ease;
    }

    .side-menu-item:hover {
      border-color: var(--brand-orange);
      background: #282834;
      color: var(--brand-yellow);
    }

    .side-menu-item.active-cat {
      border-color: var(--brand-green);
      background: rgba(34, 197, 94, 0.16);
      color: var(--brand-green);
    }

    /* ================= 3. HOT DEALS & SINGLE-CATEGORY PAGE (H & F) ================= */
    #main-home {
      display: none;
      min-height: 100vh;
      background-color: var(--bg-dark);
    }

    #main-home.visible {
      display: block;
      animation: homeReveal 0.5s ease forwards;
    }

    @keyframes homeReveal {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    .hero {
      background: linear-gradient(135deg, rgba(230, 46, 45, 0.18), rgba(255, 123, 0, 0.14), rgba(34, 197, 94, 0.15));
      border-bottom: 1px solid #27272f;
      padding: 34px 5%;
      text-align: center;
    }

    .health-badge {
      display: inline-block;
      background: rgba(34, 197, 94, 0.18);
      color: var(--brand-green);
      border: 1px solid var(--brand-green);
      padding: 6px 14px;
      border-radius: 50px;
      font-size: 0.8rem;
      font-weight: 700;
      letter-spacing: 0.8px;
      margin-bottom: 12px;
      text-transform: uppercase;
    }

    .hero h2 {
      font-size: clamp(1.85rem, 5vw, 3.1rem);
      font-weight: 900;
      margin-bottom: 10px;
      line-height: 1.15;
    }

    .hero h2 span.red { color: var(--brand-red); }
    .hero h2 span.orange { color: var(--brand-orange); }
    .hero h2 span.green { color: var(--brand-green); }

    .hero p {
      color: var(--text-muted);
      max-width: 650px;
      margin: 0 auto 18px;
      font-size: 0.96rem;
      line-height: 1.55;
    }

    .hero-menu-trigger {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: #1f1f28;
      color: var(--brand-yellow);
      border: 1.5px solid var(--brand-orange);
      padding: 10px 18px;
      border-radius: 50px;
      font-size: 0.88rem;
      font-weight: 800;
      cursor: pointer;
      transition: all 0.2s;
    }

    .hero-menu-trigger:hover {
      background: var(--brand-orange);
      color: #000;
    }

    .deals-section {
      padding: 36px 5% 60px;
      max-width: 1280px;
      margin: 0 auto;
    }

    .category-block {
      margin-bottom: 24px;
    }

    .section-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 12px;
      margin-bottom: 22px;
      border-left: 6px solid var(--brand-red);
      padding-left: 14px;
    }

    .section-header h3 {
      font-size: clamp(1.4rem, 4vw, 1.8rem);
      font-weight: 900;
      text-transform: uppercase;
    }

    .section-header h3 span {
      color: var(--brand-orange);
    }

    .section-header p {
      color: var(--brand-green);
      font-weight: 600;
      font-size: 0.88rem;
      margin-top: 2px;
    }

    .back-hot-deals-btn {
      background: rgba(255, 123, 0, 0.15);
      color: var(--brand-yellow);
      border: 1.5px solid var(--brand-orange);
      padding: 8px 14px;
      border-radius: 50px;
      font-size: 0.82rem;
      font-weight: 800;
      cursor: pointer;
      transition: all 0.2s;
    }

    .back-hot-deals-btn:hover {
      background: var(--brand-orange);
      color: #000;
    }

    .deals-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(265px, 1fr));
      gap: 20px;
    }

    .deal-card {
      background: var(--card-bg);
      border-radius: 16px;
      overflow: hidden;
      border: 1.5px solid #2c2c35;
      transition: transform 0.25s ease, border-color 0.25s ease, box-shadow 0.25s ease;
      display: flex;
      flex-direction: column;
    }

    .deal-card:hover {
      transform: translateY(-5px);
      border-color: var(--brand-orange);
      box-shadow: 0 12px 28px rgba(255, 123, 0, 0.2);
    }

    .deal-banner {
      height: 132px;
      padding: 14px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
    }

    .deal-banner.red-orange {
      background: linear-gradient(135deg, var(--brand-red), var(--brand-orange));
    }

    .deal-banner.green-orange {
      background: linear-gradient(135deg, #15803d, var(--brand-orange));
    }

    .deal-banner.red-green {
      background: linear-gradient(135deg, var(--brand-red), #16a34a);
    }

    .banner-top-row {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 8px;
    }

    .deal-tag {
      background: #000000cc;
      color: var(--brand-yellow);
      font-size: 0.7rem;
      font-weight: 800;
      padding: 5px 10px;
      border-radius: 50px;
      text-transform: uppercase;
      letter-spacing: 0.7px;
    }

    .corner-size-btn {
      background: var(--brand-yellow);
      color: #000000;
      border: 2px solid #000000;
      border-radius: 999px;
      padding: 5px 12px;
      font-size: 0.75rem;
      font-weight: 900;
      text-transform: uppercase;
      letter-spacing: 0.5px;
      cursor: pointer;
      box-shadow: 0 3px 10px rgba(0, 0, 0, 0.45);
      transition: transform 0.15s ease, background 0.15s ease, color 0.15s ease;
      white-space: nowrap;
    }

    .corner-size-btn:hover {
      background: #ffffff;
      color: var(--brand-red);
      transform: scale(1.06);
    }

    .deal-emoji {
      font-size: 2.7rem;
      align-self: flex-end;
      filter: drop-shadow(0 6px 8px rgba(0,0,0,0.4));
    }

    .deal-body {
      padding: 16px;
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
    }

    .deal-title {
      font-size: 1.12rem;
      font-weight: 800;
      margin-bottom: 6px;
      color: #fff;
    }

    .deal-desc {
      font-size: 0.85rem;
      color: var(--text-muted);
      line-height: 1.45;
      margin-bottom: 12px;
    }

    .size-hint-pill {
      display: inline-block;
      background: rgba(34, 197, 94, 0.14);
      color: var(--brand-green);
      font-size: 0.74rem;
      font-weight: 700;
      padding: 4px 10px;
      border-radius: 6px;
      margin-bottom: 12px;
      width: fit-content;
    }

    .deal-footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-top: 12px;
      border-top: 1px solid #2e2e38;
      gap: 10px;
    }

    .price-box .size-label {
      color: var(--text-muted);
      font-size: 0.72rem;
      font-weight: 700;
      text-transform: uppercase;
      display: block;
    }

    .price-box .new-price {
      font-size: 1.2rem;
      font-weight: 900;
      color: var(--brand-orange);
    }

    .add-btn {
      background: var(--brand-green);
      color: #052e16;
      border: none;
      padding: 11px 18px;
      border-radius: 10px;
      font-weight: 900;
      font-size: 0.92rem;
      cursor: pointer;
      transition: background 0.2s, transform 0.15s;
      min-height: 42px;
    }

    .add-btn:hover {
      background: #4ade80;
      transform: scale(1.04);
    }

    /* ================= 4. MENU PICTURE PAGE (C DESTINATION) ================= */
    #menu-picture-page {
      display: none;
      min-height: 100vh;
      background-color: var(--bg-dark);
      animation: homeReveal 0.5s ease forwards;
    }

    .menu-poster-wrapper {
      max-width: 1040px;
      margin: 28px auto;
      padding: 0 5% 60px;
      text-align: center;
    }

    .menu-poster-card {
      background: linear-gradient(165deg, #16161d 0%, #0d0d11 100%);
      border: 4px solid var(--brand-orange);
      border-radius: 22px;
      padding: 28px 20px;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.85), 0 0 30px rgba(255, 123, 0, 0.2);
      position: relative;
      overflow: hidden;
    }

    .menu-poster-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 8px;
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange), var(--brand-green));
    }

    .poster-header {
      margin-bottom: 22px;
      border-bottom: 2px dashed #2e2e3a;
      padding-bottom: 16px;
    }

    .poster-header h2 {
      font-size: clamp(1.6rem, 5vw, 2.8rem);
      font-weight: 900;
      letter-spacing: 1.5px;
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange), var(--brand-yellow));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .poster-header p {
      color: var(--brand-green);
      font-weight: 800;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      font-size: 0.82rem;
      margin-top: 6px;
    }

    .poster-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 16px;
      text-align: left;
    }

    .poster-category {
      background: #1b1b22;
      border: 1.5px solid #2b2b36;
      border-radius: 14px;
      padding: 15px;
    }

    .poster-category h3 {
      font-size: 1.02rem;
      font-weight: 900;
      color: var(--brand-orange);
      border-bottom: 2px solid var(--brand-red);
      padding-bottom: 7px;
      margin-bottom: 10px;
      text-transform: uppercase;
    }

    .poster-item {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      padding: 6px 0;
      border-bottom: 1px dotted #2f2f3b;
      font-size: 0.86rem;
      gap: 10px;
    }

    .poster-item:last-child {
      border-bottom: none;
    }

    .poster-item-name {
      color: var(--text-light);
      font-weight: 600;
    }

    .poster-item-price {
      color: var(--brand-green);
      font-weight: 800;
      white-space: nowrap;
      font-size: 0.8rem;
    }

    .poster-footer {
      margin-top: 24px;
      padding-top: 16px;
      border-top: 2px dashed #2e2e3a;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 15px;
    }

    .poster-contact {
      color: var(--brand-yellow);
      font-weight: 800;
      font-size: 0.92rem;
      text-align: left;
    }

    .poster-contact a {
      color: var(--brand-green);
      text-decoration: none;
    }

    .go-deals-cta {
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange));
      color: #fff;
      border: none;
      padding: 12px 22px;
      border-radius: 50px;
      font-weight: 800;
      cursor: pointer;
      font-size: 0.92rem;
      transition: transform 0.2s;
    }

    .go-deals-cta:hover {
      transform: scale(1.04);
    }

    /* Slide-Out Order Drawer */
    .cart-drawer {
      position: fixed;
      top: 0;
      right: -410px;
      width: 375px;
      max-width: 100vw;
      height: 100dvh;
      background: #16161b;
      border-left: 3px solid var(--brand-orange);
      z-index: 650;
      padding: 20px;
      display: flex;
      flex-direction: column;
      transition: right 0.35s ease;
      box-shadow: -10px 0 30px rgba(0,0,0,0.75);
    }

    .cart-drawer.open {
      right: 0;
    }

    .cart-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #2d2d37;
      padding-bottom: 14px;
      margin-bottom: 14px;
    }

    .cart-header-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .clear-cart-btn {
      background: rgba(239, 68, 68, 0.14);
      border: 1px solid #ef4444;
      color: #fca5a5;
      padding: 6px 11px;
      border-radius: 7px;
      font-size: 0.78rem;
      font-weight: 800;
      cursor: pointer;
      transition: background 0.2s, color 0.2s;
    }

    .clear-cart-btn:hover {
      background: #ef4444;
      color: #ffffff;
    }

    .close-cart {
      background: none;
      border: none;
      color: var(--brand-red);
      font-size: 1.55rem;
      font-weight: 900;
      cursor: pointer;
      line-height: 1;
      padding: 4px;
    }

    .cart-items {
      flex: 1;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      gap: 12px;
      padding-right: 2px;
    }

    .cart-item {
      background: #22222a;
      padding: 12px;
      border-radius: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
      border-left: 4px solid var(--brand-green);
    }

    .cart-item-info {
      flex: 1;
      min-width: 0;
    }

    .qty-controls {
      display: flex;
      align-items: center;
      gap: 6px;
      background: #141419;
      padding: 4px 6px;
      border-radius: 8px;
      border: 1px solid #32323e;
    }

    .qty-btn {
      width: 30px;
      height: 30px;
      border-radius: 6px;
      border: none;
      background: var(--brand-orange);
      color: #000000;
      font-weight: 900;
      font-size: 1.05rem;
      line-height: 1;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      transition: background 0.15s, transform 0.12s;
    }

    .qty-btn.minus {
      background: #33333f;
      color: #ffffff;
    }

    .qty-btn.minus:hover {
      background: var(--brand-red);
    }

    .qty-btn:hover {
      background: var(--brand-yellow);
      transform: scale(1.05);
    }

    .qty-value {
      min-width: 22px;
      text-align: center;
      font-weight: 900;
      font-size: 0.95rem;
      color: var(--text-light);
    }

    .cart-total-box {
      border-top: 2px solid #2d2d37;
      padding-top: 16px;
      margin-top: 16px;
    }

    .checkout-btn {
      width: 100%;
      margin-top: 12px;
      padding: 14px;
      border: none;
      border-radius: 10px;
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange));
      color: #fff;
      font-weight: 800;
      font-size: 1rem;
      cursor: pointer;
    }

    /* ================= 5. DEDICATED CHECKOUT & ADDRESS PAGE ================= */
    #checkout-page {
      display: none;
      min-height: 100vh;
      background: radial-gradient(circle at top, #1f1612 0%, #0d0d10 85%);
      padding: 28px 5% 60px;
    }

    .checkout-container {
      max-width: 560px;
      margin: 0 auto;
      background: #18181f;
      border: 2px solid var(--brand-orange);
      border-radius: 18px;
      padding: 24px 20px;
      box-shadow: 0 15px 40px rgba(0, 0, 0, 0.75);
    }

    .back-to-menu-btn {
      background: transparent;
      border: 1.5px solid var(--brand-orange);
      color: var(--brand-orange);
      padding: 9px 15px;
      border-radius: 8px;
      font-weight: 700;
      cursor: pointer;
      margin-bottom: 18px;
      display: inline-block;
      transition: all 0.2s;
      font-size: 0.88rem;
    }

    .back-to-menu-btn:hover {
      background: var(--brand-orange);
      color: #fff;
    }

    .checkout-page-title {
      font-size: 1.55rem;
      font-weight: 900;
      color: var(--brand-orange);
      margin-bottom: 6px;
    }

    .checkout-page-sub {
      color: var(--text-muted);
      font-size: 0.88rem;
      margin-bottom: 18px;
    }

    .order-summary-preview {
      background: #111116;
      border-left: 4px solid var(--brand-green);
      padding: 13px 15px;
      border-radius: 10px;
      font-size: 0.88rem;
      color: var(--text-muted);
      margin-bottom: 20px;
      line-height: 1.6;
    }

    .form-row-2 {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }

    .form-group {
      margin-bottom: 15px;
    }

    .form-group label {
      display: block;
      font-size: 0.9rem;
      font-weight: 700;
      margin-bottom: 6px;
      color: var(--text-light);
    }

    .house-trigger {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      cursor: pointer;
      color: var(--brand-yellow);
      text-decoration: underline dotted var(--brand-orange);
      transition: transform 0.15s ease, color 0.15s ease;
    }

    .house-trigger:hover {
      color: var(--brand-orange);
      transform: scale(1.03);
    }

    .form-group input,
    .form-group textarea {
      width: 100%;
      padding: 13px;
      border-radius: 10px;
      border: 1.5px solid #32323e;
      background: #101015;
      color: #fff;
      font-size: 16px;
      outline: none;
      transition: border-color 0.2s;
    }

    .form-group input:focus,
    .form-group textarea:focus {
      border-color: var(--brand-green);
    }

    .submit-order-btn {
      width: 100%;
      padding: 15px;
      border: none;
      border-radius: 10px;
      background: linear-gradient(90deg, var(--brand-green), #16a34a);
      color: #052e16;
      font-weight: 900;
      font-size: 1.05rem;
      cursor: pointer;
      margin-top: 6px;
      transition: transform 0.2s;
    }

    .submit-order-btn:hover {
      transform: translateY(-2px);
    }

    .contact-alt {
      text-align: center;
      margin-top: 18px;
      padding-top: 14px;
      border-top: 1px dashed #2e2e38;
      font-size: 0.95rem;
      font-weight: 700;
      color: var(--brand-yellow);
    }

    .contact-alt a {
      color: var(--brand-green);
      text-decoration: none;
    }

    .contact-alt a:hover {
      text-decoration: underline;
    }

    /* ================= POP-UP BOX ================= */
    .info-popup-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.82);
      backdrop-filter: blur(5px);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 12000;
      padding: 20px;
    }

    .info-popup-backdrop.show {
      display: flex;
      animation: popupFade 0.22s ease;
    }

    @keyframes popupFade {
      from { opacity: 0; transform: scale(0.92); }
      to { opacity: 1; transform: scale(1); }
    }

    .info-popup-box {
      background: #18181f;
      border: 2px solid var(--brand-orange);
      border-radius: 16px;
      max-width: 400px;
      width: 100%;
      padding: 24px;
      text-align: center;
      box-shadow: 0 18px 45px rgba(0, 0, 0, 0.85);
    }

    .info-popup-emoji {
      font-size: 2.6rem;
      margin-bottom: 10px;
    }

    .info-popup-title {
      font-size: 1.3rem;
      font-weight: 900;
      color: var(--brand-yellow);
      margin-bottom: 10px;
    }

    .info-popup-text {
      color: var(--text-light);
      font-size: 0.98rem;
      line-height: 1.55;
      margin-bottom: 14px;
    }

    .info-popup-number {
      background: rgba(34, 197, 94, 0.14);
      border: 1px solid var(--brand-green);
      color: var(--brand-green);
      font-weight: 800;
      padding: 10px 14px;
      border-radius: 10px;
      margin-bottom: 18px;
      font-size: 0.95rem;
    }

    .info-popup-number a {
      color: var(--brand-green);
      text-decoration: none;
    }

    .info-popup-btn {
      background: linear-gradient(90deg, var(--brand-red), var(--brand-orange));
      color: #fff;
      border: none;
      padding: 11px 28px;
      border-radius: 50px;
      font-weight: 800;
      cursor: pointer;
      font-size: 0.95rem;
    }

    /* ================= CUSTOM MOBILE VIEW & BOTTOM DOCK ================= */
    .mobile-bottom-dock {
      display: none;
    }

    footer {
      text-align: center;
      padding: 26px 5%;
      background: #0c0c0f;
      border-top: 2px solid #22222a;
      color: var(--text-muted);
      font-size: 0.88rem;
    }

    footer span {
      color: var(--brand-orange);
      font-weight: 700;
    }

    @media (max-width: 640px) {
      header {
        padding: 10px 4%;
      }

      .brand-lockup svg {
        width: 42px;
        height: 42px;
      }

      .brand-title h1 {
        font-size: 1.3rem;
      }

      .brand-title span {
        font-size: 0.65rem;
      }

      .replay-btn {
        padding: 7px 10px;
        font-size: 0.76rem;
      }

      .cart-btn {
        padding: 8px 11px;
        font-size: 0.8rem;
      }

      .hero {
        padding: 24px 4%;
      }

      .deals-section {
        padding: 24px 4% 96px;
      }

      .deals-grid {
        grid-template-columns: 1fr;
        gap: 16px;
      }

      .deal-banner {
        height: 114px;
      }

      .form-row-2 {
        grid-template-columns: 1fr;
        gap: 0;
      }

      .side-menu-drawer {
        width: 100vw;
        max-width: 100vw;
        border-left: none;
      }

      .cart-drawer {
        width: 100vw;
        border-left: none;
      }

      footer {
        padding-bottom: 92px;
      }

      .mobile-bottom-dock {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        z-index: 450;
        background: rgba(16, 16, 21, 0.98);
        backdrop-filter: blur(12px);
        border-top: 2px solid var(--brand-orange);
        display: grid;
        grid-template-columns: 1fr 1fr 1.15fr;
        gap: 8px;
        padding: 9px 12px calc(9px + env(safe-area-inset-bottom));
        box-shadow: 0 -8px 24px rgba(0, 0, 0, 0.75);
      }

      .dock-btn {
        border: 1.5px solid #2f2f3c;
        background: #1d1d26;
        color: var(--text-light);
        border-radius: 10px;
        padding: 10px 8px;
        font-size: 0.8rem;
        font-weight: 800;
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 5px;
      }

      .dock-btn.dock-order {
        background: linear-gradient(90deg, var(--brand-red), var(--brand-orange));
        border: none;
        color: #fff;
      }
    }
  </style>
</head>
<body>

  <!-- ================= 1. BLACK INTRO SPLASH SCREEN ================= -->
  <section id="intro-screen">
    <p class="intro-hint">Tap a Letter to Enter</p>
    <p class="intro-sub-legend">H &amp; F → Hot Deals &nbsp;|&nbsp; C → Menu Picture</p>
    <div class="logo-selector">
      <div class="letter-wrapper">
        <div class="letter-box" data-target="deals" title="Tap H for HFC Hot Deals">H</div>
        <span class="letter-label">Hot Deals</span>
      </div>
      <div class="letter-wrapper">
        <div class="letter-box" data-target="deals" title="Tap F for HFC Hot Deals">F</div>
        <span class="letter-label">Hot Deals</span>
      </div>
      <div class="letter-wrapper">
        <div class="letter-box" data-target="menu" title="Tap C for Menu Picture">C</div>
        <span class="letter-label">Menu Card</span>
      </div>
    </div>
  </section>

  <!-- ================= 2. BIG WIDE YELLOW WOBBLE ANIMATION ================= -->
  <section id="yellow-animation-stage">
    <div class="big-yellow-hfc" id="animated-word">HFC</div>
    <div class="big-yellow-sub" id="animated-sub">Healthy Fry-chicks</div>
    <button type="button" class="enter-now-btn" id="stage-enter-btn" onclick="proceedToTarget()">Continue →</button>
  </section>

  <!-- Side Menu Backdrop & Drawer (Opened from Top-Right Three Lines) -->
  <div class="side-menu-backdrop" id="side-menu-backdrop" onclick="closeSideMenu()"></div>
  <aside class="side-menu-drawer" id="side-menu-drawer" aria-label="HFC Menu Categories">
    <div class="side-menu-header">
      <h3>☰ Select Category</h3>
      <button type="button" class="close-side-menu" onclick="closeSideMenu()" title="Close menu">✕</button>
    </div>
    <div class="side-menu-list" id="side-menu-list"></div>
  </aside>

  <!-- ================= 3. HOT DEALS & SINGLE-CATEGORY VIEW (H & F) ================= -->
  <div id="main-home">
    <header>
      <div class="brand-lockup" onclick="replayIntro()">
        <svg width="50" height="50" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg">
          <circle cx="60" cy="60" r="54" fill="#ffffff" stroke="#e62e2d" stroke-width="6"/>
          <circle cx="60" cy="60" r="47" fill="none" stroke="#ff7b00" stroke-width="4"/>
          <g stroke="#e62e2d" stroke-width="4" stroke-linecap="round">
            <line x1="48" y1="22" x2="72" y2="44" />
            <line x1="72" y1="22" x2="48" y2="44" />
          </g>
          <text x="60" y="75" text-anchor="middle" font-family="Arial Black, sans-serif" font-size="30" font-weight="900" fill="#ff7b00" stroke="#e62e2d" stroke-width="1.5">HFC</text>
          <text x="60" y="95" text-anchor="middle" font-family="Arial, sans-serif" font-size="8.5" font-weight="800" fill="#22c55e">HEALTHY FRY-CHICKS</text>
        </svg>
        <div class="brand-title">
          <h1>HFC</h1>
          <span id="header-active-label">Hot Deals</span>
        </div>
      </div>

      <div class="nav-actions">
        <button type="button" class="replay-btn" onclick="replayIntro()">↺ Intro</button>
        <button type="button" class="cart-btn" onclick="toggleCart()">
          🛒 Order <span class="cart-count" id="cart-count">0</span>
        </button>
        <button type="button" class="three-line-btn" onclick="openSideMenu()" aria-label="Open menu categories" title="Open HFC Categories">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </header>

    <section class="hero">
      <div class="health-badge">🔥 Free Home Delivery (Min. Order Rs. 500) • Haroonabad</div>
      <h2>
        <span class="red">Healthy</span> <span class="orange">Fry-chicks</span>
        <span class="green" id="hero-category-badge">Hot Deals</span>
      </h2>
      <p>
        Only the selected category is shown below. Tap the <strong>☰</strong> button in the top-right corner to switch to <strong>Pizza</strong>, <strong>Burger</strong>, or any other category.
      </p>
      <button type="button" class="hero-menu-trigger" onclick="openSideMenu()">
        ☰ Browse All Categories (Pizza, Burgers &amp; More)
      </button>
    </section>

    <main class="deals-section" id="dynamic-menu-container"></main>

    <footer>
      © 2026 <span>HFC — Healthy Fry-chicks</span> • Fortabbas Road, Haroonabad • <span style="color:#22c55e;">+92 343 5871277</span>
    </footer>

    <!-- Mobile Sticky Bottom Dock -->
    <div class="mobile-bottom-dock">
      <button type="button" class="dock-btn" onclick="openSideMenu()">☰ Categories</button>
      <button type="button" class="dock-btn" onclick="selectCategory('cat-deals')">🔥 Hot Deals</button>
      <button type="button" class="dock-btn dock-order" onclick="toggleCart()">
        🛒 Cart (<span id="mobile-cart-count">0</span>)
      </button>
    </div>
  </div>

  <!-- ================= 4. MENU PICTURE PAGE (C DESTINATION) ================= -->
  <section id="menu-picture-page">
    <header>
      <div class="brand-lockup" onclick="replayIntro()">
        <svg width="50" height="50" viewBox="0 0 120 120" xmlns="http://www.w3.org/2000/svg">
          <circle cx="60" cy="60" r="54" fill="#ffffff" stroke="#e62e2d" stroke-width="6"/>
          <circle cx="60" cy="60" r="47" fill="none" stroke="#ff7b00" stroke-width="4"/>
          <g stroke="#e62e2d" stroke-width="4" stroke-linecap="round">
            <line x1="48" y1="22" x2="72" y2="44" />
            <line x1="72" y1="22" x2="48" y2="44" />
          </g>
          <text x="60" y="75" text-anchor="middle" font-family="Arial Black, sans-serif" font-size="30" font-weight="900" fill="#ff7b00" stroke="#e62e2d" stroke-width="1.5">HFC</text>
          <text x="60" y="95" text-anchor="middle" font-family="Arial, sans-serif" font-size="8.5" font-weight="800" fill="#22c55e">HEALTHY FRY-CHICKS</text>
        </svg>
        <div class="brand-title">
          <h1>HFC</h1>
          <span>Menu Card</span>
        </div>
      </div>

      <div class="nav-actions">
        <button type="button" class="replay-btn" onclick="replayIntro()">↺ Intro</button>
        <button type="button" class="cart-btn" onclick="selectCategory('cat-deals')">🔥 Hot Deals</button>
        <button type="button" class="three-line-btn" onclick="openSideMenu()" aria-label="Open menu categories" title="Open HFC Categories">
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </header>

    <div class="menu-poster-wrapper">
      <div class="menu-poster-card">
        <div class="poster-header">
          <h2>🍕 HEALTHY FRY-CHICKS (HFC) MENU</h2>
          <p>Spicy, Saucy &amp; Crispy • Free Home Delivery (Min. Order Rs. 500)</p>
        </div>

        <div class="poster-grid" id="poster-menu-grid"></div>

        <div class="poster-footer">
          <div class="poster-contact">
            📍 Fortabbas Road, Haroonabad &nbsp;|&nbsp; 📞 <a href="tel:+923435871277">+92 343 5871277</a>
          </div>
          <button type="button" class="go-deals-cta" onclick="selectCategory('cat-deals')">Order Hot Deals →</button>
        </div>
      </div>
    </div>

    <footer>
      © 2026 <span>HFC — Healthy Fry-chicks</span> • Fresh, Crispy &amp; Wholesome.
    </footer>
  </section>

  <!-- Slide-Out Order Drawer -->
  <aside class="cart-drawer" id="cart-drawer">
    <div class="cart-header">
      <h3>🛒 Your HFC Order</h3>
      <div class="cart-header-actions">
        <button type="button" class="clear-cart-btn" onclick="clearCart()" title="Clear all items from cart">Clear Cart</button>
        <button type="button" class="close-cart" onclick="toggleCart()" title="Close cart drawer">✕</button>
      </div>
    </div>
    <div class="cart-items" id="cart-items">
      <p style="color: var(--text-muted); text-align:center; margin-top: 40px;">Your cart is empty. Pick an item!</p>
    </div>
    <div class="cart-total-box">
      <div style="display:flex; justify-content:space-between; font-size:1.15rem; font-weight:800;">
        <span>Total:</span>
        <span style="color: var(--brand-orange);" id="cart-total">Rs. 0</span>
      </div>
      <button type="button" class="checkout-btn" onclick="goToCheckoutPage()">Confirm Order →</button>
    </div>
  </aside>

  <!-- ================= 5. DEDICATED CHECKOUT & ADDRESS PAGE ================= -->
  <section id="checkout-page">
    <div class="checkout-container">
      <button type="button" class="back-to-menu-btn" onclick="backToHomePage()">← Back to Selected Category</button>

      <h2 class="checkout-page-title">📋 Enter Delivery Details</h2>
      <p class="checkout-page-sub">Complete your order below for fast, fresh HFC delivery.</p>

      <div class="order-summary-preview" id="page-order-summary"></div>

      <form action="https://formspree.io/f/mgaeegln" method="POST" id="hfc-order-form" onsubmit="handleOrderSubmit(event)">
        <input type="hidden" name="Ordered_Items" id="hidden-order-items" />
        <input type="hidden" name="Total_Bill" id="hidden-order-total" />

        <div class="form-row-2">
          <div class="form-group">
            <label for="username">Username (Editable) *</label>
            <input type="text" id="username" name="Username" value="hfc_guest" placeholder="Change username" required />
          </div>

          <div class="form-group">
            <label for="full-name">Full Name *</label>
            <input type="text" id="full-name" name="Full_Name" placeholder="Enter your full name" required />
          </div>
        </div>

        <div class="form-row-2">
          <div class="form-group">
            <label for="phone-number">Phone Number *</label>
            <input type="tel" id="phone-number" name="Phone_Number" placeholder="03XX-XXXXXXX" required />
          </div>

          <div class="form-group">
            <label for="address-area">Area of Address *</label>
            <input type="text" id="address-area" name="Address_Area" placeholder="Fortabbas Rd / Block / Area" required />
          </div>
        </div>

        <div class="form-group">
          <label for="delivery-address">
            <span class="house-trigger" onclick="openHouseAddressPopup()" title="Click for address & contact info">
              🏠 Address
            </span> *
          </label>
          <textarea id="delivery-address" name="Delivery_Address" rows="3" placeholder="House #, Street #, Landmark, Haroonabad" required></textarea>
        </div>

        <button type="submit" class="submit-order-btn">Submit Order ✓</button>

        <button type="button" class="submit-order-btn" style="background: linear-gradient(90deg, #25d366, #16a34a); color: #052e16; margin-top: 10px;" onclick="sendOrderToWhatsApp()">
          💬 Send Order on WhatsApp
        </button>

        <p class="contact-alt">or contact at: <a href="tel:+923435871277">+92 343 5871277</a></p>
      </form>
    </div>
  </section>

  <!-- Pop-Up Modal (House Address Reminder & Order Contact) -->
  <div class="info-popup-backdrop" id="info-popup">
    <div class="info-popup-box">
      <div class="info-popup-emoji" id="popup-emoji">🏠</div>
      <h3 class="info-popup-title" id="popup-title">Please Enter an Address</h3>
      <p class="info-popup-text" id="popup-message">
        Type your house/street address in the box below so we can deliver your order.
      </p>
      <div class="info-popup-number" id="popup-contact">
        Contact at: <a href="tel:+923435871277">+92 343 5871277</a>
      </div>
      <button type="button" class="info-popup-btn" onclick="closeInfoPopup()">Got It</button>
    </div>
  </div>

  <script>
    // ================= FULL ORGANIZED & CATEGORIZED MENU DATA =================
    const MENU_CATEGORIES = [
      {
        id: 'cat-deals',
        menuLabel: '🔥 Hot Deals',
        title: 'Hot',
        highlight: 'Deals',
        subtitle: 'Zinger Burger Combos & Drinks',
        bannerClass: 'red-orange',
        emoji: '🍔',
        items: [
          {
            id: 'deal-1',
            name: 'Zinger Burger + Tin Pack',
            tag: 'Hot Deal',
            desc: 'Crispy zinger burger paired with a chilled tin drink.',
            price: 440
          },
          {
            id: 'deal-2',
            name: '2 Zinger Burgers + 500 ml Drink',
            tag: 'Hot Combo',
            desc: 'Two crispy zinger burgers with a 500 ml bottle drink.',
            price: 770
          },
          {
            id: 'deal-3',
            name: '3 Zinger Burgers + 1 Ltr Drink',
            tag: 'Group Deal',
            desc: 'Three zinger burgers served with a 1 litre drink.',
            price: 1140
          },
          {
            id: 'deal-4',
            name: '4 Zinger Burgers + 1.5 Ltr Drink',
            tag: 'Family Deal',
            desc: 'Four zinger burgers with a large 1.5 litre drink.',
            price: 1520
          }
        ]
      },
      {
        id: 'cat-burgers',
        menuLabel: '🍔 Burgers',
        title: 'Crispy & Special',
        highlight: 'Burgers',
        subtitle: 'Zinger, Tower, Chicken, Boomer & Chappli Burgers',
        bannerClass: 'red-orange',
        emoji: '🍔',
        items: [
          {
            id: 'bg-1',
            name: 'Zinger Burger',
            tag: 'Burger',
            desc: 'Crispy fried chicken fillet burger with fresh sauce and bun.',
            price: 290
          },
          {
            id: 'bg-2',
            name: 'Zinger Junior Burger',
            tag: 'Junior',
            desc: 'Compact crispy zinger burger ideal for a quick bite.',
            price: 240
          },
          {
            id: 'bg-3',
            name: 'HFC Special Zinger',
            tag: 'House Zinger',
            desc: 'Signature HFC zinger burger loaded with rich toppings.',
            price: 350
          },
          {
            id: 'bg-4',
            name: 'Zinger Tower Burger',
            tag: 'Tower',
            desc: 'Stacked crispy zinger burger with extra layers and flavour.',
            price: 410
          },
          {
            id: 'bg-5',
            name: 'Heavy Zinger Burger',
            tag: 'Heavyweight',
            desc: 'Extra hearty zinger burger for big appetites.',
            price: 470
          },
          {
            id: 'bg-6',
            name: 'Chicken Burger',
            tag: 'Classic',
            desc: 'Savory chicken patty burger served hot.',
            price: 230
          },
          {
            id: 'bg-7',
            name: 'Boomer Burger',
            tag: 'Boomer',
            desc: 'Bold-flavoured chicken burger from the HFC kitchen.',
            price: 250
          },
          {
            id: 'bg-8',
            name: 'Chappli Burger',
            tag: 'Chappli',
            desc: 'Spiced chappli kabab burger with traditional seasoning.',
            price: 230
          }
        ]
      },
      {
        id: 'cat-chicken',
        menuLabel: '🍗 Chicken & Wings',
        title: 'Chicken, Wings &',
        highlight: 'Nuggets',
        subtitle: 'Pieces, Chest, Hot Wings, Nuggets & Pop Shots',
        bannerClass: 'green-orange',
        emoji: '🍗',
        items: [
          {
            id: 'chk-1',
            name: '01 Piece Chicken',
            tag: 'Single Pc',
            desc: 'Crispy golden fried chicken piece.',
            price: 200
          },
          {
            id: 'chk-2',
            name: '01 Pc. Chicken (Chest)',
            tag: 'Chest Cut',
            desc: 'Tender, crispy fried chicken chest piece.',
            price: 230
          },
          {
            id: 'chk-3',
            name: '02 Pcs. Chicken',
            tag: '2 Pieces',
            desc: 'Two pieces of crispy fried chicken.',
            price: 360
          },
          {
            id: 'chk-4',
            name: '05 Pcs. Chicken',
            tag: '5 Pieces',
            desc: 'Five pieces of crispy fried chicken.',
            price: 900
          },
          {
            id: 'chk-5',
            name: '10 Pcs. Chicken',
            tag: '10 Pieces',
            desc: 'Ten pieces of crispy fried chicken for sharing.',
            price: 1800
          },
          {
            id: 'chk-6',
            name: '05 Pcs. Hot Wings',
            tag: 'Hot Wings',
            desc: 'Five spicy and crispy hot chicken wings.',
            price: 200
          },
          {
            id: 'chk-7',
            name: '10 Pcs. Hot Wings',
            tag: 'Hot Wings',
            desc: 'Ten spicy and crispy hot chicken wings.',
            price: 380
          },
          {
            id: 'chk-8',
            name: '05 Pcs. Nuggets',
            tag: 'Nuggets',
            desc: 'Five golden crispy chicken nuggets.',
            price: 200
          },
          {
            id: 'chk-9',
            name: '10 Pcs. Nuggets',
            tag: 'Nuggets',
            desc: 'Ten golden crispy chicken nuggets.',
            price: 380
          },
          {
            id: 'chk-10',
            name: '10 Pcs. Pop Shots',
            tag: 'Pop Shots',
            desc: 'Ten bite-sized crispy chicken pop shots.',
            price: 230
          }
        ]
      },
      {
        id: 'cat-fish-kabab',
        menuLabel: '🐟 Fish & Kababs',
        title: 'Fish &',
        highlight: 'Kababs',
        subtitle: 'Crispy Fish Pieces, Seekh Kabab & Chappli Kabab',
        bannerClass: 'red-green',
        emoji: '🐟',
        items: [
          {
            id: 'fk-1',
            name: '01 Piece Fish',
            tag: 'Fish',
            desc: 'Single crispy fried fish piece.',
            price: 250
          },
          {
            id: 'fk-2',
            name: '05 Piece Fish',
            tag: 'Fish Pack',
            desc: 'Five pieces of crispy fried fish.',
            price: 1200
          },
          {
            id: 'fk-3',
            name: '06 Seekh Kabab',
            tag: 'Seekh Kabab',
            desc: 'Six savoury seasoned seekh kababs.',
            price: 340
          },
          {
            id: 'fk-4',
            name: '02 Chappli Kabab',
            tag: 'Chappli',
            desc: 'Two spiced traditional chappli kababs.',
            price: 200
          },
          {
            id: 'fk-5',
            name: '04 Chappli Kabab',
            tag: 'Chappli Pack',
            desc: 'Four spiced traditional chappli kababs.',
            price: 390
          }
        ]
      },
      {
        id: 'cat-rolls',
        menuLabel: '🌯 Rolls & Shawarma',
        title: 'Rolls &',
        highlight: 'Shawarma',
        subtitle: 'Pratha Rolls, Zinger Rolls, Shawarma & Kabab Roll',
        bannerClass: 'green-orange',
        emoji: '🌯',
        items: [
          {
            id: 'rl-1',
            name: 'Pratha Roll',
            tag: 'Roll',
            desc: 'Flaky pratha rolled with savoury filling and sauce.',
            price: 230
          },
          {
            id: 'rl-2',
            name: 'Zinger Pratha Roll',
            tag: 'Zinger Roll',
            desc: 'Crispy zinger wrapped inside a warm pratha roll.',
            price: 290
          },
          {
            id: 'rl-3',
            name: 'Shawarma',
            tag: 'Shawarma',
            desc: 'Warm bread wrapped with seasoned chicken and sauce.',
            price: 170
          },
          {
            id: 'rl-4',
            name: 'Zinger Shawarma',
            tag: 'Zinger Wrap',
            desc: 'Crispy zinger style shawarma wrap.',
            price: 210
          },
          {
            id: 'rl-5',
            name: 'Kabab Roll',
            tag: 'Kabab Roll',
            desc: 'Savory kabab roll wrapped fresh to order.',
            price: 230
          }
        ]
      },
      {
        id: 'cat-special',
        menuLabel: '👑 Special Pizza',
        title: 'Special',
        highlight: 'Pizza',
        subtitle: 'Tap corner button to pick Medium or Large',
        bannerClass: 'green-orange',
        emoji: '🍕',
        items: [
          {
            id: 'sp-1',
            name: 'Super Special Pizza',
            tag: 'Special',
            desc: 'Loaded house-special pizza with rich toppings and melted cheese.',
            sizes: { Medium: 1300, Large: 1900 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-2',
            name: 'Prime Special Pizza',
            tag: 'Special',
            desc: 'Signature prime topping blend baked golden and cheesy.',
            sizes: { Medium: 1300, Large: 1900 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-3',
            name: 'Dual Afghani Tikka Pizza',
            tag: 'Special',
            desc: 'Double Afghani tikka style spiced chicken and cheese.',
            sizes: { Medium: 1300, Large: 1900 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-4',
            name: 'HFC Special Pizza',
            tag: 'House Special',
            desc: 'Creamy sauce, chicken sausages, fajita chunks, spicy chicken, olives & cheese.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-5',
            name: 'Afghani Tikka Pizza',
            tag: 'Special',
            desc: 'Topped with tikka chicken, grilled onion, capsicum, red sauce, olives & cheese.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-6',
            name: 'Karahi Tikka Pizza',
            tag: 'Spicy',
            desc: 'Karahi sauce, tikka chicken, cheese, ginger, green chilli, capsicum & mushrooms.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-7',
            name: 'Kabab Crest Pizza',
            tag: 'Special',
            desc: 'Garlic sauce, spicy HFC kabab, onion, black olives, sweet corn & mozzarella.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-8',
            name: 'Chicken Supreme Pizza',
            tag: 'Supreme',
            desc: 'Hot sauce, tikka chicken, fajita, smoked chicken, mushrooms, sweet corn & olives.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-9',
            name: 'Fish Tikka Pizza',
            tag: 'Chef Pick',
            desc: 'Dip sauce, fish tikka, cheese, bell pepper, onion and black olives.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'sp-10',
            name: 'Malai Boti Pizza',
            tag: 'Creamy',
            desc: 'Creamy white sauce, malai boti chicken, cheese, green chilli, tomato.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          }
        ]
      },
      {
        id: 'cat-crown',
        menuLabel: '🍕 Crown Pizza',
        title: 'Crown',
        highlight: 'Pizza',
        subtitle: 'Tap corner button to switch Medium or Large',
        bannerClass: 'red-green',
        emoji: '👑',
        items: [
          {
            id: 'cr-1',
            name: 'Crown Stuffed Crust Pizza',
            tag: 'Crown Crust',
            desc: 'Stuffed crust pizza topped with savoury chicken, herbs, and melted cheese.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          },
          {
            id: 'cr-2',
            name: 'Seekh Stuffed Crust Pizza',
            tag: 'Crown Crust',
            desc: 'Stuffed crust pizza with seekh kabab chunks, capsicum, onion & cheese.',
            sizes: { Medium: 1100, Large: 1550 },
            defaultSize: 'Medium'
          }
        ]
      },
      {
        id: 'cat-regular',
        menuLabel: '🌿 Regular Pizza',
        title: 'Regular',
        highlight: 'Pizza',
        subtitle: 'Tap corner button to switch Small, Medium or Large',
        bannerClass: 'red-orange',
        emoji: '🌿',
        items: [
          {
            id: 'reg-1',
            name: 'Special Regular Pizza',
            tag: 'Regular',
            desc: 'Classic HFC pizza with rich cheese and savoury toppings.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-2',
            name: 'Pepperoni Pizza',
            tag: 'Classic',
            desc: 'Savory pepperoni slices with stretchy mozzarella and pizza sauce.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-3',
            name: 'Arabian Green Pizza',
            tag: 'Herbed',
            desc: 'Green sauce, white sauce, garlic onion, fajita chicken, cheese & green chilli.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-4',
            name: 'Pickle Punjabi Pizza',
            tag: 'Desi Tang',
            desc: 'Hot tomato sauce, tikka chunks, onion, cheese, black olives & pickle.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-5',
            name: 'Fajita Pizza',
            tag: 'Fajita',
            desc: 'Hot sauce, fajita chicken, bell pepper and melted cheese.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-6',
            name: 'Chicken Tikka Pizza',
            tag: 'Popular',
            desc: 'Hot sauce, tikka chicken, cheese, tomato and red onion.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-7',
            name: 'Chicken Sweet Corn Pizza',
            tag: 'Sweet & Savoury',
            desc: 'Special sauce, tikka chicken, cheese and sweet corn.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-8',
            name: 'Vegetable Pizza',
            tag: 'Veggie',
            desc: 'Tomato sauce, bell pepper, onion, tomato, sweet corn, mushrooms & olives.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-9',
            name: 'Chapli Kabab Pizza',
            tag: 'Chapli Style',
            desc: 'White sauce, grilled chapli chicken, onion, black olives, pepper & herb sauce.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-10',
            name: 'BBQ Pizza',
            tag: 'Smoky BBQ',
            desc: 'BBQ sauce, tikka chicken, smoked chicken, green onion, cheese, bacon & olives.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          },
          {
            id: 'reg-11',
            name: 'Cheese Lover Pizza',
            tag: 'Extra Cheesy',
            desc: 'Tomato sauce, cheddar and mozzarella cheese.',
            sizes: { Small: 550, Medium: 950, Large: 1350 },
            defaultSize: 'Medium'
          }
        ]
      },
      {
        id: 'cat-sides',
        menuLabel: '🍝 Pasta, Rice & Fries',
        title: 'Pasta, Rice &',
        highlight: 'Fries',
        subtitle: 'Pasta, Singapuri & Chilli Rice, Fries, Raita & Extras',
        bannerClass: 'green-orange',
        emoji: '🍝',
        items: [
          {
            id: 'side-1',
            name: 'Macaroni Pasta',
            tag: 'Pasta',
            desc: 'Hot, saucy macaroni pasta cooked fresh to order.',
            price: 600
          },
          {
            id: 'side-2',
            name: 'Alfredo Pasta',
            tag: 'Pasta',
            desc: 'Creamy Alfredo pasta with rich seasoning.',
            price: 600
          },
          {
            id: 'side-3',
            name: 'White Sauce Pasta',
            tag: 'Pasta',
            desc: 'Smooth white sauce pasta with classic flavour.',
            price: 600
          },
          {
            id: 'side-4',
            name: 'Loaded Fries',
            tag: 'Fries',
            desc: 'Crispy golden fries loaded with savoury toppings.',
            price: 600
          },
          {
            id: 'side-5',
            name: 'Loaded Fries with Cheese',
            tag: 'Cheesy Fries',
            desc: 'Loaded fries topped generously with melted cheese.',
            price: 600
          },
          {
            id: 'side-6',
            name: 'Singapuri Rice',
            tag: 'Rice',
            desc: 'Flavorful Singapuri rice prepared fresh.',
            price: 240
          },
          {
            id: 'side-7',
            name: 'Chilli Crispy Rice',
            tag: 'Rice',
            desc: 'Spicy and crispy rice dish.',
            price: 240
          },
          {
            id: 'side-8',
            name: 'Fries Reg.',
            tag: 'Fries',
            desc: 'Regular portion of golden fries.',
            price: 150
          },
          {
            id: 'side-9',
            name: 'Fries Large',
            tag: 'Fries',
            desc: 'Large portion of golden fries.',
            price: 240
          },
          {
            id: 'side-10',
            name: 'Fries Family Size',
            tag: 'Family Fries',
            desc: 'Family-sized portion of golden fries.',
            price: 350
          },
          {
            id: 'side-11',
            name: 'Raita',
            tag: 'Side',
            desc: 'Fresh raita to pair with rice or kababs.',
            price: 120
          },
          {
            id: 'side-12',
            name: 'Dip Sauce',
            tag: 'Dip',
            desc: 'Savory dipping sauce.',
            price: 140
          },
          {
            id: 'side-13',
            name: 'Dinner Roll',
            tag: 'Bread',
            desc: 'Soft dinner roll.',
            price: 50
          },
          {
            id: 'side-14',
            name: 'Pratha',
            tag: 'Bread',
            desc: 'Freshly cooked pratha.',
            price: 60
          },
          {
            id: 'side-15',
            name: 'Extra Cheese',
            tag: 'Add-On',
            desc: 'Extra cheese add-on portion.',
            price: 60
          },
          {
            id: 'side-16',
            name: 'Disposable Glass',
            tag: 'Add-On',
            desc: 'Disposable drinking glass.',
            price: 5
          }
        ]
      },
      {
        id: 'cat-treats',
        menuLabel: '🍦 Water & Ice Cream',
        title: 'Water &',
        highlight: 'Ice Cream',
        subtitle: 'Mineral Water & Small / Medium / Large Ice Cream',
        bannerClass: 'red-green',
        emoji: '🍦',
        items: [
          {
            id: 'tr-1',
            name: 'Mineral Water Reg.',
            tag: 'Water',
            desc: 'Regular bottle of mineral water.',
            price: 50
          },
          {
            id: 'tr-2',
            name: 'Mineral Water Large',
            tag: 'Water',
            desc: 'Large bottle of mineral water.',
            price: 90
          },
          {
            id: 'tr-3',
            name: 'Ice Cream Small',
            tag: 'Ice Cream',
            desc: 'Small serving of ice cream.',
            price: 70
          },
          {
            id: 'tr-4',
            name: 'Ice Cream Medium',
            tag: 'Ice Cream',
            desc: 'Medium serving of ice cream.',
            price: 120
          },
          {
            id: 'tr-5',
            name: 'Ice Cream Large',
            tag: 'Ice Cream',
            desc: 'Large serving of ice cream.',
            price: 180
          }
        ]
      }
    ];

    let activeCategoryId = 'cat-deals';

    const selectedSizes = {};
    MENU_CATEGORIES.forEach(cat => {
      cat.items.forEach(item => {
        if (item.sizes) {
          selectedSizes[item.id] = item.defaultSize || Object.keys(item.sizes)[0];
        }
      });
    });

    function renderSideMenu() {
      const sideList = document.getElementById('side-menu-list');
      const categoryButtons = MENU_CATEGORIES.map(cat => `
        <button type="button" class="side-menu-item ${cat.id === activeCategoryId ? 'active-cat' : ''}" onclick="selectCategory('${cat.id}')">
          <span>${cat.menuLabel}</span>
          <span>→</span>
        </button>
      `).join('');

      const extraButtons = `
        <button type="button" class="side-menu-item" onclick="closeSideMenu(); showMenuPicturePage();">
          <span>📋 Full Menu Card</span>
          <span>→</span>
        </button>
        <button type="button" class="side-menu-item" onclick="closeSideMenu(); toggleCart();">
          <span>🛒 View Cart</span>
          <span>→</span>
        </button>
      `;

      sideList.innerHTML = categoryButtons + extraButtons;
    }

    function openSideMenu() {
      renderSideMenu();
      document.getElementById('side-menu-backdrop').classList.add('open');
      document.getElementById('side-menu-drawer').classList.add('open');
    }

    function closeSideMenu() {
      document.getElementById('side-menu-backdrop').classList.remove('open');
      document.getElementById('side-menu-drawer').classList.remove('open');
    }

    function selectCategory(categoryId) {
      activeCategoryId = categoryId;
      closeSideMenu();
      renderSideMenu();
      renderActiveCategory();
      showDealsPage();
    }

    function renderActiveCategory() {
      const container = document.getElementById('dynamic-menu-container');
      const cat = MENU_CATEGORIES.find(c => c.id === activeCategoryId) || MENU_CATEGORIES[0];

      document.getElementById('header-active-label').textContent = `${cat.title} ${cat.highlight}`;
      document.getElementById('hero-category-badge').textContent = `${cat.title} ${cat.highlight}`;

      const cardsHtml = cat.items.map(item => {
        const hasSizes = Boolean(item.sizes);
        const currentSize = hasSizes ? selectedSizes[item.id] : null;
        const currentPrice = hasSizes ? item.sizes[currentSize] : item.price;
        const availableSizeList = hasSizes ? Object.keys(item.sizes).join(' / ') : 'Single Portion';

        const cornerButtonHtml = hasSizes
          ? `<button type="button" class="corner-size-btn" onclick="cycleItemSize('${item.id}')" title="Tap to switch size (${availableSizeList})">${currentSize} ▾</button>`
          : '';

        const safeName = item.name.replace(/'/g, "\\'");

        return `
          <div class="deal-card">
            <div class="deal-banner ${cat.bannerClass}">
              <div class="banner-top-row">
                <span class="deal-tag">${item.tag}</span>
                ${cornerButtonHtml}
              </div>
              <div class="deal-emoji">${cat.emoji}</div>
            </div>
            <div class="deal-body">
              <div>
                <h4 class="deal-title">${item.name}</h4>
                <p class="deal-desc">${item.desc}</p>
                <span class="size-hint-pill">${hasSizes ? `Sizes: ${availableSizeList}` : 'Freshly Prepared'}</span>
              </div>
              <div class="deal-footer">
                <div class="price-box">
                  <span class="size-label">${hasSizes ? `Size: ${currentSize}` : 'Price'}</span>
                  <span class="new-price">Rs. ${currentPrice.toLocaleString()}</span>
                </div>
                <button type="button" class="add-btn" onclick="addSelectedItem('${item.id}', '${safeName}', ${currentPrice}, ${hasSizes ? `'${currentSize}'` : 'null'})">+ Add</button>
              </div>
            </div>
          </div>
        `;
      }).join('');

      const backButtonHtml = cat.id !== 'cat-deals'
        ? `<button type="button" class="back-hot-deals-btn" onclick="selectCategory('cat-deals')">🔥 Back to Hot Deals</button>`
        : '';

      container.innerHTML = `
        <section class="category-block" id="${cat.id}">
          <div class="section-header">
            <div>
              <h3>${cat.title} <span>${cat.highlight}</span></h3>
              <p>${cat.subtitle}</p>
            </div>
            ${backButtonHtml}
          </div>
          <div class="deals-grid">${cardsHtml}</div>
        </section>
      `;
    }

    function cycleItemSize(itemId) {
      let targetItem = null;
      for (const cat of MENU_CATEGORIES) {
        const found = cat.items.find(i => i.id === itemId);
        if (found) {
          targetItem = found;
          break;
        }
      }
      if (!targetItem || !targetItem.sizes) return;

      const sizeKeys = Object.keys(targetItem.sizes);
      const currentIdx = sizeKeys.indexOf(selectedSizes[itemId]);
      const nextSize = sizeKeys[(currentIdx + 1) % sizeKeys.length];
      selectedSizes[itemId] = nextSize;
      renderActiveCategory();
    }

    function addSelectedItem(itemId, name, price, sizeName) {
      const displayTitle = sizeName ? `${name} (${sizeName})` : name;
      addToCart(displayTitle, price);
    }

    function renderMenuPictureCard() {
      const posterGrid = document.getElementById('poster-menu-grid');
      posterGrid.innerHTML = MENU_CATEGORIES.map(cat => {
        const rows = cat.items.map(item => {
          const priceText = item.sizes
            ? Object.entries(item.sizes).map(([sz, pr]) => `${sz[0]}: ${pr}`).join(' | ')
            : `Rs. ${item.price}`;
          return `
            <div class="poster-item">
              <span class="poster-item-name">${item.name}</span>
              <span class="poster-item-price">${priceText}</span>
            </div>
          `;
        }).join('');

        return `
          <div class="poster-category">
            <h3>${cat.emoji} ${cat.title} ${cat.highlight}</h3>
            ${rows}
          </div>
        `;
      }).join('');
    }

    renderSideMenu();
    renderActiveCategory();
    renderMenuPictureCard();

    // ================= INTRO, ANIMATION & PAGE ROUTING =================
    const introScreen = document.getElementById('intro-screen');
    const yellowStage = document.getElementById('yellow-animation-stage');
    const mainHome = document.getElementById('main-home');
    const menuPicturePage = document.getElementById('menu-picture-page');
    const checkoutPage = document.getElementById('checkout-page');
    const infoPopup = document.getElementById('info-popup');
    const letters = document.querySelectorAll('.letter-box');

    let transitionTimer;
    let selectedDestination = 'deals';

    letters.forEach(letter => {
      letter.addEventListener('click', () => {
        selectedDestination = letter.getAttribute('data-target') || 'deals';

        const stageBtn = document.getElementById('stage-enter-btn');
        const stageSub = document.getElementById('animated-sub');

        if (selectedDestination === 'menu') {
          stageSub.textContent = 'HFC Menu Picture';
          stageBtn.textContent = 'View Menu Picture →';
        } else {
          activeCategoryId = 'cat-deals';
          renderActiveCategory();
          stageSub.textContent = 'Healthy Fry-chicks • Hot Deals';
          stageBtn.textContent = 'View Hot Deals →';
        }

        introScreen.classList.add('fade-out');
        yellowStage.classList.add('active');

        const word = document.getElementById('animated-word');
        word.style.animation = 'none';
        word.offsetHeight;
        word.style.animation = null;

        clearTimeout(transitionTimer);
        transitionTimer = setTimeout(() => {
          proceedToTarget();
        }, 3200);
      });
    });

    function proceedToTarget() {
      clearTimeout(transitionTimer);
      yellowStage.classList.remove('active');
      introScreen.classList.add('fade-out');

      if (selectedDestination === 'menu') {
        showMenuPicturePage();
      } else {
        activeCategoryId = 'cat-deals';
        renderActiveCategory();
        showDealsPage();
      }
    }

    function showDealsPage() {
      clearTimeout(transitionTimer);
      yellowStage.classList.remove('active');
      introScreen.classList.add('fade-out');
      menuPicturePage.style.display = 'none';
      checkoutPage.style.display = 'none';
      mainHome.classList.add('visible');
      mainHome.style.display = 'block';
      window.scrollTo(0, 0);
    }

    function showMenuPicturePage() {
      clearTimeout(transitionTimer);
      yellowStage.classList.remove('active');
      introScreen.classList.add('fade-out');
      mainHome.classList.remove('visible');
      mainHome.style.display = 'none';
      checkoutPage.style.display = 'none';
      menuPicturePage.style.display = 'block';
      window.scrollTo(0, 0);
    }

    function replayIntro() {
      clearTimeout(transitionTimer);
      closeSideMenu();
      mainHome.classList.remove('visible');
      mainHome.style.display = 'none';
      menuPicturePage.style.display = 'none';
      checkoutPage.style.display = 'none';
      yellowStage.classList.remove('active');
      introScreen.classList.remove('fade-out');
    }

    // ================= CART WITH QUANTITY +/- & CLEAR CART =================
    let cart = [];

    function addToCart(name, price) {
      const existing = cart.find(item => item.name === name && item.price === price);
      if (existing) {
        existing.qty += 1;
      } else {
        cart.push({ name, price, qty: 1 });
      }
      updateCartUI();
      document.getElementById('cart-drawer').classList.add('open');
    }

    function changeQty(index, delta) {
      if (!cart[index]) return;
      cart[index].qty += delta;
      if (cart[index].qty <= 0) {
        cart.splice(index, 1);
      }
      updateCartUI();
    }

    function clearCart() {
      cart = [];
      updateCartUI();
    }

    function getTotalItemCount() {
      return cart.reduce((sum, item) => sum + item.qty, 0);
    }

    function getTotalPrice() {
      return cart.reduce((sum, item) => sum + (item.price * item.qty), 0);
    }

    function updateCartUI() {
      const countEl = document.getElementById('cart-count');
      const mobileCountEl = document.getElementById('mobile-cart-count');
      const itemsEl = document.getElementById('cart-items');
      const totalEl = document.getElementById('cart-total');
      const totalItems = getTotalItemCount();

      countEl.textContent = totalItems;
      if (mobileCountEl) mobileCountEl.textContent = totalItems;

      if (cart.length === 0) {
        itemsEl.innerHTML = '<p style="color: var(--text-muted); text-align:center; margin-top: 40px;">Your cart is empty. Pick an item!</p>';
        totalEl.textContent = 'Rs. 0';
        return;
      }

      itemsEl.innerHTML = cart.map((item, idx) => {
        const lineTotal = item.price * item.qty;
        return `
          <div class="cart-item">
            <div class="cart-item-info">
              <strong style="display:block; font-size:0.93rem;">${item.name}</strong>
              <span style="color: var(--brand-orange); font-weight:700; font-size:0.88rem;">Rs. ${lineTotal.toLocaleString()}</span>
              <span style="color: var(--text-muted); font-size:0.75rem; display:block;">Rs. ${item.price.toLocaleString()} each</span>
            </div>
            <div class="qty-controls">
              <button type="button" class="qty-btn minus" onclick="changeQty(${idx}, -1)" aria-label="Decrease quantity">−</button>
              <span class="qty-value">${item.qty}</span>
              <button type="button" class="qty-btn" onclick="changeQty(${idx}, 1)" aria-label="Increase quantity">+</button>
            </div>
          </div>
        `;
      }).join('');

      totalEl.textContent = `Rs. ${getTotalPrice().toLocaleString()}`;
    }

    function toggleCart() {
      closeSideMenu();
      document.getElementById('cart-drawer').classList.toggle('open');
    }

    function goToCheckoutPage() {
      if (cart.length === 0) {
        alert('Please add at least one item to your order first!');
        return;
      }

      closeSideMenu();
      document.getElementById('cart-drawer').classList.remove('open');
      mainHome.style.display = 'none';
      menuPicturePage.style.display = 'none';

      const totalAmount = getTotalPrice();
      const itemListText = cart
        .map((item, i) => `${i + 1}. ${item.name} x${item.qty} (Rs. ${(item.price * item.qty).toLocaleString()})`)
        .join(', ');

      document.getElementById('hidden-order-items').value = itemListText;
      document.getElementById('hidden-order-total').value = `Rs. ${totalAmount.toLocaleString()}`;
      document.getElementById('page-order-summary').innerHTML = `
        <strong style="color:#fff;">Your Items:</strong> ${itemListText}<br/>
        <strong style="color:var(--brand-orange);">Total Payable: Rs. ${totalAmount.toLocaleString()}</strong>
      `;

      checkoutPage.style.display = 'block';
      window.scrollTo(0, 0);
    }

    function backToHomePage() {
      checkoutPage.style.display = 'none';
      mainHome.style.display = 'block';
      window.scrollTo(0, 0);
    }

    function openHouseAddressPopup() {
      document.getElementById('popup-emoji').textContent = '🏠';
      document.getElementById('popup-title').textContent = 'Please Enter an Address';
      document.getElementById('popup-message').textContent = 'Type your house/street address in the box below so we can deliver your order.';
      document.getElementById('popup-contact').innerHTML = 'Contact at: <a href="tel:+923435871277">+92 343 5871277</a>';
      infoPopup.classList.add('show');
    }

    function handleOrderSubmit(event) {
      event.preventDefault();
      const form = event.target;
      const addressVal = document.getElementById('delivery-address').value.trim();

      if (!addressVal) {
        openHouseAddressPopup();
        return;
      }

      document.getElementById('popup-emoji').textContent = '📞';
      document.getElementById('popup-title').textContent = 'Order Received!';
      document.getElementById('popup-message').textContent = 'Make sure your address is entered properly, and contact at this number for confirmation:';
      document.getElementById('popup-contact').innerHTML = 'Contact at: <a href="tel:+923435871277">+92 343 5871277</a>';
      infoPopup.classList.add('show');

      fetch(form.action, {
        method: form.method,
        body: new FormData(form),
        headers: { 'Accept': 'application/json' }
      }).catch(() => {});

      const username = document.getElementById('username').value.trim() || 'hfc_guest';
      const fullName = document.getElementById('full-name').value.trim() || 'Not provided';
      const phone = document.getElementById('phone-number').value.trim() || 'Not provided';
      const area = document.getElementById('address-area').value.trim() || 'Not provided';
      const itemsText = document.getElementById('hidden-order-items').value || 'No items';
      const totalText = document.getElementById('hidden-order-total').value || 'Rs. 0';

      const message = [
        '*🍕 New HFC Order*',
        `*Customer:* ${fullName} (@${username})`,
        `*Phone:* ${phone}`,
        `*Area:* ${area}`,
        `*Address:* ${addressVal}`,
        `*Items:* ${itemsText}`,
        `*Total:* ${totalText}`
      ].join('\n');

      const waUrl = `https://wa.me/923435871277?text=${encodeURIComponent(message)}`;
      window.open(waUrl, '_blank', 'noopener,noreferrer');
    }

    function closeInfoPopup() {
      infoPopup.classList.remove('show');
    }

    function sendOrderToWhatsApp() {
      const addressVal = document.getElementById('delivery-address').value.trim();
      if (!addressVal) {
        openHouseAddressPopup();
        return;
      }

      const username = document.getElementById('username').value.trim() || 'hfc_guest';
      const fullName = document.getElementById('full-name').value.trim() || 'Not provided';
      const phone = document.getElementById('phone-number').value.trim() || 'Not provided';
      const area = document.getElementById('address-area').value.trim() || 'Not provided';
      const itemsText = document.getElementById('hidden-order-items').value || 'No items';
      const totalText = document.getElementById('hidden-order-total').value || 'Rs. 0';

      const message = [
        '*🍕 New HFC Order*',
        `*Customer:* ${fullName} (@${username})`,
        `*Phone:* ${phone}`,
        `*Area:* ${area}`,
        `*Address:* ${addressVal}`,
        `*Items:* ${itemsText}`,
        `*Total:* ${totalText}`
      ].join('\n');

      const waUrl = `https://wa.me/923435871277?text=${encodeURIComponent(message)}`;
      window.open(waUrl, '_blank', 'noopener,noreferrer');
    }
  </script>
</body>
</html>
