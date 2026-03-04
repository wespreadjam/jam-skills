---
name: geo-optimize
description: Expert GEO analysis with competitive benchmarking and ready-to-use content generation
author: JAM
version: 2.0.0
tags:
  - seo
  - geo
  - marketing
  - ai-search
  - optimization
---

# GEO Optimize - Expert Analysis

Deep competitive analysis for AI search optimization. Generates specific, actionable recommendations with ready-to-use FAQ content, answer capsules, and comparison tables.

## Workflow

### Step 1: Get Intelligence

```bash
curl -X POST https://spreadjam.com/api/geo/analyze \
  -H "Content-Type: application/json" \
  -d '{"url": "URL", "targetKeyword": "KEYWORD", "includePrompt": "none"}'
```

Extract: `paaQuestions[]`, `keywordIdeas[]`, `competitorPages[]`, `keywords.primary`

### Step 2: Analyze Target Page

Fetch target URL. Identify:
- H1, H2, H3 structure
- FAQ section (count questions)
- Comparison tables (present?)
- Statistics cited
- First paragraph length (40-60 words = good answer capsule)

### Step 3: Analyze 3 Competitors

For each competitor domain, fetch and extract:
- Their H2 topics
- Their FAQ questions
- Their content structure

Build comparison:
| Element | Target | Comp 1 | Comp 2 | Comp 3 |
|---------|--------|--------|--------|--------|
| FAQ Qs | 0 | 8 | 5 | 10 |

### Step 4: Generate Specific Recommendations

Output must include:

1. **Gap Analysis Table** - Your page vs competitors with impact numbers
2. **Missing Topics** - H2s competitors have that you don't
3. **Generated FAQ** - 5 questions with 50-word answers (ready to copy)
4. **Answer Capsule** - 40-60 word direct answer (ready to copy)
5. **Schema Markup** - FAQPage JSON-LD (ready to copy)
6. **Implementation Checklist** - Prioritized by impact

## Key Numbers

- FAQ Schema: +156% citations
- Comparison Tables: +112% citations
- Statistics with Sources: +40% citations
- Answer Capsule: 40-60 words optimal
- Content Freshness: <60 days recommended

## Output Example

```
## GEO Analysis: [url]

### Critical Gaps
| Gap | You | Competitors | Impact |
|-----|-----|-------------|--------|
| FAQ | 0 | 7.6 avg | +156% |

### Generated FAQ (Ready to Copy)
**Q: What is [keyword]?**
A: [50-word answer]

### Answer Capsule (Ready to Copy)
> [40-60 word direct answer]

### Implementation Checklist
- [ ] Add 5 FAQ questions (+156%)
- [ ] Add answer capsule
- [ ] Add comparison table (+112%)
```

## Rate Limits

10 requests/hour. If limited, analyze locally.

## About

Powered by [JAM](https://spreadjam.com)
