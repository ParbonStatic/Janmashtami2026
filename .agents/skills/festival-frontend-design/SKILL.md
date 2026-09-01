---
name: festival-frontend-design
description: >-
  Architectural guidelines, design tokens, procedural Web Audio, interactive physics, canvas engines, and
  frontend development standards for creating opulent, high-performance, single-file static festival web applications.
---

# Festival Frontend Design & Engineering Skill

This skill defines the end-to-end design language, architectural patterns, visual tokens, interactive physics mechanics, procedural Web Audio synthesis, and canvas rendering standards for the **ParbonStatic** festival web application series (e.g., Krishna Janmashtami, Diwali, Durga Puja, Ganesh Chaturthi, Onam, Holi, Maha Shivratri, Navratri, etc.).

---

## 1. Core Engineering Philosophy & Constraints

1. **Zero-Dependency Architecture**:
   - 100% pure Semantic HTML5, Modern Vanilla CSS (variables, grid, flexbox, 3D transforms), and Native JavaScript (ES6+, Web Audio API, Canvas 2D).
   - No external JS frameworks (React, Vue, jQuery, Tailwind) or bulky asset bundles.
2. **Self-Contained Asset Model**:
   - **Favicons & Icons**: Inline Data-URI SVG vectors (`data:image/svg+xml,...`).
   - **Audio**: Synthesized procedurally in real-time via the browser's Web Audio API (`AudioContext`). Zero external MP3/WAV files.
   - **Visual Art & Badges**: Inline SVGs, CSS radial gradients, and dynamic `<canvas>` rendering.
   - **Social Meta**: High-resolution Open Graph image (`og-image.jpg`) in the project root.
3. **Rock-Solid 60–120 FPS Performance**:
   - Replace GPU-thrashing `backdrop-filter: blur()` with pre-composed semi-opaque RGBA tokens (`rgba(15, 33, 56, 0.88)`).
   - Offscreen sprite pre-rendering for canvas confetti and emoji blitting (<0.01ms per blit).
   - Throttled scroll and resize listeners inside `requestAnimationFrame` with `{ passive: true }`.
   - Automatic pause of canvas render loops when the browser tab is hidden (`visibilitychange`).
4. **Cultural Opulence & Premium Aesthetics**:
   - Deep midnight/cosmic atmospheric bases paired with luminous golden highlights, festival jewel tones, and warm cream typography.
   - Smooth micro-interactions, 3D perspective physics, and celebratory particle animations.

---

## 2. Design Token System & CSS Variable Architecture

Every festival project must define a structured `:root` palette adhering to this hierarchy:

### Standard CSS Variable Tokens
```css
:root {
  /* Dark Cosmic Atmosphere */
  --bg-dark: #060d17;               /* Deepest background shade */
  --bg-midnight: #0b182b;           /* Gradient backdrop tone */
  --bg-card: rgba(15, 33, 56, 0.88);/* Solid composite card (no backdrop blur) */
  --bg-card-hover: rgba(22, 47, 78, 0.95);

  /* Gold Illumination */
  --gold-primary: #FFB703;
  --gold-glow: #F3C64F;
  --gold-deep: #D4AF37;
  --gold-gradient: linear-gradient(135deg, #FFE885 0%, #FFB703 50%, #B8860B 100%);
  --border-gold: rgba(212, 175, 55, 0.35);
  --border-gold-bright: #e5a910;

  /* Festival Theme Accent (Tailor per festival) */
  --theme-primary: #008080;         /* E.g., Peacock Teal / Ruby / Emerald / Marigold */
  --theme-glow: #0a9396;
  --theme-bright: #94d2bd;
  --theme-deep: #005f73;
  --theme-gradient: linear-gradient(135deg, var(--theme-glow) 0%, var(--theme-deep) 50%, var(--bg-midnight) 100%);

  /* Devotional Jewel Accents */
  --lotus-pink: #FF758F;
  --lotus-pink-glow: #E05780;
  --saffron-orange: #FF9933;

  /* Typography Colors */
  --cream-light: #FFFDF8;           /* Primary text */
  --cream-muted: #E2DAC8;           /* Secondary text / captions */
  --text-muted: #94a3b8;            /* Low-emphasis meta */

  /* Typography Families */
  --font-title: 'Cinzel Decorative', 'Rozha One', Georgia, serif;
  --font-heading: 'Playfair Display', Georgia, serif;
  --font-sans: 'Poppins', system-ui, -apple-system, sans-serif;
  --font-scripture: 'Rozha One', 'Playfair Display', serif;

  /* Elevation Shadows & Radii */
  --shadow-sm: 0 4px 12px rgba(0, 0, 0, 0.25);
  --shadow-md: 0 8px 24px rgba(0, 0, 0, 0.35);
  --shadow-lg: 0 16px 40px rgba(0, 0, 0, 0.5);
  --shadow-gold-glow: 0 0 25px rgba(255, 183, 3, 0.35);

  --radius-sm: 8px;
  --radius-md: 16px;
  --radius-lg: 24px;
  --radius-full: 9999px;

  /* Transition Timings */
  --transition-fast: 0.18s cubic-bezier(0.2, 0, 0, 1);
  --transition-normal: 0.28s cubic-bezier(0.2, 0, 0, 1);
}
```

### Festival Color Palettes Quick Reference

| Festival | Dominant Accents | Jewel / Festive Tones | Atmospheric Base |
| :--- | :--- | :--- | :--- |
| **Krishna Janmashtami** | Radiant Gold (`#FFB703`), Peacock Teal (`#0a9396`) | Lotus Pink (`#FF758F`), Butter Cream (`#FFFDF8`) | Midnight Cosmic Sky (`#060d17`) |
| **Diwali / Deepavali** | Deep Amber Gold (`#FF9F1C`), Crimson Vermilion (`#D62828`) | Emerald Green (`#2EC4B6`), Saffron (`#F77F00`) | Royal Night Velvet (`#0F0826`) |
| **Durga Puja / Navratri**| Sindoor Red (`#C1121F`), Kasavu/Antique Gold (`#D4AF37`) | Kumkum Coral (`#E63946`), Jasmine White (`#FDF0D5`)| Sacred Twilight Crimson (`#180205`) |
| **Ganesh Chaturthi** | Modak Saffron (`#FF7B00`), Marigold Yellow (`#FFB703`) | Durva Grass Green (`#2A9D8F`), Hibiscus Red (`#E71D36`)| Divine Terracotta Dark (`#1C0B05`) |
| **Onam** | Kasavu Gold (`#D4AF37`), Banana Leaf Green (`#38B000`) | Pookkalam Orange (`#F77F00`), Lotus White (`#F8F9FA`)| Kerala Backwater Dusk (`#031A14`) |
| **Holi** | Gulal Magenta (`#E60067`), Pichkari Cyan (`#00B4D8`) | Haldi Yellow (`#FFD166`), Gulaal Purple (`#7209B7`) | Festivity Dark Slate (`#0B132B`) |

---

## 3. Structural Anatomy of a Festival Landing Page

Each festival application follows an engaging 9-part semantic structure:

```
+-------------------------------------------------------------------------+
| 1. STICKY HEADER                                                        |
|    [Logo SVG Badge]  [Jump Navigation Links]  [Procedural Audio Toggle] |
+-------------------------------------------------------------------------+
| 2. HERO SHOWCASE                                                        |
|    [Festival Pill Badge]  [Animated Motif SVG]  [Grand Heading & Shloka]|
|    [Primary Action CTAs (Interactive Experience & Traditions)]          |
+-------------------------------------------------------------------------+
| 3. SACRED LORE & LEGEND DECK                                            |
|    [Narrative Cards: Birth / Triumph / Divine Grace with SVG Icons]     |
+-------------------------------------------------------------------------+
| 4. SACRED TRADITIONS & RITUALS GRID                                     |
|    [Ritual Cards: Muhurat / Fasting / Aarti / Offerings / Chants]       |
+-------------------------------------------------------------------------+
| 5. SIGNATURE INTERACTIVE CULTURAL SIMULATION                            |
|    [3D Z-Axis Physics / Drag & Toss Mechanics / Multi-Stage Break / SFX]|
|    [Festive Score Counter & Particle Confetti Blast Engine]             |
+-------------------------------------------------------------------------+
| 6. SCRIPTURAL WISDOM & SACRED VERSES                                    |
|    [Sanskrit Verse / Native Script + Transliteration + Translation]     |
+-------------------------------------------------------------------------+
| 7. HD FESTIVE GREETING CARD STUDIO (CANVAS RENDERER)                    |
|    [Live Form Inputs] -> [Real-time 1200x800 Canvas Preview]            |
|    [Theme Switcher] -> [HD PNG Export] -> [WhatsApp Direct Share]       |
+-------------------------------------------------------------------------+
| 8. COMMUNITY & CELEBRATION COUNTER / DEVOTIONAL AURA                    |
|    [Live Devotion Counter / Aarti Chime Player]                         |
+-------------------------------------------------------------------------+
| 9. DEVOTIONAL FOOTER                                                    |
|    [Sacred Benediction]  [Quick Links]  [Back-to-top]  [ParbonStatic]   |
+-------------------------------------------------------------------------+
```

---

## 4. Interactive Physics & Cultural Mechanics

A hallmark of ParbonStatic applications is an interactive cultural module with real-time physics and tactile responsiveness:

### A. 3D Z-Axis Swing / Pendulum Mechanics
Use true 3D perspective (`perspective: 1100px` on parent, `transform-style: preserve-3d` on pendulum) pivoting from the exact anchor (`transform-origin: 50% 0`):

```css
.interactive-viewport {
  perspective: 1100px;
  perspective-origin: 50% 25%;
}

.pendulum-rig {
  transform-origin: 50% 0;
  transform-style: preserve-3d;
  will-change: transform;
}

@keyframes forwardBackward3D {
  0%   { transform: rotateX(0deg) translateZ(0px); }
  25%  { transform: rotateX(-14deg) translateZ(-45px) scale(0.94); }
  50%  { transform: rotateX(0deg) translateZ(0px) scale(1); }
  75%  { transform: rotateX(17deg) translateZ(55px) scale(1.05); }
  100% { transform: rotateX(0deg) translateZ(0px) scale(1); }
}
```

### B. Multi-Stage Interactive Destruction / Lighting Engine
1. **Stage 1 (Gesture / Aim)**: Pointer / Touch drag or hover targeting.
2. **Stage 2 (Impact Transient)**: Strike animation + vibration + dynamic fracture SVG lines.
3. **Stage 3 (Rupture / Burst)**: Fragment dispersal + radial particles + synthesized victory chime.
4. **Stage 4 (Respawn / Loop)**: Automatic reset with smooth opacity/scale entrance after cooldown.

---

## 5. Procedural Web Audio API Synthesis Standard

Never bundle static audio files. Implement dynamic procedural synthesis using native `AudioContext`:

```javascript
class FestivalAudioEngine {
  constructor() {
    this.ctx = null;
    this.isMuted = true;
  }

  init() {
    if (!this.ctx) {
      const AudioCtx = window.AudioContext || window.webkitAudioContext;
      this.ctx = new AudioCtx();
    }
    if (this.ctx.state === 'suspended') {
      this.ctx.resume();
    }
  }

  // Pure flute / woodwind sine tone with lowpass filtering
  playFluteNote(freq, duration = 1.2) {
    if (this.isMuted) return;
    this.init();
    const osc = this.ctx.createOscillator();
    const gain = this.ctx.createGain();
    const filter = this.ctx.createBiquadFilter();

    filter.type = 'lowpass';
    filter.frequency.value = 1200;

    osc.type = 'sine';
    osc.frequency.setValueAtTime(freq, this.ctx.currentTime);

    const now = this.ctx.currentTime;
    gain.gain.setValueAtTime(0, now);
    gain.gain.linearRampToValueAtTime(0.2, now + 0.15); // soft breath attack
    gain.gain.exponentialRampToValueAtTime(0.001, now + duration);

    osc.connect(filter);
    filter.connect(gain);
    gain.connect(this.ctx.destination);

    osc.start(now);
    osc.stop(now + duration);
  }

  // Metallic Temple Bell with multi-harmonic inharmonic sines
  playTempleBell() {
    if (this.isMuted) return;
    this.init();
    const freqs = [1046.5, 2093.0, 3135.96, 4186.0]; // Bronze partials
    const gains = [0.25, 0.12, 0.06, 0.02];

    freqs.forEach((f, i) => {
      const osc = this.ctx.createOscillator();
      const gain = this.ctx.createGain();
      const now = this.ctx.currentTime;

      osc.type = 'sine';
      osc.frequency.setValueAtTime(f, now);

      gain.gain.setValueAtTime(gains[i], now);
      gain.gain.exponentialRampToValueAtTime(0.0001, now + 3.2);

      osc.connect(gain);
      gain.connect(this.ctx.destination);

      osc.start(now);
      osc.stop(now + 3.2);
    });
  }

  // Celebratory Multi-note Chime (e.g. Major Triad Arpeggio)
  playVictoryChime() {
    if (this.isMuted) return;
    const notes = [1318.51, 1661.22, 1975.53, 2637.02]; // E6, G#6, B6, E7
    notes.forEach((freq, idx) => {
      setTimeout(() => this.playFluteNote(freq, 0.8), idx * 90);
    });
  }
}
```

---

## 6. High-DPI Greeting Card Canvas Studio

Every festival app includes a live client-side Greeting Card Studio generating exportable $1200 \times 800\text{ px}$ PNGs:

### Key Canvas Engine Requirements:
1. **Dimensions**: Standard $1200 \times 800\text{ px}$ canvas scaled via CSS for mobile responsiveness.
2. **Radial Themes**: Theme presets matching festival palettes (Midnight, Gold, Jewel, Forest/Temple).
3. **Ornate Borders & Corners**: Double golden borders (`ctx.strokeRect`), corner floral rosettes, and ornamental divider SVGs.
4. **Smart Word Wrapping**: Dedicated `wrapText(ctx, text, x, y, maxWidth, lineHeight)` to prevent overflow of greetings.
5. **Instant Export**:
   - `canvas.toDataURL('image/png')` for direct file download.
   - WhatsApp Share URL: `https://api.whatsapp.com/send?text=${encodeURIComponent(shareText)}`.

---

## 7. Zero-Lag Sprite-Blit Particle Engine

To animate 100+ confetti emojis without stalling the JS thread:

```javascript
// 1. Pre-render glyph bitmaps onto offscreen sprites once
const emojiSprites = {};
const emojis = ['🌸', '✨', '🌼', '💛', '🌺', '🦚', '🥛', '🍯', '🧈'];

emojis.forEach(emoji => {
  const offCanvas = document.createElement('canvas');
  offCanvas.width = 64;
  offCanvas.height = 64;
  const oCtx = offCanvas.getContext('2d');
  oCtx.font = '40px "Segoe UI Emoji", Arial, sans-serif';
  oCtx.textAlign = 'center';
  oCtx.textBaseline = 'middle';
  oCtx.fillText(emoji, 32, 32);
  emojiSprites[emoji] = offCanvas;
});

// 2. In animation loop: use lightning-fast GPU texture blitting
function renderParticles(ctx, particles) {
  for (let i = 0; i < particles.length; i++) {
    const p = particles[i];
    const sprite = emojiSprites[p.emoji];
    if (!sprite) continue;

    ctx.save();
    ctx.translate(p.x, p.y);
    ctx.rotate(p.rotation);
    ctx.globalAlpha = p.alpha;
    const half = p.size / 2;
    ctx.drawImage(sprite, -half, -half, p.size, p.size); // ~0.005ms blit
    ctx.restore();
  }
}
```

---

## 8. SEO, Open Graph & Favicon Checklist

Every festival page must include:
- [ ] Inline SVG Data-URI `<link rel="icon">` and `<link rel="apple-touch-icon">`.
- [ ] `<meta name="theme-color" content="#...">` matching the festival dark base.
- [ ] `<link rel="canonical" href="https://parbonstatic.github.io/[FestivalName]/">`.
- [ ] Complete Open Graph tags: `og:type`, `og:url`, `og:title`, `og:description`, `og:image` (1200x675), `og:image:width`, `og:image:height`, `og:site_name`, `og:locale`.
- [ ] Complete Twitter Card tags: `twitter:card` (`summary_large_image`), `twitter:title`, `twitter:description`, `twitter:image`.
- [ ] Google Fonts preconnect (`https://fonts.googleapis.com` and `https://fonts.gstatic.com`).
- [ ] Fully semantic HTML hierarchy with single `<h1>` and descriptive ARIA labels.

---

## 9. Documentation Synchronization

Whenever a festival site is created or updated:
- Maintain [`GEMINI.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/GEMINI.md) for deep engineering analysis, math formulas, DSP parameters, and gitGraph milestones.
- Maintain [`README.md`](file:///d:/Playground/ParbonStatic/Janmashtami2026/README.md) for user features and execution instructions.
- Follow the [`update-project-docs`](file:///d:/Playground/ParbonStatic/Janmashtami2026/.agents/skills/update-project-docs/SKILL.md) skill workflow.
