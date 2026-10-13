# GigTry — Public Documentation

**GigTry** ([https://www.gigtry.com](https://www.gigtry.com)) is a free AI tools marketplace running **89 production-grade AI tools** — text generation, image creation, video scripts, code helpers, audio tools, and productivity utilities — on a 100% free-tier serverless stack.

This repository holds the public documentation: the tool catalog, the public automation API reference, and the SEO/autonomy playbook highlights.

## Tool catalog

The complete, machine-readable catalog of all 89 tools (names, categories, endpoints, descriptions) lives in [`llms.txt`](./llms.txt) — also served live at `https://www.gigtry.com/llms.txt`.

Categories include: AI writing, image generation, video, code assistance, audio, business & marketing, education, and productivity.

## Public Automation API (v1)

GigTry exposes a read/write REST API for programmatic tool execution.

- Base URL: `https://www.gigtry.com/api/v1`
- Auth: API key (create one in your GigTry account console)
- Rate limits: per-key daily quota, enforced server-side
- Example:

```bash
curl -X POST https://www.gigtry.com/api/v1/tools/execute \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"tool": "blog-idea-generator", "input": {"topic": "remote work"}}'
```

Successful runs are reported server-side to GA4 (`api_tool_run`), so usage analytics work even when clients block browser scripts.

## Architecture notes (public)

- **Frontend/SSR**: Next.js 16 + React 19, deployed on Vercel free tier
- **Database**: Supabase Postgres (free tier)
- **AI inference**: Groq (primary), with keyless fallback chain
- **SEO surfaces**: XML sitemaps (679 static + 4,450 city URLs), RSS with engine articles, `llms.txt`, OpenSearch, 14 JSON-LD schema types
- **Autonomy**: daily content engine (live-trend research → generation → publication), heartbeat-driven job scheduler with atomic claim semantics, twice-daily cron triggers

## SEO / autonomy playbook highlights

1. Every page self-canonical; real 404 status codes; stable `lastmod` in sitemaps.
2. Content engine blends live trends (Google Trends, HN, Reddit — keyless) with a topic catalog, gated by platform-compliance rules and rate limits.
3. Server-side GA4 Measurement Protocol for engine events; client GA4 with Consent Mode v2; exception + web-vitals streaming to GA4 (free observability).
4. IndexNow pings on publish (Bing/Yandex/Seznam), sitemap ping cadence for Google.

## Links

- Website: https://www.gigtry.com
- Blog: https://www.gigtry.com/blog
- RSS: https://www.gigtry.com/feed.xml
- Tool catalog: https://www.gigtry.com/llms.txt

---

Issues in this repo are monitored by the GigTry automation. English-only project.
