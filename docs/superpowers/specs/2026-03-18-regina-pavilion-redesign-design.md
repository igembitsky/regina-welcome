# Regina's Agentic Builder Playbook — The Pavilion Redesign

## Context

Regina is a designer learning to use AI-powered development tools. The current onboarding page (`index.html`) uses a dark, glassmorphic, neon-accented tech aesthetic that doesn't resonate with her design sensibility. This redesign transforms the page into a Scandinavian minimalist experience inspired by Zaha Hadid's parametric fluidity — specifically "The Pavilion" approach, where warm ambient light, flowing parametric curves, and spatial depth create an inviting, premium experience.

The page serves two purposes:
1. **Setup tutorial** — Walk Regina through installing VS Code, developer tools, Claude Code, and Superpowers
2. **Use case inspiration** — Show her what she can build: a professional portfolio and Figma-to-prototype client workflows

## Design Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Visual direction | Hadid-Fusion Fluidity | Parametric curves on clean canvas, bold and contemporary |
| Execution style | The Pavilion | Warm ambient light, shifting backgrounds, spatial depth — like walking through a Hadid building |
| Page structure | Setup first, use cases as payoff | Keep tutorial clean, build to the exciting reveal |
| Portfolio section | The Reveal | Kinetic typography + horizontal scroll of Awwwards portfolios with design decodes |
| Figma section | Interactive demo | Live before/after showing Figma template branded for different clients |
| Interaction model | Hybrid: Calm → Dramatic | Setup scrolls naturally, parametric sweep transitions to cinematic sections |
| Regina's image | Hero-level presence | Large portrait in hero, her face is part of the brand |

## Visual Language

### Color System
- **Setup zone (warm):** Background gradient from `#f5f0e8` to `#e8e2d8`. Text: `#2c2418` (dark warm brown). Secondary: `#8a7e6b` (warm gray). Accent: `#c4a882` (warm gold).
- **The Reveal (dark):** Background `#0a0a0a`. Text: white. Secondary: `#666`. Borders: `#222`.
- **The Studio (warm return):** Gradient from dark back to `#f0ebe2` / `#e8e2d8`.
- **Ambient effects:** Radial gradients (`rgba(255,248,235,0.8)`) that shift position as user scrolls.

### Typography
- **Headings:** Inter variable font, weights 100 (ultralight) and 700-800 (bold) for dramatic contrast. Update Google Fonts import to include weights 100 through 800 (`wght@100;200;300;400;500;600;700;800`).
- **Body:** Inter, weight 400, 13-14px, generous line-height (1.6-1.7)
- **Monospace:** JetBrains Mono (retained from current) for code blocks and terminal mockups
- **Scale:** Use `clamp()` for responsive sizing. Hero heading ~52-64px on desktop, scales down for mobile.
- **Letter-spacing:** Tight (-1.5px) on large headings, wide (3-6px) on uppercase labels

### Parametric Elements
- SVG curves used as atmospheric elements throughout — not borders or dividers
- Curves are subtle (0.04-0.1 opacity) in the setup zone, more prominent in transitions
- Quadratic bezier paths (`Q` commands) for organic Hadid-like flow
- Multiple layered curves at different opacities create depth

### Layout Principles
- Maximum content width ~1100px, centered
- Generous whitespace — sections breathe
- Cards have soft shadows (`0 4px 24px rgba(107,94,75,0.08)`) and slight border-radius (8-10px)
- No hard borders between sections in the Pavilion zones — backgrounds gradient into each other

## Page Architecture

### Section 1 — Hero (full viewport)
- **Background:** Warm cream gradient with ambient radial light glows
- **Left side:** Large ultralight heading: "Hey Regina, let's build something **extraordinary.**" Parametric curve line below. Subtitle in warm gray.
- **Right side:** Regina's portrait — floating with soft shadow (`box-shadow: 0 8px 32px rgba(107,94,75,0.15)`), subtle warm light overlay on top-right corner. Rounded corners (4px). Caption "DESIGNER · BUILDER" below.
- **Nav:** Her name top-left, section counter top-right. The counter is fixed-position and updates to reflect the current visible section (01/09 through 09/09) as user scrolls. Uses warm gray color (`#8a7e6b`), inverts to `#666` on dark sections.
- **Bottom:** "SCROLL ↓" hint
- **Animation:** Portrait has subtle parallax on scroll. Ambient light glows pulse very slowly. Heading can fade in on load.

### Sections 2–6 — Setup (Calm Zone)
Five steps, each a full-width content block scrolling naturally:

1. **Create Your Accounts** — GitHub + Claude signup
2. **Install VS Code** — macOS download and install
3. **Install Developer Tools** — Homebrew + Git via Terminal
4. **Install Claude Code** — VS Code extension
5. **Install Superpowers** — Plugin for advanced features

**Per-step structure:**
- Large ultralight step number (01–05) with section title
- One-line description in warm gray
- Instructional content: same information as current page, rewritten in warm conversational tone
- Terminal mockups: dark cards (`#1a1a1a` background) with JetBrains Mono, typewriter animation on scroll-into-view
- UI mockups: VS Code window, Spotlight search, file manager — restyled in warm palette
- Copy-to-clipboard buttons on all code blocks (retain current clipboard functionality)

**Navigation:**
- Thin parametric SVG progress curve along left margin, fixed position. The path is a gently undulating vertical line (~600px tall) using quadratic bezier curves. Five anchor points are evenly spaced along the curve, one per step. A small filled circle (r=4) tracks the user's position by interpolating between anchor points as they scroll through steps 1–5. The curve and dot are only visible during the setup zone (sections 2–6) and fade out at the transition.
- Steps fade in with gentle GSAP scroll-triggered reveals (translateY + opacity)

### The Transition (full viewport)
- **Background:** Gradient from warm cream (`#f0ebe2`) through mid-tones to black (`#0a0a0a`)
- **Animation:** Parametric curves animate across viewport left-to-right (GSAP ScrollTrigger, staggered)
- **Text:** "Tools installed · Environment ready" in warm gold, then "Now, the real work begins." in white
- **Purpose:** Emotional shift from instructional to aspirational. The user feels the page change.

### Section 7 — The Reveal (Portfolio)
- **Background:** Black (`#0a0a0a`) with subtle white parametric SVG curves at low opacity
- **Part 1 — Kinetic Typography:** "Your work / **deserves** / a stage." — each line animates in via clip-reveal (GSAP). "deserves" is bold 800 weight. Subtitle below explains the design decode concept.
- **Part 2 — Horizontal Scroll Strip:** 6 portfolio cards (360px wide each, 16:10 aspect ratio for preview area) showcasing different portfolio schools:
  - The Jony Ive School (minimal, product-first)
  - The Joseph Santamaria School (immersive, kinetic)
  - The Julie Zhuo School (narrative, case-study)
  - The Adrien Lamy School (bold typography)
  - The Olha Lazarieva School (refined craft)
  - The Clay Boan School (luxury-brand)
  - Each card: CSS-generated stylistic mockup at top (gradient fills and abstract shapes matching each school's aesthetic — no external images needed), name + description, and a **Design Decode** section (3-4 bullet points: what makes it work, techniques used, what to steal). Use placeholder decode content for initial implementation; final copy will be provided separately.
  - **Desktop:** The strip is a naturally overflowing horizontal container (`overflow-x: auto`) with CSS scroll-snap (`scroll-snap-type: x mandatory`, each card snaps). Subtle auto-scroll on first appearance, then user scrolls/drags. Not a pinned GSAP scroll — keep it simple and performant.
  - **Mobile (≤768px):** Cards stack vertically in a single column, full-width, no horizontal scroll. Design decodes are visible by default (no expand interaction needed on touch).
  - "Swipe to explore ←→" label (hidden on mobile)
- **Part 3 — CTA:** "Ready to build yours?" with "Open Claude Code →" button. Parametric curve underline.

### Section 8 — The Studio (Figma → Prototype)
- **Background:** Gradient from black back to warm pavilion colors (`#f0ebe2`)
- **Heading:** "From Figma to functional. In minutes, not weeks."
- **Interactive Demo:**
  - Left panel: "YOUR FIGMA TEMPLATE" — a simple landing page wireframe: top nav bar (logo + 3 links), hero section (headline placeholder + subtitle + CTA button), three feature cards in a row, and a footer bar. All rendered as abstract shapes (rectangles, lines) in neutral grays.
  - Brand toggle tabs below the template (ACME CO, BLOOM, NOVA)
  - Right panel: "LIVE PROTOTYPE" — the same wireframe structure transformed with the selected brand:
    - **ACME CO:** Primary `#1a1a2e`, accent `#e63946`, font-weight bold, headline "Bold Solutions for Bold Teams"
    - **BLOOM:** Primary `#2d5016`, accent `#f4a261`, softer border-radius (12px), headline "Grow Naturally"
    - **NOVA:** Primary `#0a0a0a`, accent `#00c8ff`, sharp edges (2px radius), headline "Launch Forward"
  - Clicking brand tabs transforms the right panel with CSS transitions (300ms ease, color + border-radius + typography changes)
  - "Via Figma MCP" label on the template side
  - **Mobile (≤768px):** Panels stack vertically (template on top, prototype below). Brand tabs become a horizontal scrollable row.
- **Three-step workflow below:**
  1. Connect Figma — "Figma MCP reads your templates directly"
  2. Apply branding — "Tell Claude the client's colors, copy, and style"
  3. Get a prototype — "Functional HTML/CSS you can adjust by prompting"

### Section 9 — If You Get Stuck
- **Background:** Clean white-warm
- Three help paths in cards: Ask Claude, Text Igor, Documentation
- Same content as current page, restyled

### Footer
- Motivational closing, CTA back to top
- Parametric curve as footer decoration

## Technical Approach

### Content Replacement
The existing "Your First Project" / app-preview section (with `[App Name]` placeholders) is fully replaced by The Reveal and The Studio sections. No content from that section needs to be preserved.

### What to Keep
- Single-file HTML architecture (no build tools, no frameworks)
- Google Fonts: Inter (update import to `wght@100;200;300;400;500;600;700;800`) and JetBrains Mono
- Intersection Observer for scroll-triggered animations
- Copy-to-clipboard functionality
- Terminal typewriter effect
- Mobile responsive breakpoints (768px, 480px)

### What to Change
- **Complete CSS rewrite:** Remove all dark theme variables, glassmorphism, neon colors. Replace with warm Pavilion palette.
- **Remove:** Lightsaber progress bar, mesh blob animations, grain overlay, conic gradient borders, magnetic cursor effect
- **Add:** Parametric SVG progress curve (left margin), ambient radial light system (scroll-responsive), parametric SVG atmospheric curves throughout
- **Add:** GSAP ScrollTrigger for the transition animation and kinetic typography in The Reveal (load from CDN)
- **Add:** Horizontal scroll strip with drag interaction for The Reveal
- **Add:** Interactive brand-toggle demo for The Studio section
- **Add:** Image element for Regina's portrait (placeholder until images provided)

### Animation Budget
- Setup zone: Minimal — fade-in on scroll, typewriter for terminals. Keep it calm.
- Transition: One dramatic moment — curves sweeping, background shifting. Worth the complexity.
- The Reveal: Kinetic type (3 lines staggered), horizontal scroll strip. Moderate complexity.
- The Studio: Brand toggle CSS transitions. Simple and performant.
- Ambient lights: CSS-only where possible (use `background-position` animated on scroll via JS).

### Dependencies
- GSAP 3.12.x + ScrollTrigger plugin (CDN, loaded with `defer`): `https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/gsap.min.js` and `https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/ScrollTrigger.min.js`. Used for: transition curve animation, kinetic type clip-reveals in The Reveal, and scroll-triggered fade-ins in setup zone.
- Google Fonts: Inter (100-800), JetBrains Mono (400, 500)
- No other external dependencies

### Accessibility
- Respect `prefers-reduced-motion`: disable GSAP animations, typewriter effect, and auto-scroll. Show all content statically.
- Horizontal scroll strip is keyboard-navigable with left/right arrow keys.
- Verify text contrast meets WCAG AA (4.5:1 for body text). Note: warm gold accent (`#c4a882`) on cream may need darkening for small text — use `#8a7e6b` for any text smaller than 18px on light backgrounds.
- All interactive elements (brand tabs, copy buttons, CTA) are focusable and have visible focus indicators.

## Images Required
- Regina's portrait photo(s) — to be provided by Igor
- Placement: Hero section (primary), possibly transition or CTA sections

## Figma MCP Integration Note
The interactive demo in The Studio section is a static mockup demonstrating the concept. Actual Figma MCP setup instructions should be included as a future enhancement or as part of the "what's next" flow once Regina has completed setup and is ready to connect her Figma account.

## Verification

1. Open `index.html` in a browser — page should load with warm Pavilion aesthetic
2. Scroll through setup steps — calm, functional, animations subtle
3. Hit the transition — dramatic shift from warm to dark
4. The Reveal section — kinetic type animates, horizontal strip scrolls
5. The Studio section — brand tabs toggle the prototype preview
6. Mobile responsive — check at 768px and 480px breakpoints
7. Copy-to-clipboard buttons work on all code blocks
8. Terminal typewriter animations trigger on scroll-into-view
9. Portrait placeholder visible in hero (will be replaced with actual photo)
