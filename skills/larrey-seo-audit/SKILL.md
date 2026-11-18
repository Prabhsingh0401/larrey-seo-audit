---
name: larrey-seo-audit
description: Larrey is an SEO and AI search audit that examines a website like a patient (intake, vitals, a seven-system exam) and then triages what to fix first. Use when the user asks for an SEO audit, why a page or site isn't ranking or lost traffic, a technical SEO review, keyword research, on-page or content optimisation, a pre-launch SEO check, or whether ChatGPT, Claude, Perplexity or Google AI Overviews can read, cite and recommend their site. Works on a live URL, a website codebase, or both.
---

# Larrey: SEO & AI Search Audit

Named after Dominique-Jean Larrey (1766–1842), the surgeon who invented triage: treat the most dangerously wounded first, without regard to rank. Every website has dozens of things wrong. Your job is to find the few that cost the most and put them at the top.

## How a Larrey audit runs

1. **Intake.** Find the complaint before examining anything: a page that won't rank, a traffic drop, a new site, "AI never mentions us", or a general check-up. Note what you have to work with: a URL, a codebase, connected data (Search Console, GA4, a keyword or backlink tool). If the complaint is unclear, ask one question, then start.
2. **Vitals.** Read the numbers before touching anything: run AN-01 and AN-02 from `exams/analytics.md` if data is available. If not, record vitals as Untested and continue.
3. **Examine.** Load only the exam files the complaint points to (see Routing). A full check-up loads all seven.
4. **Triage.** Give every finding exactly one level (see Triage).
5. **Treat.** For each finding, write the fix: what, where (URL or `file:line`), and why. In a codebase, make the fix if the user asked for fixes; otherwise propose it.
6. **Follow up.** Write down what you expect to change, by how much, and when to re-check.

## Routing

| Complaint | Examine, in this order |
|---|---|
| Full audit / check-up | technical, on-page, content, ai-search, keyword-research, off-page, analytics |
| "This page doesn't rank" | keyword-research (intent), on-page, content, technical |
| Traffic dropped | analytics, technical, then whatever analytics points to |
| "ChatGPT / AI Overviews don't cite us" | ai-search, technical, content, off-page |
| New site or pre-launch | technical, on-page |
| "What should we write next?" | keyword-research, content |
| Local business | off-page (OF-05), on-page, technical |

## The seven systems

| Exam file | Prefix | The one question it answers |
|---|---|---|
| `exams/keyword-research.md` | KW | What is our audience actually typing, and is it worth a page? |
| `exams/on-page.md` | OP | Does this page answer the question in its first sentence? |
| `exams/technical.md` | TE | Can a crawler, and an AI assistant, actually read this? |
| `exams/content.md` | CT | What does this page say that no other page says? |
| `exams/off-page.md` | OF | Who else says we exist? |
| `exams/analytics.md` | AN | What did we change, and what moved because of it? |
| `exams/ai-search.md` | AI | Are we found and recommended by assistants? |

Every check has four parts: **Question**, **Test**, **Healthy**, and (where data may be missing) **If you can't test**.

## Triage

| Level | Meaning | Examples |
|---|---|---|
| 🔴 Critical | Stops pages being crawled, indexed or read | noindex on key pages, content missing from raw HTML, robots.txt or a firewall blocking crawlers, a sitemap full of 404s |
| 🟠 Urgent | Costing clicks or citations right now | title doesn't match intent, positions 1–5 with low CTR, structured data that contradicts the page |
| 🟢 Routine | Worth doing; schedule it | alt text, internal link anchors, refreshing an old post |
| ⚪ Untested | Needed data we didn't have | volume without a keyword tool, backlinks without a backlink tool |

Within a level, rank by: pages affected × traffic or value of those pages ÷ effort. A template fix that repairs 300 pages beats a perfect fix on one.

## Rules

1. **Evidence or nothing.** Every finding cites what you saw: a URL, a `file:line`, a snippet of fetched HTML, or a number from a named tool.
2. **Never invent metrics.** Search volume, keyword difficulty, traffic, rankings and backlinks come from a connected tool or the user. Otherwise they are Untested. Never estimate them from memory.
3. **One tool per metric.** Difficulty and rank scores are vendor scores and don't compare across tools. Name the source next to every number.
4. **Raw HTML is the truth.** AI crawlers generally don't run JavaScript. Judge what the server sends, not what a browser renders.
5. **No AI-SEO folklore.** Google says its generative AI features build on core Search systems and need no special AI files or schema. Never sell llms.txt or "AI markup" as a fix.
6. **Fix at the source.** In a codebase, fix the component, template, route config or data that generates the tag, not the built output.
7. **Predict, then measure.** Every treatment leaves with a prediction and a re-check date.
8. **Load what you need.** Read exam files only for systems you are examining, and `references/sources.md` only when citing a statistic.

## With a codebase

Before the technical exam:
- Identify the framework and the rendering mode of each route (static, server-rendered, client-rendered). It decides most of TE-02.
- Find where titles, meta descriptions, canonicals, robots meta, JSON-LD, the sitemap and robots.txt are generated.
- If analytics shows a drop, run `git log` around that date. Deploys explain more drops than algorithm updates.

## With only a URL

Fetch pages without rendering to see the raw HTML. Fetch `/robots.txt` and the sitemap. If web search is available, look at what currently ranks for the target query. Sample the homepage, one page of each template type (article, product, category, docs) and every page the complaint names.

## Report format

```
# Larrey report: {site}, {date}

**Complaint:** {one line}
**Examined:** {systems}   **Data available:** {tools, or "none"}
**Vitals:** {clicks, impressions, CTR, avg position, trend, source}, or Untested

## Triage
| # | Level | Finding | Evidence | Fix | Effort |
|---|---|---|---|---|---|
| 1 | 🔴 | ... | ... | ... | S / M / L |

## By system
### Technical (1 🔴, 2 🟢)
- **TE-02 Crawling and indexing** 🔴 Finding. Evidence. Fix.

## Untested
What couldn't be checked, and what would unlock it.

## Follow-up
Prediction: {what should move, by how much}. Re-check: {date}.
```

Lead with the triage table. Keep each finding to one or two sentences.