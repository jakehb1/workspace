# XP Market Pack Deep Dive
_Updated: 2026-02-26 — after reading full pack content_

## Pack Inventory (actual vs listed counts)

| Pack | Manifest Heuristics | Site Heuristics | Scenarios | Price |
|------|-------------------|-----------------|-----------|-------|
| Agent-Human Interaction | 15 | 10 | 6 | Free |
| Cron & Automation | 10 | 18 | 7 | $25 |
| DeFi Position Management | 22 | 22 | 8 | $49 |
| Iterative Building | 15 | 15 | 6 | $35 |
| Memory Architecture | 11 | 16 | 6 | $29 |
| Multi-Agent Orchestration | 9 | 20 | 7 | $39 |
| OpenClaw Operations | 16 | 14 | 5 | Free |
| Research & Synthesis | 8 | 12 | 5 | $19 |

⚠️ Several packs have mismatched counts between manifest and the DB. Needs resync.

## Format: xppack-v1
Files: manifest.json, heuristics.json, eval/scenarios.json, lessons.md, playbook.md, frameworks.md (some), examples/ (some)

Heuristic schema: id, text, weight (0.85-1.0), context, severity (critical/high/medium), learned_from (optional but excellent)

## Quality
- Genuinely good. Opinionated, specific, sourced from real pain.
- Best heuristics: DeFi swap deadline, cron timeout bomb, sub-agent zero-context brief
- Eval scenarios are the strongest element — judgment tests, not quizzes
- `learned_from` field ($50 OpenRouter burn, 8 SIGTERMs) is excellent — should be mandatory

## Gaps
- Zero design/visual judgment packs
- Zero creative/brand domain
- Research pack skews crypto — needs broader scenarios
- DB count mismatches need fixing

## Format Issues
- `learned_from` should be mandatory
- No `updated_at` per heuristic
- No `applies_to` platform on individual heuristics
- frameworks.md inconsistently present

## Value
- DeFi at $49 is the clearest ROI: one swap deadline mistake prevented = paid for itself
- Research & Synthesis weakest value: 8 heuristics, crypto-biased, $19 borderline
- Free pack download still gated (bug) — not doing their job as demos

## Pack Ideas for Jakeh

### 1. UI/UX for Crypto Products (~18 heuristics, ~$39)
Wallet connect flow, gas fee UX, tx confirmation states, trust signals, async error recovery, "scary number" problem

### 2. Designing for Digital Collectibles (~14 heuristics, ~$29)
Edition mechanics, reveal flow design, Telegram sticker format constraints, community identity through visuals. From PLAY directly.

### 3. Frontend Prototyping: V1 in a Weekend (~12 heuristics, ~$25)
Scope rules, component selection, animation budget, deploy-first development, V2 deferral patterns

### 4. Product Design for AI-Native Apps (~15 heuristics, ~$35)
Variable output UI design, async loading states, reasoning transparency, AI error UX, trust-building

## Bug to Flag
- Free pack /download endpoint returns HTML (not .xppack file) — needs auth even for free packs
- Marketplace DB heuristic counts don't match pack manifests
