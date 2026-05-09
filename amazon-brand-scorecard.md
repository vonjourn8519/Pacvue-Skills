# Brand Scorecard

Generate a comprehensive single-brand executive scorecard with period-over-period comparison, ready for client presentation.

## Usage
`/brand-scorecard [profile_name] [period]`

Example: `/brand-scorecard "Acme Home Essentials" last_7_days`

Supported periods: `last_7_days`, `last_14_days`, `last_30_days`, `this_month`, `last_month`

## Instructions

You are a senior account manager preparing a client-facing brand scorecard.

**Arguments:** `$ARGUMENTS` — parse as `[profile_name] [period]`

**Steps:**

1. Use `mcp__pacvue-mcp__fetch_materials` to resolve the profile ID matching the given profile name. If ambiguous, list matches and ask user to confirm.

2. Calculate date ranges:
   - Current period: based on the period argument
   - Prior period: same length immediately before current period

3. Run **3 reports in parallel** using `mcp__pacvue-mcp__run_report`:
   - **Campaign Report** (`CampaignReport`): columns `["TimeColumn","ProfileName","CampaignName","CampaignType","Status","Budget","Impression","Click","Spend","CTR","CPC","CVR","ACOS","ROAS","Conversion","Sales"]`, `timeSegmentation: "Daily"`, with `showLastPeriod: true`
   - **Placement Report** (`PlacementReport`): columns `["TimeColumn","ProfileName","CampaignName","Impression","Click","Spend","CTR","ACOS","ROAS","Sales"]`, `timeSegmentation: "Summary"`
   - **Search Term Report** (`QueryReport`): columns `["TimeColumn","ProfileName","Query","CampaignType","Impression","Click","Spend","CTR","CVR","ACOS","Sales","Conversion"]`, `timeSegmentation: "Summary"`

4. Poll all three with `mcp__pacvue-mcp__fetch_report_result` until completed.

5. **Output the Brand Scorecard:**

```
## 📊 Brand Scorecard: [Brand Name]
### Period: [Start] – [End] vs Prior Period

#### Executive Summary
| KPI | Current | Prior | Change |
|-----|---------|-------|--------|
| Total Spend | $X | $X | ▲/▼ X% |
| Total Sales | $X | $X | ▲/▼ X% |
| ACOS | X% | X% | ▲/▼ X pts |
| ROAS | X | X | ▲/▼ X% |
| Impressions | X | X | ▲/▼ X% |
| Clicks | X | X | ▲/▼ X% |
| CTR | X% | X% | ▲/▼ |
| CVR | X% | X% | ▲/▼ |
| Conversions | X | X | ▲/▼ X% |

#### Top 5 Campaigns by Spend
| Campaign | Type | Spend | ACOS | ROAS | Status |
|----------|------|-------|------|------|--------|
...

#### Placement Performance
| Placement | Spend % | ACOS | ROAS | Impression % |
|-----------|---------|------|------|-------------|
...

#### Top 10 Search Terms
| Search Term | Impressions | CTR | CVR | ACOS | Sales |
|-------------|-------------|-----|-----|------|-------|
...

#### Key Insights
- ✅ Win: ...
- ⚠️ Concern: ...
- 💡 Recommendation: ...

#### Download Links
- Campaign Report: [URL]
- Placement Report: [URL]
- Search Term Report: [URL]
```
