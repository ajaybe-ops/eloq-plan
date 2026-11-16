# 05 — Pricing and Monetization

**Version:** 2.0 · 2026-11-15

**What changed in this revision:**
1. **Plus moved $9.99 → $12.99/mo, $69.99 → $79.99/yr** — exact parity with HelloTalk VIP (verified $12.99/$79.99, S2). **Career moved $19.99 → $24.99/mo, $149 → $149.99/yr.**
2. **Voice COGS corrected from $0.051 to $0.018 per session minute.** v1 charged a full minute of ASR *and* a full minute of TTS for every minute of conversation. Duty cycles are ~55% learner speech / ~45% tutor speech. The old number overstated cost by ~2.2×, which made the whole pricing section pessimistic in the wrong direction.
3. **Conversion replaced** by benchmarked D35 scenarios (1.8% / 2.6% / 6.0%) instead of "5–8% of MAU." Break-even is **≈4.5%**.
4. **Churn moved 5.5% → 8%/month**, consistent with AI-app churn penalties and Education-category realized LTV.
5. **Human-reviewed mock moved from 1/month to 1 per 90-day interview cycle** — at $24.99, a monthly human review is a structural loss.

Every number here reconciles to `10-financial-model.csv`. If prose and model disagree, the model wins.

---

## 1. The pricing problem, stated honestly

Voice AI is expensive per minute in a way text AI is not — but less expensive than v1 believed. At the corrected launch cost of **$0.018 per learner session minute**:

| Line item | Usage | Monthly COGS |
|---|---|---|
| Free user, allowance fully used (60 min) | 60 min × $0.018 | $1.08 |
| Free user, average utilisation (20 min) | 20 min × $0.018 | $0.36 |
| Plus, median (300 min) | 300 × $0.018 | $5.40 |
| Plus, at fair-use ceiling (600 min) | 600 × $0.018 | $10.80 |
| Career, median (400 min) | 400 × $0.018 | $7.20 |
| Human-reviewed mock (add-on) | 45-min review, ~$18 cost | sold at $49 |

At $12.99/month (≈$7.82 net of the 15% store fee, blended across annual/monthly), a median Plus user is **+31% gross margin at launch** and +62% after optimization. That is a viable business on the paid side. It was not true at v1's $0.051 assumption, and the correction matters: it means the constraint is **conversion**, not COGS.

**The pricing rule is unchanged:** *give away unlimited cheap practice, meter the expensive practice, never meter the feedback.* Drills, SRS, text chat, and corrections cost cents per month. Real-time voice is the scarce resource. Metering voice while keeping feedback free means the free tier still teaches — it just talks less.

---

## 2. Tiers

| | **Free** | **Plus** | **Career** |
|---|---|---|---|
| Price (US) | $0 | **$12.99/mo · $79.99/yr** | **$24.99/mo · $149.99/yr** |
| Annual effective | — | $6.67/mo (49% off monthly) | $12.50/mo (50% off monthly) |
| Voice conversations | 3/week, ≤ 5 min each | Unlimited, fair use 20 min/day (median use ~10) | Unlimited, fair use 30 min/day (median ~13) |
| Text chat with tutor | Unlimited (fair use) | Unlimited | Unlimited |
| Scenarios | 12 core | All (12 at launch → 60+ by M12) | All + interview library |
| Corrections + explanations | ✅ (never metered) | ✅ | ✅ |
| Pronunciation score | Word-level | Full: phoneme, prosody, trends | Full + delivery analysis |
| Pronunciation drills | ✅ unlimited | ✅ + adaptive programs | ✅ |
| Vocabulary (SRS) | 20 reviews/day · Core 2k | 60/day · all base packs | Unlimited · all packs |
| Daily Plan | ✅ | ✅ + personalized study plan | ✅ + deadline countdown plan |
| Progress analytics | 7-day history, CEFR estimate | Full history, per-skill, per-phoneme | + Interview Readiness Index |
| Weekly Report Card | Basic | Full + shareable | Full + shareable |
| Interview simulator (AI) | 1 taster (10 min) | 2/month | Unlimited + pressure mode + JD tailoring |
| Human-reviewed mock | — | — | **$49 add-on** (45-min review, 48-h turnaround) |
| Offline mode | — | ✅ | ✅ |
| Video delivery analysis | — | — | ✅ (on-device) |
| Support | Community | Email, 48 h | Priority, 12 h |
| Multiple profiles | 1 | 1 | 3 (e.g., shared device) |

**One-time packs** (available to any tier; subscribers get 20% off)

| Pack | Price | Contents |
|---|---|---|
| Interview Sprint (21 days) | $29 | 21 guided sessions, 6 AI mocks, STAR drills, salary negotiation, 400-word interview lexicon |
| Business English | $39 | Meetings, email, presentations, disagreement, small talk, 500 words |
| Tech English | $29 | Standups, code review, incident calls, system design narration |
| Healthcare Communication | $49 | Patient intake, handoff, empathy, plain-language explanation (reviewed by clinicians) |
| Campus & Study Abroad | $19 | Seminars, group projects, office hours, dorm life |

**Institutional**

| Plan | Price | Includes |
|---|---|---|
| Campus Career Center | $7–9/seat/mo (min 150 seats) | Cohort dashboard, assignment of interview tracks, aggregate outcomes, SSO, no individual audio access |
| Bootcamp / Staffing | $12–18/seat/mo | White-label option, placement-rate reporting, API |

Model ACV for a 200-seat career center at $7/seat: **$16.8k/yr**. That is the B2B line in `10`, and it is a hypothesis (three pilots, no signed contracts).

---

## 3. Why these prices and these limits

**Price parity with HelloTalk is the point.** At $12.99/$79.99, the comparison stops being "cheaper, probably worse" and becomes "same price, and it answers at 2 a.m." A lower price would also signal a smaller product and leave COGS headroom thin at the 600-minute ceiling. Parity is the strongest available anchor, and it is verified rather than assumed.

**Freemium, not a free trial — but that is now a tested assumption, not a belief.** The 7-day-trial critique still stands (spike, cliff, and 55% of 3-day trial cancellations happen on day 0 per RevenueCat). But RevenueCat also shows hard paywalls converting at 10.7% D35 vs 2.1% for freemium. That gap is large enough that we test the reverse trial (T-04) instead of assuming our way past it. The free tier ships; the trial is measured against it.

**Free voice stays at 3 × 5 minutes/week.** It is enough to prove the product and feel the constraint, and average utilisation (~20 min/MAU) keeps free COGS at ~$0.26/MAU/month against ~$0.81 revenue per free MAU at M12 (base). At 60 minutes of *utilisation* the free tier goes underwater below ~4% conversion — see `13` D1 for the flip condition.

**Unlimited text chat on Free** is deliberate. Text is cheap, it teaches, and it gives the free user a reason to open the app on the three days they cannot speak. It also supplies the writing signal for the CEFR estimate.

**Corrections are never metered.** Charging for feedback would make the free tier a demo rather than a tool, and it would communicate that the core value is a commodity. The free tier's job is to make the learner *trust the feedback*; the paid tier's job is to give them *more reps*.

**Career at $24.99** is anchored against a human interview coach ($100–300 per mock), not against HelloTalk. It is priced *above* Plus because it sells a different unit: readiness for a dated event. It sits above ELSA's $19.99/mo (verified, S5), which is deliberate — we are not claiming to be the cheaper pronunciation app, we are claiming to be the interview-outcome product.

**Fair use, not "unlimited."** All paid voice plans carry a published ceiling (20/30 min per day) with graceful degradation — a warning at 80%, then a switch to text + drills for the rest of the day, never a hard lock mid-conversation. This protects margin from the 2% of users who would otherwise consume 10× the median. At the ceiling, Plus is margin-negative at launch ($10.80 COGS vs $7.82 net revenue) and only breaks even after cost optimization — which is exactly why the ceiling exists and why it is enforced.

**Packs exist because content has a shelf life and a buyer.** A learner preparing for a specific interview will pay $29 once; they will not pay $24.99/month for a year. Packs convert the deadline-driven segment without polluting the subscription, and they carry ~91% margin at launch (~95% after cost optimization — see §4.2).

**The human mock is a $49 add-on, not a subscription entitlement.** A 45-minute human review costs ~$18 fully loaded. At $24.99/month (≈$14.87 net), one per month would consume more than the entire net revenue of the plan; one per 90-day cycle would still cost ~$6/month, or 40% of Career revenue. The add-on preserves the trust anchor at a 63% margin, and it is still one-sixth of what a human interview coach charges. Bundling it would have been the same class of error as v1's COGS: a number that looks generous until it is multiplied by the user base.

---

## 4. Unit economics

### 4.1 Cost per learner session minute

A "session minute" is a minute of conversation, not a minute of audio. In a real exchange the learner speaks ~55% of the time and the tutor ~45%. v1 priced both at 100% duty — the single largest error in the first version of this plan.

| Component | Launch (M1) | Optimized (M13) | Lever |
|---|---|---|---|
| Streaming ASR (55% duty) | $0.0026 | $0.0020 | Shorter-turn model, on-device VAD, no re-transcription |
| TTS (~45% duty, blended Aura-1/2) | $0.0081 | $0.0040 | Phrase caching, streaming, cheaper voice for drills, barge-in cut-off |
| LLM (dialogue + scoring prompts) | $0.0050 | $0.0025 | Model routing, prompt caching, capped context, 1–2 sentence turns |
| Pronunciation scoring (licensed) | $0.0020 | $0.0012 | Batch/async, on-device for drills, renegotiated rate |
| Transport, storage, infra | $0.0003 | $0.0003 | Compression, 30-day retention |
| **Total** | **$0.0180** | **$0.0100** | |

Vendor basis: Deepgram streaming ASR $0.0048/min (Nova-3); TTS $0.015/1k chars (Aura-1) to $0.030/1k (Aura-2); ElevenLabs Business ≈$0.165/1k chars quoted as a premium alternative (`09` K1–K2). LLM and scoring are hypotheses until T-11 reconciles an invoice.

### 4.2 Per-user monthly economics

Net revenue is after the 15% store commission (Apple Small Business Program / Google first $1M), blended at a 60% annual-plan mix.

| Segment | Minutes/mo | Voice COGS launch → optimized | Net revenue | Gross margin launch → optimized |
|---|---|---|---|---|
| Free (allowance used) | 60 | $1.08 → $0.60 | $0 | Subsidized |
| Free (average utilisation) | 20 | $0.36 → $0.20 | $0 | Subsidized; covered by paid mix |
| **Plus, median** | 300 | $5.40 → $3.00 | **$7.82** | **31% → 62%** |
| Plus, at ceiling | 600 | $10.80 → $6.00 | $7.82 | **−38% → 23%** |
| **Career, median** | 400 | $7.20 → $4.00 | **$14.87** | **52% → 73%** |
| Human mock add-on (one-off) | 45-min review | $18.00 | $41.65 (net of fee) | **57%** |
| Pack (one-time, ~120 min) | 120 | $2.16 → $1.20 | $24.65 (net) | **91% → 95%** |

**What this table says**

1. The paid business works at launch on median usage. It did not at v1's COGS — that was a modelling error, not a strategic finding.
2. **Heavy users are the risk.** At the fair-use ceiling, Plus is negative before optimization. Enforcement of the ceiling and a design that makes a 7-minute focused session feel complete are therefore revenue features, not nanny features.
3. **Career carries the margin**, which is why the wedge matters financially and not just strategically.
4. **Human review is a product, not a perk.** Selling it at $49 keeps a 57% margin; bundling it would have cut Career margin from 52% to 11% at launch.

### 4.3 What would change if human review were included

Including one human review per 90-day cycle would add ~$6/user/month to Career COGS: Career margin falls from 52% to 11% at launch (73% to 33% optimized), and at M24 scale it would remove roughly $32k/month of gross profit, taking blended gross margin from 56.8% to ~42%. The model excludes it deliberately and `10` §8 discloses the omission. If a future test shows the add-on suppresses Career conversion, the correct fix is a higher Career price — not a free review.

---

## 5. Funnel, conversion, and LTV

| Step | Value | Status |
|---|---|---|
| Install → registered | 65% | H (own beta; industry 55–70%) |
| Registered → activated (1 session + 1 correction + 5 reviews) | 45% | H (MVP target) |
| Install → paywall view, within 35 days | 27% | H |
| **Implied paywall view → paid** | **downside 6.7% · base 9.6% · wedge 22%** | D from D35 ÷ paywall reach |
| **D35 install → paid** | **1.8% / 2.6% / 6.0%** | V benchmark (S10) for base; hypothesis for wedge |
| Paid mix Plus : Career | 90 : 10 at M1 → 68 : 32 by M12 | H |
| Blended ARPU (net, M24) | $14.32 / $13.09 / $11.52 | D from model |
| Monthly paid churn | 8% | H (M5) |
| **LTV (ARPU × 57% GM ÷ 8%)** | **$102 / $93 / $82** | D |
| **Blended CAC (M1–M12)** | **$42.23 / $29.24 / $12.67** | H (T-03) |
| **LTV : CAC** | **2.4 / 3.2 / 6.5** | D |
| **CAC payback** | **5.2 / 3.9 / 1.9 months** | D |

**The number to put on the wall: break-even D35 conversion is ≈4.5%.** That is roughly twice the North America category median and just above the top quartile. The plan does not have a comfortable base case; it has a thesis that job seekers convert at 2–3× category rates because they have a deadline and an income-linked payoff.

**Why the wedge conversion is plausible but not assumed:** at 6% D35, the implied paywall conversion is ~22%. That is high for cold traffic and normal for high-intent interview traffic — which is precisely the bet. T-01 (segment CPA) and T-05 (Career price at a fake door) test it for ~$3.5k before launch.

**Sensitivity (one input at a time):**

| Change | Effect |
|---|---|
| Churn 8% → 5% | LTV $93 → $149; LTV:CAC 3.2 → 5.1 |
| Churn 8% → 12% | LTV $93 → $62; LTV:CAC 3.2 → 2.1 |
| CAC $29 → $60 | LTV:CAC 3.2 → 1.6 — paid acquisition stops working |
| D35 2.6% → 4.0% | ARR M24 ≈ $3.6M; cash-out moves past M24 |
| Plus price $12.99 → $9.99 | Plus margin 31% → 10% at launch; the model inverts |

The asymmetry is the argument for parity pricing: at $9.99 the paid product is barely above water on median usage, and a single cost-optimization slip makes it negative.

---

## 6. Regional pricing

Purchasing-power tiers, applied by **billing country**, not IP:

| Tier | Example markets | Plus | Career | Student annual |
|---|---|---|---|---|
| A | US, UK, DE, AU, JP, KR | $12.99 / $79.99 | $24.99 / $149.99 | $49.99 |
| B | BR, MX, PL, TR, ZA, MY | $8.99 / $54.99 | $17.99 / $99.99 | $34.99 |
| C | VN, IN, ID, PH, NG, EG | $5.99 / $39.99 | $11.99 / $69.99 | $24.99 |

Rules: local currency display, local payment rails (Pix, UPI, MoMo, GCash, boleto, carrier billing), no geo-arbitrage enforcement beyond billing address, and identical features across tiers — price discrimination on ability to pay, never on learning quality.

Note the COGS implication: a Tier-C Plus user at $5.99 gross (~$3.60 net after a 40% regional fee assumption, which varies) with 300 minutes costs $5.40 at launch. **Tier C is underwater at launch unless usage is lower or cost optimization lands.** Mitigation: Tier C fair-use ceiling at 15 min/day, and launch Tier C only after the cost gate passes. This is a hypothesis to test, not a solved problem.

---

## 7. Discounts and guarantees

- **Student verification:** 40% off annual (SheerID or .edu + manual fallback). Verification must never block checkout — apply retroactively if needed.
- **Annual:** ~49% off monthly, default-selected (Education category runs 59–66% annual share, S10).
- **Interview guarantee (Career):** complete the 21-day plan (≥ 12 sessions) and if you do not feel more prepared, full refund within 30 days. Terms are explicit; abuse is bounded by completion requirements and reviewed manually. This converts the biggest objection ("what if it doesn't work?") into a reason to engage with the product.
- **Refunds:** 14 days, no questions, self-serve.
- **Pause:** 1–3 months, keeps progress and streak frozen. Pausing beats cancelling for seasonal learners (Maya after exams).

---

## 8. Packaging experiments (first 6 months post-launch)

| # | Hypothesis | Test | Primary metric | Guardrail | Backlog ID |
|---|---|---|---|---|---|
| 1 | $12.99 ≥ $9.99 on revenue per visitor | 50/50 price test, geo-matched | Revenue per visitor | Refund rate | T-13 |
| 2 | 14-day reverse trial beats metered free | Two-arm in-app test | D35 install→paid | D30 retention of non-converters | T-04 |
| 3 | $24.99 Career clears 8% at a fake door | Fake-door with qualification | CTA rate | $19.99 arm | T-05 |
| 4 | Annual default lifts LTV | Pre-selected annual vs monthly | 90-day LTV | Churn at month 13 | — |
| 5 | Pack bundle (Interview + Business) at $59 | Bundle vs separate | Attach rate | Cannibalization of Plus | — |
| 6 | "Finish this session free" paywall beats hard cap | Cap-experience test | Conversion + D7 | Session abandonment | — |
| 7 | Student annual at $24.99 in Tier C | Price test | Conversion | Margin per user | — |

**Rule:** never test price and paywall placement at the same time, and never run a price test on users acquired through a guarantee. One variable, one primary metric, pre-registered.

---

## 9. B2B economics (Phase 3)

| Metric | Value | Status |
|---|---|---|
| ACV per career center (200 seats × $7/mo) | $16.8k | H |
| Sales cycle | 3–5 months | H |
| Gross margin | 70–80% (usage is lower than consumer) | H |
| Payback | 9–12 months | H |
| Strategic value | Distribution into the student segment, outcome data at cohort scale, credibility for consumer marketing | — |

B2B is deliberately slow-rolled: it requires SSO, FERPA/GDPR review, and a sales motion the team does not have in year 1. It becomes a priority only after consumer retention is proven.

**What the model actually assumes — and why not to trust it.** `10` carries 200 seats from M16 growing 55%/month to ~6,660 seats by M24: $46.6k/month, $0.56M ARR, at $7/seat, **with no sales cost**. That is the single most optimistic line in the model. It is 21% of M24 net revenue at 100% gross margin, and removing it drops base-case M24 gross margin from 56.8% to **45.2%**. The three pilots behind the ACV are hypotheses, not contracts. Treat the B2B line as upside in every external conversation; the consumer thesis has to stand without it. Full disclosure at `10` §8.1.

---

## 10. What we will not do

- Charge for corrections, feedback, or the ability to delete your data.
- Use fake scarcity, countdown timers, or "someone is viewing this."
- Auto-renew without a pre-charge reminder email.
- Hide the annual price behind a monthly toggle.
- Sell or share voice data with advertisers — stated plainly on the pricing page.
- Price by IP address.
- Advertise "unlimited" voice without publishing the fair-use ceiling that makes it true.
- Quote a price in a comparison table without a dated source for the competitor's price.
