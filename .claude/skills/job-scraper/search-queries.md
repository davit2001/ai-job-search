# Search Queries for Job Scraper

<!-- Davit Hakobyan — Frontend / Full-Stack Engineer, Yerevan Armenia -->
<!-- Target: Fully remote (worldwide) or Armenia on-site -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** English (Professional) and Armenian (Native). Query categories are written in English; role titles are standard English — Armenian-language job postings are generally in English too for international/remote roles.

## Search Sites

Primary:
- **linkedin.com/jobs** — global remote + Armenia on-site; covered by `linkedin-search` CLI
- **freehire.me** — tech-focused global aggregator (~50 ATS platforms); covered by `freehire-search` CLI

Secondary (WebSearch fallback — company career pages):
- `site:greenhouse.io "frontend engineer" OR "frontend developer" remote`
- `site:lever.co "frontend engineer" OR "frontend developer" remote`
- `site:jobs.ashbyhq.com "frontend engineer" react`

## Query Categories

### Priority 1: Frontend Engineering (Remote)

Core direction — React/Next.js/TypeScript roles, fully remote worldwide.

```
linkedin: search -q "Frontend Engineer" -l "Remote" --remote remote --jobage 14
linkedin: search -q "Frontend Developer" -l "Remote" --remote remote --jobage 14
linkedin: search -q "React Next.js" -l "Remote" --remote remote --jobage 14
freehire: search -q "frontend react" --remote remote --category frontend --jobage 14
freehire: search -q "next.js typescript" --remote remote --category frontend --jobage 14
```

### Priority 2: Full-Stack Engineering (Remote)

Roles that combine frontend depth with Node.js/API work — a natural fit given NestJS + PostgreSQL experience.

```
linkedin: search -q "Full Stack Engineer" -l "Remote" --remote remote --jobage 14
linkedin: search -q "Full Stack Developer React" -l "Remote" --remote remote --jobage 14
freehire: search -q "fullstack react typescript" --remote remote --category fullstack --jobage 14
freehire: search -q "react node.js" --remote remote --category fullstack --jobage 14
```

### Priority 3: Software Engineer (Remote, Frontend-leaning)

Broader "Software Engineer" title at companies where frontend is the domain.

```
linkedin: search -q "Software Engineer React" -l "Remote" --remote remote --jobage 14
linkedin: search -q "Software Engineer TypeScript" -l "Remote" --remote remote --jobage 14
freehire: search -q "software engineer react" --remote remote --jobage 14
```

### Priority 4: Armenia On-site / Hybrid

Yerevan-based roles at product companies, startups, and tech hubs (e.g. Picsart, ServiceTitan, Coda, Renderforest, Krisp).

```
linkedin: search -q "Frontend Engineer" -l "Yerevan, Armenia" --jobage 14
linkedin: search -q "Frontend Developer" -l "Yerevan, Armenia" --jobage 14
linkedin: search -q "Software Engineer" -l "Yerevan, Armenia" --jobage 14
freehire: search -q "frontend engineer" --country AM --jobage 14
freehire: search -q "react developer" --country AM --jobage 14
```

## Location Filter

Acceptable for Davit (no relocation):
- **Remote / Worldwide** — ✓ primary target
- **Yerevan, Armenia** — ✓ on-site/hybrid acceptable
- **Other Armenia cities** — ✓ acceptable with commute context
- **Hybrid with occasional EU travel** — FLAG (discuss; travel to Luxembourg precedent exists)
- **Relocation required** — ✗ FAIL deal-breaker

## Language Filter

| Language | Level | Gate behavior |
|----------|-------|---------------|
| English  | Professional | PASS for all English-language requirements |
| Armenian | Native | PASS for Armenian-language requirements |

A posting requiring a language not in this table → FAIL (hard stop, per Language Gate in `04-job-evaluation.md`).

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. Flag postings where the date cannot be determined.

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape AI" → Priority 1/2 queries + custom `"AI engineer" react`, `"LLM" frontend`, `"AI product" typescript`
- "/scrape Armenia" → Priority 4 queries only
- "/scrape remote" → Priority 1-3 queries only
