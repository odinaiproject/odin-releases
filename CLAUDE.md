# Odin AI — Web Platform (odinai-website)

This is the Claude Code project memory file for the Odin AI web platform repo (Next.js).

## Project Overview

The web platform is the marketing site, billing portal, and full feature-equivalent companion to the desktop app. Pre-launch focus: marketing pages, waitlist, Stripe checkout, account management.

- **Entity**: Odin Technology Group, LLC (Florida)
- **Founder**: Matthew Manyak (sole founder)
- **Repo**: `github.com/odinaiproject/odinai-website`
- **Branch**: main (auto-deploys to Vercel)
- **Production URL**: `https://odinai-website.vercel.app` (final: `odinai.app` pending)

## Critical Context — Read These Before Anything Else

- @docs/master-baseline.md — full project state as of May 25, 2026
- @docs/compliance.md — banned terms, canonical terms, mandatory disclaimers, approved framings, attorney-hold items
- @docs/tier-gating.md — feature matrix V1-V4, what features are hidden vs live at v1

If you find yourself generating any user-facing copy or UI, **re-read `compliance.md` before generating**.

## Stack

- **Framework**: Next.js App Router with TypeScript
- **Runtime**: Node.js 24.x
- **Region**: iad1 (primary), cle1 (edge)
- **Hosting**: Vercel
- **Database**: Supabase (shared with desktop app)
- **Payments**: Stripe (live mode active)
- **Email**: Resend
- **AI**: Anthropic Claude Sonnet — **separate web API key from desktop** (provisioned May 8)
- **Status monitoring**: UptimeRobot (3 monitors live)

## Code Conventions

### Typography
- **Inter** is the universal web typeface
- Weight-driven hierarchy (900 hero, 700 labels, 400 body)
- No secondary typeface in web surfaces

### Compliance in Code
- Every public page carries the mandatory disclaimer (see `compliance.md`)
- Footer disclaimer with `odinai.app` reference
- All AI-generated outputs framed as descriptive, never predictive
- Never use banned terminology (see `compliance.md` §2)
- "Professional-grade" used throughout — "Institutional-grade" is attorney-hold
- `og:url` and meta tags reference `odinai.app` (not `odinai.com`)

### Tier Gating Discipline
- Same discipline as desktop: enforce at API route level, not UI
- Use the same tier-check pattern: check `tier` string, NOT `pro_access` boolean
- V2/V3 features are hidden with explicit release markers in code

### V2/V3 Hidden Features (Current State)

These are hidden behind release markers — comment them in when the release flips:

```typescript
// V2 RELEASE - uncomment when v2_options_flow flag flips
// { id: 'options-flow', label: 'Options Flow', href: '/options-flow' },

// V2 RELEASE - uncomment when v2_sector_screener flag flips
// { id: 'sector-screener', label: 'Sector Screener', href: '/sector-screener' },

// V3 RELEASE - uncomment when v3_odin_pulse flag flips
// { id: 'odin-pulse', label: 'Odin Pulse', href: '/odin-pulse' },
```

### Authentication
- PBKDF2-HMAC-SHA256 hash matching desktop (200k iterations, UTF-8 salt)
- JWT session lookup via `userId` (NOT `cac23483...` IDs — those were a bug pre-`SUPABASE_URL` fix)
- Email verification: **soft warning, not hard block**
- 30-day session persistence
- `/api/auth` routes exempt from geo-lock
- First name + Last name fields (not single "Full name")

### Geo-Lock
- US-only via `x-vercel-ip-country` header
- Middleware exempts: `/api/auth`, `/api/health`, admin routes
- `/not-available` page handles geo-blocked users (VPN bypass line REMOVED per compliance)
- Test 3 (real non-US IP) pending live `odinai.app` domain — `.vercel.app` doesn't inject country header reliably

### Stripe Integration
- Live mode active
- 4 live Price IDs in env vars (Valkyrie + Viking, monthly + annual) — see `master-baseline.md` §4
- `client_reference_id: session.userId` REQUIRED on checkout session
- Founding member: Stripe coupon mechanism on standard Valkyrie Price ID — NOT separate Price IDs
- `allow_promotion_codes: True` to allow coupon entry
- `trial_period_days = 7` (NOT 8 — public copy says "7-day free trial")
- Stripe customer ID stored in `users` table, NOT `tiers` table
- Billing portal reads `stripe_customer_id` from `users` table

### Webhook Handling
- Webhook host: Render (`https://odin-app.onrender.com/stripe-webhook`)
- Webhook secret rotation requires simultaneous Vercel + Render env update
- `customer.subscription.updated` maps by **price ID, not metadata**
- Tier upsert uses `on_conflict` as **query param, not Prefer header**

## Key Commands

```bash
# Dev server
npm run dev

# Build
npm run build

# Run on Vercel preview
vercel

# Push to production
git push origin main  # auto-deploys to Vercel
```

## Pages Status

### Public (no auth required)
- `/` (landing) — LIVE, ADA passing
- `/features` — LIVE, ADA passing
- `/pricing` — LIVE, founding member section REMOVED, three-tier Norse
- `/changelog` — LIVE, `alpha` → `early access` swept
- `/download` — LIVE, ADA passing, blocked items pending App Dev xattr instructions
- `/not-available` — geo-block page

### Auth-Required
- `/login` — LIVE
- `/signup` — LIVE (first + last name split)
- `/dashboard` — LIVE, tier label dynamic from Supabase
- `/billing` — billing portal redirect handler

### Blocked / Pending
- `/terms` — BLOCKED on domain + attorney review
- `/privacy` — BLOCKED on domain + attorney review
- `/refer` — BLOCKED on attorney FTC clearance (Flag 7)
- `/support` — LIVE (UptimeRobot, KB link, bug form, email link)

## ADA Accessibility Status

All 5 public HTML pages pass WCAG 2.1 AA:
- Skip-to-content links on all pages
- `<main>` landmarks
- `aria-hidden` on decorative SVGs
- Heading hierarchy (h1 → h2 → h3, no skipping)
- Empty link labels fixed

Next.js app pages: ADA pass still pending.

## Current Sprint Priorities

1. **Wait for Matthew**: Vercel Pro upgrade ($20/mo) + domain canonical confirmation
2. After domain live (in this exact order):
   - Update `NEXT_PUBLIC_APP_URL` to `https://odinai.app`
   - Trigger Resend domain verification (~1hr DNS propagation)
   - Confirm `support@odinai.app` activation
   - Deploy ToS + Privacy Policy (post-attorney review)
   - Run Geo-lock Test 3 on live domain
   - Update Stripe redirect URLs (auto via env)
3. Publish 14 compliance-cleared KB articles to Notion once support@ active
4. Deploy 9-email onboarding sequence in Resend once compliance reviews

## Known Issues

- App layout meta tags: "Institutional-grade" → "Professional-grade" + `odinai.com` → `odinai.app` (still present in some `layout.tsx` files — flagged)
- Hardcoded `total_assets = 538` in zone-counts route — should reflect ~800 combined universe
- Some founding member references in old code — superseded by coupon architecture
- Web Anthropic API key separate from desktop key (provisioned May 8) — never share

## Behavioral Rules for Claude Code

- **Compliance first**: Every public-surface copy change requires checking `compliance.md`
- **Never paraphrase locked exact strings** (mandatory disclaimer, zone agreement flag)
- **Tier-gated routes enforced at API level** — never UI-only restrictions
- **V2/V3 features stay hidden** until explicit release flag flip
- **Footer disclaimer present** on every public page
- **Mailing address in CAN-SPAM email footers** (will use mail forwarding address — currently pending)
- **No founding member pricing on public pages** — email-only distribution

## What This File Does Not Cover

- Desktop app conventions → see `odin-app` repo `CLAUDE.md`
- Algorithm implementation → see `docs/algorithm.md` (also relevant for web API endpoints that surface OdinScore)
- Financial projections, attorney details, personal Matthew context → in global `~/.claude/CLAUDE.md`
