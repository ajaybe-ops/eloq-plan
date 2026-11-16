# 10 — Financial Model

**Version:** 2.0 · 2026-11-15

**Files:** `10-financial-model.csv` (monthly P&L, M0–M24, four scenario runs), `10-financial-model-inputs.csv` (every input with evidence status), `build_model.py` (reproducible generator — edit inputs, re-run, no spreadsheet drift).

**This is a planning instrument, not a forecast.** Its job is to show which assumptions are load-bearing and what happens when they break. Three of them are decisive: D35 conversion, paid churn, and voice cost per session minute.

---

## 1. Three corrections to the v1 model

The first version of this plan was internally consistent but wrong in three places. Each correction is documented because each one changes a decision.

| # | v1 | v2 | Why it changed |
|---|---|---|---|
| 1 | Voice cost **$0.051/min**, falling to $0.021 | **$0.018/session-min**, falling to $0.010 | v1 charged a full minute of ASR *and* a full minute of TTS for every session minute. In a real conversation the learner speaks ~55% of the time and the tutor ~45%. Pricing both at 100% duty overstates COGS by ~2.2×. Verified vendor rates (S8): ASR $0.0048/min, TTS $0.015–0.030/1k chars. |
| 2 | Plus **$9.99/mo** | **$12.99/mo, $79.99/yr** | Price parity with HelloTalk VIP (S2, $12.99/$79.99) turns the comparison into "same price, and it answers." It also covers the COGS of a 300-min/month user. |
| 3 | Churn **5.5%/mo**, conversion 5–8% of MAU | Churn **8%/mo**, D35 **1.8% / 2.6% / 6.0%** | RevenueCat SOSA 2026: freemium D35 median 2.1%, NA median 2.6%, top quartile 5.6%; AI apps churn ~30% faster; Education Y1 realized LTV/payer $22.82 (S10). v1's conversion and retention were both optimistic by roughly 2–3×. |

**Net effect:** the business is *more* viable on gross margin than v1 claimed (COGS was overstated) but *less* viable on growth and retention (conversion was overstated). The wedge case becomes the whole ballgame.

---

## 2. Scenario definitions

| Input | Downside | Base | Wedge |
|---|---|---|---|
| D35 install→paid | 1.8% | 2.6% | 6.0% |
| Source | Below category median | NA median (S10) | Just above top quartile (S10) |
| Churn | 8%/mo | 8%/mo | 8%/mo |
| Install growth | 8%/mo → 5%/mo | same | same |
| Voice cost | $0.018 → $0.010 | same | same |

Everything except D35 is held constant, so the table isolates one question: **can this product convert at above-category-median rates?**

---

## 3. Headline results

| Month | Metric | Downside | Base | Wedge |
|---|---|---|---|---|
| **M6** | Paid subs | 1,281 | 1,850 | 4,270 |
| | Net revenue | $12.3k | $17.8k | $41.0k |
| | Gross margin | −64% | −30% | +15% |
| **M12** | Paid subs | 4,307 | 6,221 | 14,355 |
| | Net revenue (ARR) | $41k ($0.49M) | $59k ($0.71M) | $137k ($1.64M) |
| | Gross margin | 1.7% | 19.5% | 42.3% |
| **M18** | Paid subs | 7,770 | 11,224 | 25,901 |
| | Net revenue (ARR) | $82k ($0.98M) | $117k ($1.40M) | $266k ($3.19M) |
| | Gross margin | 34.6% | 45.1% | 58.9% |
| **M24** | Paid subs | 11,625 | 16,792 | 38,750 |
| | Net revenue (ARR) | $167k ($2.00M) | $220k ($2.64M) | $446k ($5.36M) |
| | Gross margin | 52.6% | 56.8% | 63.5% |
| | Cash | **−$1.57M** | **−$1.21M** | **+$0.31M** |
| | EBITDA-positive month | never | never | M24 |

**Reading it honestly**

- At category-median conversion (base), the company needs a **Series A around M14–M15** or it runs out of money at M18. The product is a decent $2.64M-ARR business at M24 — not venture-scale on its own.
- At wedge conversion (6%), the company is **self-funding on a $4M seed**, reaches $5.36M ARR and 63% gross margin at M24, and is EBITDA-positive by M24. That is a credible Series A story.
- At downside conversion, it never works. Kill or re-scope by M18 (see kill criteria, `08` §5).

**The plan therefore does not have a "base case" it can coast on.** It has one thesis — job seekers convert at 2–3× category rates because they have a deadline and an income-linked payoff — and the entire company either proves it in the first nine months or changes shape.

---

## 4. The cost gate

The month-9 gate from v1 is retained but restated in corrected units: **all-in voice cost must be ≤ $0.016 per session minute by M9.**

| Case | M12 gross margin | M24 gross margin | Cash-out month |
|---|---|---|---|
| Base, gate passed ($0.013 → $0.010) | 19.5% | 56.8% | M18 |
| Base, gate failed (floor $0.016) | 2.2% | 32.9% | M17 |

A failed gate costs ~9 points of gross margin at M12 and ~24 points at M24, and pulls cash-out forward one month. It does not kill the company by itself — but combined with base-case conversion it removes any path to a Series A.

**Gate fallbacks, pre-approved:** (a) move Plus to $14.99 with a 300-minute bundle; (b) cut free voice to 1 session/week; (c) move to a credits model for voice. Decide at M9 with data, not at M14 in a panic.

---

## 5. Unit economics

| | Downside | Base | Wedge |
|---|---|---|---|
| Blended ARPU (net, M24) | $14.32 | $13.09 | $11.52 |
| Blended CAC (M1–M12) | $42.23 | $29.24 | $12.67 |
| Gross-margin LTV (ARPU × 57% ÷ 8%) | $102 | $93 | $82 |
| **LTV : CAC** | **2.4** | **3.2** | **6.5** |
| CAC payback (months) | 5.2 | 3.9 | 1.9 |

*LTV uses a 57% steady-state gross margin and 8% monthly churn. At category-median retention the LTV falls to ~$40 and every ratio collapses — see §6.*

---

## 6. Sensitivity: what actually moves the outcome

### 6.1 Churn (the second-most important assumption)

Gross-margin LTV and LTV:CAC at $29 CAC, $13.09 ARPU, 57% GM:

| Monthly churn | Avg paid life | GM LTV | LTV:CAC | Verdict |
|---|---|---|---|---|
| 5% | 20 mo | $149 | 5.1 | Healthy |
| **8% (base)** | **12.5 mo** | **$93** | **3.2** | **Acceptable** |
| 12% | 8.3 mo | $62 | 2.1 | Marginal |
| 20% | 5 mo | $37 | 1.3 | Unviable |

RevenueCat's Education Y1 realized LTV of **$22.82/payer** (S10) implies the *category median* is far below even the 20%-churn row. Our $93 LTV is therefore a **top-quartile claim**, not a neutral assumption. It has to be earned with annual plans, the career wedge, and post-offer retention — and it is tested at T-06.

### 6.2 Conversion

| D35 | Paid at M24 | ARR M24 | Cash at M24 |
|---|---|---|---|
| 1.8% | 11.6k | $2.0M | −$1.57M |
| 2.6% | 16.8k | $2.64M | −$1.21M |
| 4.0% | ~26k | ~$3.6M | ~−$0.35M (est.) |
| 6.0% | 38.8k | $5.36M | +$0.31M |

The break-even conversion, holding everything else constant, is **≈4.5%**. That is the number to put on the wall: *we need to convert at roughly twice the category median, or this is a different company.*

### 6.3 Free-tier generosity

Free voice minutes per MAU is the largest controllable cost line. At 20 min/MAU and $0.013/min, free users cost $0.26/month and generate $0.81 in revenue per free MAU (base, M12) — positive. At 60 min/MAU (the v1 allowance), free cost rises to $0.78 and the model goes underwater at every conversion level below ~4%.

**Design implication:** free tier stays at 3 sessions/week × 5 minutes, with average utilisation near 20 minutes/month. If utilisation climbs above 35 minutes, either tighten the cap or raise conversion — do not let it drift.

---

## 7. Runway and financing

| | Base | Wedge |
|---|---|---|
| Seed | $4.0M | $4.0M |
| Pre-launch spend (M0) | $0.85M | $0.85M |
| Minimum cash | −$1.21M (M24) | +$0.30M (M18 trough) |
| Cash-out | M18 | never |
| Financing need | $6–8M Series A by M15, or $1.5M bridge | Optional Series A at M18–20 on strength |

**Triggers, written in advance:**

- **M9:** if D35 < 3.0% and paid churn > 10%, start the Series A process *and* cut paid acquisition by 50%.
- **M12:** if wedge indicators are absent, move to the "cash-efficient variant" — cut opex to $140k/mo, drop the community phase, sell packs and B2B only.
- **M15:** if no term sheet and cash < $900k, execute the pre-approved bridge plan (12-month extension, 15% opex cut, freeze hiring).

---

## 8. What the model deliberately does not include

| Excluded | Why | Impact if included |
|---|---|---|
| Enterprise/B2B sales cost | No sales team in model; B2B assumed to start at M16 | B2B revenue is optimistic without CAC — see the note below |
| Human-reviewed mock interviews | Sold as a $49 add-on (57% margin), not a subscription entitlement | Excluded to avoid double-counting; including one per 90 days as a bundle would cut Career margin from 52% to 11% (`05` §4.3) |
| Content production beyond M12 | 60 scenarios, 5 packs | +$150–250k one-time |
| Refunds and chargebacks | 2–4% of revenue typical | −2 to −4% revenue |
| Tax, VAT/GST, app-store currency effects | Jurisdiction-dependent | −3 to −8% net revenue |
| Fraud / free-trial abuse | Mitigated but not free | −1 to −2% revenue |

Adding all of these moves M24 gross margin down roughly 5 points and pushes the base-case cash-out earlier by ~1 month. The conclusions do not change; the margin of safety shrinks.

### 8.1 The B2B line is the model's most optimistic assumption

The B2B line assumes **200 seats at M16, growing 55% per month to ~6,660 seats by M24** — $46.6k/month, or **$0.56M ARR**, at $7/seat/month and **with zero sales cost**. That is not a forecast; it is a placeholder for "B2B exists." It is also 21% of M24 net revenue and, because no COGS is allocated to it, it contributes at 100% gross margin.

Removing B2B entirely drops base M24 gross margin from **56.8% to 45.2%** ($173.2k/month revenue against $94.9k of COGS) and does not change the cash-out month. It does remove the line that makes the base case look like a venture-scale business at M24. Neither the seat ramp nor the zero-CAC assumption has any evidence behind it: `05` §9 lists three pilots, none signed, and `08` §4 carries B2B as an open risk. **Treat B2B as upside, not base** — the frozen scenario totals above include it, so every reader should mentally subtract it when judging the base case.

---

## 9. How to use this file

1. Change an input in `build_model.py` (one constant at the top).
2. Run `python build_model.py`.
3. The CSVs regenerate; the scenario table in this document must be updated by hand in the same commit (or the doc is marked stale).

**Rule:** any pricing, COGS, or funnel number quoted in `01`, `05`, or `EXEC-SUMMARY.md` must match this model. If it does not, the model wins and the prose is wrong.
