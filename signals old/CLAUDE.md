# Signals – Daily Trend Report

## Project Overview

Signals is an automated daily briefing published to `willmurphy.github.io/signals/`. Each morning at **4:30 AM**, Claude researches and publishes a fresh trend report covering Social, Technological, and Economic domains.

**Repository:** `willmurphy.github.io`
**Output folder:** `signals/` (local) → `https://willmurphy.github.io/signals/`
**Skills reference:** See `SKILLS.md`

---

## Daily Task (runs at 4:30 AM)

### Step 1 — Research

Use web search to find today's top 3–5 trends in each domain:

- **📱 Social** — viral topics, cultural shifts, demographic changes, public sentiment, social media movements
- **💡 Technological** — AI/ML news, product launches, cybersecurity, scientific breakthroughs, emerging tech
- **📈 Economic** — markets, inflation, jobs, trade, startup funding, central bank signals, commodity prices

For each trend: what it is · why it matters · what to watch · source URL.

### Step 2 — Generate Report

Create `signals/YYYY-MM-DD.html` using today's date. See `SKILLS.md` for the exact HTML template and style guide.

### Step 3 — Update Calendar

Add a new entry to `signals/index.html` linking to today's report (most recent first). See `SKILLS.md` for the calendar template.

### Step 4 — Done

Save both files. Will handles the git commit and push to GitHub separately.

---

## Success Criteria

- [ ] `signals/YYYY-MM-DD.html` is saved and ready
- [ ] `signals/index.html` includes a link to today's report at the top
- [ ] All three sections have 3–5 sourced trend items
- [ ] HTML files are fully self-contained (no external CSS/JS)
