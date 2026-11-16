# 09 — Evidence Log

**Version:** 2.0 · 2026-11-15

**Purpose:** every quantitative claim in this document set is mapped here to either (a) a dated source, (b) arithmetic over dated sources, or (c) an explicit hypothesis with the cheapest test that would settle it.

**Status legend**

| Tag | Meaning | Obligation |
|---|---|---|
| **V** | Verified — public source, accessed and date-stamped | Re-verify at each quarterly review |
| **D** | Derived — arithmetic over V inputs | Recompute if an input changes |
| **H** | Hypothesis — no public evidence found, or evidence is private/conflicting | Must have a test ID (T-xx) and an owner |
| **X** | Decision — a product/business choice, not a factual claim | Review date only; no test required |
| **A** | Abandoned — claim withdrawn, must not appear publicly | Remove from all decks and pages |

**Rule:** nothing tagged H may appear in an investor deck, a public comparison page, or an ad without the tag converting to V.

---

## 1. Verified sources (accessed 2026-11-15)

| ID | Source | URL | What it establishes |
|---|---|---|---|
| S1 | HelloTalk marketing site | https://www.hellotalk.com/ | 70M+ learners, 200+ countries, 260+ languages; text/voice/video, Voicerooms, Livestreams, Moments, translation/transliteration/corrections; partner search by native language and city |
| S2 | HelloTalk, App Store (US) | https://apps.apple.com/us/app/hellotalk-language-exchange/id557130558 | VIP Monthly **$12.99**, VIP Yearly **$79.99**, coins; 44K ratings, 4.6; age **13+**; privacy label: precise location, audio data, identifiers, third-party advertising; 793.6 MB |
| S3 | HelloTalk "More by" listing + site apps menu | S1/S2 | Separate AI products already exist: *AI Grammar*, *Talksy* (AI language learning), *HelloWords*, *English Ai* |
| S4 | Duolingo, App Store (US) | https://apps.apple.com/us/app/duolingo-language-lessons/id570060128 | Super Duolingo **$9.99 / $83.99** (also $12.99/$119.99 variants); 5.6M ratings, 4.7; age 4+; #1 Education |
| S5 | ELSA Speak, App Store (US) | https://apps.apple.com/us/app/elsa-speak/id1083804886 | **$19.99/mo, $99.99/yr**; AI conversation coach, **Interview Coach**, pronunciation + word stress feedback, CEFR/IELTS/TOEFL/TOEIC mapping, 8,000+ lessons, professional coach verticals (negotiation, sales, leadership); 115K ratings, 4.7 |
| S6 | Speechace | https://www.speechace.com/ | B2B API selling **phoneme-level** pronunciation + fluency scoring, IELTS/PTE estimates, B2B only, pricing on request |
| S7 | Azure Speech pricing page | https://azure.microsoft.com/en-us/pricing/details/cognitive-services/speech-services/ | Pronunciation Assessment (including **prosody**) exists as a paid add-on; captured page rendered prices as placeholders, so cost is H |
| S8 | Deepgram pricing | https://deepgram.com/pricing | Streaming ASR **$0.0048/min** (Nova-3), Flux $0.0065; TTS **$0.015/1k chars** (Aura-1), **$0.030/1k** (Aura-2), $0.045/1k (Flux); managed Voice Agent $0.075/min |
| S9 | ElevenLabs pricing | https://elevenlabs.io/pricing | Business tier $990/mo for 6M credits ≈ **$0.165/1k characters**; "low-latency TTS as low as **5c/minute**" at scale |
| S10 | RevenueCat, *State of Subscription Apps 2026* | https://www.revenuecat.com/state-of-subscription-apps/ | 115k apps, $16B revenue. Freemium **D35 download→paid 2.1%** vs hard paywall **10.7%**; NA median 2.6%, top quartile 5.6%, P90 10.4%; IN/SEA median 1.4%; **AI apps +41% revenue/payer, 30% faster churn**; Education **Y1 realized LTV/payer $22.82**; Education annual plans **59–66%**; 55% of 3-day trial cancellations occur day 0; 17+ day trials convert **42.5% vs 25.5%** |
| S11 | Apple Developer, Small Business Program | https://developer.apple.com/app-store/small-business-program/ | **15% commission** while proceeds ≤ $1M/yr; 10% in some EU alternative-term cases |

---

## 2. Claim register

### 2.1 Competitor claims (used in 03-competitive-positioning.md)

| ID | Claim | Value | Tag | Evidence | Owner | Next action |
|---|---|---|---|---|---|---|
| C1 | HelloTalk VIP price | $12.99/mo, $79.99/yr | **V** | S2 | Research | Re-check quarterly |
| C2 | HelloTalk scale | 70M+ learners, 260+ languages | **V** | S1 | Research | Re-check quarterly |
| C3 | HelloTalk has no phoneme-level pronunciation score | Absent from all store copy and site features | **V** (absence documented) | S1, S2 | Research | Re-check at each release |
| C4 | HelloTalk has no structured CEFR curriculum | No curriculum claim anywhere in listing/site | **V** (absence documented) | S1, S2 | Research | Re-check |
| C5 | HelloTalk has no interview simulator | Absent from listing/site; AI products are grammar/chat/vocab | **V** | S1, S2, S3 | Research | Re-check |
| C6 | HelloTalk exposes minors to stranger chat | Age rating 13+, messaging + user-generated content, location collected | **V** | S2 | Research | Re-check |
| C7 | HelloTalk retention is ~40/20/10 (D1/D7/D30) | — | **A** | No public data; company is private | Research | Never publish. Replace with our own matched cohort (T-09) |
| C8 | Duolingo price | $9.99/mo, $83.99/yr | **V** | S4 | Research | Re-check |
| C9 | ELSA already ships interview coaching + CEFR mapping at $19.99/mo | — | **V** | S5 | Product | Update positioning: we are not first to "career English" |
| C10 | Speak (speak.com) pricing | — | **A** | Pricing page 404 on 2026-11-15; no verified source | Research | Do not name a price until verified |
| C11 | Phoneme scoring is a commodity capability | Available as API (Speechace) and platform add-on (Azure) | **V** | S6, S7 | Product | Drives the moat rewrite in 03 §7 |

### 2.2 Benchmark claims (used in 05, 06, 10)

| ID | Claim | Value | Tag | Evidence | Owner | Next action |
|---|---|---|---|---|---|---|
| B1 | Freemium D35 install→paid, category median | 2.1% | **V** | S10 | Growth | Use as base-case scenario |
| B2 | Hard-paywall D35 install→paid | 10.7% | **V** | S10 | Growth | Test reverse trial (T-04) |
| B3 | NA D35 median / top quartile / P90 | 2.6% / 5.6% / 10.4% | **V** | S10 | Growth | Wedge case = 6.0% sits just above top quartile |
| B4 | IN/SEA D35 median | 1.4% | **V** | S10 | Growth | Sets Tier-C market expectations |
| B5 | AI apps: revenue per payer / churn | +41% / −30% retention | **V** | S10 | Product | Justifies retention investment over features |
| B6 | Education Y1 realized LTV per payer | $22.82 median | **V** | S10 | Finance | Our M6 LTV ($163 revenue / $93 gross-margin) is 7× / 4× this — the gap must be earned, not assumed |
| B7 | Education annual-plan share | 59–66% | **V** | S10 | Growth | Supports 60% annual mix in model |
| B8 | 3-day trial cancellations on day 0 | 55% | **V** | S10 | Growth | First-session quality is the conversion lever |
| B9 | 17+ day trials convert vs short trials | 42.5% vs 25.5% | **V** | S10 | Growth | Supports 14-day reverse trial (T-04) |
| B10 | D1/D7/D30 language-app retention | 45/25/15 (planning) | **H** | No verified public series | Data | T-08: measure our beta; optionally buy a benchmark report |
| B11 | HelloTalk-specific retention | — | **A** | Not disclosed | — | Do not claim |

### 2.3 Cost claims (used in 05, 07, 10)

| ID | Claim | Value | Tag | Evidence | Owner | Next action |
|---|---|---|---|---|---|---|
| K1 | Streaming ASR | $0.0048–0.0065/min | **V** | S8 | Eng | Re-quote at volume |
| K2 | TTS | $0.015–0.045/1k chars → ~$0.012–0.037/min at 150 wpm | **V**/**D** | S8, S9 | Eng | Lock a vendor by M2 |
| K3 | LLM cost per conversational turn | $0.002–0.004 | **H** | Vendor API pricing not captured in this pass | Eng | T-11: 200-turn instrumented spike |
| K4 | Pronunciation scoring (GPU) | $0.002/session-min | **H** | No vendor quote; self-hosted estimate | Eng | T-12: benchmark on target GPU |
| K5 | All-in voice cost, launch | $0.018/session-min | **D** | K1–K4 with 55%/45% duty cycles | Eng | Validate in spike (T-11) |
| K6 | All-in voice cost, M13 | $0.010/session-min | **H** | Caching + routing plan | Eng | Month-9 gate: ≤ $0.016 |
| K7 | App-store commission | 15% | **V** | S11 | Finance | Re-check at $1M proceeds |
| K8 | Human rater cost | $18/hr | **H** | Freelance marketplace rates, unsourced | Research | T-10: 3 quotes for 300-utterance study |
| K9 | CAC by channel | $6–45 | **H** | Industry ranges, unsourced | Growth | T-03: live campaign test |

### 2.4 Market and business claims

| ID | Claim | Value | Tag | Evidence | Owner | Next action |
|---|---|---|---|---|---|---|
| M1 | Serviceable market | 80M learners | **H** | Top-down estimate, no source | Strategy | Bottom-up model by country (T-14) |
| M2 | English-learning digital spend | $10–15B/yr | **H** | Analyst-range estimate, uncited | Strategy | Buy one report or drop the claim |
| M3 | Job-seeker conversion is 2–4× casual learners | — | **H** | Internal reasoning only | Product | T-01: landing-page conversion by segment |
| M4 | Interview cohort: next-stage interview within 90 days | 45% | **H** | No baseline exists | Research | T-07: 200-person cohort with verified sample |
| M5 | Paid churn | 8%/mo blended | **H** | Implied by S10 category RLTV; not directly observed | Finance | T-06: 3 months live cohort data |
| M6 | LTV | $163 revenue · $93 gross-margin (base, 8% churn) | **D**/**H** | ARPU ÷ churn; both inputs H | Finance | Recompute at M6 and M12 |
| M7 | CAC | $29 blended | **H** | Model over unsourced CPI | Growth | T-03 |
| M8 | Seed raise | $4.0M | **X** | Working assumption | CEO | Revisit after T-03/T-05 |

### 2.5 Product and technical targets (these are commitments, not facts)

| ID | Claim | Value | Tag | Test |
|---|---|---|---|---|
| P1 | Pronunciation score correlates with human raters | r ≥ 0.85 | **X** (gate) | 14-pronunciation-validation.md |
| P2 | CEFR estimate agrees with examiners | κ ≥ 0.70 | **X** (gate) | 200-sample examiner study |
| P3 | p50 first-audio latency | ≤ 1.2 s | **X** | Instrumented in beta |
| P4 | Correction precision | ≥ 92% | **X** | 500-item gold set in CI |
| P5 | ASR WER, read / spontaneous | ≤ 12% / ≤ 22% | **H** | Per-L1 eval set (T-12) |
| P6 | 4-week speaking gain | +8 points | **H** | Outcome cohort (T-07) |
| P7 | Interview Readiness Index predicts real outcomes | — | **H** | Correlate IRI with 90-day outcomes (T-07) |

---

## 3. What happened to the v1 unverified register

Every item from v1 `08-risks-open-questions.md` §8 is resolved here. None were deleted; each is upgraded, downgraded, or abandoned.

| v1 assumption | v1 status | v2 resolution | ID |
|---|---|---|---|
| HelloTalk pricing and features | unverified | **Verified** from store listing + site | C1–C6 |
| HelloTalk/category retention | unverified | **Abandoned.** No public HelloTalk data exists. Category proxies verified where possible; D1/D7/D30 remain H | C7, B10 |
| Voice COGS $0.051 → $0.021 | unverified | **Corrected.** v1 priced every session minute at 100% ASR *and* 100% TTS duty, overstating cost ~2.2×. Corrected to $0.018 → $0.010 per session-minute | K5, K6 |
| Conversion 5–8% of MAU | unverified | **Replaced** by benchmarked D35 scenarios 1.8% / 2.6% / 6.0% | B1–B3 |
| Paid churn 5.5%/mo | unverified | **Revised** to 8%/mo, consistent with category RLTV and AI-app churn penalty | M5 |
| Interview cohort outcome ≥ 45% | unverified | **Downgraded to H** with a pre-registered study | M4 |
| Market size ~80M | unverified | **Downgraded to H**; not used in any public material | M1 |
| CAC $6–45 by channel | unverified | **Downgraded to H**; live test scheduled | K9 |
| CEFR κ ≥ 0.70 | unverified | Reclassified as a **commitment**, not a forecast | P2 |
| "Better retention than HelloTalk" | implied | **Abandoned as a public claim.** Replaced with "designed for daily practice" until a matched cohort exists | C7 |

---

## 4. Open tests (summary — full specs in 11-experiment-backlog.md)

| Test | Question | Cost | Weeks | Kill signal |
|---|---|---|---|---|
| T-01 | Do job seekers convert better than students? | $2.5k | 2 | Job-seeker CPA > 1.5× student |
| T-02 | Does the interview scenario beat a ChatGPT prompt in blind test? | $1.5k | 3 | < 30% prefer ours |
| T-03 | What is real CAC by channel? | $8k | 4 | Blended CAC > $60 |
| T-04 | Reverse trial (14-day) vs metered free tier | $0 (product) | 6 | Trial arm D30 not ≥ +5pp |
| T-05 | Will job seekers pay $24.99/mo? | $1k | 2 | < 8% take-rate at fake door |
| T-06 | What is real paid churn? | $0 | 12 | > 12%/mo |
| T-07 | Do learners get interviews after the program? | $6k | 16 | < 25% at 90 days |
| T-08 | What are our real D1/D7/D30? | $0 | 8 | D7 < 22% |
| T-09 | Matched-cohort comparison vs. language-exchange users | $12k | 12 | No measurable delta |
| T-10 | What do human raters actually cost? | $0 (quotes) | 1 | > $30/hr |
| T-11 | Real voice cost per session minute | $0 (spike) | 3 | > $0.025 |
| T-12 | ASR WER by L1 accent | $0 | 3 | > 25% for any launch L1 |
| T-13 | Price elasticity: $12.99 vs $9.99 | $0 | 4 | Revenue/visitor worse at $12.99 |
| T-14 | Bottom-up market size | $0 | 2 | Serviceable < 20M |
| T-15 | Free-tier generosity: 60 vs 20 min/MAU | $0 (product) | 8 | 60-min arm D35 not ≥ +0.8pp |
| T-16 | D35 calibration: downside, base, or wedge? | $0 | 12 | < 1.8% at M9 triggers the kill path |

**Mapping note:** T-15 tests the free-tier decision (D1 in `13`) against claim K5 and the free-tier arithmetic in `10` §6.3; T-16 calibrates claims B1–B3 against live cohorts and drives the scenario choice in `10` §6.2. Tests T-01–T-14 map to the claim IDs cited in their cards in `11`.

---

## 5. Claims that must never appear publicly

| Claim | Why |
|---|---|
| "HelloTalk users churn at X%" | Private company; no data; unverifiable and legally risky |
| "We retain better than HelloTalk" | Requires a matched cohort we do not yet have (T-09) |
| "Fluent in 30 days" / "native accent" | Unprovable and contrary to the product's own ethical stance |
| Any Speak (speak.com) pricing | Source not verified (C10) |
| Any market-size figure before T-14 | Currently a top-down guess (M1) |
| "Validated by research" before the P1 protocol reports | The study is designed, not run |

---

## 6. Maintenance

- **Owner:** Head of Research (rotating until hired: PM).
- **Cadence:** full re-verification quarterly; incremental updates whenever a test closes.
- **Rule:** if a source URL 404s or a price changes, the claim reverts to **H** immediately and the dependent docs are flagged in the same commit.
- **Rule:** a claim may appear in at most one canonical place (this file); other docs link to the ID rather than restating the number.

*Access dates in this file are the date the page was fetched during this revision pass: 2026-11-15. Prices and feature sets change; nothing here is a permanent fact.*
