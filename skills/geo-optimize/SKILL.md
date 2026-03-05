# GEO Optimize - Expert Analysis

Optimize content to get cited by AI search engines (ChatGPT, Perplexity, Claude, Google AI Overview). This skill performs deep competitive analysis and generates specific, actionable recommendations with ready-to-use content.

## Usage

```
/geo-optimize [url] [keyword]
/geo-optimize                     # Analyze current codebase
/geo-optimize "keyword"           # Analyze codebase for specific keyword
/geo-optimize https://... "kw"    # Analyze deployed URL + keyword
```

---

## Instructions

Follow this 4-step workflow to provide expert-level GEO analysis:

### Step 1: Gather Intelligence from API

Call the JAM GEO API to get keyword data, PAA questions, and competitor info:

```bash
curl -X POST https://www.spreadjam.com/api/geo/analyze \
  -H "Content-Type: application/json" \
  -d '{
    "url": "<TARGET_URL>",
    "targetKeyword": "<KEYWORD>",
    "includePrompt": "none"
  }'
```

From the response, extract and note:
- `paaQuestions[]` - Questions people ask (use for FAQ)
- `keywordIdeas[]` - Related topics with metrics
- `longTailKeywords[]` - Low-competition variations
- `competitorPages[]` - Competitor domains to analyze
- `keywords.primary` - Search volume, difficulty, intent
- `audit.overallScore` - Current SEO health

### Step 2: Analyze Target Page

Use WebFetch to read the target URL. As you read, identify:

**Content Structure:**
- H1, H2, H3 headings (list them)
- Word count (approximate)
- First paragraph length (is it 40-60 words? = answer capsule)

**GEO Elements Present:**
- [ ] FAQ section? (count questions)
- [ ] Comparison table?
- [ ] Statistics with sources?
- [ ] Expert quotes or citations?
- [ ] Schema markup mentioned in code?

**Note what's missing** - this is critical for recommendations.

### Step 3: Analyze Top 3 Competitors

For each competitor domain from `competitorPages[]`:
1. Construct their likely URL (domain + search for their ranking page)
2. Use WebFetch to read their content
3. Extract their structure:
   - H2 headings (what topics do they cover?)
   - FAQ questions (if any)
   - Do they have comparison tables?
   - Do they have statistics?

**Build a comparison table:**

| Element | Target Page | Competitor 1 | Competitor 2 | Competitor 3 |
|---------|-------------|--------------|--------------|--------------|
| Word Count | X | Y | Z | W |
| FAQ Questions | 0 | 8 | 5 | 10 |
| Comparison Table | No | Yes | No | Yes |
| Statistics Cited | 2 | 7 | 4 | 9 |
| Answer Capsule | No (150 words) | Yes (48 words) | No | Yes (52 words) |

**Identify content gaps:**
Topics that 2+ competitors cover that the target page doesn't.

### Step 4: Generate Specific Recommendations

Now produce actionable output with READY-TO-USE content.

---

## Output Format

Structure your response exactly like this:

```markdown
## GEO Analysis: [url]

### Target Keyword: "[keyword]"
- Search Volume: [X]/month
- Difficulty: [Y]/100
- Intent: [informational/commercial/transactional]

### Current Score: [X]/100

---

### What You Have (Good)
- [List existing positive elements]
- [e.g., "Clear H1 with keyword"]
- [e.g., "Mobile-friendly design"]

---

### Critical Gaps vs Competitors

| Gap | Your Page | Competitors Avg | Impact |
|-----|-----------|-----------------|--------|
| FAQ Section | 0 questions | 7.6 questions | +156% citations |
| Answer Capsule | 145 words (too long) | 50 words | Critical for AI extraction |
| Comparison Table | None | 2 of 3 have | +112% citations |
| Statistics | 2 cited | 6.7 average | +40% citations |

---

### Content Topics You're Missing

These H2 topics appear in top competitors but not your page:

1. **[Topic from competitor]** - covered by positions #1, #2
2. **[Topic from competitor]** - covered by positions #1, #3
3. **[Topic from competitor]** - covered by positions #2, #3

---

### Generated FAQ (Ready to Copy)

Based on People Also Ask + competitor analysis:

**Q: [Question 1 from paaQuestions]?**
A: [Write a 50-word answer based on page content and keyword intent]

**Q: [Question 2]?**
A: [50-word answer]

**Q: [Question 3]?**
A: [50-word answer]

**Q: [Question 4]?**
A: [50-word answer]

**Q: [Question 5]?**
A: [50-word answer]

---

### Answer Capsule (Ready to Copy)

Replace your first paragraph with this 40-60 word direct answer:

> [Write a direct, authoritative answer to the target keyword query. Include the keyword naturally. Make it self-contained - this is what AI will extract and cite.]

---

### Comparison Table (Ready to Copy)

| Feature | [Your Brand] | [Competitor 1] | [Competitor 2] |
|---------|--------------|----------------|----------------|
| [Key differentiator] | Yes | Partial | No |
| [Feature 2] | [Your value] | [Their value] | [Their value] |
| [Feature 3] | [Your value] | [Their value] | [Their value] |

---

### Schema Markup to Add

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "[Q1 from above]",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "[A1 from above]"
      }
    }
    // ... repeat for each FAQ
  ]
}
```

---

### Implementation Checklist

- [ ] Add FAQ section with 5 questions (impact: +156% citations)
- [ ] Replace first paragraph with answer capsule (impact: AI extraction)
- [ ] Add comparison table (impact: +112% citations)
- [ ] Add FAQPage schema markup
- [ ] Add [X] statistics with sources (impact: +40% citations)
- [ ] Cover missing topic: "[topic 1]"
- [ ] Cover missing topic: "[topic 2]"
- [ ] Update page (currently [X] days old, recommend <60 days)

---

### Platform-Specific Notes

**ChatGPT** (Bing-powered): [Specific tip based on analysis]
**Perplexity** (Reddit-heavy): [Specific tip]
**Claude** (Brave): [Specific tip]
**Google AI**: [Specific tip]
```

---

## Key Principles

1. **Be specific, not generic** - "Add FAQ" is useless. "Add these 5 FAQ questions with these answers" is useful.

2. **Show the gap** - Always compare to competitors. "You have 0 FAQs, competitors average 7" is compelling.

3. **Generate ready-to-use content** - Write the FAQ answers, the answer capsule, the comparison table. Don't just recommend them.

4. **Quantify impact** - Use the research numbers: FAQ (+156%), tables (+112%), statistics (+40%).

5. **Prioritize by impact** - Critical items first in the checklist.

---

## Handling Edge Cases

**No URL provided (codebase only):**
- Look for meta tags in layout/head files
- Extract content from main pages
- Ask user for target keyword if not clear

**No keyword provided:**
- Look at page title, H1, meta description
- Check package.json description
- Ask: "What topic do you want to rank for in AI search?"

**API rate limited:**
- Inform user: "API limit reached. Try again in [X] minutes."
- Offer to do manual analysis of provided URL

**Competitor pages can't be fetched:**
- Note which competitors couldn't be analyzed
- Proceed with available data
- Recommend user manually review competitor pages

---

## Rate Limits

10 requests per hour per IP. If rate limited, inform user.

## About

Powered by [JAM](https://spreadjam.com) - AI distribution for founders.
