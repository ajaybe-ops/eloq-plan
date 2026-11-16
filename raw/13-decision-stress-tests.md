# 13 — Decision Stress Tests

**Version:** 2.0 · 2026-11-15

**Purpose:** three decisions carry most of the plan's risk. Each is written here with the strongest case *against* it, the rebuttal, the evidence that would flip it, and the cost of being wrong. If a decision cannot survive this format, it should not survive the plan.

**How to read:** the "steelman" is not a formality. It is the best version of the argument the person across the table will make. If the rebuttal is weaker than the steelman, the decision changes — that is the point of writing it down.

---

## D1 — Free tier shaped by voice economics vs. a marketing-led tier

**Current position:** free tier is metered on voice (3 sessions/week × 5 minutes, ~20 minutes per MAU per month), unmetered on feedback, text, drills, and review. The cap exists because voice is the only genuinely expensive unit in the product.

### Steelman against it

Conversion, not COGS, is the binding constraint. The model's base case converts at 2.6% — category median. Break-even is ~4.5%. If the free tier is the top of the funnel, then making it *smaller* to protect a cost line that is already only ~$0.26 per free MAU is optimizing the wrong variable. A generous free tier:

- lifts activation and word-of-mouth, which are the only cheap acquisition channels we have;
- matches what users expect from Duolingo (functionally unlimited practice) and from HelloTalk (free human chat);
- creates the habituation that makes a paywall convert at all — a 20-minute-per-month user never forms the habit that justifies $12.99;
- and voice costs are falling, not rising: ElevenLabs already advertises ~$0.05/minute at scale and Deepgram's ASR is $0.0048/minute. The cost curve argues for buying growth now.

There is also a positioning cost: a free tier that visibly runs out in 15 minutes reads as a demo, and "demo" is exactly the frame we are trying to escape.

### Rebuttal

The steelman is right about conversion and wrong about the mechanism. The evidence (RevenueCat SOSA 2026) says freemium converts at 2.1% D35 versus 10.7% for hard paywalls, and that 55% of 3-day trial cancellations happen on **day 0**. Conversion is decided in the first session, not by the size of the monthly allowance. Giving away more voice does not fix a first session that fails to demonstrate value; it just makes each failure more expensive.

Second, the arithmetic is unforgiving at the margin:

| Free minutes / MAU / month | Free COGS at $0.013/min | Revenue per free MAU (base, M12) | Net |
|---|---|---|---|
| 20 (current) | $0.26 | $0.81 | **+$0.55** |
| 35 | $0.46 | $0.81 | +$0.35 |
| 60 (v1 allowance) | $0.78 | $0.81 | **+$0.03** — underwater below ~4% conversion |

At 60 minutes the free tier is only viable if we convert at better than 4%, i.e. only if the wedge thesis is *already proven*. That is a bet placed with the money we need to survive until the proof. And the cost is not trivial at scale: each extra 10 free minutes per MAU costs ~$0.13/MAU/month, which at 180k MAU is ~$280k/year — roughly two engineers.

Third, "generous like Duolingo" ignores that Duolingo's free tier is generous in *cheap* units (text, static content, ads). Our expensive unit is the one thing that cannot be given away at Duolingo's economics.

### What would flip it

Flip toward a more generous tier if **all three** hold at the M9 review:

1. free-tier utilisation stays **below 25 minutes/MAU** (people do not use what we give them, so the cap is not the constraint);
2. D35 conversion at the current cap is **≥ 4.0%** (we are near break-even and can afford the subsidy);
3. the T-04 reverse-trial arm shows **no** D30 retention advantage (generosity is not the retention lever either).

Then raise the cap to 45 minutes/MAU and re-run the model. Partial evidence is not enough — condition 1 alone would mean the cap is irrelevant rather than wrong.

### Cost of being wrong

- **Too stingy (our risk):** conversion plateaus at 2.6%, ARR at M24 is $2.64M, cash-out at M18, and the company needs a Series A on a non-venture outcome. That is the base case in `10`, and it is the most likely failure mode in this plan.
- **Too generous (the alternative):** at M24 scale (161,880 free MAU), raising the allowance from 20 to 60 minutes raises free voice COGS from ~$32k to ~$97k/month at the optimized $0.010/session-minute. Gross margin at M24 falls from 56.8% to **~27%**, and the M24 cash position moves from −$1.21M to roughly −$1.6M. Painful and hard to reverse once users have the habit — which is why the stingy error is worse: closing the cap is a config change, but a permanently subsidised free tier is a business model. T-15 measures the actual utilisation response before either number is trusted.

**Current call:** metered voice, generous feedback. Confidence: **medium-high** on the mechanism, **low** on the exact number (20 minutes). Review at M9 with T-04 and T-08 data.

---

## D2 — In-house pronunciation scoring vs. licensing a best-in-class API

**Current position (revised in this pass):** **license** the acoustic scoring layer (Speechace, Azure Pronunciation Assessment, or equivalent) for the MVP; build in-house only the parts that are not commodity — L1-conditioned calibration, the error-memory loop, the drill-selection policy, and the interview rubric that turns a score into an action. Revisit a full in-house model at M12+ only if the economics or the latency budget demand it.

**This is a change from v1**, which called in-house GOP scoring the moat. The evidence that forced the change: phoneme-level pronunciation scoring is sold as an API (Speechace) and shipped as a platform add-on (Azure, including prosody). It is a commodity input, not a moat. Treating it as the moat would have meant spending two quarters rebuilding something we can rent for cents and defending a position that is already occupied.

### Steelman for building in-house (against the current position)

- **Cost at scale.** At M24 the model implies ~8M session minutes/month. A scoring API at even $0.005/minute is ~$40k/month, ~$0.5M/year — more than two engineers, forever, with no asset at the end.
- **Latency and control.** Pronunciation feedback has to arrive inside the conversation turn. A third-party hop adds 150–400 ms and a failure mode we cannot fix at 2 a.m.
- **Differentiation.** If everyone can rent the same scorer, then the score is table stakes — and the only way to differentiate on *scoring* is to own a model tuned on our own L1 data. Renting guarantees we are one of many.
- **Data rights.** Vendor terms often restrict using audio to train models, or charge for it. The data flywheel (below) may be the actual moat, and renting can starve it.
- **Vendor risk.** A single API price change or deprecation can reprice the whole business overnight. We saw the category move fast in 2026 alone.

### Rebuttal

Every point above is about *what we might need at scale*. The decision in front of us is *what we need to launch*. Building a scorer that reaches r ≥ 0.85 against human raters, across six L1s, is a 9–15 month program with a real chance of failing (see `08` R1 and doc `14`). Licensing gets us a validated, published methodology in weeks, which means we learn whether the *product* works before spending a year on the *model*.

On differentiation: the steelman concedes the key point — if the scorer is rentable, it is not the moat. The moat has to be the closed loop: what we do with the score (which drill, which scenario, which correction, in what order, for this learner, this week), the longitudinal error memory, and the outcome data that proves the loop works. Those are ours whether or not we rent the acoustic layer. A competitor can rent the same scorer and still not have the loop, the content, or the evidence.

On cost: at the steelman's $0.005/minute, $0.5M/year is ~19% of M24 net revenue — which is exactly why that comparison is the wrong one. The model actually carries **$0.0012–0.002 per session-minute** for licensed scoring: roughly $125–210k/year at M24 volume, **5–8% of net revenue** (11–14% at launch pricing before optimization), and that line falls as vendors compete. Two engineers building and maintaining a scorer cost more than that in year one, before any accuracy is proven. If a vendor ever demands $0.008/minute — ~$70k/month, ~32% of ARR — building becomes the cheaper option, and that is the flip threshold.

On data rights: this is the one argument that survives, and it is a contract problem, not a build problem. Negotiate training rights explicitly, or run a parallel data-collection pipeline that logs consented audio for future model work without depending on vendor terms.

### What would flip it

Flip to in-house if, at the M12 review, **any two** of the following hold:

1. licensing cost **> $0.008 per session minute** at projected volume (i.e. > ~$70k/month at M24 scale), with no contractual path down;
2. measured p95 scoring latency **> 350 ms** added to the turn, and no vendor edge/embedded option;
3. the vendor cannot deliver **L1-conditioned calibration** or per-L1 error norms, and our own calibration layer cannot compensate (r drops below 0.80 for two launch L1s);
4. we cannot obtain **training rights** on our own audio, blocking the data flywheel.

A single condition is not enough — each is survivable on its own (renegotiate, cache, calibrate externally, collect separately).

### What an in-house build would now have to prove

The moat thesis has already flipped in principle (`03` §9): the acoustic layer is commodity, the loop is ours. So an in-house scorer is no longer justified as "the moat" — it can only be justified as **a cheaper, better component**. The bar is explicit:

| Test | Threshold to justify building | Why |
|---|---|---|
| Accuracy lift over licensed | **r ≥ 0.90** overall, and ≥ 0.85 for every launch L1 (licensed baseline: 0.85 / 0.75) | A 5-point accuracy gain is the minimum that changes what the product can claim |
| Subgroup spread | Best–worst L1 gap ≤ 0.05 (licensed: ≤ 0.10) | The only defensible reason to own the model is fairness the vendor cannot deliver |
| Fully loaded cost | ≤ **$0.006/session-min** by M18, including 2 FTE and GPU | Below the low end of licensing ($0.003–0.008), or it is a cost *increase* |
| Time to gate | Prototype r ≥ 0.85 within 6 months, or the program stops | The launch cannot wait 15 months for a component |
| Data rights | Unrestricted training rights on consented audio | Otherwise the flywheel is rented, not owned |

**It loses on this comparison if** r < 0.85 at month 6, or fully loaded cost > $0.008/session-min at M18, or the L1 spread is no better than the vendor's. In that case we keep licensing, and the engineering time goes to the loop — which is where the actual differentiation lives.

### Cost of being wrong

- **If we license and should have built:** we pay ~$0.13–0.21M/year at current vendor rates (up to ~$0.5M at the steelman's $0.005/minute), carry vendor dependency, and are 6–9 months behind on a proprietary model. Recoverable; the switch can start at any time with the data we have been collecting.
- **If we build and should have licensed:** we spend ~$180–250k in engineering, delay launch by 4–6 months (~$400k burn), and may still fail the r ≥ 0.85 gate with no fallback — because the fallback (license) is now a rushed integration under deadline pressure. This is the asymmetric error, and it is the error v1 was steering into.

**Current call:** license now, build the loop. Confidence: **high** on the direction, **medium** on the specific vendor. Review at M12 with the four flip conditions above.

---

## D3 — Job-seeker wedge vs. student-first

**Current position:** job seekers first (M0–12), students second (M12–24), B2B last.

### Steelman for student-first

- **Size and reach.** HelloTalk's actual base is broad and young; students are the largest addressable pool of English learners, they are cheap to reach on campus and short-form video, and they bring friends (the referral loop works when your cohort is co-located).
- **Longer lifetime.** A student who starts at 19 can pay for four years. A job seeker churns when they get the offer — often within 90 days. Student-first maximizes LTV, which the model needs: Education-category annual-plan share is 59–66%, and students are the ones who buy annual.
- **Cheaper content.** Campus and general-English scenarios are reusable and less research-intensive than role-specific interview content (which needs per-role JDs, rubrics, and hiring-manager review). Interview content is expensive to keep current.
- **Lower price sensitivity risk.** Parents pay; student pricing is an accepted category norm; and the $49.99 student annual has a clean story.
- **The competitor evidence cuts both ways.** ELSA already ships an Interview Coach at $19.99. If a well-funded pronunciation incumbent already owns "career English," attacking there is a frontal assault; students are the softer flank.

### Rebuttal

The student-first case is a *better business at scale* and a *worse business to start*. Three reasons:

1. **Deadline creates conversion.** The entire financial model turns on D35 conversion above ~4.5% — roughly twice the category median. Students convert on aspiration; job seekers convert on a dated event with an income-linked payoff. T-01 exists to test exactly this, and if it fails, D3 flips (see below). We should not assume it; we should test it in two weeks for $2.5k.
2. **The outcome is measurable in 90 days.** "Did you get the interview?" is verifiable. "Did your English improve this semester?" is not — which means the student-first version of this company cannot produce the one asset that makes the marketing defensible (T-07).
3. **Price anchors differ.** $12.99 against "one hour of a tutor" is a hard sell to a student; $24.99 against "$100–300 per mock interview" is an easy sell to someone with an interview in three weeks. The Career tier is where gross margin is healthiest (bounded usage, deadline-driven churn that ends in a good story rather than a refund).

On ELSA: shipping an Interview Coach is not the same as owning career outcomes. ELSA's positioning is still pronunciation-first with a career vertical; its pricing ($19.99/$99.99) leaves the premium interview-outcome tier open, and its content is not built around a specific JD and a specific interview date. The existence of a competitor validates the wedge; it does not close it. But it does mean we cannot claim to be first, and `03` is corrected accordingly.

### What would flip it

Flip to student-first if, at Gate 2 (2027-02-05):

1. **T-01:** job-seeker CPA **> 1.5×** student CPA, **and** the share of job-seeker signups with an interview within 60 days is **< 25%** (the urgency is not there); **or**
2. **T-05:** Career fake-door take-rate **< 8%** at $24.99 while a $12.99 student offer clears 15%; **or**
3. **T-02:** fewer than **30%** of blind testers prefer our interview sim to a strong general-assistant prompt (the product does not exist yet).

Any one of these is sufficient, because each independently breaks the "job seekers convert 2–3× better" premise that the model depends on.

### Cost of being wrong

- **Wedge is wrong (we chose job seekers):** ~$250k of interview content and rubric work is stranded (partially reusable as workplace content), the Career tier launches late or not at all, conversion stays at 1.8–2.6%, ARR at M24 is $2.0–2.6M, and cash-out arrives at M17–18. We would be a small consumer subscription business with an expensive content library — survivable only by cutting to a 6-person team.
- **Student-first is wrong (we had chosen it):** lower ARPU, worse conversion, no outcome study, and a positioning that competes head-on with Duolingo's free tier and HelloTalk's free chat. The failure mode is not bankruptcy; it is irrelevance — a nice app with no evidence and no pricing power.
- **Both wrong:** the honest third outcome is that neither segment converts above 4%, in which case the correct move is the `08` §5 kill criterion (re-scope to interview-only or shut down consumer) rather than a third repositioning.

**Current call:** job seekers first, with student content shipped early enough to serve the overflow. Confidence: **medium**. This is the least-evidenced of the three decisions and the one T-01/T-05/T-02 exist to settle — before launch, not after.

---

## Appendix — decisions we did not flag, and why

| Decision | Why it is not contested | Revisit |
|---|---|---|
| English-only at launch | Depth over breadth; every added language multiplies content, ASR eval, and support | M18, only after retention is proven |
| No 1:1 stranger chat, ever | It is the safety moat and the brand; the cost (slower organic growth) is accepted | Never |
| 16+ minimum age | Serving minors requires consent infrastructure and a safety team we do not have | After external safety audit |
| Feedback is never metered | Metering feedback converts the free tier into a demo and destroys trust in the score | Never |
| Community gated on external audit | One incident is existential; the audit is cheaper than the incident | At audit completion |

**The pattern:** the decisions we do not stress-test are the ones where the cost of being wrong is catastrophic and the cost of the constraint is merely slow. Everything else gets a steelman.
