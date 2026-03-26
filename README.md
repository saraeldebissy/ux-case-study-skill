# UX Case Study Skill

A Claude skill that turns your project notes, raw transcripts, or Behance/portfolio links into polished, portfolio-ready UX case studies — as styled HTML you can drop straight into your website.

Created by **Sara Khalil** · MIT License

---

## What it does

- **Interviews you** about your project (Quick mode or guided one-question-at-a-time)
- **Transforms raw content** — paste notes, a URL, or upload screenshots
- **Writes a full narrative** in your voice, targeting recruiters and hiring managers
- **Generates diagrams inline** — user journey maps, before/after flows, funnel charts, persona grids
- **Flags weak spots** before writing and runs a recruiter lens check after
- **Extracts a teaser card** for your portfolio homepage grid

**Output**: a single self-contained `.html` file, portfolio-ready, with CSS variables for easy theming.

---

## Example output

→ [UTurn Checkout Redesign](examples/uturn-case-study.html) — checkout CRO, +255% conversion

---

## Install

1. Download [`ux-case-study.skill`](ux-case-study.skill)
2. Open Claude.ai → go to your Project settings
3. Find **Skills** → click **Add Skill** or drag-and-drop the file
4. Done — Claude will now use this skill whenever you ask for a UX case study

---

## How to trigger it

Say any of these:

- `"Write a UX case study for my [project name]"`
- `"Help me document this design project"`
- `"Turn these notes into a portfolio case study"`
- `"I need a write-up for my portfolio"`

Or paste raw notes / a URL and Claude will detect the transform path automatically.

---

## Skill structure

```
skill/
├── SKILL.md                   ← core workflow (245 lines)
└── references/
    ├── ux-sections.md         ← section-by-section writing guide
    ├── html-template.md       ← base HTML + CSS template
    ├── tone-modes.md          ← Narrative / Structured / Hybrid modes
    ├── examples.md            ← narrative benchmark patterns
    ├── quality-checks.md      ← weak spot detector + recruiter lens
    └── portfolio-strategy.md  ← cross-portfolio differentiation logic
```

`SKILL.md` is always loaded when the skill triggers. Reference files are loaded on demand — only when Claude needs them for that specific task.

---

## Interview modes

When you don't have content yet, the skill offers two paths:

**Quick** — Claude asks all the must-have questions in one message. You answer once, it writes.

**Guided** — Claude asks one question at a time, reacts to your answers, and builds the brief conversationally. Feels like a portfolio review session.

---

## Output modes

**Full case study** — complete HTML with all sections: Hero · Challenge · Research · Process · Solution · Outcomes · Reflection

**Teaser card** — ~200 word summary card with 3 impact stats and a CTA, for your portfolio homepage grid. Offered automatically after the full version is delivered.

---

## Supported input sources

| Source | Works? | Notes |
|---|---|---|
| Raw notes / bullet points | ✅ | Paste directly |
| Uploaded screenshots | ✅ | Upload slide images |
| Personal portfolio URLs | ✅ | e.g. sarakhalil.me/work/project |
| Behance links | ⚠️ | Behance requires login — upload screenshots instead |
| PDFs / docs | ✅ | Upload the file |
| Interview transcripts | ✅ | Paste as text |

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) — improvements, new reference files, and example outputs are all welcome.

---

## License

MIT — use it, fork it, build on it. Keep the credit. See [LICENSE](LICENSE).
