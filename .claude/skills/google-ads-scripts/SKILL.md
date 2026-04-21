---
name: google-ads-scripts
description: Write Google Ads Scripts (JavaScript) for automation, alerting, and bulk operations. Use when the user wants to automate bid adjustments, send performance alerts, pause underperformers, generate reports in Google Sheets, manage budgets, or bulk-edit campaigns programmatically via the Google Ads Scripts editor.
---

# Google Ads Scripts Writer

Write production-ready Google Ads Scripts that run in the Google Ads Scripts editor (Tools > Scripts).

## Important Context

Google Ads Scripts run as JavaScript in a sandboxed environment:
- API: `AdsApp` object (not REST API — this is the Scripts-specific JS API)
- Execution time limit: 30 minutes per run
- Can read/write campaigns, ad groups, keywords, ads, bids
- Can access Google Sheets (SpreadsheetApp), Gmail (MailApp), and URLs (UrlFetchApp)
- Runs on Google's servers — no local environment needed
- Can be scheduled: hourly, daily, weekly, monthly

## Workflow

### 1. Understand the Automation Request

Ask if not clear:
- What should the script DO? (alert, pause, adjust bid, report, etc.)
- What is the trigger/condition? (CPA > $X, CTR < Y%, budget at Z%)
- What should happen when triggered? (email alert, pause keyword, adjust bid by X%)
- Where should output go? (email, Google Sheet, just logs)
- What scope? (all campaigns, specific campaigns, specific ad groups)
- How often should it run? (hourly, daily, weekly)

### 2. Script Architecture

All scripts follow this structure:

```javascript
// ============================================================
// CONFIGURATION — edit these values
// ============================================================
var CONFIG = {
  // ... user-configurable settings here
};

// ============================================================
// MAIN — entry point (Google runs this function)
// ============================================================
function main() {
  // ... core logic
}

// ============================================================
// HELPERS
// ============================================================
function helperFunction() {
  // ... reusable utilities
}
```

### 3. Common Script Templates

#### A. Performance Alert Script
Sends email when KPIs go out of bounds.

```javascript
var CONFIG = {
  EMAIL: 'you@example.com',
  DATE_RANGE: 'LAST_7_DAYS',
  MAX_CPA: 50,        // alert if CPA exceeds this
  MIN_CTR: 0.01,      // alert if CTR drops below 1%
  MIN_CONVERSIONS: 0, // alert if conversions drop to 0
  CAMPAIGN_LABEL: ''  // leave empty for all campaigns, or set a label name
};

function main() {
  var alerts = [];
  var campaignIterator = getCampaigns();

  while (campaignIterator.hasNext()) {
    var campaign = campaignIterator.next();
    var stats = campaign.getStatsFor(CONFIG.DATE_RANGE);

    var cost = stats.getCost();
    var conversions = stats.getConversions();
    var ctr = stats.getCtr();
    var cpa = conversions > 0 ? cost / conversions : Infinity;

    if (cpa > CONFIG.MAX_CPA) {
      alerts.push(campaign.getName() + ': CPA $' + cpa.toFixed(2) + ' > $' + CONFIG.MAX_CPA);
    }
    if (ctr < CONFIG.MIN_CTR) {
      alerts.push(campaign.getName() + ': CTR ' + (ctr * 100).toFixed(2) + '% < ' + (CONFIG.MIN_CTR * 100) + '%');
    }
    if (conversions <= CONFIG.MIN_CONVERSIONS) {
      alerts.push(campaign.getName() + ': ' + conversions + ' conversions in ' + CONFIG.DATE_RANGE);
    }
  }

  if (alerts.length > 0) {
    MailApp.sendEmail({
      to: CONFIG.EMAIL,
      subject: '[Google Ads Alert] ' + alerts.length + ' issue(s) found',
      body: alerts.join('\n')
    });
    Logger.log('Alert sent: ' + alerts.length + ' issues');
  } else {
    Logger.log('All metrics within targets');
  }
}

function getCampaigns() {
  if (CONFIG.CAMPAIGN_LABEL) {
    return AdsApp.campaigns()
      .withCondition('LabelNames CONTAINS_ANY ["' + CONFIG.CAMPAIGN_LABEL + '"]')
      .withCondition('Status = ENABLED')
      .get();
  }
  return AdsApp.campaigns().withCondition('Status = ENABLED').get();
}
```

#### B. Pause Underperforming Keywords Script
Pauses keywords spending over threshold with no conversions.

```javascript
var CONFIG = {
  DATE_RANGE: 'LAST_30_DAYS',
  MIN_COST_TO_REVIEW: 50,  // Only pause if spent more than $50
  MAX_CPA_MULTIPLIER: 2,   // Pause if CPA > 2x your target CPA
  TARGET_CPA: 25,
  DRY_RUN: true,            // Set false to actually pause keywords
  EMAIL_REPORT: 'you@example.com'
};

function main() {
  var paused = [];
  var keywordIterator = AdsApp.keywords()
    .withCondition('Status = ENABLED')
    .withCondition('CampaignStatus = ENABLED')
    .withCondition('AdGroupStatus = ENABLED')
    .forDateRange(CONFIG.DATE_RANGE)
    .withCondition('Cost > ' + CONFIG.MIN_COST_TO_REVIEW)
    .withCondition('Conversions = 0')
    .get();

  while (keywordIterator.hasNext()) {
    var keyword = keywordIterator.next();
    var stats = keyword.getStatsFor(CONFIG.DATE_RANGE);
    var cost = stats.getCost();

    if (cost > CONFIG.TARGET_CPA * CONFIG.MAX_CPA_MULTIPLIER) {
      if (!CONFIG.DRY_RUN) {
        keyword.pause();
      }
      paused.push({
        campaign: keyword.getCampaign().getName(),
        adGroup: keyword.getAdGroup().getName(),
        keyword: keyword.getText(),
        cost: cost.toFixed(2),
        conversions: stats.getConversions()
      });
    }
  }

  Logger.log((CONFIG.DRY_RUN ? '[DRY RUN] Would pause' : 'Paused') + ' ' + paused.length + ' keywords');
  paused.forEach(function(k) {
    Logger.log(k.campaign + ' > ' + k.adGroup + ' > ' + k.keyword + ' ($' + k.cost + ', ' + k.conversions + ' conv)');
  });

  if (paused.length > 0 && CONFIG.EMAIL_REPORT) {
    var body = paused.map(function(k) {
      return k.campaign + ' > ' + k.keyword + ': $' + k.cost + ' spent, 0 conversions';
    }).join('\n');
    MailApp.sendEmail(CONFIG.EMAIL_REPORT, '[Google Ads] Keywords ' + (CONFIG.DRY_RUN ? 'to review' : 'paused'), body);
  }
}
```

#### C. Budget Pacing Script
Alerts when daily budget is over/under-pacing.

```javascript
var CONFIG = {
  EMAIL: 'you@example.com',
  OVER_PACE_THRESHOLD: 1.2,   // Alert if pacing 20% over
  UNDER_PACE_THRESHOLD: 0.6,  // Alert if pacing 40% under
};

function main() {
  var now = new Date();
  var dayFraction = (now.getHours() * 60 + now.getMinutes()) / (24 * 60);
  var alerts = [];

  var campaignIterator = AdsApp.campaigns()
    .withCondition('Status = ENABLED')
    .get();

  while (campaignIterator.hasNext()) {
    var campaign = campaignIterator.next();
    var budget = campaign.getBudget();
    var dailyBudget = budget.getAmount();
    var todayStats = campaign.getStatsFor('TODAY');
    var spent = todayStats.getCost();
    var expectedSpend = dailyBudget * dayFraction;
    var paceRatio = expectedSpend > 0 ? spent / expectedSpend : 0;

    if (paceRatio > CONFIG.OVER_PACE_THRESHOLD) {
      alerts.push(campaign.getName() + ': OVER-PACING ' + (paceRatio * 100).toFixed(0) + '% (spent $' + spent.toFixed(2) + ' of $' + dailyBudget + '/day)');
    } else if (paceRatio < CONFIG.UNDER_PACE_THRESHOLD && dayFraction > 0.25) {
      alerts.push(campaign.getName() + ': UNDER-PACING ' + (paceRatio * 100).toFixed(0) + '% (spent $' + spent.toFixed(2) + ' of $' + dailyBudget + '/day)');
    }
  }

  if (alerts.length > 0) {
    MailApp.sendEmail(CONFIG.EMAIL, '[Google Ads] Budget Pacing Alert', alerts.join('\n'));
  }
  Logger.log('Budget check complete. ' + alerts.length + ' alerts.');
}
```

#### D. Google Sheets Performance Report Script
Exports campaign performance to a Google Sheet.

```javascript
var CONFIG = {
  SPREADSHEET_URL: 'https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/edit',
  SHEET_NAME: 'Daily Report',
  DATE_RANGE: 'LAST_30_DAYS'
};

function main() {
  var ss = SpreadsheetApp.openByUrl(CONFIG.SPREADSHEET_URL);
  var sheet = ss.getSheetByName(CONFIG.SHEET_NAME) || ss.insertSheet(CONFIG.SHEET_NAME);

  // Header row
  sheet.clearContents();
  sheet.appendRow(['Campaign', 'Impressions', 'Clicks', 'CTR', 'Avg CPC', 'Cost', 'Conversions', 'CPA', 'Conv Rate']);

  var campaignIterator = AdsApp.campaigns()
    .withCondition('Status = ENABLED')
    .forDateRange(CONFIG.DATE_RANGE)
    .get();

  while (campaignIterator.hasNext()) {
    var campaign = campaignIterator.next();
    var s = campaign.getStatsFor(CONFIG.DATE_RANGE);
    var conv = s.getConversions();
    var cost = s.getCost();

    sheet.appendRow([
      campaign.getName(),
      s.getImpressions(),
      s.getClicks(),
      (s.getCtr() * 100).toFixed(2) + '%',
      '$' + s.getAverageCpc().toFixed(2),
      '$' + cost.toFixed(2),
      conv,
      conv > 0 ? '$' + (cost / conv).toFixed(2) : 'N/A',
      (s.getConversionRate() * 100).toFixed(2) + '%'
    ]);
  }

  Logger.log('Report written to Google Sheets');
}
```

### 4. Custom Script Generation

For any custom request not covered above:
1. Map the user's requirement to AdsApp methods
2. Add DRY_RUN = true by default for scripts that modify data
3. Always log actions to Logger.log() for the script's Logs tab
4. Use CONFIG object at top for all user-editable values
5. Test on a single campaign/ad group first before scaling

### 5. Key AdsApp Methods Reference

```
Iteration:
  AdsApp.campaigns().get()
  AdsApp.adGroups().get()
  AdsApp.keywords().get()
  AdsApp.ads().get()

Filters (.withCondition):
  'Status = ENABLED'
  'Cost > 10' (requires .forDateRange())
  'Conversions = 0'
  'CampaignName = "Campaign Name"'
  'LabelNames CONTAINS_ANY ["label"]'

Stats (.getStatsFor(dateRange)):
  DATE_RANGE values: TODAY, YESTERDAY, LAST_7_DAYS, LAST_30_DAYS, THIS_MONTH, LAST_MONTH
  stats.getCost(), getClicks(), getImpressions(), getCtr()
  stats.getConversions(), getConversionRate(), getAverageCpc()

Mutations:
  keyword.pause() / keyword.enable()
  campaign.getBudget().setAmount(X)
  keyword.setMaxCpc(X)
  ad.pause()
```

### 6. Output Format

Always deliver:
1. Complete, copy-paste-ready script
2. Configuration section clearly commented
3. Instructions for where to paste it (Google Ads > Tools > Scripts)
4. Scheduling recommendation
5. What to set DRY_RUN to before going live

## Key Rules
- Always default DRY_RUN = true for scripts that pause/modify anything
- Never use `while(true)` loops — scripts have execution time limits
- Test on small date ranges first, scale up after confirming logic
- Logger.log() is your debugging tool — check the "Logs" tab after running
- Scripts run with account-level permissions — be careful with bulk pause/edit operations
