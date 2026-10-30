# 🔧 SEO FixPack — a Claude Skill that hands you the fix, not just the problem

**By [tinyseotool.com](https://tinyseotool.com/)** — free SEO tools for everyone.

Most SEO audits give you a list of 50 problems and leave you alone with them.
**SEO FixPack** audits a page for Google **and** AI search (ChatGPT, Perplexity, Claude, Google AI Overviews) — then gives you **ready-to-paste fixes** for every issue it finds.

```
You:    audit https://mysite.com/tool for "word counter"
Claude: Score 58/100 (D) → Top 3 problems → Fix Pack (title, meta, schema, FAQ, llms.txt…) → 7-day plan
```

## What you get

| | |
|---|---|
| 📊 **100-point score** | 5 pillars: On-page · Content & E-E-A-T · Technical · Structured data · AI-search (GEO) |
| ✍️ **Title & meta rewrites** | 3 title options + 2 meta options, character counts included |
| 🧩 **JSON-LD schema** | Filled with your page's real values — Article, WebApplication, Product, LocalBusiness, FAQ, Breadcrumb |
| ❓ **FAQ block** | HTML + matching FAQPage schema |
| 🤖 **AI-search kit** | Answer-first intro paragraph, `llms.txt`, `robots.txt` rules for GPTBot / ClaudeBot / PerplexityBot |
| 🔗 **Internal link plan** | Anchor text suggestions from links already on your site |
| 📅 **7-day action plan** | Max 3 tasks a day, highest impact first |
| 📦 **Bulk mode** | Score many URLs, full Fix Pack for the 3 weakest |

**No API keys. No paid tools.** The bundled scripts use only the Python standard library.

## Install

**Claude.ai / Claude desktop app**
1. Download `seo-fixpack.zip` from [Releases](../../releases)
2. Settings → Capabilities (Skills) → Upload skill → choose the ZIP

**Claude Code**
```bash
git clone https://github.com/tinyseotool/seo-fixpack.git ~/.claude/skills/seo-fixpack
```

## Use it

Just ask in plain words:
- "Audit https://example.com/blog/post for SEO"
- "Why isn't this page ranking? Give me a fixpack"
- "Make this page AI-search ready" (paste HTML)
- "Score these 10 URLs and fix the worst ones"

## What's inside

```
seo-fixpack/
├── SKILL.md                     # the workflow Claude follows
├── scripts/
│   ├── analyze_page.py          # extracts title, meta, headings, schema, links, images…
│   └── check_robots_ai.py       # checks 15 AI/search crawlers + llms.txt
└── references/
    ├── scoring-rubric.md        # exact 100-point rubric
    ├── geo-checklist.md         # AI-search (GEO/AEO) checks + crawler list
    └── schema-templates.md      # JSON-LD templates by page type
```

Run the scripts on their own too:
```bash
python3 scripts/analyze_page.py https://example.com > page.json
python3 scripts/check_robots_ai.py https://example.com
```

## Principles
- **Facts first** — every finding comes from the parsed page, not guesses.
- **White-hat only** — no keyword stuffing, fake reviews, or invented stats.
- **No fake promises** — it says what each fix improves, never "you'll rank #1".

## About
SEO FixPack is made and maintained by **[tinyseotool.com](https://tinyseotool.com/)** — free online SEO tools: keyword, meta, schema, robots.txt and more. Need to check a page in the browser instead? Try the tools at [tinyseotool.com](https://tinyseotool.com/).

## License
MIT © [tinyseotool.com](https://tinyseotool.com/) — use it, fork it, ship it. ⭐ Star the repo if it saved you time.
