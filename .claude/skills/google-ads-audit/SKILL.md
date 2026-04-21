---
name: google-ads-audit
description: Audit a Google Ads account or campaign for performance issues, wasted spend, structural problems, and optimization opportunities. Use when the user wants a health check, performance review, or troubleshooting of underperforming campaigns. Can work from pasted data, screenshots, CSV exports, or verbal descriptions.
---

# Google Ads Account Audit

Systematically audit a Google Ads account or campaign and produce a prioritized action plan.

## Workflow

### 1. Gather Data

Ask the user to provide as many of these as possible:

**Minimum required:**
- Campaign names and types
- Date range for analysis (recommend: last 30 days vs. prior 30 days)
- Key metrics: Impressions, Clicks, CTR, Avg CPC, Conversions, Cost/Conv, Conversion Rate, ROAS, Total Spend

**Ideal additions:**
- Search term report (CSV or pasted)
- Keyword performance report
- Ad performance report
- Audience insights
- Geographic performance
- Device performance breakdown
- Time-of-day / day-of-week report
- Quality Score data per keyword
- Budget utilization (is budget being fully spent or limited?)

The user can paste raw data, CSV content, or describe their situation. Work with what's available.

### 2. Audit Framework — 8 Categories

Systematically check each category and score it: Green (Good) / Yellow (Needs attention) / Red (Critical issue)

---

#### A. Conversion Tracking
- [ ] Is conversion tracking installed and firing? (No conversions in data = red flag)
- [ ] Are the right conversion actions being tracked? (purchases, leads, calls, etc.)
- [ ] Is there conversion deduplication in place? (avoid double-counting)
- [ ] Are auto-applied goals turned off if they're inflating numbers? (e.g. "website visits" as a conversion)
- [ ] Enhanced Conversions set up? (improves match rate for iOS/privacy changes)

**Red flags:** 0 conversions with significant spend, unusually high conversion rates (>20% for most industries), conversion value = $0

---

#### B. Campaign Structure
- [ ] Are Search and Display in separate campaigns?
- [ ] Are brand and non-brand keywords in separate campaigns?
- [ ] Is Performance Max separated by product line or goal?
- [ ] Are there too many ad groups with too few keywords (over-segmented)?
- [ ] Are there ad groups with too many unrelated keywords?
- [ ] Do Shopping/PMax campaigns have product feed health issues?

**Red flags:** Brand + non-brand in same campaign (can't control bids separately), more than 50 ad groups in a campaign, Display network enabled on Search campaigns

---

#### C. Bidding & Budget
- [ ] Is the bidding strategy appropriate for the conversion volume?
- [ ] Is the daily budget being hit (budget limited)?
- [ ] Are campaigns in "learning" status for an unusually long time?
- [ ] Is Target CPA/ROAS achievable based on historical performance?
- [ ] Are there dramatic CPC spikes (competitor changes or Quality Score drops)?

**Calculations to run:**
- Budget utilization: `actual spend / (daily budget × days in period)` — if <70%, ads may be limited by quality or targeting
- Impression share lost to budget: if >20%, budget is a bottleneck
- CPA vs target: flag if actual CPA > target CPA by >30%

---

#### D. Keywords & Search Terms
- [ ] Are there high-spend, zero-conversion keywords? (Pause candidates)
- [ ] Are search terms relevant to the business?
- [ ] Are there search terms triggering ads that should be negatives?
- [ ] Are there duplicate keywords across ad groups?
- [ ] Are broad match keywords driving irrelevant traffic?
- [ ] Is there keyword cannibalization (multiple ad groups competing for same terms)?

**Thresholds for action:**
- Keyword with >2x target CPA spend, 0 conversions → pause
- Search term CTR <0.5% with >100 impressions → consider negative
- Quality Score <5 on important keywords → investigate landing page + ad relevance

---

#### E. Ad Quality & Ad Strength
- [ ] Is there at least 1 RSA per ad group with Good or Excellent Ad Strength?
- [ ] Are ads using all available extensions (sitelinks, callouts, structured snippets)?
- [ ] Are headlines/descriptions diverse enough for machine learning?
- [ ] Are there disapproved ads causing coverage gaps?
- [ ] Are there ad groups with only 1 active ad (no testing)?

**Ad Strength scoring:**
- Poor/Average across most ad groups → rewrite headlines for more variety
- 0 extensions = losing to competitors with more real estate

---

#### F. Quality Score
- [ ] What is the average Quality Score across keywords?
- [ ] Are there keywords with QS 1-4? (Paying premium CPCs)
- [ ] Is Ad Relevance "Below average"? (Ad-keyword mismatch)
- [ ] Is Landing Page Experience "Below average"? (Page speed, relevance, mobile)
- [ ] Is Expected CTR "Below average"? (Ad copy not compelling)

**QS impact on CPC:** QS 7+ = discount vs competitors. QS 4 or below = significant CPC premium (up to 400% more).

---

#### G. Targeting & Audiences
- [ ] Are location targets set to "Presence" not "Presence or Interest"?
- [ ] Are there locations with high spend and low conversion rate? (Bid down or exclude)
- [ ] Is device performance split reviewed? (Mobile CPA often differs from Desktop)
- [ ] Are remarketing audiences attached in at least observation mode?
- [ ] Are customer match lists uploaded and refreshed?

---

#### H. Performance Trends
Compare last 30 days vs prior 30 days:
- [ ] CTR trend (up = good, down = ad fatigue or quality issue)
- [ ] Conversion rate trend (down = landing page issue or audience shift)
- [ ] CPC trend (up = competition increased or QS dropped)
- [ ] Impression share trend (down = budget or quality)

### 3. Prioritized Action Plan

After completing the audit, rank findings by impact:

**Priority 1 — Fix Immediately (Revenue Impact)**
Issues causing direct revenue loss or wasted spend. Fix within 24-48 hours.

**Priority 2 — Fix This Week (Efficiency)**
Issues causing inefficiency but not emergencies.

**Priority 3 — Optimize Over Next Month (Growth)**
Opportunities to improve performance once foundations are solid.

### 4. Output Format

```
## Google Ads Audit — [Account/Campaign Name]
Date range: [X] vs [Y]
Total spend analyzed: $[X]

### Overall Health Score: [X/10]

| Category | Status | Key Finding |
|----------|--------|-------------|
| Conversion Tracking | 🔴/🟡/🟢 | [Finding] |
| Campaign Structure  | 🔴/🟡/🟢 | [Finding] |
| Bidding & Budget    | 🔴/🟡/🟢 | [Finding] |
| Keywords            | 🔴/🟡/🟢 | [Finding] |
| Ad Quality          | 🔴/🟡/🟢 | [Finding] |
| Quality Score       | 🔴/🟡/🟢 | [Finding] |
| Targeting           | 🔴/🟡/🟢 | [Finding] |
| Trends              | 🔴/🟡/🟢 | [Finding] |

---

### PRIORITY 1 — Fix Immediately
1. [Issue]: [What to do] — Est. impact: [Save $X/month or +X% conversions]
2. ...

### PRIORITY 2 — Fix This Week
1. [Issue]: [What to do]
...

### PRIORITY 3 — Optimize This Month
1. [Opportunity]: [What to do]
...

---
Estimated monthly savings/gain if all Priority 1 items are fixed: $[X]
```

## Key Rules
- Always start with conversion tracking — if it's broken, all other data is unreliable
- Don't optimize what you can't measure — fix tracking before optimizing bids
- High CTR + low conversion rate = landing page problem, not ad problem
- Low CTR + low CPC = targeting irrelevant audience
- Never recommend pausing a campaign in the learning period — wait for it to exit first
