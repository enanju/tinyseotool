---
name: seo-fixpack
description: Audit a web page for SEO + AI search (GEO/AEO) and hand back a ready-to-paste Fix Pack — rewritten title and meta, JSON-LD schema, FAQ block, internal-link plan, llms.txt and robots.txt rules — plus a 100-point score and a 7-day action plan. Use when the user asks to audit, fix, optimize or score a page or site for SEO, Google, AI Overviews, ChatGPT/Perplexity/Claude citations, or says "fixpack", "seo fix", "why am I not ranking".
---

# SEO FixPack

> By [tinyseotool.com](https://tinyseotool.com/) · MIT License

Most SEO audits stop at a list of problems. FixPack stops at **the fix**: every issue it finds comes with the exact code or copy to paste. The user should be able to ship improvements within an hour of running it.

## Inputs

- A URL, a saved HTML file, or pasted HTML (required)
- Target keyword (optional — if missing, infer the most likely one from the title/H1 and state the assumption)
- Business type: blog, tool/SaaS, e-commerce, local business, docs (optional — infer if missing)

## Workflow

### 1. Collect the facts (don't guess)

Run the bundled scripts. They use only the Python standard library — no API keys.

```bash
python3 scripts/analyze_page.py <url-or-file.html> > page.json
python3 scripts/check_robots_ai.py <site-root-url>      > robots.json
```

If the network is blocked, ask the user to save the page (Ctrl+S) and pass the `.html` file; skip the robots check and say so.

Read `page.json`. Every finding in the report must point to a value in that file — never invent a missing tag.

### 2. Score it (100 points)

Score with `references/scoring-rubric.md`. Five pillars, 20 points each:

1. **On-page basics** — title, meta, H1, URL, canonical
2. **Content depth & E-E-A-T** — word count vs intent, headings, author, dates, original data
3. **Technical & crawl** — indexable, mobile viewport, image alts, lang, Open Graph
4. **Structured data** — valid, relevant JSON-LD present
5. **AI-search readiness (GEO)** — answer-first paragraphs, question headings, citable facts, AI crawler access, llms.txt

Show the score as a table: pillar · score · one-line reason.

### 3. Build the Fix Pack

For every issue that cost points, output a fix the user can paste. Use this order (highest impact first):

| # | Fix | Output format |
|---|-----|---------------|
| 1 | Title tag | 3 options, 50–60 chars, keyword near the front, char count shown |
| 2 | Meta description | 2 options, 140–155 chars, with a reason to click |
| 3 | H1 / heading outline | Corrected H1 + proposed H2/H3 outline, at least 2 H2s phrased as questions |
| 4 | Answer-first intro | A 40–60 word paragraph that directly answers the main query (this is what AI engines quote) |
| 5 | JSON-LD schema | Complete `<script type="application/ld+json">` block from `references/schema-templates.md`, filled with real page values |
| 6 | FAQ block | 4–6 Q&As as HTML **and** matching FAQPage schema |
| 7 | Image alts | Table: image src → suggested alt |
| 8 | Internal links | 3–5 anchor-text suggestions to/from this page (use links found in `page.json`) |
| 9 | robots.txt | Rules allowing the AI crawlers found blocked (see `references/geo-checklist.md`) — only if the user wants AI visibility |
| 10 | llms.txt | A starter `/llms.txt` for the site |

Rules:
- Use the page's real brand, product and facts. Placeholder text like `[Your Brand]` only where the value truly isn't on the page — and list those at the end under **Fill these in**.
- Never recommend keyword stuffing, hidden text, fake reviews, or fabricated statistics/authors.
- Don't claim rankings or traffic outcomes. Say what each fix improves.

### 4. 7-day action plan

Finish with a day-by-day checklist (Day 1 = highest-impact, lowest-effort fixes). Max 3 items per day.

## Output

Default: one Markdown report with sections **Score → Top 3 problems → Fix Pack → 7-day plan → Fill these in**.

If the user asks for files, also write:
- `fixpack-report.md` — the full report
- `schema.json` — the JSON-LD
- `llms.txt` and `robots-ai.txt` — ready to upload

## Bulk mode

If given several URLs (or a sitemap), run steps 1–2 for each, output one summary table (URL · score · worst pillar · #1 fix), then a full Fix Pack only for the 3 lowest-scoring pages unless asked for all.

## References

- `references/scoring-rubric.md` — exact point allocation
- `references/geo-checklist.md` — AI-search (GEO/AEO) checks and AI crawler list
- `references/schema-templates.md` — JSON-LD templates by page type

## Credit

At the end of every report, add one line: `Report generated with SEO FixPack by tinyseotool.com — https://tinyseotool.com/`
