---
name: agile-topic-scout
description: >
  Use this skill whenever the user wants to discover or browse trending topic ideas in agile
  fields — including agile methodologies, agile leadership, Scrum, Kanban, SAFe, team coaching,
  agile training, facilitation, OKRs, organizational agility, and business agility. Trigger when
  the user says: "run the topic scout", "agile topic ideas", "what's trending in agile",
  "agile content ideas", "hot agile topics", "give me agile topics", "what should I write about
  in agile", or any request to browse or discover agile topics for content creation. This skill
  ONLY researches and displays the topic table — it does not write article briefs. Article briefs
  are handled by the separate agile-article-writer skill, which is triggered automatically when
  the user selects a topic from the table and clicks Generate.
---

# Agile Topic Scout

## ⚠️ OUTPUT RULE — READ THIS FIRST, FOLLOW IT EXACTLY

This skill has ONE job and ONE output: an **interactive HTML artifact** showing 10 researched
agile topics in a selectable table.

**NEVER output:**
- Plain text lists or bullet points of topics
- Markdown tables
- Prose summaries of what was found
- Any content from Step 5 (article briefs) — that is a separate skill

**ALWAYS output:**
- One short sentence before the artifact
- Then immediately the artifact with real topic data injected

This rule is absolute. There are no exceptions.

---

## Step 1 — Run Web Research (complete before any output)

Run ALL queries below. Use `web_fetch` on the 2–3 most promising URLs for deeper content.
Do not produce any output until all searches are complete.

**Practitioner & coaching-first queries (run these first):**
- `agile team retrospective lessons learned practitioners 2026`
- `scrum master real team challenges stories 2026`
- `agile coaching team dysfunction patterns how to fix`
- `psychological safety agile team practice real examples`
- `kanban flow management team practice examples`
- `sprint review improvement examples practitioners`
- `agile team failure stories coaching reflections`
- `site:youtube.com agile coaching team retrospective 2025 2026`
- `agile podcast episode team coaching retrospective`
- `agile team velocity burnout sustainability coaches`

**Trend & context queries (supporting signal only):**
- `agile methodology trends 2026`
- `AI agile coaching team practice 2026`

**Source priority — search in this order of preference:**

Tier 1 — Practitioner-first (primary sources):
YouTube channels and episodes: Lenny's Podcast, Agile for Humans, Scrum Master Toolbox
Podcast, Agile Amped, Coaching Agile Journeys, any practitioner agile channel
Medium agile tag practitioner articles, Substack agile coaching newsletters
LinkedIn long-form posts by working agile coaches and Scrum Masters

Tier 2 — Community & experience reports:
Reddit r/agile, Agile Alliance Experience Reports, Scrum.org Practitioners blog,
ICAgile community stories, team-level case studies

Tier 3 — Institutional / research (use only when they contain concrete team-level data):
Gartner, McKinsey, Deloitte, HBR — reference only to add credibility to a
practitioner-sourced topic, never as the primary topic driver

---

## Step 2 — Score & Select 10 Topics

Score each candidate 1–5 per dimension. Select the 10 highest-scoring (≥18/25).

| Dimension            | What to assess                                              |
|----------------------|-------------------------------------------------------------|
| Recency              | Discussed in last 30–90 days?                               |
| Search signal        | Multiple distinct practitioner sources?                     |
| Coach applicability  | Can a team coach design a retro or coaching session on this immediately? |
| Practitioner buzz    | Active discussion by coaches, Scrum Masters, teams?         |
| Content gap          | Few practitioner-written articles exist yet?                |

Ensure variety across: ≥3 team coaching / team practice, ≥2 retrospective or facilitation,
≥1 leadership, ≥1 scaling, ≥1 AI + agile crossover.
At least 5 of 10 topics must be directly actionable by a team-level agile coach
(i.e. not requiring executive sponsorship to apply).

---

## Step 3 — Build the TOPICS Array

Compile one JavaScript object per topic. All fields required. All data from real search results.

```
{
  title:              string  — ≤10 words
  category:           string  — e.g. "Agile Leadership", "Team Coaching", "Scaling"
  popularityScore:    number  — 1–10 from rubric
  trendDirection:     string  — "🔥 Rising" | "📈 Emerging" | "➡️ Stable"
  mediaCoverage:      string  — "High" | "Moderate" | "Low"
  jobMarketSignal:    string  — "Yes" | "Partial" | "No"
  conferencePresence: string  — "Yes" | "No"
  sources: [
    { name: string, description: string }  — 2–3 items, description ≤12 words
  ]
  whyChosen:          string  — 2 sentences: what in research surfaced this topic
  seniorManagerAngle: string  — 2 sentences: the business/leadership hook
  suggestedAngle:     string  — one punchy potential article headline
}
```

Use "N/A" for any field where data is unavailable. Never fabricate.

---

## Step 4 — Render the Artifact (MANDATORY — no substitutes)

Write exactly one sentence, then the artifact immediately after:

> "Here are today's 10 trending agile topics — tick one to generate its article brief and Medium SEO package."

Inject all 10 topic objects into `const TOPICS = [...]` replacing `[INJECT_TOPICS_HERE]`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display&family=DM+Sans:ital,wght@0,300;0,400;0,500;0,600;1,400&display=swap');
*{box-sizing:border-box;margin:0;padding:0;}
body{font-family:'DM Sans',sans-serif;background:#0f0f13;color:#e8e8f0;min-height:100vh;padding:28px 20px 100px;}
.hdr{max-width:1100px;margin:0 auto 28px;display:flex;align-items:flex-end;justify-content:space-between;flex-wrap:wrap;gap:12px;}
.hdr h1{font-family:'DM Serif Display',serif;font-size:1.9rem;color:#e8e8f0;letter-spacing:-.3px;}
.sub{font-size:.75rem;color:#7a7a94;margin-top:3px;text-transform:uppercase;letter-spacing:.07em;}
.pill{background:#1e1e28;border:0.5px solid #2a2a38;border-radius:999px;padding:7px 16px;font-size:.82rem;color:#7a7a94;}
.pill b{color:#7c6af7;}
.tw{max-width:1100px;margin:0 auto;overflow-x:auto;}
table{width:100%;border-collapse:separate;border-spacing:0 5px;table-layout:fixed;}
col.c0{width:36px;}col.c1{width:190px;}col.c2{width:86px;}col.c3{width:118px;}col.c4{width:170px;}col.c5{width:auto;}
thead th{font-size:.68rem;font-weight:600;letter-spacing:.09em;text-transform:uppercase;color:#7a7a94;padding:0 10px 10px;text-align:left;}
thead th:first-child{padding-left:16px;}
tbody tr.mr{background:#17171e;cursor:pointer;transition:background .12s;}
tbody tr.mr:hover{background:#1e1e28;}
tbody tr.mr.sel{background:#1a1a2e;box-shadow:inset 2px 0 0 #7c6af7;}
tbody td{padding:12px 10px;vertical-align:top;}
tbody td:first-child{border-radius:8px 0 0 8px;padding-left:16px;}
tbody td:last-child{border-radius:0 8px 8px 0;}
.cbw{display:flex;align-items:flex-start;justify-content:center;padding-top:2px;}
.cb{width:18px;height:18px;border-radius:50%;border:1.5px solid #2a2a38;background:#0f0f13;display:flex;align-items:center;justify-content:center;transition:all .12s;flex-shrink:0;}
.cb.on{background:#7c6af7;border-color:#7c6af7;}
.cbd{width:7px;height:7px;border-radius:50%;background:white;display:none;}
.cb.on .cbd{display:block;}
.tn{font-size:.88rem;font-weight:600;color:#e8e8f0;line-height:1.3;margin-bottom:4px;}
.cat{display:inline-block;background:#1e1e28;color:#7a7a94;font-size:.65rem;font-weight:500;letter-spacing:.05em;padding:2px 7px;border-radius:999px;text-transform:uppercase;border:0.5px solid #2a2a38;}
.ps{font-size:.95rem;font-weight:700;color:#e8e8f0;}
.psub{font-size:.65rem;color:#7a7a94;}
.pb{width:54px;height:3px;background:#2a2a38;border-radius:999px;margin:5px 0 6px;overflow:hidden;}
.pf{height:100%;border-radius:999px;}
.br{background:#4ecdc4;}.be{background:#f7c56a;}.bs{background:#7a7a94;}
.tr{font-size:.75rem;font-weight:500;}
.trr{color:#4ecdc4;}.tre{color:#f7c56a;}.trs{color:#7a7a94;}
.mr2{display:flex;flex-direction:column;gap:4px;}
.mi{display:flex;align-items:center;gap:5px;font-size:.73rem;color:#7a7a94;}
.dot{width:6px;height:6px;border-radius:50%;flex-shrink:0;}
.dh,.dy{background:#4ade80;}.dm,.dp{background:#f7c56a;}.dl,.dn{background:#f87171;}
.sl{display:flex;flex-direction:column;gap:5px;}
.sn{font-size:.73rem;font-weight:600;color:#4ecdc4;}
.sd{font-size:.71rem;color:#7a7a94;line-height:1.35;}
.rt{font-size:.74rem;color:#a0a0b8;line-height:1.5;margin-bottom:6px;}
.ang{font-size:.72rem;color:#7c6af7;font-style:italic;line-height:1.35;}
.exr{display:none;}
.exr.open{display:table-row;}
.exr td{background:#13131a;padding:0 16px;border-radius:0 0 8px 8px;}
.exi{padding:12px 0 14px;border-top:1px solid #2a2a38;display:grid;grid-template-columns:1fr 1fr;gap:20px;}
.exl{font-size:.65rem;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:#7a7a94;margin-bottom:4px;}
.exb{font-size:.78rem;color:#a0a0b8;line-height:1.5;}
.bot{max-width:1100px;margin:20px auto 0;display:flex;align-items:center;gap:16px;flex-wrap:wrap;}
.hint{font-size:.82rem;color:#7a7a94;transition:opacity .2s;}
.gb{background:linear-gradient(135deg,#7c6af7,#5b53d4);border:none;border-radius:10px;color:#fff;font-family:'DM Sans',sans-serif;font-size:.88rem;font-weight:600;padding:12px 26px;cursor:pointer;display:none;box-shadow:0 4px 20px rgba(124,106,247,.35);transition:filter .15s;}
.gb.vis{display:inline-block;}
.gb:hover{filter:brightness(1.1);}
</style>
</head>
<body>
<div class="hdr">
  <div>
    <h1>Agile Topic Scout</h1>
    <div class="sub" id="dl"></div>
  </div>
  <div class="pill"><b id="sc">0</b>&nbsp;of 1 selected</div>
</div>
<div class="tw">
  <table>
    <colgroup><col class="c0"><col class="c1"><col class="c2"><col class="c3"><col class="c4"><col class="c5"></colgroup>
    <thead>
      <tr>
        <th></th><th>Topic</th><th>Popularity</th>
        <th>Metrics</th><th>Sources</th><th>Reason &amp; suggested angle</th>
      </tr>
    </thead>
    <tbody id="tb"></tbody>
  </table>
</div>
<div class="bot">
  <div class="hint" id="hint">↑ Tick one topic to generate its article brief</div>
  <button class="gb" id="gb" onclick="gen()">Generate article brief →</button>
</div>
<script>
const TOPICS=[INJECT_TOPICS_HERE];
let sel=-1;
function dc(v,t){
  if(t==='media')return v==='High'?'dh':v==='Moderate'?'dm':'dl';
  if(t==='job')return v==='Yes'?'dy':v==='Partial'?'dp':'dn';
  return v==='Yes'?'dy':'dn';
}
function tc(tr){return tr.includes('Rising')?'trr':tr.includes('Emerging')?'tre':'trs';}
function bc(tr){return tr.includes('Rising')?'br':tr.includes('Emerging')?'be':'bs';}
function build(){
  document.getElementById('dl').textContent=new Date().toLocaleDateString('en-US',{weekday:'long',year:'numeric',month:'long',day:'numeric'});
  const tb=document.getElementById('tb');
  TOPICS.forEach((t,i)=>{
    const pct=Math.round(t.popularityScore/10*100);
    const sh=t.sources.map(s=>`<div class="sn">${s.name}</div><div class="sd">${s.description}</div>`).join('<div style="height:3px"></div>');
    const tr=document.createElement('tr');
    tr.className='mr';tr.id='r'+i;tr.onclick=()=>tog(i);
    tr.innerHTML=`
      <td class="cbw"><div class="cb" id="cb${i}"><div class="cbd"></div></div></td>
      <td><div class="tn">${i+1}. ${t.title}</div><span class="cat">${t.category}</span></td>
      <td><div class="ps">${t.popularityScore}<span class="psub">/10</span></div><div class="pb"><div class="pf ${bc(t.trendDirection)}" style="width:${pct}%"></div></div><div class="tr ${tc(t.trendDirection)}">${t.trendDirection}</div></td>
      <td><div class="mr2"><div class="mi"><div class="dot ${dc(t.mediaCoverage,'media')}"></div>Media: ${t.mediaCoverage}</div><div class="mi"><div class="dot ${dc(t.jobMarketSignal,'job')}"></div>Jobs: ${t.jobMarketSignal}</div><div class="mi"><div class="dot ${dc(t.conferencePresence,'conf')}"></div>Conf: ${t.conferencePresence}</div></div></td>
      <td><div class="sl">${sh}</div></td>
      <td><div class="rt">${t.seniorManagerAngle}</div><div class="ang">💡 "${t.suggestedAngle}"</div></td>`;
    tb.appendChild(tr);
    const ex=document.createElement('tr');
    ex.className='exr';ex.id='ex'+i;
    ex.innerHTML=`<td colspan="6"><div class="exi"><div><div class="exl">Why this topic now</div><div class="exb">${t.whyChosen}</div></div><div><div class="exl">Senior manager hook</div><div class="exb">${t.seniorManagerAngle}</div></div></div></td>`;
    tb.appendChild(ex);
  });
}
function tog(i){
  if(sel!==-1&&sel!==i){
    document.getElementById('r'+sel).classList.remove('sel');
    document.getElementById('cb'+sel).classList.remove('on');
    document.getElementById('ex'+sel).classList.remove('open');
  }
  if(sel===i){
    document.getElementById('r'+i).classList.remove('sel');
    document.getElementById('cb'+i).classList.remove('on');
    document.getElementById('ex'+i).classList.remove('open');
    sel=-1;
  } else {
    document.getElementById('r'+i).classList.add('sel');
    document.getElementById('cb'+i).classList.add('on');
    document.getElementById('ex'+i).classList.add('open');
    sel=i;
  }
  const has=sel!==-1;
  document.getElementById('sc').textContent=has?'1':'0';
  document.getElementById('gb').classList.toggle('vis',has);
  document.getElementById('hint').style.opacity=has?'0':'1';
}
function gen(){
  if(sel===-1)return;
  const t=TOPICS[sel];
  const msg=`/agile-article-writer\n\nTopic: ${t.title}\nCategory: ${t.category}\nPopularity: ${t.popularityScore}/10\nTrend: ${t.trendDirection}\nWhy chosen: ${t.whyChosen}\nSenior manager angle: ${t.seniorManagerAngle}\nSuggested angle: ${t.suggestedAngle}\nSources: ${t.sources.map(s=>s.name+' — '+s.description).join(' | ')}`;
  if(typeof sendPrompt==='function')sendPrompt(msg);
  else alert(msg);
}
build();
</script>
</body>
</html>
```

---

## Quality Standards

- Never fabricate sources or metrics — use "N/A" if unavailable
- At least 5 of the 10 topics must be directly actionable by a team-level agile coach without needing executive buy-in
- At least 2 topics must reference a YouTube channel, podcast episode, or practitioner video as a primary source
- Institutional reports (Gartner, McKinsey, Deloitte) may only appear as supporting sources, never as the sole reason a topic was chosen
- Complete ALL searches before producing any output
- The artifact is the ONLY acceptable output — no plain text, no markdown tables
- This skill ends when the artifact renders — article briefs are handled by agile-article-writer
