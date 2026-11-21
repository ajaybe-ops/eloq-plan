# Eloq

**Small, timeboxed voice rooms for conversations worth having.**

> Tap once, get a room worth fifteen minutes with three to five other people — and no way for anyone to message you afterwards.

**Plan v6.0 · locked 2026-11-18 · pre-launch, Austin first**

---

## Start here

| Time | Read | Why |
| --- | --- | --- |
| **2 min** | This page | What the product is, what is locked, what it costs |
| **10 min** | [`live/11`](live/11-build-and-launch.html) §0, then [`live/10`](live/10-execution-lock.html) §1 | The plan on one page, then the five locked decisions |
| **30 min** | [`live/09`](live/09-v5-master-plan.html) → [`10`](live/10-execution-lock.html) → [`11`](live/11-build-and-launch.html) | Product, monetization, execution |
| **Building it** | [`live/11`](live/11-build-and-launch.html) §5 | Stack, six two-week sprints, exit criteria |
| **Funding or operating it** | [`live/10`](live/10-execution-lock.html) §5–6 | Unit economics, break-even, kill signals |
| **Safety review** | [`live/11`](live/11-build-and-launch.html) §4 | Vibe Check, the report buffer, enforcement |

The plan is a static site. To read it as intended:

```bash
git clone https://github.com/ajaybe-ops/eloq-plan.git
cd eloq-plan
python -m http.server 8000
# open http://localhost:8000/live/
```

No build step is required; the rendered HTML is committed.

---

## The product in six sentences

1. You open the app and tap one topic.
2. It puts you in a room with three to five people who chose the same one.
3. You get fifteen minutes, a prompt if you want one, and a balance meter.
4. A quiet hairline shows the time; the controls disappear after six seconds.
5. If someone is a problem, one long-press removes them and the room continues.
6. At the end you get three takeaways and one question to come back to.

```
open → pick a topic → match → 15:00 room → recap
```

No profiles to browse. No follower counts. No stage. No DMs. The room is the whole product.

**How a room forms, in order**

1. **Trusted-first.** A new account is only matched into a room that already holds a trusted speaker. Nobody's first room is four strangers who are all also new.
2. **Rostered ping.** If no room can form, a rostered speaker for that topic gets one silent ping. If they take it, the room opens.
3. **AI rescue.** After 60 seconds with two people waiting, a labelled AI co-host can join for up to 3 minutes. If the room still has fewer than two humans when the seat expires, it closes rather than runs thin.

**What this is not:** a feed, a creator platform, a dating app, or a continuous-recording product. Audio leaves the device only when someone files a report, and then only the last 30 seconds.

---

## What is locked

These decisions are closed. Changing one requires a written reversal trigger from [`live/10`](live/10-execution-lock.html).

| # | Decision | The short version |
| --- | --- | --- |
| **D1** | Free cap | **30 min/day and 90 min/week.** The weekly cap contains cost; the daily cap does not bind for most users. First three rooms (or 48 hours) are uncapped so a new user finishes a conversation before seeing a limit. |
| **D2** | Pro price | **$19.99/mo · $199/yr at launch.** A $24.99 test waits until the practice record and voice feedback ship. Pro is the business: at a 35% mix, break-even is 4.2%; Plus alone needs 6.7%. |
| **D3** | Vibe Check | **Remove the person, not the room.** Two weighted reports remove a participant instantly. `productivity_score` moves only after a human upholds an inappropriate-content report. |
| **D4** | AI co-host | **Paid rooms and a capped free rescue.** After 60 seconds with two people waiting: max 3 minutes, max once per user per day, always labelled. |
| **D5** | Room length | **15 minutes for topic rooms, 10 for practice.** A topic needs time to get past positions; a drill does not. |

Also closed:

- **18+ at launch.** 16–17 only after a specific safety review. Any confirmed minor in an 18+ room is a hard stop.
- **Five taps to a room:** Welcome → Topic → 18+ → Phone OTP → Join. No email, name, photo, or profile.
- **One primary action per screen.** Any screen needing a second decision goes back to design.
- **No messaging graph.** A room ends and the people in it cannot contact each other. That is the product, not a missing feature.

---

## The business

| | **Free** | **Plus** | **Pro** |
| --- | --- | --- | --- |
| **Price** | $0 | **$9.99/mo · $79.99/yr** | **$19.99/mo · $199/yr** |
| **Live rooms** | 30 min/day · 90 min/week | Unlimited, fair use 120 min/day | Unlimited, fair use 180 min/day |
| **Standard + Practice rooms** | Yes | Yes | Yes |
| **Expert rooms** | — | Yes | Yes |
| **Career / interview rooms** | 1 trial | Yes | Yes + voice feedback |
| **AI recap** | 1 per week | Unlimited | Unlimited + action items |
| **Transcript / export** | — | Transcript | Transcript + export |
| **Priority matching** | — | 2× queue weight | 4× queue weight |
| **Trial** | — | 7 days on annual only | 7 days on annual only |

The free tier limits the **expensive** resource — speaking minutes — never the room itself. A capped user finishes the conversation they are in; safety tools and the three recap takeaways are never sold.

**Unit economics, base case**

| Metric | Value |
| --- | --- |
| Cost per 15-minute room | **$0.068** |
| Maxed free user | **$0.94/month** at 90 min/week |
| Average free MAU | 5.4 rooms/month (81 minutes) |
| Break-even conversion | **4.2%** at a 35% Pro mix (5.3% at 28%, 6.5% at 20%) |
| Planned conversion | **4.2% (Y1) → 5.8% (Y2) → 7.0% (Y3)** |
| Launch CAC | **~$9**, not $3.50 |
| Austin 90-day plan | **$24k committed**; variable acquisition capped at **$10–14k** |

The AI co-host costs **$0.03–0.06/minute** — $0.45–0.90 for a 15-minute room, or 7–13× an entire human room. That is why it is paid, capped, and labelled rather than ambient.

Full model and sensitivities: [`live/10`](live/10-execution-lock.html) §5. The one-line version: **Plus exists to convert; Pro exists to pay for the free tier.**

---

## How it is built

| Layer | Choice | Why |
| --- | --- | --- |
| Client | **React Native + Expo**, bare workflow | One codebase; LiveKit's mobile SDK is mature; native audio work stays contained |
| Audio / SFU | **LiveKit** | Server-side `RemoveParticipant`, data channels, simulcast, Apache-2.0 self-host path |
| Backend | **TypeScript (NestJS)** | Typed contracts with the client; fast iteration |
| Database | **Postgres** | Rooms, reports, entitlements; JSONB for takeaways |
| Cache / queue | **Redis**, **SQS** | Sub-millisecond counters; durable ASR retries |
| VAD | **Silero VAD v5** via ONNX Runtime Mobile | 1.8 MB, <1% CPU, no vendor |
| ASR | **faster-whisper / CTranslate2** on L4 | 40× realtime at batch 8; API until ~2.5M speaker-min/month |
| Storage | **S3**, 7-day audio lifecycle | Audio never lives in the database |
| Payments | **StoreKit 2** + **Play Billing 7** | Server-side validation; one subscription group |
| Analytics / flags | **PostHog** self-hosted, **Unleash** self-hosted | No ad SDKs; event ownership |
| Observability | **OpenTelemetry → Grafana**, **Sentry** | One trace from join to recap |

**Four invariants the build must not break**

1. A LiveKit token is minted **only after** the entitlement check passes. The client never decides whether it has minutes.
2. The mic is **not** continuously transcribed. On-device VAD selects speech; the server transcribes a 6-minute window, a 5% safety sample, and a 30-second clip that exists only if someone reports.
3. A Vibe Check calls `RemoveParticipant` and adds a room-level deny entry. It never ends the room and never touches a score.
4. Duration is server truth. A client-reported number is clamped to the server's elapsed time; the LiveKit webhook reconciles the rest.

---

## What is verified — and what is not

Every material figure is sourced, derived, or tagged as a hypothesis with a test:

| Tag | Meaning |
| --- | --- |
| **(V)** | Verified against a dated public source |
| **(D)** | Derived by arithmetic over verified inputs |
| **(H)** | Hypothesis — no public evidence; has a test ID and a cost |
| **(X)** | Decision or commitment, not a factual claim |

**Verified:** competitor pricing and features, store fees, ASR/TTS list rates, category subscription benchmarks.

**Not verified — and treated as hypotheses with dated tests:** our conversion, churn, CAC, retention, voice cost under our own load, safety rate at density, and whether the group format forms a habit. The tests that settle them are in the execution plan; none of these is quoted publicly as a fact.

> If a number cannot be traced to a source, a calculation, or a dated test, it does not go in the plan.

---

## What would make us kill it

Written before the build, so it cannot be rationalised later.

| Checkpoint | Threshold | If missed |
| --- | --- | --- |
| **Day 30** | P90 time-to-room ≤ 90s · D7 ≥ 25% · reports ≤ 3/1k room-min · zero minor incidents | Concentrate to one topic; freeze growth; stop on any minor incident |
| **Day 60** | DAU ≥ 700 · P90 ≤ 45s · D7/D30 ≥ 30%/15% · conversion ≥ 4% · Pro share ≥ 25% · CAC ≤ $35 | Drop to three topics; pivot to cohort rooms; kill paid acquisition |
| **Day 90** | DAU ≥ 2,000 · P90 ≤ 30s · D30 ≥ 18% · conversion ≥ 5.5% · Pro ≥ 30% · GM ≥ 30% | Stop paid growth; collapse Pro; pivot to a cohort/B2B2C product |

**The two hard stops**

1. **Any confirmed minor in an 18+ room.** Matching stops immediately, an external audit follows, and there is no relaunch without a new verification vendor and a public report.
2. **Day 90 with DAU < 800 and D7 < 20%.** The group format has not found a habit. Stop the consumer product, return remaining capital, or pivot to a cohort model where the buyer supplies the density.

Slow revenue in month one, a competitor launch, or a bad press cycle are **not** kill signals. The numbers above are structure.

---

## Repository map

```
.
├─ README.md              ← you are here
├─ live/                  ← current plan (v6.0), rendered
│  ├─ index.html          ← start here
│  ├─ 09-v5-master-plan.html
│  ├─ 10-execution-lock.html
│  ├─ 11-build-and-launch.html
│  └─ prototype.html      ← clickable onboarding → room → recap
├─ raw/                   ← markdown copies
│  ├─ README.md           ← this page
│  ├─ README-v2.md        ← earlier AI-tutor plan overview
│  ├─ 01-product-spec.md … 14-pronunciation-validation.md
│  └─ EXEC-SUMMARY.md · NEXT-14-DAYS.md
├─ *.html                 ← rendered archive of the earlier plan
└─ style.css · robots.txt
```

**Two plan sets live here.** The current product is the **live-audio network** in `live/`. The earlier **AI English-tutor** plan in `raw/` (`README-v2.md` and the root HTML files) is retained as record — it is where the safety architecture, the pricing anchors, and the evidence discipline came from, but it is not the product being built. If the two are ever shown to the same person, the live plan is the product and the tutor is a feature (Pro interview rooms).

---

## Status

- **Plan:** locked at v6.0. Open items are listed at the end of [`live/10`](live/10-execution-lock.html) §7 — self-hosted ASR timing and the Pro feature bundle.
- **Build:** implementation in progress. This repository is the plan of record, not the app source.
- **Launch:** Austin first, one prime topic per evening, 2,000 DAU target at day 90.
- **License:** proprietary. All rights reserved. This is an internal planning repository; no license is granted for reuse.

---

<sub>Eloq v6.0 · 2026-11-18 · material figures are verified, derived, or tagged as a hypothesis with a test.</sub>
