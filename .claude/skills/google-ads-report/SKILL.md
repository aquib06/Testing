---
name: google-ads-report
description: Generate Google Ads performance reports with analysis and recommendations. Use when the user wants a weekly/monthly report, executive summary, client-ready report, ROAS/CPA analysis, or trend analysis from Google Ads data. Can work from pasted metrics, CSV exports, or Google Ads report screenshots.
---

# Google Ads Performance Reporter

Transform raw Google Ads data into clear, actionable reports with analysis and next steps.

## Workflow

### 1. Gather the Data

Ask the user to provide:
- Raw data: paste metrics, upload CSV, or describe numbers
- Reporting period: date range + comparison period
- Report purpose: internal review / client report / executive summary
- Business context: goals, recent changes, seasonality notes
- Key KPIs they care about most (CPA, ROAS, Revenue, Leads, CTR)

Minimum data needed to produce a useful report:
- Spend, Clicks, Impressions, Conversions, Conversion Value (if ecommerce)
- Broken out by campaign (not just account totals)

### 2. Calculate Core Metrics

If not already calculated, compute these from raw data:

```
CTR = Clicks / Impressions × 100
Avg CPC = Spend / Clicks
Conversion Rate = Conversions / Clicks × 100
CPA (Cost per Acquisition) = Spend / Conversions
ROAS = Conversion Value / Spend
CPM = Spend / Impressions × 1000
Impression Share = Impressions / Eligible Impressions (if provided)

Period-over-period change:
  % change = (New - Old) / Old × 100
  Flag: >10% change as Notable, >25% as Significant
```

### 3. Report Formats

#### Format A: Internal Performance Report (Weekly)

```markdown
# Google Ads Performance Report
**Period:** [Date range] vs [Prior period]
**Prepared:** [Date]

## Account Summary

| Metric | This Period | Prior Period | Change |
|--------|------------|--------------|--------|
| Spend | $X | $X | ±X% |
| Clicks | X | X | ±X% |
| Impressions | X | X | ±X% |
| CTR | X% | X% | ±X% |
| Avg CPC | $X | $X | ±X% |
| Conversions | X | X | ±X% |
| CPA | $X | $X | ±X% |
| Conv. Rate | X% | X% | ±X% |
| [ROAS if ecommerce] | X.XX | X.XX | ±X% |

## Campaign Breakdown

| Campaign | Spend | Conv | CPA | vs Prior |
|----------|-------|------|-----|----------|
| [Campaign 1] | $X | X | $X | ±X% |
| [Campaign 2] | $X | X | $X | ±X% |

## Key Wins
- [Metric that improved significantly and why]
- [Campaign that outperformed]

## Key Concerns
- [Metric that declined and why]
- [Campaign that underperformed]

## Actions Taken This Period
- [What was changed/tested]

## Recommended Actions Next Period
1. [Action] — Expected impact: [X]
2. [Action] — Expected impact: [X]
```

#### Format B: Client Report (Monthly, Non-Technical)

```markdown
# [Client Name] — Google Ads Monthly Report
**[Month Year]**

---

## The Big Picture

This month, your Google Ads campaigns generated **[X conversions / $X revenue]** 
from a spend of **$X**, giving you a **[CPA of $X / ROAS of X.X]**.

[1-2 sentence plain-English summary of whether the month was good/neutral/needs work and why]

---

## Results vs. Goals

| Goal | Target | Actual | Status |
|------|--------|--------|--------|
| Monthly Spend | $X | $X | ✅/⚠️/❌ |
| Conversions | X | X | ✅/⚠️/❌ |
| CPA | $X | $X | ✅/⚠️/❌ |
| ROAS | X.X | X.X | ✅/⚠️/❌ |

---

## What's Working

**[Campaign Name]** delivered [X conversions] at a CPA of $[X] — 
[X]% below your target. [1 sentence explaining why it worked.]

---

## What Needs Attention

**[Area]** saw [metric drop]. This is likely due to [plain-English reason]. 
We're addressing this by [action].

---

## What We Did This Month
- [Change made] → [result]
- [Test run] → [outcome]

## What We're Doing Next Month
1. [Planned action and expected outcome]
2. [Planned action and expected outcome]

---
*Data source: Google Ads | Period: [dates]*
```

#### Format C: Executive Summary (1-Page)

```markdown
# Google Ads — Executive Summary
**[Period] | Total Spend: $[X]**

### Performance Snapshot
- **Revenue/Leads Generated:** [X] at $[CPA/ROAS]
- **vs Prior Period:** [+/-X%] conversions, [+/-X%] cost efficiency
- **vs Target:** [On track / X% above target / X% below target]

### Top Performer: [Campaign Name]
[One sentence on what drove results]

### Biggest Opportunity: [Area]
[One sentence on what to fix or scale]

### Budget Efficiency
[X]% of budget delivered [X]% of conversions.
[Recommendation: reallocate / increase / hold]
```

### 4. Analysis Rules

When analyzing data, always:

**Segment before concluding:**
- Don't report account-level CTR without breaking it down by campaign type
- Display/PMax CTR (~0.1-0.5%) looks bad next to Search CTR (3-10%) — always compare apples to apples

**Contextualize changes:**
- CPA went up 20% — was it seasonality? Did you add a new campaign? Did a top keyword get competition?
- Always ask: "What changed?" before calling something a problem

**Flag data anomalies:**
- Conversion spike on a single day = likely tracking issue, not real
- 0 impressions on an active campaign = disapproval, billing issue, or targeting too narrow
- CTR doubles overnight = check for accidental broad match or campaign restructure

**Industry benchmarks (approximate, varies widely):**
| Metric | Search Avg | Display Avg | Shopping Avg |
|--------|-----------|-------------|--------------|
| CTR | 3-6% | 0.1-0.5% | 0.5-2% |
| Conv Rate | 2-5% | 0.5-1% | 1-3% |
| CPC | $1-5 (varies) | $0.50-2 | $0.50-2 |

### 5. Trend Analysis

When comparing multiple periods:

```
Week 1: $X spend, X conv, $X CPA
Week 2: $X spend, X conv, $X CPA  
Week 3: $X spend, X conv, $X CPA
Week 4: $X spend, X conv, $X CPA

Trend: [Improving / Declining / Stable / Volatile]
Signal: [What this trend indicates]
Action: [What to do based on trend]
```

Patterns to identify:
- **Improving CPA trend:** Bidding strategy is learning — maintain course
- **Rising CPA + rising spend:** Scaling into diminishing returns — consider bid cap
- **Flat conversions + rising spend:** Impression share maxed — test new audiences
- **Declining CTR over time:** Ad fatigue — refresh creatives

### 6. Recommendations Framework

Always tier recommendations by effort vs. impact:

| Priority | Effort | Impact | Example |
|----------|--------|--------|---------|
| Quick Win | Low | High | Pause 3 zero-conversion keywords draining $200/month |
| Strategic | Medium | High | Restructure brand vs non-brand campaigns |
| Test | Low | Unknown | A/B test new headline angle |
| Long-term | High | High | Implement enhanced conversions for better tracking |

## Key Rules
- Numbers without context are useless — always explain the "so what"
- Never present raw data without a recommendation attached
- Client reports should have zero jargon — replace "CTR" with "click rate" if needed
- A good report answers: What happened? Why? What are we doing about it?
- If data is insufficient to draw conclusions, say so explicitly rather than speculating
