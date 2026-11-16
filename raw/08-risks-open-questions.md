# 08 — Risks, Open Questions, and Validation Plan

**Version:** 2.0 · 2026-11-15

**What changed in this revision:**
1. **The assumptions register is closed.** Every v1 unverified item is now either verified, derived, recorded as a hypothesis with a test ID, or abandoned. The canonical register is `09-evidence-log.md`; §8 here is a resolution map, not a second list.
2. **Kill criteria restated in corrected units** ($0.016 per session minute, not $0.035 per "voice minute").
3. **The 60-day validation plan moved** to `11-experiment-backlog.md`, where it is prioritised by information value per dollar and dated.
4. **The build-vs-license decision reversed** (R1, §7): pronunciation scoring is a commodity; the moat is the loop. See `13` D2.
5. **Prices corrected** throughout ($12.99 Plus, $24.99 Career).

---

## 1. Risk register

Scoring: **Likelihood** and **Impact** are H/M/L. **Trigger** is the observable event that tells us the risk is materializing — a risk without a trigger is a worry, not a risk.

| # | Risk | L | I | Trigger | Mitigation |
|---|---|---|---|---|---|
| R1 | **Pronunciation score fails validation** (r < 0.85 vs. human raters) | M | **H** | Week-6 spike returns r < 0.75 | Fallback ladder in `14` §6: bands → relative feedback → remove composite. Protocol pre-registered; rater pool screened at ICC ≥ 0.75 |
| R2 | **False corrections erode trust** | M | **H** | "This is wrong" rate > 4% or support tickets citing bad corrections | Hybrid deterministic + LLM gate at 0.8 confidence; 500-item gold set in CI; human audit 1%/week; instant rollback of prompt versions |
| R3 | **Voice COGS make the model unviable** | M | **H** | Blended cost > $0.016/session-min at M9 | Cost levers in `07` §9; month-9 gate to reprice or re-bundle; fair-use caps; TTS caching; measured (not modelled) cost in T-11 |
| R4 | **Retention below benchmark** (novelty churn) | **H** | **H** | D7 < 22% at M6 | Time-to-first-correction < 4 min; day-2 return experiments; streak repair; weekly report card; deadline countdown |
| R5 | **General assistants (ChatGPT/Gemini) ship a speaking coach** | **H** | **H** | A major assistant launches scored pronunciation or interview prep | Depth moat: validated assessment, closed-loop personalization, interview rubrics with evidence, published outcome data. Do not compete on general chat |
| R6 | **HelloTalk or Duolingo adds AI conversation + scoring** | M | M | Competitor ships a scored speaking feature | They can add features quickly; they cannot copy a validated instrument or four years of outcome labels quickly. Accelerate outcome publishing and interview depth |
| R7 | **Price resistance in Tier B/C markets** | M | M | Conversion < 2% in Tier C after 8 weeks | PPP pricing, local rails, student annual, pack purchases instead of subscription; Tier-C ceiling at 15 min/day |
| R8 | **ASR bias against non-native accents** → unfair scores and reputational damage | M | **H** | WER gap > 10 points between L1 groups | Per-L1 WER evaluation in CI; accent-robust fine-tuning; suppress scores below confidence; publish fairness results; `14` §7 audit |
| R9 | **Minor safety incident** | L | **Catastrophic** | Any report involving a user under 18 | 16+ gate, no DMs, pods-only, 1-hour escalation SLA, external safety audit before community launch |
| R10 | **Interview simulator is judged worse than a ChatGPT prompt** | M | **H** | < 30% of testers prefer it in blind comparison | Follow-up probing, rubric with evidence quotes, JD tailoring, pressure mode, human-reviewed mock as the premium anchor (T-02) |
| R11 | **Regulatory exposure** (EU AI Act, GDPR, voice data) | M | M | Regulator inquiry or app-store policy change | AI disclosure at first use; no voice biometrics; DPIA; regional processing; legal review per market |
| R12 | **Content production slower than roadmap** | **H** | M | < 8 scenarios ready at M4 | LLM-assisted authoring + human review; 5-scenario MVP if needed; license vetted content |
| R13 | **Key hire failure** (speech ML, conversation design) | M | **H** | Roles unfilled by week 8 | Contract specialists for the spike; advisor with L2 pronunciation publications; reduce scope to drill-only |
| R14 | **Seasonality of interview demand** | **H** | M | Revenue dips > 25% in off-season months | Student segment, workplace track, annual plans, B2B contracts, pause instead of cancel |
| R15 | **Data breach / audio leak** | L | **H** | Any unauthorized access | Encryption, short retention, least privilege, pen test pre-launch, incident runbook, cyber insurance |
| R16 | **Comparative advertising challenge** | L | M | Cease-and-desist or ad-platform rejection | Factual, dated, substantiated claims; legal review; neutral framing where required (`03` §8.3) |
| R17 | **Ethical: learners form dependent relationships with the tutor** | M | M | Session lengths climbing, distress signals, press coverage | No companion framing, no romantic persona, session caps, "this is practice, not a relationship" framing, off-ramps to humans |
| R18 | **Accent erasure** — the product teaches learners their identity is a defect | M | **H** | AE-1 or AE-4 fails (`14` §7); press or community criticism | Intelligibility-based rubric; accent-erasure acceptance criteria as release gates; no "native" strings (AE-5) |
| R19 | **Founder/team over-indexes on features, under-indexes on outcomes** | M | M | Roadmap slips toward social features | North star is scored speaking minutes; quarterly outcome cohort is a board-level commitment; counter-metrics (§2 of `06`) |

---

## 2. The four risks that can kill the company

Everything above matters; these are existential.

1. **R3 — unit economics.** If all-in voice cost does not fall below ~$0.016/session-minute, the freemium model compresses: at the fair-use ceiling, Plus is already margin-negative at launch. Mitigation is a hard M9 gate with pre-approved fallbacks (raise price, cut free minutes, or move to credits). Do not "wait and see."
2. **R1/R2 — assessment credibility.** The entire positioning is "measurable feedback." One viral screenshot of a wrong correction or a nonsense score undoes a year of marketing. Hence CI gates, rollback, and conservative confidence thresholds.
3. **R9 — minor safety.** A single serious incident ends the student segment, invites regulation, and poisons the brand. Community launch is gated on an external safety audit, not a date.
4. **R18 — accent erasure.** This is new on the existential list, and it deserves to be. If the score punishes Vietnamese final consonants or Spanish epenthesis because they are not "native," we are selling shame with a progress bar. That is a press story, a regulator story, and a moral failure in one. The acceptance criteria in `14` §7 are the control.

---

## 3. Open questions (with owners and deadlines)

| # | Question | Why it matters | How to answer | Deadline |
|---|---|---|---|---|
| Q1 | Which launch market first: Vietnam, Brazil, or India? | Determines content, payment rails, influencer strategy, CAC | 20 interviews per market; waitlist conversion test with $500 of ads per market | 2027-02-05 |
| Q2 | Is the pronunciation composite credible enough to gate the paywall? | If not, pricing must lean on interview prep | Validation study (`14`) + 20 user trust interviews | 2027-05-14 |
| Q3 | Do learners prefer Coach mode (interruptions) or Flow mode (deferred feedback)? | Core UX and pedagogy | In-app A/B with D7 and score-delta endpoints | 2027-03-15 |
| Q4 | Will job seekers pay $24.99 without a human in the loop? | Career tier is the margin engine | Fake-door test (`T-05`) + 15 pricing interviews | 2027-02-05 |
| Q5 | Should the free tier include unlimited text chat? | COGS vs. habit formation | Cohort test: unlimited text vs. 50 messages/day | 2027-08-01 |
| Q6 | Is 16–17 worth the compliance burden in year 1? | Safety risk vs. student funnel | Legal cost estimate; parental-consent conversion data | 2027-04-16 |
| Q7 | Build or license interview question banks? | Content speed vs. differentiation | Vendor demos; cost per role pack | 2027-06-01 |
| Q8 | Does the community layer need to exist at all? | Could be a distraction from the wedge | Survey: % who cite "meeting people" as a top-3 reason to stay | 2028-06-01 |
| Q9 | What is the real "better than HelloTalk" retention delta? | Central marketing claim | Matched-cohort panel study, third-party run (T-09) | 2028-02-01 |
| Q10 | Can we legitimately map scores to IELTS/TOEFL bands? | Huge marketing upside, high misrepresentation risk | Correlation study vs. official scores, n ≥ 100 | 2028-09-01 |

---

## 4. Validation plan (pointer)

The v1 60-day plan is now `11-experiment-backlog.md`. It keeps the same four gates, dated and with owners:

| Gate | Date | Pass condition |
|---|---|---|
| 1 — Economics | 2027-01-08 | Voice cost ≤ $0.018/session-min measured; no launch L1 > 25% WER |
| 2 — Wedge | 2027-02-05 | Job-seeker CPA ≤ student CPA; Career price confirmed at a fake door |
| 3 — Product | 2027-02-26 | Interview sim ≥ 55% blind preference vs a strong general-assistant prompt |
| 4 — Go/no-go | 2027-03-05 | Model re-run on real numbers; build or re-scope, in writing |

**Cost of the whole plan:** ~$31k cash, ~6 engineer-weeks, 8 weeks. It retires the three biggest unknowns before a line of production UI is written.

---

## 5. Kill criteria (pre-committed, so we do not rationalize)

| Signal | Threshold | Action |
|---|---|---|
| Activation after 2 onboarding iterations | < 30% | Stop paid acquisition; rebuild first session |
| D30 at month 9 | < 10% | Re-scope to interview-only product or shut down consumer |
| Pronunciation validity after 2 attempts | r < 0.80 | Remove composite score entirely; pivot messaging to structured practice |
| All-in voice cost at month 9 | > $0.020/session-min | Reprice, cut free minutes, or move to credits |
| D35 install→paid at month 9 | < 1.8% | The freemium model is not converting; switch to reverse trial or hard paywall, or re-scope |
| CAC payback | > 18 months for 2 consecutive quarters | Shift to organic/referral-only growth |
| Interview sim blind preference vs ChatGPT | < 30% | Do not launch the Career tier; stay consumer-only |
| Outcome study effect | treatment ≤ control + 5pp | Remove "get hired" from positioning |
| Any confirmed minor-safety incident | — | Immediate community freeze + external audit |
| Any AE-1/AE-4 failure after one remediation attempt | — | Suppress composite score; publish the failure |

Writing these down before launch is the point. Post-hoc thresholds always move.

---

## 6. Ethical commitments

These are constraints on the business, not marketing copy:

1. **No manufactured urgency.** Deadlines in the product come from the user's real interview date.
2. **No dependency by design.** No romantic or companion framing, no "I missed you," no emotional manipulation in notifications. Session-length caps exist partly for this reason.
3. **No accent shame.** We score intelligibility. We will not tell a learner they "sound wrong" for having an accent. Testable criteria: `14` §7.
4. **No fake progress.** Scores are traceable to evidence; uncertain scores are hidden; we publish our error rates.
5. **No selling voice data.** Not to advertisers, not to model vendors, not "anonymized."
6. **Minors are not a growth channel.** If the 16–17 segment cannot be served safely, we will not serve it.
7. **Honest limits.** We prepare for exams; we do not certify. We estimate CEFR; we do not award it. We say so on the same screen as the number.
8. **Publish the null result.** If the outcome study shows no effect, it gets published with the same prominence as a win.

---

## 7. Decision log

| Date | Decision | Rationale | Owner | Revisit |
|---|---|---|---|---|
| 2026-11-15 | English-only at launch | Depth over breadth | CPO | M18 |
| 2026-11-15 | Voice is metered, feedback is not | COGS + trust | CPO/CFO | M9 |
| 2026-11-15 | No 1:1 stranger chat, ever | Safety is the brand | CEO | Never |
| 2026-11-15 | Interview simulator is Phase 2 but strategically forced | Wedge + margin | CPO | M9 |
| 2026-11-15 | Community gated on external safety audit | Existential risk | CEO | At audit |
| 2026-11-15 | **License pronunciation scoring; build the calibration and error-memory loop in-house** | Scoring is a commodity (Speechace, Azure); the loop is the moat (`13` D2) | CTO | M12, with four flip conditions |
| 2026-11-15 | Plus at $12.99 / $79.99 (parity with HelloTalk VIP) | Same price, different product; covers median-usage COGS | CEO | After T-13 |
| 2026-11-15 | Career at $24.99; human mock is a $49 add-on | One included human review per 90 days would cut Career margin from 52% to 11% | CEO | After T-05 |
| 2026-11-15 | 16+ only at launch | Compliance capacity | CEO/Legal | M12 |
| 2026-11-15 | Free tier at 3×5 min/week, ~20 min/MAU utilisation | Free COGS stays below revenue per free MAU at base conversion | CPO | M9 (see `13` D1) |

---

## 8. v1 assumptions register — resolution map

Every v1 unverified item, and where it went. Nothing was deleted; each is verified, corrected, downgraded to a dated hypothesis, or abandoned.

| v1 assumption | v1 status | v2 resolution | Evidence / test | Where |
|---|---|---|---|---|
| HelloTalk pricing and feature set | unverified | **Verified** — $12.99/mo, $79.99/yr, 70M+ learners, 260+ languages, 13+ | S1, S2 (accessed 2026-11-15) | `09` C1–C6, `03` §1–2 |
| HelloTalk/category retention (D1/D7/D30) | unverified | **Abandoned as a HelloTalk claim.** No public data. Category conversion benchmarks verified; retention measured on our own beta | S10; T-08; T-09 | `09` C7, B10, B11; `06` §4 |
| Voice COGS $0.051 → $0.021/min | unverified | **Corrected** to $0.018 → $0.010 per *session* minute (duty-cycle error of ~2.2×) | K1–K5; T-11 | `05` §4, `10` §1 |
| Conversion 5–8% of MAU | unverified | **Replaced** by benchmarked D35 scenarios 1.8% / 2.6% / 6.0%; break-even ≈ 4.5% | S10; T-01, T-04 | `05` §5, `10` §6.2 |
| Paid churn 5.5%/mo | unverified | **Revised** to 8%/mo, with sensitivity at 5/8/12/20% | S10; T-06 | `09` M5, `10` §6.1 |
| Interview cohort outcome ≥ 45% | unverified | **Downgraded** to hypothesis (≥ 35% target) with a pre-registered 200/200 study | T-07 | `06` §6, `09` M4 |
| Market size ~80M serviceable | unverified | **Downgraded** to hypothesis; must be rebuilt bottom-up before any deck uses it | T-14 | `09` M1 |
| CAC $6–45 by channel | unverified | **Downgraded** to hypothesis; live channel test, $8k | T-03 | `09` K9, `05` §5 |
| CEFR estimate κ ≥ 0.70 | unverified | **Reclassified** as a commitment (release gate), not a forecast | P2 | `06` §7 |
| "Better retention than HelloTalk" | implied | **Abandoned as a public claim** until a matched cohort exists | T-09 | `03` §3, `09` §5 |
| In-house pronunciation scoring is the moat | implicit | **Reversed.** Scoring is commodity; license it, own the loop | C11, S6, S7 | `03` §9, `13` D2 |
| Speak pricing | unverified | **Abandoned** — pricing page 404 on 2026-11-15; do not name a price | C10 | `09` C10 |
| ELSA positioning | not stated | **Corrected** — ELSA ships interview coaching + CEFR mapping at $19.99/$99.99; we are not first | S5 | `03` §4, `09` C9 |

**Rule:** nothing marked H in `09` goes into a public comparison page, an investor deck, or an ad without the tag converting to V. A claim that changes price or feature status reverts to H the day it is found stale.
