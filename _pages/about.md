---
permalink: /about/
title: "About"
---

Charger got refunded! Yay!

<div class="stick-jump" role="img" aria-label="A silly stick figure repeatedly jumping for joy">
  <style>
    .stick-jump {
      max-width: 20rem;
      margin: 2rem auto;
      text-align: center;
    }

    .stick-jump__figure {
      transform-box: fill-box;
      transform-origin: center bottom;
      animation: stick-jump 1.1s ease-in-out infinite;
    }

    .stick-jump__shadow {
      transform-box: fill-box;
      transform-origin: center;
      animation: stick-shadow 1.1s ease-in-out infinite;
    }

    @keyframes stick-jump {
      0%, 100% { transform: translateY(0) rotate(-4deg); }
      50% { transform: translateY(-2.5rem) rotate(4deg); }
    }

    @keyframes stick-shadow {
      0%, 100% { transform: scaleX(1); opacity: 0.35; }
      50% { transform: scaleX(0.55); opacity: 0.12; }
    }

    @media (prefers-reduced-motion: reduce) {
      .stick-jump__figure,
      .stick-jump__shadow {
        animation: none;
      }
    }
  </style>

  <svg viewBox="0 0 220 220" width="220" height="220" aria-hidden="true">
    <line class="stick-jump__shadow" x1="55" y1="190" x2="165" y2="190"
      stroke="currentColor" stroke-width="12" stroke-linecap="round" />
    <g class="stick-jump__figure" fill="none" stroke="currentColor"
      stroke-width="7" stroke-linecap="round" stroke-linejoin="round">
      <circle cx="110" cy="54" r="25" fill="#ffd166" />
      <path d="M96 50h4M120 50h4M101 65q9 8 18 0" />
      <path d="M110 79v62M110 94L76 72M110 94l34-22M110 141l-28 37M110 141l28 37" />
      <path d="M73 72l-12-13M147 72l12-13M82 178l-14 4M138 178l14 4" />
    </g>
    <text x="110" y="215" text-anchor="middle" font-size="13" fill="currentColor">
      boing!
    </text>
  </svg>
</div>
