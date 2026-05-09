# Campaign Type Analysis

Break down SP vs SB vs SD vs STV performance side-by-side and recommend optimal budget reallocation.

## Usage
`/campaign-type-analysis [profile_name] [period]`

Example: `/campaign-type-analysis "Luminary Health" last_30_days`

## Instructions

You are a media mix strategist analyzing campaign type performance to optimize budget allocation.

**Arguments:** `$ARGUMENTS` — profile name and period (default: last 30 days).

**Steps:**

1. Use `mcp__pacvue-mcp__fetch_materials` to resolve the profile ID.

2. Run **2 reports in parallel** using `mcp__pacvue-mcp__run_report`:

   **a) Campaign Report by Type** (`CampaignReport`) with `showLastPeriod: true`:
   - `columns`: `["TimeColumn","ProfileName","CampaignName","CampaignType","Impression","Click","Spend","CTR","CPC","CVR","ACOS","ROAS","Conversion","Sales","AttributedDetailPageView14d","OrdersNewToBrand14d","SalesNewToBrand14d","PlacementReport"]`
   - `configs`: `{ "timeSegmentation": "Summary", "currencyExchange": "US" }`
   - `filters`: `{ "profile": [<profile_id>] }`

   **b) Placement Report** (`PlacementReport`):
   - `columns`: `["ProfileName","CampaignName","CampaignType","Impression","Click","Spend","CTR","ACOS","ROAS","Sales"]`
   - `configs`: `{ "timeSegmentation": "Summary" }`

3. Poll both with `mcp__pacvue-mcp__fetch_report_result` until completed.

4. **Aggregate by campaign type** (SP / SB / SD / STV) and calculate:
   - Spend share % of total
   - ACOS, ROAS, CTR, CVR, CPC per type
   - NTB contribution (orders, sales, %) per type
   - Detail Page Views per type (awareness signal for SB/SD)
   - Efficiency score: ROAS relative to spend share

5. **Output the Campaign Type Analysis:**

```
## 🧩 Campaign Type Analysis: [Brand Name]
**Period:** [Start] – [End] | vs Prior Period

---
### Media Mix Overview
| Type | Spend | Spend % | ▲/▼ vs Prior |
|------|-------|---------|-------------|
| Sponsored Products (SP) | $X | X% | ▲/▼ X pts |
| Sponsored Brands (SB) | $X | X% | ▲/▼ X pts |
| Sponsored Display (SD) | $X | X% | ▲/▼ X pts |
| Sponsored TV (STV) | $X | X% | ▲/▼ X pts |
| **Total** | **$X** | **100%** | |

---
### Performance by Campaign Type
| KPI | SP | SB | SD | STV | Best |
|-----|----|----|----|----|------|
| ACOS | X% | X% | X% | X% | 🏆 |
| ROAS | X | X | X | X | 🏆 |
| CTR | X% | X% | X% | X% | 🏆 |
| CVR | X% | X% | X% | X% | 🏆 |
| CPC | $X | $X | $X | $X | 🏆 |
| DPV (14d) | X | X | X | — | 🏆 |

---
### New-to-Brand Contribution (14d)
| Type | NTB Orders | NTB Orders % | NTB Sales | NTB Sales % |
|------|-----------|-------------|-----------|------------|
| SP | | | | |
| SB | | | | |
| SD | | | | |

*Note: SB/SD typically drive higher NTB than SP — a healthy NTB % indicates brand growth*

---
### Funnel Role Assessment
| Type | Primary Role | Current Efficiency | Recommended Role |
|------|-------------|-------------------|-----------------|
| SP | Conversion / Harvest | [Efficient/Inefficient] | [Maintain/Scale/Cut] |
| SB | Awareness / NTB | [Efficient/Inefficient] | [Maintain/Scale/Cut] |
| SD | Retargeting / Defense | [Efficient/Inefficient] | [Maintain/Scale/Cut] |
| STV | Upper Funnel | [Efficient/Inefficient] | [Maintain/Scale/Cut] |

---
### Budget Reallocation Recommendation
**Current allocation:** SP X% / SB X% / SD X% / STV X%
**Recommended allocation:** SP X% / SB X% / SD X% / STV X%

| Move | From | To | Rationale |
|------|------|----|-----------|
| $X | SD | SP | SP ROAS is X× higher — reinvest in what's working |
| $X | SP | SB | NTB % is low — invest in brand awareness to build pipeline |
...

---
### Strategic Insights
- **SP**: [1-2 sentence insight]
- **SB**: [1-2 sentence insight]
- **SD**: [1-2 sentence insight]
- **Overall**: [Key takeaway and next step]

---
### Recommended Actions
1. **Immediate (this week):** ...
2. **Short-term (2–4 weeks):** ...
3. **Test to consider:** ...

### Download Links
- Campaign Report: [URL]
- Placement Report: [URL]
```
