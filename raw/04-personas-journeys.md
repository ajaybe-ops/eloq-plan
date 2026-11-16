# 04 — Personas and User Journeys

**Version:** 2.0 · 2026-11-15

**What changed in this revision:** all price references updated to $12.99 Plus / $24.99 Career / $49.99 student annual; the human-reviewed mock is a $49 add-on rather than an included monthly entitlement; the paywall moments now reference the 3-day Career trial that T-04 actually tests. Personas and journey structure are unchanged.

## 1. Primary personas

### Persona A — "Maya," 19, university student

| Attribute | Detail |
|---|---|
| Where | Hanoi, Vietnam (also representative of Jakarta, Bangkok, Cairo, Mexico City) |
| Study | 2nd-year Business Administration |
| English | B1 — reads well, writes okay, freezes when speaking; IELTS 5.5, target 6.5 |
| Device | Mid-range Android, 4G, 6 GB data/month, shares a room |
| Money | $0–5/mo of her own; parents fund education purchases |
| Goal | Exchange semester in Australia in 14 months; then a regional graduate job |
| Trigger events | Seminar presentation in 3 weeks; IELTS in 5 months |
| What she has tried | Duolingo (streak died), HelloTalk (two partners ghosted; one asked for photos), YouTube shadowing (no feedback) |
| Real fear | Being laughed at; sounding stupid in front of classmates |
| What would make her pay | Visible improvement before a high-stakes moment; a parent-approved annual price |

**Jobs to be done**
- *Functional:* "Help me speak for 3 minutes without freezing."
- *Social:* "Don't let me embarrass myself in the seminar / the interview."
- *Emotional:* "Let me practice without anyone watching me fail."

**Success definition:** completes a 3-minute presentation scenario with a Speak Score ≥ 70 and no more than 2 long pauses; IELTS speaking mock ≥ 6.0.

---

### Persona B — "Daniel," 26, job seeker

| Attribute | Detail |
|---|---|
| Where | São Paulo, Brazil (representative of Lagos, Bengaluru, Manila, Warsaw, Cairo) |
| Work | Backend developer, 4 years, Python/Go |
| English | B2 — strong reading, decent writing, weak spontaneous speech; heavy L1 interference (/ɪ/–/iː/, th-stopping, final clusters) |
| Device | Personal laptop + Android phone; stable wifi at home |
| Money | $15–40/mo; will pay for anything that plausibly converts to a $40k+ salary jump |
| Goal | Remote role at a US/EU company; has failed 3 final rounds |
| Trigger event | Recruiter screen scheduled in 3 weeks |
| What he has tried | HelloTalk (scheduling hell), Cambly ($14/hr, cancelled after 3 sessions), ChatGPT voice (useful but unfocused), YouTube "tell me about yourself" videos |
| Real fear | Sounding less competent than he is; being filtered out for language, not skill |
| What would make him pay | A concrete, role-specific rehearsal with a score he can act on; a human-reviewed mock as the premium anchor |

**Jobs to be done**
- *Functional:* "Get me through a 45-minute English interview without losing the thread."
- *Social:* "Make me sound credible to a hiring manager."
- *Emotional:* "Give me a reason to believe I won't freeze this time."

**Success definition:** completes 10 simulated interviews, Interview Readiness Index ≥ 75, reports at least one real interview passed to the next stage.

---

### Anti-personas (explicitly not served in year 1)

| Anti-persona | Why not |
|---|---|
| Absolute beginners (A0–A1) | Voice-first conversation is the wrong pedagogy; needs grammar foundations and L1 instruction |
| Casual hobby learners | Low intent, low willingness to pay, high churn; they are Duolingo's customer |
| People seeking friendship/dating | We are not a social product; serving them would corrupt the design |
| Under-16 | Voice AI + minors is a compliance burden we are not staffed for at launch |
| Native-speaker accent polishing (C2) | Small market; our scoring is calibrated for intelligibility up to C1 |

## 2. Journey A — Maya (student)

| Stage | What she does | What she thinks / feels | Friction | Product opportunity |
|---|---|---|---|---|
| **Trigger** | Professor announces a graded 5-min presentation in English | "I'm going to die." Anxiety, avoidance | Doesn't know where to start | Search intent: "presentation English practice" → land on a scenario page |
| **Discovery** | Sees a TikTok: someone's pronunciation before/after, 30 seconds, no fluff | "Wait, it tells you *which sound*?" Curiosity | Sceptical of another app | Short-form must show the score screen, not a talking head |
| **Install** | Downloads; opens at 10 p.m. in her dorm | Hopeful, self-conscious | Will abandon at any friction; roommates nearby | "Silent mode" onboarding: all audio through headphones, no speaker output |
| **Onboarding (4 min)** | Picks goal "presentation / study abroad," takes 3-min placement | Nervous about being judged | Placement feels like a test | Frame as calibration: "There's no score to fail. We're finding your starting line." |
| **First value (minute 5)** | Does a 3-min "Introduce yourself to a class" scenario; gets 2 corrections and a heatmap | Surprise: "It heard that?" | First correction must be *right* | Show one correction she recognizes as real; do not show 12 at once |
| **Day 2–3** | Daily Plan, 9 min, streak starts | Mild motivation | Novelty fades | Report Card preview: "2 more sessions to unlock your first trend line" |
| **Week 1** | 5 sessions; saves 14 words; score 58 → 63 | "Maybe this works." | Life intervenes; misses 2 days | Streak repair + re-entry flow, no shame screen |
| **Week 2–4** | Presentation scenario × 6, pressure mode on | Confidence rising; still afraid of the real room | Scenario gets stale | Branching variants (hostile Q&A, time cut in half, slides fail) |
| **Paywall moment** | Uses her third free session of the week on day 6, mid-scenario | Frustrated | Interrupting a session to sell is hostile | Cap applies at the next natural boundary; offer "finish this session free, then choose" |
| **Conversion** | Asks parents; annual at student price | Price-sensitive, needs justification | Card access, currency | Local payment methods (MoMo, Pix, UPI, GCash), student annual $49.99 |
| **Habit (month 2–3)** | 4 sessions/week; IELTS speaking mock | Pride; shares report card in group chat | Boredom risk | Can-do milestones, new scenario drops, weekly focus |
| **Outcome** | Presentation goes well; IELTS speaking 6.0 | "I can do this." | — | Ask for outcome + testimonial; graduate to IELTS track |
| **Churn risk** | Exam ends → goal achieved → cancels | "I don't need this now" | Seasonal | Pause instead of cancel; "next goal" prompt (exchange application, internship) |

**Design implications for Maya**
1. Never require her to speak aloud in public — headphone-first, whisper mode.
2. One correction at a time in the first session; save the full report for later.
3. Make progress visible by day 7, or she will not return.
4. Price in local currency with local payment rails; offer student annual.
5. Celebrate *can-do* moments ("you spoke for 3 minutes"), not points.

## 3. Journey B — Daniel (job seeker)

| Stage | What he does | What he thinks / feels | Friction | Product opportunity |
|---|---|---|---|---|
| **Trigger** | Recruiter emails: screen on Thursday, 3 weeks out | Panic + urgency | Doesn't know what they'll ask | "I have an interview" is the single best onboarding entry point |
| **Discovery** | Googles "practice English job interview"; finds the comparison page and an interview-question library | "This is exactly my problem." | Distrust of AI feedback | Show a sample report card with quoted evidence, above the fold |
| **Onboarding (5 min)** | Pastes the job description; picks "backend engineer, US startup"; 3-min placement | Impatient, wants value now | Long onboarding is fatal for him | JD → role detection → skip generic setup; placement can be deferred to after first session |
| **First value (minute 6)** | 12-min simulated screen: "Tell me about yourself" + 3 follow-ups | Uncomfortable — the follow-ups are better than expected | AI might be too soft | Follow-up probing is the "oh, this is real" moment. Make it question #2 |
| **Report** | Sees structure score, filler-word count, 2 quoted weak answers, pronunciation top-3 | "This is more specific than my $14/hr tutor." | Report too long | 3 numbers, 2 fixes, 1 plan — collapsing detail behind "see all" |
| **Day 2** | 7-day prep plan; drills his top 2 phonemes; rewrites STAR stories | Focused, slightly overwhelmed | Generic advice | Plan is tied to *his* JD and *his* last answers |
| **Week 1** | 4 sessions, 2 full mocks; Index 54 → 63 | "I might actually be okay." | Time pressure | Countdown mode: "11 days, 6 sessions to target" |
| **Paywall moment** | Second mock hits the free cap; wants the full 30-min technical round | Ready to pay | Must not lose progress | Career trial: 3 days free, full sim, cancel anytime |
| **Conversion** | Buys Career annual ($149.99) or monthly ($24.99) | Rational: one offer is worth 100× the price | Card friction in BR | Pix / boleto, USD + local currency display |
| **Week 2–3** | Pressure mode, hostile questions, salary negotiation drill | Nervous but rehearsed | Over-practicing scripted answers | Randomize follow-ups; "no two sessions the same" |
| **Interview day** | 15-min warm-up scenario in the morning | Calm | Last-minute panic | "Morning warm-up" one-tap flow |
| **After** | Reports outcome in-app | Relief or disappointment | No feedback loop | 60-second outcome survey; if rejected, auto-generate a targeted post-mortem plan |
| **Expansion** | Refers a friend; buys Business English pack for the new job | "I want to keep this." | Churn after getting the job | Reposition: onboarding at work, meetings, small talk → Business tier |
| **Churn risk** | Gets the offer → "done" | Goal achieved | 60–70% will churn | "First 90 days at work" track; annual retention play |

**Design implications for Daniel**
1. Interview date in onboarding turns a nice-to-have into a countdown.
2. Follow-up questions, not question lists, are the credibility test.
3. Quotes from his own answers beat generic advice.
4. He will pay — but only after the free mock proves it is better than ChatGPT.
5. Post-offer retention is a product problem (workplace track), not a discount problem.

## 4. First-session script (both personas)

The first 6 minutes decide the business. Target: **first meaningful correction by 3:30, first score by 4:30, session complete by 6:00.**

| Time | Screen / event | Design intent |
|---|---|---|
| 0:00 | "What are you getting ready for?" → 4 options (Interview · Presentation · Everyday speaking · Study abroad) | Goal before signup; personalizes everything |
| 0:20 | "When is it?" → date picker or "no date" | Enables countdown; no penalty for skipping |
| 0:40 | Mic check with a fun sentence ("The weather is weird today") | Tests audio, sets tone, no evaluation yet |
| 1:00 | 20-second calibration read (for pronunciation baseline) | Framed as "finding your starting line" |
| 1:30 | "Pick a scenario" → 3 recommended, all under 5 min | Choice, but curated — not a library |
| 2:00 | Scenario starts; tutor greets in role | Immediate immersion, no tutorial |
| 3:30 | First correction (Coach mode), one sentence, plain language | The "it noticed" moment |
| 4:30 | Session ends with a score + one win + one focus | Reward before cost |
| 5:00 | "Save these 3 words?" → one tap | Vocabulary capture without a form |
| 5:30 | "Tomorrow: 9 minutes. Same time?" → notification opt-in | Commitment device at peak satisfaction |
| 6:00 | Home screen with streak = 1, plan preview | Clear next action |

**Failure modes to design out**
- No correction in the first session → user concludes it is a chatbot. *Hard requirement: at least one correction before minute 4.*
- Score shown without explanation → user distrusts it. *Every score has a one-line "what this means."*
- Too many corrections → user feels attacked. *Max 3 in session one, max 2 per minute thereafter.*
- Empty home screen → uninstall. *Tomorrow's plan is pre-populated before the session ends.*

## 5. Paywall moments (and the rules around them)

| Moment | Trigger | Offer | Rule |
|---|---|---|---|
| **Cap hit mid-flow** | Daily voice minutes exhausted | "Finish this session free — then 7 days of Plus for $1" | Never cut a session mid-sentence; the cap applies at the next natural boundary |
| **Trend locked** | Taps a 30-day trend | Plus unlocks history + per-phoneme analytics | Show a blurred preview with real numbers — not a generic upsell |
| **Mock interview** | Wants a full 30-min sim | Career trial (3 days) | Full sim must be experienced before asking for money |
| **Plan generation** | Sets an interview date in < 21 days | Career: "11-day prep plan" | Urgency is genuine, not manufactured |
| **Pack** | Repeated errors in a domain (e.g., salary negotiation) | Interview Pack $29 | Only offered after the need is demonstrated |
| **Student annual** | Verified .edu / student ID | $49.99/yr | Verification must not block the flow |

**Anti-patterns we will not use:** fake countdown timers, "3 people are viewing this," paywalling corrections, paywalling the delete-my-data flow, and interrupting the first session.

## 6. Churn and win-back

| Churn type | Signal | Counter |
|---|---|---|
| **Goal achieved** | Interview date passed; no sessions for 10 days | "First 90 days at work" track; pause instead of cancel |
| **Streak break** | 4+ days inactive after a miss | Repair offer + "restart with a 3-minute session" |
| **Plateau** | Score flat 3 weeks | New scenario type + explicit "plateau is normal" framing + harder variant |
| **Price** | Visits pricing page 2× without converting | Local pricing, student tier, annual downgrade |
| **Frustration** | "This correction is wrong" ×2 | Human review of the sample; correction-quality follow-up |
| **Technical** | Repeated failed sessions, high latency | Device diagnostics; audio-only mode; support outreach |

Win-back messages must contain a *number that changed*, not sentiment: "Your fluency score went up 6 points while you were away — your next drill is ready."

## 7. Edge cases and accessibility journeys

| Case | Design response |
|---|---|
| **Shared / family device** | Profiles with separate PINs; no audio autoplay; delete-by-profile |
| **Noisy environment** | "Quiet mode": whisper-level drills with noise-robust ASR; suggest text mode |
| **No credit card** | Carrier billing, Pix, UPI, MoMo, gift cards, bank transfer for annual |
| **Low bandwidth** | Audio-only at 16 kHz, 24 kbps; pre-downloaded drills; resume after drop |
| **Minor (16–17)** | Guardian consent, pods only, no profile discovery, stricter moderation, no purchase without guardian |
| **Learner with speech difference** | Explicit "adjust scoring for my speech" setting; scoring recalibrated, never framed as a deficit |
| **Interview in 6 hours** | "Emergency mode": 20-min targeted drill on self-introduction + 3 likely questions |
| **VPN / region mismatch** | Price shown in billing country, not IP; no dark-pattern geo-arbitrage |
