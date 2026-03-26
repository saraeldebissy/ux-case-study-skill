---
name: ux-case-study
description: >
  Create polished, portfolio-ready UX/Product case studies as HTML output. Use this skill
  whenever a user wants to document a design project, write up a UX case study, turn project
  notes into a structured narrative, or create a portfolio piece. Trigger on phrases like
  "write a case study", "write a ux case study", "document my project", "help me tell the
  story of this design", "I need a portfolio write-up", "turn these notes into a case study",
  or any time a user shares raw project notes, transcripts, or briefs and wants them shaped
  into a professional case study. Also trigger when a user mentions building or updating their
  design portfolio, targeting a specific role, or job searching as a designer. Always use this
  skill even if the user just says "case study" or pastes messy project notes — don't try to
  wing it without reading this skill first.
---

# UX Case Study Skill

Produces portfolio-ready UX/Product case studies as styled HTML, targeting recruiters and
hiring managers. Supports two entry paths, adaptive questioning, portfolio strategy awareness,
quality checks, Visualizer-generated diagrams, and both full + teaser output formats.

---

## On First Trigger — Check Portfolio Context

Before starting, read `references/portfolio-strategy.md` and check:
- Is the user building/updating a portfolio or job searching? → invoke portfolio strategy
- Is this a second case study this session? → use cross-portfolio differentiation logic
- Otherwise → proceed directly to entry path detection

---

## Entry Path Detection

**Immediately determine which path applies:**

### Path A — Transform
User has provided raw material: notes, a transcript, bullet points, or an uploaded file.
→ Skip to [Transform Path](#transform-path)

### Path B — Interview
User has not provided content yet, or has only described the project vaguely.
→ Start [Interview Path](#interview-path)

---

## Interview Path

**Before starting, ask the user which mode they want:**

> "How do you want to work through this?
> - **Quick** — I'll ask everything at once, you answer in one go
> - **Guided** — I'll walk you through it one question at a time, like a planning session"

Wait for their answer, then proceed accordingly.

---

### Quick Mode

Run in **3 phases**. Each phase = one conversational message, not a bullet dump.
Group questions naturally. Wait for response before moving to the next phase.

### Phase 1 — Must-Have Inputs

**Project Identity**: name/title · your role · timeline · solo or team?

**The Problem**: what was broken and for whom · why it mattered · how it was discovered

**The Solution**: what was designed/shipped · what makes it smart or different

**Outcomes & Impact**: metrics if any · qualitative signals if no hard data · business impact

**Visuals Inventory**: assets you have · what's missing that could be generated

---

### Phase 2 — Adaptive Depth + Context

Always ask in Phase 2:
- **Confidentiality**: NDA-protected? → flag anonymization needs throughout; suggest
  alternatives inline (*"e.g. 'a B2B SaaS platform' instead of the client name"*)
- **Tone reference**: share a case study you admire (URL or description), or pick a mode:
  Narrative / Structured / Hybrid → read `references/tone-modes.md` before writing

Ask only if relevant:

| If… | Then ask about… |
|---|---|
| Research mentioned | Methods, key findings, how research changed direction |
| Multiple iterations | What got cut, pivot moments, tradeoffs made |
| Team project | How decisions were made, your specific contribution |
| Constraints were a factor | Tech limits, time pressure, stakeholder dynamics |
| Weak outcome data | Proxy signals, quotes, before/after comparisons |
| Portfolio context applies | Role target, seniority, what portfolio is missing → `references/portfolio-strategy.md` |
| User returning mid-session | Ask them to paste previous answers, continue from where they left off |

---

### Guided Mode

Ask one question at a time. After each answer, briefly reflect or acknowledge what you
heard before moving to the next — like a real planning conversation, not a form.

**Question sequence (adapt order based on flow):**

1. What's the project and what was your role in it?
2. What was broken or painful — who felt it, and why did it matter?
3. How did you discover that was the real problem to solve?
4. What did you ultimately design or ship?
5. What makes the solution smart — what's the insight baked into it?
6. Do you have results? Numbers, quotes, anything that shows it worked?
7. What assets do you have — screenshots, wireframes, recordings?
8. Is this project confidential or NDA-protected?
9. Share a case study you admire, or tell me: narrative and personal, or clean and structured?

After question 9 → run the **Weak Spot Detector** (Pass 1 from `references/quality-checks.md`)
before proceeding to visual confirmation and writing.

**Tone in Guided mode**: conversational, curious, encouraging. React to what they say.
If an answer is unexpectedly rich, follow up naturally before moving on. This should feel
like a portfolio review session — not an intake form.

---

### Phase 3 — Weak Spot Check + Visual Confirmation

**Step 1 — Weak Spot Detector**: Read `references/quality-checks.md` (Pass 1).
Silently evaluate collected inputs. Surface only real gaps in a brief message.
Give user the option to fill them or proceed.

**Step 2 — Visual plan**: Confirm what you'll generate vs. what needs `[INSERT]` placeholders.
Ask if anything to add or change.

Then proceed to writing.

---

## Transform Path

1. Read everything provided
2. Silently map to: Project Identity · Problem · Solution · Outcomes · Visuals
3. Ask one focused follow-up covering genuine gaps + always ask confidentiality and tone
4. Run Weak Spot Detector (Pass 1 from `references/quality-checks.md`) on mapped inputs
5. Proceed to writing

---

## Writing the Output

Read before drafting:
- `references/ux-sections.md` — section-by-section writing guide
- `references/html-template.md` — HTML structure and CSS
- `references/tone-modes.md` — apply the selected or inferred mode
- `references/examples.md` — use as quality benchmarks while writing

### Full Version Structure

1. **Hero** — title, role, timeline, company/client (or anonymized), 1–2 sentence hook
2. **The Challenge** — problem, who it affected, why it mattered, what had been tried
3. **Research & Discovery** — *(omit if not applicable)* methods, findings, the "aha"
4. **Design Process** — iterations, key decisions, tradeoffs, what got cut and why
5. **The Solution** — what shipped, core design decisions, what makes it work
6. **Outcomes & Impact** — metrics, qualitative signals, business value, what's unresolved
7. **Reflection** — what you'd do differently, what you learned, your personal highlight

### Visual Slots

- **Generate with Visualizer** for diagrams, flows, journey maps, charts
- **`[INSERT]` placeholder** for screenshots, real wireframes, confidential assets

### Visual Generation Guide

| Writing about… | Generate… |
|---|---|
| User research findings | Affinity map or insight cards |
| Multi-step user experience | User journey map |
| Before/after states | Side-by-side comparison diagram |
| Process/iterations | Design process flow |
| Metrics / improvement | Bar chart or stat visual |
| Information architecture | Sitemap or flow diagram |

### Output Format

Single self-contained `.html` file. Follow `references/html-template.md`.
Apply `frontend-design` skill for aesthetic direction — pick distinctive fonts and
override CSS variables to match the chosen tone mode.

---

## After Writing — Recruiter Lens Pass

Read `references/quality-checks.md` (Pass 2). Re-read the draft as a skeptical recruiter.
Append a **Recruiter Lens Review** block after your response (outside the HTML) with
3–5 direct flags: what's working, what's weak, suggested fixes.

---

## Teaser Extraction

After delivering the full version + recruiter notes, offer:

> "Want a teaser card? (~200 words, hero image slot, 3 impact highlights, CTA) — for your
> portfolio homepage grid."

If yes, extract from the full version without asking new questions:
- Hook (1 sentence)
- What you did (2–3 sentences)
- 3 impact bullets (metrics or qualitative wins)
- `[INSERT: Hero image]` slot
- CTA: `[View full case study →]`

Output as a separate HTML snippet for embedding as a portfolio card.

---

## Multi-Format Routing

If the user asks for additional formats after the HTML is done:
- **"I also want a PDF"** → hand off to the `pdf` skill, pass the HTML file as input
- **"Make this a deck / presentation"** → hand off to the `pptx` skill; suggest treating
  each case study section as a slide group
- Don't attempt both formats in the same pass — finish HTML first, then route

---

## Localization

If the user's writing is in a non-native language, or they ask for a language polish pass:
After writing, offer: *"Want me to do a light English polish pass? I'll keep your voice but
tighten phrasing and fix anything that reads as non-native."*
If yes, re-read and rewrite only the prose sections (not the HTML structure or CSS).

---

## Reference Files Index

| File | Read when… |
|---|---|
| `references/ux-sections.md` | Before writing — section writing guide |
| `references/html-template.md` | Before writing — HTML structure + CSS |
| `references/tone-modes.md` | After tone reference is given, before writing |
| `references/examples.md` | While writing — quality benchmarks |
| `references/quality-checks.md` | Pass 1: after interview · Pass 2: after writing |
| `references/portfolio-strategy.md` | If portfolio/job search context is present |
