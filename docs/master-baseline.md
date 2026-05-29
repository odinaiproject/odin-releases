# Odin AI — Master Baseline

**Date**: May 25, 2026
**Status**: Authoritative project state across all threads
**Entity**: Odin Technology Group, LLC · Saint Augustine, FL
**App version (canonical)**: v1.0.0

This document is the single source of truth on overlapping facts across threads. If any other artifact conflicts with what's here, this document wins. Updated whenever significant cross-thread state changes (attorney meeting outcomes, domain confirmation, major sprint completion).

---

## 1. Entity & Infrastructure

| Item | Status |
|------|--------|
| Entity | ACTIVE — Odin Technology Group, LLC · Florida · filed May 8, 2026 |
| EIN | OBTAINED |
| Banking | ACTIVE — Wells Fargo business account + debit card (Mercury references in older briefs are superseded) |
| Stripe live keys | ACTIVE — live mode, real payments processing |
| IP Assignment Agreement | EXECUTED May 8, 2026 — Matthew → Odin Technology Group, LLC |
| Domain canonical | PENDING — odinai.app, blocked on Vercel Pro upgrade |
| Vercel Pro upgrade | PENDING — $20/month, required for custom domain |
| Supabase Pro upgrade | PENDING — required before paying user 4 |
| Attorney engagement | INITIATED — Jennifer Connors, Holland & Knight · $10K publisher exemption opinion · email sent May 8 · meeting pending |
| Apple Developer | PENDING — $99/year, enables notarization |
| Current address | 359 Zancara Street, Saint Augustine FL 32084 (mail forwarding service signup pending) |

## 2. Product State

- **Repos**:
  - Desktop: `github.com/odinaiproject/odin-app`
  - Web: `github.com/odinaiproject/odinai-website`
- **Platform**: macOS Apple Silicon (arm64) only at v1 · Intel deprecated · Windows pending GitHub Actions
- **Web**: `odinai-website.vercel.app` — full feature parity with desktop achieved
- **AI model**: Anthropic Claude Sonnet (`claude-sonnet-4-20250514`)
- **Build status**: 32/32 endpoints passing functional check · all warm-up sub-10ms after 35s startup
- **Algorithm Reference**: v1.2.18 (hybrid OdinScore methodology) · v1.2.19 staged for attorney tier label
- **Intelligence Expansion Brief**: v1.1 · all 29 capabilities BUILT in V1 code (App Dev May 24-25 sprint)
- **Sidebar**: 8 sections, ~28 items: Portfolio / Scanners / Signals / Markets / Intelligence / Calendar / Research

## 3. Pricing — Norse Three-Tier (Locked 90-Day Commit)

| Brand | Internal | Monthly | Annual | Founding (waitlist only) | Trial |
|-------|----------|---------|--------|-------------------------|-------|
| Nord | free | $0 | — | — | — |
| Viking | basic | $24.99 | $199.99/yr · Save $100 | Not offered | 7 days |
| Valkyrie | pro | $49.99 | $399/yr · 2 months free | $349/yr OR $39.99/mo | 7 days |
| Advisory | advisory | TBD ~$199/seat/mo | Contact | — | Post-launch |

**Discipline**: Norse names live at consumer-facing display layer ONLY. Internal Supabase IDs (`free`/`basic`/`pro`) and Stripe Price IDs unchanged. Pricing locked 90 days post-launch with explicit day-90 review.

## 4. Live Stripe Price IDs (Live Mode)

| Plan | Env Variable | Price ID |
|------|--------------|----------|
| Valkyrie Monthly | `STRIPE_PRICE_ID` | `price_1TXWidK9eo0P9RNGM954rRw3` |
| Valkyrie Annual | `STRIPE_ANNUAL_PRICE_ID` | `price_1TXWkcK9eo0P9RNGnaa2TARj` |
| Viking Monthly | `STRIPE_VIKING_MONTHLY_PRICE_ID` | `price_1TXR43K9eo0P9RNGee8XNB4i` |
| Viking Annual | `STRIPE_VIKING_ANNUAL_PRICE_ID` | `price_1TXR42K9eo0P9RNGaWA4RcM8` |

**Founding member architecture**: Stripe coupon mechanism on standard Valkyrie Price IDs — NOT separate Price IDs. `allow_promotion_codes: True` on desktop checkout matches web.

## 5. Founding Member Mechanics

- Waitlist threshold: **350 signups**
- Target conversion cohort: ~50 paying members
- Founding annual: **$349/year** — locked for life while subscribed
- Founding monthly: **$39.99/month** — intentional alpha/beta reward
- Distribution: **Email-only** · NEVER shown on public pricing page
- Urgency framing: **scarcity-based "[N] spots remaining"** — NEVER 72-hour or time-based
- Conversion mechanism: Stripe coupon applied to standard Valkyrie checkout

## 6. Asset Universe

- Tier 1 (core): ~538 — S&P 500 + Nasdaq 100 + always-include ETFs/crypto · weekly Wikipedia cache
- Tier 2: ~270 — S&P 400 mid-caps · loaded on-demand
- **Combined active universe: ~800 symbols** (canonical for external comms)
- Nord / Viking: core universe only · Valkyrie: full universe · **enforced at API router level, not UI**

## 7. Critical Path to Commercial Launch

The single highest-leverage Matthew action is **Vercel Pro upgrade + domain canonical confirmation**. This step alone unblocks 6+ downstream items. Attorney meeting is the longest lead time but runs in parallel.

1. Vercel Pro upgrade ($20/mo) → enables custom domain
2. Confirm domain canonical (odinai.app) + DNS pointing → unblocks ToS, PP, Resend, support@, Stripe redirects, geo-lock Test 3
3. Schedule attorney meeting (parallel) → unblocks tier label, Section 6 items, ToS review, /refer, trade secret, brand guardrails
4. Apple Developer + notarization (parallel)
5. Mail forwarding service signup (parallel) → address propagation in ToS, PP, email footers, KB
6. Update `NEXT_PUBLIC_APP_URL` after domain
7. Resend domain verification
8. ToS + Privacy Policy deploy (post-attorney)
9. Geo-lock Test 3 on live domain
10. Founding member email assembly (pending coupon confirm + threshold + alpha quotes)
11. Waitlist hits 350 → founding member email sends
12. Commercial public launch

## 8. Pre-Commercial Launch Blocker Inventory

| Item | Owner | Status |
|------|-------|--------|
| Attorney meeting + written publisher opinion | Matthew + Attorney | PENDING |
| ToS deployed and attorney-reviewed | Web Dev + Attorney | BLOCKED |
| Vercel Pro upgrade | Matthew | PENDING |
| Supabase Pro upgrade | Matthew | PENDING |
| Credential rotation (full sequence) | Matthew + App Dev | PENDING |
| Yahoo Finance → commercial provider | R&D + App Dev | PENDING |
| Mailing address in all email footers | App Dev + Marketing | BLOCKED on mail forwarding |
| Supabase DPA executed | Matthew | PENDING |
| Vercel DPA active (post Pro upgrade) | Matthew | PENDING |
| Mail forwarding signup + address propagation | Matthew | PENDING |
| Registered agent — Florida DOS | Matthew | PENDING |
| Business insurance (E&O + GL) | Matthew | PENDING |
| Data breach notification protocol | Compliance | IN PROGRESS |
| Anthropic credit top-up | Matthew | PENDING |
| Geo-lock Test 3 (real non-US IP) | Matthew | PENDING |
| Founding member coupon enforcement | App Dev | PENDING |
| Founding member email deploy | Marketing | BLOCKED |
| support@odinai.app active | Matthew | BLOCKED on domain |
| Apple Developer + notarization | Matthew | PENDING |
| ADA — Next.js app pages | Web Dev + App Dev | PENDING |

## 9. Thread Status

- **App Dev**: ACTIVE — Intelligence Expansion Brief v1.1 (29 capabilities) all built. Sidebar restructured. Quality sprint complete. Hybrid OdinScore implementation next.
- **Web Dev**: ACTIVE — full platform parity sprint complete. Payment flow confirmed end-to-end. ADA passing. Awaiting domain for ToS/PP deployment.
- **R&D**: ACTIVE — Algorithm Reference v1.2.18 + Intelligence Expansion Brief v1.1 delivered. Sprint 2 planned. v1.2 brief update recommended (12 gaps identified).
- **Compliance**: ACTIVE — 11 of 13 hard blockers closed since May 8. Risk level LOW. Attorney engagement initiated. 5 hold items pending counsel.
- **Marketing**: ACTIVE — 30-day social library executing. Onboarding emails revised. Founder Reference doc produced.
- **Creatives**: ACTIVE — 14 SVG templates approved (8 square + 8 story, 6 content types).
- **Sales**: DORMANT — startup brief delivered. Founder-led when active.
- **Tech Support**: BUILT — UptimeRobot live, KB 14 articles + 20 templates compliance-cleared, awaiting support@ activation.
- **Executive**: ACTIVE — Master PM Update v3 May 25. Feature Matrix v2 final. Publisher exemption probability 75-85%.

## 10. Open Decisions Requiring Matthew

1. Vercel Pro timing — recommend this week
2. Domain canonical confirmation — odinai.app
3. Attorney meeting scheduling — Jennifer Connors, H&K
4. Mail forwarding path — third-party recommended ($15-30/mo)
5. **R&D Item 1**: Brief v1.2 update scope — R&D recommends Option A (full update)
6. **R&D Item 2**: "Upside Factors/Risk Factors" vs "Historical Context/Watch Factors" — Compliance ruling needed
7. **R&D Item 3**: Confirm "Signal Search" name
8. **R&D Item 4**: Mobile design principle — R&D recommends ambient awareness
9. **Marketing M-1**: Approve Onboarding_Emails_Revised.docx
10. 350 waitlist threshold confirmation
11. **Marketing M-4**: Distribute Founder Reference doc to all project threads
12. Live trading guardrails (interim until attorney clears): no explicit asset-signal connections in public posts
13. Founding member cohort cap

## 11. Sprint Status

- **Sprint 1**: COMPLETE — R2 Insider Cluster Radar, R3 Sector Rotation Radar, `radar_scores` table, multi-mode UI, S2 Credit composite, P2 Aggregate insider
- **Sprint 2**: PLANNED — M1 Yield Curve Morphology, M3 Fed Policy, M2 Global Liquidity Phase 1, SY1 Narrative Engine, SY2 Signal Divergence, Signal Search Phase 1
- **Sprint 3**: STAGED — S1 Market Breadth, P2 Smart Money sector breakdown, M5 LEI, P1 Put/Call, FL1 Pre-Earnings, FL2 Systemic Risk

## 12. Document Register

**Cross-thread authoritative:**

- This document (Master Baseline) — current
- Master PM Update v3 — current
- Algorithm Reference v1.2.18 — current (see `docs/algorithm.md`)
- Intelligence Expansion Brief v1.1 — current (v1.2 update recommended)
- Compliance Master Brief #2 (May 18) — current (see `docs/compliance.md`)
- Cross-Platform Copy Brief Final — active (terminology question open)
- Feature Matrix v2 — authoritative V1-V4 gating (see `docs/tier-gating.md`)
- IP Assignment Agreement — executed May 8
- Master Credential Inventory — needs refresh (Wells Fargo replaces Mercury, live Stripe IDs, EIN obtained)
- Matthew Manyak Founder Reference — authoritative

**Stale artifacts to refresh:**

- Original Executive Summary (pre-Norse pricing, 193 asset count)
- Brand Pitch Brief (same issues)
- Older Master Technical Reference (pre-v1.2.18)
- Alpha Install Guide v1.2.11 (old version)
- Master Credential Inventory (Mercury references, test Stripe IDs)
