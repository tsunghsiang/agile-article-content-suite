---
name: agile-illustration-generator
description: >
  Use this skill whenever the user wants to generate illustrations or visual assets for a
  completed Medium article, especially one produced by agile-post-writer. Trigger when the
  user says: "add illustrations to my post", "generate images for this article",
  "create visuals for my Medium post", "make illustrations for this", "I need images for
  this article", or any request to visually enhance a written Medium post with diagrams,
  cover art, or inline graphics. Also triggers automatically when the user types
  /agile-illustration-generator after agile-post-writer output. This skill always produces:
  (1) one click-optimised featured/preview image, and (2) 2–4 inline illustrations placed
  at strategic reading-rhythm points throughout the article. All visuals are delivered as
  rendered SVG/HTML artifacts the user can screenshot and upload directly to Medium.
---

# Agile Illustration Generator

## ⚠️ SKILL RESPONSIBILITY — READ FIRST

This skill has ONE job: produce publication-ready visual assets for a Medium agile article.

**Trigger:** A completed Medium post (from agile-post-writer or typed by the user) plus any
explicit request to illustrate it.

**Output 1 — Featured / Preview Image:** One high-impact cover image optimised for
click-through rate when used as Medium's story preview.

**Output 2 — Inline Illustrations:** 2–4 contextual diagrams or concept visuals, each
placed after a specific paragraph in the article. Quantity is driven by article length and
rhythm — never pad, never cut a section that genuinely needs a visual.

**Format:** Every illustration is rendered as a live SVG or HTML widget via `show_widget`.
The user screenshots each rendered output and uploads it to Medium. Claude always states
the recommended placement (section heading + first words of the target paragraph) after
each illustration.

---

## Research Foundation — Why These Decisions

The illustration rules in this skill are grounded in the following findings:

### Featured Image / Preview CTR Research
- Articles with images receive **94% more views** than text-only articles on Medium
  (Better Marketing / Medium internal data)
- **Human faces with expressive emotions** boost engagement by up to **35%**; the brain
  processes faces 60,000× faster than text — but for agile/B2B audiences, abstract or
  metaphorical visuals often outperform literal faces
- **Rule of Three**: limit to 3 primary visual elements — one dominant subject, one
  supporting object, one short text (≤5 words). More than 3 elements reads as noise
- **Curiosity gap principle** (Loewenstein): tease the insight without revealing the answer.
  The image should pose a visual question; the article title answers it
- **Color contrast and brightness** drive scroll-stops: warm colours (amber, coral, red)
  signal urgency/importance; cool colours (teal, blue) signal authority/calm
- **Z-pattern layout**: place the primary emotional or conceptual hook in the top-left
  quadrant — eye tracking shows 40% of thumbnail clicks originate there
- **Medium preview crop**: Medium auto-crops featured images to approximately a 16:9
  landscape box. Keep all essential content in the **centre 60% of the canvas** to survive
  any crop. A safe zone of 1:1 ratio in the image centre protects core information across
  all Medium surfaces (feed, homepage, search, Twitter share)
- **Flat minimalist designs perform poorly in 2026** — prefer layered visual depth with a
  clear foreground, midground, and background

### Inline Illustration Research
- Inline images break cognitive load and signal to the reader that the article rewards
  sustained attention — they are a pacing tool, not decoration
- The optimal placement cadence is **one visual every 300–400 words**, after a section that
  introduces a new concept, framework, or turning point
- Keep inline illustrations **conceptually simple**: 2–3 primary elements maximum
- **Wide landscape (16:9) or square (1:1)** work best across Medium desktop and mobile
- Use **captions** — they are read ~300% more often than body copy and are a second hook
  for skimming readers

### Medium Technical Specs (as of 2025–2026)
- **Featured image**: 1600 × 900 px (16:9); minimum 1200 × 675 px
- **Inline images**: 1600 px wide target; PNG for diagrams/charts, JPG for photo-style
- **File size**: under 1 MB per image
- **Safe core zone for preview crops**: centre 1:1 area of any featured image
- Set focal point using **Shift+F** in Medium editor, then **Alt/Opt + click** to fine-tune

---

## Step 1 — Parse the Article

Extract from the incoming message:
- `headline` — the article title
- `sections` — list of H2 section names and their opening sentences
- `core argument` — central thesis
- `target reader` — who the article is for (practitioner vs executive)
- `opening mode` — Coaching Story (Mode A) or Provocation (Mode B)
- `key data points` — any stats mentioned in the article
- `tone` — the emotional register (challenging, reflective, urgent, practical)

If the full article is not present, ask the user to paste it. Do not proceed without
the article text — illustrations must be anchored to specific content.

---

## Step 2 — Plan the Illustration Set

Before generating anything, produce a short **Illustration Plan** in plain text:

```
### Illustration Plan

**Featured Image concept:**
[One sentence describing the visual metaphor, dominant element, colour palette, and the
curiosity gap it creates. Explain WHY this hooks the target reader.]

**Inline illustration 1 — after section "[Section Name]":**
[Concept + type: diagram / metaphor / framework / data visual]
[Why this placement: what cognitive load does it relieve?]

**Inline illustration 2 — after section "[Section Name]":**
[Concept + type]
[Why this placement]

[Inline illustration 3 — optional, if article ≥ 1,400 words]
[Concept + type]
[Why this placement]

[Inline illustration 4 — optional, if article ≥ 1,500 words AND a fourth section warrants it]
[Concept + type]
[Why this placement]
```

After the plan, write:

> "Does this plan work for you, or would you like to adjust any concept before I render?"

Wait for the user's response. If they approve, proceed to Step 3. If they request changes,
revise the plan once before rendering.

---

## Step 3 — Render the Featured Image

### Design Rules for the Featured Image

The featured image must satisfy ALL of the following:

**Visual structure:**
- Canvas: 1600 × 900 px (16:9). In SVG, use `viewBox="0 0 1600 900"`.
- **Safe zone**: keep all essential content within the centre 960 × 900 area (x: 320–1280).
  The outer 320 px on each side may be cropped in narrow preview tiles.
- **Three layers of depth**: background (abstract texture or gradient field), midground
  (primary metaphor or concept shape), foreground (dominant text or icon element).
- **Dominant subject** must fill at least 40% of the canvas height.
- Place the strongest conceptual element in the **top-left quadrant** (Z-pattern principle).

**Typography (on the featured image):**
- Maximum **5 words** of text, rendered in bold, high-contrast type.
- Text must NOT repeat the article title word-for-word. It should tease an insight or pose
  a question — the curiosity gap. Example: title is "Why Agile Fails at Scale" →
  image text says "Scale changes everything." or "The hidden layer."
- Minimum font size equivalent to 72px at 1600px width.
- Always use high contrast: light text on dark background or vice versa. Never mid-tone
  on mid-tone.

**Colour and mood (match target reader):**
- Practitioner audience → teal / purple / coral with clean geometric shapes
- Executive / C-suite audience → deep navy / amber / white with authority-signalling layout
- Use at most 3 colours: one dominant (60%), one accent (30%), one highlight (10%)

**What to AVOID:**
- Stock photo aesthetics — no literal desk, laptop, or handshake imagery
- Text-heavy images — more than 5 words kills mobile readability
- Flat, single-colour backgrounds with just text — no depth, no visual interest
- Clip-art icons or generic emoji-as-icon approaches
- Repeating the full article title on the image

**After rendering**, always add:

```
📌 Featured Image — placement instructions:
- Upload this as your story's cover image in Medium editor
- Press Shift+F on the image after upload to set it as featured image
- Press Alt/Opt + click on the [describe focus point] to set focal point
- Recommended alt text: "[one sentence describing the image content and mood]"
```

---

## Step 4 — Render Each Inline Illustration

For each inline illustration in the approved plan, render it sequentially.
Between each rendering, write one sentence of plain text explaining what the image conveys
and where in the article it should go.

### Design Rules for Inline Illustrations

**Canvas**: use `viewBox="0 0 1200 675"` (16:9) or `viewBox="0 0 900 900"` (1:1 square)
depending on whether the content is landscape-oriented or compact/symmetric.

**Content rules:**
- **Max 3 primary elements** — a concept label, a shape or structure, a brief annotation
- Every element must earn its place: if removing it doesn't reduce understanding,
  cut it from the illustration
- Use **diagrams, metaphors, frameworks, and data visuals** — not decorative illustration
- Abstract agile concepts benefit from **spatial metaphors** (e.g. a spectrum, a bridge,
  a two-by-two matrix, a before/after split, concentric circles, a staircase)
- Keep text **inside the illustration to ≤ 6 short labels** — this is a diagram, not slides
- Avoid walls of text inside the SVG

**Illustration types by section type:**

| Article Section | Recommended Type |
|---|---|
| Opening hook / provocation | Bold typographic contrast visual or tension metaphor |
| Problem definition | Before/after split or gap diagram |
| Framework or insight | Two-by-two matrix, spectrum, or layered model |
| Evidence / case study | Simple data bar or comparison visual |
| Action steps | Sequential step diagram (3 steps max) |
| Closing challenge | Upward arrow or horizon metaphor |

**Caption rule:** After rendering each inline illustration, write the suggested caption:

```
📎 Inline illustration [N] — placement and caption:
- Place this image after the paragraph that begins: "[first 8 words of target paragraph]"
- Suggested caption: "[one punchy sentence — 10–15 words — that adds context not visible
  in the illustration itself]"
```

---

## Step 5 — Final Delivery Note

After all illustrations are rendered, append this summary block:

```
---
### 🖼️ Your Illustration Set — Upload Checklist

| # | Type | Section | Action |
|---|---|---|---|
| 1 | Featured image | Cover | Upload → Shift+F to set featured |
| 2 | Inline illustration | After "[Section]" | Upload → add caption |
| 3 | Inline illustration | After "[Section]" | Upload → add caption |
| [4] | [Inline illustration] | After "[Section]" | Upload → add caption |

**Screenshot tip:** Right-click each rendered image and "Save as" or use your OS
screenshot tool (Mac: Cmd+Shift+4, Win: Win+Shift+S) to capture only the visual area.
Upload as PNG for diagrams, JPG is also fine.

**Recommended image size before upload:** Resize to 1600px wide if your screenshot tool
outputs at a different resolution — Medium renders responsively but crisp retina export
is always better.
---
```

---

## Quality Checklist — Verify Before Rendering Each Visual

**Featured image:**
- [ ] Canvas is 1600 × 900 (viewBox 1600 900)
- [ ] All essential content within safe zone (x: 320–1280)
- [ ] Max 5 words of text on image
- [ ] Text does NOT repeat the article title verbatim
- [ ] Strong visual depth: background + midground + foreground layers
- [ ] Primary element fills ≥ 40% of canvas height
- [ ] Dominant element placed in top-left quadrant
- [ ] Max 3 colours; high contrast between text and background
- [ ] Creates a curiosity gap — image poses a visual question

**Each inline illustration:**
- [ ] Max 3 primary visual elements
- [ ] Canvas is 1200×675 (landscape) or 900×900 (square)
- [ ] Illustration type matches section function (see table above)
- [ ] Max 6 short text labels inside the SVG
- [ ] Placement instruction stated: after "[first 8 words]"
- [ ] Caption written: 10–15 words, adds context not visible in image

**Overall set:**
- [ ] Featured image + 2–4 inline illustrations produced (never 0 inline, never 5+)
- [ ] Inline illustration count matches article length:
  - < 1,200 words → 2 inline illustrations
  - 1,200–1,400 words → 2–3 inline illustrations
  - > 1,400 words → 3–4 inline illustrations
- [ ] No two consecutive sections have no illustration gap of > 400 words
- [ ] Upload checklist appended at the end

---

## Handoff Note — After Delivery

After the upload checklist, always append:

```
---
### ✅ Ready to publish?

Your Medium post and illustration set are complete. Before publishing:

1. Upload all illustrations in the order shown above
2. Set your featured image (Shift+F) and focal point (Alt/Opt + click)
3. Review the Medium preview in the publish settings panel to confirm the crop looks right
4. Add alt text to each image for accessibility

If you'd like to adjust any illustration's concept or style, just describe what you want
changed and I'll re-render it.
```
