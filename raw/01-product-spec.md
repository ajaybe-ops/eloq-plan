# 01 — Product Specification

**Version:** 2.0 · 2026-11-15

**What changed in this revision:** pricing references updated to $12.99 Plus / $24.99 Career; market sizing downgraded to explicit hypotheses with a test (T-14) instead of a unverified marker; pronunciation described as licensed acoustic scoring plus in-house calibration rather than "core IP"; CEFR and accent-erasure commitments cross-referenced to `14`. No feature scope changed.

## 1. Vision

Anyone preparing for an English-speaking life event — an interview, a first job, a semester abroad — should be able to rehearse it out loud, tonight, alone, without embarrassment, and get feedback precise enough to change what they do tomorrow.

## 2. Problem statement

**Who:** 16–30 year-old English learners (~B1–C1) in emerging and non-anglophone markets, split into two high-intent groups: students and job seekers.

**What they do today:** HelloTalk, Tandem, Cambly, italki, YouTube, ChatGPT, and free "speaking clubs." Each fails in a specific way:

| Substitute | Failure mode |
|---|---|
| Language-exchange apps (HelloTalk, Tandem) | Partner availability, ghosting, unqualified corrections, safety concerns, zero structure |
| Human tutoring (Cambly, italki) | $10–$30/hr, scheduling friction, no between-session accountability |
| General LLMs (ChatGPT voice) | No curriculum, no scoring, no memory of your errors, no drills, no progression |
| Content apps (Duolingo, BBC Learning) | Input-heavy, almost no scored speaking output |
| Self-study (YouTube, shadowing) | No feedback loop; learners cannot hear their own errors |

**Core job to be done:**
> "When I have to speak English in a situation that matters, help me practice it realistically, tell me exactly what is wrong, and prove to me that I am improving — without depending on another person's schedule or goodwill."

**The gap in one line:** the market has *conversation* (HelloTalk) and *curriculum* (Duolingo) but not *measured conversation*.

## 3. Product principles

1. **Speaking first.** Any feature that does not increase spoken output or improve the quality of the next utterance is secondary.
2. **Never fake precision.** If the score is uncertain, say so ("estimated"). Trust is the whole product.
3. **Correct the error, not the accent.** We score intelligibility and prosody, not proximity to a US accent. Accent erasure is not a goal and will not be marketed.
4. **The learner owns their data.** Voice recordings are sensitive. Default retention 30 days, exportable, deletable in one tap, never used for ad targeting.
5. **One clear next action.** At every point the app answers "what should I do right now?" — never a content library dump.
6. **No social pressure at launch.** No leaderboards against strangers, no public profiles, no DMs. Motivation comes from personal progress, not comparison.
7. **Degrade gracefully.** Bad wifi, noisy room, shared device, old phone — the session must still be useful.

## 4. Market and segment strategy

**All figures in this table are hypotheses (H) except where noted.** They are used for internal planning only and must not appear in an investor deck or a public page until T-14 rebuilds them bottom-up. See `09` M1–M2.

| Layer | Estimate | Status |
|---|---|---|
| Global English learners | ~1.5B | H — widely cited, no single defensible source |
| Digital English-learning spend | ~$10–15B/yr | H — analyst-range estimate, uncited |
| Serviceable segment | ~80M | H — top-down guess; T-14 rebuilds by country |
| Beachhead (interview prep) | ~6M | H — derived from the above, not independently measured |
| Model output at M24 | 179k MAU · 11.6k–38.8k paid · $2.0–5.4M ARR | D — `10-financial-model.csv`, base and wedge scenarios |

**Sequencing rationale:** the wedge assumes job seekers convert **2–3×** better than casual learners because the purchase is tied to income and a dated event. That is the plan's central hypothesis (M3), tested by T-01 for $2.5k before launch. Students are cheaper to acquire but monetize later — they are the top of the funnel, not the launch market.

A three-year projection beyond M24 is deliberately **not** given: extrapolating a consumer subscription past the model horizon produces a number nobody can defend, which is how the v1 "$8–20M ARR" line appeared. If the wedge works, the M24 run-rate is the input to a new model, not a slide.

## 5. Personas (summary — full journeys in `04-personas-journeys.md`)

| | **Maya, 19 — Student** | **Daniel, 26 — Job seeker** |
|---|---|---|
| Context | Sophomore, Hanoi; engineering major | Backend dev, São Paulo; applying to remote US roles |
| Level | B1 (IELTS 5.5 target 6.5) | B2 (strong reading, weak speaking) |
| Trigger | Study-abroad application, seminar presentations | Interview scheduled in 3 weeks |
| Pain | Freezes when speaking; no one to practice with; HelloTalk partners disappear | Sounds less competent than he is; loses offers after "tell me about yourself" |
| Budget | $0–5/mo, parent-funded | $20–40 one-time or $15/mo |
| Success | Speaks 3 min without freezing; IELTS speaking 6.5 | Gets through a 45-min interview; receives an offer |
| Primary surface | Phone, 10-min bursts, evenings | Laptop + phone, 30–45 min blocks |

## 6. Experience architecture

```
Onboarding (4 min) → Placement (3 min speaking) → Goal selection
        │
        ▼
   ┌─────────────── Daily Home ───────────────┐
   │  Today's Plan · Streak · Next best action│
   └───────┬──────────────┬──────────────┬─────┘
           ▼              ▼              ▼
     Conversation      Drills         Review Queue
     (scenario/free)  (pronun/vocab)  (SRS + error bank)
           │              │              │
           └──────────► Session Report ◄─┘
                          │
              Corrections · Scores · New words
                          │
                    Progress (CEFR, skills, trends)
```

## 7. Feature specifications

Each spec lists the user-visible behavior, the underlying mechanism, and acceptance criteria (AC). ACs are written to be testable — they are the seed of the QA plan.

---

### 7.1 Conversational AI tutor

**What it is:** a voice-first (with text fallback) tutor that runs scenario-based dialogues and free conversation, adapts difficulty, and returns structured feedback.

**Session types**

| Type | Length | Behavior |
|---|---|---|
| Scenario roleplay | 5–8 min | Tutor plays a role (recruiter, colleague, barista, professor); learner pursues a goal; success criteria at the end |
| Free talk | 5–15 min | Tutor follows learner interests, still tracks errors and vocabulary |
| Drill | 2–4 min | Tight loop on one target: minimal pairs, tense choice, STAR answers |
| Interview sim | 15–30 min | See 7.6 |
| Review conversation | 5 min | Recycles due vocabulary and past errors in natural dialogue |

**Dialogue mechanics**

- **Turn-taking:** push-to-talk default; hands-free mode with VAD-based endpointing (700 ms silence) for Plus. Barge-in supported (learner can interrupt the tutor mid-sentence; tutor stops within 300 ms).
- **Latency budget:** speech-end → first tutor audio ≤ 1.2 s p50, ≤ 2.0 s p95 (see `07-technical.md`).
- **Correction modes:**
  - *Flow* (default for fluency work): no interruptions; corrections collected for the session report.
  - *Coach* (default for interview prep): one micro-correction per turn, max 2 per minute, phrased as a recast ("Nice — you'd usually say *I've been working here since 2021*").
  - *Strict* (exam prep): explicit rule explanation on every error; used sparingly.
- **Adaptive difficulty:** tutor targets a CEFR band (learner's level +0.5). Controls: vocabulary ceiling, sentence length, speech rate (A2: 120 wpm; C1: 165 wpm), idiom density, and scaffolding (does it offer a hint, or wait?). Difficulty adjusts every 3 turns based on learner repair rate and comprehension signals ("sorry?", long pauses, off-topic replies).
- **Scaffolding ladder:** wait → hint in L1 → provide phrase → model the answer → move on. Never leave the learner stuck for more than 12 seconds.
- **Persona consistency:** each scenario has a fixed persona card (role, register, patience, accent). The tutor must not break character to become a cheerleader mid-scenario; praise is delivered at the report stage. This is a deliberate anti-sycophancy choice — constant "Great job!" destroys signal.
- **Goal completion:** every scenario has 2–4 success conditions (e.g., "state your salary expectation," "ask a clarifying question," "close the meeting with next steps"). These are scored, not just tracked.

**Under the hood:** a dialogue policy layer (state machine for scenario beats) wrapped around an LLM. The state machine prevents the classic failure where the model forgets the scenario or skips to the end.

**Acceptance criteria**
- AC1: A learner can complete a full 5-min scenario with no text input and no more than 2 conversational dead-ends.
- AC2: Tutor never claims a grammatically wrong sentence is correct (validated against a 500-item golden set; ≥ 98% pass).
- AC3: Difficulty band is respected: < 5% of tutor turns contain vocabulary above the target band, excluding proper nouns.
- AC4: Session report is available ≤ 5 s after session end, containing ≥ 1 correction, ≥ 1 vocabulary item, and a score.

---

### 7.2 Pronunciation feedback

**The promise:** "Here is the exact sound that is costing you intelligibility, here is what it should sound like, and here is a 90-second drill."

**Scores (0–100 each, plus composite)**

| Dimension | Definition | Signal source |
|---|---|---|
| Accuracy | Share of phonemes produced acceptably | GOP (goodness of pronunciation) from phoneme posteriors + forced alignment |
| Fluency | Pace, pause ratio, filled pauses, self-repairs | Timing from aligned transcript |
| Completeness | Words produced vs. words in target | Alignment coverage |
| Prosody | Stress placement, pitch range, rhythm | F0 contour comparison vs. reference |
| **Speak Score** | Weighted composite, mapped to CEFR-ish band | Calibrated regression |

Weights are level-dependent: at A2, accuracy and completeness dominate; at C1, prosody and fluency dominate. Publishing one fixed weighting would mislead advanced learners.

**Feedback surfaces**

1. **Word heatmap** — transcript colored by score; tap a word to hear the learner's audio vs. a reference model, slowed to 70%.
2. **Phoneme detail** — IPA string with per-phoneme score; for errors, a 3-second mouth-position animation and a minimal-pair contrast ("ship /ʃɪp/ vs. sheep /ʃiːp/").
3. **Pitch contour overlay** — learner's F0 curve against the reference, with stress markers. This is the feature that makes "you sound flat/robotic" actionable.
4. **Targeted drill** — auto-generated 8–12 item drill on the weakest 1–2 phonemes, mixing isolation → word → phrase → sentence.
5. **Progress trend** — per-phoneme improvement over 30/90 days.

**Key design decisions**

- **Intelligibility, not accent.** Scoring targets *canonical* phoneme realization, not a specific native accent. We explicitly allow /æ/–/ɑ/ mergers, rhotic variation, and vowel-space differences that do not impede comprehension.
- **L1-aware calibration.** Error profiles differ systematically (e.g., Mandarin L1: final consonant deletion, /l/–/n/; Spanish L1: /ɪ/–/iː/, initial /s/-clusters; Vietnamese L1: final consonants, consonant clusters). The scorer uses an L1-conditioned threshold so a learner is not penalized for a *shared, comprehensible* variant.
- **Honest uncertainty.** If SNR < 15 dB or the utterance is < 1.5 s, we suppress the score and ask for a re-record. A noisy score is worse than no score.
- **Reference audio is licensed or synthesized.** Never scrape native-speaker audio.

**Acceptance criteria**
- AC1: Correlation with trained human raters ≥ 0.85 (Pearson) on a 600-utterance multilingual test set, cluster-bootstrapped; ≥ 0.75 per L1 subgroup with a best–worst gap ≤ 0.10 (`14`).
- AC2: Test–retest reliability ≥ 0.90 for the same recording scored twice.
- AC3: Score is stable across device microphones (≤ 4 points mean shift between reference headset and a mid-range Android phone).
- AC4: A learner can go from score → drill → re-record in ≤ 3 taps.
- AC5: No score is shown when audio quality is insufficient; the reason is stated plainly.

---

### 7.3 Vocabulary system

**Capture:** long-press any word in a transcript, or say "save that word." Card is created with: the word, the sentence it appeared in, **the learner's own audio of that sentence**, a plain-English definition, an L1 gloss (optional), collocations, and a CEFR/frequency tag.

The learner's own audio is the differentiator: it makes the card *theirs* and doubles as a pronunciation artifact.

**Review engine:** FSRS (Free Spaced Repetition Scheduler) rather than SM-2 — better retention per review at the same workload. Target retention 0.90; 4-grade recall; daily cap 20 (free) / 60 (Plus); interleaved by default, with "cram" mode before an interview.

**Card types:** recognition (see → meaning), production (meaning → say it out loud, scored), cloze in context, and collocation gap-fill. Production cards are the ones that transfer to speech, so ≥ 40% of reviews must be production.

**Packs**

| Pack | Contents | Audience |
|---|---|---|
| Core 2k | NGSL-based high-frequency base | Everyone (free) |
| Interview | 400 items: achievements, ownership, ambiguity, failure, salary, small talk | Job seekers |
| Business | Meetings, negotiation, email, presentations, disagreement | Professionals |
| Tech | Standups, code review, incident response, system design | Engineers |
| Healthcare | Patient intake, handoff, empathy phrases, plain-language explanation | Nurses, med students |
| Campus | Seminars, group projects, office hours, dorm life | Students |

**Coverage model:** the app shows "you recognize 84% of the words in this article/interview description." This makes vocabulary progress tangible and drives pack purchases.

**Acceptance criteria**
- AC1: Capture-to-card ≤ 2 s, works offline, syncs later without duplicates.
- AC2: 30-day retention of captured words ≥ 85% at target workload (measured in-product).
- AC3: Every pack item has audio, an example in a realistic sentence, and an L1 gloss for all 6 supported L1s.
- AC4: A learner can complete a 10-card review in ≤ 3 minutes.

---

### 7.4 Daily exercises and accountability

**Today's Plan** is a single card stack, 8–12 minutes total:

1. 60-second warm-up (shadowing or minimal pair)
2. Vocabulary review (due cards, capped)
3. One micro-scenario (2–4 min, voice)
4. One listening or comprehension item (60–90 s)
5. Optional: "fix yesterday's top error" (30 s)

**Streaks — designed not to punish.** Daily streak plus a weekly goal (e.g., 4 sessions/week). Two *streak freezes* per month, auto-applied, plus a "repair" option for 24 hours after a break. Rationale: Duolingo-style hard streaks maximize daily opens but cause total abandonment after the first miss; for a paid product, week-4 retention matters more than day-2 vanity.

**Review queue priority order:** (1) overdue SRS cards, (2) errors seen ≥ 2 times in the last 14 days, (3) weakest phoneme drill, (4) new material.

**Notifications:** max 1/day, time-zone aware, content-bearing ("Your /θ/ score dropped 12 points — 90-second drill?"). Never guilt-based.

**Acceptance criteria**
- AC1: Plan is generated in < 500 ms and is different each day but stable if reopened.
- AC2: A learner who misses 3 days sees a re-entry flow (not a broken streak wall) and can restart in one tap.
- AC3: Notification opt-out rate < 15% in the first 30 days.

---

### 7.5 Progress analytics

**CEFR estimate** from four signals: lexical/syntactic complexity of produced speech, task success on level-appropriate scenarios, pronunciation composite, and comprehension accuracy. Displayed with a confidence band ("B1+ · likely B1–B2") and a disclaimer that it is an estimate, not a certification.

**Skill breakdown:** Speaking, Listening, Reading (from chat/text and exercise items), Writing (chat), plus two job-relevant indices:
- **Interview Readiness Index (0–100):** structure, relevance, fluency, pronunciation, register.
- **Workplace Communication Index:** clarity, politeness/register, turn-taking, comprehension under speed.

**Weekly Report Card:** a shareable card with 3 numbers (speaking minutes, score delta, words mastered), one "win," one "focus," and next week's plan. This is the retention and acquisition artifact — shareable cards are the cheapest organic channel we have.

**Milestones:** CEFR can-do statements, not arbitrary badges ("I can describe my work experience in 2 minutes without notes"). Badges exist but are tied to real behaviors.

**Acceptance criteria**
- AC1: CEFR estimate agrees with certified examiner ratings at quadratic weighted κ ≥ 0.70.
- AC2: Every score on screen is traceable to evidence (tap → the utterance that produced it).
- AC3: Report card renders in < 1 s and is shareable as an image without exposing audio or personal data.

---

### 7.6 Interview simulator (differentiator)

**Flow:** paste job description (or pick a role template) → choose interview type (behavioral, technical, case, HR screen) → 20–30 min simulated interview with 6–10 questions, follow-ups, and interruptions → rubric-scored report → targeted 7-day prep plan.

**What makes it credible**

- **Follow-up probing.** Real interviewers dig. The simulator must ask "What was *your* specific contribution?" and "What would you do differently?" — this is where LLM interview tools usually collapse into a list of pre-written questions.
- **STAR structure coaching.** Detects missing Situation/Task/Action/Result and asks for the missing element in real time.
- **Pressure mode.** Interruptions, skeptical tone, time pressure, one deliberately hostile question ("Why should we hire you over someone with more experience?"). Explicitly opt-in.
- **Delivery analysis.** Filler-word rate, pace, pause distribution, hedging language ("I think maybe sort of"), uptalk, and — on desktop only, with consent — eye contact and posture from the webcam. **All video processing on-device; no frames uploaded.**
- **Rubric scoring** with evidence quotes, not vibes: each score links to the exact utterance.
- **Company/role packs** for common hiring loops (Big Tech behavioral, consulting case, healthcare residency, customer support).

**Acceptance criteria**
- AC1: 80% of users report the questions were "similar to or harder than" their real interview (post-session survey).
- AC2: Report identifies ≥ 1 structural weakness and ≥ 1 language weakness with quoted evidence in 100% of sessions.
- AC3: A 30-min session costs ≤ $0.35 in inference (see cost model).
- AC4: Video never leaves the device; verifiable in the privacy center.

---

### 7.7 Community layer (Phase 3 — deliberately gated)

HelloTalk's social pull is real: learners want belonging and real humans. We capture that without importing the failure modes.

**Design**

- **Practice Pods:** scheduled 25-min group sessions, 4–6 learners at similar CEFR, one AI facilitator. The AI runs the agenda, pairs learners, and produces a shared correction summary afterward. Because the AI carries the pedagogy, a weak human partner no longer ruins the session.
- **No 1:1 stranger DMs at launch.** Pods only. This removes the entire harassment/grooming surface that plagues exchange apps.
- **Moderated voice rooms** with automated + human moderation, recording consent, and a one-tap report that attaches the audio buffer.
- **Minors (16–17):** pods only, age-banded, no profile discovery, guardian consent, no direct contact of any kind. This is non-negotiable and will cost us growth — that is the point.
- **Reputation:** contribution-based ("gave 12 useful corrections"), not follower counts.

**Why it is Phase 3 and not Phase 1:** community requires trust & safety staffing, moderation infrastructure, and a critical mass of same-level users. Launching it early would recreate HelloTalk's core weakness while adding legal risk.

---

### 7.8 Non-goals (v1)

| Non-goal | Why |
|---|---|
| 100+ languages | English-only focus is the entire quality advantage |
| Social feed / Moments | High moderation cost, low learning value |
| AI "companion" persona / emotional dependency design | Ethically fraught; attracts the wrong retention and press |
| Certification (replacing IELTS/TOEFL) | We estimate and prepare; we do not certify. Partner instead |
| Human tutor marketplace at launch | Operational complexity; AI-first, human later for high-value review |
| Desktop-first product | Learners practice on phones; desktop exists for interviews only |

## 8. Content strategy

- **Scenario library:** 12 at MVP, 24 at public launch (M6), 60 by M12, 150 by M18. Each scenario = persona card, 2–4 success conditions, target vocabulary, 3 difficulty variants, and a rubric.
- **Authoring pipeline:** in-house pedagogy lead writes specs → LLM drafts variants → human review → automated eval (level appropriateness, safety, factual accuracy) → playtest with 5 learners.
- **L1 support:** UI + hints + glosses in 6 languages at launch; voice tutor is English-only (deliberate — the tutor should not switch to L1 except for a single-word hint).
- **Accent coverage in TTS:** at least 5 tutor voices (US, UK, Indian, Australian, neutral) so learners are not trained on one accent. Interview sim defaults to the target company's region.

## 9. Accessibility and inclusion

- Full captions on all tutor audio; adjustable playback speed 0.7–1.2×.
- Dyslexia-friendly font option; high-contrast mode.
- Works one-handed, on 4-year-old Android devices, at 3G speeds.
- Low-data mode: audio-only, 16 kHz capture, no video.
- No score shaming: never compare a learner to other learners; only to their past self.

## 10. Definition of done for the product

A feature ships when: acceptance criteria pass, it is instrumented, it has a documented failure mode, it works on the bottom-quartile device, and a first-time user can discover it without a tooltip tour.
