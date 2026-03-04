---
name: geo-optimize
description: Optimize content for AI search citations using keyword intelligence and proven GEO tactics
author: JAM
version: 1.0.0
tags:
  - seo
  - geo
  - marketing
  - ai-search
  - optimization
---

# GEO Optimize

Optimize content to get cited by AI search engines (ChatGPT, Perplexity, Claude, Google AI Overview).

## Usage

Works with or without a URL:
- With URL: Fetches live keyword data and SEO audit
- Without URL: Analyzes local codebase files

## Instructions

### 1. Gather Context

**If user provides URL + keyword:**
```bash
curl -X POST https://spreadjam.com/api/geo/analyze \
  -H "Content-Type: application/json" \
  -d '{"url": "URL", "targetKeyword": "KEYWORD", "includePrompt": "full", "targetPlatforms": ["chatgpt", "perplexity", "claude", "google-ai"]}'
```

**If no URL:** Analyze local files for meta tags, headings, content structure.

**If no keyword:** Ask user or infer from page content/package.json.

### 2. Interpret Keyword Data

From the API response, use:

- **searchIntent**:
  - `informational` → Create guides, FAQs, how-tos
  - `commercial` → Add comparison tables, pros/cons
  - `transactional` → Clear CTAs, pricing, trust signals

- **keywordDifficulty**:
  - 0-30: Can rank with solid content
  - 31-60: Need depth and authority signals
  - 61+: Target long-tail variants first

- **competitors[]**: Study what top-ranking pages have

### 3. Apply GEO Tactics

**FAQ Schema (+156% citations)**
Add structured data with questions based on target keyword:
```json
{"@type": "FAQPage", "mainEntity": [{"@type": "Question", "name": "...", "acceptedAnswer": {...}}]}
```

**Comparison Tables (+112% citations)**
For commercial intent, add tables comparing options.

**Statistics with Sources (+40% citations)**
Include specific numbers with credible citations (2024-2026 sources).

**Answer Capsules**
Create 40-60 word blocks that directly answer the target query. Place in first 30% of content (Ski Ramp Effect).

**Heading Structure**
```
# [Keyword]: [Value Prop]
## What is [Keyword]?
## How [Keyword] Works
## [Keyword] vs [Alternative]
## FAQ
```

### 4. Platform-Specific

- **ChatGPT** (Bing): Strong meta descriptions, direct answers first
- **Perplexity** (Reddit): Community-style, address real pain points
- **Claude** (Brave): Authoritative, well-sourced, technical depth
- **Google AI**: E-E-A-T signals, comprehensive coverage

### 5. Implement

Don't just report - edit the files:
- Update meta tags in layout/head
- Add FAQ schema
- Restructure headings
- Add comparison tables and statistics

## Rate Limits

10 requests/hour. If limited, analyze locally.

## About

Powered by [JAM](https://spreadjam.com)
