# Nureli

**A gentle iOS app for emotional self-discovery — built for people who grew up in emotionally unavailable homes.**

[App Store](#) · [Website](https://nureli.app) · [Privacy Policy](#)

---

Nureli is a therapeutic companion for adults navigating Childhood Emotional Neglect (CEN). It offers structured self-reflection, psychologist-approved content, and a private space to process emotions at your own pace — with no pressure, no streaks, and no performance metrics.

---

## App Structure

Nureli is organized around four tabs, each with a distinct role in the emotional growth journey.

### Hearth
*The home base — showing up, not tracking.*

- **The Noticing** — a soft check-in that asks how you feel right now, with no labels required
- **No-Words Welcome** — a non-verbal check-in path for days when language feels inaccessible
- **Weekly Witnessing** — a receipt-backed reflection on the week, count-free
- Bloom growth visualization decoupled from days/streaks

### Mirror
*Structured reflection and inner-work exercises.*

Eleven reflection cards, each targeting a distinct aspect of CEN recovery:

| Card | Focus |
|------|-------|
| Descent | Deep emotional excavation |
| Daily Ritual | Grounding practices |
| Witness Stand | Objective self-observation |
| Complaint Box | Permission to be frustrated |
| Inner Child | Reparenting work |
| Unsent Letter | Closure without contact |
| CEN Moments | Pattern recognition |
| The Pond | Shared reflection space |
| + 3 more | Progressive unlock |

### Grove (Learn)
*A 90-day psychologist-approved curriculum.*

- Day 1–90 structured learning arc
- Deep sessions with scenario-based practice
- No timers, no progress bars, no Day-N-of-90 labels
- Content regions: Roots (1–15), Seedling (16–30), Child's Garden (31–45), Roothold (46–60), Canopy (61–75), Flowering (76–90)

### Journey
*Your story over time — without fabricated dashboards.*

- **Then & Now** — regression-aware comparison of where you started vs. where you are
- **Letter to Who You Were** — milestone-triggered reflective letters
- **Seasonal Ceremony** — transitions marked with intention, not metrics
- **Your Story So Far** — narrative summary of growth
- Self-Trust score persists and evolves
- Emotion constellation fed from real check-in data

---

## Technical Stack

| Layer | Technology |
|-------|-----------|
| Platform | iOS 18+ (iPhone only) |
| Language | Swift 6, SwiftUI |
| Navigation | SwiftUI Tab (iOS 18 Tab API) |
| Backend | Supabase (Postgres + Auth + Edge Functions) |
| AI | OpenAI via Supabase Edge Functions (on-device-first) |
| Payments | RevenueCat |
| Analytics | PostHog |
| Auth | Sign in with Apple, Google Sign-In |

---

## Design System

- **Typography:** SF Pro Rounded (system) + Instrument Serif (display)
- **Palette:** Single warm cream base (`#FFF9F1`), lit per-tab with botanical light metaphors — sunrise, water, daylight, evening
- **Motion:** Arbitrated 6-part system; no animation fires without passing a reduced-motion gate
- **Accessibility:** WCAG AA contrast throughout; ink token ramp anchored at `#2A2429` (14.4:1)
- **No AI imagery:** All botanical art is coded SVG — not generated raster

---

## Privacy

- Reflection data is private and encrypted
- No selling of personal data
- No third-party ad tracking
- On-device processing preferred; cloud AI only with explicit consent
- Full data export and account deletion available from Settings

---

## Content Philosophy

Nureli's content is built on the clinical framework around Childhood Emotional Neglect as described by Dr. Jonice Webb. All curriculum content is reviewed by licensed psychologists.

The app does **not**:
- Position itself as therapy or a clinical tool
- Track streaks or surface performance metrics
- Use urgency, shame, or pressure copy
- Make claims about curing or treating any condition

---

## Status

Nureli is actively developed and available on the App Store.

Built with care in India 🌱
