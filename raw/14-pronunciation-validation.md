# 14 — Pronunciation Validation Protocol

**Version:** 2.0 · 2026-11-15

**Status:** designed, not yet run. First execution gate: 2027-05-14 (release candidate).
**Owner:** ML lead, with Research as independent analyst. The person who built the scorer does not compute the correlation.

> This document exists because the product's central promise is a number, and a number nobody has validated is a liability. It is also the document that makes the moat claim falsifiable: if the correlation does not clear the gate, the moat is not there, and `03` says what replaces it.

---

## 1. What the study must prove — and what it must not

**Prove:** our composite pronunciation score ranks utterances the way trained human listeners rank them for **intelligibility**, consistently across L1 backgrounds, well enough that a learner can trust the direction and magnitude of the number.

**Not prove:** that we can detect "accent," that we can make someone sound American, or that a high score means a hiring manager will hire them. Those are different claims, and two of them we will never make.

**Ship-as-beta rule:** until the r ≥ 0.85 gate is met on the full 600-utterance set, every composite score ships labeled **"beta / estimated"**, has no CEFR mapping attached in the UI, and is excluded from all marketing claims. The beta label is a release condition enforced by the checklist, not a copy decision someone can make under launch pressure. If the gate is never met, the product ships without a composite score (see §6) rather than shipping a number it cannot defend.

**Why intelligibility and not "accentedness":** accentedness and intelligibility are correlated but distinct; a speaker can be heavily accented and perfectly understood. Scoring accentedness would optimize for the wrong outcome and would build the accent-erasure failure mode directly into the metric. The rubric, the model target, and the marketing all point at intelligibility.

---

## 2. Design

| Element | Specification |
|---|---|
| Type | Criterion-validity study: system score vs. human consensus rating, same utterances, blinded |
| Population | Adult L1 speakers of Mandarin, Spanish, Portuguese, Hindi, Vietnamese, Arabic (the six launch L1s) |
| Speakers | 120 (20 per L1), stratified A2 / B1 / B2+ (≈ 7 per band per L1) |
| Utterances | 5 per speaker = **600** (2 read, 2 semi-spontaneous prompt responses, 1 interview answer) |
| Audio | Recorded on the production capture path (same codec, VAD, noise suppression) — not studio audio, because the product will never see studio audio |
| System output | Frozen model version, run **before** human ratings are collected; scores sealed |
| Human ratings | 3 independent raters per utterance = 1,800 ratings |
| Holdout discipline | Model is frozen and versioned; no tuning, threshold adjustment, or prompt change after unsealing. Any change restarts the study |

**Why 600:** with r ≈ 0.85, the standard error of a correlation at n = 600 is ≈ 0.011, giving a 95% CI of roughly ±0.02 — tight enough to distinguish 0.85 from 0.80. Utterances are clustered within speakers, so the analysis uses a **cluster bootstrap by speaker (120 clusters)**, not a naive independent-samples CI. Effective n is smaller than 600; the reported CI reflects that.

**Power for the subgroup read:** 100 utterances per L1 gives ±0.05 around a subgroup r of 0.85. That is enough to detect a broken L1 (r < 0.75), not enough to rank L1s finely — and we will not rank them.

---

## 3. Rater pool

| Requirement | Specification |
|---|---|
| Background | Licensed SLP, phonetics-trained linguist, or ESL teacher with ≥ 3 years of adult pronunciation teaching |
| Count | 9 recruited, 6 retained (3 per utterance; rotation for fatigue) |
| L1 mix | At least 3 raters are L2 English speakers; at least 2 have the same L1 as a rated subgroup, to catch "sounds wrong to a non-member" bias |
| Screening | Rate a 20-utterance calibration set; retain only raters with ICC ≥ 0.75 against the calibration consensus |
| Training | 2-hour session on the rubric, anchor examples, and the explicit instruction: *rate how easy this speaker is to understand, not how native they sound* |
| Blinding | Raters see no system score, no speaker metadata beyond the prompt, no L1 label |
| Order | Randomized per rater; each rater hears utterances from all L1s |
| Drift control | 5% repeated utterances (blind duplicates) spread across the study; drift > 8 points triggers retraining and re-rating of that block |
| Compensation | $22/hour target (validated by T-10), paid regardless of outcome |

---

## 4. Rubric

Single holistic dimension plus three diagnostic dimensions. The **holistic intelligibility score is the primary criterion**; the diagnostics exist to explain failures, not to be averaged into the headline.

| Dimension | Scale | Anchors |
|---|---|---|
| **Intelligibility (primary)** | 0–100 | **90–100:** effortless to follow; no listener repair. **75–89:** occasional effort; meaning never in doubt. **60–74:** sustained effort; 1–2 points need inference from context. **40–59:** frequent effort; listener would ask for repetition. **20–39:** much of the message is lost. **0–19:** isolated words only |
| Segmental accuracy | 0–4 | 4 = no segment interferes with meaning; 0 = multiple segments make words unrecognizable |
| Prosody (stress, rhythm, intonation) | 0–4 | 4 = stress placement supports meaning; 0 = flat or misplaced stress causes misparse |
| Fluency (pace, pausing, repair) | 0–4 | 4 = smooth, natural pausing; 0 = halting enough to impede comprehension |

**Instruction to raters, verbatim:** *"Rate how easy this speaker is to understand in this utterance. A strong accent is not an error. If you understood everything without effort, the score is high even if the speaker sounds clearly non-native."*

**Adjudication:** disagreements > 25 points on the holistic scale are re-rated blind by a fourth rater; the median of all ratings is used. Adjudication rate is reported (target < 10%; higher means the rubric is underspecified).

---

## 5. Statistics and gates

| Metric | Definition | Target |
|---|---|---|
| Human consensus | Mean of 3 raters; ICC(2,1) reported as reliability of that mean | **ICC ≥ 0.80** (below this, the criterion itself is noisy and the study is inconclusive, not failed) |
| **Primary r** | Pearson correlation, system composite vs. human consensus, cluster-bootstrapped CI | **r ≥ 0.85**; lower CI bound ≥ 0.80 |
| Rank agreement | Spearman ρ | ≥ 0.80 |
| Calibration | Mean absolute error between system score and human consensus | ≤ 8 points |
| Severe disagreement | Share of utterances where the absolute gap between system and human is > 25 points | ≤ 5% |
| Per-L1 r | Same, within each L1 (n ≈ 100) | ≥ 0.75 each; best–worst gap ≤ 0.10 |
| Per-band r | A2 / B1 / B2+ | ≥ 0.78 each (no "works only for advanced learners" outcome) |
| Accent-erasure check | See §7 | All four criteria pass |

All of these are **pre-registered** before data collection: hypothesis, primary metric, subgroup analyses, exclusion rules (e.g., recordings with clipping or < 40% speech), and the decision table in §6. Deviations are reported with reasons.

---

## 6. Failure handling (decided in advance, so the result cannot be negotiated)

| Outcome | Interpretation | What ships | Timeline |
|---|---|---|---|
| **r ≥ 0.85, all subgroups ≥ 0.75, all guardrails pass** | Gate passed | Full composite score, phoneme detail, trends; publish methodology | On schedule |
| **0.80 ≤ r < 0.85** | Directionally valid, magnitude unreliable | Ship **bands only** (`Needs work / Getting there / Clear / Strong`), no 0–100 number; publish the CI and the limitation | +3 weeks (UI copy, analytics) |
| **0.75 ≤ r < 0.80** | Weak | Ship **relative feedback only** ("this phoneme was clearer than last week"), no absolute score, no CEFR-linked claim; drop the score from all marketing | +6 weeks |
| **r < 0.75** | Gate failed | **Remove the composite score.** Product becomes drill-and-correction with human-reviewed rubrics for interview prep. `03` moat claim is withdrawn and replaced (see `03` §7.6) | Immediate re-scope; CEO + CPO decision |
| **Any single L1 r < 0.75** | L1-specific failure, likely ASR bias | Suppress composite for that L1 only; keep drills and corrections; run a 6-week remediation; publish the gap | Contained |
| **ICC < 0.80** | Human criterion unreliable | Study inconclusive — do not interpret r. Re-run with more raters/training, or simplify the rubric to holistic only | +4 weeks, ~$4k |

**The rule that makes this real:** the failure table is signed off by the CEO before data collection, and the model version is sealed with a hash. A post-hoc "let's look at a different correlation" is how every failed validation in this industry survived.

---

## 7. Accent-erasure guardrail (testable product requirements)

**The risk:** a pronunciation scorer trained on "how native does this sound" will systematically penalize L1-typical features that do not impair understanding — Vietnamese final-consonant deletion, Spanish epenthetic /e/, Hindi retroflex /t/, Arabic /p/–/b/ merging, Mandarin tone-carryover into English stress. Learners then chase accent reduction, lose confidence, and are taught that their identity is a defect. That is both an ethical failure and a product failure: it optimizes a signal that does not predict being understood.

**Guardrail definition:** the product must measure and reward **intelligibility**, and must never present sounding native as the goal.

| # | Requirement | Acceptance criterion | Measurement |
|---|---|---|---|
| **AE-1** | No penalty for intelligibility-neutral L1 variants | For utterance pairs that human raters score as equally intelligible (±5 points), the system score differs by **≤ 5 points** | 40 paired items per L1 (240 total), constructed from the study corpus; report per L1 |
| **AE-2** | The score means what we say it means | **≥ 90%** of users in a comprehension test (n = 60) correctly state that the score measures *how easily they are understood*, not *how native they sound* | Unmoderated comprehension test on the score screen; open-ended + multiple choice |
| **AE-3** | Drills target intelligibility, not accent | **≥ 95%** of drill recommendations map to an error class with measured comprehension impact (human confusions in the corpus), not merely to a non-native feature | Drill-selection audit on 200 recommendations |
| **AE-4** | Outcomes improve understanding, not accent similarity | In the 4-week cohort, human-rated **intelligibility** gain ≥ accent-similarity gain; accent similarity must not be the primary reported improvement | Pre/post 3-min tasks, blind-rated, n = 200 (T-07 cohort) |
| **AE-5** | No native-speaker comparison anywhere | Zero UI strings, notifications, or ads containing "native," "native-like," "sound American/British," or a country ranking of accents | Automated string audit in CI + manual review each release |
| **AE-6** | The learner is told what is not being measured | The score screen states, in one sentence, that accent is not a defect and that the score is about being understood | Screenshot review; included in the release checklist |

**If AE-1 fails**, the scorer is penalizing identity-linked variation. Fix by recalibrating on intelligibility-weighted targets or suppressing those phonemes from scoring — not by relabeling the marketing. If it cannot be fixed, the composite ships as bands (same fallback as §6).

**If AE-4 fails** (learners improve accent similarity but not intelligibility), the product is teaching the wrong thing and the curriculum needs rework before launch, regardless of how good the score correlation is.

---

## 8. Threats to validity

| Threat | Mitigation |
|---|---|
| Rater halo (one bad dimension colors the holistic score) | Holistic rated first, diagnostics after; randomized order; report dimension correlations |
| Rater drift over 6 weeks | Blind duplicates (5%), drift > 8 points triggers retraining and re-rating |
| Studio-quality audio inflating scores | All audio captured on the production path |
| Scripted speech easier than spontaneous | 40% read, 40% semi-spontaneous, 20% interview answer; reported separately |
| Selection bias (confident learners volunteer) | Recruit through the beta with a small incentive; stratify by CEFR band; report the achieved distribution |
| Model tuned on the test set | Model frozen and hashed before unsealing; any change restarts the study |
| Multiple comparisons across 6 L1s | Pre-register the subgroup analysis; apply Holm correction to subgroup p-values; treat subgroup r as descriptive with CI |
| Correlation without calibration | Report MAE and severe-disagreement rate alongside r; a high r with a 15-point bias is a fail |

---

## 9. Cost and timeline

| Line | Cost |
|---|---|
| Speaker recruitment + incentives (120 × $25) | $3,000 |
| Rater time: 1,800 ratings × ~1.5 min + 18 h training/adjudication ≈ 63 h × $22 | $1,390 |
| Rater recruitment/screening | $600 |
| Independent analyst (2 days) | $1,600 |
| Contingency (re-rating, extra adjudication) | $1,500 |
| **Total** | **≈ $8,100** |

**Timeline:** recruit 2 weeks → collect 3 weeks → rate 4 weeks (overlapping) → analysis 1 week. **8 weeks end-to-end**, starting 2027-03-15 to hit the 2027-05-14 release gate. If it slips, launch slips — the score is the product.

---

## 10. What we publish

- The method, the rubric, the rater qualifications, and the correlation with CI.
- Per-L1 results (including any subgroup below target) and the accent-erasure audit.
- The limitations in plain language: what the score does not measure, which accents are least reliable, and what we are doing about it.
- The negative results, if any. A published r = 0.79 with a documented remediation plan buys more trust than a suspiciously perfect 0.91.

**What we do not publish:** individual rater identities, raw audio, or any per-nationality comparison framed as a ranking. The point of the study is to earn the right to show a number; it is not to produce a leaderboard of accents.
