# Eloq — Executive Summary

**One page. Sendable today.** Version 2.0 · 2026-11-16 · Confidential

---

## What it is

Eloq is an AI English fluency coach for people with a dated, high-stakes English event: a job interview, a first job, a semester abroad. It gives them a real conversation on demand, phoneme-level pronunciation feedback, an error-memory-driven review queue, and a weekly measure of whether they are actually getting better.

The benchmark is HelloTalk. HelloTalk is a 70M-user language-exchange network whose supply is volunteers' free time. It is genuinely good at friendship and cultural exchange. It cannot guarantee a partner, a curriculum, or a measurement — because its core loop depends on strangers showing up.

## Thesis

1. **Reliability beats randomness.** A partner gives you an hour a week when they feel like it. A coach is there at 2 a.m., corrected, without judgment.
2. **Structure beats conversation.** Guided scenarios, CEFR progression, and a daily plan outperform unstructured chat for people with a deadline.
3. **Proof beats promises.** A score you can trend, a report card you can show, and a published validation study are the trust assets in a category built on vibes.

## Wedge

**Job seekers preparing for English-language interviews.** They have a deadline, a budget, and an outcome we can point at ("I got the interview"). Consumers pay for outcomes, not features. The wedge is tested for $2.5k before a line of production UI is written (T-01), because the entire financial model depends on job seekers converting at 2–3× category rates.

## Moat — honest verdict

**Phoneme-level pronunciation scoring is not a moat.** It is sold as an API (Speechace) and shipped as a platform add-on (Azure). Our v1 plan called it the moat; that was wrong, and the plan now says so.

What can be defensible, in order of strength:

| Layer | Verdict |
|---|---|
| Acoustic scoring | Commodity — license it |
| Closed-loop personalization (which drill, which scenario, in what order) | Plausible, unproven |
| Interview content depth (roles, JDs, rubrics with evidence) | Medium — copyable slowly |
| **Longitudinal outcome data (practice → interview → offer)** | **The only asset that cannot be bought** — and we have zero of it today |
| Switching costs (error history, review state, mock recordings) | Modest; not yet measured |

**Three-year narrative:** Year 1, validity and content. Year 2, 5,000+ learners with 90-day outcome labels plus career-center distribution. Year 3, the Interview Readiness Index becomes the reference standard career centers cite. That is a plausible flywheel, not a proven one — and if validation fails and the outcome study is null, the fallback is assessment/credentialing sold to institutions, which is a smaller, slower, better-margin business (`03` §9.8).

## Unit economics

Prices: **Plus $12.99/mo · $79.99/yr** (parity with HelloTalk VIP) · **Career $24.99/mo · $149.99/yr** (anchored under ELSA at $19.99/mo and far under a $100–300 human mock).

Corrected voice cost: **$0.018 per learner session minute at launch → $0.010 by M13** (v1 overstated this by ~2.2× by charging 100% ASR and 100% TTS duty on the same minute). Month-9 gate: **≤ $0.016**.

| | Downside | Base | Wedge |
|---|---|---|---|
| D35 install → paid | 1.8% | **2.6%** (NA median) | **6.0%** (just above top quartile) |
| ARR at M24 | $2.00M | **$2.64M** | **$5.36M** |
| Gross margin M24 | 52.6% | **56.8%** | **63.5%** |
| Cash at M24 | −$1.57M | **−$1.21M** | **+$0.31M** |
| LTV : CAC | 2.4 | **3.2** | **6.5** |
| Cash-out | M17 | **M18** | never |

**Break-even D35 conversion is ≈4.5%** — roughly twice the category median. There is no comfortable base case. The company either proves the wedge converts above 4.5% in the first nine months or changes shape.

**Model caveat we disclose rather than bury:** the base case includes a B2B line (200 seats at M16 ramping to ~6,660 by M24, $0.56M ARR, no sales cost). Strip it out and base M24 gross margin falls from 56.8% to 45.2%. Treat B2B as upside; the consumer thesis has to stand without it (`10` §8.1).

## Milestones

| When | Milestone | Gate |
|---|---|---|
| M0 (Dec 2026) | Seed close, build starts | Team of 8; cost instrumentation specced |
| M3 (Feb 2027) | Wedge + product gates | T-01 job-seeker CPA ≤ student; T-02 interview sim ≥ 55% preference |
| M6 (Jun 2027) | Public MVP | Activation ≥ 40%, D7 ≥ 25%, crash-free ≥ 99.5% |
| M9 (Sep 2027) | Cost gate + D35 read | Voice ≤ $0.016/session-min; D35 ≥ 1.8% or kill path |
| M12 (Dec 2027) | Series A point | ARR ~$0.7M (base), D35 ≥ 2.6%, churn ≤ 8% |
| M24 (Dec 2028) | Scale or re-scope | $2.64M base / $5.36M wedge ARR; GM ≥ 55% |

## Top three risks

1. **Conversion.** If D35 stalls at 2.6%, cash runs out at M18 and the Series A has no story. Trigger: D35 < 1.8% at M9. Response: cut paid acquisition 50%, execute the cash-efficient variant, plan a bridge or re-scope. Tested by T-16, pre-empted by T-01.
2. **Credibility.** One viral nonsense score or wrong correction undoes a year of marketing. Trigger: r < 0.85, false-correction rate > 3%, or an accent-erasure audit failure. Response: ship bands instead of a number, or remove the composite score and re-position around structured practice.
3. **Unit cost.** If voice cost stalls above $0.020/session-minute, Plus is margin-negative at the fair-use ceiling. Trigger: month-9 gate missed. Response: reprice, cut free minutes, or move to credits — decided at M9, not M14.

(A fourth, gating constraint: **minor safety.** No community layer until an external safety audit passes. One incident is existential.)

## The ask

**$4.0M seed for 18 months of runway.** Use of funds: ~$0.85M pre-launch build and data collection, ~$1.6M engineering and content through M12, ~$1.1M growth experiments, ~$0.45M legal/safety/infrastructure.

What it buys: the two studies that make the company defensible — a published pronunciation validation (r ≥ 0.85, per-L1) and a 400-person interview-outcome study with a control group — plus enough traffic to know whether the wedge converts above 4.5%.

**What we are not claiming:** we have no users, no retention data, and no validated score yet. Every competitor comparison is dated and sourced in `09-evidence-log.md`; every unverified number is tagged (H) with the test that would settle it. The plan is designed to be falsified cheaply, and the kill criteria are written down before launch.
