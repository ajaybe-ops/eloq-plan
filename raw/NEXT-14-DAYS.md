# What I'd do in the next 14 days

**Version:** 1.0 · 2026-11-16

**Window:** Monday 2026-11-16 → Sunday 2026-11-29
**Rule:** the next 14 days exist to retire the three load-bearing unknowns — voice cost, wedge conversion, and whether the interview product exists. Everything else can wait.

---

## The three things that matter

| Question | Why it decides the company | Test | Cost |
|---|---|---|---|
| What does a minute actually cost? | At $0.020+ the pricing inverts | T-11 | $0 |
| Do job seekers convert better than students? | The entire model rests on 2× category conversion | T-01 | $2.5k |
| Will they pay $24.99 for interview prep? | Career is the margin engine | T-05 | $1k |

If only three things get done in 14 days, these are the three. Everything below serves them.

---

## Week 1 — instrument, don't decide

| Day | Action | Owner | Output |
|---|---|---|---|
| **Mon 11-16** | Freeze the v2 doc set; create the decision-memo template (number, CI, decision, date); assign one owner per test | CEO | Test owners named; template in repo |
| Mon 11-16 | Send RFQ to 3 rater marketplaces/recruiters (T-10); post for 6 screened raters | Research | 3 quotes requested |
| Mon 11-16 | Write the T-11 instrumentation spec: log ASR seconds, TTS chars, tokens, GPU-seconds per turn, reconciled to invoice | Eng lead | Spec reviewed |
| **Tue 11-17** | Instrument staging with cost telemetry; run 20 test sessions | Eng lead | First raw cost number |
| Tue 11-17 | Start T-14 bottom-up market model: 5 countries × 3 dated sources | Strategy | Spreadsheet v0 |
| Tue 11-17 | Draft T-01 landing pages (job-seeker vs student), tracking plan, $2.5k budget split | Growth | Pages in staging |
| **Wed 11-18** | Launch T-01 ($1,250 per arm, geo-matched); verify UTM + conversion events fire | Growth | Live campaign |
| Wed 11-18 | Screen 6 raters on the 20-utterance calibration set | Research | ICC screen result |
| Wed 11-18 | Draft T-05 fake-door pricing page ($24.99 vs $19.99) + qualification questions | PM | Page in staging |
| **Thu 11-19** | Launch T-05 ($500); confirm no charge path exists | Growth | Live page |
| Thu 11-19 | Record first 60 utterances for T-12 (6 L1s × 10), read + spontaneous | ML lead | Corpus v0 |
| Thu 11-19 | Review T-14 draft; kill any figure without a dated source | Strategy | Source table |
| **Fri 11-20** | T-11 at 50+ sessions; reconcile against vendor dashboard | Eng lead | Cost estimate ±20% |
| Fri 11-20 | T-01 week-1 read — **no decision**, check tracking integrity only | Growth | Sanity check |
| Fri 11-20 | T-05 week-1 read — **no decision** | Growth | Sanity check |
| **Sat–Sun** | No spend changes. Read the two landing-page comment threads; fix clarity issues only | PM | Copy fixes |

**Friday checkpoint (no gate):** is the instrumentation trustworthy? If cost telemetry is not reconcilable to invoices by Friday, stop and fix it — a number you cannot defend is worse than no number.

---

## Week 2 — read, decide, write it down

| Day | Action | Owner | Output |
|---|---|---|---|
| **Mon 11-23** | T-14 complete: SAM/SOM by country, all sources dated | Strategy | Market memo |
| Mon 11-23 | T-12 scoring: 2 human transcripts per utterance; WER by L1 with CI | ML lead | WER table |
| Mon 11-23 | T-01 week-2 read with CI; segment CPA and "interview within 60 days" share | Growth | Readout |
| **Tue 11-24** | T-11 close: cost per session minute by session type; p50/p90 | Eng lead | Cost memo |
| Tue 11-24 | T-10: select rater vendor; book the 600-utterance study for March | Research | Signed SOW |
| Tue 11-24 | T-05 week-2 read; compare $24.99 vs $19.99 CTA rate | Growth | Readout |
| **Wed 11-25** | **Gate 1 memo:** voice cost ≤ $0.018 and no launch L1 > 25% WER? Pass / conditional / fail | CEO + Eng + ML | Written decision |
| Wed 11-25 | If Gate 1 fails: pick the fallback *now* (tighten free tier, drop an L1, reprice) | CEO | Fallback chosen |
| **Thu 11-26** | **Gate 2 memo:** is job-seeker CPA ≤ student CPA? Is $24.99 clearing 8%? | CEO + Growth | Written decision |
| Thu 11-26 | If wedge fails: start the student-first replan per `13` D3 (do not wait for launch) | CEO + PM | Replan brief |
| **Fri 11-27** | Re-run `build_model.py` with any measured input that changed; regenerate CSVs; update `10` and `EXEC-SUMMARY.md` | Finance | Model v2.1 |
| Fri 11-27 | Update `09-evidence-log.md`: every closed test changes a claim from H to V/D, or stays H with a new date | Research | Register updated |
| **Sat 11-28** | Write the internal status memo: what we now know, what we still don't, what changed in the plan | CEO | 2 pages |
| **Sun 11-29** | Plan the next 14 days against the *measured* numbers, not the planned ones | CEO | Next sprint list |

---

## Definition of done for the 14 days

- [ ] A measured (not modelled) voice cost per session minute, reconciled to at least one vendor invoice or dashboard.
- [ ] A T-01 read with a confidence interval, and a written wedge decision.
- [ ] A T-05 read, and a written Career price decision.
- [ ] T-14 market memo with every figure sourced and dated.
- [ ] Six screened raters and a signed SOW for the 600-utterance study.
- [ ] `09-evidence-log.md` updated: no test closed without a claim changing state.
- [ ] The model re-run if any input moved; no doc quoting a stale number.
- [ ] One page of "what we got wrong this week" — because the first two weeks always produce some.

## What we will not do in the 14 days

- Build the app. The point of these tests is to avoid building the wrong one.
- Run a brand study, a naming exercise, or a logo review.
- Add scenarios, packs, or features beyond what the tests need.
- Negotiate a vendor contract longer than a pilot.
- Publish any comparative claim. Nothing is verified enough yet, and `09` §5 lists what may never be said.

## The failure mode to avoid

Spending 14 days making the plan prettier. The documents are good enough to act on; the numbers inside them are not yet good enough to bet on. The only work that matters now is converting (H) into (V) or (D) — one measured cost, one conversion read, one price signal.
