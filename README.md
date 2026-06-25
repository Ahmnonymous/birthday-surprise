# Birthday Surprise Website

A handcrafted, single-page interactive birthday journey for **Arzoo Tariq** — warm, thoughtful, and respectful. Pure HTML, CSS, and JavaScript. No build step. GitHub Pages compatible.

**Tone:** Observational, mature, celebratory — not romantic. Framed as *what I've noticed in a few days*, not *I know everything about you*.

---

## Project structure

```
Birthday/
├── index.html              # Complete site (~3,600+ lines) — HTML, CSS, JS inline
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

## Journey Mode

After the welcome screen, **Start Journey** activates **Journey Mode** — a guided step-by-step experience with a fixed bottom navigation bar.

### Journey steps (9)

| Step | Section | ID | Advance when |
|------|---------|-----|--------------|
| 0 | Welcome | `#section-welcome` | Welcome card entrance done |
| 1 | Memories | `#section-photos` | Photo typewriter complete or skipped |
| 2 | Noticed | `#section-noticed` | Cinematic sequence complete or skipped |
| 3 | Celebrating | `#section-celebrate` | Card entrance animations done |
| 4 | More Likes | `#section-instagram` | Card entrance animations done |
| 5 | Quiz | `#section-quiz` | All 4 questions answered |
| 6 | Make A Wish | `#section-cake` | Section entered (candle blow optional) |
| 7 | Garden | `#section-garden` | Garden intro typewriter complete or skipped |
| 8 | Final Message | `#section-sky` | Final typewriter complete or skipped |

### Journey bar controls

Fixed bottom bar (`#journey-bar`, z-index 850):

- **Progress dots** — tap completed/current steps to jump back
- **Skip Animation** — instantly reveals active typewriter/cinematic (not quiz answers)
- **Previous** — go to prior step (hidden on step 0)
- **Continue Journey** — steps 0–7 (disabled until step gate passes)
- **Finish Journey** — step 8 (sky finale)

### Dual scroll behavior

- Journey Mode dims inactive sections (`opacity` + `blur`) and focuses the current step
- Manual scroll still works — `IntersectionObserver` syncs progress and runs section enter logic
- Free-scroll without Journey Mode also triggers section animations via `ScrollTrigger` fallbacks

### Skip Animation & reduced motion

- **Skip Animation** calls `TypewriterEngine.skip()` and marks the current step ready
- `prefers-reduced-motion`: text reveals instantly, Skip button hidden, particles disabled

---

## Journey map

```
Loader → Welcome → [Start Journey] → Photos → Noticed → Celebrate → Instagram → Quiz → Cake → Garden → Sky
                                                                                              ↳ Secret Letter 💌
                                                                                              ↳ Moon Easter Egg (×5)
```

---

## Personalization (`CONFIG`)

Edit the `CONFIG` object at the top of the `<script>` block in `index.html` (~line 1600).

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

### Journey orchestration
- `JourneyController` — step navigation, completion gates, scroll sync, keyboard ←/→
- `TypewriterEngine` — cancellable typewriters with skip support
- `DecorationManager` — particle intensity by active section + text-focus dimming; pauses off-screen canvases

### Audio system
- **Play/pause** via 🎵 button
- **Volume slider** and **mute** in glass panel (bottom-right, z-index 860)
- Panel shifts up when journey bar is visible to avoid overlap
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
- Expanded copy no longer clipped (`max-height: none`)

### Instagram section
- "A Few Things That Deserve More Likes"
- 5 cards: Creativity, Growth, Strength, Effort, Kindness
- Tap reveals personalized message with hover animations

### Quiz
- Observational questions with confetti on each answer
- **Next** blocked until all 4 questions answered (Skip does not bypass quiz)
- No auto-scroll to cake — user advances via Journey bar

### Cake
- Enhanced flame glow + cake aura
- Mic blow detection + fallback button
- Smoke, confetti, birthday music
- Typewriter wish on blow: *"May all the wishes you don't talk about find their way to you."*

### Garden
- Upgraded bloom (elastic GSAP)
- Particle burst on each flower
- Flower messages flip below when near top edge
- Handcrafted messages

### Sky finale
- Slow typewriter closing note
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

### Z-index scale

| Layer | z-index |
|-------|---------|
| Particle canvases | 0 |
| Section content | 2 |
| Moon, flower messages | 10 |
| Journey bar | 850 |
| Audio panel | 860 |
| Lightbox | 9400 |
| Easter egg modal | 9500 |
| Secret letter modal | 9600 |

### Accessibility
- Semantic landmarks, ARIA labels, keyboard focus
- Journey bar: `aria-current="step"`, `aria-disabled` on Continue when gated
- Focus moves to section heading on step change
- `aria-expanded` on expandable cards
- `aria-live` on typewriter regions
- `prefers-reduced-motion` disables particles, shortens animations, instant text

### Performance
- Particle `requestAnimationFrame` loops pause when canvas leaves viewport
- Decorative intensity reduced 50% during active typewriter (`DecorationManager.setTextFocus`)
- Confetti skipped when `document.hidden` or reduced motion (unless user-triggered with `force: true`)
- Debounced `ScrollTrigger.refresh()` on resize

### GitHub Pages
1. Push `Birthday/` contents to repo (or set `/docs` to `Birthday/`)
2. Enable Pages in repo settings
3. Ensure `assets/` paths remain relative to `index.html`

---

## Code organization (`index.html`)

1. HEAD / META / CDN  
2. CSS: Variables, Loader, Global UI, Journey bar, Sections 1–9, Modals  
3. HTML: Loader, Audio panel, Journey bar, Lightbox, Modals, Sections  
4. JS: CONFIG  
5. JS: Utilities (audio, confetti, scroll)  
6. JS: `TypewriterEngine`, `DecorationManager`, `JourneyController`  
7. JS: Section inits (`initWelcome` … `initEasterEgg`)  
8. JS: `init()`  

---

## QA checklist

### Journey Mode (all 10 steps)
- [ ] Loader → Welcome → Start Journey activates bar
- [ ] Each step: text fully visible during and after animations
- [ ] Continue disabled until gate passes; Skip reveals typewriter instantly
- [ ] Previous returns to prior step with smooth scroll
- [ ] Quiz blocks Continue until Q4 done; Skip does not skip quiz
- [ ] Finish Journey on sky step fires confetti
- [ ] Manual scroll updates progress dots and section focus
- [ ] Keyboard ←/→ navigates when journey active

### Sections
- [ ] Photos: swipe, arrows, lightbox, placeholders if no images
- [ ] Cinematic section plays paragraph sequence once (or skip)
- [ ] Celebrate cards expand/collapse without clipping long copy
- [ ] Instagram cards reveal on tap
- [ ] Mic blow + button + wish message
- [ ] Flowers bloom with particles; tooltips not clipped
- [ ] Sky typewriter + secret letter modal scroll on small screens
- [ ] Moon ×5 easter egg

### Layout & overlap
- [ ] Journey bar + audio panel do not overlap (375px, 768px, 1280px)
- [ ] No horizontal overflow on mobile
- [ ] Safe-area insets on journey bar (notched devices)
- [ ] Modals above journey chrome

### Performance & a11y
- [ ] Particles dim/pause when section inactive or off-screen
- [ ] Music: play, pause, volume, mute, fade
- [ ] `prefers-reduced-motion`: instant text, journey still navigable
- [ ] No console errors with missing audio

---

## Intent

A personal gift celebrating quiet strength, resilience, creativity, and independence — written for someone you've only known a short while, without pressure or romantic overtones.

Customize via `CONFIG` and `assets/`. No framework. No build. Just open and share.
