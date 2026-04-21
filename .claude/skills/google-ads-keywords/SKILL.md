---
name: google-ads-keywords
description: Google Ads keyword research, expansion, and negative keyword strategy. Use when the user needs keyword lists, match type recommendations, negative keyword lists, search term analysis, or keyword pruning for any Google Ads campaign type.
---

# Google Ads Keyword Research & Strategy

Build high-performing keyword lists with correct match types and a robust negative keyword strategy.

## Workflow

### 1. Gather Context

Ask if not provided:
- Product/service being advertised
- Landing page URL (to extract seed keywords)
- Target audience and geography
- Campaign type (Search / Shopping / hybrid)
- Budget level (drives how aggressive to expand)
- Existing keyword list or search term report (if optimizing, not starting fresh)

### 2. Seed Keyword Generation

Start from these sources in order:
1. User's website/landing page — extract core terms
2. Product/service synonyms and alternatives
3. Problem-based terms (what pain does the product solve?)
4. Competitor brand terms (if bidding on competitors)
5. Long-tail variations (how, best, price, near me, review, vs, alternative)

Organize seeds by intent tier:
- **Bottom of funnel (buy intent):** "buy [product]", "[product] price", "[product] near me"
- **Middle of funnel (consideration):** "best [product]", "[product] reviews", "[product] vs [competitor]"
- **Top of funnel (awareness):** "[problem] solution", "how to [fix problem]"

### 3. Match Type Strategy

| Match Type | When to Use | Risk |
|------------|-------------|------|
| Exact `[keyword]` | High-intent, proven converters. Brand terms. | Low volume |
| Phrase `"keyword"` | Variations of a core theme. Mid-intent. | Some irrelevant traffic |
| Broad (with Smart Bidding) | Large budgets, good conversion data (100+/month), PMax complement | Unpredictable spend |

**Current best practice (2025-2026):**
- Start with exact + phrase for new campaigns
- Add broad only after 60+ days of data with Smart Bidding
- Never use broad match with manual CPC or new accounts

### 4. Keyword Grouping

Group keywords by intent and theme. Each ad group should share one core theme:

```
Ad Group: [Theme Name]
Primary intent: [buy / learn / compare / local]

Exact match:
- [exact keyword 1]
- [exact keyword 2]

Phrase match:
- "[phrase keyword 1]"
- "[phrase keyword 2]"

Expected search volume: High / Medium / Low
Suggested bid range: $X - $Y (if user provides industry)
```

Aim for 5-15 keywords per ad group. More than 20 = split into sub-groups.

### 5. Negative Keyword Lists

Always produce two negative lists:

#### Account-Level Negatives (universal blockers)
These should be applied to every campaign:
- free, cheap, discount (if premium product)
- jobs, careers, salary, hire (unless it's a job platform)
- DIY, how to make, tutorial (unless selling courses)
- Wikipedia, Reddit (informational, rarely convert)
- Images, photos, pictures (unless image-related product)
- [competitor product names] (if not bidding on competitors)

#### Campaign-Level Negatives (specific to campaign theme)
Based on what the campaign covers, block adjacent irrelevant queries:
- If selling new products: used, second hand, refurbished
- If B2B: personal, home, residential (and vice versa for B2C)
- If selling one product category: all other product category names

#### Search Term Report Analysis (if user provides one)
When the user provides a search term report (CSV or pasted data):
1. Filter for terms with impressions > 50 and 0 conversions
2. Calculate CTR — flag anything below 1% as likely irrelevant
3. Flag search terms with high cost and 0 conversions as immediate negatives
4. Surface any search terms converting well that are NOT in the keyword list (add these as exact match)

Output format:
```
NEGATIVES TO ADD:
- [term] → reason: [high cost, no conv | irrelevant | wrong intent]

KEYWORDS TO ADD (found in search terms, not in keyword list):
- [term] → [exact match] → ad group: [group name]
```

### 6. Keyword Metrics Estimates

When the user doesn't have Search Console or Keyword Planner data, provide realistic estimates based on industry:

| Industry | Avg CPC Range | Competition |
|----------|--------------|-------------|
| Legal / Finance | $5 - $50+ | Very High |
| SaaS / Software | $3 - $20 | High |
| Ecommerce (general) | $0.5 - $5 | Medium |
| Local services | $2 - $15 | Medium-High |
| Healthcare | $3 - $25 | High |

Note: Always recommend the user verify with Google Keyword Planner for actual volume data.

### 7. Output Format

Deliver a ready-to-import keyword plan:

```csv
Campaign,Ad Group,Keyword,Match Type,Max CPC
[Campaign],[Ad Group],[keyword],Exact,$X
[Campaign],[Ad Group],"[keyword]",Phrase,$X
```

Also include a plain-text version for review:

```
CAMPAIGN: [Name]
  AD GROUP: [Name]
    [keyword] (Exact) — intent: buy
    "[keyword]" (Phrase) — intent: compare
  
  NEGATIVES (campaign level):
    -[negative]
    -[negative]

ACCOUNT NEGATIVES:
  -[negative]
```

## Key Rules
- Quality Score depends on keyword → ad → landing page relevance. Keep themes tight.
- Broad match + manual CPC = wasted spend. Always pair broad with Smart Bidding.
- Negative keywords are as important as positive keywords. Budget 30% of setup time to negatives.
- Revisit search term report weekly for first 30 days, then monthly.
- Low search volume keywords (<10 searches/month) waste crawl budget — pause or remove.
