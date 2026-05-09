# Agency SOV Tracker

Monitor Share of Voice across your client portfolio and surface competitive gains/losses.

## Usage
`/agency-sov-tracker [profile_names] [period]`

Example: `/agency-sov-tracker "Acme Home Essentials, Apex Wellness Co" last_7_days`
Omit profiles to run for all. Omit period to default to last 7 days.

## Instructions

You are a competitive intelligence analyst tracking Share of Voice for agency clients.

**Arguments:** `$ARGUMENTS` — comma-separated profile names (optional) and period (optional).

**Steps:**

1. Use `mcp__pacvue-mcp__fetch_materials` to resolve profile IDs.

2. Run `mcp__pacvue-mcp__run_report` — **SOV Report** (`SOVReport`) for each profile with:
   - `startDate` / `endDate`: based on period argument (default: last 7 days)
   - `columns`: `["TimeColumn","ProfileName","KeywordGroup","Brand","Impression","SOV","Rank","SearchVolume","Click","Spend"]`
   - `configs`: `{ "timeSegmentation": "Summary", "currencyExchange": "US" }`
   - `filters`: `{ "profile": [<profile_ids>] }`
   - Also run with `showLastPeriod: true` for period-over-period comparison

3. Poll all with `mcp__pacvue-mcp__fetch_report_result` until completed.

4. **Output the SOV Report:**

```
## 📡 Share of Voice Tracker — [Period]

### Portfolio SOV Overview
| Brand | Avg SOV % | SOV Change (PoP) | Avg Rank | Top Keyword Group |
|-------|-----------|-----------------|----------|-------------------|
...

### 📈 SOV Winners (gained most)
| Brand | Keyword Group | SOV Now | SOV Before | Change |
|-------|---------------|---------|------------|--------|
...

### 📉 SOV Losers (lost most)
| Brand | Keyword Group | SOV Now | SOV Before | Change | Likely Competitor |
|-------|---------------|---------|------------|--------|------------------|
...

### 🏆 SOV by Keyword Group (Top 10 groups)
| Keyword Group | Brand | SOV % | Rank | Search Volume |
|---------------|-------|-------|------|---------------|
...

### Competitive Alerts
- ⚠️ [Brand] lost X% SOV on "[keyword group]" — possible competitor surge
- ✅ [Brand] gained X% SOV — bid increases paying off

### Strategic Recommendations
1. ...
2. ...

### Download Links
[Per-profile report URLs]
```
