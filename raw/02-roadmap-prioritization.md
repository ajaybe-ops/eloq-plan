# 02 — Feature Prioritization and Roadmap

**Version:** 2.0 · 2026-11-15

**What changed in this revision:** Career tier price reference updated to $24.99; pronunciation feasibility gate restated against the 600-utterance protocol in `14` (r ≥ 0.85 with a fallback ladder, not a binary); human-reviewed mocks repositioned from a Phase 3 marketplace to a $49 add-on at Career launch. RICE scores and phase boundaries are unchanged.

## 1. Prioritization framework

We use **RICE** as the default, with one documented override: *strategic wedge features*. RICE measures value to current users and systematically undervalues features that create a new market or a defensible position — for Eloq, the interview simulator is exactly that. Any override is written down with its reason, so the process stays honest.

```
RICE = (Reach × Impact × Confidence) / Effort
Reach      = % of the 12-month target user base the feature touches per quarter
Impact     = 3 massive · 2 high · 1 medium · 0.5 low · 0.25 minimal
Confidence = 100% (data) · 80% (strong signal) · 50% (hypothesis)
Effort     = person-weeks, including design, QA, and instrumentation
```

## 2. RICE scoring (v1 candidates)

| # | Feature | Reach | Impact | Conf. | Effort | RICE | Decision |
|---|---|---|---|---|---|---|---|
| 1 | Daily Plan + streaks + review queue | 95 | 2 | 85% | 6 | **26.9** | MVP |
| 2 | Correction engine (grammar/lexis/register) | 100 | 3 | 80% | 10 | **24.0** | MVP |
| 3 | Vocabulary capture + FSRS | 80 | 2 | 90% | 8 | **18.0** | MVP |
| 4 | Voice tutor + 12 scenarios | 100 | 3 | 90% | 16 | **16.9** | MVP |
| 5 | Progress analytics v1 + weekly report | 90 | 2 | 70% | 9 | **14.0** | MVP |
| 6 | Pronunciation feedback v1 (word-level) | 90 | 3 | 60% | 14 | **11.6** | MVP (score labeled beta) |
| 7 | Interview simulator | 35 | 3 | 65% | 18 | **3.8** | Phase 2 + **strategic override** |
| 8 | Offline mode (lessons, SRS, drills) | 30 | 1 | 80% | 10 | **2.4** | Phase 2 |
| 9 | B2B career-center dashboard | 10 | 3 | 70% | 14 | **1.5** | Phase 3 |
| 10 | Video delivery analysis | 15 | 2 | 50% | 12 | **1.3** | Phase 3 |
| 11 | Community practice pods | 25 | 2 | 45% | 30 | **0.8** | Phase 3 |
| 12 | Human coach marketplace | 12 | 2 | 55% | 26 | **0.5** | Phase 4 |

**Why the interview simulator overrides its score:** RICE reach is computed against the full learner base, but interview prep is the *entry point* for the highest-LTV segment and the only feature with a defensible, outcome-based marketing claim. It also anchors the $24.99 Career tier, which is what makes the unit economics work. Decision owner: Head of Product; review at M9.

**Why pronunciation v1 is in the MVP despite moderate RICE:** it is the single clearest proof that we are not "another chat wrapper." Without it, the product is a subset of ChatGPT voice. It ships as a beta score with explicit uncertainty labeling, which is acceptable; shipping it *silently wrong* is not.

## 3. Phase 0 — Foundations (weeks 0–6, pre-MVP)

| Workstream | Deliverable | Exit criterion |
|---|---|---|
| Audio pipeline spike | End-to-end loop: capture → streaming ASR → LLM → streaming TTS | p50 round-trip ≤ 1.5 s on a mid-range Android over 4G |
| Pronunciation feasibility | Licensed scoring API + L1 calibration vs. 100 human-rated utterances | r ≥ 0.80 to proceed to the full 600-utterance study; below 0.75, ship bands only (`14` §6) |
| Correction quality | Hybrid checker (deterministic + LLM) on 500 gold sentences | Precision ≥ 90%, recall ≥ 60% |
| Safety baseline | Age gate, consent, PII redaction, report flow | Legal sign-off |
| Content | 12 scenarios authored and playtested | 5 learners complete each with ≤ 1 dead-end |

**Gate:** if the pronunciation spike returns r < 0.75, the MVP ships *drill-only* pronunciation (no composite score), and the score moves to Phase 2. This decision is made at week 6, not at launch.

## 4. Phase 1 — MVP (months 1–6): "Proof of feedback"

**Goal:** a learner can have a real conversation tonight, get corrected, and see a number move within 7 days.

| Included | Notes |
|---|---|
| Voice + text tutor; 12 scenarios at build, 24 by public launch | 5 CEFR bands × roleplay variants |
| Correction engine, Flow/Coach modes | Report card at session end |
| Pronunciation v1 | Word-level heatmap, accuracy/fluency/completeness, drills for top 3 weak words |
| Vocabulary capture + FSRS, Core 2k pack | Long-press capture, own-audio cards |
| Daily Plan, streak + weekly goal, review queue | 8–12 min/day |
| Progress v1 | Estimated CEFR, 4 skill bars, weekly report card |
| Accounts, subscriptions, paywall | Free/Plus; Career tier visible but "coming soon" |
| Safety & privacy v1 | Moderation, 30-day audio retention, delete-all, export |
| Onboarding + 3-min placement | Placement drives initial CEFR band |

**MVP success criteria (measured at week 12 of general availability)**
- Activation (first session with ≥ 1 correction + 5 reviews in 24 h): ≥ 45%
- D7 ≥ 28%, D30 ≥ 15%
- Weekly speaking minutes/WAU ≥ 18
- Correction precision ≥ 92%; false-positive rate < 5%
- Paid conversion ≥ 2.5% of MAU (early signal; full target in `06-metrics.md`)

**What we deliberately excluded and why:** community (safety infra not ready), interview sim (needs the conversation engine to be stable first), offline (cost without evidence of need), video (privacy burden), multiple languages (dilutes English quality).

## 5. Phase 2 — Expansion (months 6–12): "The career wedge"

**Goal:** become the default interview-prep tool for English-speaking job seekers, and turn a good product into a paid one.

| Feature | Rationale | Key risk |
|---|---|---|
| **Interview simulator v1** | Owns the wedge; justifies $24.99; generates the outcome data we market on | Question realism; must beat "ChatGPT interview prompt" |
| **JD tailoring** | Paste a job description → role-specific questions and vocabulary | Hallucinated company facts — constrain to the JD text |
| **Pronunciation v2** | Phoneme detail, intonation overlay, prosody drills, L1-aware thresholds | Requires the validation study to hold per-L1 |
| **Study plans** | Goal + deadline → 2/4/8-week plan with weekly checkpoints | Plan quality vs. over-scheduling |
| **Offline drills + SRS** | Commute and low-connectivity markets | Sync conflicts |
| **Packs** | Interview, Business, Tech, Healthcare, Campus | Content production cost |
| **Analytics v2** | Interview Readiness Index, error trends, "can-do" milestones | Over-claiming precision |
| **Referral** | "Give a week, get a week" | Fraud |

**Exit criteria for Phase 2:** interview-sim cohort shows ≥ 8-point Interview Readiness gain over 3 weeks; Career tier ≥ 25% of new subscriptions; D30 ≥ 22%.

## 6. Phase 3 — Community and institutions (months 12–18)

| Feature | Rationale | Guardrail |
|---|---|---|
| Practice Pods (AI-facilitated, 4–6 learners) | Captures HelloTalk's belonging appeal without stranger DMs | Age-banded; moderated; recording consent |
| Moderated voice rooms | Social retention for students | 24/7 moderation + 1-tap report with audio buffer |
| B2B career-center console | University pilot revenue; cohort reporting | FERPA/GDPR compliance; no individual audio to institutions |
| Human-reviewed mock interview (marketplace) | High-value upsell; validates AI scoring against humans | Vetted reviewers; rubric-calibrated |
| Video delivery analysis | Interview realism | On-device only; explicit consent per session |

**Community is gated on a safety review**, not a date. Prerequisites: moderation vendor SLA, human escalation rota, minor-safety audit, incident response runbook with a 1-hour acknowledgement target.

## 7. Phase 4 — Scale (months 18–30)

- Additional L1s (Indonesian, Japanese, Korean, Turkish, French) — UI, hints, glosses only; tutor stays English.
- Enterprise L&D tier with SSO, SCIM, admin analytics.
- Public API / LMS integrations (Canvas, Moodle).
- On-device small model for offline free conversation (cost + privacy win).
- Credential partnerships: preparation tracks mapped to IELTS/TOEFL/TOEIC band ranges (never issuing certificates ourselves).

## 8. What we cut if capacity drops 30%

In order, cut from the bottom:

1. Video delivery analysis (Phase 3 → keep deferred)
2. Offline free conversation (keep drills + SRS only)
3. Healthcare pack (highest content cost, smallest early segment)
4. Practice Pods (defer to Phase 4; community is not required for the wedge)
5. Free-talk mode (scenarios only — sharper pedagogy, cheaper inference)

**Never cut:** correction quality, pronunciation validation, safety, onboarding, or the weekly report. These are the product.

## 9. Dependency map

```
Audio pipeline ──► Voice tutor ──► Scenarios ──► Interview sim
       │                │              │
       └──► ASR ──► Pronunciation ─────┘
                          │
Correction engine ◄───────┘
       │
       └──► Error bank ──► Review queue ──► Daily Plan ──► Streaks
                                  │
Vocabulary capture ──► FSRS ──────┘
                                  │
                          Progress analytics ──► Report card ──► Referral
Safety & privacy ──► (blocks) Community pods
Payments ──► (blocks) Premium launch
```

## 10. Timeline and team

| Phase | Window | Team (FTE) |
|---|---|---|
| 0 | W0–6 | 1 PM, 1 designer, 2 backend, 1 mobile, 1 ML, 0.5 content lead |
| 1 (MVP) | M1–6 | +1 mobile, +1 ML (speech), +1 content, 0.5 QA, 0.5 T&S |
| 2 | M6–12 | +1 growth, +1 content (interview), +1 data/analytics, 1 QA |
| 3 | M12–18 | +2 T&S moderators, +1 B2B eng, +1 partnerships |

**Critical path:** audio latency → correction quality → pronunciation validity → interview sim. Everything else can slip; these four cannot.

## 11. Milestones with go/no-go criteria

| Milestone | Date | Go criteria | No-go action |
|---|---|---|---|
| M0 Prototype | W6 | Latency p50 ≤ 1.5 s; pronunciation r ≥ 0.75 | Drill-only pronunciation; re-plan MVP |
| M1 Closed beta (300 users) | M4 | ≥ 40% return in week 2; correction precision ≥ 90% | Fix quality before scaling spend |
| M2 Public MVP | M6 | Activation ≥ 40%; D7 ≥ 25% | Hold paid marketing; iterate onboarding |
| M3 Career launch | M10 | Interview sim NPS ≥ 40; ≥ 30% of testers say "better than ChatGPT" | Reposition or rebuild sim |
| M4 Community pilot | M15 | Safety audit passed; 0 critical incidents in 8-week pilot | Indefinite deferral |
