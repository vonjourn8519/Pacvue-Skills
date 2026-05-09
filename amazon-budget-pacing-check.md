# Budget Pacing Check

Check whether campaigns are on track to hit monthly budget targets and flag over/under-pacing brands.

## Usage
`/budget-pacing-check [profile_name]`

Example: `/budget-pacing-check "Apex Wellness Co"`
Omit profile name to check ALL profiles.

## Instructions

You are a media investment analyst checking budget pacing for the current month.

**Arguments:** `$ARGUMENTS` — profile name (optional). If omitted, run for all profiles.

**Steps:**

1. Determine today's date and calculate:
   - `days_elapsed`: days passed in the current month (including today)
   - `days_remaining`: days left in the current month
   - `days_total`: total days in the current month
   - `expected_spend_pct`: days_elapsed / days_total × 100

2. Use `mcp__pacvue-mcp__fetch_materials` to resolve profile ID(s).

3. Run `mcp__pacvue-mcp__run_report` — **Campaign Report** with:
   - `startDate`: first day of current month
   - `endDate`: yesterday
   - `columns`: `["ProfileName","CampaignName","CampaignType","Status","Budget","ActlAvl","Impression","Spend","Sales","ACOS","ROAS"]`
   - `configs`: `{ "timeSegmentation": "Summary", "currencyExchange": "US" }`
   - `filters`: `{ "profile": [<profile_ids>] }`

4. Poll with `mcp__pacvue-mcp__fetch_report_result` until completed.

5. **Calculate pacing for each campaign:**
   - `actual_spend_pct` = (spend_to_date / budget) × 100
   - `pacing_delta` = actual_spend_pct − expected_spend_pct
   - 🔴 **Overpacing**: pacing_delta > +15% (at risk of exhausting budget early)
   - 🟡 **Underpacing**: pacing_delta < -15% (underdelivering, leaving money on table)
   - 🟢 **On Track**: within ±15%

6. **Output the Pacing Report:**

```
## 💰 Budget Pacing Check — [Month Year]
**As of [Date] — Day [N] of [Total] ([X]% through month)**

### Portfolio Pacing Summary
| Profile | Monthly Budget | Spent to Date | Remaining | Pace % | Status |
|---------|---------------|---------------|-----------|--------|--------|
...

### 🔴 Overpacing Campaigns (risk of early budget exhaustion)
| Profile | Campaign | Budget | Spent | Pace % | Est. Exhaustion Date |
|---------|----------|--------|-------|--------|---------------------|
...

### 🟡 Underpacing Campaigns (underdelivering)
| Profile | Campaign | Budget | Spent | Pace % | Est. Month-End Spend |
|---------|----------|--------|-------|--------|---------------------|
...

### 💡 Recommended Actions
- Overpacing: Consider budget caps, bid reductions, or dayparting
- Underpacing: Consider bid increases, budget raises, or expanded targeting

### Download: [URL]
```
