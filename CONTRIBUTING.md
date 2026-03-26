# Contributing to UX Case Study Skill

Thanks for wanting to improve this. Contributions are welcome — whether it's a small wording fix, a new reference file, or a full example output.

---

## What's most useful to contribute

**Example outputs** — the best way to improve the skill is to show it more real cases. If you've used it to generate a case study you're happy with, add it to `examples/` with a note in the PR about what project type it is.

**Reference file improvements** — the files in `skill/references/` are where the writing quality lives. If you notice the skill producing weak hooks, thin reflections, or missing something in a particular section, the fix likely lives in `ux-sections.md` or `quality-checks.md`.

**New tone modes** — `tone-modes.md` currently has Narrative, Structured, and Hybrid. If you work in a domain where a different voice works better (academic, agency pitch, developer-focused), add a new mode with examples.

**Bug fixes** — if the skill is triggering when it shouldn't, or not triggering when it should, the fix is usually in the `description:` field of `SKILL.md`'s frontmatter.

---

## How to contribute

1. Fork the repo
2. Make your changes in the `skill/` folder
3. If you changed `SKILL.md` or any reference file, repackage the `.skill` file:
   ```bash
   zip -r ux-case-study.skill ux-case-study/
   ```
   Replace the existing `ux-case-study.skill` in the root with your new one.
4. Open a PR with a short description of what you changed and why

---

## Guidelines

- Keep `SKILL.md` under 500 lines — if you're adding logic, move the detail into a reference file
- Don't change the skill `name:` field in the frontmatter — it breaks installs for existing users
- Example outputs should be real projects (anonymised if needed), not synthetic demos
- If you're adding a new reference file, add a row for it in the Reference Files Index at the bottom of `SKILL.md`

---

## Questions

Open an issue — happy to discuss before you build something big.
