<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Aphma</title>
  <meta name="description" content="Aphma — a modern text transformation platform for encoding, decoding, hashing, encrypting, formatting, and more." />
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    :root {
      --bg: #f7f8fc;
      --bg-2: #ffffff;
      --bg-3: #eef1f7;
      --ink: #181c28;
      --muted: #7a8294;
      --line: rgba(22, 28, 45, 0.08);
      --line-2: rgba(22, 28, 45, 0.05);
      --shadow-soft: 0 18px 50px rgba(20, 24, 36, 0.06);
      --shadow-card: 0 12px 34px rgba(20, 24, 36, 0.08);
      --shadow-card-2: 0 24px 70px rgba(20, 24, 36, 0.11);
      --shadow-inset: inset 0 1px 0 rgba(255,255,255,0.9);
      --radius-xl: 30px;
      --radius-lg: 24px;
      --radius-md: 18px;
      --radius-sm: 14px;
      --ease: cubic-bezier(0.22, 1, 0.36, 1);
      --ease-spring: cubic-bezier(0.16, 1, 0.3, 1);
      --ease-soft: cubic-bezier(0.33, 1, 0.68, 1);
    }

    * {
      box-sizing: border-box;
    }

    html {
      scroll-behavior: smooth;
    }

    body {
      margin: 0;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background:
        radial-gradient(circle at 20% 10%, rgba(117, 133, 255, 0.08), transparent 24%),
        radial-gradient(circle at 80% 20%, rgba(160, 170, 255, 0.08), transparent 18%),
        radial-gradient(circle at 50% 100%, rgba(120, 140, 255, 0.07), transparent 20%),
        linear-gradient(180deg, #fbfcff 0%, #f5f7fc 42%, #f7f8fc 100%);
      color: var(--ink);
      overflow-x: hidden;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      pointer-events: none;
      background-image:
        linear-gradient(rgba(20, 24, 36, 0.018) 1px, transparent 1px),
        linear-gradient(90deg, rgba(20, 24, 36, 0.018) 1px, transparent 1px);
      background-size: 72px 72px;
      mask-image: linear-gradient(180deg, rgba(0,0,0,0.08), transparent 45%);
      opacity: 0.22;
    }

    ::selection {
      background: rgba(111, 121, 255, 0.18);
      color: var(--ink);
    }

    .page-shell {
      position: relative;
      width: min(1480px, calc(100% - 32px));
      margin: 0 auto;
      padding: 14px 0 36px;
    }

    .glass {
      background: rgba(255,255,255,0.76);
      backdrop-filter: blur(18px);
      border: 1px solid rgba(255,255,255,0.7);
      box-shadow: var(--shadow-soft);
    }

    .nav {
      position: sticky;
      top: 12px;
      z-index: 40;
      border-radius: 999px;
      padding: 14px 18px;
    }

    .brand-mark {
      width: 14px;
      height: 14px;
      border-radius: 999px;
      background: linear-gradient(135deg, #d8dcff, #8a90ff 72%, #1d2030 100%);
      box-shadow: 0 6px 18px rgba(122, 130, 255, 0.28);
    }

    .nav-link {
      position: relative;
      color: #5e6679;
      transition: transform 280ms var(--ease), color 280ms var(--ease), opacity 280ms var(--ease);
      border-radius: 999px;
      padding: 10px 14px;
    }

    .nav-link:hover {
      color: var(--ink);
      transform: translateY(-1px);
    }

    .nav-link.active {
      color: var(--ink);
      background: rgba(255,255,255,0.9);
      box-shadow: 0 8px 24px rgba(20, 24, 36, 0.06);
    }

    .btn {
      position: relative;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      border-radius: 999px;
      padding: 14px 22px;
      font-weight: 600;
      letter-spacing: -0.02em;
      transition:
        transform 380ms var(--ease-spring),
        box-shadow 380ms var(--ease-spring),
        background 380ms var(--ease-spring),
        border-color 380ms var(--ease-spring),
        color 380ms var(--ease-spring),
        filter 380ms var(--ease-spring);
      will-change: transform;
      user-select: none;
      overflow: hidden;
    }

    .btn::after {
      content: "";
      position: absolute;
      inset: -2px;
      background: radial-gradient(circle at var(--mx, 50%) var(--my, 50%), rgba(255,255,255,0.35), transparent 36%);
      opacity: 0;
      transition: opacity 420ms var(--ease);
      pointer-events: none;
    }

    .btn:hover::after {
      opacity: 1;
    }

    .btn:hover {
      transform: translateY(-2px) scale(1.01);
      filter: saturate(1.02);
    }

    .btn-primary {
      color: #fff;
      background: linear-gradient(180deg, #171c2b 0%, #0f1422 100%);
      box-shadow:
        0 14px 28px rgba(12, 15, 25, 0.16),
        inset 0 1px 0 rgba(255,255,255,0.08);
    }

    .btn-primary:hover {
      box-shadow:
        0 18px 38px rgba(12, 15, 25, 0.22),
        inset 0 1px 0 rgba(255,255,255,0.08);
    }

    .btn-secondary {
      color: var(--ink);
      background: rgba(255,255,255,0.88);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 10px 24px rgba(20,24,36,0.06);
    }

    .section {
      margin-top: 28px;
      border-radius: 36px;
      position: relative;
      overflow: hidden;
    }

    .section-card {
      background: rgba(255,255,255,0.72);
      backdrop-filter: blur(22px);
      border: 1px solid rgba(255,255,255,0.82);
      box-shadow: 0 30px 90px rgba(12, 18, 32, 0.07);
    }

    .hero {
      padding: 42px 22px 28px;
    }

    .hero-grid {
      display: grid;
      grid-template-columns: 1.02fr 0.98fr;
      gap: 26px;
      align-items: center;
      min-height: 680px;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 12px;
      border-radius: 999px;
      background: rgba(255,255,255,0.72);
      border: 1px solid rgba(20,24,36,0.05);
      color: #7d86a5;
      font-size: 13px;
      letter-spacing: 0.01em;
      box-shadow: 0 10px 20px rgba(20,24,36,0.04);
    }

    .eyebrow-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: linear-gradient(180deg, #a8b0ff, #6f78ff);
      box-shadow: 0 0 0 5px rgba(111, 120, 255, 0.11);
    }

    .hero-title {
      font-size: clamp(58px, 6.2vw, 104px);
      line-height: 0.98;
      letter-spacing: -0.07em;
      font-weight: 800;
      margin: 18px 0 18px;
      color: #151a28;
    }

    .hero-title .soft {
      color: #aab0ff;
    }

    .hero-copy {
      color: #788094;
      font-size: 18px;
      line-height: 1.65;
      max-width: 560px;
    }

    .hero-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
      margin-top: 28px;
    }

    .metrics {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 12px;
      margin-top: 34px;
      max-width: 540px;
    }

    .metric {
      padding: 16px 18px;
      border-radius: 22px;
      background: rgba(255,255,255,0.78);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 10px 25px rgba(20,24,36,0.05);
      text-align: left;
    }

    .metric strong {
      display: block;
      font-size: 16px;
      letter-spacing: -0.03em;
      color: #151a28;
      margin-bottom: 4px;
    }

    .metric span {
      display: block;
      font-size: 12px;
      color: #8d95a9;
    }

    .example-wrap {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 650px;
    }

    .hero-orbit {
      position: absolute;
      inset: 14px;
      border-radius: 42px;
      background:
        radial-gradient(circle at 72% 22%, rgba(154, 161, 255, 0.16), transparent 15%),
        radial-gradient(circle at 30% 82%, rgba(154, 161, 255, 0.12), transparent 16%);
      overflow: hidden;
      pointer-events: none;
    }

    .hero-orbit::before,
    .hero-orbit::after {
      content: "";
      position: absolute;
      border: 1.5px solid rgba(130, 138, 255, 0.22);
      border-radius: 50%;
      animation: driftOrbit 18s var(--ease-soft) infinite alternate;
    }

    .hero-orbit::before {
      width: 66%;
      height: 66%;
      right: -3%;
      top: 7%;
      transform: rotate(16deg);
    }

    .hero-orbit::after {
      width: 48%;
      height: 48%;
      left: -7%;
      bottom: -3%;
      transform: rotate(-12deg);
      animation-duration: 20s;
    }

    @keyframes driftOrbit {
      0% {
        transform: translate3d(0, 0, 0) rotate(0deg) scale(1);
      }
      50% {
        transform: translate3d(8px, -8px, 0) rotate(7deg) scale(1.02);
      }
      100% {
        transform: translate3d(-4px, 6px, 0) rotate(-6deg) scale(0.99);
      }
    }

    .panel {
      position: relative;
      width: min(100%, 560px);
      padding: 18px;
      border-radius: 36px;
      background: rgba(255,255,255,0.78);
      backdrop-filter: blur(18px);
      border: 1px solid rgba(255,255,255,0.8);
      box-shadow:
        0 28px 65px rgba(20,24,36,0.08),
        0 12px 24px rgba(20,24,36,0.04);
      transform-style: preserve-3d;
    }

    .panel::before {
      content: "";
      position: absolute;
      inset: 0;
      border-radius: 36px;
      background: linear-gradient(180deg, rgba(255,255,255,0.35), transparent 45%);
      pointer-events: none;
    }

    .panel-inner {
      position: relative;
      border-radius: 28px;
      padding: 20px;
      background: linear-gradient(180deg, rgba(255,255,255,0.9), rgba(250,251,255,0.8));
      border: 1px solid rgba(20,24,36,0.04);
      box-shadow: inset 0 1px 0 rgba(255,255,255,0.85);
    }

    .panel-label {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      color: #6f78ff;
      font-size: 13px;
      font-weight: 600;
      margin-bottom: 14px;
    }

    .panel-label .dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: #8d94ff;
      box-shadow: 0 0 0 6px rgba(141, 148, 255, 0.14);
    }

    .field {
      margin-bottom: 16px;
    }

    .field label {
      display: block;
      font-size: 12px;
      color: #7f8797;
      margin-bottom: 8px;
      font-weight: 600;
    }

    .select,
    .textarea,
    .output,
    .searchbar {
      width: 100%;
      border: 1px solid rgba(20,24,36,0.07);
      border-radius: 18px;
      background: rgba(255,255,255,0.9);
      box-shadow: 0 10px 22px rgba(20,24,36,0.04);
      outline: none;
      transition: border-color 280ms var(--ease), box-shadow 280ms var(--ease), transform 280ms var(--ease);
    }

    .select:focus,
    .textarea:focus,
    .searchbar:focus {
      border-color: rgba(124, 134, 255, 0.35);
      box-shadow: 0 14px 30px rgba(124, 134, 255, 0.12);
    }

    .select {
      appearance: none;
      padding: 14px 46px 14px 16px;
      font-size: 14px;
      color: #252a38;
      background-image:
        linear-gradient(45deg, transparent 50%, #838aa0 50%),
        linear-gradient(135deg, #838aa0 50%, transparent 50%),
        linear-gradient(to right, transparent, transparent);
      background-position:
        calc(100% - 20px) calc(50% - 3px),
        calc(100% - 14px) calc(50% - 3px),
        calc(100% - 2.75rem) 50%;
      background-size: 6px 6px, 6px 6px, 1px 1.5rem;
      background-repeat: no-repeat;
    }

    .textarea {
      min-height: 96px;
      resize: vertical;
      padding: 14px 16px;
      color: #252a38;
      font-size: 14px;
      line-height: 1.6;
    }

    .output {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 14px;
      padding: 13px 14px 13px 16px;
    }

    .output code {
      display: block;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
      font-size: 12px;
      color: #46506a;
      max-width: 72%;
    }

    .icon-chip {
      width: 30px;
      height: 30px;
      border-radius: 999px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      border: 1px solid rgba(20,24,36,0.06);
      background: rgba(255,255,255,0.92);
      color: #6a7286;
      box-shadow: 0 6px 16px rgba(20,24,36,0.06);
    }

    .icon-chip svg {
      width: 14px;
      height: 14px;
    }

    .run-btn {
      width: 100%;
      margin-top: 6px;
      padding: 14px 18px;
      border: 0;
      border-radius: 18px;
      background: linear-gradient(180deg, #fff, #f4f6fb);
      color: #171c2b;
      font-weight: 700;
      box-shadow: 0 12px 24px rgba(20,24,36,0.08);
      transition: transform 300ms var(--ease-spring), box-shadow 300ms var(--ease-spring);
    }

    .run-btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 18px 30px rgba(20,24,36,0.1);
    }

    .floating-action {
      position: absolute;
      right: -10px;
      top: 50%;
      transform: translateY(-50%);
      width: 56px;
      height: 56px;
      border-radius: 999px;
      display: grid;
      place-items: center;
      background: rgba(255,255,255,0.84);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 14px 34px rgba(20,24,36,0.12);
      color: #8f96ff;
      animation: floatPulse 5.6s var(--ease-soft) infinite;
    }

    @keyframes floatPulse {
      0%, 100% { transform: translateY(-50%) translateX(0) scale(1); }
      50% { transform: translateY(calc(-50% - 8px)) translateX(-2px) scale(1.04); }
    }

    .section-heading {
      text-align: center;
      margin-bottom: 26px;
    }

    .section-heading h2 {
      font-size: clamp(28px, 3vw, 48px);
      line-height: 1.05;
      letter-spacing: -0.05em;
      color: #171c2b;
      margin: 0;
    }

    .section-heading p {
      color: #7d8597;
      margin: 10px auto 0;
      max-width: 620px;
      font-size: 15px;
      line-height: 1.7;
    }

    .category-row {
      display: grid;
      grid-template-columns: 1fr auto;
      align-items: center;
      margin-bottom: 18px;
      gap: 16px;
    }

    .section-title {
      font-size: 15px;
      font-weight: 700;
      color: #141928;
      letter-spacing: -0.02em;
    }

    .mini-btn {
      padding: 12px 16px;
      font-size: 13px;
      font-weight: 700;
    }

    .carousel {
      position: relative;
      padding: 12px 0 8px;
    }

    .carousel-track {
      display: grid;
      grid-auto-flow: column;
      grid-auto-columns: minmax(138px, 1fr);
      gap: 14px;
      overflow-x: auto;
      scrollbar-width: none;
      scroll-snap-type: x mandatory;
      padding-bottom: 10px;
    }

    .carousel-track::-webkit-scrollbar {
      display: none;
    }

    .cat-card {
      scroll-snap-align: start;
      min-height: 148px;
      border-radius: 22px;
      padding: 18px 18px 16px;
      background: rgba(255,255,255,0.84);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 14px 32px rgba(20,24,36,0.06);
      transition: transform 360ms var(--ease-spring), box-shadow 360ms var(--ease-spring);
      position: relative;
      overflow: hidden;
    }

    .cat-card::before {
      content: "";
      position: absolute;
      inset: auto auto -48px -40px;
      width: 120px;
      height: 120px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(146, 153, 255, 0.18), transparent 68%);
      transition: transform 420ms var(--ease-spring);
    }

    .cat-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 20px 44px rgba(20,24,36,0.1);
    }

    .cat-card:hover::before {
      transform: scale(1.12);
    }

    .cat-ico {
      width: 44px;
      height: 44px;
      border-radius: 16px;
      display: grid;
      place-items: center;
      background: linear-gradient(180deg, rgba(141,148,255,0.12), rgba(141,148,255,0.05));
      color: #7a82ff;
      box-shadow: inset 0 1px 0 rgba(255,255,255,0.9);
      margin-bottom: 18px;
    }

    .cat-ico svg {
      width: 18px;
      height: 18px;
    }

    .cat-name {
      font-size: 14px;
      font-weight: 700;
      color: #171c2b;
      margin-bottom: 4px;
    }

    .cat-count {
      color: #80889b;
      font-size: 12px;
    }

    .tools-wrap {
      border-radius: 38px;
      padding: 28px;
      overflow: hidden;
      position: relative;
    }

    .tools-wrap::before,
    .tools-wrap::after {
      content: "";
      position: absolute;
      border-radius: 999px;
      filter: blur(2px);
      pointer-events: none;
      opacity: 0.8;
    }

    .tools-wrap::before {
      width: 320px;
      height: 320px;
      right: -120px;
      top: 36px;
      background: radial-gradient(circle, rgba(159,166,255,0.18), transparent 62%);
      animation: driftBlob 16s var(--ease-soft) infinite alternate;
    }

    .tools-wrap::after {
      width: 260px;
      height: 260px;
      left: -120px;
      bottom: 40px;
      background: radial-gradient(circle, rgba(159,166,255,0.13), transparent 68%);
      animation: driftBlob 18s var(--ease-soft) infinite alternate-reverse;
    }

    @keyframes driftBlob {
      0% { transform: translate3d(0, 0, 0) scale(1); }
      50% { transform: translate3d(14px, -10px, 0) scale(1.06); }
      100% { transform: translate3d(-8px, 10px, 0) scale(0.98); }
    }

    .tool-search {
      margin: 22px auto 16px;
      width: min(100%, 720px);
      position: relative;
    }

    .searchbar {
      padding: 16px 20px 16px 50px;
      font-size: 14px;
      color: #252a38;
      background-image: none;
    }

    .search-ico {
      position: absolute;
      left: 18px;
      top: 50%;
      transform: translateY(-50%);
      color: #8f96aa;
      width: 18px;
      height: 18px;
      pointer-events: none;
    }

    .search-slash {
      position: absolute;
      right: 16px;
      top: 50%;
      transform: translateY(-50%);
      color: #9ba2b5;
      font-size: 12px;
      font-weight: 700;
      padding: 2px 8px;
      border-radius: 8px;
      background: rgba(244,246,251,0.9);
      border: 1px solid rgba(20,24,36,0.05);
    }

    .chip-row {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin: 18px 0 18px;
      justify-content: center;
    }

    .chip {
      border: 1px solid rgba(20,24,36,0.05);
      background: rgba(255,255,255,0.82);
      color: #707889;
      border-radius: 999px;
      padding: 10px 16px;
      font-size: 13px;
      font-weight: 600;
      transition: transform 280ms var(--ease), background 280ms var(--ease), color 280ms var(--ease), box-shadow 280ms var(--ease);
      box-shadow: 0 8px 20px rgba(20,24,36,0.04);
    }

    .chip:hover {
      transform: translateY(-1px);
      color: #171c2b;
      box-shadow: 0 14px 24px rgba(20,24,36,0.07);
    }

    .chip.active {
      background: linear-gradient(180deg, #171c2b 0%, #0f1422 100%);
      color: #fff;
      box-shadow: 0 14px 28px rgba(12, 15, 25, 0.16);
    }

    .tool-list {
      display: grid;
      gap: 10px;
      margin-top: 14px;
    }

    .tool-item {
      display: grid;
      grid-template-columns: 42px minmax(0, 1fr) auto auto;
      align-items: center;
      gap: 14px;
      padding: 14px 18px;
      background: rgba(255,255,255,0.84);
      border: 1px solid rgba(20,24,36,0.05);
      border-radius: 20px;
      box-shadow: 0 12px 28px rgba(20,24,36,0.04);
      transition: transform 320ms var(--ease-spring), box-shadow 320ms var(--ease-spring), border-color 320ms var(--ease-spring);
    }

    .tool-item:hover {
      transform: translateY(-2px);
      box-shadow: 0 18px 36px rgba(20,24,36,0.07);
      border-color: rgba(124, 134, 255, 0.16);
    }

    .tool-item strong {
      display: block;
      font-size: 14px;
      color: #171c2b;
      margin-bottom: 3px;
    }

    .tool-item p {
      margin: 0;
      color: #8590a4;
      font-size: 12px;
      line-height: 1.5;
    }

    .tool-badge {
      justify-self: end;
      padding: 8px 12px;
      border-radius: 999px;
      background: rgba(243,245,251,0.9);
      color: #7580a0;
      font-size: 12px;
      font-weight: 700;
      border: 1px solid rgba(20,24,36,0.04);
      white-space: nowrap;
    }

    .tool-action {
      color: #71798c;
      font-size: 13px;
      font-weight: 700;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      white-space: nowrap;
      padding-left: 6px;
    }

    .tool-action svg {
      width: 14px;
      height: 14px;
    }

    .section-grid-4 {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 16px;
    }

    .audience-card {
      min-height: 180px;
      border-radius: 24px;
      padding: 22px;
      background: rgba(255,255,255,0.84);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 16px 34px rgba(20,24,36,0.05);
      transition: transform 360ms var(--ease-spring), box-shadow 360ms var(--ease-spring);
    }

    .audience-card:hover {
      transform: translateY(-6px);
      box-shadow: 0 22px 44px rgba(20,24,36,0.09);
    }

    .audience-icon {
      width: 44px;
      height: 44px;
      border-radius: 16px;
      display: grid;
      place-items: center;
      background: linear-gradient(180deg, rgba(141,148,255,0.12), rgba(141,148,255,0.04));
      color: #7a82ff;
      margin-bottom: 18px;
    }

    .audience-icon svg {
      width: 18px;
      height: 18px;
    }

    .audience-card h3 {
      font-size: 18px;
      margin: 0 0 8px;
      letter-spacing: -0.03em;
      color: #151a28;
    }

    .audience-card p {
      margin: 0;
      color: #7e869a;
      line-height: 1.65;
      font-size: 14px;
    }

    .stats-grid {
      display: grid;
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 0;
      border-radius: 28px;
      overflow: hidden;
      background: rgba(255,255,255,0.74);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 18px 44px rgba(20,24,36,0.05);
    }

    .stat {
      padding: 32px 20px;
      text-align: center;
      position: relative;
    }

    .stat:not(:last-child)::after {
      content: "";
      position: absolute;
      right: 0;
      top: 18%;
      bottom: 18%;
      width: 1px;
      background: rgba(20,24,36,0.06);
    }

    .stat strong {
      display: block;
      font-size: clamp(32px, 3vw, 50px);
      letter-spacing: -0.06em;
      line-height: 1;
      color: #141928;
      margin-bottom: 8px;
    }

    .stat span {
      display: block;
      color: #8a91a3;
      font-size: 13px;
      line-height: 1.55;
    }

    .cta-grid {
      display: grid;
      grid-template-columns: 1.05fr 0.95fr;
      gap: 24px;
      align-items: center;
    }

    .cta-copy {
      padding: 18px 6px 18px 0;
    }

    .cta-title {
      font-size: clamp(34px, 3.8vw, 58px);
      line-height: 1.02;
      letter-spacing: -0.06em;
      margin: 0 0 16px;
      color: #151a28;
    }

    .cta-title .soft {
      color: #9ba1ff;
    }

    .cta-copy p {
      color: #7f8797;
      font-size: 16px;
      line-height: 1.75;
      margin: 0 0 22px;
      max-width: 560px;
    }

    .mock-stack {
      position: relative;
      min-height: 340px;
    }

    .mock-card {
      position: absolute;
      top: 36px;
      left: 22px;
      width: min(360px, 84%);
      border-radius: 28px;
      padding: 20px;
      background: rgba(255,255,255,0.86);
      border: 1px solid rgba(20,24,36,0.05);
      box-shadow: 0 24px 55px rgba(20,24,36,0.08);
      transform: rotate(-2deg);
    }

    .mock-card.alt {
      top: 70px;
      right: 12px;
      left: auto;
      width: min(320px, 78%);
      transform: rotate(5deg);
    }

    .mock-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 14px;
      color: #798096;
      font-size: 13px;
      font-weight: 700;
    }

    .mock-head .status {
      display: inline-flex;
      align-items: center;
      gap: 8px;
    }

    .mock-head .status::before {
      content: "";
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: #8d94ff;
      box-shadow: 0 0 0 5px rgba(141,148,255,0.12);
    }

    .mock-list {
      display: grid;
      gap: 10px;
    }

    .mock-item {
      display: grid;
      grid-template-columns: 22px 1fr;
      gap: 10px;
      align-items: center;
      padding: 10px 12px;
      border-radius: 14px;
      background: rgba(246,247,251,0.9);
      color: #657085;
      font-size: 12px;
      border: 1px solid rgba(20,24,36,0.04);
    }

    .mock-dot {
      width: 20px;
      height: 20px;
      border-radius: 999px;
      background: linear-gradient(180deg, rgba(141,148,255,0.15), rgba(141,148,255,0.08));
      display: grid;
      place-items: center;
      color: #7f87ff;
      font-size: 11px;
    }

    .footer {
      padding: 28px 0 12px;
    }

    .footer-grid {
      display: grid;
      grid-template-columns: 1.6fr 1fr 1fr 1fr 1.35fr;
      gap: 18px;
      padding: 22px 6px 0;
    }

    .footer-title {
      color: #151a28;
      font-weight: 800;
      letter-spacing: -0.04em;
      font-size: 18px;
      margin-bottom: 10px;
    }

    .footer-copy {
      color: #7f8797;
      font-size: 14px;
      line-height: 1.75;
      max-width: 320px;
      margin-bottom: 18px;
    }

    .socials {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .social {
      width: 34px;
      height: 34px;
      border-radius: 999px;
      display: grid;
      place-items: center;
      background: rgba(255,255,255,0.82);
      border: 1px solid rgba(20,24,36,0.05);
      color: #7c8395;
      box-shadow: 0 8px 18px rgba(20,24,36,0.05);
      transition: transform 280ms var(--ease), box-shadow 280ms var(--ease), color 280ms var(--ease);
    }

    .social:hover {
      transform: translateY(-2px);
      box-shadow: 0 14px 28px rgba(20,24,36,0.08);
      color: #151a28;
    }

    .footer-link {
      display: block;
      color: #81889a;
      font-size: 14px;
      line-height: 1.9;
      transition: color 250ms var(--ease), transform 250ms var(--ease);
    }

    .footer-link:hover {
      color: #151a28;
      transform: translateX(2px);
    }

    .email-row {
      display: flex;
      gap: 10px;
      align-items: center;
      margin-top: 18px;
    }

    .email-input {
      flex: 1;
      padding: 14px 16px;
      border-radius: 999px;
      border: 1px solid rgba(20,24,36,0.05);
      background: rgba(255,255,255,0.86);
      color: #252a38;
      outline: none;
      box-shadow: 0 10px 22px rgba(20,24,36,0.04);
    }

    .footer-bottom {
      margin-top: 18px;
      padding-top: 14px;
      color: #9aa1b0;
      font-size: 13px;
    }

    .reveal {
      opacity: 0;
      transform: translateY(20px);
      filter: blur(6px);
      transition:
        opacity 900ms var(--ease-spring),
        transform 900ms var(--ease-spring),
        filter 900ms var(--ease-spring);
    }

    .reveal.in-view {
      opacity: 1;
      transform: translateY(0);
      filter: blur(0);
    }

    .stagger > * {
      opacity: 0;
      transform: translateY(18px);
      transition: opacity 720ms var(--ease-spring), transform 720ms var(--ease-spring);
    }

    .stagger.in-view > * {
      opacity: 1;
      transform: translateY(0);
    }

    .stagger.in-view > *:nth-child(1) { transition-delay: 60ms; }
    .stagger.in-view > *:nth-child(2) { transition-delay: 120ms; }
    .stagger.in-view > *:nth-child(3) { transition-delay: 180ms; }
    .stagger.in-view > *:nth-child(4) { transition-delay: 240ms; }
    .stagger.in-view > *:nth-child(5) { transition-delay: 300ms; }
    .stagger.in-view > *:nth-child(6) { transition-delay: 360ms; }
    .stagger.in-view > *:nth-child(7) { transition-delay: 420ms; }
    .stagger.in-view > *:nth-child(8) { transition-delay: 480ms; }

    .fade-up {
      animation: fadeUp 1100ms var(--ease-spring) both;
    }

    @keyframes fadeUp {
      from {
        opacity: 0;
        transform: translateY(24px);
        filter: blur(10px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
        filter: blur(0);
      }
    }

    .floaty {
      animation: floaty 9s var(--ease-soft) infinite;
    }

    .floaty-delay {
      animation: floaty 11s var(--ease-soft) infinite 1.2s;
    }

    .floaty-delay-2 {
      animation: floaty 10s var(--ease-soft) infinite 0.6s;
    }

    @keyframes floaty {
      0%, 100% { transform: translate3d(0, 0, 0); }
      50% { transform: translate3d(0, -10px, 0); }
    }

    .shine {
      position: relative;
      overflow: hidden;
    }

    .shine::before {
      content: "";
      position: absolute;
      top: -120%;
      left: -40%;
      width: 32%;
      height: 340%;
      background: linear-gradient(90deg, transparent, rgba(255,255,255,0.22), transparent);
      transform: rotate(24deg);
      animation: sheen 8.5s var(--ease-soft) infinite;
      pointer-events: none;
    }

    @keyframes sheen {
      0% { left: -52%; }
      45% { left: 120%; }
      100% { left: 120%; }
    }

    @media (max-width: 1200px) {
      .hero-grid,
      .cta-grid,
      .footer-grid {
        grid-template-columns: 1fr;
      }

      .example-wrap,
      .mock-stack {
        min-height: 520px;
      }

      .section-grid-4,
      .stats-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }

      .footer-grid > *:first-child {
        max-width: 760px;
      }
    }

    @media (max-width: 900px) {
      .page-shell {
        width: min(100% - 18px, 1480px);
      }

      .nav {
        border-radius: 28px;
      }

      .hero {
        padding: 28px 14px 20px;
      }

      .hero-title {
        font-size: clamp(44px, 9vw, 72px);
      }

      .hero-copy,
      .cta-copy p {
        font-size: 15px;
      }

      .metrics {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }

      .tool-item {
        grid-template-columns: 36px minmax(0, 1fr);
      }

      .tool-badge,
      .tool-action {
        grid-column: 2;
        justify-self: start;
      }

      .section-card {
        border-radius: 28px;
      }

      .tools-wrap {
        padding: 20px;
      }
    }

    @media (max-width: 640px) {
      .nav-left,
      .nav-center,
      .nav-right {
        width: 100%;
      }

      .nav {
        padding: 14px;
      }

      .hero-grid {
        min-height: auto;
      }

      .metrics,
      .section-grid-4,
      .stats-grid {
        grid-template-columns: 1fr;
      }

      .panel {
        padding: 12px;
        border-radius: 28px;
      }

      .panel-inner {
        padding: 16px;
      }

      .hero-actions,
      .email-row {
        flex-direction: column;
        align-items: stretch;
      }

      .btn,
      .email-input,
      .run-btn {
        width: 100%;
      }

      .cta-copy {
        padding-right: 0;
      }

      .mock-card,
      .mock-card.alt {
        width: 92%;
      }

      .mock-card.alt {
        top: 160px;
      }
    }
  </style>
</head>
<body>
  <div class="page-shell">
    <header class="nav glass">
      <div class="flex items-center justify-between gap-4 flex-wrap">
        <div class="nav-left flex items-center gap-3">
          <div class="brand-mark"></div>
          <div class="text-[18px] font-extrabold tracking-[-0.05em] text-[#151a28]">Aphma</div>
        </div>

        <nav class="nav-center hidden lg:flex items-center gap-1 text-[14px] font-medium">
          <a class="nav-link active" href="#home">Home</a>
          <a class="nav-link" href="#tools">Tools</a>
          <a class="nav-link" href="#editors">Editors</a>
          <a class="nav-link" href="#favorites">Favorites</a>
          <a class="nav-link" href="#history">History</a>
          <a class="nav-link" href="#api">API</a>
          <a class="nav-link" href="#pricing">Pricing</a>
          <a class="nav-link" href="#about">About</a>
        </nav>

        <div class="nav-right flex items-center gap-3 flex-wrap justify-end">
          <div class="hidden md:flex items-center gap-2 px-4 py-2 rounded-full bg-white/80 border border-black/5 shadow-[0_8px_20px_rgba(20,24,36,0.04)]">
            <svg class="w-4 h-4 text-[#8c93a6]" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="11" cy="11" r="7"></circle>
              <path d="M20 20l-3.5-3.5"></path>
            </svg>
            <span class="text-[13px] text-[#8a91a3]">Search tools...</span>
            <span class="text-[11px] font-bold text-[#9aa1b4] ml-1">⌘ K</span>
          </div>
          <a href="#signin" class="text-[14px] text-[#71798c] font-medium px-2 py-2">Sign in</a>
          <a href="#signup" class="btn btn-primary text-[14px] px-5 py-3">Sign up</a>
        </div>
      </div>
    </header>

    <main id="home">
      <section class="section section-card hero shine reveal">
        <div class="hero-grid">
          <div class="relative z-[2]">
            <div class="eyebrow fade-up" style="animation-delay: 60ms;">
              <span class="eyebrow-dot"></span>
              <span>1000+ tools and growing</span>
            </div>

            <h1 class="hero-title fade-up" style="animation-delay: 130ms;">
              Transform.<br />
              Encrypt. Encode.<br />
              All in <span class="soft">One</span> Place.
            </h1>

            <p class="hero-copy fade-up" style="animation-delay: 200ms;">
              Aphma is the ultimate toolkit for developers, researchers, and curious minds to convert, encode, decode, hash, encrypt, format, validate, inspect, and manipulate text in one beautifully unified interface.
            </p>

            <div class="hero-actions fade-up" style="animation-delay: 270ms;">
              <a href="#tools" class="btn btn-primary">Explore Tools
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M5 12h12"></path>
                  <path d="M13 6l6 6-6 6"></path>
                </svg>
              </a>
              <a href="#quick" class="btn btn-secondary">Try a Quick Encode</a>
            </div>

            <div class="metrics fade-up" style="animation-delay: 340ms;">
              <div class="metric floaty">
                <strong>1000+</strong>
                <span>Tools</span>
              </div>
              <div class="metric floaty-delay">
                <strong>50+</strong>
                <span>Categories</span>
              </div>
              <div class="metric floaty-delay-2">
                <strong>∞</strong>
                <span>Possibilities</span>
              </div>
              <div class="metric floaty">
                <strong>0</strong>
                <span>Limits</span>
              </div>
            </div>
          </div>

          <div class="example-wrap reveal" style="transition-delay: 160ms;">
            <div class="hero-orbit"></div>
            <div class="panel floaty" id="tiltPanel">
              <div class="panel-inner">
                <div class="panel-label"><span class="dot"></span> Live Example</div>

                <div class="field">
                  <label for="mode">Tool</label>
                  <select id="mode" class="select">
                    <option>Base64 Encode</option>
                    <option>Base64 Decode</option>
                    <option>URL Encode</option>
                    <option>URL Decode</option>
                    <option>MD5 Hash</option>
                    <option>SHA256 Hash</option>
                    <option>AES Encrypt</option>
                  </select>
                </div>

                <div class="field">
                  <label for="input">Input</label>
                  <textarea id="input" class="textarea">Hello, Aphma!</textarea>
                  <div class="mt-2 text-right text-[11px] text-[#95a0b3]">13 / 10,000</div>
                </div>

                <div class="field mb-2">
                  <label for="output">Output</label>
                  <div class="output">
                    <code id="output">SGVsbG8sIEFwaG1hIQ==</code>
                    <div class="flex items-center gap-2">
                      <button class="icon-chip" aria-label="Copy output">
                        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                          <rect x="9" y="9" width="10" height="10" rx="2"></rect>
                          <path d="M5 15V7a2 2 0 0 1 2-2h8"></path>
                        </svg>
                      </button>
                      <button class="icon-chip" aria-label="Clear output">
                        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                          <path d="M6 6l12 12"></path>
                          <path d="M18 6L6 18"></path>
                        </svg>
                      </button>
                      <button class="icon-chip" aria-label="Save output">
                        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                          <path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path>
                          <path d="M17 21v-8H7v8"></path>
                          <path d="M7 3v5h8"></path>
                        </svg>
                      </button>
                    </div>
                  </div>
                  <div class="mt-2 text-right text-[11px] text-[#95a0b3]">13 / 10,000</div>
                </div>

                <button class="run-btn">Run</button>
              </div>
            </div>

            <div class="floating-action">
              <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2">
                <path d="M13 2L4 14h7l-1 8 10-13h-7l0-7z"></path>
              </svg>
            </div>
          </div>
        </div>
      </section>

      <section class="section section-card p-6 md:p-8 mt-7 reveal" id="categories">
        <div class="category-row">
          <div class="section-title">Popular Categories</div>
          <a href="#allcategories" class="btn btn-secondary mini-btn">View all categories</a>
        </div>

        <div class="carousel">
          <div class="carousel-track stagger in-view">
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 12h16"></path><path d="M12 4v16"></path></svg></div>
              <div class="cat-name">Encoding</div>
              <div class="cat-count">320+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 12h16"></path><path d="M12 4l-8 8 8 8"></path></svg></div>
              <div class="cat-name">Decoding</div>
              <div class="cat-count">280+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 3l7 4v10l-7 4-7-4V7l7-4z"></path><path d="M12 12v9"></path></svg></div>
              <div class="cat-name">Hashing</div>
              <div class="cat-count">210+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="4" y="10" width="16" height="10" rx="2"></rect><path d="M8 10V7a4 4 0 0 1 8 0v3"></path></svg></div>
              <div class="cat-name">Encryption</div>
              <div class="cat-count">180+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 7h16"></path><path d="M4 12h16"></path><path d="M4 17h16"></path></svg></div>
              <div class="cat-name">Formatting</div>
              <div class="cat-count">120+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 12h16"></path><path d="M12 4v16"></path></svg></div>
              <div class="cat-name">Data</div>
              <div class="cat-count">100+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="8"></circle><path d="M2 12h4"></path><path d="M18 12h4"></path></svg></div>
              <div class="cat-name">Network</div>
              <div class="cat-count">80+ tools</div>
            </div>
            <div class="cat-card">
              <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 12h16"></path><path d="M12 4l4 4-4 4-4-4 4-4z"></path><path d="M12 12l4 4-4 4-4-4 4-4z"></path></svg></div>
              <div class="cat-name">More</div>
              <div class="cat-count">Expanding daily</div>
            </div>
          </div>
        </div>
      </section>

      <section class="section section-card p-6 md:p-8 mt-7 tools-wrap reveal" id="tools">
        <div class="section-heading">
          <h2>Powerful Tools. Infinite Possibilities.</h2>
          <p>Over 1000 tools to handle any text transformation you can imagine, presented in a clean system that feels fast, calm, and precise.</p>
        </div>

        <div class="tool-search">
          <svg class="search-ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="7"></circle>
            <path d="M20 20l-3.5-3.5"></path>
          </svg>
          <input class="searchbar" id="toolSearch" placeholder="Search any tool..." />
          <span class="search-slash">/</span>
        </div>

        <div class="chip-row" id="chips">
          <button class="chip active" data-filter="all">All</button>
          <button class="chip" data-filter="encoding">Encoding</button>
          <button class="chip" data-filter="decoding">Decoding</button>
          <button class="chip" data-filter="hashing">Hashing</button>
          <button class="chip" data-filter="encryption">Encryption</button>
          <button class="chip" data-filter="formatting">Formatting</button>
          <button class="chip" data-filter="data">Data</button>
          <button class="chip" data-filter="network">Network</button>
          <button class="chip" data-filter="filters">Filters</button>
        </div>

        <div class="tool-list" id="toolList">
          <article class="tool-item" data-category="encoding" data-name="Base64 Encode Encode text to Base64">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14"></path><path d="M12 5l7 7-7 7"></path></svg></div>
            <div>
              <strong>Base64 Encode</strong>
              <p>Encode text to Base64</p>
            </div>
            <div class="tool-badge">Encoding</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="decoding" data-name="Base64 Decode Decode Base64 to text">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 12H5"></path><path d="M12 19l-7-7 7-7"></path></svg></div>
            <div>
              <strong>Base64 Decode</strong>
              <p>Decode Base64 to text</p>
            </div>
            <div class="tool-badge">Decoding</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="hashing" data-name="MD5 Hash Generate MD5 hash">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="8"></circle><path d="M12 8v8"></path><path d="M8 12h8"></path></svg></div>
            <div>
              <strong>MD5 Hash</strong>
              <p>Generate MD5 hash</p>
            </div>
            <div class="tool-badge">Hashing</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="hashing" data-name="SHA256 Hash Generate SHA256 hash">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 3l8 4v10l-8 4-8-4V7l8-4z"></path><path d="M12 12l0 9"></path></svg></div>
            <div>
              <strong>SHA256 Hash</strong>
              <p>Generate SHA256 hash</p>
            </div>
            <div class="tool-badge">Hashing</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="encoding" data-name="URL Encode Encode URL special characters">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 14h6"></path><path d="M8 10l-4 4 4 4"></path><path d="M20 10h-6"></path><path d="M16 6l4 4-4 4"></path></svg></div>
            <div>
              <strong>URL Encode</strong>
              <p>Encode URL special characters</p>
            </div>
            <div class="tool-badge">Encoding</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="decoding" data-name="URL Decode Decode URL special characters">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 10h-6"></path><path d="M16 6l4 4-4 4"></path><path d="M4 14h6"></path><path d="M8 10l-4 4 4 4"></path></svg></div>
            <div>
              <strong>URL Decode</strong>
              <p>Decode URL special characters</p>
            </div>
            <div class="tool-badge">Decoding</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="encryption" data-name="AES Encrypt Encrypt text with AES algorithm">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="4" y="10" width="16" height="10" rx="2"></rect><path d="M8 10V7a4 4 0 0 1 8 0v3"></path></svg></div>
            <div>
              <strong>AES Encrypt</strong>
              <p>Encrypt text with AES algorithm</p>
            </div>
            <div class="tool-badge">Encryption</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>

          <article class="tool-item" data-category="formatting" data-name="JSON Format Format and validate JSON">
            <div class="cat-ico"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M8 4c-2 0-2 2-2 3v2c0 1-1 1-1 1s1 0 1 1v2c0 1 0 3 2 3"></path><path d="M16 4c2 0 2 2 2 3v2c0 1 1 1 1 1s-1 0-1 1v2c0 1 0 3-2 3"></path></svg></div>
            <div>
              <strong>JSON Format</strong>
              <p>Format and validate JSON</p>
            </div>
            <div class="tool-badge">Formatting</div>
            <div class="tool-action">Use Tool <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg></div>
          </article>
        </div>

        <div class="text-center mt-5">
          <a href="#alltools" class="btn btn-secondary mini-btn">View All Tools</a>
        </div>
      </section>

      <section class="section section-card p-6 md:p-8 mt-7 reveal" id="editors">
        <div class="mb-6">
          <h2 class="text-[30px] md:text-[40px] font-extrabold tracking-[-0.05em] text-[#151a28] mb-3">Built for Everyone</h2>
          <p class="max-w-[670px] text-[#7c8396] leading-[1.8]">Whether you are a developer, pentester, student, or just someone who loves tools, Aphma is built to feel simple, beautiful, and fast.</p>
        </div>

        <div class="section-grid-4 stagger in-view">
          <article class="audience-card">
            <div class="audience-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 12l16 0"></path><path d="M12 4l0 16"></path></svg></div>
            <h3>Developers</h3>
            <p>Speed up your workflow with powerful text manipulation tools, search, presets, and one-click helpers.</p>
          </article>

          <article class="audience-card">
            <div class="audience-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 8h16"></path><path d="M8 4v8"></path><path d="M12 12l4 4"></path><path d="M16 12l-4 4"></path></svg></div>
            <h3>Security Researchers</h3>
            <p>Encrypt, hash, decode, and inspect data with a calm interface designed for focused analysis.</p>
          </article>

          <article class="audience-card">
            <div class="audience-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M7 8h10"></path><path d="M7 12h10"></path><path d="M7 16h6"></path><path d="M6 4h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2z"></path></svg></div>
            <h3>Students</h3>
            <p>Learn and experiment with encoding, decoding, formatting, and data transformations in a playful space.</p>
          </article>

          <article class="audience-card">
            <div class="audience-icon"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14"></path><path d="M12 5l7 7-7 7"></path></svg></div>
            <h3>Everyone</h3>
            <p>Simple, beautiful, and easy to use. No learning curve required, just a tool for whatever text needs happen next.</p>
          </article>
        </div>
      </section>

      <section class="section section-card p-6 md:p-8 mt-7 reveal">
        <div class="stats-grid">
          <div class="stat">
            <strong>1000+</strong>
            <span>Tools<br />And counting</span>
          </div>
          <div class="stat">
            <strong>50+</strong>
            <span>Categories<br />Organized for you</span>
          </div>
          <div class="stat">
            <strong>1M+</strong>
            <span>Conversions<br />Every month</span>
          </div>
          <div class="stat">
            <strong>99.9%</strong>
            <span>Uptime<br />Always available</span>
          </div>
        </div>
      </section>

      <section class="section section-card p-6 md:p-8 mt-7 reveal" id="pricing">
        <div class="cta-grid">
          <div class="cta-copy">
            <h2 class="cta-title">Ready to Transform Text Like <span class="soft">Never Before?</span></h2>
            <p>Join thousands of users who trust Aphma for their daily text transformation needs. Fast interactions, soft surfaces, and smooth motion make every tool feel polished.</p>
            <div class="hero-actions">
              <a href="#signup" class="btn btn-primary">Get Started for Free</a>
              <a href="#tools" class="btn btn-secondary">Explore All Tools</a>
            </div>
          </div>

          <div class="mock-stack">
            <div class="mock-card floaty">
              <div class="mock-head">
                <span class="status">Recent</span>
                <span>▾</span>
              </div>
              <div class="mock-list">
                <div class="mock-item"><span class="mock-dot">A</span><span>Base64 Encode</span></div>
                <div class="mock-item"><span class="mock-dot">B</span><span>SHA256 Hash</span></div>
                <div class="mock-item"><span class="mock-dot">C</span><span>URL Decode</span></div>
                <div class="mock-item"><span class="mock-dot">D</span><span>JSON Format</span></div>
                <div class="mock-item"><span class="mock-dot">E</span><span>AES Encrypt</span></div>
              </div>
            </div>

            <div class="mock-card alt floaty-delay-2">
              <div class="mock-head">
                <span class="status">Categories</span>
                <span>▾</span>
              </div>
              <div class="mock-list">
                <div class="mock-item"><span class="mock-dot">1</span><span>Encoding</span></div>
                <div class="mock-item"><span class="mock-dot">2</span><span>Decoding</span></div>
                <div class="mock-item"><span class="mock-dot">3</span><span>Hashing</span></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <footer class="section footer reveal" id="about">
        <div class="footer-grid">
          <div>
            <div class="footer-title">Aphma</div>
            <div class="footer-copy">The ultimate toolkit for all your text transformation needs, presented with a calm white interface and soft depth.</div>
            <div class="socials">
              <a class="social" href="#" aria-label="Social 1">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 8h-4v12h4z"></path><path d="M9 12c0-2.2 1.8-4 4-4s4 1.8 4 4v8h4v-8c0-4.4-3.6-8-8-8s-8 3.6-8 8v8h4z"></path></svg>
              </a>
              <a class="social" href="#" aria-label="Social 2">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M23 3a10.9 10.9 0 0 1-3.14 1.53A4.48 4.48 0 0 0 16 3c-2.5 0-4.5 2-4.5 4.5V9A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5 0-.18 0-.35-.01-.53A7.72 7.72 0 0 0 23 3z"></path></svg>
              </a>
              <a class="social" href="#" aria-label="Social 3">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="2" width="20" height="20" rx="5"></rect><path d="M16 8a6 6 0 1 1-8 0"></path><circle cx="17" cy="7" r="1"></circle></svg>
              </a>
              <a class="social" href="#" aria-label="Social 4">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"></path></svg>
              </a>
            </div>
          </div>

          <div>
            <div class="footer-title">Product</div>
            <a class="footer-link" href="#tools">Tools</a>
            <a class="footer-link" href="#categories">Categories</a>
            <a class="footer-link" href="#api">API</a>
            <a class="footer-link" href="#pricing">Pricing</a>
          </div>

          <div>
            <div class="footer-title">Resources</div>
            <a class="footer-link" href="#">Documentation</a>
            <a class="footer-link" href="#">Guides</a>
            <a class="footer-link" href="#">Changelog</a>
            <a class="footer-link" href="#">Status</a>
          </div>

          <div>
            <div class="footer-title">Company</div>
            <a class="footer-link" href="#about">About</a>
            <a class="footer-link" href="#">Contact</a>
            <a class="footer-link" href="#">Privacy</a>
            <a class="footer-link" href="#">Terms</a>
          </div>

          <div>
            <div class="footer-title">Stay Updated</div>
            <div class="footer-copy">Get the latest updates and new tools delivered to your inbox.</div>
            <div class="email-row">
              <input class="email-input" placeholder="Enter your email" />
              <a class="btn btn-primary px-4 py-3" href="#subscribe" aria-label="Subscribe">
                <svg class="w-4 h-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h12"></path><path d="M13 6l6 6-6 6"></path></svg>
              </a>
            </div>
          </div>
        </div>

        <div class="footer-bottom text-center">© 2024 Aphma. All rights reserved.</div>
      </footer>
    </main>
  </div>

  <script>
    const revealEls = document.querySelectorAll('.reveal, .stagger');
    const io = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('in-view');
          if (entry.target.classList.contains('stagger')) {
            // Allow parent to remain visible once children animate in.
          }
        }
      });
    }, { threshold: 0.16 });
    revealEls.forEach((el) => io.observe(el));

    const chips = document.querySelectorAll('.chip');
    const tools = document.querySelectorAll('.tool-item');
    const toolSearch = document.getElementById('toolSearch');

    function applyFilter() {
      const active = document.querySelector('.chip.active')?.dataset.filter || 'all';
      const q = (toolSearch.value || '').toLowerCase().trim();

      tools.forEach((tool) => {
        const cat = tool.dataset.category;
        const hay = (tool.dataset.name || '').toLowerCase();
        const catOk = active === 'all' || cat === active;
        const searchOk = !q || hay.includes(q);
        tool.style.display = catOk && searchOk ? '' : 'none';
      });
    }

    chips.forEach((chip) => {
      chip.addEventListener('click', () => {
        chips.forEach((c) => c.classList.remove('active'));
        chip.classList.add('active');
        applyFilter();
      });
    });

    toolSearch.addEventListener('input', applyFilter);

    const modes = [
      'Base64 Encode',
      'Base64 Decode',
      'URL Encode',
      'URL Decode',
      'MD5 Hash',
      'SHA256 Hash',
      'AES Encrypt'
    ];

    const outputs = {
      'Base64 Encode': 'SGVsbG8sIEFwaG1hIQ==',
      'Base64 Decode': 'Hello, Aphma!',
      'URL Encode': 'Hello%2C%20Aphma!',
      'URL Decode': 'Hello, Aphma!',
      'MD5 Hash': '4b1c4e9d7c3d8f2f7c9f5c1f3b8d9a1a',
      'SHA256 Hash': '3f1f8f2d9d4f3a64a1c6a3c5a8b8c8d0e5f0fa6f8e0b2a7f1b4c0d9e3a1f6b7',
      'AES Encrypt': 'U2FsdGVkX1+5b0xwA4mR8f4z2Xq2fVgqN3n4Y2M=' 
    };

    const modeSelect = document.getElementById('mode');
    const input = document.getElementById('input');
    const output = document.getElementById('output');

    modeSelect.addEventListener('change', () => {
      output.textContent = outputs[modeSelect.value] || 'Output appears here';
      input.placeholder = `Type text for ${modeSelect.value.toLowerCase()}...`;
    });

    const panel = document.getElementById('tiltPanel');
    const clamp = (v, min, max) => Math.min(max, Math.max(min, v));

    let raf = null;
    function setTilt(x, y) {
      const rect = panel.getBoundingClientRect();
      const px = ((x - rect.left) / rect.width - 0.5) * 2;
      const py = ((y - rect.top) / rect.height - 0.5) * 2;
      const rotY = clamp(px * 4.4, -5, 5);
      const rotX = clamp(-py * 4.4, -5, 5);
      panel.style.transform = `perspective(1400px) rotateX(${rotX}deg) rotateY(${rotY}deg) translateY(-2px)`;
    }

    panel.addEventListener('pointermove', (e) => {
      if (raf) cancelAnimationFrame(raf);
      raf = requestAnimationFrame(() => setTilt(e.clientX, e.clientY));
    });

    panel.addEventListener('pointerleave', () => {
      panel.style.transform = 'perspective(1400px) rotateX(0deg) rotateY(0deg) translateY(0px)';
    });

    const buttons = document.querySelectorAll('.btn, .social, .icon-chip, .run-btn, .chip, .nav-link, .cat-card, .tool-item, .audience-card');
    buttons.forEach((btn) => {
      btn.addEventListener('pointermove', (e) => {
        const rect = btn.getBoundingClientRect();
        const mx = ((e.clientX - rect.left) / rect.width) * 100;
        const my = ((e.clientY - rect.top) / rect.height) * 100;
        btn.style.setProperty('--mx', `${mx}%`);
        btn.style.setProperty('--my', `${my}%`);
      });
    });

    const navLinks = document.querySelectorAll('.nav-link');
    navLinks.forEach((link) => {
      link.addEventListener('click', () => {
        navLinks.forEach((l) => l.classList.remove('active'));
        link.classList.add('active');
      });
    });

    const inputTexts = [
      'Hello, Aphma!',
      'The future of text tools.',
      'Encode, transform, and ship.',
      'Clean UI. Fast tools. Smooth motion.'
    ];

    let idx = 0;
    setInterval(() => {
      idx = (idx + 1) % inputTexts.length;
      if (document.activeElement !== input) {
        input.value = inputTexts[idx];
      }
    }, 5200);

    // Gentle page entrance tuning.
    window.addEventListener('load', () => {
      document.body.classList.add('loaded');
      applyFilter();
    });
  </script>
</body>
</html>
