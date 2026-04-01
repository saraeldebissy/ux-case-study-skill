# HTML Template — UX Case Study

Output is a single self-contained `.html` file. White page, editorial typography, clean
section labels, full-width visuals, descriptive placeholders, and 3-column stat containers
with highlighted numbers.

Apply `frontend-design` skill for font selection. Avoid Inter/Roboto. Pick one distinctive
display font + one clean body font from Google Fonts.

---

## Design Principles (from reference site)

- **White background** — pure white, no off-whites or tinted surfaces
- **Section label** — small, uppercase, spaced, muted — sits above the heading like a tag
- **Headings** — large, display font, generous size
- **Body text** — clean, readable, generous line height, max ~65ch wide
- **Visuals** — full width, no card wrapper, just the image breathing on the page
- **Placeholders** — specific, not generic — describe exactly what goes here
- **Data/findings** — always 3 containers side by side, number large and highlighted
- **No decorative borders or shadows** — whitespace does the separation work

---

## Visual Slot Rules

**Rule 1 — Real asset exists**
User has a screenshot, wireframe, or image → render as full-width `<figure class="cs-visual">` with a caption.

**Rule 2 — Placeholder (user will insert)**
No asset yet → render `.cs-placeholder` with a specific label + hint describing exactly what goes there.
Never write "Insert image here" — always write what specifically should go here.

**Rule 3 — Diagram to create**
Visual doesn't exist but needs to be made → either generate with Visualizer inline,
OR render a `.cs-diagram-desc` block describing exactly what the diagram should show.

---

## Data / Findings Rule

Any time there are 3 data points, findings, or metrics → use `.cs-stats` (3-column grid).
Numbers go large in accent color. Label goes below in muted small text.
2 data points → use `.cs-stats--two`. 4+ → two rows of 2, or a prose list.

---

## Hero Metadata Rule

For each metadata field (Scope · Role · Duration · Year):
- **Stated or inferable from context** → use it
- **Not available** → render a muted placeholder so the user knows to fill it in:

```html
<div>
  <span class="cs-meta-label">Year</span>
  <span class="cs-meta-value" style="color:var(--light);">[Year]</span>
</div>
```

Never omit a field silently. Never guess with no basis. Always leave a visible signal.

---

## Base Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>[Project Name] — [Your Name]</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=DISPLAY_FONT&family=BODY_FONT&display=swap" rel="stylesheet" />

  <style>
    :root {
      --white:      #FFFFFF;
      --text:       #111111;
      --muted:      #888888;
      --light:      #AAAAAA;
      --border:     #E8E8E8;
      --surface:    #F5F5F5;
      --accent:     #111111;
      --font-d:     'DISPLAY_FONT', Georgia, serif;
      --font-b:     'BODY_FONT', system-ui, sans-serif;
      --max:        680px;
      --max-wide:   960px;
    }
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body {
      background: var(--white);
      color: var(--text);
      font-family: var(--font-b);
      font-size: 1.0625rem;
      line-height: 1.8;
      -webkit-font-smoothing: antialiased;
    }
    img, video { max-width: 100%; display: block; }
    a { color: var(--text); text-decoration: none; }

    /* NAV */
    .cs-nav {
      max-width: var(--max-wide);
      margin: 0 auto;
      padding: 1.5rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .cs-nav a { font-size: 0.875rem; color: var(--muted); }
    .cs-nav a:hover { color: var(--text); }

    /* HERO */
    .cs-hero {
      max-width: var(--max-wide);
      margin: 0 auto;
      padding: 4rem 2rem 3rem;
    }
    .cs-hero__title {
      font-family: var(--font-d);
      font-size: clamp(2rem, 5vw, 3.5rem);
      font-weight: 400;
      line-height: 1.15;
      letter-spacing: -0.01em;
      max-width: 22ch;
      margin-bottom: 2rem;
    }
    .cs-hero__eyebrow {
      display: flex;
      flex-wrap: wrap;
      gap: 2.5rem;
    }
    .cs-meta-label {
      font-size: 0.625rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--light);
      display: block;
      margin-bottom: 0.2rem;
    }
    .cs-meta-value {
      font-size: 0.875rem;
      color: var(--muted);
    }
    .cs-hero__title {
      font-family: var(--font-d);
      font-size: clamp(2rem, 5vw, 3.5rem);
      font-weight: 400;
      line-height: 1.15;
      letter-spacing: -0.01em;
      max-width: 22ch;
    }

    /* HERO IMAGE — full width */
    .cs-hero-image {
      max-width: var(--max-wide);
      margin: 3rem auto 0;
      padding: 0 2rem;
    }
    .cs-hero-image img { width: 100%; border-radius: 4px; }

    /* BODY CONTAINER */
    .cs-body {
      max-width: var(--max-wide);
      margin: 0 auto;
      padding: 0 2rem;
    }

    /* INTRO */
    .cs-intro {
      max-width: var(--max);
      padding: 3rem 0;
      border-bottom: 1px solid var(--border);
    }
    .cs-intro p { margin-bottom: 1.25rem; }
    .cs-intro p:last-child { margin-bottom: 0; }
    .cs-intro strong { font-weight: 600; }

    /* SECTIONS */
    .cs-section {
      padding: 4rem 0;
      border-bottom: 1px solid var(--border);
    }
    .cs-section:last-child { border-bottom: none; }

    /* Section label — small tag above heading */
    .cs-label {
      font-size: 0.625rem;
      font-weight: 600;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--light);
      display: block;
      margin-bottom: 0.75rem;
    }

    /* Section heading */
    .cs-title {
      font-family: var(--font-d);
      font-size: clamp(1.5rem, 3vw, 2.25rem);
      font-weight: 400;
      line-height: 1.2;
      margin-bottom: 1.75rem;
      max-width: 28ch;
    }

    /* Prose */
    .cs-prose { max-width: var(--max); }
    .cs-prose p { margin-bottom: 1.125rem; }
    .cs-prose p:last-child { margin-bottom: 0; }
    .cs-prose strong { font-weight: 600; }
    .cs-prose h3 {
      font-size: 1rem;
      font-weight: 600;
      margin: 2rem 0 0.5rem;
    }

    /* STATS — 3-column with highlighted numbers */
    .cs-stats {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1px;
      background: var(--border);
      border: 1px solid var(--border);
      border-radius: 4px;
      overflow: hidden;
      margin: 2.5rem 0;
    }
    .cs-stats--two { grid-template-columns: repeat(2, 1fr); }
    .cs-stat {
      background: var(--white);
      padding: 2rem 1.5rem;
    }
    .cs-stat__n {
      font-family: var(--font-d);
      font-size: 2.75rem;
      font-weight: 400;
      color: var(--accent);
      line-height: 1;
      margin-bottom: 0.5rem;
      letter-spacing: -0.02em;
    }
    .cs-stat__l {
      font-size: 0.875rem;
      color: var(--muted);
      line-height: 1.5;
    }

    /* FULL-WIDTH VISUAL */
    .cs-visual { margin: 2.5rem 0; }
    .cs-visual img, .cs-visual video { width: 100%; border-radius: 4px; }
    .cs-visual figcaption {
      margin-top: 0.625rem;
      font-size: 0.75rem;
      color: var(--light);
      letter-spacing: 0.02em;
    }

    /* PLACEHOLDER — specific, not generic */
    .cs-placeholder {
      background: var(--surface);
      border-radius: 4px;
      padding: 2.5rem;
      min-height: 200px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      gap: 0.375rem;
      margin: 2.5rem 0;
    }
    .cs-ph-tag {
      font-size: 0.625rem;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--light);
    }
    .cs-ph-title { font-size: 1rem; font-weight: 600; color: var(--muted); }
    .cs-ph-hint { font-size: 0.875rem; color: var(--light); }

    /* DIAGRAM DESCRIPTION BLOCK */
    .cs-diagram-desc {
      margin: 2.5rem 0;
      padding: 1.5rem 2rem;
      border-left: 2px solid var(--border);
      background: var(--surface);
      border-radius: 0 4px 4px 0;
    }
    .cs-dd-tag {
      font-size: 0.625rem;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--light);
      margin-bottom: 0.5rem;
    }
    .cs-dd-text { font-size: 0.9375rem; color: var(--muted); line-height: 1.65; }

    /* QUOTE */
    .cs-quote { margin: 2.5rem 0; max-width: var(--max); }
    .cs-quote p {
      font-family: var(--font-d);
      font-size: 1.375rem;
      font-style: italic;
      line-height: 1.5;
    }
    .cs-quote cite {
      display: block;
      margin-top: 0.75rem;
      font-size: 0.8125rem;
      color: var(--light);
      font-style: normal;
    }

    /* FOOTER */
    .cs-footer {
      max-width: var(--max-wide);
      margin: 0 auto;
      padding: 3rem 2rem;
      display: flex;
      justify-content: space-between;
      border-top: 1px solid var(--border);
      flex-wrap: wrap;
      gap: 1rem;
    }
    .cs-footer a { font-size: 0.875rem; color: var(--muted); }
    .cs-footer a:hover { color: var(--text); }

    @media (max-width: 640px) {
      .cs-stats, .cs-stats--two { grid-template-columns: 1fr; }
      .cs-hero__eyebrow { gap: 1.25rem; }
    }
  </style>
</head>
<body>

  <nav class="cs-nav">
    <a href="/">← Work</a>
  </nav>

  <header class="cs-hero">
    <!-- Optional: small company/client label above the title -->
    <!-- <span class="cs-meta-label" style="margin-bottom:1rem;display:block;">[Company × Project]</span> -->

    <h1 class="cs-hero__title">[Project title as a strong statement or question]</h1>

    <div class="cs-hero__eyebrow">
      <div>
        <span class="cs-meta-label">Scope</span>
        <span class="cs-meta-value">[UX · Research]</span>
      </div>
      <div>
        <span class="cs-meta-label">Role</span>
        <span class="cs-meta-value">[Your Role]</span>
      </div>
      <div>
        <span class="cs-meta-label">Duration</span>
        <span class="cs-meta-value">[Timeline]</span>
      </div>
      <div>
        <span class="cs-meta-label">Year</span>
        <span class="cs-meta-value">[Year]</span>
      </div>
    </div>
  </header>

  <div class="cs-hero-image">
    <div class="cs-placeholder">
      <span class="cs-ph-tag">Hero Image</span>
      <span class="cs-ph-title">[Final design, key screen, or cover visual]</span>
      <span class="cs-ph-hint">Wide crop — 1400×500px or similar aspect ratio</span>
    </div>
  </div>

  <div class="cs-body">

    <div class="cs-intro">
      <p>[Scene-setting paragraph — who the client is, what happened, why you were brought in.]</p>
      <p><strong>My role</strong><br>[Your specific contribution — one focused paragraph.]</p>
      <p><strong>Results</strong><br>[Lead with the headline outcome. Number first.]</p>
    </div>

    <!-- PROBLEM DEFINITION -->
    <section class="cs-section">
      <span class="cs-label">Problem Definition</span>
      <h2 class="cs-title">[Problem headline]</h2>
      <div class="cs-prose">
        <p>[Problem narrative — what was broken, who it affected, why it mattered.]</p>
      </div>

      <!-- 3-column stats for data points -->
      <div class="cs-stats">
        <div class="cs-stat">
          <div class="cs-stat__n">[X%]</div>
          <div class="cs-stat__l">[What this number means in plain language]</div>
        </div>
        <div class="cs-stat">
          <div class="cs-stat__n">[X%]</div>
          <div class="cs-stat__l">[What this number means]</div>
        </div>
        <div class="cs-stat">
          <div class="cs-stat__n">[X%]</div>
          <div class="cs-stat__l">[What this number means]</div>
        </div>
      </div>

      <figure class="cs-visual">
        <div class="cs-placeholder">
          <span class="cs-ph-tag">Analytics Screenshot</span>
          <span class="cs-ph-title">[Specific screenshot — e.g. GA sales funnel]</span>
          <span class="cs-ph-hint">Showing [what it reveals]</span>
        </div>
        <figcaption>[Caption — source + date]</figcaption>
      </figure>
    </section>

    <!-- DISCOVERY -->
    <section class="cs-section">
      <span class="cs-label">Discovery</span>
      <h2 class="cs-title">[Discovery headline]</h2>
      <div class="cs-prose">
        <p>[How you investigated — methods, tools, what you were looking for.]</p>
        <h3>[Sub-finding label]</h3>
        <p>[Specific finding and what it meant.]</p>
      </div>

      <div class="cs-stats">
        <div class="cs-stat">
          <div class="cs-stat__n">[X%]</div>
          <div class="cs-stat__l">[Finding in plain language]</div>
        </div>
        <div class="cs-stat">
          <div class="cs-stat__n">[X%]</div>
          <div class="cs-stat__l">[Finding in plain language]</div>
        </div>
        <div class="cs-stat">
          <div class="cs-stat__n">[X]</div>
          <div class="cs-stat__l">[Finding in plain language]</div>
        </div>
      </div>

      <figure class="cs-visual">
        <div class="cs-placeholder">
          <span class="cs-ph-tag">Research Visual</span>
          <span class="cs-ph-title">[Specific asset — e.g. Hotjar scroll map]</span>
          <span class="cs-ph-hint">Showing [specific behavior or finding]</span>
        </div>
        <figcaption>[Caption]</figcaption>
      </figure>
    </section>

    <!-- SOLUTION -->
    <section class="cs-section">
      <span class="cs-label">Solution</span>
      <h2 class="cs-title">[Solution headline]</h2>
      <div class="cs-prose">
        <p>[What you designed — lead with the insight, then the decisions.]</p>
      </div>

      <!-- Real wireframe if available, placeholder if not -->
      <figure class="cs-visual">
        <div class="cs-placeholder">
          <span class="cs-ph-tag">Wireframe</span>
          <span class="cs-ph-title">[Specific design artifact — e.g. redesigned onboarding flow]</span>
          <span class="cs-ph-hint">Lo-fi or hi-fi, full layout preferred</span>
        </div>
      </figure>

      <!-- If a diagram needs to be created — describe it, or generate with Visualizer -->
      <div class="cs-diagram-desc">
        <div class="cs-dd-tag">Diagram to create</div>
        <div class="cs-dd-text">
          [Describe exactly what the diagram should show — e.g. "Before/after layout comparison:
          left = original two-column with CTA buried, right = single column with CTA below form.
          Annotate the 3 key changes."]
        </div>
      </div>
    </section>

    <!-- RESULTS -->
    <section class="cs-section">
      <span class="cs-label">Results</span>
      <h2 class="cs-title">[Results headline]</h2>

      <div class="cs-stats">
        <div class="cs-stat">
          <div class="cs-stat__n">+[X%]</div>
          <div class="cs-stat__l">[What improved and over what timeframe]</div>
        </div>
        <div class="cs-stat">
          <div class="cs-stat__n">−[X%]</div>
          <div class="cs-stat__l">[What decreased and why that's good]</div>
        </div>
        <div class="cs-stat">
          <div class="cs-stat__n">[X]</div>
          <div class="cs-stat__l">[Third metric or timeframe]</div>
        </div>
      </div>

      <div class="cs-prose">
        <p>[Context behind the numbers — what changed downstream, business impact.]</p>
      </div>

      <figure class="cs-visual">
        <div class="cs-placeholder">
          <span class="cs-ph-tag">Results Screenshot</span>
          <span class="cs-ph-title">[Analytics showing the uplift]</span>
          <span class="cs-ph-hint">Before/after comparison preferred</span>
        </div>
      </figure>
    </section>

    <!-- REFLECTIONS -->
    <section class="cs-section">
      <span class="cs-label">Reflections</span>
      <h2 class="cs-title">[Reflection headline]</h2>
      <div class="cs-prose">
        <h3>[Learning 1]</h3>
        <p>[Specific, not generic. What this project changed about how you work.]</p>
        <h3>[Learning 2]</h3>
        <p>[What you'd do differently.]</p>
        <p>[Closing line — the one thing that stuck.]</p>
      </div>
    </section>

  </div>

  <footer class="cs-footer">
    <a href="/">← Back to work</a>
    <a href="#">Next project →</a>
  </footer>

</body>
</html>
```

---

## Component Quick Reference

| Situation | Component class |
|---|---|
| Real image / screenshot | `<figure class="cs-visual"><img /></figure>` |
| User will insert image | `<div class="cs-placeholder">` — be specific |
| Diagram to be created | `<div class="cs-diagram-desc">` — describe it |
| Visualizer output | Wrap in `<figure class="cs-visual">` |
| 3 data points / findings | `<div class="cs-stats">` |
| 2 data points | `<div class="cs-stats cs-stats--two">` |
| Pull quote | `<blockquote class="cs-quote">` |

## Stat number formatting
- Change metrics: always include sign → `+48%` / `−22%`
- Time: `2 wks` / `6 mo` / `3 days`
- Counts: `7` / `100K+` / `1.5M`
- Keep labels one line — short and plain

## Placeholder specificity rule
❌ Never: *"Insert image here"*
✅ Always: *"Hotjar scroll map showing where users dropped off during the sign-up flow"*
