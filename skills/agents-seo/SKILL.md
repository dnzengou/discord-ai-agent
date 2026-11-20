---
name: agents-seo
description: Make a site AI-agent discoverable and AI-crawler friendly. Adds llms.txt, robots.txt (with explicit allows for GPTBot/ClaudeBot/Perplexity/Google-Extended/etc.), sitemap.xml, /.well-known/ai-plugin.json, OpenGraph/Twitter cards, canonical URL, and JSON-LD (SoftwareApplication + FAQPage + HowTo). Use whenever a landing page or docs site should be discoverable by LLM search, retrieved by agentic browsers, or cite-worthy in AI answers. Triggers include "AI SEO", "llms.txt", "agentic SEO", "LLM discoverability", "make it detectable by AI", "ChatGPT / Claude / Perplexity findable".
license: Apache-2.0
---

# Agents-SEO: SEO for the agentic web

Classic SEO ranks pages for humans scrolling. Agents-SEO makes a page retrievable, parseable, and cite-worthy for LLM search and agent browsers.

## The seven artifacts (ship all of them)

1. **`/llms.txt`** — short, human-readable Markdown summary of the site. H1 title, one-line value prop, "Who it's for", "Quick start", "Key capabilities", "For AI agents reading this" (canonical URLs to deeper docs). Keep it under 2 KB.
2. **`/robots.txt`** — explicit `Allow: /` for the top AI user-agents: `GPTBot`, `ChatGPT-User`, `OAI-SearchBot`, `ClaudeBot`, `Claude-Web`, `anthropic-ai`, `Google-Extended`, `GoogleOther`, `PerplexityBot`, `Perplexity-User`, `CCBot`, `Bytespider`, `Amazonbot`, `Applebot-Extended`, `Meta-ExternalAgent`, `cohere-ai`, `MistralAI-User`, `DuckAssistBot`, `YouBot`, `Diffbot`. Include `Sitemap:` line.
3. **`/sitemap.xml`** — every page an agent should consider, plus `/llms.txt` itself, with `lastmod`.
4. **`/.well-known/ai-plugin.json`** — ChatGPT-plugin-manifest shape. Even where the API isn't consumed, agents parse it as a capability card.
5. **`<head>` metadata** — canonical URL, OpenGraph, Twitter card, `<link rel="alternate" type="text/plain" href="/llms.txt">`, `<meta name="robots" content="index,follow,max-image-preview:large">`.
6. **JSON-LD structured data** — minimum `SoftwareApplication` (or `WebSite`), plus `FAQPage` and `HowTo` for installable products. These show up verbatim in LLM answers.
7. **Semantic HTML** — one `<h1>`, descriptive `<h2>`s, real links (not JS-only), short paragraphs. Agent extractors cost-cut aggressively; don't hide answers inside widgets.

## Writing rules for LLM-crawled content

- **Answer-first**: the first sentence of every section is the answer. The rest is proof.
- **Numbers over adjectives**: "64 tools, ~2 min setup" beats "powerful suite, fast onboarding."
- **Canonical anchors**: every claim links to its source (GitHub, docs, changelog).
- **No walls of CSS**: agents strip visuals; what remains should still make the sale.
- **One idea per paragraph**: easier to quote without butchering.

## Checklist (ship-ready)

- [ ] `/llms.txt` exists, under 2 KB, answer-first
- [ ] `/robots.txt` explicitly allows top AI crawlers and names the sitemap
- [ ] `/sitemap.xml` is valid and includes `/llms.txt`
- [ ] `/.well-known/ai-plugin.json` parses as JSON and names capabilities
- [ ] `<link rel="canonical">` on every HTML page
- [ ] OpenGraph title/description/image + Twitter card tags
- [ ] JSON-LD `SoftwareApplication` + `FAQPage` + `HowTo` where applicable
- [ ] Favicon and an OG image (≥ 1200×630)
- [ ] First screen states what, who, how long — without needing JavaScript

## Why this works

LLM search engines (OpenAI SearchGPT, Perplexity, Google AI Overviews, Claude Web) retrieve pages, extract structured answers, and cite URLs. They favor pages that (a) say what they are in the first 200 tokens, (b) expose structured metadata, and (c) don't block their crawlers. The seven artifacts above cover all three. The `llms.txt` convention is emerging as the de-facto standard for a "here's the whole site in 2 KB" signal — ship it even if no single engine mandates it yet; it compounds as adoption grows.

## Reuse this skill

Copy `skills/agents-seo/` into any repo and point its SKILL.md at that project's site. The per-site values that change: canonical domain, product name/description, capability list, FAQ answers, HowTo steps.
