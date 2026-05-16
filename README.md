# pi-web-tools

pi coding agent web capabilities — extensions and skills for web search, scraping, crawling, and research.

## Extensions

| Extension | Description | Tools |
|-----------|-------------|-------|
| [firecrawl](https://github.com/Sylvan-Cheng/pi-firecrawl-extension) | Web scraping & search via Firecrawl v2 API | `firecrawl_scrape`, `firecrawl_search`, `firecrawl_crawl`, `firecrawl_map`, `firecrawl_usage` |
| [tavily](https://github.com/Sylvan-Cheng/pi-tavily-extension) | Web search & research via Tavily API | `tavily_search`, `tavily_extract`, `tavily_crawl`, `tavily_map`, `tavily_research`, `tavily_usage` |

## Skills

| Skill | Description |
|-------|-------------|
| [tool-routing](.pi/skills/tool-routing/SKILL.md) | Guides tool selection between Tavily and Firecrawl |

## Setup

```bash
# Clone with submodules
git clone --recurse-submodules https://github.com/Sylvan-Cheng/pi-web-tools.git

# Set API keys
export FIRECRAWL_API_KEY="fc-..."
export TAVILY_API_KEY="tvly-..."

# Copy to pi extensions directory
cp -r .pi/extensions/* ~/.pi/agent/extensions/
cp -r .pi/skills/* ~/.pi/agent/skills/
```
