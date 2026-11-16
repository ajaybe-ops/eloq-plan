# 12 — Launch Checklist

**Version:** 2.0 · 2026-11-15

**Launch date:** **T-0 = Monday 2027-06-07** (public MVP, US/CA/UK + two Tier-B markets).
**Assumption:** seed closes 2026-12-01. If it closes later, every date below shifts by the same number of weeks; the *relative* spacing is the plan, the calendar is an artifact.

> A launch date is a gate, not a wish. §10 defines the six conditions that will postpone launch. They are written now, while postponing is cheap and nobody's bonus depends on the date.

---

## 1. Date map

| Milestone | Date | What must be true |
|---|---|---|
| M0 — seed close, build starts | 2026-12-01 | Team of 8 hired or contracted; cost instrumentation specced |
| Gate 1 — economics | 2027-01-08 | Voice cost ≤ $0.018/session-min measured (T-11); no launch L1 > 25% WER (T-12) |
| Gate 2 — wedge | 2027-02-05 | Job-seeker CPA ≤ student CPA (T-01); Career price confirmed (T-05) |
| Gate 3 — product | 2027-02-26 | Interview sim ≥ 55% blind preference vs strong prompt (T-02) |
| Closed beta opens | 2027-03-01 | 500 seats; onboarding instrumented; support staffed |
| Waitlist → beta conversion | 2027-04-12 | ≥ 35% of waitlist accepts; D7 ≥ 30% in beta |
| Feature freeze | 2027-05-14 | No new scope; bug-fix and polish only |
| Release candidate | 2027-05-24 | Submitted to App Store and Play; review notes written |
| **T-0 public launch** | **2027-06-07** | §10 conditions met |
| T+7 review | 2027-06-14 | Crash-free ≥ 99.5%, activation ≥ 40%, no P0 incidents |
| T+30 review | 2027-07-07 | D7 read, CAC read, cost per minute reconciled to invoice |
| Career tier launch | 2027-09-13 | T-02 read passed; 1 human-review vendor live |
| Campus push | 2027-12-06 | Student annual live; 20 ambassadors signed |
| B2B pilots | 2028-03-06 | 3 career centers signed; SSO + FERPA review done |

---

## 2. Legal and compliance (all blocking)

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| L1 | Terms of Service, Privacy Policy, Cookie Policy drafted by counsel | CEO + outside counsel | 2027-04-02 | Signed opinion letter in the legal folder |
| L2 | DPIA (GDPR Art. 35) for voice processing, including retention and sub-processors | DPO (fractional) | 2027-04-09 | DPIA document + risk register |
| L3 | Sub-processor list published (ASR, TTS, LLM, hosting, analytics) with DPAs signed | Eng + Legal | 2027-04-09 | DPA PDFs; public list on site |
| L4 | Data deletion and export tested end-to-end (≤ 72 h SLA) | Eng | 2027-04-23 | Test ticket with timestamps |
| L5 | AI disclosure at first use ("you are talking to an AI") + in-app persistent label | PM | 2027-04-16 | Screenshot + copy approval |
| L6 | Age gate (16+) and minor policy; no under-16 onboarding path | PM + Legal | 2027-04-16 | Flow test recording |
| L7 | Comparative-advertising substantiation file: every claim → source, date, screenshot | Research | 2027-05-07 | Folder indexed; legal sign-off |
| L8 | Comparative creative reviewed for US/UK/CA and stricter markets; **no comparative claim publishes unless it is backed by a dated source in `09` §1 and absent from the `09` §5 never-publish list** | Legal | 2027-05-14 | Written approval per market, claim ID cited next to each line |
| L9 | Trademark check on "Eloq" in launch markets; app name and icon cleared | Legal | 2027-01-15 | Search report |
| L10 | Apple/Google policy review: IAP rules, subscription disclosure, account deletion | Eng | 2027-05-07 | Checklist signed |
| L11 | Refund policy, cancellation flow, and pre-renewal notice copy | Finance + PM | 2027-05-07 | Copy in review build |
| L12 | Accessibility audit (WCAG 2.1 AA for web, VoiceOver/TalkBack passes for app) | Design | 2027-05-21 | Audit report + fixes closed |
| L13 | Security: external pen test, findings closed, cyber insurance bound | Eng | 2027-05-21 | Report + remediation log |
| L14 | Voice data: no biometric identification, no ad targeting, 30-day default retention documented | Eng + Legal | 2027-04-23 | Architecture doc + policy text match |

---

## 3. Money

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| M1 | Products configured: Plus $12.99/$79.99, Career $24.99/$149.99, 5 packs, 3 PPP tiers | Eng + Finance | 2027-04-16 | Store console screenshots |
| M2 | Sandbox purchase test on iOS, Android, web for every SKU and every currency | QA | 2027-04-30 | Test matrix, all green |
| M3 | Restore purchases, upgrade/downgrade, proration, grace period | Eng | 2027-04-30 | Test cases in CI |
| M4 | Tax/VAT/GST configured; invoices compliant per market | Finance | 2027-05-14 | Sample invoices per country |
| M5 | Dunning and involuntary-churn recovery (card retry, email sequence) | Eng | 2027-05-07 | Live in staging |
| M6 | Refund + chargeback runbook with thresholds | Finance | 2027-05-14 | Runbook doc |
| M7 | Price localization reviewed by a native speaker per market | Growth | 2027-05-07 | Sign-off table |
| M8 | Revenue reconciliation: store payout ↔ dashboard ↔ warehouse, within 1% | Finance + Data | 2027-05-21 | Reconciled month-0 dry run |

---

## 4. Product and onboarding

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| PC-1 | First session → 6 min to first correction (target < 4 min) | PM | 2027-04-30 | 12-user usability test, median recorded |
| PC-2 | 12 launch scenarios playable end-to-end on 3 device classes | Content + QA | 2027-05-07 | Matrix complete |
| PC-3 | Placement test produces a level + confidence, and a plan | ML + PM | 2027-04-23 | Test accounts at A2/B1/B2 |
| PC-4 | Paywall triggers tested (cap, trend lock, interview library) | Growth | 2027-05-07 | Trigger map + screenshots |
| PC-5 | Free-tier caps enforced client and server side; graceful degradation copy | Eng | 2027-04-30 | Abuse test |
| PC-6 | Deletion, export, pause, and cancel reachable in ≤ 3 taps | PM | 2027-05-07 | Navigation recording |
| PC-7 | Offline drills + SRS sync conflict handling | Eng | 2027-05-14 | Airplane-mode test |
| PC-8 | Crash-free ≥ 99.5% in beta for 14 consecutive days | Eng | 2027-05-24 | Dashboard link |
| PC-9 | Onboarding A/B harness live (so T-04 can run post-launch) | Eng | 2027-05-07 | Flag config |
| PC-10 | Empty states, error states, and "AI is unsure" states designed | Design | 2027-05-14 | Figma + build |

---

## 5. Content

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| C1 | 12 scenarios (4 interview, 4 workplace, 4 campus) with rubrics | Content | 2027-05-07 | Reviewed + versioned |
| C2 | 400-word interview lexicon, 3 role packs (tech, business, healthcare-lite) | Content | 2027-05-14 | Native-speaker review |
| C3 | Correction gold set: 500 items, ≥ 92% precision in CI | ML | 2027-04-23 | CI report |
| C4 | Pronunciation coverage for launch phonemes; drill library mapped | ML + Content | 2027-05-07 | Coverage table |
| C5 | Moderation red-team set (≥ 300 prompts), recall ≥ 95% | Trust & Safety | 2027-05-14 | Red-team report |
| C6 | Cultural review of scenarios for launch markets (names, roles, salary-talk norms) | Content | 2027-05-14 | Review notes closed |
| C7 | Human-review vendor contracted for Career mocks, 48-h SLA | Ops | 2027-05-21 | Signed SOW |

---

## 6. Quality gates (measured, not asserted)

Copy of `06` §7. **Any red line blocks release.**

| Gate | Threshold | Owner | Due |
|---|---|---|---|
| Correction precision | ≥ 92% | ML | 2027-05-14 |
| False-correction rate | < 3% | ML | 2027-05-14 |
| Pronunciation ↔ human r | ≥ 0.85 | ML | 2027-05-14 (see doc `14`) |
| ASR WER read / spontaneous | ≤ 12% / ≤ 22% | ML | 2027-04-23 |
| p50 / p95 first audio | ≤ 1.2 s / ≤ 2.0 s | Eng | 2027-05-14 |
| Moderation recall | ≥ 95% | T&S | 2027-05-14 |
| Minor-safety incidents | 0 | T&S | continuous |
| Data-deletion SLA | ≤ 72 h | Eng | 2027-04-23 |

---

## 7. Analytics and instrumentation

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| A1 | Event taxonomy from `06` §8 implemented; no unnamed events in prod | Data | 2027-05-07 | Schema diff clean |
| A1b | North star (WSSM) and all ten counter-metrics CM-1…CM-10 instrumented, on one dashboard, owners assigned | Data + Product | 2027-05-21 | Dashboard link; screenshot in release folder |
| A2 | Server-side timestamps for funnel and latency; client clock untrusted | Eng | 2027-05-07 | Sample event dump |
| A3 | Warehouse + definitions layer live; one owner per metric | Data | 2027-05-14 | dbt project + metric registry |
| A4 | Attribution: SKAdNetwork/AdAttributionKit + UTM + install referrer reconciled | Growth | 2027-05-21 | Test campaign |
| A5 | Consent-mode analytics; EU users excluded from ad-attribution joins | Eng | 2027-05-07 | Consent test |
| A6 | Cost telemetry joined to session minutes (T-11 in production) | Eng | 2027-05-21 | Dashboard |
| A7 | Weekly report card data pipeline tested on 20 accounts | Data | 2027-05-21 | Sample emails |

---

## 8. Trust, safety, and support

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| S1 | Text + audio moderation live in all launch languages | T&S | 2027-05-14 | Sample verdicts |
| S2 | Report/block/escalate flows; 1-hour escalation SLA for minor-safety signals | T&S | 2027-05-14 | On-call test page |
| S3 | Incident runbook: severity ladder, comms templates, regulator notification path | CEO + Eng | 2027-05-14 | Tabletop exercise run |
| S4 | On-call rota with paging for 30 days post-launch | Eng | 2027-05-24 | Rota published |
| S5 | Help center: 40 articles incl. billing, deletion, score meaning, limitations | Support | 2027-05-21 | Live in staging |
| S6 | Support SLA: email 48 h, priority 12 h; macros and refund script | Support | 2027-05-21 | First-response drill |
| S7 | Status page + incident comms channel | Eng | 2027-05-21 | Test post |
| S8 | Abuse playbook: free-tier farming, trial abuse, referral fraud | Growth + T&S | 2027-05-14 | Detection rules live |

---

## 9. App Store, web, and GTM

| # | Item | Owner | Due | Evidence of done |
|---|---|---|---|---|
| G1 | Store listing: name, subtitle, 6 screenshots (score, correction, interview, plan, report card, privacy), 30-s preview | Design | 2027-05-14 | Asset folder + review notes |
| G2 | ASO keyword set (EN + 2 markets), localized metadata | Growth | 2027-05-14 | Metadata sheet |
| G3 | Privacy nutrition labels match actual data collection (audited against code) | Eng + Legal | 2027-05-21 | Audit checklist |
| G4 | Ratings prompt after 3rd completed session, never after a failure | PM | 2027-05-14 | Flow test |
| G5 | Landing page: promise, 3 proof blocks, pricing, FAQ, deletion link | Design | 2027-05-07 | Live on staging |
| G6 | 5 SEO articles + 1 dated comparison page with legal sign-off | Content + Legal | 2027-05-21 | URLs + approval |
| G7 | Waitlist → launch email sequence (5 emails), suppression rules | Growth | 2027-05-14 | Test send |
| G8 | Press kit: 3 screenshots, founder bio, 2-paragraph pitch, data policy | CEO | 2027-05-21 | Folder link |
| G9 | Creator briefs (5 creators): claim list they may and may not use | Growth | 2027-05-21 | Signed briefs |
| G10 | Launch-day posts drafted: Product Hunt, 2 communities, LinkedIn, X | Growth | 2027-05-28 | Drafts approved |
| G11 | Support macros for launch-week questions (price, privacy, "is this AI", refunds) | Support | 2027-05-28 | Macro list |

---

## 10. No-go criteria (decided now, applied at 2027-06-01)

Launch slips one month if **any** of these is true:

1. Pronunciation ↔ human correlation **< 0.85**, and the fallback (band-only scores, no composite number) is not shipped.
2. Correction precision **< 90%** on the 500-item gold set.
3. Any known minor-safety incident, moderation recall **< 90%**, or the escalation path untested.
4. Deletion or export does not work end-to-end in production.
5. Store review rejected for a policy issue that cannot be fixed in 72 hours.
6. Voice cost per session minute **> $0.025** with no working mitigation, i.e. the unit economics at launch price are structurally negative.

A slipped launch costs roughly $60k in burn and two weeks of learning. A launch with a broken deletion flow or a nonsense score costs the company. The asymmetry is the whole argument.

---

## 11. Launch week runbook

| When | What | Owner |
|---|---|---|
| T-3 d | Freeze config; snapshot pricing and flags; final smoke test | Eng |
| T-1 d | Load test at 5× expected peak; verify rate limits and cost alarms | Eng |
| T-1 d | Brief support and creators; confirm on-call | Ops |
| T-0 06:00 | Release staged rollout 10% → 50% over 6 h | Eng |
| T-0 08:00 | Emails, posts, creator content live | Growth |
| T-0 hourly | Watch: crash-free, activation, latency, cost/min, support tickets | On-call |
| T-0 18:00 | Day-0 read; decide 100% rollout | CEO + Eng |
| T+1 d | First-session funnel read; fix the single biggest drop-off | PM |
| T+3 d | Cost reconciliation vs invoice (not estimate) | Eng + Finance |
| T+7 d | Review against §10 plus activation ≥ 40%, crash-free ≥ 99.5% | All |
| T+14 d | Start T-04 (reverse trial) if traffic supports it | Growth |
| T+30 d | D7 read, CAC read, model re-run, public post-mortem (internal) | CEO + Data |

---

## 12. What is deliberately not on this list

| Not doing at launch | Why |
|---|---|
| Community / pods | Gated on an external safety audit; a launch-day social feature is a launch-day liability |
| Human coaching marketplace | Two-sided supply is a different company; the Career mock is a vendor, not a marketplace |
| Video delivery analysis | On-device only, Phase 2; no launch-blocking value |
| 6+ languages of interface | English-only product; L1 *support* is not localized UI |
| Web app parity | Mobile-first; web is landing + account management at launch |
| B2B console | Phase 3; SSO and FERPA are not week-one problems |
