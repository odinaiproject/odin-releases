# Odin AI — Tier Gating Reference (Feature Matrix v2)

**Authority**: This file is authoritative on all tier gating decisions. Supersedes earlier "Feature Matrix Executive" brief on five reconciled items. When generating code for any feature, check the matrix here before assuming a tier boundary.

**Critical discipline**: Tier gates must be enforced at **API router level**, not UI-only. UI restrictions can be bypassed via DevTools or direct API calls. If you're writing a new tier-gated feature and only adding a UI check, the implementation is incomplete.

---

## 1. Three-Tier Structure

| Brand | Internal ID | Monthly | Annual |
|-------|-------------|---------|--------|
| Nord (free) | `free` | $0 | — |
| Viking (basic) | `basic` | $24.99 | $199.99/yr |
| Valkyrie (pro) | `pro` | $49.99 | $399/yr |

Founding member: $349/yr or $39.99/mo — applied as Stripe coupon on standard Valkyrie checkout. Not a separate Price ID.

Advisory: Custom-quoted post-launch, not exposed in UI at v1.

## 2. V1 Feature Matrix (Launch)

| Feature | Nord | Viking | Valkyrie |
|---------|------|--------|----------|
| Dashboard + prices | ✓ | ✓ | ✓ |
| Valuation Zones — core (~538 assets) | ✓ | ✓ | ✓ |
| Valuation Zones — full (~800 assets) | — | — | ✓ |
| Macro dashboard | ✓ | ✓ | ✓ |
| Sector Rotation | ✓ | ✓ | ✓ |
| Market Cycle | ✓ | ✓ | ✓ |
| Macro Regime | ✓ | ✓ | ✓ |
| Crypto On-Chain | ✓ | ✓ | ✓ |
| Credit Analysis | ✓ | ✓ | ✓ |
| Portfolio Tracker | ✓ | ✓ | ✓ |
| Watchlist | 5 · core | 10 · core | Unlimited · full |
| Earnings Calendar | ✓ | ✓ | ✓ |
| Compare Assets | ✓ | ✓ | ✓ |
| Thesis Tracker | ✓ | ✓ | ✓ |
| 200W Screener | Read only | Full | Full |
| Daily Brief | — | 3x/week + timestamp | Daily |
| Smart Alerts — Zone/Earnings | — | ✓ | ✓ |
| Smart Alerts — Convergence | — | — | ✓ |
| Trade Journal | — | ✓ | ✓ |
| **Odin's Eye** | — | 8 runs/mo · 6 signals · buy-zone only · core universe | Unlimited · 12 signals · full output · full universe |
| **AI Research** | — | 10 queries/mo (hard cap) | 50 queries/mo (soft cap, notification at 40) |
| **Insider Tracker** | — | — | ✓ (hard wall) |

## 3. Five Reconciled Decisions (Executive Thread Prevails)

These five items previously had conflicting guidance. Executive thread decisions are authoritative:

| Feature | Old (Feature Matrix Brief) | Current (Executive Thread) |
|---------|---------------------------|----------------------------|
| Odin's Eye | Nord 3x/mo, Viking 10x/mo | Nord none, Viking 8 runs · 6 signals · buy-zone · core |
| AI Research | Nord 3x/mo | Nord none |
| Insider Tracker | Free all tiers, gate V2 | Valkyrie only, hard wall at launch |
| Options Flow | Free all tiers, gate V2 | Hidden V1 → V2 release · Viking+ when released |
| Smart Alerts | Free all tiers | Split: Zone/Earnings Viking+, Convergence Valkyrie only |

## 4. Odin's Eye — Detailed Gating

Critical detail: **Viking gets buy-zone signals ONLY. Overextended signals are Valkyrie-exclusive.** This is a hard gate enforced at API router level — not a UI restriction.

| Parameter | Nord | Viking | Valkyrie |
|-----------|------|--------|----------|
| Monthly runs | None — not accessible | 8 runs/month | Unlimited |
| Signals per run | — | 6 maximum | 12 full output |
| Signal direction | — | Buy-zone only (at or below 200W MA) | Full output — buy-zone AND overextended |
| Asset universe | — | Core only (~538 Tier 1) | Full universe (~800 symbols) |
| Usage indicator | — | "X of 8 runs used. Resets in N days." | Not applicable |
| Upgrade prompt | — | On run 9+: upgrade to Valkyrie CTA | Not applicable |

**Compliance rationale**: Overextended signals sit closer to directional guidance than buy-zone signals. Keeping them behind the Valkyrie wall with more committed, sophisticated subscribers is a cleaner compliance posture.

## 5. Tier Detection Functions (Backend)

These functions are the authoritative tier-check helpers. Do not invent new ones. Do not check `pro_access` to identify Valkyrie — `pro_access` is True for Viking too.

```python
def _is_valkyrie(user) -> bool:
    """Check if user is on Valkyrie tier (internal: 'pro')."""
    return user.tier == 'pro'  # NOT pro_access — that's True for Viking too

def _is_viking_plus(user) -> bool:
    """Check if user is Viking or Valkyrie."""
    return user.tier in ('basic', 'pro')

def _is_nord(user) -> bool:
    """Check if user is on free tier."""
    return user.tier == 'free' or not user.tier
```

## 6. Release Cadence

| Release | Timing | Headline Features |
|---------|--------|-------------------|
| **V1** | Launch | Complete core platform · all foundational features · all 29 Intelligence Expansion Brief capabilities BUILT |
| **V2** | 30-60 days post-launch | Options Flow, Market Heatmaps, Sector Screener, TA Screener, Fundamentals (tiered Core/Full), Earnings auto-fetch |
| **V3** | 60-120 days post-launch | Odin Pulse, Vol Regime · Earnings Reactions + Pattern Library if attorney cleared |
| **V4** | Scale phase | Beta Features (all), iOS/mobile, Polygon migration, Advisory tier activation, White-label API |

**Critical**: V1 through V3 features are all built and live in production code. Release cadence is a staged visibility and access strategy, not a development timeline. V2 and V3 gates are built as config flags so each release is a flip not a code push.

## 7. V2 Release Checklist (Config Flips Only)

All V2 features are built. Release = flip these flags to True in main.py + uncomment sidebar items:

- `v2_options_flow` → True (uncomment sidebar line)
- `v2_market_heatmaps` → True (uncomment sidebar line)
- `v2_sector_screener` → True
- `v2_ta_screener` → True (requires Tiingo or alternative commercial data live)
- `v2_fundamentals_viking` → True (requires Tiingo)
- `v2_fundamentals_valkyrie` → True (requires Tiingo)
- `v2_earnings_autofetch` → True

## 8. Fundamentals — V2 Tiering

Fundamentals split between Viking Core and Valkyrie Full to maintain Viking/Valkyrie value differential.

### Viking — Core Fundamentals (core universe only)

- P/E Ratio (trailing)
- Revenue (annual)
- EPS (trailing)
- Market Cap
- Dividend Yield
- 52-week high/low

### Valkyrie — Full Fundamentals (full universe)

All Viking Core metrics plus:

- P/E Forward
- P/B Ratio
- P/S Ratio
- EV/EBITDA
- Gross / Operating / Net Margin
- Revenue Growth YoY
- Earnings Growth YoY
- Free Cash Flow
- Debt/Equity
- Return on Equity
- Analyst consensus + price targets

**Compliance note**: Analyst consensus and price targets require proximate disclaimer adjacent to the data: "Analytical output only — not a recommendation."

## 9. Asset Universe Enforcement

- **Tier 1 (core)**: ~538 — S&P 500 + Nasdaq 100 + always-include ETFs/crypto · weekly Wikipedia cache
- **Tier 2**: ~270 — S&P 400 mid-caps · loaded on-demand
- **Combined active universe**: ~800 symbols (canonical for external comms)

Enforcement:

- **Nord / Viking**: core universe only (~538)
- **Valkyrie**: full universe (~800)
- **Enforced at API router level**, not UI

## 10. Smart Alerts Split

| Alert Type | Available To |
|------------|--------------|
| Zone alerts (asset enters/exits zone) | Viking+ |
| Earnings alerts | Viking+ |
| **Convergence alerts** (Convergence Score ≥ 55) | **Valkyrie only** |
| Price targets | Viking+ |
| % moves | Viking+ |

Two separate tier gates required. Convergence cannot be exposed via Viking-tier API.

## 11. Sidebar Structure (8 Sections, ~28 Items)

| Section | Pages |
|---------|-------|
| **Portfolio** | Dashboard, Portfolio, Watchlist, Trade Journal, Smart Alerts |
| **Scanners** | Odin's Eye, Odin Pulse |
| **Signals** | 200W Screener, Valuation Zones, Insider Tracker, Options Flow, Convergence Score |
| **Markets** | Sector Rotation, Market Cycle, Macro/FED, Macro Regime, Market Breadth, Credit Analysis, Crypto On-Chain, Systemic Risk |
| **Intelligence** | Macro Intelligence, Historical Intelligence, Factor Regime, Narrative Intelligence, Volatility Intelligence, Sentiment & Positioning |
| **Calendar** | Calendar Hub (unified with filters) |
| **Research** | AI Research, Pre-Earnings Brief, Compare Assets, Thesis Tracker, TA Screener, Sector Screener, Dark Pool, Institutional Footprint, Market Heatmaps |

Removed from sidebar (backend kept): Signal Divergence, Sector Horizons. Deleted entirely: Regime Journal.

## 12. Trial Period

**Hard rule**: `trial_period_days = 7` (NOT 8). Public-facing copy says "7-day free trial, billing begins on day 8." Code must match exactly.

- 7 days full Valkyrie access
- Payment collected upfront at checkout
- Auto-converts to paid on day 7 unless cancelled
- First subscription only — returning customers billed immediately (code-enforced via `stripe_customer_id` check in checkout route)

## 13. Founding Member Mechanics

- Waitlist threshold: 350 confirmed signups
- Target cohort: ~50 paying members
- Distribution: Email-only · NEVER show on public pricing page
- Conversion: Stripe coupon applied to standard Valkyrie Price ID at checkout
- Founding annual: $349/yr — locked for life while subscribed
- Founding monthly: $39.99/mo — intentional alpha/beta reward
- Urgency framing: scarcity-based "[N] spots remaining" — NEVER 72-hour or time-based
- `allow_promotion_codes: True` on desktop checkout to match web
