# Cross-Brand Benchmarks

Compare KPIs across all managed brands filtered by a campaign tag (e.g. SP, SB, Branded, Generic) to identify best/worst performers.

## Usage
`/cross-brand-benchmarks [campaign_tag] [period]`

Example: `/cross-brand-benchmarks "Branded" last_30_days`
Example: `/cross-brand-benchmarks "SP" last_7_days`

## Instructions

You are an agency analytics lead benchmarking performance across all client brands.

**Arguments:** `$ARGUMENTS` — campaign tag name and period.

**Steps:**

1. Use `mcp__pacvue-mcp__fetch_materials` to:
   - Get all profile IDs
   - Get campaign tag IDs — find the tag ID matching the given tag name (case-insensitive)

2. Run `mcp__pacvue-mcp__run_report` — **Campaign Tag Report** (`CampaignTagReport`) with:
   - `startDate` / `endDate`: based on period argument
   - `columns`: `["ProfileName","CampaignTag","Impression","Click","Spend","CTR","CPC","CVR","ACOS","ROAS","Conversion","Sales","OrdersNewToBrand14d","SalesNewToBrand14d"]`
   - `configs`: `{ "timeSegmentation": "Summary", "currencyExchange": "US" }`
   - `filters`: `{ "profile": [<all_profile_ids>], "campaign_tag": [<tag_id>] }`

3. Poll with `mcp__pacvue-mcp__fetch_report_result` until completed.

4. **Calculate agency benchmarks** across all brands:
   - Median and mean for: ACOS, ROAS, CTR, CVR, CPC
   - Rank brands from best to worst for each KPI

5. **Output the Benchmark Report:**

```
## 📊 Cross-Brand Benchmarks — Tag: "[Tag]" | [Period]

### Agency Benchmarks (N brands)
| KPI | Best | Median | Mean | Worst |
|-----|------|--------|------|-------|
| ACOS | X% | X% | X% | X% |
| ROAS | X | X | X | X |
| CTR | X% | X% | X% | X% |
| CVR | X% | X% | X% | X% |
| CPC | $X | $X | $X | $X |

### Brand Rankings
| Rank | Brand | Spend | ACOS | ROAS | CTR | CVR | vs Median ACOS |
|------|-------|-------|------|------|-----|-----|----------------|
| 🥇 1 | ... | | | | | | |
...

### 🌟 Top Performers (ACOS significantly below median)
| Brand | ACOS | Median | Delta | What's working |
|-------|------|--------|-------|----------------|
...

### ⚠️ Underperformers (ACOS significantly above median)
| Brand | ACOS | Median | Delta | Likely issue |
|-------|------|--------|-------|-------------|
...

### New-to-Brand Performance (14d)
| Brand | NTB Orders | NTB Sales | NTB Order % |
|-------|-----------|-----------|------------|
...

### Agency-Wide Recommendations
1. Share [Top Brand]'s strategy with underperformers — X% lower ACOS
2. ...

### Download: [URL]
```
