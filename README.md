# Pacvue Agency Skills (not official from Pacvue)

Claude Code skills powered by the Pacvue MCP API for agency clients.

## Setup

These skills are registered in `~/.claude/settings.json` under `skillPaths`.

**Requires:** `pacvue-mcp` MCP server configured in `~/.claude.json`

---

## Available Skills

### Amazon

| Skill | Usage | Best For |
|-------|-------|----------|
| `/amazon-agency-morning-brief` | No args needed | Daily AM portfolio triage |
| `/amazon-brand-scorecard` | `[profile_name] [period]` | Client calls, QBRs |
| `/amazon-budget-pacing-check` | `[profile_name]` | Mid-month budget reviews |
| `/amazon-agency-sov-tracker` | `[profiles] [period]` | Competitive strategy |
| `/amazon-cross-brand-benchmarks` | `[campaign_tag] [period]` | Agency-wide optimization |
| `/amazon-new-client-onboarding` | `[profile_name]` | New brand audits |
| `/amazon-weekly-client-report` | `[profile_name]` | Weekly client emails |
| `/amazon-campaign-type-analysis` | `[profile_name] [period]` | Media mix optimization |

## Supported Periods
- `last_7_days` (default)
- `last_14_days`
- `last_30_days`
- `this_month`
- `last_month`

## Examples

```
/amazon-agency-morning-brief
/amazon-brand-scorecard "Acme Home Essentials" last_7_days
/amazon-budget-pacing-check "Apex Wellness Co"
/amazon-agency-sov-tracker "Acme Home Essentials, Luminary Health" last_14_days
/amazon-cross-brand-benchmarks "Branded" last_30_days
/amazon-new-client-onboarding "Verdant Beauty Co"
/amazon-weekly-client-report "Horizon Foods (USA)"
/amazon-campaign-type-analysis "Luminary Health" last_30_days
```
