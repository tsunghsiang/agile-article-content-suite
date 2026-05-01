---
name: agile-article-writer
description: >
  Use this skill whenever the user wants to generate a full article brief and Medium SEO package
  for a specific agile topic. Trigger when the user sends a message starting with
  "/agile-article-writer", or when they say: "write an article brief for", "generate an outline
  for", "create an article about [agile topic]", "write a brief for [topic]", or any request to
  turn a named agile topic into a structured article. Also triggers automatically when the user
  clicks the Generate button in the agile-topic-scout artifact — that button sends a pre-formatted
  message containing the topic title, context, and sources which this skill uses directly.
  This skill always produces TWO outputs in sequence: (1) a full 7-section article brief,
  and (2) a complete Medium SEO publishing package with title, subtitle, URL slug, 5 tags,
  and keyword notes.
---

# Agile Article Writer

## ⚠️ SKILL RESPONSIBILITY

This skill has ONE trigger and TWO outputs.

**Trigger:** A message containing a topic name — either typed by the user or sent automatically
by the agile-topic-scout artifact (which pre-fills the topic title, category, context, and
sources).

**Output 1 — Article Brief:** A full 7-section article brief in plain text.

**Output 2 — Medium SEO Package:** A complete Medium publishing package immediately below
the brief. This is not optional. Every run of this skill must produce both outputs.

---

## Step 1 — Parse the Input

When triggered, extract from the incoming message:
- `topic title` — the article subject
- `category` — e.g. Agile Leadership, Team Coaching (use if provided)
- `whyChosen` — research context from the scout (use if provided)
- `seniorManagerAngle` — executive hook from the scout (use if provided)
- `sources` — named sources from the scout (use if provided)
- `suggestedAngle` — headline seed from the scout (use if provided)

If some fields are missing (e.g. user typed the topic manually without scout context), do a
**single targeted web search** on the topic title to gather enough context to write confidently.
Do not run 12 searches — one focused search is sufficient since this skill's job is writing,
not research.

---

## Step 2 — Write the Article Brief

Produce the full brief using exactly this structure. Do not skip any section.

```
### Article Brief: [Topic Title]

**Headline:** [≤12 words — punchy, specific, front-loads the primary keyword]
**Subtitle:** [One sentence — who it's for and what they will concretely learn]
**Target Reader:** [Specific role: e.g. VP Engineering, CHRO, Head of Agile Practice]
**Estimated read:** ~X min

---

**Core Argument:**
[1–2 sentences — the single central thesis in plain, direct language]

---

**Outline:**
1. Opening hook — [a surprising stat, counterintuitive claim, or scene-setting scenario]
2. Context — [why this matters right now, what changed recently]
3. The problem — [the specific tension or gap the target reader faces]
4. Unique insight — [a reframe, framework, or unconventional take the reader hasn't seen]
5. Evidence — [real-world example, case study, or data point that proves the insight]
6. Action — [3 concrete things the reader can do differently starting this week]
7. Close — [a forward-looking challenge or call to action that creates urgency]

---

**Key Data Points:**
- [Stat or finding 1 — Source name, year]
- [Stat or finding 2 — Source name, year]
- [Stat or finding 3 — Source name, year]

---

**Senior Manager Call to Action:**
[One sentence: the single most important thing the reader should do or decide after reading]
```

---

## Step 3 — Write the Medium SEO Package

Immediately after the brief, output the following block. Do not skip it.
Count characters explicitly for title and subtitle — do not estimate.

```
---
### 📝 Medium Publishing Package

**Title**
[Exact text to paste into Medium's title field]
↳ Rules: 50–60 characters; primary keyword in first 4 words; reads as a natural headline
↳ Character count: [N] — confirm ≤60

**Subtitle**
[Exact text to paste into Medium's subtitle field]
↳ Rules: 120–155 characters; one sentence; expands the title promise; includes 1–2
  secondary keywords; gives a human a specific reason to click
↳ Character count: [N] — confirm ≤155

**URL slug**
[the-exact-slug-to-set-before-publishing]
↳ Rules: 4–7 words; lowercase; hyphens only; no stop words (a, the, and, of, in, to);
  primary keyword as close to the start as possible

**Tags** (paste in this order for best distribution)
1. [Most specific subject tag]
2. [Target reader's professional identity tag]
3. [Trending or high-volume Medium tag for this domain]
4. [Methodology or framework tag if relevant]
5. [Broad discovery tag]

**Tag rationale:**
[2 sentences explaining why this tag combination maximises both Medium feed distribution
and Google search discovery for this specific topic and audience.]

**SEO notes**
- Primary keyword: [exact 2–4 word phrase]
- Secondary keywords: [list 2–3]
- Canonical URL: [one sentence — whether to set one and when]
- Cross-posting tip: [one sentence specific to this topic]
---
```

---

## Character Counting Protocol

Before writing the final title and subtitle, draft them, count every character including
spaces and punctuation, then adjust if over limit. Show the count explicitly in the output.

Example of correct output:
```
**Title**
Agile Leadership Is Failing. Here's the Fix.
↳ Character count: 44 — confirm ≤60 ✓
```

Example of incorrect output:
```
**Title**
Agile Leadership Is Failing. Here's the Fix.
↳ Character count: approximately 45
```

The count must be exact. Never use "approximately".

---

## Keyword Selection Rules

**Primary keyword** — the 2–4 word phrase the target reader would type into Google when
looking for this specific content. Prefer phrases with professional or commercial intent.
Good: "agile leadership skills 2026" / "psychological safety agile teams"
Avoid: "agile" alone, generic terms like "leadership tips"

**Secondary keywords** — 2–3 related phrases that appear naturally in the subtitle. One per
sentence maximum. Do not stuff.

**Plain language over jargon** — prefer "agile team performance" over "evidence-based agile
velocity correlation" unless the target reader is a deep practitioner.

---

## Tag Selection Rules

Choose tags in this priority order:
1. Most specific subject tag matching the article's core topic
   (e.g. "Agile Coaching" not just "Agile")
2. Target reader's professional identity
   (e.g. "Leadership", "Product Management", "Software Engineering")
3. Trending or high-volume Medium tag in this domain
   (e.g. "Artificial Intelligence", "Future Of Work", "Remote Work")
4. Methodology or framework if relevant
   (e.g. "Scrum", "SAFe", "OKRs", "Design Thinking")
5. Broad discovery tag
   (e.g. "Business", "Technology", "Productivity", "Management")

---

## Quality Standards

- Both outputs (brief + SEO package) must appear in every response — no exceptions
- Character counts must be exact — compute them, do not estimate
- Sources cited in Key Data Points must come from real search results or scout context
  Use "N/A" if unavailable — never fabricate
- The article brief outline must contain all 7 sections — do not collapse or skip any
- The tone of the brief should match the target reader:
  - C-suite / senior managers → direct, business-outcome focused, low jargon
  - Practitioners → more specific, framework-aware, evidence-heavy
- Never output an artifact or interactive widget — plain structured text only

---

## Step 7 — Handoff to Post Writer

After the Medium SEO package, always append this exact handoff block.
This gives the user a one-click way to trigger the agile-post-writer skill.

```
---
### ✍️ Ready to write the full Medium post?

Reply with:

/agile-post-writer

And I will write the complete publish-ready article in your Medium voice and style,
using the brief and SEO package above as the source.
```
