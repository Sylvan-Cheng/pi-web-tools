> ## Documentation Index
> Fetch the complete documentation index at: https://docs.tavily.com/llms.txt
> Use this file to discover all available pages before exploring further.

# Introduction

> Easily integrate our APIs with your services.

## Base URL

The base URL for all requests to the Tavily API is:

```plaintext theme={null}
https://api.tavily.com
```

## Authentication

All Tavily endpoints are authenticated using API keys.
[Get your free API key](https://app.tavily.com).

```bash theme={null}
curl -X POST https://api.tavily.com/search \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer tvly-YOUR_API_KEY" \
  -d '{"query": "Who is Leo Messi?"}'
```

## Endpoints

<CardGroup cols={2}>
  <Card icon="magnifying-glass" horizontal href="/documentation/api-reference/endpoint/search">
    **`/search`**

    Tavily's powerful web search API.
  </Card>

  <Card icon="file-lines" horizontal href="/documentation/api-reference/endpoint/extract">
    **`/extract`**

    Tavily's powerful content extraction API.
  </Card>

  <Card icon="circle-nodes" horizontal href="/documentation/api-reference/endpoint/crawl">
    `/crawl` , `/map`

    Tavily's intelligent sitegraph navigation and extraction tools.
  </Card>

  <Card icon="book" horizontal href="/documentation/api-reference/endpoint/research">
    **`/research`**

    Tavily's comprehensive research API for in-depth analysis.
  </Card>
</CardGroup>

## Project Tracking

You can optionally attach a Project ID to your API requests to organize and track usage by project. This is useful when a single API key is used across multiple projects or applications.

To attach a project to your request, add the `X-Project-ID` header:

```bash theme={null}
curl -X POST https://api.tavily.com/search \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer tvly-YOUR_API_KEY" \
  -H "X-Project-ID: your-project-id" \
  -d '{"query": "Who is Leo Messi?"}'
```

**Key features:**

* An API key can be associated with multiple projects
* Filter requests by project in the [/logs endpoint](/documentation/api-reference/endpoint/usage) and platform usage dashboard
* Helps organize and track where requests originate from

<Note>
  When using the SDKs, you can specify a project using the `project_id`
  parameter when instantiating the client, or by setting the `TAVILY_PROJECT`
  environment variable.
</Note>
