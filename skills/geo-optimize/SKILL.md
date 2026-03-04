# GEO Optimize

Optimize content to get cited by AI search engines (ChatGPT, Perplexity, Claude, Google AI Overview). This skill combines real-time keyword intelligence with proven GEO tactics to help users improve their AI citation potential.

## Usage

```
/geo-optimize [url] [keyword]
/geo-optimize                     # Analyze current codebase
/geo-optimize "keyword"           # Analyze codebase for specific keyword
/geo-optimize https://... "kw"    # Analyze deployed URL
```

## Instructions

### Step 1: Determine Context

Check what the user provided:

**Has URL + keyword** → Call the API, then apply recommendations to codebase if available

**Has URL only** → Call API, extract keyword suggestions from the response

**Has keyword only** → Analyze local codebase files for that keyword

**Has neither** → Look for:
- `package.json` description or keywords
- README.md main topic
- Meta tags in layout/head files
- Ask user: "What topic do you want to rank for in AI search?"

### Step 2: Gather Data

**If URL is available**, call the JAM GEO API:

```bash
curl -X POST https://spreadjam.com/api/geo/analyze \
  -H "Content-Type: application/json" \
  -d '{
    "url": "URL_HERE",
    "targetKeyword": "KEYWORD_HERE",
    "includePrompt": "full",
    "targetPlatforms": ["chatgpt", "perplexity", "claude", "google-ai"]
  }'
```

The API returns:
- `audit.overallScore` - SEO health (0-100)
- `audit.issues[]` - Problems to fix (critical, warning, info)
- `audit.meta` - Current title, description, headings, word count
- `keywords.primary` - Search volume, difficulty, intent for target keyword
- `keywords.related[]` - Related keyword opportunities
- `keywords.competitors[]` - Top 10 domains ranking for this keyword
- `geoPrompt` - Full optimization guide
- `platformTips` - Platform-specific recommendations

**If no URL**, analyze local files:
- Find `app/layout.tsx`, `pages/_app.tsx`, or `index.html` for meta tags
- Find main content files (MDX, markdown, or page components)
- Extract: title, description, headings, approximate word count

### Step 3: Analyze Using Keyword Intelligence

Use the keyword data to inform your recommendations:

**Search Intent** (from `keywords.primary.searchIntent`):
- `informational` → User wants to learn. Create comprehensive guides, FAQs, how-tos.
- `commercial` → User is comparing options. Add comparison tables, pros/cons, alternatives.
- `transactional` → User wants to buy/act. Clear CTAs, pricing, trust signals.
- `navigational` → User looking for specific brand. Ensure brand mentions are clear.

**Keyword Difficulty** (from `keywords.primary.keywordDifficulty`):
- 0-30: Low competition. Can rank with solid content.
- 31-60: Medium. Need depth, E-E-A-T signals, backlinks.
- 61-100: High. Target long-tail variants, build authority first.

**Competitor Analysis** (from `keywords.competitors[]`):
- Identify what top-ranking pages have that this page lacks
- Note common patterns in competitor content structure
- Find gaps in competitor coverage to exploit

### Step 4: Apply GEO Tactics

Based on the data, implement these proven citation improvements:

#### A. FAQ Schema (+156% citation improvement)

If the content answers questions, add FAQ structured data:

```tsx
// Add to page or layout
<script type="application/ld+json">
{JSON.stringify({
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Question text here?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Answer text here."
      }
    }
  ]
})}
</script>
```

Generate questions from:
- The target keyword + "what is", "how to", "why", "best"
- Related keywords as question topics
- Competitor FAQ sections

#### B. Comparison Tables (+112% citation improvement)

For commercial intent keywords, add comparison tables:

```markdown
| Feature | Us | Competitor A | Competitor B |
|---------|-----|--------------|--------------|
| Price | $X | $Y | $Z |
| Key feature | Yes | No | Partial |
```

Use competitor data to identify comparison opportunities.

#### C. Statistics with Sources (+40% citation improvement)

Add credible statistics throughout content:

```markdown
According to [Source], 73% of users prefer X over Y.
```

- Cite recent studies (2024-2026)
- Link to authoritative sources
- Include specific numbers, not vague claims

#### D. Answer Capsules (optimal AI extraction)

Create 40-60 word summary blocks that directly answer the target query:

```markdown
**What is [keyword]?**

[Keyword] is [concise definition]. It helps [target audience]
achieve [outcome] by [mechanism]. Key benefits include [benefit 1],
[benefit 2], and [benefit 3].
```

Place these prominently - AI extracts from the first 30% of content most often (Ski Ramp Effect).

#### E. Heading Structure

Optimize headings for AI parsing:

```markdown
# [Primary Keyword]: [Value Proposition]

## What is [Primary Keyword]?
[Answer capsule]

## How [Primary Keyword] Works
[Explanation with steps]

## [Primary Keyword] vs [Competitor/Alternative]
[Comparison table]

## [Primary Keyword] FAQ
[FAQ section]
```

#### F. Platform-Specific Optimization

**ChatGPT (uses Bing)**
- Strong meta descriptions (Bing weighs them heavily)
- Clear, direct answers in first paragraph
- Bing Webmaster Tools submission

**Perplexity (Reddit-heavy)**
- Content that mirrors authentic community discussions
- Address real user pain points and questions
- Natural, conversational tone

**Claude (uses Brave)**
- Authoritative, well-researched content
- Clear source attribution
- Technical depth appreciated

**Google AI Overview**
- Existing Google ranking matters most
- E-E-A-T signals (expertise, experience, authority, trust)
- Comprehensive coverage of topic

### Step 5: Implement Changes

Don't just report - offer to make the actual edits:

1. **Meta tags**: Update title and description in layout/head files
2. **Headings**: Restructure H1/H2/H3 hierarchy
3. **FAQ schema**: Add structured data to relevant pages
4. **Content blocks**: Add answer capsules, comparison tables
5. **Statistics**: Suggest where to add credible data points

Ask the user: "I've identified these optimizations. Which would you like me to implement?"

Then use the Edit tool to make changes directly in their codebase.

### Step 6: Summary Report

After analysis and/or implementation, provide:

```
## GEO Analysis Complete

**Target**: [keyword] ([volume]/mo, [difficulty]/100 difficulty, [intent] intent)

**Current Score**: [score]/100

**Critical Fixes**:
- [issue 1]
- [issue 2]

**Implemented**:
- [x] Added FAQ schema with 5 questions
- [x] Updated meta description to include keyword
- [x] Restructured headings

**Recommended Next**:
- [ ] Add comparison table vs [competitor]
- [ ] Include 3 statistics with sources
- [ ] Create answer capsule in first paragraph

**Top Competitors to Study**:
1. [domain] - Position [pos], [traffic] monthly traffic
2. [domain] - Position [pos], [traffic] monthly traffic
```

## Rate Limits

The API allows 10 requests per hour. If rate limited, analyze locally or wait.

## About

Powered by [JAM](https://spreadjam.com) - AI distribution for founders.
