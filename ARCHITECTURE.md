# Architecture Overview

## High-Level Structure

```
Nureli iOS App
├── Onboarding          — First-run flow, CEN education, account creation
├── Tab: Hearth         — Daily presence and check-ins
├── Tab: Mirror         — Structured reflection exercises (11 cards)
├── Tab: Grove          — 90-day psychologist curriculum
├── Tab: Journey        — Long-arc growth and story
└── Settings            — Account, privacy, subscription, data
```

## Data Architecture

### Local-first, cloud-synced

Nureli uses a local-baseline + remote-override strategy:

- **On-device**: User reflections, check-in history, progress markers
- **Supabase Postgres**: Cloud sync across devices, content overrides, profile
- **Content delivery**: Baseline content ships with the app; editorial updates arrive via `content_library` table without an App Store release

### AI / Intelligence Layer

```
User input
    └── On-device classification (privacy-safe)
        ├── Local response (most cases)
        └── Edge function (OpenAI, consent-gated)
            └── Personalized insight returned
```

The living profile accumulates across sessions; cross-device progress syncs via Supabase with Row Level Security on all tables.

## Content Tiers

| Tier | Location | Coverage |
|------|----------|----------|
| Tier 1 | Bundled in app | Deep sessions + 75 scenarios per region (Days 1–45 complete) |
| Tier 2 | Bundled fallback | Thin content for Days 46–90 (expanding) |
| Remote override | Supabase `content_library` | Editorial updates, A/B variants |

## Subscription Model

Managed via RevenueCat.

- **Free tier**: Limited Mirror cards, Grove Days 1–7, basic check-ins
- **Premium** (`premium` entitlement): Full Mirror library, full Grove curriculum, Journey features, AI companion
- Pricing: Annual ($64.90/yr) with 3-day free trial; Monthly ($17.90/mo)
- Customer Center: subscription management, cancellation, restore purchases

## Auth

- Sign in with Apple (primary)
- Google Sign-In (secondary)
- Supabase Auth backend
- Session persistence across launches
- Sign-in accessible from both onboarding and Settings (added post-launch)

## Edge Functions (Supabase)

| Function | Purpose |
|----------|---------|
| `ai-mirror` v5 | Reflection companion, context-aware responses |
| `delete-account` | GDPR-compliant account + data deletion |

## Navigation

Uses iOS 18 native `Tab` API. Portrait-only, iPhone-only.

Transitions use `.zoom` and `.matchedTransitionSource` (iOS 18 APIs, no availability guard needed).

## Accessibility

- Ink token ramp ensures WCAG AA contrast at all type sizes
- Reduced-motion gate on all animations
- VoiceOver supported (voice journaling intentionally excluded — deliberate product decision)
