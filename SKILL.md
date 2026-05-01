---
name: agile-article-content-suite
description: >
  A complete agile content creation suite for writing and publishing Medium articles.
  Use this skill for ANY request related to agile content — topic discovery, article
  briefs, Medium post writing, or illustration generation. Triggers for the full suite
  include: "I want to write an agile article", "help me create content for Medium",
  "agile content workflow", or "start the agile writing process". Also routes
  automatically between sub-skills: agile-topic-scout → agile-article-writer →
  agile-post-writer → agile-illustration-generator. Always consult this skill first
  when any agile writing or content task is mentioned — even casual ones like
  "what should I write about agile?" or "help me post something on Medium about Scrum".
---

# Agile Article Content Suite

A bundled suite of four collaborating skills for end-to-end agile content creation on Medium.

---

## The Four-Stage Workflow

```
[1] agile-topic-scout
       ↓  (user picks a topic)
[2] agile-article-writer
       ↓  (user confirms the brief)
[3] agile-post-writer
       ↓  (user reviews the post)
[4] agile-illustration-generator
```

Each stage hands off cleanly to the next. The user can also jump into any stage directly.

---

## Sub-Skills — When to Load Each

All four sub-skills live in the `skills/` folder. Read the relevant file when a stage is triggered.

| Stage | File | Trigger |
|-------|------|---------|
| Topic Scout | `skills/agile-topic-scout.md` | User wants topic ideas, "what's trending in agile", or `/agile-topic-scout` |
| Article Writer | `skills/agile-article-writer.md` | User has a topic and wants a brief + SEO package, or `/agile-article-writer` |
| Post Writer | `skills/agile-post-writer.md` | User wants to write the full Medium post from a brief, or `/agile-post-writer` |
| Illustration Generator | `skills/agile-illustration-generator.md` | User wants visuals/cover art for a finished post, or `/agile-illustration-generator` |

---

## Entry Point Logic

When this suite is triggered, first determine where the user is in the workflow:

1. **No topic yet** → load `skills/agile-topic-scout.md` and run the topic scout
2. **Has a topic, needs a brief** → load `skills/agile-article-writer.md`
3. **Has a brief, needs the post** → load `skills/agile-post-writer.md`
4. **Has a post, needs visuals** → load `skills/agile-illustration-generator.md`
5. **User types a slash command** (`/agile-topic-scout`, `/agile-article-writer`, etc.) → load the matching skill file directly

If in doubt, ask: *"Where would you like to start — finding a topic, writing a brief, drafting the post, or creating illustrations?"*

---

## Handoff Conventions

Each sub-skill ends with a handoff prompt that guides the user to the next stage. Honour these — do not skip them. They are the connective tissue that makes the suite feel like a single workflow rather than four disconnected tools.

---

## Reference Files

- `skills/agile-topic-scout.md` — Topic discovery: HTML artifact with 10 researched agile topics
- `skills/agile-article-writer.md` — Brief + SEO package: 7-section outline + Medium publishing fields
- `skills/agile-post-writer.md` — Full Medium post in @uragilecoach voice and style
- `skills/agile-illustration-generator.md` — Cover image + 2–4 inline SVG/HTML illustrations
