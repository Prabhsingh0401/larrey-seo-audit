# Analytics exam (AN)

> What did we change, and what moved because of it?

### AN-01 Traffic
**Question:** Which single number would tell us this month went well?
**Test:** Agree on one number with the user: organic sessions to key pages, or organic conversions. Compare with the previous period and the same period last year.
**Healthy:** One agreed number, trended, with seasonality noted.
**If you can't test:** Ask for a GA4 or Search Console export, or mark Untested.

### AN-02 Search Console
**Question:** Are impressions growing while clicks stay flat, and do we know why?
**Test:** Clicks, impressions, CTR and position over 3, 6 and 12 months, split by query and by page. Read the pattern:
- Impressions up, clicks flat: new rankings at low positions, SERP features or AI answers taking clicks, or weak titles.
- Positions 1–5 with low CTR: titles and descriptions (OP-02, OP-03).
- A sudden drop: match the date against deploys (`git log`) before blaming an algorithm update.
Check the Generative AI performance report too, if the property has one.
**Healthy:** Every big movement has an explanation.

### AN-03 Rankings
**Question:** Has the baseline moved, or the ruler?
**Test:** Use one rank tracker. Search Console's average position is impression-weighted: it falls when we start appearing for many new low-position queries, even if nothing got worse.
**Healthy:** Rank changes are explained before anyone reacts to them.

### AN-04 User behaviour
**Question:** Are people finding the bit they came for?
**Test:** GA4 engagement rate by landing page. High traffic with low engagement usually means an intent mismatch (KW-04) or a slow page (TE-03).
**Healthy:** Key landing pages engage at or above the site average.

### AN-05 Conversions
**Question:** Are we counting leads, or leads that became money?
**Test:** Key events are set up in GA4 and firing. In a codebase, find the tracking code and confirm the events exist. Ask whether leads are tied to revenue anywhere.
**Healthy:** Organic conversions are counted and trusted.

### AN-06 Review and repeat
**Question:** What did we predict would happen before we changed it?
**Test:** Keep a change log: date, change, prediction, re-check date. Build it from git history where possible.
**Healthy:** Every change from this audit leaves with a prediction.