# Birthday Surprise Website

A handcrafted, single-page interactive birthday journey for **Arzoo Tariq** — warm, thoughtful, and respectful. Pure HTML, CSS, and JavaScript. No build step. GitHub Pages compatible.

**Tone:** Observational, mature, celebratory — not romantic. Framed as *what I've noticed in a few days*, not *I know everything about you*.

---

## Project structure

```
Birthday/
├── index.html              # Complete site (~2,600+ lines) — HTML, CSS, JS inline
├── README.md               # This documentation
└── assets/
    ├── README.txt          # Asset filenames quick reference
    ├── photo1.jpg …        # Polaroid photos (auto-discovered, see below)
    ├── bg-music.mp3        # Looping background music
    ├── happy-birthday.mp3  # Short clip when candles are blown
    ├── click.mp3           # (optional) UI click
    ├── bloom.mp3           # (optional) Flower bloom
    └── sparkle.mp3         # (optional) Celebration sparkle
```

Open `index.html` in any modern browser, or deploy the `Birthday/` folder to GitHub Pages.

---

## Journey map (10 sections)

```
Loader → Welcome → Photos → The Arzoo I've Noticed → Celebrating You → Instagram → Quiz → Cake → Garden → Sky
                                                                                              ↳ Secret Letter 💌
                                                                                              ↳ Moon Easter Egg (×5)
```

| # | Section | ID | Highlights |
|---|---------|-----|------------|
| — | Loader | `#loader` | Pulsing cake, min 1.2s, GSAP fade-out |
| 1 | Welcome | `#section-welcome` | Aurora gradient, hearts/stars, Start Journey + confetti |
| 2 | Photo journey | `#section-photos` | Polaroids, parallax, swipe, lightbox, sparkles, photo auto-discovery |
| 3 | The Arzoo I've Noticed | `#section-noticed` | Cinematic typewriter — one paragraph at a time with fade transitions |
| 4 | Celebrating you | `#section-celebrate` | 4 expandable premium cards (tap to reveal deeper messages) |
| 5 | Instagram | `#section-instagram` | 5 Instagram-style cards — tap to reveal appreciation messages |
| 6 | Quiz | `#section-quiz` | Observational questions, confetti, scroll to cake |
| 7 | Cake | `#section-cake` | 3D cake, mic blow, glow, smoke, wish typewriter |
| 8 | Garden | `#section-garden` | Bloom animations, particles, handcrafted flower messages |
| 9 | Sky | `#section-sky` | Lanterns, shooting stars, cinematic closing letter, secret message button |

---

## Personalization (`CONFIG`)

Edit the `CONFIG` object at the top of the `<script>` block in `index.html` (~line 1500).

| Key | Purpose |
|-----|---------|
| `name` | Recipient name |
| `photoCount` | Max photos to auto-scan (`photo1.jpg` … `photoN.jpg`) |
| `photoCaptions` | Captions aligned to photo index |
| `photos` | Fallback list if no assets found |
| `photoMessages` | Typewriter under carousel |
| `cinematicMessages` | "The Arzoo I've Noticed" paragraphs |
| `celebrateCards` | `{ icon, title, preview, expanded }` |
| `instagramCards` | `{ icon, label, message }` |
| `quiz` | Questions and options |
| `gardenIntroMessages` | Garden intro typewriter |
| `flowerMessages` | One per flower |
| `cakeWishMessage` | Shown after candles blown |
| `finalMessage` | Sky scene closing |
| `secretLetter` | Handwritten modal letter |
| `music` / `sfx` | Audio file paths |

### Photo auto-discovery

Browsers cannot list folders. On load, the site probes `assets/photo1.jpg` through `assets/photo{photoCount}.jpg` and builds the carousel from files that exist. To add photos:

1. Drop `photo5.jpg`, `photo6.jpg`, etc. into `assets/`
2. Optionally extend `photoCaptions` and `photoCount` in `CONFIG`

No code changes required beyond `CONFIG` if filenames follow the pattern.

---

## Features

### Audio system
- **Play/pause** via 🎵 button
- **Volume slider** and **mute** in glass panel (bottom-right)
- **Smooth fade in/out** (GSAP volume tween)
- **Birthday clip** on candle blow; background music fades out and resumes after
- Missing `bg-music.mp3` fails silently — no console errors

### Photo journey
- Floating polaroids with GSAP
- Scroll parallax on section
- Touch swipe + arrow navigation
- **Lightbox** on tap (Escape to close)
- Sparkle particles overlay

### Cinematic storytelling
- "The Arzoo I've Noticed" — dark aurora scene, particles, paragraph-by-paragraph typewriter with fade between lines

### Celebrating you cards
- 🥗 Nutritionist · 📸 Creator · 💪 Quiet Strength · 🌿 Independence
- Tap to expand with animation + confetti + SFX

### Instagram section
- "A Few Things That Deserve More Likes"
- 5 cards: Creativity, Growth, Strength, Effort, Kindness
- Tap reveals personalized message with hover animations

### Cake
- Enhanced flame glow + cake aura
- Mic blow detection + fallback button
- Smoke, confetti, birthday music
- Typewriter: *"May all the wishes you don't talk about find their way to you."*

### Garden
- Upgraded bloom (elastic GSAP)
- Particle burst on each flower
- New handcrafted messages

### Sky finale
- Slow typewriter closing note (user-specified copy)
- Signature: *"From someone who noticed the strength behind your silence 🌙"*
- **A Little Message For You 💌** — paper-texture modal with live typewriter letter

### Easter egg
- Click **moon** 5 times → Fun Fact modal

---

## Technical stack

| Library | CDN | Use |
|---------|-----|-----|
| GSAP 3.12 | jsDelivr | Animations, fades, timelines |
| ScrollTrigger | jsDelivr | Scroll-linked reveals |
| ScrollToPlugin | jsDelivr | Section navigation |
| canvas-confetti | jsDelivr | Celebrations |
| Google Fonts | CDN | Nunito + Cormorant Garamond |

### Accessibility
- Semantic landmarks, ARIA labels, keyboard focus
- `aria-expanded` on expandable cards
- `aria-live` on typewriter regions
- `prefers-reduced-motion` disables particles, shortens animations

### GitHub Pages
1. Push `Birthday/` contents to repo (or set `/docs` to `Birthday/`)
2. Enable Pages in repo settings
3. Ensure `assets/` paths remain relative to `index.html`

---

## Code organization (`index.html`)

1. HEAD / META / CDN  
2. CSS: Variables, Loader, Global UI, Sections 1–9, Modals  
3. HTML: Loader, Audio panel, Lightbox, Modals, Sections  
4. JS: CONFIG  
5. JS: Utilities (audio, confetti, typewriter, photos, particles)  
6. JS: Section inits (`initWelcome` … `initSecretLetter`, `initEasterEgg`)  
7. JS: `init()`  

---

## QA checklist

- [ ] Loader → Welcome → full scroll journey  
- [ ] Photos: swipe, arrows, lightbox, placeholders if no images  
- [ ] Cinematic section plays paragraph sequence once  
- [ ] Celebrate cards expand/collapse  
- [ ] Instagram cards reveal on tap  
- [ ] Quiz confetti + scroll to cake  
- [ ] Mic blow + button + wish message  
- [ ] Flowers bloom with particles  
- [ ] Sky typewriter + secret letter modal  
- [ ] Moon ×5 easter egg  
- [ ] Music: play, pause, volume, mute, fade  
- [ ] Mobile 375px + desktop 1280px  
- [ ] Reduced motion respected  
- [ ] No console errors with missing audio  

---

## Intent

A personal gift celebrating quiet strength, resilience, creativity, and independence — written for someone you've only known a short while, without pressure or romantic overtones.

Customize via `CONFIG` and `assets/`. No framework. No build. Just open and share.
