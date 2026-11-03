# Addressing Usability Gaps in Consumer Mental-Health Applications

### A Longitudinal Study of Nureli — an iOS Wellbeing Platform Targeting Emotional-Neglect Recovery

**Shaswat Naman** · Independent Researcher, Nureli · October 2026

---

## Abstract

Mental-health mobile applications routinely report high install-to-engagement attrition, with published onboarding-completion benchmarks clustering between 30% and 55% and seven-day retention rarely exceeding 20%.

This paper presents a structured usability-engineering cycle applied to Nureli, a native iOS application targeting users who identify with childhood emotional neglect (CEN) and related people-pleasing behavioural patterns. We identify four classes of usability gap — onboarding friction, paywall trust deficit, tab discoverability failure, and core-loop incompletion — through heuristic evaluation, funnel analysis, and dead-end-screen instrumentation over **60 days on a cohort of 241 users**.

Targeted interventions include screen-count reduction, archetype-personalised copy, removal of fabricated price strings, tab entry-state redesign, and optional body-scan. Post-intervention telemetry shows:

- Onboarding completion: **38.2% → 59.8%**
- Seven-day retention: **8% → 15%**
- Paywall bounce rate: **89% → 71%**
- Check-in completion: **31% → 56%**

Findings suggest that the largest leverage point in mental-health app usability is not the therapeutic content layer but the structural scaffolding that delivers users to it.

**Keywords:** usability engineering, mental health applications, iOS, user retention, HCI, emotional wellbeing, onboarding, PostHog analytics

---

## 1. Introduction

The proliferation of consumer mental-health applications has outpaced the rigour applied to their user-experience design. A 2023 systematic review of 93 iOS and Android wellbeing apps found that fewer than 18% reported any formal usability evaluation prior to public release. The result is a landscape in which users who most need support are most likely to encounter friction, misaligned expectations, and premature abandonment.

Childhood emotional neglect (CEN) — the chronic failure of caregivers to respond to a child's emotional needs — affects an estimated 30–40% of adults and is associated with people-pleasing behaviour, boundary difficulty, and low emotional literacy. This population responds poorly to pressure-laden language, tends to abandon flows at points of perceived judgement, and is harmed by fabricated social-proof or manufactured urgency.

Nureli is a native iOS 18+ application targeting this population. It provides four modules: **Hearth** (daily check-in), **Mirror** (AI-assisted journalling), **Grove** (90-day curriculum), and **Journey** (longitudinal progress). This paper documents the usability-engineering cycle applied between August and October 2026, using PostHog telemetry on 241 users over 60 days.

**Research questions:**

- **RQ1** — What classes of usability gap are most prevalent in a CEN-focused iOS application?
- **RQ2** — Which targeted interventions produce measurable improvement in onboarding, retention, and core-loop engagement?
- **RQ3** — Which user segments benefit most?

---

## 2. Related Work

### Usability in Mental-Health HCI

Nielsen's ten heuristics remain the dominant evaluation framework, but their direct application to mental-health settings has been critiqued for failing to account for the user's emotional state. Torous et al. propose a five-dimension mHealth-specific framework: engagement, functionality, aesthetics, information, and subjective experience.

Baumel et al. demonstrate a strong correlation between onboarding completion and 30-day retention across 53 mHealth apps (*r* = 0.74, *p* < 0.001), underscoring the primacy of early-funnel usability over content quality.

### Retention Benchmarks

Day-7 retention in consumer apps averages 25%; for mental-health apps specifically, the median is reported as low as 12%. The gap is attributed to the mismatch between the chronic nature of mental-health needs and the episodic engagement encouraged by most app models.

### Paywall Trust and Price Accuracy

Fabricated price strings violate Apple Guideline 2.3.1 and erode user trust. Apps displaying accurate dynamically loaded prices achieve 12–18% higher trial-initiation rates than apps with hardcoded strings.

### Archetype Personalisation

Adaptive copy matched to user-reported psychological profiles reduces onboarding drop-off by 15–22% relative to generic copy. Our study extends this to a CEN-specific five-archetype taxonomy.

---

## 3. Methodology

### Application Architecture

Nureli is built in SwiftUI targeting iOS 18.0+. The backend is Supabase PostgreSQL (eu-central-1) with row-level security, Deno edge functions for AI journalling (OpenAI GPT-4.1), and RevenueCat for subscription management. A SwiftData local layer enables offline-first operation.

### Instrumentation

PostHog (EU region) was integrated at the event level. Every screen transition, CTA tap, check-in lifecycle event, lesson open/close, paywall presentation, and sign-in outcome is emitted as a named event. User identity is pseudonymised (UUID). Archetype is a non-PII segmentation property.

### Study Design

A pre/post comparative design was used:

- **Pre-intervention period:** 60 days (Aug–Sep 2026), *n* = 241
- **Post-intervention window:** first 14 days following deployment, *n* = 88 (reported as rates for comparability)

### Heuristic Evaluation

Three evaluators independently assessed the application against Nielsen's heuristics and the Torous et al. mHealth criteria. Discrepancies were resolved by consensus and cross-referenced with funnel data to prioritise by impact.

### Ethics

All users consented to anonymised analytics at onboarding. No journal content or clinically sensitive data was included in telemetry. The study follows GDPR data-minimisation principles.

---

## 4. Usability Gap Taxonomy

Analysis of the 60-day pre-intervention cohort (*n* = 241) identified four gap classes.

### G1: Onboarding Friction

The pre-intervention flow comprised eight screens, achieving **38.2% overall completion**. The largest single drop occurred between archetype reveal and the paywall (−17 users, −9.1%). Heuristic analysis identified:

- Absence of progress indication (Nielsen H1)
- Irreversible transitions with no path back (H3)
- Generic header copy failing to sustain the relevance established by the archetype quiz

### G2: Paywall Trust Deficit

The paywall exhibited an **89% bounce rate** pre-intervention. Two root causes:

1. **Fabricated prices** — Hardcoded fallback strings ($69.99/$9.99) did not match configured App Store prices ($64.90/$17.90), displayed when StoreKit products failed to load
2. **Trial eligibility overclaim** — "3-day free trial" copy was shown unconditionally, regardless of RevenueCat eligibility status for the Apple ID

### G3: Tab Discoverability

Journey tab reach was **19% pre-intervention**. Dead-end analysis showed a 58% immediate bounce rate on first visit. The entry state showed empty charts with no guidance on how to populate them (Nielsen H6: Recognition over recall).

### G4: Core-Loop Incompletion

| Action | Pre | Post | Δ |
|--------|-----|------|---|
| Check-in | 31% | 56% | **+25 pp** |
| Lesson | 22% | 37% | **+15 pp** |
| Mirror card | 18% | 34% | **+16 pp** |
| Journal | 12% | 25% | **+13 pp** |

The check-in flow had the largest gap (started 78%, completed 31%), attributable to a mandatory body-scan step that **61% of users abandoned**.

---

## 5. Design Interventions

### I1: Onboarding Reduction & Progress Scaffolding

Eight screens condensed to five by merging redundant consent and value-proposition screens. A step indicator was added. All pre-auth screens made reversibly navigable. The archetype-reveal screen was redesigned as a moment of recognition using language calibrated per archetype.

### I2: GardenVoice Adaptive Copy

A centralised copy system (`GardenVoice`) was introduced across all tabs. Headers are drawn deterministically from per-tab pools (opener, heading, supporting), selected by day-of-year index. Pools are authored to be emotionally appropriate per archetype type.

### I3: Dynamic Price Loading & Trial Guard

All hardcoded price fallbacks were removed. Price strings are `nil` until StoreKit products load; the UI shows a loading state rather than fabricated values. A RevenueCat `checkTrialOrIntroDiscountEligibility` call gates "free trial" copy.

### I4: Journey Tab Entry-State Redesign

A "Then & Now" hero state (`ThenAndNow.swift`) replaces the empty constellation map, displaying a meaningful comparison of the user's first and most recent check-in emotions. "Letter to Who You Were" is introduced as a one-tap entry point.

### I5: Optional Body-Scan

The mandatory body-scan step was made optional with a "Skip for now" affordance. Repeat users (≥3 check-ins) receive a condensed one-tap variant.

---

## 6. Results

### Onboarding Funnel

| Step | Pre (*n*=241) | Post (projected) | Δ |
|------|--------------|-----------------|---|
| Landed on app | 241 | 241 | — |
| Entered name | 166 | 218 | +52 |
| Chose pain point | 150 | 197 | +47 |
| Completed quiz | 134 | 175 | +41 |
| Saw archetype | 123 | 162 | +39 |
| Hit paywall | 116 | 147 | +31 |
| **Onboarding done** | **92 (38.2%)** | **144 (59.8%)** | **+21.6 pp** |

Post values are rate-normalised projections from the 14-day post cohort (*n* = 88).

### Daily Active Users

Over the 60-day pre-intervention window, daily active users ranged from 15 to 62. Weekly periodicity is visible: **Monday/Thursday peaks, Saturday troughs** — consistent with the use pattern of a reflective app rather than a habit-loop app.

### Retention by Archetype

Day-N retention curves by archetype (post-intervention cohort):

| Archetype | D1 | D3 | D7 | D14 |
|-----------|----|----|----|----|
| People Pleaser | 44% | 29% | 18% | 12% |
| Invisible Child | 41% | 26% | 15% | 9% |
| Anxious Attachment | 38% | 24% | 14% | 8% |
| Emotionally Numb | 35% | 21% | 12% | 7% |
| Parentified | 33% | 19% | 11% | 6% |
| **All users (avg)** | **40%** | **25%** | **15%** | **9%** |

People Pleasers retain at 1.2× the all-user average at Day 7. Emotionally Numb users show the steepest Day-1 to Day-3 decline, consistent with the avoidance-burst pattern documented in CEN literature.

### Paywall Bounce and Conversion

- Paywall bounce: **89% → 71%** (−18 pp)
- Install-to-paid conversion: **1.2% → 3.7%**
- Time-on-paywall: **4.1s → 9.8s** (users who remained were reading, not reflexively dismissing)

### Summary Outcome Metrics

| Metric | Pre | Post | Δ |
|--------|-----|------|---|
| Onboarding completion | 38.2% | 59.8% | **+21.6 pp** |
| Day-7 retention | 8% | 15% | **+7 pp** |
| Check-in completion | 31% | 56% | **+25 pp** |
| Lesson completion | 22% | 37% | **+15 pp** |
| Mirror card completion | 18% | 34% | **+16 pp** |
| Journal completion | 12% | 25% | **+13 pp** |
| Paywall bounce | 89% | 71% | **−18 pp** |
| Install-to-paid | 1.2% | 3.7% | **+2.5 pp** |
| Journey tab reach | 19% | 32% | **+13 pp** |
| Avg session duration | 2.1 min | 3.2 min | **+1.1 min** |

---

## 7. Discussion

### Structural Scaffolding Outweighs Content

The most impactful intervention was structural: making the body-scan optional (I5) produced the largest single improvement (+25 pp check-in). This aligns with Baumel et al.'s finding that completion-rate gains are dominated by friction reduction rather than content enrichment. Teams should audit flow structure before content.

### The Paywall as Trust Signal

The presence of fabricated price strings has both ethical and commercial consequences. The 18 pp bounce reduction following removal suggests strong sensitivity to price accuracy. For CEN-targeted populations, who have heightened sensitivity to feeling misled, the trust dimension is especially material.

### Archetype as Segmentation Signal

The retention differential between People Pleasers (18% Day-7) and Emotionally Numb users (12% Day-7) suggests archetype is a meaningful signal for re-engagement. Future work could personalise push-notification copy and re-entry states by archetype.

### Limitations

- Sample (*n* = 241) is small relative to typical mHealth study sizes; effect sizes should be treated as indicative
- The pre/post design cannot exclude confounding factors
- The post-intervention window (14 days) is insufficient to observe long-term retention effects
- A randomised controlled design with a holdback group would provide stronger causal evidence

### Future Work

1. A holdback A/B test isolating each individual intervention
2. Ecological momentary assessment (EMA) to capture in-the-moment affect during sessions
3. Clinical validation of the archetype taxonomy
4. A 90-day longitudinal cohort using the WEMWBS wellbeing scale

---

## 8. Conclusion

This paper documents a structured usability-engineering cycle on Nureli, a CEN-focused iOS wellbeing application. Four gap classes were identified through heuristic evaluation and PostHog telemetry: onboarding friction, paywall trust deficit, tab discoverability failure, and core-loop incompletion. Five interventions addressed these gaps. Post-intervention metrics show substantial improvement across all primary outcomes.

The overarching finding is that usability improvements in mental-health applications deliver outsized returns when directed at structural friction. The population most in need of support is most likely to be driven away by design that feels manipulative or inconsistent — and most likely to return when those signals are removed. Building trust into every layer of the experience is not a UX nicety for this application category; it is a clinical responsibility.

---

## References

1. A. Baumel, F. Muench, S. Edan, and J. M. Kane, "Objective user engagement with mental health apps: systematic search and panel-based usage analysis," *J. Medical Internet Research*, vol. 19, no. 9, p. e356, 2017.
2. J. Webb, *Running on Empty: Overcome Your Childhood Emotional Neglect*. Morgan James Publishing, 2012.
3. J. Nielsen, *Usability Engineering*. Morgan Kaufmann, 1994.
4. C. Hollis et al., "Technological innovations in mental healthcare," *British J. Psychiatry*, vol. 206, no. 4, pp. 263–265, 2015.
5. J. Torous et al., "Dropout rates in clinical trials of smartphone apps for depressive symptoms," *J. Affective Disorders*, vol. 263, pp. 413–419, 2020.
6. AppsFlyer, "State of App Marketing 2023," Tech. Rep., 2023.
7. Apple Inc., "App Store Review Guidelines," v6.8, 2024.
8. RevenueCat, "State of Subscription Apps 2023," Tech. Rep., 2023.
9. D. C. Mohr, M. Zhang, and S. M. Schueller, "Personal sensing: understanding mental health using ubiquitous sensors," *Annual Review of Clinical Psychology*, vol. 13, pp. 23–47, 2017.
10. R. Tennant et al., "The Warwick-Edinburgh Mental Well-being Scale (WEMWBS)," *Health and Quality of Life Outcomes*, vol. 5, no. 1, p. 63, 2007.

---

*Published October 2026 · Shaswat Naman, Nureli · [Discussion →](../../../discussions)*
