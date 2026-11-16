# 06 — Metrics and Success Criteria

**Version:** 2.0 · 2026-11-15

**What changed in this revision:**
1. **Counter-metrics added (§2).** The north star can be gamed in at least six ways; each now has a paired counter-metric with a threshold and a response.
2. **Benchmarks are sourced, not asserted.** The "HelloTalk retention is ~40/20/10" claim is **withdrawn** — HelloTalk publishes nothing. Category benchmarks now come from RevenueCat's 2026 dataset, and the one HelloTalk-specific claim we want is gated behind a matched-cohort study (T-09).
3. **Targets are ranges with confidence intervals, not single numbers.** A point estimate at n = 500 is false precision.
4. **M24 targets corrected** to match the financial model ($2.0–5.4M ARR, not the v1 "$20–35M" that no scenario produced).
5. **Outcome study specified end-to-end** (§6), including randomization, verification, ITT analysis, and publication rules.

---

## 1. North star

> **Weekly Scored Speaking Minutes per Active Learner (WSSM)**

*Definition:* total minutes of learner speech that received a pronunciation/fluency score in a 7-day window, divided by weekly active learners (≥ 1 session in the window).

**Why this and not DAU:** DAU rewards opening the app; minutes-of-scored-speech rewards the only behavior that produces fluency. It is also hard to inflate with notifications, because the minutes have to actually be spoken.

**Guardrails on the north star** (the first line of defense against gaming):
- Median session length stays 5–12 minutes (longer is not better; fatigue ≠ progress).
- Correction precision stays ≥ 92%.
- Session abandonment (started but not finished) stays < 18%.

But guardrails are not enough, because WSSM can still be inflated without improving anyone's English. That is what §2 is for.

---

## 2. Counter-metrics (the anti-gaming layer)

Every metric the team is paid on will be optimized, including in ways that hurt the learner. These are the counter-metrics we report **next to** the north star, every week, on the same dashboard. A north-star win that comes with a counter-metric breach is not a win.

| # | Counter-metric | Definition | Threshold | What it prevents | Response if breached |
|---|---|---|---|---|---|
| CM-1 | **Unique-speech ratio** | Unique scored seconds ÷ total scored seconds (audio-hash dedupe) | ≥ 0.85 | Replaying the same clip dozens of times to farm "scored minutes" | Exclude duplicates from scoring and from WSSM; show the learner a re-record prompt |
| CM-2 | **Conversation share** | Minutes in free/scenario conversation ÷ total scored minutes | ≥ 60% (Plus) | Farming cheap drill minutes; drills score fast and are easy to pad | Rebalance the Daily Plan toward conversation; review drill scoring cost |
| CM-3 | **Level-appropriate share** | Share of sessions at or above the learner's current band | ≥ 70% | Staying in A2 content because it produces high scores | Cap easy-content repetition; require a stretch session per week |
| CM-4 | **Score stability (drift)** | Change in mean score for a fixed, human-rated gold set, month over month | ≤ ±2 points | Score inflation from model/prompt drift | Recalibrate; freeze the model version; re-run the gold set |
| CM-5 | **Score–evidence consistency** | Share of score movements ≥ 5 points that have a corresponding change in the correction log | ≥ 80% | Unexplained score jumps that feel arbitrary (or are engineered) | Investigate the scoring path; suppress the trend line until explained |
| CM-6 | **Streak repair share** | Repaired streak days ÷ total streak days | ≤ 35% | A streak that is mostly repairs is a participation trophy, not a habit | Reduce repair availability; re-anchor streaks to weekly goals |
| CM-7 | **Notification opt-out rate** | Opt-outs ÷ notification recipients, monthly | ≤ 3% | Push spam inflating DAU/WAL without learning | Cap at 2 pushes/day; audit copy for urgency |
| CM-8 | **"This is wrong" rate** | User-flagged corrections confirmed wrong ÷ total corrections | ≤ 3% | Surfacing more (and worse) corrections to look "helpful" | Roll back the model; tighten the confidence gate |
| CM-9 | **Refund and chargeback rate** | Refunds ÷ paid transactions, monthly | ≤ 4% | Dark-pattern paywalls and oversold guarantees | Review paywall copy and the guarantee terms |
| CM-10 | **Post-session self-report** | "Did this session help you say something you couldn't say before?" (sampled 10%) | ≥ 60% yes | Minutes that feel like work but teach nothing | Session design review; content quality audit |

**Reporting rule:** the weekly review opens with the north star, then the ten counter-metrics, then revenue. In that order. If a counter-metric is red for two consecutive weeks, the growth experiment that caused it stops — regardless of its conversion lift.

---

## 3. Definitions (the ones teams argue about)

| Metric | Definition | Notes |
|---|---|---|
| **Activated user** | Completes ≥ 1 voice session of ≥ 3 min **and** receives ≥ 1 correction **and** reviews ≥ 5 vocabulary items, all within 24 h of signup | Deliberately demanding: this is the first value moment |
| **D1 / D7 / D30 retention** | % of a signup cohort with ≥ 1 qualifying session on day 1 / within 7 days / within 30 days | "Qualifying" = ≥ 3 min voice or ≥ 10 reviews |
| **Weekly active learner (WAL)** | ≥ 1 qualifying session in a rolling 7 days | Not "opened the app" |
| **Streak-7 / Streak-30** | % of cohort with an unbroken daily or weekly-goal streak at day 7/30 | Repair days count as kept if repaired within 24 h (see CM-6) |
| **D35 conversion** | Installs that become paying subscribers within 35 days ÷ installs | The model's input; use this, not "conversion of MAU" |
| **Paid conversion (MAU)** | Paying subscribers / MAU | Report only as a secondary view; MAU is a denominator that flatters |
| **Trial → paid** | Paid within 3 days of trial end / trials started | Career trial only |
| **ARPU** | Net revenue (after store fees, refunds, tax) / paying users / month | Never gross |
| **Logo churn** | Cancellations + expirations / paying users at period start | Monthly; split voluntary/involuntary |
| **Correction precision** | Correct corrections / all corrections shown | Sampled weekly, human-audited |
| **False-correction rate** | User-flagged "this is wrong" corrections confirmed wrong / total corrections | Target < 3% |
| **Interview Readiness Index (IRI)** | 0–100 composite: structure, relevance, fluency, pronunciation, register | Must be validated, not invented (P7) |
| **CEFR agreement** | Quadratic weighted κ between app estimate and certified examiner | ≥ 0.70 |

---

## 4. Benchmarks: what "good" looks like

**First, the honest part: HelloTalk does not publish retention data, and neither does ELSA.** Any claim of the form "we retain better than HelloTalk" is currently unverifiable. The only valid way to make it is a matched-cohort study we run ourselves (T-09, $12k, 12 weeks). Until then, public messaging says "designed for daily practice," not "retains better than X." That sentence replaces the v1 benchmark table's HelloTalk column.

What we *can* source (RevenueCat, *State of Subscription Apps 2026*, accessed 2026-11-15):

| Benchmark | Value | Implication |
|---|---|---|
| Freemium D35 install→paid, all categories | 2.1% | Our base case is only slightly above this |
| North America D35 median | 2.6% | **Base-case scenario** |
| NA top quartile / P90 | 5.6% / 10.4% | Wedge case at 6.0% is just above top quartile |
| Hard-paywall D35 | 10.7% | Why we test a reverse trial (T-04) |
| IN/SEA D35 median | 1.4% | Tier-C expectations |
| AI apps: revenue per payer / churn | +41% / 30% faster | Churn is the tax on the AI category |
| Education Y1 realized LTV per payer | $22.82 | Our $93 LTV is a top-quartile claim, not a neutral one |
| Education annual-plan share | 59–66% | Supports 60% annual mix in the model |
| 3-day trial cancellations on day 0 | 55% | Conversion is decided in the first session |

**Our targets vs. those benchmarks** (M12, with the basis stated):

| Metric | Category benchmark | Eloq M12 target | Why we think we can beat it | Confidence |
|---|---|---|---|---|
| D1 | No verified series | **55%** (CI 48–62%) | Onboarding delivers a correction in < 6 min; deadline-driven intent | Medium |
| D7 | No verified series | **35%** (CI 27–43%) | Daily Plan + visible score movement; deadline countdown | Medium-low |
| D30 | No verified series | **22%** (CI 15–29%) | Structured progression; pause instead of cancel | Low-medium |
| D35 install→paid | 2.6% NA median | **2.6% base / 6.0% wedge** | Segment-specific intent; Career SKU | Low (this is the bet) |
| Monthly churn | Category RLTV implies high | **8%** (CI 6–12%) | Annual plans; bounded Career usage | Low-medium |
| DAU/MAU | No verified series | **30%** (CI 22–38%) | Practice is a daily behaviour | Medium |

**How to read the confidence column:** "Low" means we have no evidence yet and the target could plausibly be half. "Medium" means we have a mechanism and partial analogue evidence. Nothing here is "high" before beta data — and the plan should be sized accordingly, which is exactly what the scenario model does.

---

## 5. Targets by phase (ranges, not points)

### MVP (month 6, closed beta + early public)

| Metric | Target | Range at n ≈ 1,000 signups |
|---|---|---|
| Activation | ≥ 40% | 36–44% |
| D7 | ≥ 25% | 21–29% |
| D30 | ≥ 15% | 11–19% |
| WSSM per WAL | ≥ 18 min | 15–21 |
| Session completion | ≥ 80% | 77–83% |
| Correction precision | ≥ 90% | gate, not estimate |
| p50 first-audio latency | ≤ 1.5 s | gate |
| D35 install→paid | ≥ 1.8% | 1.3–2.5% |
| Crash-free sessions | ≥ 99.5% | gate |

### Month 12

| Metric | Target | Range |
|---|---|---|
| Activation | ≥ 50% | 46–54% |
| D7 / D30 | 35% / 22% | 30–40 / 18–26 |
| WSSM per WAL | ≥ 28 min | 24–32 |
| D35 install→paid | ≥ 2.6% | 2.0–3.4% |
| Trial → paid (Career) | ≥ 35% | 28–42% |
| Monthly churn | ≤ 8% | 6–12% |
| ARPU (net) | ≥ $13.00 | $12–14.50 |
| LTV : CAC | ≥ 3.0 | 2.2–4.2 |
| 4-week score gain (20 min/day cohort) | +8 points | +5 to +11 |
| Interview cohort: next-stage interview ≤ 90 days | ≥ 35% | 28–42% (T-07) |

### Month 24

Sized to the base case, with the wedge as upside. **v1's "$20–35M ARR at M24" was not produced by any scenario in this model and has been removed.**

| Metric | Downside | Base | Wedge |
|---|---|---|---|
| MAU | 179k | 179k | 179k |
| Paying subscribers | 11.6k | 16.8k | 38.8k |
| ARR (net revenue × 12) | $2.00M | $2.64M | $5.36M |
| Gross margin | 52.6% | 56.8% | 63.5% |
| Cash at M24 | −$1.57M | −$1.21M | +$0.31M |
| B2B ARR | $0.56M | $0.56M | $0.56M |

The MAU line is identical across scenarios because installs are held constant — only conversion varies. That is deliberate: it isolates the one variable the company can actually influence in year one.

**The constraint, stated once:** break-even D35 conversion is **≈4.5%** (`10` §6.2). The base-case M12 target of 2.6% sits *below* break-even, which is why the meaningful gate is not "hit the target" but "get above break-even before the runway ends." Any dashboard that shows conversion without this line is lying by omission.

---

## 6. Learning outcome measurement (end-to-end design)

This is the part most language apps fake. The design below is the one we will publish, including when it fails.

### 6.1 The two studies

| | **Study A — speaking gain** | **Study B — interview outcome** |
|---|---|---|
| Question | Does 4 weeks of practice improve scored speaking? | Does the program change hiring outcomes? |
| Design | Pre/post with a waitlist control | Randomized encouragement design with a matched control |
| n | 300 (200 treatment / 100 control) | 400 (200 / 200) |
| Duration | 4 weeks + 30-day delayed post-test | 16 weeks (90-day outcome window) |
| Primary | Blind-rated intelligibility delta on standardized tasks | Next-stage interview within 90 days |
| Secondary | CEFR movement, vocabulary retention, IRI delta | Offer rate, time-to-offer, self-reported confidence |
| Control activity | Drills + SRS only, no voice sessions | Waitlist, plus a light-content newsletter (keeps engagement comparable) |
| Cost | ~$9k | ~$6k |
| Owner | Research (independent analyst) | Research |

**Why a waitlist control is ethical here:** the control group receives the product at the end of the study. We do not withhold treatment beyond 90 days, and the study is described as such at consent. A randomized encouragement design (randomized invitation to the intensive cohort) is used where full randomization would deny access to people who signed up specifically for it.

### 6.2 Procedure (Study B, the one that matters commercially)

1. **Recruit** from in-app users who declare an interview within 90 days and consent to follow-up. Target 500 to absorb 20% attrition.
2. **Baseline** within 72 h: placement, IRI, target role, JD, interview date, country, English level.
3. **Randomize** (stratified by level, country, and weeks-to-interview) to intensive track (≥ 5 sessions/week + 2 AI mocks) or control.
4. **In-product instrumentation** records sessions, mocks, drill completion, and IRI trajectory — no self-report for usage.
5. **Outcome capture at day 90:** did you have a next-stage interview? An offer? Verified by (a) recruiter email or calendar screenshot where consent allows, or (b) self-report plus a 20% verification subsample. Report both the verified and the full-sample estimate.
6. **Analysis:** intention-to-treat as primary; per-protocol as secondary. Logistic regression with pre-registered covariates. Report absolute risk difference with a 95% CI, not just a p-value.
7. **Publication:** method, n, attrition, effect size, CI, and limitations. Negative and null results published with the same prominence.
8. **Decision use:** if the treatment effect is < 5 percentage points, the "get hired" claim is removed from all marketing within 30 days (T-07 kill criterion).

### 6.3 Validity guardrails

- Pre-register the analysis plan (primary metric, covariates, exclusions) before unblinding.
- Blind raters to condition and to time point; randomize the order of pre/post recordings.
- Report attrition by arm; if differential attrition > 10 points, the result is labeled "at risk of bias."
- Never quote a testimonial as evidence of typical results.
- Publish the control-group outcome too. If the control also improves 20 points, the product is not the cause.

---

## 7. Quality metrics (release blockers, not dashboards)

| Metric | Threshold | Consequence if breached |
|---|---|---|
| Correction precision | ≥ 92% | Roll back the correction model version |
| False-correction rate | < 3% | Block release |
| ASR WER, read speech | ≤ 12% overall; ≤ 18% per L1 | Improve model or add L1 adaptation |
| ASR WER, spontaneous speech | ≤ 22% | Improve endpointing/vocabulary |
| Pronunciation–human correlation | ≥ 0.85 Pearson (lower CI ≥ 0.80) | Do not show composite score (see `14` §6) |
| Accent-erasure audit (AE-1…AE-6) | All pass | Suppress composite or recalibrate (`14` §7) |
| p95 first-audio latency | ≤ 2.0 s | Latency incident |
| TTS naturalness (MOS) | ≥ 4.2 / 5 | Switch vendor for that locale |
| Moderation recall (red-team set) | ≥ 95% | Block release |
| Minor-safety incidents | 0 | Immediate incident review |
| Data-deletion SLA | ≤ 72 h | Compliance escalation |

---

## 8. Instrumentation

**Event taxonomy** (one namespace, one meaning per event):

```
app_open, onboarding_step{step,completed}, goal_set{type,deadline},
placement_start, placement_complete{level,confidence},
session_start{type,scenario,difficulty}, turn_end{latency_ms,asr_conf,audio_hash},
correction_shown{type,confidence}, correction_flagged{reason},
session_end{duration_s,words,score_delta,completed,unique_speech_s},
report_view{section}, vocab_capture{source}, review_complete{cards,retention},
drill_start{phoneme}, drill_complete{items,score_delta},
interview_start{role,type}, interview_end{iri,questions},
paywall_view{trigger}, checkout_start{plan,price,currency},
subscribe{plan,price,currency}, cancel{reason,save_offer_shown},
notification_sent{type}, notification_optout,
share{surface}, referral_sent, referral_converted,
delete_request, export_request
```

**Rules**
1. Every experiment is defined before instrumentation; no post-hoc metric selection.
2. Client events are timestamped server-side for latency and funnel integrity.
3. No PII in event properties; audio is referenced by opaque ID only; `audio_hash` exists solely for CM-1 dedupe.
4. One warehouse, one definitions layer (dbt-style), one owner per metric.
5. Dashboards are reviewed monthly; anything unused for 60 days is deleted.
6. Counter-metrics ship in the same dashboard release as the north star. A north star without its counter-metrics does not launch.

---

## 9. Experiment cadence and statistical discipline

| Cadence | What runs |
|---|---|
| Weekly | 1 onboarding/paywall experiment, 1 content experiment; counter-metric review |
| Bi-weekly | 1 model/prompt quality experiment (offline eval + small online A/B) |
| Monthly | Pricing/packaging readout; retention cohort review |
| Quarterly | Outcome cohort report; benchmark refresh; strategy review |

**Power:** all A/B tests are powered at 80% for a 5% relative lift on the primary metric; underpowered tests are labeled "directional" and never ship a decision on their own. Minimum runtime 7 days **and** ≥ 1 full weekly cycle, whichever is longer. No test is read early because it "looks done."

---

## 10. Vanity metrics we will not report

- Total registered users (never a business metric).
- Cumulative minutes practiced (only a growth chart in disguise; also the most gameable).
- App store rating alone (manipulable, non-diagnostic).
- "Lessons completed" without a score delta.
- Social followers, press mentions, or awards.
- Any retention number that includes users who only opened the app.
- Any "conversion" number whose denominator is MAU rather than installs.

---

## 11. Leading indicators to watch weekly

1. **Time to first correction** (< 4 min target) — predicts D7 more strongly than any other onboarding metric.
2. **Day-2 return rate** — the earliest reliable signal of habit.
3. **Second-session score delta** — if learners do not see movement by session 2, the feedback is too vague.
4. **Review-queue completion rate** — if < 60%, the queue is too long or too boring.
5. **Paywall view → checkout start** — predicts conversion 3 weeks out.
6. **"This correction is wrong" rate** — leading indicator of trust collapse (CM-8).
7. **p95 latency** — leading indicator of silent churn; users rarely complain, they leave.
8. **Unique-speech ratio** — leading indicator that WSSM growth is real (CM-1).

---

## 12. Ownership and review

| Metric group | Owner | Review |
|---|---|---|
| North star + counter-metrics | Head of Product | Weekly |
| Retention cohorts | Data | Weekly |
| Unit economics (COGS, ARPU, churn) | Finance | Monthly |
| Quality gates | ML lead | Every release |
| Outcome studies | Research | Quarterly |
| Benchmark refresh | Research | Quarterly |

**The one rule that matters:** nobody owns a metric alone. The person who owns the north star does not own the counter-metrics that constrain it — those sit with Quality and Research, who have no incentive to inflate the number. That separation is the cheapest governance we can buy.
