# New Client Onboarding Audit

Run a comprehensive account audit for a newly onboarded brand — generates a structured brief covering account structure, spend distribution, top ASINs, and top search terms.

## Usage
`/new-client-onboarding [profile_name]`

Example: `/new-client-onboarding "Verdant Beauty Co"`

## Instructions

You are a senior account strategist conducting a new client onboarding audit.

**Arguments:** `$ARGUMENTS` — profile name of the new client.

**Steps:**

1. Use `mcp__pacvue-mcp__fetch_materials` to:
   - Resolve the profile ID
   - Fetch all campaign tags for this profile (context: profile ID)
   - Fetch all portfolios for this profile

2. Run **4 reports in parallel** using `mcp__pacvue-mcp__run_report` for the last 30 days:

   **a) Campaign Report** (`CampaignReport`):
   - `columns`: `["ProfileName","CampaignName","CampaignType","Status","Budget","Impression","Click","Spend","CTR","CPC","CVR","ACOS","ROAS","Conversion","Sales","biddingStrategy"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

   **b) ASIN Report** (`ASINReport`):
   - `columns`: `["ProfileName","CampaignName","CampaignType","Impression","Click","Spend","ACOS","ROAS","Sales","Conversion"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

   **c) Search Term Report** (`QueryReport`):
   - `columns`: `["ProfileName","Query","CampaignType","Impression","Click","Spend","CTR","CVR","ACOS","Sales","Conversion"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

   **d) Placement Report** (`PlacementReport`):
   - `columns`: `["ProfileName","CampaignName","Impression","Click","Spend","CTR","ACOS","ROAS","Sales"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

3. Poll all with `mcp__pacvue-mcp__fetch_report_result` until completed.

4. **Output the Onboarding Brief:**

```
## 🆕 New Client Onboarding Brief: [Brand Name]
**Generated:** [Date] | **Data Period:** Last 30 Days

---
### Account Structure
| Element | Count |
|---------|-------|
| Total Campaigns | N |
| Active Campaigns | N |
| Paused Campaigns | N |
| Archived Campaigns | N |
| Portfolios | N |
| Campaign Tags | N |
| SP Campaigns | N |
| SB Campaigns | N |
| SD Campaigns | N |

### 30-Day Performance Summary
| KPI | Value |
|-----|-------|
| Total Spend | $X |
| Total Sales | $X |
| ACOS | X% |
| ROAS | X |
| Total Impressions | X |
| Total Clicks | X |
| CTR | X% |
| CVR | X% |
| Total Conversions | X |

### Spend Distribution by Campaign Type
| Type | Spend | Spend % | ACOS | ROAS |
|------|-------|---------|------|------|
| Sponsored Products | | | | |
| Sponsored Brands | | | | |
| Sponsored Display | | | | |

### Top 10 Campaigns by Spend
| Campaign | Type | Spend | ACOS | ROAS | Status | Bidding |
|----------|------|-------|------|------|--------|---------|
...

### Top 10 ASINs by Sales
| ASIN | Spend | Sales | ACOS | ROAS | Conversions |
|------|-------|-------|------|------|-------------|
...

### Top 20 Search Terms by Spend
| Search Term | Impressions | Clicks | CTR | CVR | Spend | ACOS | Sales |
|-------------|-------------|--------|-----|-----|-------|------|-------|
...

### Placement Performance
| Placement | Spend % | ACOS | ROAS | Impression % |
|-----------|---------|------|------|-------------|
...

### 🔍 Key Findings
- **Strengths:** ...
- **Gaps / Risks:** ...
- **Quick Wins (0–30 days):** ...
- **Strategic Opportunities (30–90 days):** ...

### Recommended First Actions
1. ...
2. ...
3. ...

### Download Links
- Campaign Report: [URL]
- ASIN Report: [URL]
- Search Term Report: [URL]
- Placement Report: [URL]
```
