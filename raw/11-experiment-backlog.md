# 11 — Experiment Backlog

**Version:** 2.0 · 2026-11-15

**Supersedes:** the 60-day validation plan in `08` §4 (that plan is now the first two columns of this one).
**Rule of this document:** a test exists only if it changes a decision. If the result — either way — would not change what we build, price, or fund, it is not on this list. Vanity research is how seed-stage teams burn a quarter.

---

## 1. How these are ranked

Information value per dollar:

```
IV/$  ≈  P(result changes decision) × cost of being wrong  ÷  cost of test
```

That formula puts free engineering spikes above paid media tests, and it puts the wedge-defining tests above everything. The ranking below is the order to *start* them, not the order to finish them — several run in parallel.

| Rank | ID | Test | Decision it unblocks | Cost | Weeks | Why here |
|---|---|---|---|---|---|---|
| 1 | T-11 | Voice cost per session minute | Whether Plus at $12.99 has a margin at all | $0 | 3 | Cheapest test with the largest effect on the model |
| 2 | T-12 | ASR WER by L1 accent | Which L1s we launch; whether scores can be shown | $0 | 3 | Blocks the product's core promise |
| 3 | T-10 | Human rater cost | Whether the validation study is affordable | $0 (quotes) | 1 | Gates T-07 and doc `14` |
| 4 | T-01 | Job seeker vs student conversion | The wedge itself | $2.5k | 2 | The entire financial model rests on this |
| 5 | T-14 | Bottom-up market size | Whether the TAM story survives diligence | $0 | 2 | Free, and it removes a public-claim risk |
| 6 | T-05 | Will job seekers pay $24.99? | Career tier price | $1k | 2 | Price is hard to change after launch |
| 7 | T-02 | Interview sim vs ChatGPT prompt | Whether the Career tier has a product | $1.5k | 3 | Kills or funds the wedge |
| 8 | T-04 | Reverse trial vs metered free | Free-tier architecture | $0 (product) | 6 | 8 weeks of build if wrong |
| 9 | T-08 | Our real D1/D7/D30 | All retention targets | $0 | 8 | Needs beta traffic; cannot run earlier |
| 10 | **T-15** | **Free-tier generosity: 60 vs 20 min/MAU** | **Whether the cap is a growth constraint or a cost control** | **$0 (product)** | **8** | **Load-bearing: at 60 min the free tier is underwater below ~4% conversion** |
| 11 | T-13 | $12.99 vs $9.99 | Plus price | $0 | 4 | Only matters after activation works |
| 12 | **T-16** | **D35 calibration: is reality downside, base, or wedge?** | **Whether to raise, hold, or cut the growth plan** | **$0** | **12** | **The model's three scenarios become distinguishable only with live cohorts** |
| 13 | T-03 | Real CAC by channel | Paid acquisition budget | $8k | 4 | Expensive; needs a working funnel first |
| 14 | T-06 | Real paid churn | LTV and runway | $0 | 12 | Needs 3 months of live cohorts |
| 15 | T-07 | Do learners get interviews? | The outcome claim | $6k | 16 | Longest lead time; start recruiting early |
| 16 | T-09 | Matched cohort vs language exchange | Whether we may say "better than HelloTalk" | $12k | 12 | Marketing claim only; nothing else depends on it |

**Total to retire the top nine unknowns: ≈ $5.0k in cash plus ~6 engineer-weeks.** The two expensive tests (T-07, T-09) are deferred because nothing in the build depends on them — only the marketing does, and marketing can wait for evidence instead of preceding it.

---

## 2. Test cards

### T-11 — Real voice cost per session minute

- **Hypothesis:** all-in incremental cost ≤ $0.018 per learner session minute at launch, ≤ $0.010 by M13.
- **Method:** instrument 200 real sessions on the production stack (streaming ASR, LLM turn generation, TTS, pronunciation scoring). Log per-turn audio seconds, characters synthesized, tokens, GPU-seconds. Reconcile against vendor invoices, not estimates.
- **Primary metric:** $ per session minute, with p50/p90 across session types (drill, conversation, interview).
- **MDE:** ±$0.003 — this is a measurement, not an A/B, so the bar is invoice reconciliation within 15%.
- **Sample:** 200 sessions / ≥ 2,000 learner-minutes / 3 device classes / 2 networks.
- **Duration:** 3 weeks. **Cost:** $0 cash (vendor credits).
- **Owner:** Eng lead (infra).
- **Kill:** p50 > $0.025 → cut free minutes before launch and re-run pricing (T-13).
- **Scale:** ≤ $0.018 → proceed to launch pricing; publish the unit-cost table internally as the canonical figure.
- **Note:** this test exists because v1 was wrong by 2.2× on this exact number. Do not accept a spreadsheet answer.

### T-12 — ASR word error rate by L1 accent

- **Hypothesis:** WER ≤ 12% read / ≤ 22% spontaneous overall, and no launch L1 worse than 25%.
- **Method:** 300 utterances (6 L1s × 50), read + spontaneous, transcribed by two humans, scored against vendor ASR. Stratify by CEFR band (A2, B1, B2+).
- **Primary metric:** WER per L1 with 95% CI; secondary: substitution patterns that indicate accent bias rather than learner error.
- **MDE:** detect a 5-point WER gap between L1 groups (n=50/L1 gives ±~7 points; report as directional per L1 and pooled).
- **Sample:** 300 utterances, 2 human transcripts each.
- **Duration:** 3 weeks. **Cost:** $0 cash beyond staff time (recordings from beta).
- **Owner:** ML lead.
- **Kill:** any proposed launch L1 > 25% WER → drop that L1 from launch, or suppress scoring for it (feedback only).
- **Scale:** all six L1s under 22% spontaneous → keep six-language onboarding support.
- **Note:** fairness is a release gate, not a nice-to-have (`08` R8). Also check whether errors cluster on *intelligible* L1 variants — that is the accent-erasure risk in doc `14` §6.

### T-10 — Human rater cost and availability

- **Hypothesis:** qualified raters (SLP, ESL teacher, phonetics-trained) available at ≤ $22/hr, with ≥ 12 qualified candidates in 2 weeks.
- **Method:** three recruiter/marketplace quotes; screen six candidates on a 20-utterance calibration set; measure inter-rater agreement on the screen.
- **Primary metric:** cost per rated utterance-minute; ICC on the screen set.
- **MDE:** n/a (sourcing test).
- **Sample:** 3 quotes, 6 screened raters.
- **Duration:** 1 week. **Cost:** $0 (quotes) + ~$200 screening.
- **Owner:** Research.
- **Kill:** > $30/hr or ICC < 0.70 on screen → change rubric granularity (rate intelligibility + prosody only, drop segmental counts) before committing to the main study.
- **Scale:** ≤ $22/hr and ICC ≥ 0.80 → book the 600-utterance study described in `14`.

### T-01 — Do job seekers convert better than students?

- **Hypothesis:** cost per activated signup is lower for job-seeker messaging than student messaging, and job seekers reach paywall view at ≥ 1.5× the rate.
- **Method:** two landing pages (identical product pitch, different promise and creative), identical spend, geo-matched. Job seeker angle: "interview in English in 8 weeks." Student angle: "speak up in seminars."
- **Primary metric:** cost per verified waitlist signup (email + goal + deadline).
- **MDE:** 30% relative difference in signup rate at 80% power.
- **Sample:** 800 visitors per arm (≈1,600 total).
- **Duration:** 2 weeks. **Cost:** $2.5k media + $0 (page build reuses onboarding).
- **Owner:** Growth.
- **Kill:** job-seeker CPA > 1.5× student CPA **and** job-seeker "interview within 60 days" share < 25% → wedge is wrong; re-plan around student-first (see `13` D3).
- **Scale:** job-seeker CPA ≤ student CPA → lock the wedge, fund interview content first.
- **Note:** this is the single most consequential test in the plan. The model's break-even conversion (~4.5%) assumes the wedge converts at 2–3× category rates.

### T-14 — Bottom-up market size

- **Hypothesis:** serviceable obtainable market ≥ 20M learners across five launch countries, reachable at ≤ $45 CAC.
- **Method:** desk research — tertiary enrollment, English-requirement exam volumes (IELTS/TOEFL/PTE), outbound job-seeker counts, smartphone penetration, app-store category revenue. Build from country-level counts upward; do not use an analyst headline.
- **Primary metric:** SAM (learners with a dated English-speaking goal) and SOM (reachable at target CAC).
- **MDE:** n/a. **Sample:** 5 countries, 3 sources each, all dated.
- **Duration:** 2 weeks. **Cost:** $0.
- **Owner:** Strategy.
- **Kill:** SOM < 20M → the "venture-scale" story is dead; plan a profitable niche instead and say so in the deck.
- **Scale:** SOM ≥ 40M → unlock the higher-growth hiring plan in `10` §7.

### T-05 — Will job seekers pay $24.99?

- **Hypothesis:** ≥ 8% of qualified job-seeker visitors take a $24.99/mo or $149.99/yr Career offer at a fake door.
- **Method:** fake-door pricing page after a 3-question qualification (target role, interview date, current level). Price shown; click-through to a waitlist with "we'll email you when Career opens." No charge.
- **Primary metric:** qualified visitor → pricing-page CTA rate.
- **MDE:** 4 percentage points around a 10% baseline.
- **Sample:** 1,000 qualified visitors (≈450/arm if testing $24.99 vs $19.99).
- **Duration:** 2 weeks. **Cost:** $1k media.
- **Owner:** Growth + PM.
- **Kill:** < 8% take-rate at $24.99 with $19.99 ≥ 8% → launch at $19.99 and cut Career COGS (drop the human mock).
- **Scale:** ≥ 12% at $24.99 → keep price, and test $29.99 in the same design next quarter.
- **Caveat:** fake doors overstate intent. Treat the *relative* gap between price points as the signal, not the absolute rate.

### T-02 — Interview simulator vs a ChatGPT prompt

- **Hypothesis:** ≥ 55% of blind testers prefer our interview session to a well-prompted general assistant for interview practice.
- **Method:** 30 job seekers, within-subject, order-randomized, same role and same JD. Blind scoring by the participant on: realism, usefulness of feedback, confidence for the real interview, likelihood to use again. Then a think-aloud on why.
- **Primary metric:** forced-choice preference; secondary: rubric-with-evidence quality rating.
- **MDE:** 20 points above 50% (n=30 gives ~80% power for 70/30).
- **Sample:** 30 completed paired sessions (recruit 45).
- **Duration:** 3 weeks. **Cost:** $1.5k incentives.
- **Owner:** PM (product research).
- **Kill:** < 30% prefer ours → do not launch Career in M9; stay consumer Plus and re-scope the wedge.
- **Scale:** ≥ 55% and ≥ 40% say "materially more useful" → Career launches on schedule.
- **Note:** the comparison must use a *strong* ChatGPT prompt (role, JD, STAR, feedback at end), not a strawman. A win against a bad prompt is worthless.

### T-04 — Reverse trial vs metered free tier

- **Hypothesis:** a 14-day full-access reverse trial produces higher D30 paid conversion than the 3×5-minute metered free tier, without wrecking D30 retention of non-converters.
- **Method:** two-arm in-app test at first session. Arm A: metered free (current). Arm B: 14 days of Plus, then fall back to metered free (not locked out). Both arms see identical paywall creative after the trial.
- **Primary metric:** D35 install → paid (the model's actual input), reported with D30 retention as a co-primary.
- **MDE:** +1.0pp absolute on a 3% base; co-primary D30 retention +5pp on 15%.
- **Sample:** 2,300 installs per arm for the paid endpoint; 400/arm for the retention endpoint. Run to the larger.
- **Duration:** 6 weeks (4 weeks to accrue installs + 35-day maturity). **Cost:** $0 cash, ~3 engineer-weeks.
- **Owner:** Growth + Eng.
- **Kill:** trial arm D35 paid not ≥ +1pp absolute → stay metered, stop testing trial length.
- **Scale:** trial arm wins on both endpoints → adopt reverse trial at M9 and re-run the cost model with the new free-minute profile.
- **Evidence basis:** RevenueCat SOSA 2026 — hard paywalls convert ~5× better at D35 (10.7% vs 2.1%), and 17+ day trials convert 42.5% vs 25.5% for short trials. Those are category numbers, not ours; this test is how we find out if they transfer.

### T-08 — Our real D1 / D7 / D30

- **Hypothesis:** D1 ≥ 55%, D7 ≥ 35%, D30 ≥ 22% (the M12 targets, measured early to avoid a late surprise).
- **Method:** cohort instrumentation from day one of beta; no retroactive definitions. Report by acquisition channel and by persona (self-declared goal).
- **Primary metric:** D7 qualifying-session retention.
- **MDE:** descriptive with ±3pp CI at n=1,000 signups.
- **Sample:** 1,000 beta signups minimum.
- **Duration:** 8 weeks. **Cost:** $0.
- **Owner:** Data.
- **Kill:** D7 < 22% after two onboarding iterations → `08` §5 kill criteria fire; stop paid acquisition.
- **Scale:** D7 ≥ 30% in beta → proceed to public launch and start T-03.
- **Note:** this is the test that decides whether the retention targets in `06` are real or aspirational. Publish the number internally even when it is bad.

### T-15 — Free-tier generosity: 60 vs 20 minutes per MAU (load-bearing)

- **Hypothesis:** raising the free allowance from 20 to 60 minutes per MAU does **not** lift D35 install→paid by ≥ 1pp, and does raise free COGS by ~$0.50/MAU.
- **Why it is load-bearing:** the model shows free-tier cost is the largest controllable COGS line. At 20 min/MAU the free user costs ~$0.26/month against ~$0.81 revenue per free MAU at M12 (base) — positive. At 60 min it costs ~$0.78, which is underwater at any conversion below ~4.0%. The cap is either a growth lever or a cost control, and we do not know which.
- **Method:** two-arm in-app test at onboarding, 8 weeks. Arm A: 3×5 min/week (current, ~20 min/MAU average). Arm B: 3×20 min/week (allows ~60 min/MAU utilisation). Identical paywall, onboarding, and content. Measure both conversion and actual utilisation (many users will not use the extra minutes, which is the point).
- **Primary metric:** D35 install→paid. Co-primary: free COGS per MAU (from T-11's production instrumentation).
- **MDE:** +0.8pp absolute on a 2.6% base (powered at n ≈ 5,800 installs per arm — run as a rolling sequential read at 8 weeks and label directional if underpowered).
- **Sample:** as many installs as 8 weeks of beta+launch traffic provides; minimum 2,500/arm.
- **Duration:** 8 weeks. **Cost:** $0 cash, ~1 engineer-week.
- **Owner:** Growth + Finance.
- **Kill:** Arm B lifts D35 by < 0.8pp **or** raises free COGS per MAU by more than $0.30 without a conversion lift → keep 20 minutes; the cap is not the constraint.
- **Scale:** Arm B lifts D35 by ≥ 1.5pp and utilisation stays < 35 min/MAU → move to 45 min/MAU and re-run the model (`13` D1 flip condition requires all three conditions, not just this one).
- **Maps to:** D1 (free tier), K5 (voice COGS), `10` §6.3.

### T-13 — $12.99 vs $9.99

- **Hypothesis:** $12.99 produces equal or higher revenue per visitor than $9.99 despite lower conversion.
- **Method:** geo-matched price test on the paywall, monthly plans only, 50/50. Annual untouched.
- **Primary metric:** net revenue per paywall view over 35 days.
- **MDE:** 20% relative on revenue per visitor.
- **Sample:** 3,000 paywall views per arm (may be underpowered early; if so, label directional and decide on the larger of the two effects).
- **Duration:** 4 weeks. **Cost:** $0.
- **Owner:** Growth.
- **Kill:** revenue per visitor worse at $12.99 by > 10% → move Plus to $9.99 and re-run the model at the lower ARPU.
- **Scale:** $12.99 ≥ $9.99 → keep parity with HelloTalk VIP; use "same price as HelloTalk, and it answers" in creative.
- **Note:** never run this while T-04 is live — price and paywall structure interact.

### T-16 — D35 calibration: downside, base, or wedge? (load-bearing)

- **Hypothesis:** our D35 install→paid settles in the base band (2.2–3.0%), not the downside (< 2.0%) and not the wedge (> 5.5%).
- **Why it is load-bearing:** D35 is the only variable that separates the three financial scenarios. Holding everything else constant, 1.8% produces a $2.0M ARR business that runs out of cash at M17; 2.6% produces $2.64M and cash-out at M18; 6.0% produces $5.36M and a self-funding company. Nothing else in the model moves the outcome as much.
- **Method:** rolling cohort measurement on 90-day maturity, segmented by acquisition channel, persona (self-declared goal), and market. No A/B — this is a measurement with a pre-registered decision rule. Report a 4-week rolling estimate with a 95% CI and a 12-week smoothed estimate.
- **Primary metric:** D35 install→paid.
- **MDE:** distinguish 2.6% from 3.4% at 80% power with n ≈ 4,600 installs per read (≈8 weeks at launch volume).
- **Sample:** all installs, minimum 10,000 by M9.
- **Duration:** 12 weeks (rolling). **Cost:** $0.
- **Owner:** Growth + Data.
- **Decision rule (pre-registered):**
  - **< 1.8% at M9** → downside confirmed. Execute the `08` §5 kill path: cut paid acquisition 50%, start the cash-efficient variant, and plan a bridge or re-scope.
  - **1.8–3.0%** → base confirmed. Proceed to Series A at M14–15 with the $2.64M-ARR story and the wedge as upside, not as the plan.
  - **3.0–5.5%** → between base and wedge. Extend the wedge tests (T-01, T-05) and hold hiring flat until the band resolves.
  - **> 5.5%** → wedge confirmed. Raise the growth plan, increase paid spend, and re-run the model on the new D35.
- **Kill:** n/a — this is a calibration test, not a feature test; the decision rule above is the kill/scale logic.
- **Maps to:** B1–B3, M5, `10` §6.2, `13` D3.

### T-03 — Real CAC by channel

- **Hypothesis:** blended CAC ≤ $29 with at least one channel ≤ $15 at scale.
- **Method:** $8k across short-form video, search, and one community/creator channel; separate landing pages and promo codes per channel; 8-week attribution window.
- **Primary metric:** CAC per activated user and per paid subscriber, by channel, with CI.
- **MDE:** distinguish $15 from $30 CAC at n≈200 installs per channel.
- **Sample:** ~600 installs total, ≥ 150 per channel.
- **Duration:** 4 weeks spend + 4 weeks maturity. **Cost:** $8k.
- **Owner:** Growth.
- **Kill:** blended CAC > $60, or no channel < $45 → paid acquisition is not a growth engine; shift to organic/referral and re-plan the hiring plan.
- **Scale:** one channel ≤ $20 CAC with payback < 6 months → double spend there and only there.

### T-06 — Real paid churn

- **Hypothesis:** blended monthly churn ≤ 8%, with annual plans ≤ 3%.
- **Method:** cohort survival analysis on live subscribers; separate monthly and annual; separate Career and Plus; exclude involuntary churn from the product-quality read but include it in the LTV read.
- **Primary metric:** monthly logo churn at 90 days of cohort age.
- **MDE:** ±2pp at n=500 paid.
- **Sample:** 500 paid subscribers, 3 months.
- **Duration:** 12 weeks. **Cost:** $0.
- **Owner:** Finance + Data.
- **Kill:** > 12%/mo → LTV:CAC falls below 2 at current CAC; stop paid acquisition and fix onboarding before scaling.
- **Scale:** ≤ 6%/mo → the base-case LTV in `10` §5 is conservative; revisit the Series A timing.
- **Context:** RevenueCat's Education Y1 realized LTV of $22.82/payer implies category churn is much worse than our 8% assumption. Assume we are wrong until T-06 says otherwise.

### T-07 — Do learners get interviews? (outcome study)

- **Hypothesis:** ≥ 35% of the interview cohort reaches a next-stage interview within 90 days, vs ≤ 20% in a matched control.
- **Method:** 200 treatment / 200 control (waitlist or drills-only), matched on target role, country, English level, and interview timeline. Pre-registered analysis. Outcome verified by screenshot or recruiter email where the participant consents; otherwise self-report with a 20% verification subsample.
- **Primary metric:** next-stage interview within 90 days.
- **MDE:** 10pp absolute (35% vs 25% → n≈220/arm at 80% power; 200/arm detects ~11pp).
- **Sample:** 200 per arm, recruit 500 to absorb attrition.
- **Duration:** 16 weeks. **Cost:** $6k incentives.
- **Owner:** Research.
- **Kill:** treatment ≤ control + 5pp → the outcome claim is dead; stop using "get hired" in positioning and lead with measured speaking gain.
- **Scale:** ≥ 35% and ≥ 10pp over control → publish it. This is the only marketing asset a competitor cannot copy.

### T-09 — Matched cohort vs language-exchange users

- **Hypothesis:** our D30 retained-practice rate exceeds a matched language-exchange cohort by ≥ 10pp.
- **Method:** third-party panel (or disclosed survey with app-usage self-report) matched on country, age, English level, and goal. Same measurement window, same definition of "practice session."
- **Primary metric:** D30 retained practice.
- **MDE:** 10pp at n=300/arm.
- **Sample:** 300 per arm.
- **Duration:** 12 weeks. **Cost:** $12k.
- **Owner:** Research.
- **Kill:** no measurable delta → permanently retire "retains better than HelloTalk" and keep the reliability/structure message.
- **Scale:** ≥ 10pp → publish methodology and use it in comparison pages, with legal review.

---

## 3. Eight-week schedule

| Week | Running | Milestone |
|---|---|---|
| 1 | T-10 quotes, T-11 instrumentation, T-14 desk research | Rater vendor chosen; cost instrumentation live |
| 2 | T-11 sessions, T-12 recordings, T-01 landing pages live | First cost number (provisional) |
| 3 | T-11 close, T-12 scoring, T-01 read | **Gate 1:** voice cost ≤ $0.018 and no L1 > 25% WER, or re-scope |
| 4 | T-05 fake door, T-02 recruiting, T-04 design | Price point shortlisted |
| 5 | T-05 read, T-02 sessions, T-04 build | **Gate 2:** Career price and wedge confirmed |
| 6 | T-02 read, T-04 launch, T-08 baseline | **Gate 3:** interview sim beats a strong prompt, or Career is cut |
| 7 | T-04 accruing, T-08 accruing, T-13 prep | Beta retention read (provisional) |
| 8 | All reads, model re-run, go/no-go memo | **Gate 4:** build the MVP on these numbers, or re-scope |

**Gate rule:** a gate is a written memo with the number, the CI, and the decision. No gate is passed verbally, and no gate is re-run without changing the design first.

**Post-launch additions:** T-15 (free-tier generosity) and T-16 (D35 calibration) begin at public launch (M6). They need live cohorts, so no amount of pre-launch spending accelerates them — which is why the pre-launch plan is engineered to be cheap and fast rather than exhaustive.

---

## 4. Sample-size method (so nobody has to trust the numbers above)

Two-proportion tests, two-sided α = 0.05, power = 80%:

```
n per arm = 7.84 × p(1 − p) / MDE²
```

where `p` is the baseline rate and `MDE` is the absolute difference to detect. Examples:

| Baseline | MDE | n per arm |
|---|---|---|
| 10% | 3pp | 784 |
| 15% | 5pp | 392 |
| 30% | 7pp | 660 |
| 3% | 1pp | 2,233 |

**Caveats we will state in every readout:** these are planning numbers, not promises; multiple comparisons inflate false positives (we pre-register one primary metric per test); and any test that lands under its planned n is labeled **directional** and cannot on its own trigger a pricing or positioning change.

---

## 5. Tests we are deliberately not running

| Not running | Why |
|---|---|
| Brand awareness / perception tracking | Meaningless at pre-launch scale; expensive; changes nothing |
| Feature-preference surveys ("would you use X?") | People are bad at predicting their own behavior; fake doors and usage data are cheaper and truer |
| Competitor NPS | We cannot sample their users credibly; would produce a number we could not defend |
| Price ladder beyond three points | Diminishing information; confuses the read |
| A/B tests on the north star directly | It is an outcome, not a lever; test the levers (activation, session length, drill completion) |
| "Will AI replace tutors?" | Strategy essay, not an experiment |

---

## 6. Governance

1. **One primary metric per test.** Secondary metrics are reported, never used to declare a win.
2. **Pre-register** the hypothesis, the metric, the MDE, and the stopping rule before launch. Store it in the test log with a date.
3. **No peeking-then-stopping.** Interim reads are for safety (crash rate, abuse), not for significance.
4. **Results land in `09-evidence-log.md`** — the claim register is the single source of truth. A test that closes without updating the register did not happen.
5. **Kill criteria are pre-committed** and may only be changed with a written reason and a new date.
6. **Every test has one owner** who is accountable for the readout, not for the outcome being favorable.
