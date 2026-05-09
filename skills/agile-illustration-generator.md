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
  at strategic reading-rhythm points throughout the article. All visuals are generated in
  Canva and saved to the user's "medium" folder (folder ID: FAFcT0EuO00).
---

# Agile Illustration Generator

## ⚠️ SKILL RESPONSIBILITY — READ FIRST

This skill has ONE job: produce publication-ready visual assets for a Medium agile article,
generated entirely in Canva and saved to the user's "medium" folder.

**Default tool: Canva for ALL illustrations.** Do NOT use SVG or show_widget for any
illustration in this skill. Every visual — featured image and all inline illustrations —
must be generated via the Canva generate-design tool and saved to folder ID: FAFcT0EuO00.

**Output 1 — Featured / Preview Image:** One high-impact cover image.
Canva design_type: twitter_post (1600×900, 16:9 landscape — matches Medium spec exactly).

**Output 2 — Inline Illustrations:** 2–4 contextual diagrams.
Canva design_type: twitter_post (1600×900, 16:9 landscape — same as featured).

**Folder:** All designs saved to the user's Canva "medium" folder (ID: FAFcT0EuO00).

---

## Research Foundation

### Featured Image CTR Research
- Articles with images receive 94% more views on Medium
- Rule of Three: limit to 3 primary visual elements
- Curiosity gap principle: image poses a visual question; the title answers it
- Warm colours (amber, coral) signal urgency; cool (teal, blue) signal authority
- Medium auto-crops featured images to ~16:9 — keep key content in centre 60%
- Layered visual depth always outperforms flat minimalist designs

### Inline Illustration Research
- Optimal placement: one visual every 300–400 words, after a new concept or turning point
- Max 2–3 primary elements per illustration
- Captions are read 300% more often than body copy — always write one

### Medium Technical Specs (2025–2026)
- Featured image: 1600 × 900 px (16:9)
- Inline images: 1600 px wide target, PNG preferred
- Set focal point: Shift+F then Alt/Opt+click in Medium editor

---

## Step 1 — Parse the Article

Extract: headline, sections (H2 names + opening sentences), core argument,
target reader, opening mode, key data points, tone.

If the full article is not present, ask the user to paste it.
Do not proceed without the article text — illustrations must be anchored to specific content.

---

## Step 2 — Plan the Illustration Set

Produce this plan before generating anything:

### Illustration Plan

**Featured Image concept:**
[Visual metaphor + dominant element + colour palette + curiosity gap]
**3-second message:** "[What a reader sees in 3 seconds with no caption]"

**Inline 1 — after section "[Section Name]":**
[Concept + type: comparison / spectrum / framework / step diagram]
**3-second message:** "[One clear takeaway]"

**Inline 2 — after section "[Section Name]":**
[Concept + type]
**3-second message:** "[One clear takeaway]"

[Inline 3 — if article ≥ 1,400 words]
[Inline 4 — if article ≥ 1,500 words AND a fourth section warrants it]

After the plan, ask:
"Does this plan work for you, or would you like to adjust anything before I generate?"
Wait for approval. If approved → Step 3. If changes requested → revise once → proceed.

---

## Step 3 — Generate ALL Illustrations in Canva

### ⚠️ CRITICAL FORMAT RULE
ALL illustrations — featured AND inline — must use design_type: twitter_post (1600×900, 16:9 landscape).
NEVER use poster, infographic, or any portrait format. Medium requires landscape images.

### Canva Query Construction Formula

Build every query using this structure:

[Core tension or transformation from the article] + [target reader's role or context]
+ [specific visual metaphor representing the concept] + [mood: urgent/authoritative/reflective]
— clean layout, ONE dominant visual element, no clutter,
no stock photo aesthetics, no literal office imagery, professional style

**Examples by concept type:**
- AI disruption → "AI network overtaking human sprint board, engineering leader,
  dramatic tech takeover, dark high contrast, cinematic, one dominant element"
- Role evolution → "coach standing at boundary between human and machine zones,
  agile team, systems thinking, authoritative, deep navy and amber"
- Comparison → "split panel slow manual vs instant AI, Scrum Master, before-after
  tension, bold geometric, teal and white"
- Step framework → "ascending staircase three bold steps, agile practitioner,
  practical action, clean minimalist, amber highlights"
- Spectrum → "horizontal spectrum chaos to clarity, agile leader, positioning
  diagram, thought-provoking, purple gradient"

Always include: core tension, target reader's role, specific visual metaphor,
mood word, and "one dominant visual, no clutter" in every query.

### Design Type Reference

| Illustration Role       | Canva design_type                      |
|-------------------------|----------------------------------------|
| Featured / cover image  | twitter_post (1600×900, 16:9 landscape)|
| Inline — all types      | twitter_post (1600×900, 16:9 landscape)|

### Generation Sequence

Generate ALL illustrations in order — do not batch or skip.
For EACH illustration, execute sub-steps A → B → C → D in full before moving to the next.

**A — Generate candidates:**
Call generate-design with:
- design_type: twitter_post
- query: built from the formula above
- user_intent: "Generate [featured image / inline illustration N] for Medium article: [title]"

**B — Ask user to pick:**
"👆 Pick the design you prefer (1, 2, 3, or 4) for [featured / inline N]."
Wait for user selection before proceeding.

**C — Create and save to medium folder:**
1. create-design-from-candidate (job_id + candidate_id)
2. move-item-to-folder → to_folder_id: FAFcT0EuO00
3. Confirm: "✅ Saved to your Canva medium folder as [descriptive name]."

**D — State placement instruction:**
"📎 Place after paragraph beginning: '[first 8 words of target paragraph]'
Suggested caption: '[10–15 words adding context not visible in the image]'"

Then proceed immediately to the next illustration.

---

## Step 4 — Final Delivery Summary

After all illustrations are saved, append this block:

---
### 🖼️ Illustration Set — Upload Checklist

| # | Type | Canva name | Medium placement |
|---|---|---|---|
| 1 | Featured image | [name] | Cover — Shift+F to set featured |
| 2 | Inline | [name] | After "[Section]" |
| 3 | Inline | [name] | After "[Section]" |
| 4 | Inline | [name] | After "[Section]" |

All designs are in your Canva "medium" folder.
Open each in Canva to tweak, download as PNG, upload to Medium.

---

## Step 5 — Handoff Note

After the upload checklist, always append:

---
### ✅ Ready to publish?

1. Open each design in Canva — tweak text, colours, layout as needed
2. Download as PNG (File → Download → PNG)
3. Upload to Medium in the order above
4. Set featured image (Shift+F) and focal point (Alt/Opt+click)
5. Add alt text to each image
6. Check Medium preview crop in publish settings

To regenerate any illustration, describe what you want changed.
Type /linkedin-post-writer when ready to write the LinkedIn promo post.

---

## Quality Checklist

Verify before generating each illustration:

**Each Canva query:**
- [ ] Core tension named (not just the topic)
- [ ] Target reader's role included
- [ ] Specific visual metaphor (not generic)
- [ ] Mood word included
- [ ] "One dominant visual, no clutter" in every query
- [ ] design_type is twitter_post — never poster, never infographic

**Overall set:**
- [ ] ALL illustrations use twitter_post (1600×900, 16:9 landscape) — no portrait formats
- [ ] Inline count: <1,200 words → 2; 1,200–1,400 → 2–3; >1,400 → 3–4
- [ ] All saved to Canva folder FAFcT0EuO00
- [ ] Placement + caption stated for each inline illustration
- [ ] Upload checklist appended
- [ ] Handoff note appended
