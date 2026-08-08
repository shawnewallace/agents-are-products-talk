# Agents Are Products, Not Prompts
### CincyDeliver 2026 · 60-minute session · Outline v4

**Core thesis:** AI-assisted development breaks down not because the model fails, but because the practice was never engineered to scale past the person who built it. Treat agent creation as software engineering — an operationalized team practice, not a hero's personal prompt collection.

**Through-line:** The discipline we already apply to code — version control, review, testing, lifecycle, deprecation — is exactly what agents need. *Operationalize AI-assisted development so it doesn't depend on hero developers.*

**Audience takeaway:** A maturity model to locate your team, and a repeatable, rigor-driven process for designing and maintaining agents as products.

**Time budget:** ~52 min content + ~8 min Q&A.

> **Source material:** Part 2 of the Centric GitHub Copilot workshop (`ai-code-workshop`) — flagged **[from workshop]** with paths. Intro framing draws on Shawn's blog *"Wishful Thinking?"* (shawnewallace.com, 2026-06-17) — flagged **[from blog]** — and Shawn's own *Agentic AI Maturity Model* slide (§3). The workshop already lands the thesis — *"Agents are products, not prompts. Design, test, and maintain them like code"* (`part2/05-agent-design.md`).

---

## 1. Cold open — the practice that only worked for one person (3 min) — *[anonymized, real]*
- Open on a real story: an engineer built out a set of AI-assisted agents solo — in a vacuum, no team input, no design review — refining them alone until they worked exactly the way they wanted. Genuinely good work. Then the team inherited the assets, not the judgment behind them: nobody had been part of shaping the constraints, nobody understood why the agent was scoped the way it was, nobody trusted output they hadn't helped build. Adoption stalled. Concrete, specific, a little painful.
- Reframe: *the model didn't fail — the practice was never designed to be handed off. It was a hero's workflow, not an engineered artifact.*
- Promise: leave able to operationalize AI-assisted development as a team or enterprise practice — agents you can maintain, test, hand off, and change without fear.

## 2. Code vs. software: why hero developers don't scale (5 min) — *[from blog]*
- **AI is good at code, not software.** It's a genuine accelerant for boilerplate and execution, but a system is a set of decisions — structure, boundaries, tradeoffs, "is it done / is it correct" — and that judgment is still human.
- **The split no one's naming:** AI amplifies senior engineers with taste, and quietly leaves juniors behind. A junior can now ship code that *looks* senior without understanding it.
- **The hero trap:** if your AI-assisted practice works only because a few senior "heroes" know when to trust the output and when to push back, you don't have a practice — you have individual heroics. That judgment is trapped in their heads. It doesn't scale, and (the preceptorship problem) it doesn't develop the next generation.
- **The real wishful thinking:** hoping this just works out on its own. The alternative is to *operationalize* — encode that hard-won judgment into engineered artifacts the whole team uses. (Ties to Shawn's companion posts: *encoding process into artifacts* / *the instructions are the process*.)

## 3. The Agentic AI Maturity Model (4 min) — *the roadmap for the talk*
Shawn's own model — *Agentic AI Maturity Model: Coding & Application Modernization*. Five levels of integration, each raising the AI/human ratio and shifting the human role. Two things to trace as you climb: individual productivity **and** organizational capability, and the human role shifting **Producer → Reviewer → Director**.
- **L1 — AI Autocomplete** · IDE plugin · inline suggestions, rarely beyond the editor · 10% AI / 90% Human · ~10–15% lift · role: **Producer**.
- **L2 — AI Chat** · chatbot / sidebar · conversational explain, refactor, generate snippets · 20% AI / 80% Human · ~20–25% · role: **Producer**.
- **L3 — AI Assist** · Copilot / IDE agent · multi-step edits across files; human reviews and ships · 50% AI / 50% Human · ~25–50% · role: **Reviewer**.
- **⚡ THE CAPABILITY GAP (between L3 and L4)** — the hard jump from "AI assists, a human ships every change" to "agents run long-running work and a human directs." You cannot cross it with prompted heroics; crossing it *requires* engineered, governed agents. **This gap is the whole reason for the talk.**
- **L4 — Agentic Augmented** · long-running agents · background tasks, PR creation, narrated cloud workflows · 75% AI / 25% Human · ~1x–5x · role: **Director**.
- **L5 — Agentic Adaptive** · agents as automation · self-directing systems; humans set goals and review outcomes · 90% AI / 10% Human · ~10–20x · role: **Director**.
- **Tie to the intro:** the Producer→Reviewer→Director shift *is* the move off hero-dependence — humans stop being the bottleneck producer and start directing an engineered system. And the capability gap is exactly where "agents are products, not prompts" stops being a slogan and becomes the requirement.
- **Position the rest of the talk:** §5–6 (engineering agents) and §8 (maintenance rigor) are *how you cross the capability gap* into L4–L5.

## 4. Why agents fail: prompt engineering ≠ software engineering (4 min)
- The trap that keeps teams stuck below the capability gap: an agent is one text box away from "working," so they stop there — no source control, no tests, no review.
- Three symptoms of a prompted-not-designed agent: **inconsistent** (same input, different behavior) · **unmaintainable** (one giant prompt) · **brittle** (requirements shift, it quietly breaks).
- **[from workshop]** Common pitfalls (`part2/05-agent-design.md`): task-based agents · vague instructions · over-scoping · no testing · set-and-forget.

## 5. Design rigor: the framework for engineering an agent (9 min)
- **[from workshop]** Capability hierarchy (`part2/03-custom-agents-intro.md`): **Prompts** · **Instructions** · **Skills** · **Agents** — the same ladder as the maturity model; agents are the engineered end.
- **New — where information belongs (added 2026-07-23):** "Right layer compounds. Wrong layer costs you." Instructions are small and non-negotiable — every task pays for them, so overloading them taxes every call. Skills are on-demand — real procedure, loaded only when triggered, so depth there is close to free, but buried/mis-triggered skills never fire. Agents are a fully separate context — right when the scope justifies dedicated tools and workflow, wrong (dead weight to maintain) when spun up for something a skill could've handled. Punchline ties to the talk's software-engineering-rigor thesis: *"Same rigor as any interface: get the layer right and it compounds — get it wrong and it costs you."* This is a design decision, not a dumping ground.
- **Agent Components model [from workshop]** (`part2/05-agent-design.md`): Identity & Role · Responsibilities · Context · Constraints · Process · Output Format · Tone — plus frontmatter (`name`, `description`, `tools`, `model`, `handoffs`). A system with named parts, not a paragraph.
- **[from workshop]** Design process (`docs/guides/agent-design-guide.md`): define problem + success criteria → identify role → set scope and explicit out-of-scope → design output format. Requirements-and-design work, not prompt tinkering.
- **[from workshop]** Three patterns (`part2/05-agent-design.md`): **role-based scope** (WHO not WHAT) · **explicit constraints** (ALWAYS/NEVER) · **structured outputs** (defined sections).
- **You don't have to invent this from a blank page** — the industry has already converged on this component pattern in open-source libraries (more in §9).

## 6. Live decomposition of a production agent (12 min) — *the centerpiece*
Two beats: the template, then proof it's real.
- **Beat 1 — decompose the template.** `demo/architecture-reviewer.agent.md` **[from workshop, adapted]**. Maps 1:1 onto the framework. For each: what it does, why it's a separate part, how you'd test it, what breaks if you skip it.
  - **Frontmatter (interface)** — `name`, `description`, `tools:['read','search/changes']`, `model`.
  - **Identity & Role** — "expert software architect specializing in Clean Architecture and DDD."
  - **Responsibilities** — bounded list of what it will/won't do.
  - **Context** — .NET stack rules, layer directions, known violations.
  - **Constraints** — ALWAYS/NEVER rules (circular deps, boundaries, immutable value objects).
  - **Analysis Process** — deterministic, repeatable steps.
  - **Output Format** — fixed Summary / Findings / Recommendations, PR-ready.
  - **Tone + Examples** — how it communicates, plus a concrete catalog of what to flag.
  - **Payoff moment:** live-edit one component (add a violation bullet to Context/Examples) — no rewrite, nothing else breaks. Maintainability, live — and exactly what makes it safe to hand to someone else on the team.
- **Beat 2 — jump to a real agent in code.** **[from workshop]** Run it against the Scenario 4 sample (`docs/requirements/agent-scenarios/architecture-reviewer.md`) — a compact `NotificationService.cs` that `new`s up `SmtpEmailSender` directly and imports Infrastructure into Application. Small enough to read in seconds, violation obvious once flagged. Prove the payoff-moment edit actually gets caught.
  - **Execution, time-dependent:** if time allows, invoke the agent live on stage for the "wow" moment; if the segment is running tight, fall back to pre-captured output of the same scenario. Prep both — decide in the room.

## 7. Real agents across the SDLC (6 min)
Same architecture, different configuration **[from workshop]** (`.github/agents/`, catalog `docs/guides/custom-agent-catalog.md`).
- **Visual: SDLC roster + handoff chain chart.** Two rows. Top row — the roster in SDLC order: **Backlog Generator** (requirements) · **Architecture Reviewer** (design/review, highlighted amber as the §6 anchor) · **Test Strategist** (QA) · **Quality Gate** (pre-merge). Bottom row — the handoff chain: **Spec → Plan → Build → Review**, where Review is itself an agent that validates the written code against the spec and does the initial code review; a human approves between each handoff (`send:false`).
- No new per-agent breakdown for the top row — Architecture Reviewer already did that work in §6. Revisit it as the anchor: same `.agent.md`, same components, just point out which component carries the weight for each other role (Backlog Generator → Output Format; Quality Gate → Constraints; etc.) without opening each file.
- **[from workshop]** `handoffs` chain agents into human-in-the-loop workflows — `send:false` keeps a human between steps; walk the Spec → Plan → Build → Review chain as the concrete example.
- Callback: this roster is what the far side of the capability gap looks like — the human as **Director** of engineered agents across the whole lifecycle, not one hero producing.

## 8. Maintenance rigor: run your agents like a codebase (7 min)
The half everyone skips — what actually holds an L4–L5 practice together **[from workshop]** (`docs/guides/agent-governance.md`).
- **Version control** — `.agent.md` in git; conventional commits (`feat(agent):`, `fix(architecture-reviewer):`); `BREAKING CHANGE:` markers when the output contract changes.
  - **Live artifact:** commit `6f995a3` — the real PR that added dual-stack support to this exact agent (later stripped back out for the demo copy) — walked live via `git show` (safe, no live model calls) as a genuine example of the conventional-commit format above.
- **Code review** — every change via PR. Tiered: **minor** (typo, no review) · **moderate** (new constraint, one approval) · **major** (role/output change, two approvals + docs + announce). Reviewer checklist: functionality, quality, testing, docs, integration.
- **Testing** — 3–5 saved test scenarios per agent; test-before-merge; re-run on every change to catch regressions.
- **Lifecycle** — proposal → development → review → production → maintenance → deprecation. Team-owned, not individual; optional "agent champion."
- **Deprecation** — retire agents like dead code: mark deprecated, point to replacement, grace period, remove cleanly.
- Punchline: this is why the cold-open practice wouldn't have stayed trapped in one person's head — governance is what lets it survive the hand-off, without heroes.
- **Execution, time-dependent:** full walkthrough of all five pillars if time allows; if the talk is running short, cut straight to the live `git show` artifact and the punchline — it's the most concrete, highest-payoff moment of the section.

## 9. The repeatable process — what to do Monday (1 min)
- **[from workshop]** Iteration loop (`part2/05-agent-design.md`): **Define → Test → Observe → Refine → Repeat.**
- Checklist to photograph: **don't start from scratch — fork an open-source agent/skill library** (`agent-skills`, `Squad`, `hve-core`), then treat it like the rest of this list, not a finished product → define the contract before the prompt → decompose into named components → write 3–5 test scenarios → commit as a reviewed `.agent.md` → iterate on components, not one monolithic prompt.

## 10. Close + Q&A (~1 min + ~7)
- Callback to the cold-open story and the maturity model: the senior engineer's practice didn't need a smarter model, it needed to stop living in one person's head. You don't cross the capability gap by prompting harder — you cross it by engineering agents as products a whole team can run. Pick your rung and take the next step.
- Thesis restated: *design your agents, maintain them like code, and operationalize the judgment — that's how the human role becomes Director instead of hero producer.*
- Where to get the slides, the checklist, and the agent files.

---

## Reusable assets (inventory)
- **Maturity model (§3):** Shawn's *Agentic AI Maturity Model* slide — L1 AI Autocomplete → L5 Agentic Adaptive, the Capability Gap (L3→L4), and the Producer→Reviewer→Director role shift. **Exact source: slide 3 of `2026-global-azure-columbus.pptx`** (uploaded 2026-07-20) — reuse this slide as-is (same layout/content) rather than rebuild.
- **Blog framing (intro):** *Wishful Thinking?* (shawnewallace.com/2026-06-17-wishful-thinking) — code vs. software, senior/junior split, hero trap, preceptorship, "real wishful thinking." Companion posts: *ai-dev-flow* (encoding process into artifacts), *the-instructions-are-the-process*.
- **Thesis + framework + iteration + pitfalls:** `part2/05-agent-design.md`.
- **Hierarchy framing:** `part2/03-custom-agents-intro.md`.
- **SDLC workflow comparisons:** `part2/04-workflow-agents.md`.
- **Design process:** `docs/guides/agent-design-guide.md`.
- **Governance (maintenance rigor):** `docs/guides/agent-governance.md`.
- **Real agent files:** `.github/agents/*.agent.md` (architecture-reviewer, quality-gate, test-coverage, test-strategist, backlog-generator, modernization).
- **Catalog:** `docs/guides/custom-agent-catalog.md`. **Labs:** `docs/labs/lab-09-agent-design.md`, `lab-10-capstone-build-agent.md`.
- **"Don't start from scratch" open-source pointers (§5, §9):** [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) (production-grade engineering skills) · [bradygaster/squad](https://github.com/bradygaster/squad) (Microsoft — AI agent teams as files in your repo) · [microsoft/hve-core](https://github.com/microsoft/hve-core) (agents, prompts, instructions, skills + RPI methodology).

## Deck status
- **v1 built 2026-07-20:** `agents-are-products.pptx` — 15 slides (title, §1–§10, §3 imported as image from the reference deck, §7 embeds the SDLC chart). Built with pptxgenjs, validated (schema + content QA clean), visually reviewed slide-by-slide. Cincy Deliver 2026 is **Friday, July 24, 2026** — 4 days out as of this build.
- **2026-07-22 addition:** new "Further Reading" slide inserted between §9 (What to do Monday) and the close — 18 slides total now. Top row of 4 linked cards (agent-skills, Squad, hve-core, Awesome Copilot); bottom row of 3 (Twitter/X, LinkedIn, GitHub). Matches existing card-grid style/palette, validated + visually reviewed.
- **2026-07-22 cleanup:** both DEMO slides (§6 Beat 2 code demo, §8 `git show` commit demo) had presenter-only stage direction ("SWITCH TO VS CODE/TERMINAL — RETURN HERE AFTER") printed on the visible slide. Removed from the slide and moved into each slide's speaker notes instead; the audience-facing italic caption stays on-slide.
- **2026-07-22 sponsor slide:** `2026SponsorSlide.pptx` (conference-provided, Cincy Deliver 2026 Sponsors — Diamond: ingage, Japikse Family Foundation; Platinum: Centric; Gold: vindex) added as both the first and last slide — 20 slides total now. Brought over as a fully self-contained slide (its own slideMaster/layouts/theme/media, namespaced `sponsor*`) rather than restyled, so it renders exactly as provided by the conference.
- **2026-07-22 review fixes:** full slide-by-slide review, then three fixes applied and validated: (1) maturity-model image — Capability Gap badge moved from the L2/L3 boundary to the correct L3/L4 boundary (pixel edit of the embedded PNG); (2) slide 11 (§6 Beat 2) — "Execution — time-dependent" card removed from the visible slide (presenter logistics; already in the DEMO slide's speaker notes), remaining violation card re-centered; (3) literal backticks removed from on-slide text (slide 11 "`new`s up" → "Instantiates", slide 14 "`.agent.md`"). Still open from review: verify X/LinkedIn handles on Further Reading slide (deck says ShawnWallace / shawnwallace; GitHub+blog use shawnewallace). Also retitled slide 11 "Scenario 4: NotificationService.cs" → "The test case: NotificationService.cs" (the "Scenario 4" numbering is ai-code-workshop-internal, meaningless to this audience) and added full speaker notes to it (purpose, the sample, the point to land, execution options).
- **2026-07-22 §6 restructure:** §6 DEMO slide deleted (deck now 19 slides; later footer numbers decremented). Former test-case slide rebuilt as "What the agent produced": slim violation card + dark mono output card (Summary / [HIGH] finding / Recommendation, styled like the §8 commit card) + italic takeaway ("Agents don't make up for a bad process — they amplify a good one…"). Full speaker notes on it, including a BEFORE FRIDAY reminder that the output is a representative mock-up — run the agent once against the sample and swap in the real Findings if they differ. Slide 10's callout reworded ("The payoff: adding a violation bullet to Context is a one-line change — nothing else breaks") since there's no live edit.
- **2026-07-22 speaker notes:** full notes added to all 17 content slides (sponsor slides excluded) — per-section timing cues matching the outline's budget, delivery beats, transitions, and the §8 compress-if-short fallback. `6f995a3` confirmed real by Shawn same day.
- **2026-07-23 §5 new slide:** inserted a new content slide between the capability-hierarchy slide (§5, formerly "6") and the Agent Components model slide (formerly "7") — now footer "7", everything after renumbered +1 through "17" (Further Reading). Topic: where new agent information belongs — instructions vs. skills vs. agents — framed as "right layer compounds, wrong layer costs you," closing with a software-engineering-rigor punchline ("same rigor as any interface"). Built with the same 3-card + coral-top-bar + navy-punchline-bar pattern as the §4 pitfalls slide (visually reviewed, matches deck style exactly). Speaker notes added (~1 min). Deck is now 21 slides total (incl. both sponsor slides). A pre-existing note on the prior slide already teed this up ("It's all about context for a lot of reasons…").
- **2026-07-24 talk delivered:** session given as scheduled. Handles confirmed correct as-is. Repo published to `shawnewallace/agents-are-products-talk` on GitHub; `punch-list.md` retired.

## Decisions locked
- **Deck visual style:** matched from `2026-global-azure-columbus.pptx` (Shawn's Global Azure Columbus 2026 deck, uploaded 2026-07-20). Dark navy background `#0B1F3A`; coral accent `#F78166` (top/bottom bars, callout blockquote rule, capability-gap emphasis); gold accent `#FFD166` (level badges, underline rules, "Framework" label); blue accent `#4F9DE6` (progress bars, links, italic subtitle emphasis); slate gray `#94A3B8` (muted/secondary text); white primary text. Font: Aptos Display (headers) / Aptos (body), bold sans throughout. Amber used in the §7 SDLC chart (built 2026-07-20) lines up with this gold accent — no rework needed there.
- **§7 scope:** no per-agent tour. Top-row roster is **Backlog Generator, Architecture Reviewer, Test Strategist, Quality Gate** — named only, Architecture Reviewer is the sole demo (already shown in §6), point at which component matters most for each other role without opening their files. **Modernization dropped from the roster entirely**, replaced by a bottom-row visual: the handoff chain **Spec → Plan → Build → Review**, where Review is an agent validating code against spec (not just a human gate), with a human approving between each handoff (`send:false`). Avoids repeating a 12-minute deep-dive pattern four more times in 6 minutes. Chart built and approved 2026-07-20.
- **§6/§8 live-demo scope (revised 2026-07-22):** §6 no longer live-invokes the agent. Beat 1 (decompose the real `.agent.md` against the component template) is the centerpiece; Beat 2 is now a single pre-captured-output slide ("What the agent produced") showing the Findings flagging the Application→Infrastructure violation in `NotificationService.cs`, plus the takeaway line: *agents don't make up for a bad process — they amplify/accelerate a good one; SE rigor keeps the artifacts aligned with the process, with clear demarcation points between phases.* The §6 DEMO slide (VS Code switch) is deleted — reclaims ~3–4 min and kills the riskiest prep. Rationale: the decomposition is the lesson; the credibility gap between "well-structured file" and "here's what it produced" is closed by one screenshot, no live model call needed. §8's `git show 6f995a3` demo is unchanged (zero risk, no model call); §8 depth still time-dependent.
- **§6 centerpiece: Architecture Reviewer** — chosen over Quality Gate (components blur together, weaker demo of the framework) and Backlog Generator (audience-friendly but too thin for 12 min of depth). Most complete instance of every named component, and the outline's payoff moment ("add a violation to detect in one component") maps directly onto its Context/Examples sections. Local copy imported to `demo/architecture-reviewer.agent.md` (source: `.github/agents/architecture-reviewer.agent.md` in `ai-code-workshop`) — added an explicit `## Identity & Role` heading (missing in the source) so all seven framework components are uniformly labeled for the live walkthrough.
- **Audience stack: .NET only.** Stripped Spring Boot content out of the demo copy of Architecture Reviewer entirely rather than generalizing the framing live — one stack keeps the live decomposition focused and avoids splitting attention across two sets of framework-specific violations in a 12-minute segment.
