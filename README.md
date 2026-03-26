<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="description" content="Brainy Trio: three mini games — Liquid Sort, Sudoku, Bollywood Match. Complete all three to reveal your final location." />
  <title>Brainy Trio · Puzzle Hub</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,400;0,9..40,500;0,9..40,600;0,9..40,700&display=swap" rel="stylesheet" />
  <style>
    /* ===== Design system ===== */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      /* Colors – dark + teal & amber */
      --bg: #0c0f14;
      --bg-card: #13171e;
      --bg-elevated: #1a1f28;
      --border: rgba(255, 255, 255, 0.08);
      --border-strong: rgba(255, 255, 255, 0.14);
      --text: #f0f2f5;
      --text-muted: #8b92a0;
      --accent: #14b8a6;
      --accent-strong: #2dd4bf;
      --accent-amber: #f59e0b;
      --accent-amber-strong: #fbbf24;
      --accent-muted: rgba(20, 184, 166, 0.15);
      --success: #22c55e;
      --error: #ef4444;
      --focus-ring: 0 0 0 3px rgba(20, 184, 166, 0.5);
      /* Spacing (4px base) */
      --space-1: 4px;
      --space-2: 8px;
      --space-3: 12px;
      --space-4: 16px;
      --space-5: 20px;
      --space-6: 24px;
      --space-8: 32px;
      --space-10: 40px;
      /* Typography */
      --font-display: "Syne", system-ui, sans-serif;
      --font-sans: "DM Sans", system-ui, sans-serif;
      --text-xs: 0.7rem;
      --text-sm: 0.8rem;
      --text-base: 0.9rem;
      --text-lg: 1rem;
      --text-xl: 1.15rem;
      --text-2xl: 1.75rem;
      --leading-tight: 1.25;
      --leading-normal: 1.5;
      /* Radius & motion */
      --radius-sm: 8px;
      --radius-md: 12px;
      --radius-lg: 16px;
      --radius-full: 9999px;
      --ease: cubic-bezier(0.25, 0.1, 0.25, 1);
      --duration: 0.2s;
      --shadow-card: 0 25px 50px -12px rgba(0, 0, 0, 0.45);
      /* 3D depth */
      --shadow-3d-sm: 0 2px 4px rgba(0,0,0,0.3), 0 4px 8px rgba(0,0,0,0.2);
      --shadow-3d-md: 0 8px 16px rgba(0,0,0,0.4), 0 16px 32px rgba(0,0,0,0.25), 0 0 0 1px rgba(0,0,0,0.1);
      --shadow-3d-lg: 0 20px 40px rgba(0,0,0,0.5), 0 40px 80px rgba(0,0,0,0.3), 0 0 0 1px rgba(0,0,0,0.15);
      --shadow-inset: inset 0 2px 6px rgba(0,0,0,0.4), inset 0 0 0 1px rgba(0,0,0,0.2);
      --shadow-raised: 0 6px 0 rgba(0,0,0,0.2), 0 8px 20px rgba(0,0,0,0.35);
      --highlight-top: linear-gradient(180deg, rgba(255,255,255,0.08) 0%, transparent 50%);
    }

    html { scroll-behavior: smooth; }
    body {
      min-height: 100vh;
      font-family: var(--font-sans);
      font-size: var(--text-base);
      line-height: var(--leading-normal);
      background:
        radial-gradient(ellipse 100% 100% at 50% 0%, #151a22 0%, var(--bg) 50%),
        var(--bg);
      color: var(--text);
      padding: 0 var(--space-4) var(--space-8);
      overflow-y: auto;
      -webkit-font-smoothing: antialiased;
      perspective: 1200px;
    }

    /* Focus visible for accessibility */
    button:focus-visible,
    .nav-btn:focus-visible,
    .option:focus-visible,
    .sudoku-cell:focus-visible {
      outline: none;
      box-shadow: var(--focus-ring);
    }
    .nav-btn { outline: none; }

    /* ===== Layout ===== */
    .app-shell {
      max-width: 680px;
      margin: 0 auto;
      transform-style: preserve-3d;
      overflow: visible;
    }

    /* ===== Hero – 3D recessed panel ===== */
    .hero {
      position: relative;
      text-align: center;
      padding: 4rem var(--space-5) 3.5rem;
      background:
        var(--highlight-top),
        radial-gradient(ellipse 120% 80% at 50% -20%, rgba(20, 184, 166, 0.25) 0%, transparent 50%),
        radial-gradient(ellipse 80% 50% at 80% 50%, rgba(245, 158, 11, 0.1) 0%, transparent 50%),
        var(--bg);
      color: var(--text);
      border: 1px solid var(--border);
      border-radius: 1.25rem;
      box-shadow:
        var(--shadow-inset),
        0 4px 20px rgba(0,0,0,0.3);
      overflow: hidden;
      transform: translateZ(0);
    }
    .hero::before {
      content: "";
      position: absolute;
      inset: 0;
      background: linear-gradient(180deg, transparent 0%, rgba(0,0,0,0.15) 100%);
      pointer-events: none;
      border-radius: inherit;
    }
    .hero-inner {
      position: relative;
      max-width: 520px;
      margin: 0 auto;
    }
    .hero-eyebrow {
      font-family: var(--font-sans);
      font-size: var(--text-xs);
      font-weight: 700;
      letter-spacing: 0.3em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: var(--space-3);
    }
    .hero-title {
      font-family: var(--font-display);
      font-size: clamp(2rem, 6vw, 2.75rem);
      font-weight: 800;
      line-height: 1.1;
      letter-spacing: -0.04em;
      color: var(--text);
    }
    .hero-title .hero-title__highlight {
      display: block;
      color: var(--accent-strong);
      margin-top: 0.35rem;
      font-weight: 700;
    }
    .hero-subtitle {
      margin-top: var(--space-4);
      font-size: 1rem;
      color: var(--text-muted);
      line-height: 1.6;
      max-width: 28rem;
      margin-left: auto;
      margin-right: auto;
    }
    .hero-cta-row {
      margin-top: var(--space-6);
      display: flex;
      justify-content: center;
      align-items: center;
      gap: var(--space-4);
      flex-wrap: wrap;
    }
    .hero-pill {
      display: inline-flex;
      align-items: center;
      gap: var(--space-2);
      padding: var(--space-2) var(--space-4);
      border-radius: var(--radius-full);
      border: 1px solid var(--border-strong);
      background: var(--bg-elevated);
      font-size: var(--text-sm);
      color: var(--text-muted);
      box-shadow: var(--shadow-3d-sm), inset 0 1px 0 rgba(255,255,255,0.06);
    }
    .hero-pill-dot {
      width: 8px;
      height: 8px;
      border-radius: var(--radius-full);
      background: var(--accent-amber);
      flex-shrink: 0;
      animation: pulse-dot 2s ease-in-out infinite;
    }
    @keyframes pulse-dot {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.5; }
    }

    /* ===== App card – 3D floating panel ===== */
    .app {
      margin-top: var(--space-6);
      padding: var(--space-6) var(--space-5) var(--space-5);
      background:
        var(--highlight-top),
        var(--bg-card);
      border: 1px solid rgba(255,255,255,0.06);
      border-radius: 1.5rem;
      box-shadow: var(--shadow-3d-lg);
      position: relative;
      z-index: 1;
      transform: translateZ(20px);
      transition: transform 0.35s var(--ease), box-shadow 0.35s var(--ease);
      overflow: visible;
    }
    .app:hover {
      transform: translateZ(24px) rotateX(1deg);
      box-shadow:
        0 24px 48px rgba(0,0,0,0.5),
        0 48px 96px rgba(0,0,0,0.35),
        0 0 0 1px rgba(0,0,0,0.2),
        0 0 60px rgba(20, 184, 166, 0.08);
    }
    .app__header { margin-bottom: var(--space-2); }
    .badge {
      display: inline-block;
      font-size: 0.65rem;
      font-weight: 700;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--accent-amber);
      padding: var(--space-1) var(--space-3);
      border: 1px solid rgba(245, 158, 11, 0.35);
      border-radius: var(--radius-full);
      background: rgba(245, 158, 11, 0.1);
      box-shadow: var(--shadow-3d-sm), inset 0 1px 0 rgba(255,255,255,0.1);
    }
    .app__title {
      font-family: var(--font-display);
      font-size: var(--text-xl);
      font-weight: 700;
      margin-top: var(--space-2);
      letter-spacing: -0.02em;
    }
    .subtitle {
      font-size: 0.9rem;
      color: var(--text-muted);
      margin: var(--space-2) 0 var(--space-4);
      line-height: 1.5;
    }

    /* ===== Nav – 3D tab bar ===== */
    .nav {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-2);
      margin-bottom: var(--space-5);
      padding: var(--space-2);
      background: rgba(0,0,0,0.25);
      border-radius: var(--radius-md);
      box-shadow: var(--shadow-inset);
    }
    .nav-btn {
      padding: var(--space-3) var(--space-4);
      border: none;
      border-radius: var(--radius-sm);
      border-bottom: 3px solid transparent;
      background: transparent;
      color: var(--text-muted);
      font-family: inherit;
      font-size: var(--text-sm);
      font-weight: 500;
      cursor: pointer;
      transition: color var(--duration) var(--ease),
                  border-color var(--duration) var(--ease),
                  transform var(--duration) var(--ease),
                  box-shadow var(--duration) var(--ease);
      text-align: left;
      display: flex;
      flex-direction: column;
      gap: 2px;
      flex: 1;
      min-width: 0;
    }
    .nav-btn span:first-child { font-weight: 600; }
    .nav-btn span:last-child { font-size: 0.7rem; color: var(--text-muted); opacity: 0.8; }
    .nav-btn:hover {
      color: var(--text);
      transform: translateY(-1px);
    }
    .nav-btn--active {
      color: var(--accent-strong);
      background: rgba(20, 184, 166, 0.12);
      border-bottom-color: var(--accent);
      box-shadow: 0 4px 12px rgba(0,0,0,0.3), inset 0 1px 0 rgba(255,255,255,0.06);
      transform: translateY(-2px);
    }
    .nav-btn--active span:last-child { color: var(--accent); opacity: 0.9; }

    /* ===== Game panels – 3D recessed ===== */
    .game-panel {
      padding: var(--space-5);
      border-radius: 1rem;
      background: var(--bg-elevated);
      border: 1px solid var(--border);
      box-shadow: var(--shadow-inset), 0 4px 12px rgba(0,0,0,0.2);
      overflow: visible;
    }
    .game-panel h2 {
      font-size: var(--text-lg);
      font-weight: 600;
      margin-bottom: var(--space-2);
    }
    .game-panel > p {
      font-size: 0.875rem;
      color: var(--text-muted);
      margin-bottom: var(--space-3);
      line-height: var(--leading-normal);
    }
    .game-panel__rule {
      margin-top: var(--space-3);
      font-size: 0.8125rem;
      color: var(--text-muted);
    }
    .water-tubes-wrap {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-3);
      margin-top: var(--space-3);
      justify-content: center;
    }
    .water-tube {
      display: flex;
      flex-direction: column;
      align-items: stretch;
      box-shadow:
        0 6px 0 rgba(0,0,0,0.25),
        0 8px 24px rgba(0,0,0,0.4),
        inset 0 1px 0 rgba(255,255,255,0.08);
      border: 3px solid rgba(248, 250, 252, 0.75);
      transition: transform 0.2s var(--ease), box-shadow 0.2s var(--ease), border-color 0.2s var(--ease);
    }
    .water-tube:hover:not(.water-tube--selected) {
      transform: translateY(-3px);
      box-shadow:
        0 9px 0 rgba(0,0,0,0.2),
        0 12px 28px rgba(0,0,0,0.45),
        inset 0 1px 0 rgba(255,255,255,0.1);
    }
    .water-tube:active:not(.water-tube--selected) {
      transform: translateY(2px);
      box-shadow:
        0 2px 0 rgba(0,0,0,0.3),
        0 4px 12px rgba(0,0,0,0.35),
        inset 0 2px 4px rgba(0,0,0,0.2);
    }
    /* Selected tube – very obvious + pulse ring */
    .water-tube--selected {
      transform: translateY(-4px) scale(1.06);
      border-color: #2dd4bf !important;
      box-shadow:
        0 0 0 4px rgba(20, 184, 166, 0.45),
        0 0 28px rgba(20, 184, 166, 0.55),
        0 8px 0 rgba(0,0,0,0.2),
        0 12px 32px rgba(0,0,0,0.45),
        inset 0 1px 0 rgba(255,255,255,0.2);
      animation: water-tube-pulse 1.1s ease-in-out infinite;
      z-index: 2;
    }
    @keyframes water-tube-pulse {
      0%, 100% { box-shadow: 0 0 0 4px rgba(20, 184, 166, 0.45), 0 0 28px rgba(20, 184, 166, 0.55), 0 8px 0 rgba(0,0,0,0.2), 0 12px 32px rgba(0,0,0,0.45), inset 0 1px 0 rgba(255,255,255,0.2); }
      50% { box-shadow: 0 0 0 6px rgba(45, 212, 191, 0.5), 0 0 36px rgba(20, 184, 166, 0.65), 0 8px 0 rgba(0,0,0,0.2), 0 12px 32px rgba(0,0,0,0.45), inset 0 1px 0 rgba(255,255,255,0.25); }
    }
    .level-badges { display: flex; gap: var(--space-2); margin-top: var(--space-1); }
    .level-badge {
      font-size: var(--text-xs);
      color: var(--text-muted);
      padding: var(--space-1) var(--space-3);
      border-radius: var(--radius-full);
      border: 1px dashed var(--border);
      box-shadow: inset 0 1px 2px rgba(0,0,0,0.2);
    }

    /* Bollywood header block */
    .bolly-header {
      padding: var(--space-3) var(--space-3);
      border-radius: var(--radius-md);
      border: 1px solid rgba(20, 184, 166, 0.25);
      background: var(--accent-muted);
      margin-bottom: var(--space-2);
      box-shadow: var(--shadow-3d-sm), inset 0 1px 0 rgba(255,255,255,0.06);
    }
    .bolly-header__row {
      font-weight: 700;
      letter-spacing: 0.02em;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .bolly-header__indicator {
      font-size: 0.75rem;
      text-transform: uppercase;
      letter-spacing: 0.08em;
      color: var(--accent-strong);
    }
    .bolly-header__subtitle {
      margin-top: var(--space-1);
      color: var(--text);
      font-size: var(--text-base);
    }
    .bolly-rows { margin-top: var(--space-1); }

    /* Bollywood grid – fixed column ratio, aligned rows */
    .bolly-grid {
      display: grid;
      grid-template-columns: minmax(0, 1.35fr) minmax(0, 1fr);
      gap: var(--space-3) var(--space-4);
      align-items: start;
      width: 100%;
    }
    .bolly-grid__head {
      font-family: var(--font-display);
      font-size: 0.75rem;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      color: var(--accent-strong);
      padding-bottom: var(--space-2);
      border-bottom: 1px solid var(--border);
    }
    .bolly-movie {
      padding: var(--space-3);
      border-radius: var(--radius-md);
      background: rgba(20, 184, 166, 0.1);
      border: 1px solid rgba(20, 184, 166, 0.35);
      color: var(--text);
      font-size: 0.875rem;
      line-height: 1.45;
      word-break: break-word;
      min-height: 2.75rem;
      display: flex;
      align-items: center;
    }
    .bolly-select-wrap {
      min-width: 0;
      width: 100%;
    }
    .bolly-select {
      width: 100%;
      max-width: 100%;
      padding: var(--space-3);
      border-radius: var(--radius-md);
      border: 1px solid var(--border-strong);
      background: var(--bg-card);
      color: var(--text);
      font-family: inherit;
      font-size: 0.875rem;
      cursor: pointer;
      appearance: auto;
    }
    .bolly-select:focus {
      outline: none;
      border-color: var(--accent);
      box-shadow: 0 0 0 2px rgba(20, 184, 166, 0.35);
    }
    @media (max-width: 520px) {
      .bolly-grid {
        grid-template-columns: minmax(0, 1.15fr) minmax(0, 0.85fr);
        gap: var(--space-2) var(--space-3);
      }
      .bolly-movie { font-size: 0.8125rem; padding: var(--space-2); min-height: auto; }
      .bolly-select { padding: var(--space-2); font-size: 0.8125rem; }
    }

    /* Location section */
    .location-section {
      margin-top: var(--space-5);
    }
    .location-section .subtitle { margin-bottom: var(--space-3); }
    .location-section .actions { justify-content: flex-start; margin-top: 0; }

    .options {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: var(--space-3);
      margin-top: var(--space-2);
    }
    .option {
      padding: var(--space-3) var(--space-2);
      border-radius: var(--radius-md);
      border: 1px solid var(--border);
      background: var(--bg-card);
      font-size: var(--text-sm);
      color: var(--text);
      cursor: pointer;
      box-shadow: var(--shadow-3d-sm);
      transition: border-color var(--duration) var(--ease),
                  background-color var(--duration) var(--ease),
                  transform var(--duration) var(--ease),
                  box-shadow var(--duration) var(--ease);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: var(--space-2);
      text-align: center;
    }
    .option:hover {
      border-color: var(--accent);
      background: var(--bg-elevated);
      transform: translateY(-2px);
      box-shadow: 0 6px 16px rgba(0,0,0,0.35), 0 0 0 1px rgba(20,184,166,0.2);
    }
    .option input { accent-color: var(--accent); }
    .option-swatch {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      border: 2px solid var(--border);
    }

    .color-grid { display: grid; gap: var(--space-1); margin-top: var(--space-3); }
    .color-cell {
      aspect-ratio: 1;
      border-radius: var(--radius-sm);
      border: 1px solid var(--border);
      background: var(--bg-card);
      cursor: pointer;
      touch-action: none;
      transition: box-shadow var(--duration) var(--ease);
    }
    .color-cell--endpoint::after {
      content: "";
      position: absolute;
      inset: 6px;
      border-radius: 50%;
      border: 2px solid rgba(0, 0, 0, 0.25);
    }
    .color-cell--path { box-shadow: 0 0 0 2px var(--accent); }

    .actions {
      margin-top: var(--space-4);
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-end;
      gap: var(--space-3);
      align-items: center;
    }
    .actions--sudoku { margin-top: var(--space-3); }

    /* ===== Buttons ===== */
    button {
      font-family: inherit;
      border: none;
      border-radius: var(--radius-sm);
      padding: var(--space-3) var(--space-4);
      font-size: var(--text-base);
      font-weight: 500;
      cursor: pointer;
      transition: transform var(--duration) var(--ease),
                  box-shadow var(--duration) var(--ease),
                  opacity var(--duration) var(--ease);
      display: inline-flex;
      align-items: center;
      gap: var(--space-2);
    }
    .btn-primary {
      background: linear-gradient(180deg, #1dd1c1 0%, var(--accent) 50%, #0d9488 100%);
      color: #0c0f14;
      font-weight: 600;
      border-bottom: 3px solid rgba(0,0,0,0.25);
      box-shadow:
        0 4px 0 rgba(0,0,0,0.2),
        0 6px 20px rgba(20, 184, 166, 0.4),
        inset 0 1px 0 rgba(255,255,255,0.25);
    }
    .btn-primary:hover:not(:disabled) {
      transform: translateY(-2px);
      border-bottom-width: 4px;
      box-shadow:
        0 6px 0 rgba(0,0,0,0.2),
        0 10px 28px rgba(20, 184, 166, 0.5),
        inset 0 1px 0 rgba(255,255,255,0.3);
    }
    .btn-primary:active:not(:disabled) {
      transform: translateY(1px);
      border-bottom-width: 1px;
      box-shadow:
        0 1px 0 rgba(0,0,0,0.25),
        0 2px 8px rgba(20, 184, 166, 0.3),
        inset 0 2px 4px rgba(0,0,0,0.2);
    }
    .btn-primary:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    .status {
      margin-top: var(--space-2);
      min-height: 1.375rem;
      font-size: 0.875rem;
      color: var(--text-muted);
    }
    .status--error { color: var(--error); }
    .status--success { color: var(--success); }

    .location-result {
      margin-top: var(--space-3);
      padding: var(--space-4);
      border-radius: var(--radius-md);
      background: var(--accent-muted);
      border: 1px solid rgba(20, 184, 166, 0.25);
      font-size: var(--text-base);
      box-shadow: var(--shadow-3d-sm), inset 0 1px 0 rgba(255,255,255,0.08);
    }
    .location-result a {
      color: var(--accent-strong);
      text-decoration: none;
      word-break: break-all;
    }
    .location-result a:hover { text-decoration: underline; }
    .copy-btn {
      margin-top: var(--space-3);
      padding: var(--space-2) var(--space-3);
      border-radius: var(--radius-sm);
      border: 1px solid var(--border);
      border-bottom: 2px solid rgba(0,0,0,0.2);
      background: var(--bg-elevated);
      color: var(--text);
      font-size: var(--text-sm);
      cursor: pointer;
      font-family: inherit;
      box-shadow: 0 2px 6px rgba(0,0,0,0.25);
      transition: border-color var(--duration) var(--ease),
                  background-color var(--duration) var(--ease),
                  transform var(--duration) var(--ease),
                  box-shadow var(--duration) var(--ease);
    }
    .copy-btn:hover {
      border-color: var(--accent);
      background: var(--bg-card);
      transform: translateY(-1px);
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
    }
    .copy-btn:active {
      transform: translateY(0);
      box-shadow: 0 1px 3px rgba(0,0,0,0.25);
    }

    /* ===== Sudoku – 3D raised grid (fits fully in view) ===== */
    .sudoku-grid {
      display: grid;
      grid-template-columns: repeat(9, 1fr);
      grid-template-rows: repeat(9, minmax(0, 1fr));
      gap: 0;
      margin-top: var(--space-3);
      width: 100%;
      max-width: min(420px, 100%);
      aspect-ratio: 1;
      background: #fff;
      border: 2px solid var(--text);
      border-radius: var(--radius-sm);
      overflow: hidden;
      box-shadow: 0 6px 0 rgba(0,0,0,0.08), 0 8px 24px rgba(0,0,0,0.15);
    }
    .sudoku-cell {
      aspect-ratio: 1;
      min-width: 0;
      min-height: 0;
      text-align: center;
      font-size: clamp(0.65rem, 2.2vw, 0.875rem);
      background: #fff;
      border: 1px solid #cbd5e1;
      color: #0c0f14;
      border-radius: 0;
      font-family: inherit;
    }
    .sudoku-cell:focus {
      outline: 2px solid var(--accent);
      outline-offset: -2px;
      background: #ecfdfa;
    }
    .sudoku-cell[disabled] {
      background: #f1f5f9;
      font-weight: 700;
      color: #0c0f14;
    }
    .sudoku-grid .bold-bottom { border-bottom-width: 3px; }
    .sudoku-grid .bold-right { border-right-width: 3px; }

    /* ===== Footer ===== */
    .footer {
      margin-top: var(--space-6);
      font-size: 0.75rem;
      color: var(--text-muted);
      text-align: center;
      line-height: var(--leading-normal);
    }

    /* Utility: screen reader only */
    .visually-hidden {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border: 0;
    }

    /* ===== Responsive ===== */
    @media (max-width: 480px) {
      .hero { padding: 2.5rem var(--space-4) 2.5rem; }
      .app {
        padding: var(--space-5) var(--space-3) var(--space-4);
        transform: none;
      }
      .app:hover { transform: none; }
      .nav { flex-direction: column; }
      .nav-btn { border-bottom: none; border-left: 3px solid transparent; }
      .nav-btn--active { border-left-color: var(--accent); border-bottom: none; }
      .options { grid-template-columns: repeat(2, 1fr); }
      .app__header { flex-direction: column; align-items: flex-start; gap: var(--space-2); }
    }
  </style>
</head>
<body>
  <div class="app-shell">
    <section class="hero">
      <div class="hero-inner">
        <div class="hero-eyebrow">Play · Solve · Reveal</div>
        <h1 class="hero-title">
          Brainy Trio
          <span class="hero-title__highlight">Puzzle Experience</span>
        </h1>
        <p class="hero-subtitle">
          A mini game night in your browser. Sort liquids, crack Sudoku, match Bollywood legends — then reveal your final location name.
        </p>
        <div class="hero-cta-row">
          <button type="button" class="btn-primary" onclick="document.getElementById('game-colors').scrollIntoView({ behavior: 'smooth' });">
            Start Liquid Sort
          </button>
          <div class="hero-pill">
            <span class="hero-pill-dot" aria-hidden="true"></span>
            3 games · one final reveal
          </div>
        </div>
      </div>
    </section>

    <main class="app" role="main">
      <header class="header app__header">
        <div>
          <span class="badge">Brainy Trio</span>
          <h2 class="title app__title">Three mini games · One link</h2>
        </div>
      </header>
      <p class="subtitle">
        Select a game below. Games auto‑advance; complete all three to see your final location name.
      </p>

      <nav class="nav" role="tablist" aria-label="Games">
        <button type="button" class="nav-btn nav-btn--active" role="tab" aria-selected="true" data-game="colors" id="nav-colors">
          <span>Liquid Sort</span>
          <span>3 levels</span>
        </button>
        <button type="button" class="nav-btn" role="tab" aria-selected="false" data-game="sudoku" id="nav-sudoku" style="display:none;">
          <span>Sudoku</span>
          <span>1 calm grid</span>
        </button>
        <button type="button" class="nav-btn" role="tab" aria-selected="false" data-game="riddle" id="nav-riddle" style="display:none;">
          <span>Bollywood Match</span>
          <span>3 levels · tougher</span>
        </button>
      </nav>

      <section class="game-panel" id="game-colors">
      <h2>Game 1 · Liquid Sort (Water Sort)</h2>
      <p>
        Sort the liquids so each tube contains only one colour. Tap a tube to pick it, then tap another tube to pour.
      </p>
      <div class="level-badges">
        <span class="level-badge" id="water-level-indicator">Level 1 of 3</span>
      </div>
      <p class="game-panel__rule">
        Rule: you can pour only onto the same top colour (or an empty tube), and only if there is space.
      </p>
      <div id="water-tubes" class="water-tubes-wrap"></div>
      <div class="actions">
        <span id="water-status" class="status"></span>
        <button id="water-undo-btn" class="btn-primary">Undo</button>
        <button id="water-reset-btn" class="btn-primary">Reset level</button>
      </div>
      </section>

      <section class="game-panel" id="game-sudoku" style="display:none;">
      <h2>Game 2 · Mini Sudoku</h2>
      <p>
        Fill the grid so each row, column and 3×3 box contains digits 1–9. This is a single curated level.
      </p>
      <div id="sudoku-grid" class="sudoku-grid"></div>
      <div class="actions actions--sudoku">
        <span id="sudoku-status" class="status"></span>
        <button id="sudoku-check-btn" class="btn-primary">Check solution</button>
      </div>
      </section>

      <section class="game-panel" id="game-riddle" style="display:none;">
      <h2>Game 3 · Bollywood Movie Match</h2>
      <p>
        Match each recent movie to its lead actor. Clear all three levels to unlock your location name.
      </p>

      <div class="bolly-header">
        <div class="bolly-header__row">
          <span>Recent Bollywood</span>
          <span id="bolly-level-indicator" class="bolly-header__indicator">Level 1 of 3</span>
        </div>
        <p class="bolly-header__subtitle">
          Choose the correct lead actor for every movie in this level.
        </p>
      </div>

      <div id="bolly-rows" class="bolly-rows"></div>

      <div class="actions">
        <span id="riddle-status" class="status"></span>
        <button id="riddle-check-btn" class="btn-primary">Check matches</button>
      </div>

        <section id="location-section" class="location-section" style="display:none;">
          <p class="subtitle">
          Tap below to reveal the venue name and a link to open it in Google Maps.
        </p>
          <div class="actions">
            <button type="button" id="locate-btn" class="btn-primary">Reveal location</button>
            <span id="location-status" class="status"></span>
          </div>
          <div id="location-output" class="location-result" style="display:none;"></div>
        </section>
      </section>

      <div class="footer">
        After you complete all three games, you can reveal the venue and open it in Google Maps.
      </div>
    </main>
  </div>

  <script>
    (function () {
      // Navigation between 3 games
      const navButtons = Array.from(document.querySelectorAll(".nav-btn"));
      const navColors = document.getElementById("nav-colors");
      const navSudoku = document.getElementById("nav-sudoku");
      const navRiddle = document.getElementById("nav-riddle");

      let game1Complete = false;
      let game2Complete = false;
      let game3Complete = false;
      const panels = {
        colors: document.getElementById("game-colors"),
        sudoku: document.getElementById("game-sudoku"),
        riddle: document.getElementById("game-riddle"),
      };

      navButtons.forEach((btn) => {
        btn.addEventListener("click", () => {
          const game = btn.getAttribute("data-game");
          // Only allow access when previous games are complete
          if (game === "sudoku" && !game1Complete) return;
          if (game === "riddle" && !game2Complete) return;
          navButtons.forEach((b) => b.classList.remove("nav-btn--active"));
          btn.classList.add("nav-btn--active");
          Object.keys(panels).forEach((key) => {
            panels[key].style.display = key === game ? "block" : "none";
          });
        });
      });

      // Game 1: Liquid Sort (Water Sort) - 3 levels
      const waterTubesEl = document.getElementById("water-tubes");
      const waterStatusEl = document.getElementById("water-status");
      const waterResetBtn = document.getElementById("water-reset-btn");
      const waterUndoBtn = document.getElementById("water-undo-btn");
      const waterLevelIndicator = document.getElementById("water-level-indicator");

      const TUBE_CAPACITY = 4;
      const WATER_LEVELS = [
        // Level 1 (easy): 3 colours, 2 empty tubes
        [
          ["#ef4444", "#3b82f6", "#22c55e", "#ef4444"],
          ["#3b82f6", "#22c55e", "#ef4444", "#3b82f6"],
          ["#22c55e", "#ef4444", "#3b82f6", "#22c55e"],
          [],
          [],
        ],
        // Level 2 (medium): 4 colours, 2 empty tubes
        [
          ["#ef4444", "#3b82f6", "#22c55e", "#f97316"],
          ["#f97316", "#22c55e", "#3b82f6", "#ef4444"],
          ["#3b82f6", "#f97316", "#ef4444", "#22c55e"],
          ["#22c55e", "#ef4444", "#f97316", "#3b82f6"],
          [],
          [],
        ],
        // Level 3 (harder but solvable): 5 colours, 2 empty tubes
        [
          ["#ef4444", "#3b82f6", "#22c55e", "#f97316"],
          ["#a855f7", "#22c55e", "#3b82f6", "#ef4444"],
          ["#f97316", "#a855f7", "#ef4444", "#22c55e"],
          ["#3b82f6", "#f97316", "#a855f7", "#3b82f6"],
          ["#22c55e", "#ef4444", "#f97316", "#a855f7"],
          [],
          [],
        ],
      ];

      let waterLevelIndex = 0;
      let tubes = [];
      let selectedTubeIndex = null;
      let undoStack = [];

      function cloneTubes(src) {
        return src.map((t) => t.slice());
      }

      function loadWaterLevel(index) {
        waterLevelIndex = index;
        tubes = cloneTubes(WATER_LEVELS[index]);
        selectedTubeIndex = null;
        undoStack = [];
        waterLevelIndicator.textContent =
          "Level " + (waterLevelIndex + 1) + " of " + WATER_LEVELS.length;
        waterStatusEl.classList.remove("status--error", "status--success");
        waterStatusEl.textContent = "Solve the level by sorting colours.";
        renderTubes();
      }

      function topColor(tube) {
        return tube.length ? tube[tube.length - 1] : null;
      }

      function contiguousTopCount(tube) {
        if (!tube.length) return 0;
        const c = topColor(tube);
        let count = 0;
        for (let i = tube.length - 1; i >= 0; i--) {
          if (tube[i] !== c) break;
          count++;
        }
        return count;
      }

      function canPour(fromIdx, toIdx) {
        if (fromIdx === toIdx) return false;
        const from = tubes[fromIdx];
        const to = tubes[toIdx];
        if (!from.length) return false;
        if (to.length >= TUBE_CAPACITY) return false;
        const fromTop = topColor(from);
        const toTop = topColor(to);
        if (!toTop) return true;
        return toTop === fromTop;
      }

      function doPour(fromIdx, toIdx) {
        if (!canPour(fromIdx, toIdx)) return false;
        const from = tubes[fromIdx];
        const to = tubes[toIdx];
        const c = topColor(from);
        const movable = contiguousTopCount(from);
        const space = TUBE_CAPACITY - to.length;
        const amount = Math.min(movable, space);
        if (amount <= 0) return false;

        undoStack.push(cloneTubes(tubes));
        for (let i = 0; i < amount; i++) {
          to.push(from.pop());
        }
        return true;
      }

      function isSolved() {
        return tubes.every((t) => {
          if (t.length === 0) return true;
          if (t.length !== TUBE_CAPACITY) return false;
          return t.every((c) => c === t[0]);
        });
      }

      /** Short UI sounds (Web Audio – no files). */
      let waterAudioCtx = null;
      function playWaterSound(kind) {
        try {
          if (!waterAudioCtx) {
            waterAudioCtx = new (window.AudioContext || window.webkitAudioContext)();
          }
          if (waterAudioCtx.state === "suspended") {
            waterAudioCtx.resume();
          }
          const ctx = waterAudioCtx;
          const osc = ctx.createOscillator();
          const gain = ctx.createGain();
          osc.connect(gain);
          gain.connect(ctx.destination);
          var freq = 520;
          var dur = 0.06;
          if (kind === "select") {
            freq = 880;
            dur = 0.07;
          } else if (kind === "deselect") {
            freq = 380;
            dur = 0.06;
          } else if (kind === "pour") {
            freq = 640;
            dur = 0.08;
          } else if (kind === "error") {
            freq = 220;
            dur = 0.12;
          }
          osc.type = "sine";
          osc.frequency.setValueAtTime(freq, ctx.currentTime);
          gain.gain.setValueAtTime(0.12, ctx.currentTime);
          gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + dur);
          osc.start(ctx.currentTime);
          osc.stop(ctx.currentTime + dur);
        } catch (e) {}
      }

      function renderTubes() {
        waterTubesEl.innerHTML = "";
        tubes.forEach((tube, idx) => {
          const tubeEl = document.createElement("button");
          tubeEl.type = "button";
          tubeEl.className =
            "water-tube" +
            (idx === selectedTubeIndex ? " water-tube--selected" : "");
          tubeEl.setAttribute(
            "aria-pressed",
            idx === selectedTubeIndex ? "true" : "false"
          );
          tubeEl.style.width = "70px";
          tubeEl.style.height = "190px";
          tubeEl.style.padding = "10px 6px 12px";
          tubeEl.style.borderRadius = "18px";
          tubeEl.style.background =
            "rgba(15, 23, 42, 0.4)";
          // Inner glass area
          const inner = document.createElement("div");
          inner.style.flex = "1";
          inner.style.margin = "6px 4px 0 4px";
          inner.style.borderRadius = "14px";
          inner.style.border = "2px solid rgba(15, 23, 42, 0.9)";
          inner.style.background = "rgba(15,23,42,0.95)";
          inner.style.display = "flex";
          inner.style.flexDirection = "column";
          inner.style.justifyContent = "flex-end";
          inner.style.gap = "3px";

          for (let s = 0; s < TUBE_CAPACITY; s++) {
            const liquidIndex = tube.length - 1 - s;
            const color = liquidIndex >= 0 ? tube[liquidIndex] : null;
            const seg = document.createElement("div");
            seg.style.height = "28px";
            seg.style.borderRadius = "10px";
            // Clear, bright colours inside each tube segment (like the reference image)
            seg.style.background = color
              ? color
              : "rgba(15, 23, 42, 0.1)";
            seg.style.border = color
              ? "1px solid rgba(15, 23, 42, 0.9)"
              : "1px dashed rgba(148, 163, 184, 0.5)";
            seg.style.boxShadow = color
              ? "0 0 6px " + color
              : "inset 0 0 3px rgba(15, 23, 42, 0.9)";
            inner.appendChild(seg);
          }

          tubeEl.appendChild(inner);

          tubeEl.addEventListener("click", () => {
            waterStatusEl.classList.remove("status--error", "status--success");
            if (selectedTubeIndex === null) {
              if (!tubes[idx].length) {
                playWaterSound("error");
                waterStatusEl.classList.add("status--error");
                waterStatusEl.textContent = "Pick a non-empty tube first.";
                return;
              }
              selectedTubeIndex = idx;
              waterStatusEl.textContent = "Now tap a tube to pour into.";
              playWaterSound("select");
              renderTubes();
              return;
            }

            if (selectedTubeIndex === idx) {
              selectedTubeIndex = null;
              waterStatusEl.textContent = "Selection cleared.";
              playWaterSound("deselect");
              renderTubes();
              return;
            }

            const poured = doPour(selectedTubeIndex, idx);
            selectedTubeIndex = null;
            renderTubes();
            if (!poured) {
              playWaterSound("error");
              waterStatusEl.classList.add("status--error");
              waterStatusEl.textContent = "Invalid pour. Try another tube.";
              return;
            }
            playWaterSound("pour");

            if (isSolved()) {
              waterStatusEl.classList.add("status--success");
              if (waterLevelIndex === WATER_LEVELS.length - 1) {
                waterStatusEl.textContent =
                  "Level complete! You finished Liquid Sort. Sudoku is opening…";
                game1Complete = true;
                navSudoku.style.display = "flex";
                // Automatically switch to Sudoku game
                navSudoku.click();
              } else {
                waterStatusEl.textContent = "Level complete! Moving to next level...";
                setTimeout(() => loadWaterLevel(waterLevelIndex + 1), 900);
              }
            } else {
              waterStatusEl.textContent = "Good pour. Keep going!";
            }
          });

          waterTubesEl.appendChild(tubeEl);
        });
      }

      waterResetBtn.addEventListener("click", () => loadWaterLevel(waterLevelIndex));
      waterUndoBtn.addEventListener("click", () => {
        if (!undoStack.length) {
          waterStatusEl.classList.add("status--error");
          waterStatusEl.textContent = "Nothing to undo.";
          return;
        }
        tubes = undoStack.pop();
        selectedTubeIndex = null;
        waterStatusEl.classList.remove("status--error", "status--success");
        waterStatusEl.textContent = "Undid the last move.";
        renderTubes();
      });

      loadWaterLevel(0);

      // Game 2: Sudoku (one fixed puzzle)
      const sudokuGridEl = document.getElementById("sudoku-grid");
      const sudokuStatusEl = document.getElementById("sudoku-status");
      const sudokuCheckBtn = document.getElementById("sudoku-check-btn");

      // Beginner-friendly Sudoku: more clues, unique solution
      const sudokuPuzzle =
        "534678000" +
        "672000348" +
        "000342567" +
        "859701423" +
        "420853701" +
        "703924850" +
        "961507204" +
        "287419605" +
        "340286179";

      const sudokuSolution =
        "534678912" +
        "672195348" +
        "198342567" +
        "859761423" +
        "426853791" +
        "713924856" +
        "961537284" +
        "287419635" +
        "345286179";

      const sudokuInputs = [];

      function buildSudoku() {
        sudokuGridEl.innerHTML = "";
        for (let i = 0; i < 81; i++) {
          const cell = document.createElement("input");
          cell.type = "text";
          cell.inputMode = "numeric";
          cell.maxLength = 1;
          cell.className = "sudoku-cell";

          const row = Math.floor(i / 9);
          const col = i % 9;
          if (row === 2 || row === 5) {
            cell.classList.add("bold-bottom");
          }
          if (col === 2 || col === 5) {
            cell.classList.add("bold-right");
          }

          const value = sudokuPuzzle[i];
          if (value !== "0") {
            cell.value = value;
            cell.disabled = true;
          } else {
            cell.addEventListener("input", () => {
              const v = cell.value.replace(/[^1-9]/g, "");
              cell.value = v.slice(0, 1);
            });
          }

          sudokuGridEl.appendChild(cell);
          sudokuInputs.push(cell);
        }
      }

      sudokuCheckBtn.addEventListener("click", () => {
        sudokuStatusEl.classList.remove("status--error", "status--success");
        sudokuStatusEl.textContent = "";

        let allFilled = true;
        let correct = true;
        for (let i = 0; i < 81; i++) {
          const expected = sudokuSolution[i];
          const cell = sudokuInputs[i];
          const value = cell.value.trim();
          if (value === "") {
            allFilled = false;
          }
          if (value !== expected) {
            correct = false;
          }
        }

        if (!allFilled) {
          sudokuStatusEl.classList.add("status--error");
          sudokuStatusEl.textContent = "Fill every cell before checking.";
          return;
        }

        if (!correct) {
          sudokuStatusEl.classList.add("status--error");
          sudokuStatusEl.textContent = "Something is off. Adjust a few numbers and try again.";
          return;
        }

        sudokuStatusEl.classList.add("status--success");
        sudokuStatusEl.textContent =
          "Perfect Sudoku! You solved this level. Opening Bollywood Match…";
        game2Complete = true;
        sudokuCheckBtn.disabled = true;
        // Reveal Riddle in the navigation
        navRiddle.style.display = "flex";
        // Automatically switch to Bollywood Match game
        navRiddle.click();
      });

      buildSudoku();

      // Game 3: Bollywood match quest + Location name
      const riddleStatusEl = document.getElementById("riddle-status");
      const riddleCheckBtn = document.getElementById("riddle-check-btn");
      const locationSection = document.getElementById("location-section");
      const locateBtn = document.getElementById("locate-btn");
      const locationStatusEl = document.getElementById("location-status");
      const locationOutputEl = document.getElementById("location-output");
      const bollyRowsEl = document.getElementById("bolly-rows");
      const bollyLevelIndicator = document.getElementById("bolly-level-indicator");

      const BOLLYWOOD_LEVELS = [
        // Level 1 – mix of popular and slightly older
        {
          movies: [
            { title: "Sholay (1975)", correct: "amitabh" },
            { title: "Dilwale Dulhania Le Jayenge (1995)", correct: "srk" },
            { title: "Lagaan (2001)", correct: "aamir" },
            { title: "Jajantaram Mamataram(2003)", correct: "jaaved" },
          ],
          options: [
            { value: "amitabh", label: "Amitabh Bachchan" },
            { value: "dharmendra", label: "Dharmendra" },
            { value: "srk", label: "Shah Rukh Khan" },
            { value: "aamir", label: "Aamir Khan" },
            { value: "salman", label: "Salman Khan" },
            {value: "jaaved", label: "Jaaved Jaaferi"}          ],
        },
        // Level 2 – 90s / 2000s with overlapping stars
        {
          movies: [
            { title: "Andaz Apna Apna (1994)", correct: "aamir" },
            { title: "Kabhi Khushi Kabhie Gham (2001)", correct: "srk" },
            { title: "Hum Dil De Chuke Sanam (1999)", correct: "salman" },
            { title: "Barfi! (2012)", correct: "ranbir" },
          ],
          options: [
            { value: "aamir", label: "Aamir Khan" },
            { value: "srk", label: "Shah Rukh Khan" },
            { value: "salman", label: "Salman Khan" },
            { value: "hrithik", label: "Hrithik Roshan" },
            { value: "ranbir", label: "Ranbir Kapoor" },
          ],
        },
        // Level 3 – more recent + critically acclaimed, harder to guess
        {
          movies: [
            { title: "Mission Mangal (2019)", correct: "vidya" },
            { title: "Masaan (2015)", correct: "vicky" },
            { title: "Andhadhun (2018)", correct: "ayushmann" },
            { title: "Haider (2014)", correct: "shahid" },
          ],
          options: [
            { value: "vidya", label: "Vidya Balan" },
            { value: "vicky", label: "Vicky Kaushal" },
            { value: "ayushmann", label: "Ayushmann Khurrana" },
            { value: "rajkummar", label: "Rajkummar Rao" },
            { value: "shahid", label: "Shahid Kapoor" },
            { value: "akshay", label: "Akshay Kumar"}
          ],
        },
      ];

      let bollyLevelIndex = 0;

      function renderBollywoodLevel() {
        const level = BOLLYWOOD_LEVELS[bollyLevelIndex];
        if (!level) return;

        bollyLevelIndicator.textContent =
          "Level " + (bollyLevelIndex + 1) + " of " + BOLLYWOOD_LEVELS.length;
        riddleStatusEl.classList.remove("status--error", "status--success");
        riddleStatusEl.textContent = "";

        bollyRowsEl.innerHTML = "";
        const grid = document.createElement("div");
        grid.className = "bolly-grid";

        const headerMovie = document.createElement("div");
        headerMovie.className = "bolly-grid__head";
        headerMovie.textContent = "Movie";
        const headerActor = document.createElement("div");
        headerActor.className = "bolly-grid__head";
        headerActor.textContent = "Lead actor";
        grid.appendChild(headerMovie);
        grid.appendChild(headerActor);

        level.movies.forEach((movie) => {
          const movieDiv = document.createElement("div");
          movieDiv.className = "bolly-movie";
          movieDiv.textContent = movie.title;

          const wrap = document.createElement("div");
          wrap.className = "bolly-select-wrap";

          const select = document.createElement("select");
          select.className = "bolly-select";
          select.dataset.correct = movie.correct;
          select.setAttribute("aria-label", "Lead actor for " + movie.title);

          const placeholder = document.createElement("option");
          placeholder.value = "";
          placeholder.textContent = "Choose actor…";
          select.appendChild(placeholder);

          level.options.forEach((opt) => {
            const option = document.createElement("option");
            option.value = opt.value;
            option.textContent = opt.label;
            select.appendChild(option);
          });

          wrap.appendChild(select);
          grid.appendChild(movieDiv);
          grid.appendChild(wrap);
        });

        bollyRowsEl.appendChild(grid);
      }

      riddleCheckBtn.addEventListener("click", function () {
        riddleStatusEl.classList.remove("status--error", "status--success");
        riddleStatusEl.textContent = "";

        const selects = Array.from(
          document.querySelectorAll(".bolly-select")
        );

        if (!selects.length) {
          riddleStatusEl.classList.add("status--error");
          riddleStatusEl.textContent = "Something went wrong loading this level.";
          return;
        }

        for (const sel of selects) {
          if (!sel.value) {
            riddleStatusEl.classList.add("status--error");
            riddleStatusEl.textContent = "Choose an actor for every movie.";
            return;
          }
        }

        let allCorrect = true;
        for (const sel of selects) {
          if (sel.value !== sel.dataset.correct) {
            allCorrect = false;
            break;
          }
        }

        if (!allCorrect) {
          riddleStatusEl.classList.add("status--error");
          riddleStatusEl.textContent = "Not quite. Check the matches and try again!";
          return;
        }

        if (bollyLevelIndex < BOLLYWOOD_LEVELS.length - 1) {
          bollyLevelIndex += 1;
          riddleStatusEl.classList.add("status--success");
          riddleStatusEl.textContent = "Level cleared! Loading the next set of movies...";
          setTimeout(() => {
            renderBollywoodLevel();
          }, 800);
          return;
        }

        riddleStatusEl.classList.add("status--success");
        riddleStatusEl.textContent =
          "Amazing! You’ve completed all Bollywood levels. Now you can reveal your location name.";
        game3Complete = true;
        locationSection.style.display = "block";
      });

      function copyToClipboard(text) {
        if (navigator.clipboard && navigator.clipboard.writeText) {
          return navigator.clipboard.writeText(text);
        }
        const textarea = document.createElement("textarea");
        textarea.value = text;
        document.body.appendChild(textarea);
        textarea.select();
        try {
          document.execCommand("copy");
        } finally {
          document.body.removeChild(textarea);
        }
        return Promise.resolve();
      }

      locateBtn.addEventListener("click", function () {
        locationStatusEl.classList.remove("status--error", "status--success");
        locationStatusEl.textContent = "";
        locationOutputEl.style.display = "none";

        if (!game3Complete) {
          locationStatusEl.classList.add("status--error");
          locationStatusEl.textContent =
            "Finish all three games, including the riddle, before sharing your location.";
          return;
        }

        // Final reveal: clue (not the location itself).
        const revealTitle = "Final reveal clue:";
        const revealClue =
          "Pehle bilkul blank dikhta hoon,\n" +
          "Phir rang aate hi famous ho jaata hoon.\n" +
          "Painter ka favourite playground samajh lo mujhe.";
        const copyText = revealTitle + "\n" + revealClue;
        locationStatusEl.classList.add("status--success");
        locationStatusEl.textContent = "Clue revealed.";

        locationOutputEl.style.display = "block";
        locationOutputEl.innerHTML =
          "<div><strong>" +
          revealTitle +
          "</strong></div>" +
          "<pre style='margin-top:10px;white-space:pre-wrap;font-family:inherit;color:inherit;opacity:0.95;line-height:1.6;user-select:none;-webkit-user-select:none;-ms-user-select:none;'>" +
          revealClue +
          "</pre>";
      });

      // Initialise first Bollywood level
      renderBollywoodLevel();
    })();
  </script>
</body>
</html>



