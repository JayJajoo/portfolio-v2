# Jay Jajoo — Portfolio v2

> Personal portfolio website with glassmorphism design, particle animations, and full dark-mode aesthetic.
> Live at: **https://jayjajoo.github.io/portfolio-v2**

---

## Stack

- **Vanilla HTML + CSS + JavaScript** — zero build step, zero dependencies
- Single `index.html` file — drop it anywhere and it works
- GitHub Pages for hosting

---

## Design System

### Color Palette

| Token | Hex | Usage |
|---|---|---|
| `--bg-deep` | `#050510` | Page background |
| `--bg-surface` | `rgba(255,255,255,0.04)` | Glass card base |
| `--bg-surface-hover` | `rgba(255,255,255,0.08)` | Glass card hover state |
| `--accent-cyan` | `#00d4ff` | Primary accent, links, glow |
| `--accent-purple` | `#7b2fff` | Secondary accent, gradient |
| `--accent-pink` | `#ff2d78` | Highlights, tags |
| `--text-primary` | `#e8e8f0` | Body text |
| `--text-muted` | `#8888aa` | Secondary text, captions |
| `--border` | `rgba(255,255,255,0.08)` | Card borders |

### Typography

```
Headings  →  'Orbitron' (Google Fonts) — futuristic, geometric
Body      →  'Inter' (Google Fonts) — clean, readable
Code/mono →  'JetBrains Mono' (Google Fonts)
```

Heading scale: `4rem → 2.5rem → 1.75rem → 1.25rem → 1rem`
Line height: `1.7` for body, `1.2` for headings

### Glassmorphism Formula

Every card uses this exact recipe:

```css
.glass-card {
  background: rgba(255, 255, 255, 0.04);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4),
              inset 0 1px 0 rgba(255, 255, 255, 0.06);
}
```

Hover state adds:
```css
border-color: rgba(0, 212, 255, 0.3);
box-shadow: 0 0 30px rgba(0, 212, 255, 0.15);
transform: translateY(-4px);
```

---

## Animation System

### Keyframes

| Name | Effect | Used On |
|---|---|---|
| `rotate-border` | Rotating conic-gradient border | Project cards, avatar |
| `shimmer` | Left-to-right shine sweep | Card hover |
| `float` | Gentle up-down bob | Background orbs |
| `pulse-glow` | Breathing glow ring | Avatar |
| `fadeInUp` | Slide up + fade in | Section entrance |
| `stagger-in` | Sequential child entrance | Skill pills |
| `typing-blink` | Cursor blink | Hero subtitle |
| `counter-up` | Numeric count animation | Stat counters |
| `particle-drift` | Random drift | Canvas particles |
| `scanline` | Horizontal scan | Hero overlay |

### Scroll Reveal

Uses `IntersectionObserver` — no library needed:

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach(el => {
    if (el.isIntersecting) el.target.classList.add('visible');
  });
}, { threshold: 0.15 });
```

Elements get `.reveal` class by default (opacity 0, translateY 30px).
`.visible` transitions to opacity 1, translateY 0 over 0.6s.

### Typing Effect

Cycles through an array of roles with a typewriter effect:
```js
const roles = ['Data Scientist', 'ML Engineer', 'LLM Builder', 'AI Researcher'];
```
Character-by-character write, pause 2s, character-by-character erase, repeat.

### Particle System

Canvas-based, ~80 particles. Each particle:
- Random position, velocity, size (1–3px)
- Color: cyan or purple, low opacity
- Mouse proximity → particles repel slightly
- Particles connect with lines when within 120px of each other

---

## Sections

### 1. 🚀 Hero
- Full-screen dark canvas with particles
- Animated `JJ` initials avatar — rotating conic-gradient ring, pulse glow
- Name `Jay Jajoo` in Orbitron
- Typing subtitle cycling through roles
- Two CTA buttons: **Download Resume** + **View GitHub**
- Social icon row: LinkedIn, GitHub, Email, Kaggle
- Scroll indicator arrow bouncing at bottom

### 2. 🧠 About
- Glass card with bio paragraph
- 4 animated stat counters: GPA 3.96 · 1,700+ Features Engineered · 9.5M Records Processed · 2 Publications
- Tech philosophy blurb

### 3. ⚡ Skills
- 4 category groups: Languages · ML/AI · Data & MLOps · Cloud & Tools
- Each skill is a pill tag with icon emoji and glow on hover
- Staggered entrance animation (each pill delays by 50ms)

### 4. 💼 Experience
- Vertical timeline, left-aligned connector line
- Each role is a glass card: company, title, dates, bullet points
- Timeline dot pulses on scroll-enter

### 5. 🚀 Projects
- 3-column responsive grid (→ 2 → 1 on smaller screens)
- Each card: project name, description, tech stack tags, GitHub link button
- Rotating neon border on hover, shine sweep, lift effect
- 7 projects total (4 from resume + 3 from GitHub)

### 6. 📄 Publications
- Two glass cards side-by-side
- Publisher badge (Springer green, IEEE blue)
- Paper title, venue, year

### 7. 🏆 Achievements
- AWS cert badge card
- Two publication achievement cards
- Glowing border treatment

### 8. 📬 Contact
- Central glass card with email, LinkedIn, GitHub, Kaggle icon buttons
- Each button has glow color matching the platform brand

---

## File Structure

```
portfolio-v2/
├── index.html       ← everything lives here
└── README.md        ← this file
```

No `node_modules`, no `package.json`, no build step.

---

## Deploy to GitHub Pages

1. Push `index.html` to `main` branch
2. Go to repo → **Settings** → **Pages**
3. Source: **Deploy from a branch** → `main` → `/ (root)`
4. Click **Save**
5. Live in ~60 seconds at `https://jayjajoo.github.io/portfolio-v2`

---

## Customization Guide

### Update content
All content is in the HTML — search for section comments like `<!-- HERO -->`, `<!-- PROJECTS -->` etc.

### Change accent colors
Edit the CSS variables at the top of `<style>`:
```css
:root {
  --accent-cyan: #00d4ff;    /* change this */
  --accent-purple: #7b2fff;  /* and this */
}
```

### Add a new project
Copy a `.project-card` block and fill in the details. Add new tech tags by copying `.tag` spans.

### Change typing roles
Edit the array in the `<script>` section:
```js
const roles = ['Data Scientist', 'ML Engineer', 'LLM Builder', 'AI Researcher'];
```

### Swap avatar for a real photo
Replace the `#avatar` div with:
```html
<img src="your-photo.jpg" alt="Jay Jajoo" class="avatar-img" />
```
And add `.avatar-img { border-radius: 50%; width: 180px; height: 180px; object-fit: cover; }` to the CSS.

---

## Commit History

| Commit | What was added |
|---|---|
| `init: project scaffold + README` | Folder structure, README |
| `feat: hero section — nav, canvas, avatar, typing` | HTML head + CSS vars + hero |
| `feat: about + skills sections` | About stats, skill pills |
| `feat: experience timeline + projects grid` | Timeline cards, project cards |
| `feat: publications + achievements + contact` | Final content sections |
| `feat: full JS — particles, scroll reveal, counters` | All JavaScript |
| `polish: responsive + cursor + back-to-top` | Mobile CSS, final UX |

---

Built with ❤️ and way too many CSS keyframes.
