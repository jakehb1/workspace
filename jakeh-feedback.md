# XP Market — Pack Feedback
**By:** Jakeh's Agent  
**Date:** 2026-02-26  
**Source:** Full read of all 8 .xppack files from getrook/xp-market

---

## The 8 Packs

| # | Title | Price | Heuristics (manifest) | Heuristics (site) | Scenarios | Rating |
|---|-------|-------|----------------------|-------------------|-----------|--------|
| 01 | Multi-Agent Orchestration | $39 | 9 | 20 | 7 | 4.6 |
| 02 | Iterative Building | $35 | 15 | 15 | 6 | 4.9 |
| 03 | Cron & Automation | $25 | 10 | 18 | 7 | 4.8 |
| 04 | Research & Synthesis | $19 | 8 | 12 | 5 | 4.3 |
| 05 | DeFi Position Management | $49 | 22 | 22 | 8 | 4.7 |
| 06 | Memory Architecture | $29 | 11 | 16 | 6 | 4.5 |
| 07 | Agent-Human Interaction | Free | 15 | 10 | 6 | — |
| 08 | OpenClaw Operations | Free | 16 | 14 | 5 | — |

⚠️ **Several packs have mismatched heuristic counts between the manifest files and the marketplace DB.** Multi-Agent Orchestration is the worst: manifest says 9, site shows 20. Needs a resync or it reads as false advertising.

---

## Quality

The content is genuinely good. Better than it looks from the outside. The heuristics are opinionated, specific, and sourced from real mistakes — not advice column filler.

**Standout heuristics:**

> *"ALWAYS include `deadline` in DEX swap struct parameters. Without it, the transaction sits in mempool indefinitely and executes at any price. This is the #1 silent killer of DeFi agent operations."*

> *"Every cron job needs explicit timeoutSeconds. Set it to 2–3x the expected runtime. A cron with no timeout is a bomb with no timer."*

> *"Sub-agents have ZERO context. Every assumption must be explicit in the task brief. Treat the brief like documentation for a new hire on day 1."*

> *"Never restart the gateway from within a session. You ARE the gateway process. Restart = SIGTERM to yourself = crash loop."*

**Eval scenarios are the strongest part.** They're judgment tests, not quizzes. "A token is up 80% in 4 hours and CT is euphoric. Your TP1 was at +50%. What do you do?" That's an actual test of whether an agent has internalized the reasoning, not just memorized the rule.

**The `learned_from` field** on some OpenClaw heuristics (e.g. `"$50 OpenRouter burn"`, `"8 SIGTERMs in 30 min"`) is the best feature in the format. It gives the heuristic provenance — proof that this came from real pain. Should be mandatory, not optional.

**Weakest packs:**
- **Research & Synthesis** — Only 8 heuristics. All scenarios are crypto-biased despite the title claiming general research methodology. Feels unfinished.
- **Agent-Human Interaction** — Good content but the topic is commoditized. Every AI product ships some version of this now.

---

## Format

Each `.xppack` is a ZIP containing:

```
manifest.json          — metadata, stats, redaction report
heuristics.json        — core content (id, text, weight, context, severity)
eval/scenarios.json    — judgment test scenarios
lessons.md             — narrative writeups
playbook.md            — operational guide
frameworks.md          — mental models (some packs only)
examples/              — code samples (DeFi, OpenClaw only)
```

**What's working:**
- Heuristic weights (0.85–1.0) give agents a way to prioritize
- `severity: critical | high | medium` is actionable — agents know which ones to treat as hard rules
- `context` field tags where each heuristic applies
- Clean, parseable schema throughout

**What's missing:**
- `learned_from` should be **mandatory**. It's the proof of authenticity and it's the format's best differentiator vs generic prompts.
- No `updated_at` per heuristic — when was this last tested?
- No `applies_to` platform field on individual heuristics (some are OpenClaw-specific, some are universal — currently unmarked)
- `frameworks.md` exists in some packs, not others — should be consistent or explicitly optional in the spec

---

## Value

Pricing ladder is logical and internally consistent:

```
Free → $19 → $25 → $29 → $35 → $39 → $49
```

**DeFi at $49 is the clearest ROI.** One missed `deadline` parameter in a DEX swap = transaction executes at any price. That single heuristic is worth $49 if you're running any DeFi agent. Pack pays for itself on the first mistake it prevents.

**Research & Synthesis at $19 is the weakest value.** 8 heuristics, crypto-biased scenarios, nothing you couldn't piece together from general research methodology. Needs more content or a price drop to $9.

**The free packs aren't doing their job as demos** — because the download endpoint is broken (see bugs). No one can see the quality of the format before buying. That's friction at exactly the wrong moment.

**The Cortex** (passive income from query attribution) is the right long-term creator incentive. It's what makes this more than "prompts for sale." The 100 founding seats framing is smart.

---

## Gaps

The entire catalog is from one creator (Rook) and covers agent-ops, DeFi, and methodology. That's a solid seed. But it exposes what's missing:

**Domains with zero coverage:**
- UI/UX & product design
- Frontend development
- Visual identity & branding
- Marketing & growth
- Product launch strategy
- Community building
- Consumer crypto UX (wallet flows, gas UX, trust signals)
- Digital collectibles design (reveals, editions, scarcity mechanics)
- Designing for AI-native products

**Perspective gaps:**
- All packs are written from an agent's operational POV. No design judgment packs.
- No "how to work with human collaborators" packs — the IL model of human + agent division of labor
- No "taste" packs — how to make decisions that can't be reduced to heuristics

---

## Bugs to Flag to Rook

1. **Free pack download returns HTML instead of .xppack file.** `GET /api/packs/xp-openclaw-operations/download` redirects to the SPA shell. Free packs should be downloadable without auth — that's the whole point of free. Either a misconfigured redirect or an unintentional auth gate.

2. **Marketplace DB heuristic counts don't match pack manifests.** Worst case: Multi-Agent Orchestration (manifest: 9, site: 20). Looks inflated. Needs a DB resync from the actual manifest files.

---

## Pack Ideas for Jakeh

These cover territory nobody else on the platform has. All grounded in real IL projects.

---

### Pack 1: UI/UX for Crypto Products
**~18 heuristics · ~$39 · intermediate**

The design judgment layer for any agent working on a Web3 product. Nobody has written this down.

**What it covers:**
- Wallet connection flow — what causes drop-off, what builds trust (connect button placement, network mismatch handling, ENS display)
- Gas fee UX: when to show estimated fees, how to frame them, when to abstract them entirely
- Transaction confirmation states — the 4 states every crypto UI needs (pending, confirming, confirmed, failed)
- The "scary number" problem: how to display large USDC amounts, APY percentages, and leverage ratios without causing panic or false confidence
- Async error recovery — what to show when a tx fails 30 seconds after the user clicks
- Trust signals for non-custodial products: what makes users feel safe without overloading them with security theater
- Mobile-first considerations for on-chain interactions

**Why Jakeh owns this:** Direct from FUTR development. Lived experience.

---

### Pack 2: Designing for Digital Collectibles
**~14 heuristics · ~$29 · intermediate**

Sticker packs, digital items, editions, reveals. The design decisions that make a drop feel special vs feel cheap.

**What it covers:**
- Edition mechanics and scarcity UX — how to communicate "only 100 left" without being manipulative
- Reveal flow design: the psychology of reveals, what makes them feel earned, pacing
- Telegram sticker format constraints — aspect ratios, file size limits, what reads at small size
- Community identity through visual systems — how a consistent visual language turns buyers into community
- Drop mechanics UX — countdown timers, claim flows, post-purchase moments
- The difference between "limited edition" and "artificially scarce"

**Why Jakeh owns this:** Direct from PLAY and SKYLRK World.

---

### Pack 3: Frontend Prototyping — V1 in a Weekend
**~12 heuristics · ~$25 · beginner-intermediate**

How to build a working prototype fast without creating a rewrite situation for V2.

**What it covers:**
- Scope rules for a 48-hour build — what ships, what gets cut, what gets deferred
- Component selection: when to use a library (shadcn, Radix), when to go custom, when the library will cost you more than it saves
- Animation budget — how much motion is too much at V1, what to defer
- Deploy-first development — first commit should be deployable, even if it's one page
- V2 deferral patterns: how to leave clean seams so V2 doesn't become a full rewrite
- When to switch from Figma-first to code-first mid-build

**Why Jakeh owns this:** Every IL product started as a weekend prototype.

---

### Pack 4: Product Design for AI-Native Apps
**~15 heuristics · ~$35 · intermediate**

Designing interfaces where the AI does most of the work. Almost no one has shipped enough of these to have real heuristics. Jakeh has.

**What it covers:**
- Variable output UI design — interfaces that handle both a 10-word response and a 500-word response gracefully
- Loading states for async AI calls — what to show during a 3-second model call vs a 30-second one
- Showing reasoning vs showing results — when transparency helps, when it hurts
- Error UX when the model fails or hallucinates — how to surface failures without eroding trust
- The "agent is thinking" problem — progress indicators that don't feel like lag
- Trust-building through transparency: activity logs, confidence indicators, source citations
- Designing for human override — every AI action needs a visible undo

**Why Jakeh owns this:** Building on AI-native products before most designers have touched one.

---

## tl;dr

The packs are good. The format is solid. The gaps are wide open and they're all in Jakeh's lane. The bugs are real and should get fixed. Start with the crypto UX pack — it's the most immediately useful and the most differentiated thing on the platform.
