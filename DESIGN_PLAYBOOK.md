# Roblox Game Design Bible — Research Playbook and Action Plan

**Status:** Research-backed, provisional implementation design — **awaiting source-code audit and owner approval**  
**Date:** 14 November 2026  
**Repository inspected:** https://github.com/cutieyousie-netizen/yousif (default branch: main)

> **Audit limitation:** The connected repository has only README.md (containing "# yousif" and "roblox"). There are **no game scripts or configurations** to inspect. Genre, feature inventory, architecture and current code quality are therefore **unknown**. Every path marked **PROPOSED** below is a suggested future module, **not an existing file**. Do not treat the actions as evidence that the game has any particular feature or bug. No gameplay code has been changed.

## 0. Evidence and research method

**Research sources, in descending order of authority**
1. Official Roblox Creator Hub documentation and developer conference (RDC) presentations.
2. First-hand post-mortems and transcripts supplied by the owner (10 uploaded transcripts, plus the longer supplied transcript text).
3. Third-party developer talks and validated YouTube metadata.
4. The game's own user analytics and playtesting, **once made available**.

**Video-review honesty:** This document contains a **21-video, 5-pillar research register**. Titles, video URLs and topical relevance were verified from official Roblox pages, indexed YouTube descriptions or reliable references. One full RDC 2025 transcript (Top Game Performance Tales) was publicly accessible and reviewed, and the owner supplied extensive verbatim developer transcripts. **We could not directly extract the full captions of the other listed YouTube videos in this environment.** Those entries are annotated as metadata/documentation-assisted research, not falsely presented as full transcript reviews. Some indexed videos discuss related design principles rather than directly providing game-feel implementation instructions.

**Transcript tooling evaluated:**
- [youtube-transcript-api](https://github.com/jdepoix/youtube-transcript-api): selected; small Python dependency, retrieves existing human/automatic captions, no API key or video download required. Proposed command: pip install youtube-transcript-api; Python usage: YouTubeTranscriptApi().fetch(video_id).
- [yt-dlp](https://github.com/yt-dlp/yt-dlp): maintained, very popular and capable; alternative for captions with --write-subs --write-auto-subs --skip-download, but a larger scope and more YouTube dependencies.
- Generic transcription wrappers: not selected due to setup cost and less transparent maintenance.

**Environment result:** pip installation of youtube-transcript-api failed because outbound network/package-registry access is unavailable. Consequently live caption retrieval was **not** performed. This is a research limitation, not a successful extraction.

## 1. Design thesis and falsifiable hypotheses

**Product principle:** Provide an immediately understandable, enjoyable action; make it feel good on every device; turn that action into meaningful progression and social play; give players a reason to return; sell optional, clearly valued enhancements without making the free game miserable.

**The design in three layers:**
- **Micro-loop (seconds):** input -> readable immediate world response -> satisfying feedback -> next action. Examples depend on the actual genre: strike / dodge / hit feedback; collect / reveal reward; place / see construction take effect.
- **Core session loop (minutes):** pursue objective -> perform repeatable gameplay -> earn resource/result -> choose upgrade/new challenge -> re-enter stronger or with more possibilities.
- **Macro-loop (days/weeks):** save meaningful progress -> unlock new strategies/content -> maintain friendships/identity -> return for updates, quests or mastery, without punitive streak mechanics.

**Research-backed rules:**
- Get users to the fun immediately, ideally within the first minute. The exact first-30-seconds target is a **playtest hypothesis**, not an official hard threshold.
- Teach only the first required action and one reward; reveal secondary systems via contextual tutorials. The goal is to learn by doing, not by reading.
- Balance early progression with first-session milestones; watch for stall points. The oft-quoted "next reward in 10–15 minutes" is a useful starting experiment, **not** a universal target.
- Ensure every repeatable action has a legible response (world reaction, animation, short sound and/or unobtrusive particles). Do not rely on screenshake as the sole sign of impact.
- Design mobile-first while testing controller/desktop; no essential input should depend on desktop hover.
- Monetization should be transparent, fair and optional. Do **not** manufacture intentionally frustrating mechanics solely to sell relief.
- Track per-source acquisition and organic Home Recommendation signals separately from paid acquisition.

**2026 discovery correction:** According to Roblox's Discovery FAQ, strongest RFY recommendation signals include **play through rate, first play bounce rate, play days per user and playtime per user**. Also relevant: intentional co-play days, qualified sessions, spend days and Robux spent per user. The signal window now covers D1, D2–7 and D8–28. Roblox explicitly says an unsuccessful initial launch is **not permanently penalized**; ongoing improvements can be re-tested. Do **not** hard-code viral claims ("14-day death", "run ads for exactly seven days", "10-minute sessions guarantee growth") as platform rules.

Official references:
- https://create.roblox.com/docs/discovery
- https://create.roblox.com/docs/discovery-faq
- https://devforum.roblox.com/t/recommended-for-you-algorithm-improvements-that-better-value-long-term-retention/4684575

## 2. Pillar playbooks

### A. Core gameplay loops

**Problem to diagnose:** A technically functional game may still feel purposeless if players cannot state what they are doing, why it matters and what they can work towards.

**Practices**
1. Write a **single-sentence core fantasy** and diagram the interaction -> repeatable action -> progression engine. Require the real first-time playtest to validate it.
2. Give first-time players an immediately available interaction, not a long loading flow or forced tour. The first positive response should be obvious.
3. Make the next meaningful goal visible before the player finishes the current one; early goals should vary in purpose (mechanical mastery, strategy, collecting, expression).
4. Avoid feature accumulation that does not deepen the primary action. One mechanic with combinatorial possibilities can be more effective than five disconnected activities.
5. For every expensive feature ask: does this create new decisions, richer multiplayer moments, or compelling return intent? If no, deprioritize.

**Design artifacts to request from the game owner** after code access: one-sentence pitch, 60-second fresh-player recording, 15-minute session milestone timeline, progression cost table, moment-to-moment feedback inventory.

Official Roblox reference: https://create.roblox.com/docs/production/game-design/core-loops

### B. First-time experience and retention

**Problem to diagnose:** Early players abandon because they cannot locate or understand the first action, must swap tools/inventory unnecessarily, or hit a progression wall before grasping the payoff.

**Practices**
1. Make **first 30 seconds**: spawn safely -> identify action -> perform action -> receive visible payoff. No unsolicited shop popup in this window.
2. Make **30–90 seconds**: repeat the loop, show first progression choice, free the player from tutorial railroading.
3. Use visual signposting, temporary highlights, unobtrusive animated arrows, contextual coaching and timed hints only after inactivity.
4. Give prerequisite items automatically when sensible; teach their acquisition later when genuinely needed.
5. Log explicit funnel steps: Joined -> First Input -> First Core Action -> First Reward -> First Upgrade -> Second Core Action -> Exit / Return. Name these according to the actual game.
6. Track advancement times and failure rates for first upgrades/regions. Instrument **progression funnels** in addition to onboarding.
7. Support sustainable return hooks: persisted mastery, optional daily challenges, social goals and meaningful weekly content. Avoid compulsory daily check-ins, manipulative streak loss or punishing offline decay.

**Evaluate:** FTUE funnel completion by device, 60-second and 180-second bounces, player observations, D1 / D7 cohorts, play days and reasons players state for leaving.

Official Roblox references:
- https://create.roblox.com/docs/production/game-design/onboarding
- https://create.roblox.com/docs/production/game-design/onboarding-techniques
- https://create.roblox.com/docs/production/analytics/retention
- https://create.roblox.com/docs/production/game-design/liveops-planning

### C. UI/UX and cross-device design

**Problem to diagnose:** Tiny touch targets, cluttered HUDs, hidden purchase information, console focus problems and confusing navigation create avoidable churn.

**Practices**
1. Prioritize **one primary gameplay action** and essential status over decorative currencies, repeated banners and low-urgency menus.
2. Use context-sensitive action buttons; surface prompts when the mechanic becomes relevant.
3. Implement responsive layout with UDim2 scale/offset, appropriate UIAspectRatioConstraint, UISizeConstraint, list/grid layout, automatic size where appropriate, device-safe insets and localisation testing.
4. Test smallest supported phones, tablets, desktop and consoles in both Studio emulation and on actual hardware. Check touch reach, camera/action zones, Roblox CoreGui overlap, controller selection and focus.
5. Use consistent semantic typography/colour and brief, interruptible tweens. Reduce or suppress decorative transitions when GuiService.ReducedMotionEnabled is true.
6. Provide an intentionally designed shop hierarchy with precise price, contents, duration and ownership state; avoid UI offer stacks.

**Evaluate:** time to first tap, mis-taps, UI obscuring gameplay, controller navigation coverage, screen size edge cases, readability, UX feedback and A/B test results.

Official Roblox references:
- https://create.roblox.com/docs/production/game-design/ui-ux-design
- https://create.roblox.com/docs/reference/engine/classes/GuiService

### D. Ethical monetization

**Problem to diagnose:** The shop is disconnected from real player needs, purchase flows fail to grant goods, or revenue-oriented progression destroys trust and retention.

**Practices**
1. Put **free-to-play completeness first**: all essential mechanics playable without spending; sell expressive customisation, transparent convenience and optional content.
2. Distinguish one-time **passes** from repeatable **developer products**. Offer a small understandable starter pack only after players experience what it helps.
3. Contextualise offers at natural decision moments (before a run, at a non-disruptive upgrade point, or when returning to a lobby). Provide a clear decline path and frequency cap.
4. Present exact benefits and pricing; avoid misleading FOMO, fabricated scarcity or unverified "discounts." Reward paying players without making PvP unwinnable for non-paying players.
5. Handle developer product receipts **on the server** via MarketplaceService.ProcessReceipt or supported BindReceiptHandler patterns. Make granting idempotent using PurchaseId and durable storage; never grant purchases solely on the client's purchase popup result.
6. Log impression -> open -> initiated purchase -> confirmed receipt, segmented by device and experience tenure. Track payer conversion, revenue per user, repeat spend and refund/complaint signals; guard economy inflation.
7. If testing passes or limited items, add fair free paths, age-appropriate presentation, and clearly disclosed probabilities where relevant.

**Evaluate:** purchase completion reliability, conversion and repeat purchase by cohort, player complaints, effects on D1/D7 and economy sinks/sources. Never make conversion the only success criterion.

Official Roblox references:
- https://create.roblox.com/docs/production/game-design/monetization-foundations
- https://create.roblox.com/docs/production/game-design/contextual-purchases
- https://create.roblox.com/docs/production/game-design/season-pass-design
- https://create.roblox.com/docs/reference/engine/classes/MarketplaceService

### E. Game feel / "juice"

**Problem to diagnose:** The same mechanics can feel unresponsive without immediate, understandable physical and audiovisual feedback; excessive effects can create lag and accessibility problems.

**Practices**
1. For each primary action, define four stages: **anticipation -> input confirmation -> impact / result -> recovery**. Prioritise input response over ornamental effects.
2. Add short, distinct sounds for input, hit, miss, collect, equip, success; route to SoundGroups with separate volume controls.
3. Use restrained particles/trails for important impacts and rewards. Reuse pooled objects where sensible, cap emit rates and test low-end device budgets.
4. Treat camera shake, hit stop, time dilation and flashing as configurable **client-only** presentation. Keep gameplay outcome server-authoritative and allow intensity/reduced-motion controls.
5. Use timely animation markers and clear windups for combat; avoid making essential signals only audible or only colour-coded.
6. Profile real devices and monitor crashes/latency. A high-particle celebration that causes mobile stutters harms the sensation of responsiveness.

**Evaluate:** input-to-feedback perceived lag, player comprehension of hits, real-device frame rate, sound clarity, reduced-motion behaviour and per-action fun ratings.

Official Roblox references:
- https://create.roblox.com/docs/education/build-it-play-it-island-of-move/animations-and-feedback
- https://create.roblox.com/docs/performance-optimization
- https://create.roblox.com/docs/reference/engine/classes/GuiService

## 3. Prioritized implementation action plan — requires actual game source

**IMPORTANT:** No current source paths exist in the inspected repository. All module paths below are **PROPOSED** and must be reconciled with the real project before implementation. Do not create these code files until review is approved.

### P0 — Must address before paid acquisition or growth push

| ID | Technique and evidence | Why it matters | PROPOSED Luau / Roblox architecture | Success test |
|---|---|---|---|---|
| A01 | Explicit onboarding + progression funnels; owner's Raise Anomaly/Hack a Business post-mortems, RDC 2024 Analytics, AnalyticsService docs | Reveals whether churn comes from confusion, input or balancing | src/server/Services/AnalyticsService.luau + src/shared/AnalyticsEvents.luau; server emits LogOnboardingFunnelStepEvent and LogProgressionEvent/LogCustomEvent with stable event names | All main first-session stages visible by device; biggest drop-off identifiable |
| A02 | Get to fun in first 30s, contextual tutorial; Roblox Onboarding Techniques + owner transcripts | Reduces first-play bounce and cognitive overload | src/client/Controllers/OnboardingController.luau; src/shared/OnboardingSteps.luau; subscribe to real game state, display short visual prompts, cancel/skip, hints only on inactivity | First core action achievable without text manual; 60s/180s bounce improves in measured test |
| A03 | Show outcome, reward, next objective; official Core Loops and owner's progression case study | Establishes loop comprehension and momentum | src/server/Services/ProgressionService.luau + src/shared/ProgressionConfig.luau; server owns rewards and milestones; client HUD subscribes to replicated progress | Test players can explain the loop, perform two cycles, and locate next meaningful milestone |
| A04 | Mobile-first HUD + complete controller path; Roblox Learn Mobile UI panel and UI/UX docs | Removes avoidable cross-device abandonment | src/client/Controllers/HUDController.luau and InputController.luau + src/shared/UITheme.luau; responsive constraints and per-device contextual actions | Small-phone gameplay unobscured; primary action usable on touch, mouse and gamepad |
| A05 | Real-device performance gate; RDC 2025 Top Game Performance Tales + RDC 2024 performance | Heavy effects and memory failures can destroy retention | QA/performance-checklist.md; instrument client errors and monitor published crash/frame metrics; review world assets and animations once source exists | Stable first session on low-end devices; no crash spikes after deployment |

### P1 — Follow once core experience is measurable

| ID | Technique and evidence | Why it matters | PROPOSED Luau / Roblox architecture | Success test |
|---|---|---|---|---|
| A06 | Remove economic progression cliffs; owner's Raise Anomaly post-mortem + Roblox retention docs | Supports longer sessions and D1 intent | src/shared/EconomyConfig.luau + src/server/Services/EconomyService.luau; centralize prices/reward growth, version balancing values, log first 5–10 upgrades | Reduced stall time without destroying later economy; first upgrades actually reached |
| A07 | Reliable saved progression; long-loop principle from Roblox Core Loops and Retention | Gives players a reason to return | src/server/Services/ProfileService.luau; DataStoreService:UpdateAsync with schema version, retry/error policy, server authoritative validation | Rejoin recovers progress and entitlements; recovery tests pass |
| A08 | Daily/weekly optional quests + social milestones; Roblox LiveOps and season pass docs | Improves play days and D7 through meaningful goals | src/server/Services/QuestService.luau; src/shared/QuestDefinitions.luau; server-validates progress; offer free path and catch-up | D1/D7 and quest participation improve without negative player reports |
| A09 | Satisfying audio/VFX/animation feedback; Roblox animations/feedback docs, accessibility panel | Makes repeated interactions feel better and outcomes legible | src/client/Controllers/FeedbackController.luau + src/shared/FeedbackCatalog.luau; local-only camera/audio/VFX, central effect budgets, reduced-motion option | Player tests rate feedback clearer; no significant frame/crash regression |
| A10 | Server-side ethical purchase lifecycle; Roblox MarketplaceService + monetization docs | Prevents entitlement loss and protects trust | src/server/Services/PurchaseService.luau + src/shared/OfferCatalog.luau + src/client/Controllers/ShopController.luau; idempotent receipt processor, verified ownership, non-disruptive offers | Every test purchase granted exactly once; prices/contents clear; no blocking paywall |
| A11 | Gameplay feedback collection and weekly hypotheses; owner Hack a Business case study | Gives qualitative explanation for quantitative drop-offs | src/client/Controllers/FeedbackControllerUI.luau (separate from impact feedback) + moderated feedback storage; maintain docs/experiment-log.md | Every update has hypothesis, cohort/date, measured outcome and rollback criterion |

### P2 — After stable baseline and first successful tests

| ID | Technique and evidence | Why it matters | PROPOSED Luau / Roblox architecture | Success test |
|---|---|---|---|---|
| A12 | LiveOps cadence and events; RDC 2024 LiveOps and official LiveOps docs | Builds return occasions without endless progression grind | src/server/Services/LiveOpsService.luau + src/shared/EventConfig.luau; event states/eligibility on server, limited cosmetics with honest timings | Post-event D7 and sustained engagement improve versus pre-event baseline |
| A13 | Art/packaging testing + acquisition separation; official Discovery documentation and owner case studies | Improves impression-to-play while avoiding misleading ads | No gameplay script required initially; creative variants, analytics acquisition cohorts, clearly matching icon/title/experience | Organic Home PTR/bounce improves; paid effects analysed separately |
| A14 | Controlled UX and offer tests; Roblox Experiments/Configs, Monetization docs | Avoids guessing and shipping many competing changes at once | Versioned configs, kill switches and feature flags appropriate to deployed architecture | A/B or staged test yields interpretable improvement without disproportionate fairness complaints |

### Order of operations

1. Obtain actual game source and classify genre, remotes, UI hierarchy, current state/data persistence, economy and purchases.
2. Record a complete fresh-account playthrough on phone and desktop; diagram the actual core loop and timed unlocks.
3. Implement analytics instrumentation and identify the worst **high-impact, adequately sampled** funnel bottleneck.
4. Fix onboarding, loop clarity or responsiveness first; re-measure before adding expensive content.
5. Balance progression and data persistence; then ethical offers and meaningful return hooks.
6. Introduce events and ads only after organic user response supports the experience.

Use **research -> hypothesis -> minimal change -> controlled test -> keep/revert -> repeat**. Avoid making five major updates simultaneously because the resulting data will not identify which change helped.

## 4. Proposed project structure (not present in repo)

Use the real existing convention if possible (Rojo, Studio-native, Knit, Aero, Flamework, etc.). Do **not** force a rewrite for cosmetic consistency. A potential Rojo structure, only if justified by actual source:

- default.project.json
- src/shared/AnalyticsEvents.luau
- src/shared/ProgressionConfig.luau
- src/shared/EconomyConfig.luau
- src/shared/UITheme.luau
- src/shared/OfferCatalog.luau
- src/shared/FeedbackCatalog.luau
- src/server/Services/AnalyticsService.luau
- src/server/Services/ProgressionService.luau
- src/server/Services/EconomyService.luau
- src/server/Services/ProfileService.luau
- src/server/Services/PurchaseService.luau
- src/server/Services/QuestService.luau
- src/server/Services/LiveOpsService.luau
- src/client/Controllers/OnboardingController.luau
- src/client/Controllers/HUDController.luau
- src/client/Controllers/InputController.luau
- src/client/Controllers/FeedbackController.luau
- src/client/Controllers/ShopController.luau
- docs/experiment-log.md
- QA/performance-checklist.md

**Architecture guardrails:** Server validates rewards, progression, prices, purchases and competitive outcomes. Client owns HUD, input translation, camera and lightweight audiovisual feedback. Remotes must have narrow schemas, rate limiting where needed, and validation. Save data on the server; never trust client-advertised balances. Preserve and extend the real codebase rather than duplicating functionality.

Roblox API references:
- https://create.roblox.com/docs/reference/engine/classes/AnalyticsService
- https://create.roblox.com/docs/reference/engine/classes/MarketplaceService
- https://create.roblox.com/docs/reference/engine/classes/GuiService

## 5. Video research register — 21 verified videos (4–5 per pillar)

**Reading key:** **D** = supported by official Roblox docs or video description/talk listing; **T** = accessible full caption transcript reviewed; **U** = topic reinforced by owner-provided full transcripts (not necessarily this named video). A **D** item is *not* a claim that this video's full transcript was extracted.

### Core loops — 4 videos

1. **What's a core loop on Roblox?** — Roblox Learn, 2023. [Video](https://www.youtube.com/watch?v=gkFKF9A-snY). **D**. Use: define repeated action and progression engine; supported by official Core Loops docs.
2. **Deep Systems, Deep Engagement: Building Complex RPG Mechanics | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=qLP05zvMsW0). **D**. Use: identify when progression depth creates choices, not confusing feature sprawl.
3. **Build Games That Bring Players Together | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=LIKiUlkTqZc). **D**. Use: potential shared gameplay/social macro-loop design.
4. **What Drives Discovery: Understanding the Algorithm | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=bkRZeTZAvLw). **D**. Use: validate why engaging loops and first-session comprehension matter to discovery; cross-check against official Discovery FAQ.

### Retention, FTUE and LiveOps — 4 videos

5. **What are onboarding techniques on Roblox?** — Roblox Learn, 2023. [Video](https://www.youtube.com/watch?v=dXqZC4x2Vn8). **D**. Use: visual elements, contextual tutorials and timed hints.
6. **What are retention metrics on Roblox?** — Roblox Learn, 2023. [Video](https://www.youtube.com/watch?v=LpAU6TheAZ4). **D**. Use: cohort interpretation, D1/D7 and diagnosis.
7. **Using Analytics to Grow and Improve Your Experience | RDC 2024** — Roblox, 2024; panel of Roblox and creators. [Video](https://www.youtube.com/watch?v=QC6XWgJRJEM). **D**. Use: onboarding, economy and retention funnels.
8. **Finding Success with your LiveOps Strategy | RDC 2024** — Roblox, 2024; developer team talk. [Video](https://www.youtube.com/watch?v=DxrLfwsfV1I). **D**. Use: roadmap, planned update cadence, player-facing event delivery.

### UI/UX — 4 videos

9. **Mobile UI/UX for Roblox with Cindering and UndoneBuilder** — Roblox Learn, 2023. [Video](https://www.youtube.com/watch?v=BsyU-SJ9L-c). **D**. High-value indexed chapters: scale/offset (11:07), aspect constraints (12:34), mobile-first (26:20), reducing friction (38:07), UX analytics (43:08).
10. **Mobile UI/UX for Roblox Q&A with Cindering and UndoneBuilder** — Roblox Learn, 2023. [Video](https://www.youtube.com/watch?v=PjwJb_nSePY). **D**. Chapters: controller support (07:16), grid/list/scroll (08:53), testing and feedback (11:00), limited screen space (14:13).
11. **UI Frameworks Panel | RDC 2024** — Roblox developers, 2024. [Video](https://www.youtube.com/watch?v=OHqMLEL5QnY). **D** via a sourced technical reference. Use: large UI state and consistency; library choices require inspection of real project.
12. **UI and UX Design** — official video embedded in Roblox Creator Hub. [Video](https://www.youtube.com/watch?v=lOOvOIJoMi4). **D**. Use: hierarchy, attention, context-sensitive UI; directly supported by current official UI/UX documentation.

### Monetization — 4 videos

13. **Mastering Monetization: Lessons from Top Creators | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=hoMbv_R8AMU). **D**. Use: prioritize offers to test against official monetization principles, rather than equate spend with fun.
14. **Monetizing Intellectual Property | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=oxiaIhN5Ybo). **D**. Relevant mainly if a properly licensed IP/brand partnership exists; do not assume the current game has one.
15. **Season Pass Design** — official video embedded in Roblox Creator Hub. [Video](https://www.youtube.com/watch?v=k2gbQI-ggB4). **D**. Use: free/premium track fairness, manageable tasks and realistic pass duration.
16. **Avatars at the Center: Driving Gameplay, Identity, and Commerce | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=gCp4zzjjJ14). **D**. Use: identity/expression as potential non-pay-to-win value.

### Game feel, responsiveness and performance — 5 videos

17. **Mastering Server Authority to Build Competitive Multiplayer Games | RDC 2026** — Roblox, 2026. [Video](https://www.youtube.com/watch?v=9IqNHhYXK0s). **D**. Use: separate trusted game outcomes from responsive local presentation, pending actual game's genre.
18. **Top Game Performance Tales | RDC 2025** — Roblox / Peter McNeill and Lynn, 2025. [Video](https://www.youtube.com/watch?v=rwLEnBtXr30). **T** full transcript reviewed at https://prepublish.ai/youtube-transcript/rwLEnBtXr30. Specific case studies: Dead Rails animating too many distant NPCs and high physics cost; Grow a Garden real-device memory/crash problems and an over-complex model. Use: performance is part of feel; test real hardware and stress test worst-case worlds.
19. **Using Roblox Tools to Improve Performance | RDC 2024** — Roblox / MrChickenRocket, 2024. [Video](https://www.youtube.com/watch?v=cWDNVvOh4o0). **D**. Use: rendering and diagnosis; never ship unprofiled cosmetic overload.
20. **Designing for Accessibility with BitwiseAndrea, WooleyWool, and ControlCoreAngel** — Roblox Learn, 2023. [Video](https://www.youtube.com/watch?v=K1pEI6LVJJA). **D**. Indexed chapters cover visual/auditory/motor accessibility, epilepsy and migraines. Use: accessible shake, colour, flash and audio options. For current ReducedMotionEnabled API refer to Creator Hub, not an old video.
21. **Finding Your Art Direction | RDC 2024** — Roblox / Gino Roy, 2024. [Video](https://www.youtube.com/watch?v=vWx8UTxsi0A). **D**. Use: visual clarity and environmental readability, supporting game feel; source is more art direction than hit effects.

**Priority when caption access becomes available:** Retrieve and review videos 2, 7, 9, 13, 17, 18 and 20 first. Save per-video timestamped evidence, counterexamples, limitations and exactly which changes survive a test in **this** game's genre. Do not infer actual quote details from a title.

## 6. Evidence from owner-supplied full transcripts

The provided developer transcripts gave concrete examples, but their claimed numerical benchmarks are not automatically Roblox policy.

- **Steal a Superstar**: immediately understandable steal -> passive cash -> upgrade/rebirth sequence. Claimed D1/D7 and conversion outcomes are an anecdote about one game's audience, not a universal threshold.
- **Hack a Business**: developer compared player feedback, competitor mechanic and time-of-session retention before making one change, then re-measured.
- **Raise Anomaly**: removed unnecessary equipping/food-shopping from first-time onboarding; taught food acquisition only once needed; logged the steps where users quit.
- **Raise Anomaly progression post-mortem**: fresh-account testing and timestamped milestones exposed first-upgrade and mid-game price cliffs; progression changes reportedly improved D1. Do not assume those fixes apply to unrelated genres.
- **Build a Base and Steal**: creators emphasized one simple mechanic with deep strategy, social moments and performance on console/mobile.
- **Combat game relaunch case study**: targeting a more specific player audience and changing presentation/progression reportedly correlated with sharp CCU growth; avatar appearance is not reliable evidence of a user's age or purchasing ability and should not be used to stereotype players.
- **Farmer Die / Alien Ranch research method**: look for proven but underserved gameplay and improve quality, progression and reliability rather than making a near-identical clone.
- **Production/hiring talks**: prototype the smallest fun loop, define written scope, provide references, playtest early, use a cohesive style guide and avoid adding systems until the core is validated.

## 7. Audit table and approval gate

| Audit item | Finding |
|---|---|
| Repository identity | cutieyousie-netizen/yousif, public, main |
| Root tree | README.md only |
| README contents | "# yousif" and "roblox" |
| Project format | Unknown: no .rbxl/.rbxlx, Rojo project, scripts or other game files |
| Game genre and core loop | Unknown |
| Existing FTUE, HUD, remotes, data, monetization, VFX | Not inspectable |
| Actual script-to-recommendation mapping | **Blocked**: do not invent existing file references |
| Code changes | **None** |
| Proposed module architecture | Documented above, not implemented |

**Approval gate:** The owner must provide the actual Roblox Studio project or synchronised Luau source (or connect the GitHub repo containing it). Once available, update this file with verified **existing** paths and a concrete change-by-change diff plan. Before any coding, agree on the first two or three measurable, highest-impact interventions and the success/rollback criteria.

**Nothing in this document authorises game-code implementation.**
