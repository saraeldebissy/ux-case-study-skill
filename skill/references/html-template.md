# HTML Template — UX Case Study

This is the base HTML structure and CSS for outputting a case study. Read this before writing
the final HTML. The output should be a single self-contained `.html` file.

Apply the `frontend-design` skill for aesthetic direction — choose a distinctive typographic
and color palette that fits the user's tone reference. The CSS variables below are the
theming layer; override them to match the chosen aesthetic.

---

## File Structure

The output is ONE file: `[project-name]-case-study.html`

```
<head>         → meta, Google Fonts import, all CSS
<body>
  <nav>        → sticky top bar with project title + back link
  <article>
    <header>   → hero section
    <main>
      <section> × N   → one per case study section
    </main>
  </article>
  <footer>     → next/prev project nav + back to portfolio CTA
</body>
```

---

## Base Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>[Project Name] — Case Study</title>

  <!-- Replace with chosen fonts from Google Fonts. Avoid Inter/Roboto/Arial. -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=DISPLAY_FONT&family=BODY_FONT&display=swap" rel="stylesheet" />

  <style>
    /* ─── THEME TOKENS ─────────────────────────────────────────── */
    :root {
      --bg:           #FAFAF8;        /* page background */
      --surface:      #F2F0EC;        /* card / section bg */
      --border:       #E0DDD7;        /* dividers */
      --text:         #1A1A18;        /* primary text */
      --text-muted:   #6B6860;        /* captions, meta */
      --accent:       #2A4EFF;        /* links, highlights */
      --accent-soft:  #EEF1FF;        /* accent tint bg */

      --font-display: 'DISPLAY_FONT', serif;
      --font-body:    'BODY_FONT', sans-serif;

      --max-w:        760px;
      --max-w-wide:   1040px;

      --space-xs:     0.5rem;
      --space-sm:     1rem;
      --space-md:     2rem;
      --space-lg:     4rem;
      --space-xl:     7rem;
    }

    /* ─── RESET ─────────────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-body);
      font-size: 1.0625rem;
      line-height: 1.75;
      -webkit-font-smoothing: antialiased;
    }
    img { max-width: 100%; display: block; }
    a { color: var(--accent); text-decoration: none; }
    a:hover { text-decoration: underline; }

    /* ─── NAV ────────────────────────────────────────────────────── */
    .cs-nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: color-mix(in srgb, var(--bg) 85%, transparent);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      padding: var(--space-xs) var(--space-md);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: var(--space-md);
    }
    .cs-nav__back {
      font-size: 0.875rem;
      color: var(--text-muted);
      display: flex;
      align-items: center;
      gap: 0.375rem;
    }
    .cs-nav__back::before { content: '←'; }
    .cs-nav__title {
      font-family: var(--font-display);
      font-size: 0.9375rem;
      font-weight: 600;
      color: var(--text);
      opacity: 0;
      transition: opacity 0.2s;
    }
    .cs-nav__title.visible { opacity: 1; }

    /* ─── HERO ───────────────────────────────────────────────────── */
    .cs-hero {
      max-width: var(--max-w-wide);
      margin: 0 auto;
      padding: var(--space-xl) var(--space-md) var(--space-lg);
    }
    .cs-hero__meta {
      display: flex;
      flex-wrap: wrap;
      gap: var(--space-xs);
      margin-bottom: var(--space-md);
    }
    .cs-tag {
      font-size: 0.8125rem;
      font-weight: 500;
      letter-spacing: 0.03em;
      padding: 0.25rem 0.75rem;
      border-radius: 999px;
      background: var(--surface);
      border: 1px solid var(--border);
      color: var(--text-muted);
    }
    .cs-hero__title {
      font-family: var(--font-display);
      font-size: clamp(2.25rem, 5vw, 4rem);
      line-height: 1.1;
      letter-spacing: -0.02em;
      color: var(--text);
      margin-bottom: var(--space-md);
      max-width: 18ch;
    }
    .cs-hero__hook {
      font-size: 1.1875rem;
      color: var(--text-muted);
      max-width: 56ch;
      line-height: 1.6;
    }

    /* Hero image placeholder */
    .cs-hero__image {
      margin-top: var(--space-lg);
      width: 100%;
      aspect-ratio: 16 / 7;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      overflow: hidden;
    }

    /* ─── ARTICLE LAYOUT ─────────────────────────────────────────── */
    article {
      max-width: var(--max-w-wide);
      margin: 0 auto;
      padding: 0 var(--space-md);
    }
    main {
      display: grid;
      grid-template-columns: 1fr min(var(--max-w), 100%) 1fr;
    }
    main > * { grid-column: 2; }
    main > .cs-full-bleed { grid-column: 1 / -1; }

    /* ─── SECTIONS ───────────────────────────────────────────────── */
    .cs-section {
      padding: var(--space-lg) 0;
      border-top: 1px solid var(--border);
    }
    .cs-section:first-child { border-top: none; }

    .cs-section__label {
      font-size: 0.75rem;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: var(--space-sm);
    }
    .cs-section__title {
      font-family: var(--font-display);
      font-size: clamp(1.5rem, 3vw, 2.25rem);
      line-height: 1.2;
      letter-spacing: -0.01em;
      margin-bottom: var(--space-md);
      color: var(--text);
    }

    /* Body prose */
    .cs-prose p           { margin-bottom: var(--space-sm); }
    .cs-prose p:last-child { margin-bottom: 0; }
    .cs-prose strong      { font-weight: 600; color: var(--text); }

    /* ─── BLOCKQUOTE ─────────────────────────────────────────────── */
    .cs-quote {
      margin: var(--space-md) 0;
      padding: var(--space-md) var(--space-md) var(--space-md) calc(var(--space-md) + 4px);
      border-left: 4px solid var(--accent);
      background: var(--accent-soft);
      border-radius: 0 8px 8px 0;
    }
    .cs-quote p {
      font-family: var(--font-display);
      font-size: 1.125rem;
      line-height: 1.55;
      color: var(--text);
    }
    .cs-quote cite {
      display: block;
      margin-top: var(--space-xs);
      font-size: 0.875rem;
      color: var(--text-muted);
      font-style: normal;
    }

    /* ─── STAT CARDS ─────────────────────────────────────────────── */
    .cs-stats {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
      gap: var(--space-sm);
      margin: var(--space-md) 0;
    }
    .cs-stat {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: var(--space-md);
    }
    .cs-stat__value {
      font-family: var(--font-display);
      font-size: 2.25rem;
      font-weight: 700;
      color: var(--accent);
      line-height: 1;
      margin-bottom: var(--space-xs);
    }
    .cs-stat__label {
      font-size: 0.875rem;
      color: var(--text-muted);
      line-height: 1.4;
    }

    /* ─── VISUAL INSERT PLACEHOLDER ──────────────────────────────── */
    .cs-insert {
      margin: var(--space-md) 0;
      width: 100%;
      min-height: 280px;
      background: var(--surface);
      border: 2px dashed var(--border);
      border-radius: 10px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: var(--space-xs);
      padding: var(--space-md);
      text-align: center;
      color: var(--text-muted);
    }
    .cs-insert__icon  { font-size: 2rem; opacity: 0.4; }
    .cs-insert__label { font-size: 0.9375rem; font-weight: 500; }
    .cs-insert__hint  { font-size: 0.8125rem; opacity: 0.7; }

    /* Wide inserts (full bleed within article) */
    .cs-insert--wide {
      min-height: 360px;
    }

    /* ─── VISUALIZER EMBED ───────────────────────────────────────── */
    /* Wrapper for Visualizer-generated inline diagrams */
    .cs-visual {
      margin: var(--space-md) 0;
      border-radius: 10px;
      overflow: hidden;
      border: 1px solid var(--border);
    }

    /* ─── FOOTER ─────────────────────────────────────────────────── */
    .cs-footer {
      margin-top: var(--space-xl);
      padding: var(--space-lg) var(--space-md);
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: var(--space-md);
      flex-wrap: wrap;
      max-width: var(--max-w-wide);
      margin-inline: auto;
    }
    .cs-footer__cta {
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      padding: 0.75rem 1.5rem;
      background: var(--accent);
      color: #fff;
      border-radius: 8px;
      font-weight: 600;
      font-size: 0.9375rem;
      transition: opacity 0.15s;
    }
    .cs-footer__cta:hover { opacity: 0.85; text-decoration: none; }

    /* ─── RESPONSIVE ─────────────────────────────────────────────── */
    @media (max-width: 640px) {
      .cs-hero { padding-top: var(--space-lg); }
      .cs-stats { grid-template-columns: 1fr 1fr; }
      .cs-footer { flex-direction: column; align-items: flex-start; }
    }
  </style>
</head>

<body>

  <!-- NAV -->
  <nav class="cs-nav">
    <a href="/" class="cs-nav__back">Portfolio</a>
    <span class="cs-nav__title">[Project Name]</span>
  </nav>

  <article>

    <!-- HERO -->
    <header class="cs-hero">
      <div class="cs-hero__meta">
        <span class="cs-tag">[Role]</span>
        <span class="cs-tag">[Timeline]</span>
        <span class="cs-tag">[Company / Anonymized]</span>
      </div>
      <h1 class="cs-hero__title">[Project Title]</h1>
      <p class="cs-hero__hook">[1–2 sentence hook — the core tension or headline result]</p>

      <!-- Replace with actual hero image or generated visual -->
      <div class="cs-insert cs-hero__image">
        <span class="cs-insert__icon">🖼</span>
        <span class="cs-insert__label">Hero Image</span>
        <span class="cs-insert__hint">Final design, key screen, or cover visual</span>
      </div>
    </header>

    <main>

      <!-- SECTION: THE CHALLENGE -->
      <section class="cs-section">
        <p class="cs-section__label">Challenge</p>
        <h2 class="cs-section__title">[Challenge headline]</h2>
        <div class="cs-prose">
          <p>[Problem description — who was affected, what was at stake]</p>
          <p>[Discovery — how the problem was found]</p>
          <p>[Constraints or context that shaped the starting point]</p>
        </div>

        <!-- Visualizer OR insert — e.g. problem diagram, analytics drop-off -->
        <div class="cs-insert">
          <span class="cs-insert__icon">📊</span>
          <span class="cs-insert__label">Problem evidence</span>
          <span class="cs-insert__hint">Analytics screenshot, before state, or data visual</span>
        </div>
      </section>

      <!-- SECTION: RESEARCH & DISCOVERY (omit if not applicable) -->
      <section class="cs-section">
        <p class="cs-section__label">Research & Discovery</p>
        <h2 class="cs-section__title">[Research headline]</h2>
        <div class="cs-prose">
          <p>[Methods used + sample size]</p>
          <p>[2–3 key findings]</p>
          <p>[The "aha" insight that changed direction]</p>
        </div>

        <!-- Visualizer: user journey map, affinity clusters, insight cards -->
        <div class="cs-visual">
          <!-- VISUALIZER OUTPUT GOES HERE -->
        </div>
      </section>

      <!-- SECTION: DESIGN PROCESS -->
      <section class="cs-section">
        <p class="cs-section__label">Design Process</p>
        <h2 class="cs-section__title">[Process headline]</h2>
        <div class="cs-prose">
          <p>[How many iterations, key pivots]</p>
          <p>[Key decision moment: options → choice → why]</p>
          <p>[What got cut and why]</p>
        </div>

        <!-- Visualizer: process flow OR insert for wireframes -->
        <div class="cs-visual">
          <!-- VISUALIZER OUTPUT GOES HERE -->
        </div>

        <div class="cs-insert">
          <span class="cs-insert__icon">✏️</span>
          <span class="cs-insert__label">Wireframes / Iterations</span>
          <span class="cs-insert__hint">Early explorations, sketches, or prototype screenshots</span>
        </div>
      </section>

      <!-- SECTION: THE SOLUTION -->
      <section class="cs-section">
        <p class="cs-section__label">Solution</p>
        <h2 class="cs-section__title">[Solution headline]</h2>
        <div class="cs-prose">
          <p>[What was shipped — scope it clearly]</p>
          <p>[Core decision 1: what → why → what it solves]</p>
          <p>[Core decision 2: what → why → what it solves]</p>
        </div>

        <div class="cs-insert cs-insert--wide">
          <span class="cs-insert__icon">🎨</span>
          <span class="cs-insert__label">Final Design</span>
          <span class="cs-insert__hint">Key screens, prototype recording, or annotated mockups</span>
        </div>
      </section>

      <!-- SECTION: OUTCOMES & IMPACT -->
      <section class="cs-section">
        <p class="cs-section__label">Outcomes</p>
        <h2 class="cs-section__title">[Outcomes headline]</h2>

        <!-- Stat cards — populate from actual metrics; remove if no data -->
        <div class="cs-stats">
          <div class="cs-stat">
            <div class="cs-stat__value">[+X%]</div>
            <div class="cs-stat__label">[Metric name]</div>
          </div>
          <div class="cs-stat">
            <div class="cs-stat__value">[−X%]</div>
            <div class="cs-stat__label">[Metric name]</div>
          </div>
          <div class="cs-stat">
            <div class="cs-stat__value">[Xmo]</div>
            <div class="cs-stat__label">[Metric name]</div>
          </div>
        </div>

        <div class="cs-prose">
          <p>[Business impact + context]</p>
          <p>[What's unresolved or still being tracked]</p>
        </div>

        <!-- User quote if available -->
        <blockquote class="cs-quote">
          <p>"[User or stakeholder quote]"</p>
          <cite>— [Name or role], [Company or context]</cite>
        </blockquote>

        <!-- Visualizer: before/after chart or metric visual -->
        <div class="cs-visual">
          <!-- VISUALIZER OUTPUT GOES HERE -->
        </div>
      </section>

      <!-- SECTION: REFLECTION -->
      <section class="cs-section">
        <p class="cs-section__label">Reflection</p>
        <h2 class="cs-section__title">[Reflection headline]</h2>
        <div class="cs-prose">
          <p>[What you'd do differently]</p>
          <p>[What you learned]</p>
          <p>[Personal highlight / contribution you're proudest of]</p>
          <p>[What's next for this product area]</p>
        </div>
      </section>

    </main>
  </article>

  <!-- FOOTER -->
  <footer class="cs-footer">
    <div>
      <p style="font-size:0.875rem; color:var(--text-muted);">Next project</p>
      <a href="#" style="font-weight:600; font-size:1.0625rem;">[Next Project Name] →</a>
    </div>
    <a href="/" class="cs-footer__cta">← Back to Portfolio</a>
  </footer>

  <script>
    // Fade in nav title on scroll
    const navTitle = document.querySelector('.cs-nav__title');
    const hero = document.querySelector('.cs-hero__title');
    if (navTitle && hero) {
      const obs = new IntersectionObserver(
        ([e]) => navTitle.classList.toggle('visible', !e.isIntersecting),
        { threshold: 0 }
      );
      obs.observe(hero);
    }
  </script>

</body>
</html>
```

---

## Usage Notes

### Fonts
Pick two from Google Fonts that fit the tone. Examples:
- Editorial/refined: `Playfair Display` (display) + `DM Sans` (body)
- Modern/minimal: `Syne` (display) + `Instrument Sans` (body)
- Bold/expressive: `Fraunces` (display) + `Plus Jakarta Sans` (body)
- Technical: `Space Grotesk` is overused — try `IBM Plex Serif` + `Figtree` instead

### CSS Variables
Override just the `:root` variables to fully retheme. The whole design adapts.
Dark theme: flip `--bg: #0F0F0D`, `--surface: #1A1A18`, `--text: #F0EDE8`.

### Stat Cards
If there are no hard metrics, replace `.cs-stats` with a qualitative highlights list:
```html
<ul class="cs-highlights">
  <li>[Qualitative signal 1]</li>
  <li>[Qualitative signal 2]</li>
</ul>
```

### Visualizer Placement
Drop Visualizer output inside `.cs-visual` divs. The border-radius and border are
already applied — the visual will slot in cleanly.

### INSERT Placeholders
Every `<div class="cs-insert">` is a placeholder. Replace with:
```html
<figure>
  <img src="your-image.png" alt="Description" />
  <figcaption>Caption text</figcaption>
</figure>
```

### Removing Optional Sections
Research & Discovery is wrapped in its own `<section>` — delete it entirely if not applicable.
Stat cards block can be removed and replaced with prose if no metrics exist.
