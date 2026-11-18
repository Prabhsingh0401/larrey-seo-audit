# On-page exam (OP)

> Does this page answer the question in its first sentence?

### OP-01 Keyword placement
**Question:** Does the page title match how people ask the question?
**Test:** Compare the target query with the `<title>`, H1, URL slug and first sentence.
**Healthy:** The main phrase appears naturally in all four, and the first sentence answers it.

### OP-02 Title tag
**Question:** Is our title close to the way the question is asked?
**Test:** Read `<title>` from raw HTML. Check it is unique across the site, leads with the topic and fits about 60 characters. In a codebase, find where titles are generated and flag templates that produce duplicates.
**Healthy:** Unique, specific, phrased like the query. Pages ChatGPT cited had titles measurably closer to the prompt than pages it skipped (see sources).

### OP-03 Meta description
**Question:** Would this make someone choose us over the result above?
**Test:** Present, unique, specific, roughly 150–160 characters, with a concrete outcome or number. With Search Console, list pages in positions 1–5 whose CTR is well below the site average: they are rewrite candidates.
**Healthy:** It sells the click. Google may rewrite it; it is still worth writing.

### OP-04 Header tags
**Question:** Where a heading can be a question, is it, and is it answered in the sentence right under it?
**Test:** Extract the H1–H3 outline. One H1. Headings in the reader's words. Read the first sentence under each H2.
**Healthy:** The outline alone shows what the page answers, and each section opens with the answer.

### OP-05 Unique information
**Question:** How many data points does this page carry that the pages above it do not?
**Test:** If web search is available, compare with the top three results. Count original numbers, examples, screenshots, code and first-hand detail only we have.
**Healthy:** At least one thing a reader can't get from the results above us.

### OP-06 Images
**Question:** Is the image indexable, with real alt text, or hidden behind JavaScript?
**Test:** `<img>` is in the raw HTML with a real `src`. Alt text describes the image (not a filename, not empty on content images). Width and height are set, the format is modern, the file size is sensible.
**Healthy:** Every content image passes. Decorative images use `alt=""`.

### OP-07 Internal linking
**Question:** Does the anchor text match the title of the page it points to?
**Test:** Collect internal links (crawl, or grep the codebase). Flag "click here" and "read more" anchors, important pages with few inbound links, and sitemap pages nothing links to.
**Healthy:** Descriptive anchors, no orphan pages, key pages linked from navigation or hubs.