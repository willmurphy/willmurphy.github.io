# Signals – Skills & Templates

This file documents the tools, templates, and conventions Claude uses when generating the daily Signals report.

---

## Skills Available

### 🔍 Web Search
Used in Step 1 to research current trends.

- Use the `WebSearch` tool with targeted queries per domain.
- Query examples:
  - `"top social trends today 2026"`
  - `"AI technology news this week"`
  - `"economic market news today"`
- Cross-reference at least 2–3 sources per trend item.
- Prefer: Reuters, Bloomberg, AP News, The Verge, TechCrunch, WSJ, FT.
- Each trend must include at least one source URL.

---

### 📄 HTML Report Generation
Used in Step 2 to generate `signals/YYYY-MM-DD.html`.

**Page structure (in order):**
1. Header (title, date, back-link)
2. **Themes** — cross-reference all trends and group into 3–5 connected themes. Each theme has:
   - A name
   - A **horizon badge** classifying the theme's time horizon (see badge types below)
   - A "signals" attribution line showing which domain trends connect to it
   - A rich analytical paragraph (4–8 sentences) on the larger change happening in the world
   - An **opportunity callout** (for all themes except those tagged "Insight") describing a concrete, actionable opportunity
3. **Technological** section (4–5 trends, each with a detailed paragraph of 4–8 sentences)
4. **Economic** section (4–5 trends, each with a detailed paragraph of 4–8 sentences)
5. **Social** section (4–5 trends, each with a detailed paragraph of 4–8 sentences)
6. Footer

**Horizon badge types:**
- `horizon-near` — "Near-term Opportunity · 1 yr" (yellow)
- `horizon-mid` — "Mid-term Opportunity · 2–3 yrs" (purple)
- `horizon-long` — "Long-term Opportunity · 5+ yrs" (green)
- `horizon-insight` — "Insight" (gray) — used for themes that are analytical observations rather than opportunities; these do NOT get an opportunity callout

**Opportunity callout color coding:**
- `.near` — amber left border (matches near-term horizon)
- `.mid` — purple left border (matches mid-term horizon)
- `.long` — green left border (matches long-term horizon)

**Source link format:**
- Include the source name AND a descriptive title in the link text
- Example: `↗ Washington Post – Pentagon Declares Anthropic a Threat to National Security`

**Full page template:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Will's Signals – [Full Date]</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
      background: #f9f9f7; color: #1a1a1a;
      max-width: 780px; margin: 0 auto; padding: 2rem 1.5rem 4rem;
    }
    header { border-bottom: 2px solid #1a1a1a; padding-bottom: 1rem; margin-bottom: 2.5rem; }
    header nav a { font-size: 0.85rem; color: #555; text-decoration: none; }
    header nav a:hover { color: #1a1a1a; }
    header h1 { font-size: 2.2rem; font-weight: 700; letter-spacing: -0.5px; margin-top: 0.5rem; }
    header .date { font-size: 1rem; color: #555; margin-top: 0.25rem; }
    section { margin-bottom: 3rem; }
    section h2 { font-size: 1.15rem; font-weight: 700; border-bottom: 1px solid #ddd; padding-bottom: 0.5rem; margin-bottom: 1.5rem; }
    .trend { margin-bottom: 1.75rem; padding-bottom: 1.75rem; border-bottom: 1px solid #efefed; }
    .trend:last-child { border-bottom: none; padding-bottom: 0; }
    .trend h3 { font-size: 1.44rem; font-weight: 600; margin-bottom: 0.4rem; line-height: 1.4; }
    .trend p { font-size: 1.34rem; line-height: 1.7; color: #333; }
    .trend .source { display: inline-block; margin-top: 0.5rem; font-size: 1.15rem; color: #888; text-decoration: none; }
    .trend .source:hover { color: #0066cc; }
    footer { border-top: 1px solid #ddd; padding-top: 1rem; margin-top: 1rem; font-size: 1.18rem; color: #aaa; }
    footer a { color: #888; text-decoration: none; }
    footer a:hover { color: #1a1a1a; }
    #themes { background: #fff; color: #1a1a1a; border: 1.5px solid #d0d0cc; border-radius: 10px; padding: 1.75rem 2rem; margin-bottom: 3rem; }
    #themes h2 { font-size: 0.75rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.1em; color: #888; border-bottom: 1px solid #e0e0dc; padding-bottom: 0.5rem; margin-bottom: 1.5rem; }
    .theme-item { margin-bottom: 1.5rem; padding-bottom: 1.5rem; border-bottom: 1px solid #efefed; }
    .theme-item:last-child { margin-bottom: 0; padding-bottom: 0; border-bottom: none; }
    .theme-item h3 { font-size: 1.37rem; font-weight: 700; color: #1a1a1a; margin-bottom: 0.35rem; line-height: 1.4; }
    .theme-item .signals { font-size: 1.08rem; color: #888; margin-bottom: 0.5rem; }
    .theme-item p { font-size: 1.27rem; line-height: 1.65; color: #333; }
    .horizon {
      display: inline-block;
      font-size: 0.72rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.07em;
      border-radius: 4px;
      padding: 0.2rem 0.55rem;
      margin-bottom: 0.45rem;
    }
    .horizon-near    { background: #fef3c7; color: #92400e; }
    .horizon-mid     { background: #ede9fe; color: #5b21b6; }
    .horizon-long    { background: #dcfce7; color: #166534; }
    .horizon-insight { background: #f1f5f9; color: #475569; }
    .opportunity-callout {
      margin-top: 1rem;
      padding: 0.75rem 1rem;
      border-left: 3px solid #d0d0cc;
      background: #fafaf8;
      border-radius: 0 5px 5px 0;
    }
    .opportunity-callout .opp-label {
      font-size: 0.68rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.09em;
      color: #aaa;
      margin-bottom: 0.3rem;
    }
    .opportunity-callout.near { border-left-color: #f59e0b; }
    .opportunity-callout.mid  { border-left-color: #8b5cf6; }
    .opportunity-callout.long { border-left-color: #22c55e; }
    .opportunity-callout p {
      font-size: 1.1rem;
      line-height: 1.6;
      color: #444;
      margin: 0;
    }
  </style>
</head>
<body>
  <header>
    <nav><a href="index.html">← Will's Signals</a></nav>
    <h1>Will's Signals</h1>
    <p class="date">[Full Date, e.g. Friday, February 27, 2026]</p>
  </header>

  <!-- THEMES: Cross-reference all trends and group into 3–5 connected themes.
       Each theme should name the forces in play, cite which domain signals connect to it,
       include a horizon badge, a rich analytical paragraph, and an opportunity callout
       (except for "Insight" themes which omit the callout). -->
  <section id="themes">
    <h2>Themes</h2>

    <div class="theme-item">
      <h3>[Theme Name]</h3>
      <div><span class="horizon horizon-near">Near-term Opportunity · 1 yr</span></div>
      <div class="signals">[Domain]: [signal], [signal] · [Domain]: [signal]</div>
      <p>[4–8 sentences of rich analysis on what these signals have in common, what larger shift they point to, and why it matters. Be specific, cite data points from the trends, and connect the dots across domains.]</p>
      <div class="opportunity-callout near">
        <div class="opp-label">Top Opportunity</div>
        <p>[2–4 sentences describing a concrete, actionable opportunity. Be specific about what to build/invest in, who the target customer is, why the timing is right, and what the competitive moat looks like.]</p>
      </div>
    </div>

    <div class="theme-item">
      <h3>[Insight Theme Name]</h3>
      <div><span class="horizon horizon-insight">Insight</span></div>
      <div class="signals">[Domain]: [signal], [signal] · [Domain]: [signal]</div>
      <p>[4–8 sentences of analytical observation. No opportunity callout for Insight themes.]</p>
    </div>

    <!-- Repeat for 3–5 themes total. Aim for 3–4 opportunity themes + 1 insight theme. -->
  </section>

  <section id="technological">
    <h2>💡 Technological</h2>

    <div class="trend">
      <h3>[Trend Title]</h3>
      <p>[4–8 sentences: what the trend is, specific data points, why it matters, second-order effects, what to watch.]</p>
      <a class="source" href="[URL]" target="_blank">↗ [Source Name] – [Article Title or Description]</a>
    </div>

    <!-- Repeat for 4–5 trends -->
  </section>

  <section id="economic">
    <h2>📈 Economic</h2>

    <div class="trend">
      <h3>[Trend Title]</h3>
      <p>[4–8 sentences: what the trend is, specific data points, why it matters, second-order effects, what to watch.]</p>
      <a class="source" href="[URL]" target="_blank">↗ [Source Name] – [Article Title or Description]</a>
    </div>

    <!-- Repeat for 4–5 trends -->
  </section>

  <section id="social">
    <h2>📱 Social</h2>

    <div class="trend">
      <h3>[Trend Title]</h3>
      <p>[4–8 sentences: what the trend is, specific data points, why it matters, second-order effects, what to watch.]</p>
      <a class="source" href="[URL]" target="_blank">↗ [Source Name] – [Article Title or Description]</a>
    </div>

    <!-- Repeat for 4–5 trends -->
  </section>

  <footer>
    <p>Generated by Claude · <a href="index.html">Back to Calendar</a></p>
  </footer>

</body>
</html>
```

**Content rules:**
- Tone: professional, analytical, factual — informed perspective without being editorial
- Each trend: 4–8 sentences covering what it is, specific data points, why it matters, second-order effects, what to watch
- 4–5 trends per section (aim for 5)
- Themes should have 4–8 sentence analytical paragraphs that connect dots across domains
- Opportunity callouts should be concrete and actionable — name what to build/invest in, who the customer is, why the timing is right
- Source links should include the source name AND a descriptive article title
- No external CSS/JS — file must be fully self-contained

**Common mistakes to avoid (critical — follow the template exactly):**
- **Themes box styling**: Use `background: #fff; border: 1.5px solid #d0d0cc; border-radius: 10px` (light card). NEVER use a dark background (`#1a1a1a`) — that is not the correct design.
- **Horizon badges are required**: Every theme MUST have a `<div><span class="horizon horizon-near">Near-term Opportunity · 1 yr</span></div>` (or `-mid`, `-long`, `-insight`) badge. Never omit these.
- **Opportunity callouts are required**: Every theme MUST have an opportunity callout block EXCEPT themes tagged `horizon-insight`. Never omit these.
- **Signals line format**: Use domain prefixes — `Technological: [signal] · Economic: [signal]`. Do NOT use bare keyword lists.
- **Source link format**: Use `↗ Source Name – Article Title` with `target="_blank"`. Do NOT use bare source names.
- **Include ALL CSS from the template**: The stylesheet MUST include `.horizon`, `.horizon-near/mid/long/insight`, `.opportunity-callout`, `header nav a:hover`, and `footer a:hover` rules. Copy the full `<style>` block from the template — do not write it from memory.
- **Paragraph depth**: Trend paragraphs must be 4–8 substantive sentences with specific data points, second-order effects, and "what to watch." Theme paragraphs must also be 4–8 sentences of rich cross-domain analysis. Short 2–3 sentence summaries are NOT acceptable.
- **Use `←` entity**: Use `←` (not `&larr;`) for the back-link arrow to match the established reports.

---

### 📅 Calendar Page Update
Used in Step 3 to update `signals/index.html`.

The calendar is a JavaScript-driven interactive grid. To add a new report, add a new entry to the `REPORTS` object in the `<script>` block:

```javascript
const REPORTS = {
  'YYYY-MM-DD': 'YYYY-MM-DD.html',  // ← add new entries at the top
  // ... existing entries
};
```

**Update rule:** Add the new date entry at the **top** of the `REPORTS` object, most recent first.

**Do NOT replace the full index.html template** — only edit the `REPORTS` object inside the existing `<script>` block.

---

### 🐙 GitHub Publishing
Used in Step 4 to commit and push the report.

**Commands:**
```bash
cd ~/willmurphy.github.io
git add signals/
git commit -m "Signals report: YYYY-MM-DD"
git push origin main
```

**Requirements:**
- The `willmurphy.github.io` repo must be cloned locally at `~/willmurphy.github.io`
- Git must be configured with credentials (SSH key or credential helper) to push without a password prompt
- GitHub Pages must be enabled on the `main` branch

**Verify the live URL:**
```
https://willmurphy.github.io/signals/YYYY-MM-DD.html
```

---

## Folder Structure

```
Signals/                          ← This project root (local workspace)
├── CLAUDE.md                     ← Task instructions for Claude
├── SKILLS.md                     ← This file: templates & tool reference
└── signals/                      ← Output folder → willmurphy.github.io/signals/
    ├── index.html                ← Calendar page (updated daily)
    └── YYYY-MM-DD.html           ← Daily report pages (generated each morning)
```

The contents of `signals/` mirror what gets pushed to `willmurphy.github.io/signals/`.
