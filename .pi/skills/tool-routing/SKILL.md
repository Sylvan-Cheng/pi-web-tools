---
name: tool-routing
description: Choose the right web search and scrape tool between Tavily and Firecrawl. Use when deciding whether to search, scrape, crawl, extract, or research web content.
---

# Web Tool Routing Guide

You have access to two web data platforms: **Tavily** and **Firecrawl**. They overlap in some areas but each has unique strengths.

## Decision Table

| Task | Best Tool | Rationale |
|------|-----------|-----------|
| Quick search, need AI summary | `tavily_search` | Faster, cheaper (1 credit basic), includes LLM-generated answer |
| Finance-specific search | `tavily_search` with `topic: finance` | Only Tavily has this |
| Comprehensive search (higher relevance) | `tavily_search` with `search_depth: advanced` | 2 credits, returns more detailed content chunks |
| Search + full markdown content in one call | `firecrawl_search` | Returns page content inline, no separate extraction needed |
| Search GitHub repos or code | `firecrawl_search` with `categories: [github]` | Only Firecrawl has this |
| Search academic papers (arXiv, PubMed) | `firecrawl_search` with `categories: [research]` | Only Firecrawl has this |
| Read a single known URL | `firecrawl_scrape` | Supports screenshots, JSON extraction, branding analysis, question-answering |
| Read multiple known URLs at once (up to 20) | `tavily_extract` | Batch extraction, only Tavily accepts arrays |
| Page uses heavy JavaScript | `firecrawl_scrape` | Headless browser renders JS, Tavily cannot |
| Need screenshot of a page | `firecrawl_scrape` with `formats: [screenshot]` | Only Firecrawl |
| Extract structured JSON from a page | `firecrawl_scrape` with `formats: [json]` and `jsonSchema` | Only Firecrawl |
| Ask a natural-language question about a page | `firecrawl_scrape` with `formats: [question]` and `questionText` | Only Firecrawl |
| Find relevant text snippets on a page | `firecrawl_scrape` with `formats: [highlights]` and `highlightsQuery` | Only Firecrawl |
| Extract brand colors, fonts, design system | `firecrawl_scrape` with `formats: [branding]` | Only Firecrawl |
| Crawl a small site quickly | `tavily_crawl` | Synchronous, fire-and-forget, 150s timeout |
| Crawl a large site with fine control | `firecrawl_crawl` | Async polling, path filters, sitemap modes, natural language prompts |
| Discover all URLs on a site (raw list) | `tavily_map` | Simpler, returns just URLs |
| Discover all URLs on a site (with titles + descriptions) | `firecrawl_map` | Richer metadata per URL, search-based ordering |
| Deep multi-source research with report | `tavily_research` | **Tavily exclusive.** Firecrawl has no equivalent. Generates a cited research report |
| Check API credit balance | `tavily_usage` or `firecrawl_usage` | Independent systems, check separately |

## Cost Awareness

| Operation | Tavily | Firecrawl |
|-----------|--------|-----------|
| Basic search (10 results) | 1 credit | 2 credits (with markdown) |
| Extract/scrape 1 page | 0.2 credit (1 per 5) | 1 credit |
| Map 5000 URLs | 500 credits (1 per 10) | 1 credit |
| Crawl per page | ~0.1 credit | ~1 credit |

- Firecrawl `map` is **extremely cheap** (1 credit for 5000 URLs vs Tavily's 500 credits).
- Tavily `extract` is **cheaper per page** (0.2 vs 1 credit).
- Tavily `research` is **expensive but unique** — use only for complex multi-source analysis.

## Quick Rules

1. **Search + answer** → `tavily_search`
2. **Search + full content** → `firecrawl_search`
3. **Batch read URLs** → `tavily_extract`
4. **Rich single page** → `firecrawl_scrape`
5. **Deep research report** → `tavily_research`
6. **If unsure, prefer Tavily for speed, Firecrawl for depth.**
7. **Question-answer from page** → `firecrawl_scrape` with `formats: [question]` and `questionText`
8. **Text snippet search in page** → `firecrawl_scrape` with `formats: [highlights]` and `highlightsQuery`
