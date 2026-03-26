# Quality Checks — Weak Spot Detector & Recruiter Lens

Two sequential passes that run at different moments in the workflow:
1. **Weak Spot Detector** — runs *before* writing, surfaces story gaps from interview answers
2. **Recruiter Lens Pass** — runs *after* writing, reads the draft as a skeptical hiring manager

---

## Pass 1 — Weak Spot Detector

**When**: After Phase 2 of the interview, before writing begins.
**How**: Silently evaluate the collected inputs against each check below. Then surface only
the genuine gaps — don't flag things that are fine. Present as a brief, direct message before
Phase 3 (visual confirmation).

**Format**:
> "Before I start writing, a few gaps worth noting:
> - [Gap 1 + suggestion]
> - [Gap 2 + suggestion]
> Want to fill these in, or should I work with what we have?"

Give the user the option to fill gaps or proceed — never block writing on weak data.

### Checks

| Area | Flag if… | Suggested fix |
|---|---|---|
| **Hook** | No concrete tension, number, or specific stakes | Ask: "What's the one stat or moment that captures how bad the problem was?" |
| **Your role** | "We" used exclusively, no individual contribution clear | Ask: "What was specifically yours — what would have been different without you?" |
| **Problem discovery** | Problem stated but no explanation of how it was found | Ask: "How did you/the team first realize this was the problem to solve?" |
| **Research** | Research mentioned but no findings shared | Ask: "What did you learn that you didn't expect? What changed because of research?" |
| **Decision rationale** | Solution described but no design decisions explained | Ask: "What was the hardest call you made, and why did you make it?" |
| **Outcomes** | No metrics AND no qualitative signals | Ask: "Any proxy signals — support tickets, NPS comments, stakeholder reactions, adoption?" |
| **Reflection** | Missing entirely or only a platitude ("I learned a lot") | Ask: "What would you actually do differently, with hindsight?" |
| **Confidentiality gap** | Project is confidential but real company/product names used | Suggest anonymization patterns (see ux-sections.md → Confidentiality Patterns) |

---

## Pass 2 — Recruiter Lens Pass

**When**: After the full case study HTML is written, before delivering to user.
**How**: Re-read the draft silently wearing the hat of a skeptical senior recruiter who
has 90 seconds and has seen 200 portfolios this month. Then append a short "Recruiter Notes"
block at the end of your response — NOT inside the HTML file.

**Format**:
> **Recruiter Lens Review**
> - ✅ [What's working and why]
> - ⚠️ [Flag 1 — specific line or section + why it's weak + suggested fix]
> - ⚠️ [Flag 2 — etc.]

Keep it to 3–5 bullets max. Be direct. Don't sugarcoat, but don't pile on.

### What to flag

**Hidden individual contribution**
"We" appears throughout with no "I" moments. Recruiters assume the person wrote "we" to
hide that they were a minor contributor. Flag any section where the user's specific role
is unclear.

**Vague claims**
- "Improved the user experience" → flag, ask for specificity
- "Users found it easier to use" → flag, ask for a quote or metric
- "Stakeholders were pleased" → flag, replace with what they actually said or did

**Passive problem framing**
"I was tasked with..." or "The team was asked to..." buries agency. Recruiter reads this
as someone who executes orders, not someone who solves problems.

**Process section that drags**
If the Design Process section lists deliverables (sketches → wireframes → prototype → handoff)
without explaining a single decision, flag it. Deliverable lists are not process.

**Weak or missing hook**
If the first sentence of the hero section could describe any project at any company, it's
not a hook — it's a title. Flag it.

**Outcome section with no specifics**
"The product launched successfully" or "feedback was positive" with nothing else. Flag and
suggest the thin-data pattern from examples.md.

**Reflection that's too safe**
"I learned to communicate better with stakeholders" is a non-answer. If the reflection
doesn't name a real mistake or a genuine surprise, flag it.

**Jargon without context**
Tool names dropped without explanation ("I used FigJam for the affinity mapping") that
assume the reader knows the tool's relevance. Flag if jargon doesn't serve the story.
