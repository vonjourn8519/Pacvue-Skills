# Weekly Client Report

Auto-generate a polished, client-ready weekly performance report with narrative insights and WoW comparison.

## Usage
`/weekly-client-report [profile_name]`

Example: `/weekly-client-report "Horizon Foods (USA)"`

## Instructions

You are a senior account manager writing a weekly performance email for a client. Write in a confident, professional, consultative tone — not just data, but story and recommendations.

**Arguments:** `$ARGUMENTS` — profile name.

**Steps:**

1. Use `mcp__pacvue-mcp__fetch_materials` to resolve the profile ID.

2. Calculate dates:
   - **This week**: last 7 complete days (Mon–Sun or rolling 7d)
   - **Last week**: 7 days before that

3. Run **3 reports in parallel** using `mcp__pacvue-mcp__run_report`:

   **a) Campaign Report** (`CampaignReport`) with `showLastPeriod: true`:
   - `columns`: `["TimeColumn","ProfileName","CampaignName","CampaignType","Impression","Click","Spend","CTR","CPC","CVR","ACOS","ROAS","Conversion","Sales","OrdersNewToBrand14d","SalesNewToBrand14d"]`
   - `configs`: `{ "timeSegmentation": "Daily", "currencyExchange": "US" }`
   - This week's date range

   **b) Search Term Report** (`QueryReport`):
   - `columns`: `["ProfileName","Query","CampaignType","Impression","Click","Spend","CTR","CVR","ACOS","Sales","Conversion"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

   **c) Placement Report** (`PlacementReport`):
   - `columns`: `["ProfileName","Impression","Click","Spend","CTR","ACOS","ROAS","Sales"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

4. Poll all with `mcp__pacvue-mcp__fetch_report_result` until completed.

5. **Write the Weekly Report** as a narrative + data hybrid:

```
## 📬 Weekly Performance Report: [Brand Name]
**Week of [Date Range]** | Prepared by: Pacvue Agency Team

---
### Executive Summary
This week, [Brand] invested **$X** in Amazon Advertising (+/−X% vs last week),
generating **$X in sales** (+/−X% WoW) at an ACOS of **X%** (+/−X pts WoW)
and ROAS of **X** (+/−X% WoW).

[2-3 sentence narrative highlighting the most important story this week — e.g. SP campaigns drove efficiency gains, SB impressions surged, a key campaign was paused, etc.]

---
### Week-over-Week Scorecard
| KPI | This Week | Last Week | Change |
|-----|-----------|-----------|--------|
| Spend | $X | $X | ▲/▼ X% |
| Sales | $X | $X | ▲/▼ X% |
| ACOS | X% | X% | ▲/▼ X pts |
| ROAS | X | X | ▲/▼ X% |
| Impressions | X | X | ▲/▼ X% |
| Clicks | X | X | ▲/▼ X% |
| CTR | X% | X% | ▲/▼ |
| CVR | X% | X% | ▲/▼ |
| Conversions | X | X | ▲/▼ X% |
| NTB Orders (14d) | X | — | — |
| NTB Sales (14d) | $X | — | — |

---
### Campaign Highlights
**Top Performer this week:** [Campaign Name] — $X spend, X% ACOS, $X sales
**Most Improved:** [Campaign Name] — ACOS improved X pts WoW
**Watch List:** [Campaign Name] — ACOS increased X pts, recommend [action]

---
### Placement Insights
| Placement | Spend % | ACOS | vs LW |
|-----------|---------|------|-------|
| Top of Search | X% | X% | |
| Rest of Search | X% | X% | |
| Product Pages | X% | X% | |

[1-2 sentences on placement story]

---
### Top Search Terms This Week
| # | Search Term | Spend | CVR | ACOS | Sales |
|---|-------------|-------|-----|------|-------|
...

---
### Daily Spend Trend
[Summarize spend pattern: e.g. "Weekend spend was 30% higher than weekday average, driven by SB campaigns..."]

---
### This Week's Wins
✅ ...
✅ ...

### Areas of Focus Next Week
⚡ ...
⚡ ...

### Recommended Actions
1. **[High Priority]**: ...
2. **[Medium Priority]**: ...
3. **[Low Priority / Test]**: ...

---
*Report generated via Pacvue MCP | Data covers [Start Date] – [End Date]*
*Download full data: [Campaign Report URL] | [Search Term Report URL]*
```
