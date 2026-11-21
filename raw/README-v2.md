# Eloq — AI English Fluency Coach

**Version:** 2.0 · 2026-11-16

**Status:** publish-ready plan, pre-build. Every number is either verified, derived, or tagged as a hypothesis with a test.
**Scope:** English learners 16+, students and job seekers. English only; L1 support for Mandarin, Spanish, Portuguese, Hindi, Vietnamese, Arabic.

---

## The pitch

HelloTalk sold the dream of "talk to real people and learn a language." What it actually delivers is a scheduling lottery: you wait for a partner, hope they are patient, hope they show up, and hope their corrections are useful. Fluency is a skill, and skills need reps, feedback, and progression — not luck.

Eloq is the reliable version of that dream. An AI tutor that is always available, never ghosts, and — critically — **measures you**. Every session produces phoneme-level pronunciation scores, grammar diagnostics, and a review queue built from your actual mistakes. Add CEFR-aligned paths and a job-interview simulator, and you get the one thing HelloTalk cannot promise: *evidence that you are getting better.*

**Thesis**

1. **Reliability beats randomness.** 24/7 availability with consistent pedagogy removes the #1 reason language-exchange users churn: waiting.
2. **Structure beats conversation.** Free chat is pleasant and pedagogically weak. Guided scenarios plus progression produce measurable gains.
3. **Proof beats promises.** A score you can trend, a report card you can share, and a published validation study are the trust assets in a category built on vibes.

**The wedge:** job seekers preparing for English-language interviews. Highest willingness to pay, clearest ROI, shortest path to a measurable outcome ("I got the offer"). This is a hypothesis with a $2.5k test (T-01), not a fact — and the whole financial model depends on it.

**Beachhead → expansion:** interview prep (M0–12) → university students and career centers (12–24) → professionals and B2B L&D (24+).

---

## What changed in v2 — the three material changes

| # | v1 | v2 | Why |
|---|---|---|---|
| 1 | Plus $9.99 / $69.99 · Career $19.99 / $149 | **Plus $12.99 / $79.99 · Career $24.99 / $149.99** | HelloTalk VIP is verified at $12.99/$79.99. Parity turns the comparison into "same price, and it answers." |
| 2 | Conversion 5–8% of MAU · churn 5.5% | **D35 install→paid 1.8% / 2.6% / 6.0% · churn 8%** | RevenueCat 2026 benchmarks: NA median 2.6%, top quartile 5.6%; AI apps churn ~30% faster. Break-even is ≈4.5%. |
| 3 | In-house GOP pronunciation scoring is the moat | **Phoneme scoring is commodity; license it. Moat = closed loop + outcome data + interview depth** | Speechace sells phoneme scoring as an API; Azure ships prosody as an add-on. A moat anyone can rent is not a moat. |

Plus a correction the model forced: **voice COGS $0.051 → $0.018 per session minute**. v1 charged 100% ASR duty and 100% TTS duty on the same minute, overstating cost ~2.2×.

---

## Evidence state

The canonical register is [`09-evidence-log.md`](09-evidence-log.md). It holds **46 claim IDs**:

| State | Count | Meaning |
|---|---|---|
| **V** verified | 21 | Dated public source, accessed 2026-11-15 (includes 9 RevenueCat benchmarks and 6 competitor facts) |
| **D** derived | 2 | Arithmetic over verified inputs, recomputable (plus 2 dual-tagged rows) |
| **H** hypothesis | 15 | No public evidence; each has a test ID (T-xx) in [`11`](11-experiment-backlog.md) |
| **A** abandoned | 3 | Withdrawn; must not appear publicly |
| **X** decision/commitment | 5 | Product choice or release gate, not a factual claim |

**What is verified:** HelloTalk and ELSA pricing, features, ratings, age rating, and data collection; Duolingo pricing; Deepgram/ElevenLabs rates; RevenueCat category benchmarks; Apple's 15% commission.

**What is not:** our conversion, churn, CAC, retention, voice cost under our own load, market size, and the validity of our score. Those are (H), and the tests that settle them are dated and costed. No doc in this set quotes an (H) number as if it were a fact.

---

## Business model

| Tier | Price (US) | Core promise |
|---|---|---|
| Free | $0 | 3 voice sessions/week (5 min), unlimited text chat, all drills, corrections never metered |
| Plus | **$12.99/mo · $79.99/yr** | Unlimited practice (fair use 20 min/day), full analytics, study plan, base packs |
| Career | **$24.99/mo · $149.99/yr** | Interview simulator, JD tailoring, pressure mode, readiness index; human mock at $49 |
| Packs | $19–$49 one-time | Interview Sprint, Business, Tech, Healthcare, Campus |
| Campus / B2B | $7–9/seat/mo (min 150) | Career-center dashboards, cohort reporting, SSO |

Free tier limits the **expensive** resource (voice minutes), never the **learning** (corrections, review queue, progress). Paywalling feedback would destroy trust in the first session.

The free-tier cap is load-bearing: at 20 min/MAU the free user costs ~$0.26/month against ~$0.81 revenue per free MAU; at 60 min it costs ~$0.78 and goes underwater below ~4% conversion. Tested in T-15.

---

## Headline numbers (base case, with wedge as upside)

| Metric | Downside | Base | Wedge |
|---|---|---|---|
| D35 install → paid | 1.8% | 2.6% | 6.0% |
| ARR at M24 | $2.00M | $2.64M | $5.36M |
| Gross margin M24 | 52.6% | 56.8% | 63.5% |
| Cash at M24 | −$1.57M | −$1.21M | +$0.31M |
| LTV : CAC | 2.4 | 3.2 | 6.5 |
| Cash-out | M17 | M18 | never |

Break-even D35 conversion: **≈4.5%**. The base case is not a comfortable plan; it is a thesis under test.

Full model, inputs, and sensitivities: [`10-financial-model.md`](10-financial-model.md) and the CSVs. If prose and model disagree, the model wins.

---

## Document index

| File | Contents | State |
|---|---|---|
| [`EXEC-SUMMARY.md`](EXEC-SUMMARY.md) | One page for an investor or hiring manager: thesis, wedge, moat, economics, milestones, risks, ask | New |
| [`01-product-spec.md`](01-product-spec.md) | Vision, problem, principles, feature specs, acceptance criteria, community layer, non-goals | Updated |
| [`02-roadmap-prioritization.md`](02-roadmap-prioritization.md) | RICE scoring, MVP vs later phases, cut list, dependencies, timeline, team | Updated |
| [`03-competitive-positioning.md`](03-competitive-positioning.md) | HelloTalk and ELSA teardowns, comparison table, GTM, **moat rewrite with a durability verdict** | Rewritten |
| [`04-personas-journeys.md`](04-personas-journeys.md) | Student and job-seeker personas, JTBD, journeys, paywall and churn moments | Updated |
| [`05-pricing.md`](05-pricing.md) | Tiers, limits, corrected COGS, benchmarked conversion, LTV/CAC, experiments | Rewritten |
| [`06-metrics.md`](06-metrics.md) | North star, **10 counter-metrics**, definitions, CI targets, outcome study design | Rewritten |
| [`07-technical.md`](07-technical.md) | Architecture, licensed scoring + in-house loop, LLM orchestration, moderation, offline, cost | Updated |
| [`08-risks-open-questions.md`](08-risks-open-questions.md) | Risk register, kill criteria, open questions, **assumption resolution map** | Rewritten |
| [`09-evidence-log.md`](09-evidence-log.md) | **Canonical claim register**, sources, test IDs, never-publish list | New |
| [`10-financial-model.md`](10-financial-model.md) | Scenarios, cost gate, LTV/CAC, runway, exclusions; reproducible via `build_model.py` | New |
| [`11-experiment-backlog.md`](11-experiment-backlog.md) | T-01–T-16 with MDE, sample size, cost, owner, kill/scale; ranked by IV/$ | New |
| [`12-launch-checklist.md`](12-launch-checklist.md) | Dated legal, money, product, content, quality, analytics, safety, ASO, launch runbook | New |
| [`13-decision-stress-tests.md`](13-decision-stress-tests.md) | Three load-bearing decisions: steelman, rebuttal, flip condition, cost of wrong | New |
| [`14-pronunciation-validation.md`](14-pronunciation-validation.md) | Rater pool, rubric, ICC, n=600, r ≥ 0.85 gate, L1 subgroups, accent-erasure criteria | New |

**Supporting:** [`NEXT-14-DAYS.md`](NEXT-14-DAYS.md) (action list) · `10-financial-model.csv` (monthly P&L, 4 runs) · `10-financial-model-inputs.csv` (every input + status) · `build_model.py` (generator).

---

## How to read the numbers

| Tag | Meaning | Where |
|---|---|---|
| **V** | Verified against a dated public source | `09` §1–2 |
| **D** | Derived arithmetic over V inputs | `09` §2–3, `10` |
| **H** | Hypothesis — no public evidence; has a test | `09` §2, test ID in `11` |
| **A** | Abandoned — do not publish | `09` §5 |
| **X** | Decision or commitment, not a fact | `09` §2.5 |

**Rule:** nothing tagged H goes into an investor deck, a public comparison page, or an ad without converting to V. The never-publish list is at `09` §5, and it includes "we retain better than HelloTalk," any HelloTalk retention number, and any market-size figure before T-14.

---

## What is still hypothesis (the honest list)

1. **Job seekers convert at 2–3× category rates.** T-01, $2.5k, 2 weeks.
2. **D35 lands in the base band or above.** T-16, 12 weeks, needs live traffic.
3. **Churn is 8%/month, not 12%.** T-06, 12 weeks.
4. **Voice cost is $0.018 now and $0.010 by M13.** T-11, 3 weeks.
5. **Our score correlates r ≥ 0.85 with human raters, per L1.** `14`, 8 weeks, ~$8.1k.
6. **Practice changes interview outcomes.** T-07, 16 weeks, $6k.
7. **The free-tier cap is not the growth constraint.** T-15, 8 weeks.

If items 1–4 fail, the plan changes shape. If 5–6 fail, the moat claim is withdrawn and the fallback is in `03` §9.8. Both outcomes are written down in advance, which is the point.
