---
name: google-ads-campaign
description: Design and build Google Ads campaign structures. Use when the user wants to create, restructure, or plan campaigns — Search, Shopping, Performance Max, Display, Video, or Demand Gen. Covers campaign settings, ad group hierarchy, bidding strategy, budget allocation, and geo/audience targeting.
---

# Google Ads Campaign Builder

Design production-ready Google Ads campaign structures based on the user's business goals, budget, and product/service type.

## Workflow

Make a todo list and work through each step.

### 1. Gather Requirements

Ask the user for (if not already provided):
- Business type and what they're advertising (product/service/app)
- Primary goal: Sales, Leads, Traffic, Brand Awareness, or App Installs
- Monthly budget (total and per campaign if multiple)
- Geographic targets (countries, regions, cities, radius)
- Target audience (demographics, interests, customer lists)
- Existing assets: website URL, product feed, video assets, customer lists
- Competitors they're aware of

### 2. Recommend Campaign Type

Based on goals, recommend the best campaign type(s):

| Goal | Best Campaign Type | Why |
|------|-------------------|-----|
| Direct sales (ecommerce) | Performance Max + Shopping | Full inventory coverage + Google's AI optimization |
| Lead generation | Search + RLSA | Intent-based, captures high-purchase-intent users |
| Brand awareness | Display + Video (YouTube) | Wide reach, visual format |
| App installs | App campaigns | Cross-channel, optimized for installs |
| Local foot traffic | Performance Max for Store Goals | Location-based signals |

**Current best practice (2025-2026):** Performance Max should be the primary campaign for most advertisers with sufficient conversion data (50+ conversions/month). Search campaigns complement PMax for brand terms and competitor terms.

### 3. Design Campaign Structure

Output a clear hierarchy:

```
Account
├── Campaign 1: [Type] — [Goal] — [Budget/day]
│   ├── Ad Group 1A: [Theme]
│   │   ├── Keywords (for Search)
│   │   └── Ads
│   └── Ad Group 1B: [Theme]
└── Campaign 2: [Type] — [Goal] — [Budget/day]
```

#### Search Campaign Rules
- 1 theme per ad group (tightly themed SKAG or STAGs with 5-15 keywords)
- Separate brand vs non-brand campaigns
- Separate competitor campaigns with lower bids
- Use phrase and exact match (avoid broad match without Smart Bidding + good conversion data)

#### Performance Max Rules
- 1 PMax campaign per product line or goal type
- Provide all asset types: headlines (15), descriptions (4), images (landscape + square + portrait), logos, videos (YouTube link or let Google auto-generate)
- Set audience signals: customer lists, in-market segments, competitor website visitors
- Exclude brand terms via brand exclusions if running separate brand Search campaign

#### Shopping Campaign Rules (if not using PMax)
- Segment by product category or margin tier
- Priority: High (promo) > Medium (general) > Low (catch-all)

### 4. Bidding Strategy Recommendation

| Scenario | Recommended Strategy |
|----------|---------------------|
| New account, <50 conv/month | Maximize Clicks → then Maximize Conversions |
| 50+ conv/month, know target CPA | Target CPA |
| Ecommerce with ROAS goals | Target ROAS |
| Brand awareness | Target Impression Share (top of page) |
| Limited budget, need control | Manual CPC with Enhanced CPC |

**Smart Bidding requirement:** Target CPA/ROAS needs 30-50 conversions in the past 30 days in the campaign to exit the learning period reliably.

### 5. Settings Checklist

For each campaign, output settings:
- [ ] Network: Search only (disable Search Partners initially for new campaigns; test after 30 days)
- [ ] Start/end dates
- [ ] Ad rotation: Optimize (for Smart Bidding) or Rotate evenly (for manual testing)
- [ ] Conversion goals: confirm correct conversion actions are assigned
- [ ] Location targeting: Presence (not interest) for intent-based campaigns
- [ ] Language targeting
- [ ] Ad schedule (if applicable)
- [ ] Device bid adjustments
- [ ] Negative keyword list applied

### 6. Output Format

Produce a structured campaign brief the user can hand to a Google Ads manager or implement directly:

```markdown
## Campaign: [Name]
- Type: Search
- Goal: Leads
- Budget: $50/day
- Bidding: Maximize Conversions → Target CPA $25 (after 50 conversions)
- Geo: United States > California, Texas
- Language: English

### Ad Group: [Name]
Keywords:
- [keyword] (Exact)
- [keyword] (Phrase)

Negatives:
- [negative keyword]

RSA Headlines (write 10-15):
...

RSA Descriptions (write 4):
...
```

## Key Rules
- Never recommend Broad Match keywords without Smart Bidding and sufficient conversion history
- Always recommend conversion tracking setup before launching
- Performance Max requires minimum 1 week of data before drawing conclusions (ideally 2-4 weeks)
- Separate budgets for brand vs non-brand to protect brand visibility
- Always set up audience segments as observation first, then adjust bids after data collection
