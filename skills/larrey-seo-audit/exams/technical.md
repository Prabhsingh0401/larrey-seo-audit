# Technical exam (TE)

> Can a crawler, and an AI assistant, actually read this?

### TE-01 Site structure
**Question:** Can someone reach any page in three clicks from the homepage?
**Test:** Map navigation and hub pages. In a codebase, read the routes. Check URLs are readable, lowercase and consistent (one trailing-slash style).
**Healthy:** Important pages within three clicks. No orphaned sections.

### TE-02 Crawling and indexing
**Question:** Is our content in the raw HTML?
**Test:** Fetch the page without running JavaScript (`curl -sL URL` or a non-rendering fetch). Confirm the H1, body text and internal links are in the response. Check the HTTP status, `<meta name="robots">`, the `X-Robots-Tag` header and the canonical. In a codebase, check each route's rendering mode: a page that loads its main content client-side, or ships an empty root `<div>`, fails.
**Healthy:** 200 status, indexable, self-referencing canonical, all content and links in the first response.
**Why it matters:** The crawlers behind ChatGPT, Claude and Perplexity generally don't execute JavaScript. If it isn't in the HTML, they don't see it.

### TE-03 Speed
**Question:** Is the thing a visitor came for visible before anything else loads?
**Test:** Use PageSpeed Insights or CrUX field data if available. "Good" at the 75th percentile: LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1. In a codebase: the LCP image isn't lazy-loaded and has priority, fonts don't block rendering, third-party scripts load late.
**Healthy:** All three in the good range on mobile.
**If you can't test:** Review the code for those causes and mark the metrics Untested.

### TE-04 Mobile
**Question:** Does it work one-handed on a phone, on mobile data?
**Test:** Viewport meta present, no horizontal scroll, usable tap targets, the same content on mobile as desktop (Google indexes the mobile version), reasonable page weight.
**Healthy:** Nothing important is hidden or missing on mobile.

### TE-05 Sitemap and robots
**Question:** Does the sitemap list only pages we would be happy to rank?
**Test:** Fetch `/robots.txt` and every sitemap. Each sitemap URL should return 200, be canonical and be indexable. robots.txt must not block CSS, JS or key sections. Check rules for AI crawlers and confirm they are deliberate: `GPTBot`, `OAI-SearchBot`, `ChatGPT-User`, `ClaudeBot`, `Claude-SearchBot`, `Claude-User`, `PerplexityBot`, `Google-Extended` (this one controls Gemini's use of content, not Search ranking). Ask about CDN or firewall bot settings: a firewall can block a crawler that robots.txt allows.
**Healthy:** A clean sitemap, and robots rules that match what the user actually wants.

### TE-06 Structured data
**Question:** Does the structured data match the visible text?
**Test:** Extract the JSON-LD. Every claim in it (name, price, rating, author, date, FAQ answer) must appear on the visible page. Use types Google supports. Validate the syntax.
**Healthy:** Markup and page agree. In a codebase, the best fix is generating JSON-LD from the same data that renders the page.
**Why it matters:** Google requires structured data to describe visible content. Markup that only exists in code does not count.

### TE-07 Fix what's broken
**Question:** Which broken thing is costing us the most, and how would we know?
**Test:** Find 4xx and 5xx pages, redirect chains, broken internal links, duplicate pages without canonicals, and mixed content. With Search Console, read the "not indexed" reasons in the page indexing report. Rank by the traffic or value of the affected pages.
**Healthy:** Nothing important is broken. This check feeds triage directly.