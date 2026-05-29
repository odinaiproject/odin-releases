# Odin AI — Compliance Discipline

**This file is the highest-importance reference for any code, copy, or communication generated for Odin AI. Read carefully before generating any user-facing content.**

The compliance posture for Odin is *publisher exemption under Lowe v. SEC*. Every word that reaches a user is descriptive of observable data, not advisory. Every numerical score is a distance metric, not a prediction. Every analytical output is framed as historical context, not future guidance.

This is enforced structurally — not as an afterthought. If you find yourself reframing a request to make it compliant, the request itself probably needs to change.

---

## 1. Canonical Terminology (USE THESE)

| Concept | Canonical Label | Internal Code |
|---------|-----------------|---------------|
| Per-asset distance score | **OdinScore** | `valuation.py::conviction_score()` (internal name) |
| AI price target | **OdinCast** | — |
| Multi-signal alert composite | **Convergence Score** | `signals.py::score_signal()` |
| High-conviction tier (≥75) | **NO LABEL DISPLAYED — attorney hold** | — |
| AI synthesis feature | **Odin's Eye** (multi-mode radar at scale) | `radar.py` |
| Crowd convergence | **Odin Pulse** (renamed to avoid Convergence Score conflict) | — |
| Insider activity | **Notable Cluster** · **Insider Score** | `insider.py` + `radar.py` |
| Sector momentum | **Above Trend** / **Neutral** / **Below Trend** | `sectors.py` |
| AI output structure | **Upside Factors / Risk Factors / Summary** | (note: alt "Historical Context / Watch Factors" unresolved) |
| Free tier | **Nord** | `free` (internal) |
| Basic paid | **Viking** | `basic` (internal) |
| Premium paid | **Valkyrie** | `pro` (internal) |
| Methodology quality | **Professional-grade** (interim — "Institutional-grade" on attorney hold) | — |

## 2. Banned Terminology (NEVER USE)

Each term has a compliance or brand reason. App Dev and Web Dev confirm all swept from code/web. When generating new code or copy, **NEVER use any of these**:

- ~~Conviction Score~~ → use **OdinScore**
- ~~Signal Composite~~ → use **OdinScore**
- ~~Price Target~~ → use **OdinCast**
- ~~Verdict~~ → use **Summary**
- ~~Bull Case / Bear Case~~ → use **Upside Factors / Risk Factors**
- ~~High Conviction (as label)~~ → no label displayed pending attorney
- ~~Opportunity Radar~~ → use **Odin's Eye**
- ~~Overweight / Underweight~~ → use **Above Trend / Below Trend**
- ~~Leading / Lagging~~ (sector) → use **Above Trend / Below Trend**
- ~~Win rate / Historical accuracy~~ → use **Historical hit rate / Past observations**
- ~~Buy signal / Sell signal~~ → NEVER use in any form
- ~~Beat the market / Outperform~~ → NEVER use
- ~~Alpha~~ (as feature descriptor) → use **early access**
- ~~Guaranteed returns~~ → NEVER use
- ~~Institutional-grade~~ → use **Professional-grade** (interim, attorney hold)
- ~~72 hours only / time-limited urgency~~ → use scarcity-based threshold framing

## 3. Mandatory Disclaimer

Every page, every output surface, every email footer carries:

> For informational and educational purposes only. Not investment advice. Past performance does not predict future results.

For social media templates and short surfaces:

> Observational data only. Not investment advice.

For Daily Brief outputs specifically, **timestamp adjacent to content** is mandatory (not in footer):

> Brief generated [timestamp]. Market conditions change continuously.

## 4. Approved Framings (USE THESE PHRASINGS)

These are the approved ways to describe Odin's outputs. Use them as templates when generating UI strings, marketing copy, or AI prompts.

### Odin's Eye

> Odin's Eye is the synthesis layer. It runs across the universe and surfaces assets where multiple observable signals concurrently meet defined criteria — valuation zone, sector context, insider activity, macro regime. The output is a Notable Signal: an OdinScore, the upside factors we observed, the risk factors we observed, and a plain-English summary.

### OdinScore

> OdinScore is a 0-100 distance metric. It measures how far an asset's current price sits below or above its long-term moving average — the 200-week MA. Higher score means deeper discount-to-MA. Lower score means greater premium-to-MA. It's a descriptive measure of one observable thing — it's not a probability, it's not a forecast, and it's not a recommendation.

### Zone Agreement Flag (LOCKED EXACT STRING)

> Two independent methodologies produced the same classification from the same observable data.

This is the approved compliance framing — **cannot be modified without re-review**. Fires in State 3 only when Z-score zone and absolute threshold zone produce identical classification.

### Convergence Signals

> Convergence Score combines three observable inputs — current valuation zone, current sector momentum, current cycle phase. When all three line up favorably, the score crosses 55 and an alert fires. Above 75 we flag it as a higher-conviction setup. The score is purely mechanical — it's a sum of three deterministic components. No AI is involved in the calculation.

### Insider Tracker

> We pull SEC EDGAR Form 4 filings every 15 minutes. When 3 or more senior insiders — CEO, CFO, President, Director — file open-market purchases of the same security within a 14-day window, we flag it as a Notable Cluster. The display shows the exact filings, the dollar values, and the timestamps. It's just public data, organized.

### AI Synthesis

> The AI is Anthropic Claude — same model family as ChatGPT-class systems. We use it for synthesis, not for prediction. When you see an Odin's Eye result, the system has already filtered the universe mechanically — that's the deterministic part. Then Claude takes the structured data for that filtered set and writes the plain-English summary. Claude is never asked to predict; it's asked to describe.

## 5. OdinScore Four-State Disclosure Strings (LOCKED)

These four strings are the compliance-cleared disclosures for the hybrid OdinScore states. They are exact-string locked — do not paraphrase.

### State 0 — Insufficient History (bars < 200w)

> OdinScore requires 200 weeks of weekly price history. This asset has {N}w available — ready in approximately {weeks_until}w.

### State 1 — Absolute Fallback (200W SMA exists, Z-window < 52w)

> Limited History — absolute thresholds applied. Z-score activates in ~{weeks_to_z}w.

### State 2 — Expanding Z-score (52w to full lookback)

> Z-score window: {N}w of {M}w — higher variance until full window reached.

### State 3 — Full Hybrid

> Z-score window: full. Hybrid methodology in effect.

## 6. Approved Compliance Moments (For Sales / Marketing Generated Text)

When the topic touches advisory-adjacent territory, use these framings. Don't apologize for what Odin doesn't do — frame the limitations as design choices.

### On not giving advice

> We don't give investment advice — by design, not because we're avoiding it. Every signal you see is descriptive, not predictive. We give you the integrated context, you make the call. That's the model.

### On not having buy/sell signals

> There are no buy or sell signals. We surface observable patterns — valuation distance, insider clusters, sector momentum. Those are facts. Whether to act on them is your judgment. We respect that judgment more than the apps that pretend the algorithm has the answer.

### On historical performance disclaimers

> Past observations don't predict future returns. That's true of any signal anyone has ever surfaced. We're explicit about it because intellectual honesty is the foundation of the product.

### "Should I buy [ticker]?" deflection

> Honest answer: I can't tell you that, and I wouldn't even if I could. Odin doesn't tell you what to buy — and neither do I. What I can tell you is what Odin shows for [ticker] right now: [valuation zone] · [insider activity] · [sector context]. What you do with that is your call. If you want recommendations, you need a registered investment advisor — that's a different product than Odin.

### "What do you personally trade?" deflection (Matthew personal brand)

> I'm going to deflect that one — not because I'm hiding anything, but because if I tell you, it could land as a recommendation, and that's not what we're doing. I'll tell you what I look at: I check Odin's Eye every morning · I watch the regime score · I track sector rotation. What I do with those signals personally is my own decisions, made for my own situation, with my own risk tolerance.

## 7. Attorney Hold Items (Interim Posture)

These items are pending attorney clearance. Until the attorney meeting delivers written guidance, use the interim posture below in any code, copy, or generated content.

| Item | Interim Posture |
|------|-----------------|
| Landing hero headline | "Professional-grade" in use, "Institutional-grade" banned |
| Dynamic regime label on public page | Static label only — no live data display |
| Standing disclaimer sufficiency | Current disclaimer in place + professional consultation sentence |
| Referral programme copy | BLOCKED — no referral copy published anywhere |
| Convergence Score ≥75 tier label | NO LABEL DISPLAYED on any surface |
| Matthew personal brand / live trading | No explicit asset-signal connections in public posts |
| FL3 Options Intelligence Layer copy | Internal/master tier only |
| FL5 Economic Calendar real-time | Internal/master tier only |
| Earnings Reactions + Pattern Library | Internal/master tier only |
| Collaborative watchlist ToS language | Feature built but ToS language pending |

## 8. Matthew Personal Brand Constraint

This is the most legally sensitive area in the entire stack. The SEC has pursued finfluencer cases against founders whose audiences inferred trading recommendations from public trading activity — even without explicit signal-to-trade connections.

**Until attorney clearance:**

- No explicit connection between personal trades and Odin signals in any public format
- Saying "I just bought X and here is what Odin shows" is the specific pattern to avoid
- Talking about markets generally is fine
- General disclosure required on all personal brand platforms: "Matthew Manyak is the founder of Odin AI and may trade assets that appear in Odin's signal outputs."

When generating any code or copy for Matthew's personal brand surfaces, apply this constraint by default.

## 9. Tier Gating — Enforcement Discipline

Tier gating must be **enforced at API router level**, never UI-only. UI restrictions can be bypassed via DevTools or direct API calls. Specifically:

- **Insider Tracker**: Hard wall for Viking. No preview, no teaser. API returns 403 for Viking tier.
- **Odin's Eye buy-zone only for Viking**: Overextended signals must NOT be returned in API response for Viking tier (not hidden in UI).
- **Asset universe**: Core for Nord/Viking (~538). Full for Valkyrie (~800). Enforced at radar.py and screener routes.
- **Smart Alerts split**: Zone/Earnings for Viking+. Convergence for Valkyrie only. Two separate gates.
- **AI Research caps**: Viking 10/mo hard cap. Valkyrie 50/mo soft cap (notification at 40, no hard block).
- **Odin's Eye runs**: Viking 8/mo. Valkyrie unlimited.
- **`_is_valkyrie()` function**: Must check tier name string, NOT `pro_access` flag (which is True for Viking too — bug fixed but worth noting).
- **`_is_viking_plus()` function**: Helper for Viking+ gates.

## 10. Compliance Routing (For Any New Output)

When generating new user-facing content (UI strings, marketing copy, KB articles, email templates, etc.), apply these checks:

1. Does it use any banned terminology? → fix before generating
2. Does it use any approved canonical terminology where applicable? → ensure consistency
3. Does it carry the mandatory disclaimer? → add if user-facing
4. Does it make any performance claims, predictions, or recommendations? → reframe to descriptive
5. Does it touch any attorney-hold item? → use interim posture
6. Is it tier-gated and is the gate enforced at API level? → don't rely on UI alone
7. If Matthew personal brand surface → check constraint in §8

If the answer to any of these is "I'm not sure," route to Compliance thread for review before deployment.

## 11. Compliance Thread Status (May 18, 2026)

- Risk level: **LOW** (unchanged)
- DPAs: 4 of 5 closed (Resend, Render, Stripe live, Vercel PDF) · Supabase pending LLC execution
- Attorney engagement: initiated, meeting pending
- ADA accessibility: all 5 public web pages WCAG 2.1 AA · desktop app 31 elements fixed across 13 files
- Geo-lock: built, tested, compliance-cleared · Test 3 (real non-US IP) pending live domain
- Knowledge base: 14 articles compliance-reviewed · 9 cleared, 6 gated on domain/App Dev
- Response templates: 20/20 cleared
- Hybrid OdinScore: methodology + 4 UI strings cleared
- Trade Journal UI + Odin Pulse UI: cleared
- Monthly newsletter: activated
- Publisher exemption probability: 75-85% overall (attorney converts to near-certainty)
