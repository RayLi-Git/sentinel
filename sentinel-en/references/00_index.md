# Sentinel Knowledge Base Index — 87 Thinking Habits × Engineering Context

> The first stop after Sentinel triggers. Read this file to orient, then jump into the matching subcategory `.md` for the full code-ified content.
> **Dual index**: habits are stored once under the four major categories (no duplication); this file also provides a "phase → habit" lookup table for direct use in the five-phase flow.

---

## 🔍 Stuck Symptom → Where to Look (engineering-context lookup)

| Your stuck point looks like | Major category | Subcategory file |
|---|---|---|
| Don't know what you're solving; requirements/problem definition unclear | Critical | Analyze problems |
| Tech selection hard; trade-off criteria unclear; ROI miscalculated | Critical | Analyze decisions |
| Have logs/numbers but can't read meaning; misreading perf data | Critical | Analyze data |
| Reasoning shaky, gaps in logic, conditions not fully covered | Critical | Evaluate reasoning |
| Is this assumption/claim credible? Misled by surface? | Critical | Evaluate claims |
| Can't come up with new approach; need to innovate under perf/compat constraints | Creative | Problem solving |
| Build a hypothesis from scratch; visualize/model a complex system | Creative | Data and exploration |
| Design A/B tests, verify causation, sampling comparison | Creative | Applied research methods |
| Naming/docs/PR descriptions scattered, don't match the reader | Communication | Verbal communication |
| Architecture diagrams/dashboards/decks/charts poor | Communication | Nonverbal communication |
| Ethical gray zones (privacy/data usage); need to tell the truth | Interaction | Solving ethical problems |
| Causality too complex, emergence present, need system/dependency diagrams | Interaction | Complex systems interaction |
| Convince the team to adopt a plan; cross-team negotiation | Interaction | Negotiation and persuasion |
| Team collaboration, code review dynamics, accountability, self-awareness | Interaction | Working with others |
| Handling external input/string-SQL/command building; injection fears | Security | Input and trust boundaries |
| Using keys/passwords/tokens; permission design; sensitive data | Security | Secrets and least privilege |
| Login/authn/authz; what would an attacker hit; pre-ship checks | Security | Auth and attack surface |
| Installing third-party packages; CI/CD; deploy; supply chain risk | Security | Dependencies and supply chain |

---

## 🔄 Phase → Habit Lookup (use this directly in the five-phase flow)

> The same habit can be used across phases; this lists "most commonly invoked in that phase". Each habit is stored only once in its subcategory file.

| Phase | Primary habits | Subcategory source |
|---|---|---|
| 1️⃣ Plan | #rightproblem #breakitdown #gapanalysis #strategize #constraints #purpose / Security: #trustboundary #attacksurface #sensitivedata | Analyze problems / Working with others / Problem solving / Analyze decisions / Security |
| 2️⃣ Build | #optimization #algorithms #constraints #analogies #designthinking #audience #composition / Security: #untrustedinput #injectionprevention #secretsmanagement #authnz | Problem solving / Verbal communication / Security |
| 3️⃣ Diagnose | #rightproblem #variables #complexcausality #levelsofanalysis #evidencebased #hypothesisdevelopment #correlation | Analyze problems / Complex systems / Evaluate reasoning / Data and exploration / Analyze data |
| 4️⃣ Solve | #biasidentification #biasmitigation #testability #optimization #constraints #decisiontrees #utility / Security: #securebydefault #leastprivilege | Analyze decisions / Evaluate claims / Problem solving / Security |
| 5️⃣ Retro | #selfawareness #biasmitigation #studyreplication #levelsofanalysis #responsibility | Working with others / Analyze decisions / Applied research methods / Complex systems |

---

## 📋 Full 87-Habit Index (by five major categories)

> Source note: Critical / Creative / Communication / Interaction — **76 habits, from the world-class thinking-habits framework**; Security thinking **11 habits are an in-house extension**, designed specifically for vibe coding security needs. 76 world-class + 11 in-house = 87.

### Critical Thinking (29)

**Analyze problems** — `01_critical_thinking/analyze_problems.md`
- #1 **#breakitdown** (#breakitdown) — Cut huge, vague tasks into small handleable chunks
- #2 **#gametheory** (#gametheory) — Analyze strategies under multi-party (user/system/dependency) interactions
- #3 **#gapanalysis** (#gapanalysis) — Lock down the minimal gap between "expected behavior vs actual behavior"
- #4 **#rightproblem** (#rightproblem) — Confirm you're solving the real problem, not an imagined or surface need
- #5 **#variables** (#variables) — Move only one variable at a time to isolate the true cause

**Analyze decisions** — `01_critical_thinking/analyze_decisions.md`
- #6 **#biasidentification** (#biasidentification) — Catch the cognitive biases behind "I assumed"
- #7 **#biasmitigation** (#biasmitigation) — Actively design process to lower bias impact
- #8 **#decisiontrees** (#decisiontrees) — Lay out tech selection as comparable branches
- #9 **#psychologicalexplanation** (#psychologicalexplanation) — Understand motivations behind user/your own behavior
- #10 **#purpose** (#purpose) — Nail down "why are we doing this" before touching anything
- #11 **#utility** (#utility) — Weigh proposal value by cost/benefit

**Analyze data** — `01_critical_thinking/analyze_data.md`
- #12 **#confidenceintervals** (#confidenceintervals) — Look at perf/metrics via intervals not single points
- #13 **#correlation** (#correlation) — Distinguish "co-occurrence" from "causation"
- #14 **#descriptivestats** (#descriptivestats) — Use statistical summaries to read mounds of logs/metrics
- #15 **#distributions** (#distributions) — Understand the shape of latency/error-rate distributions (not just average)
- #16 **#probability** (#probability) — Use probability to estimate "how often will it go wrong"
- #17 **#regression** (#regression) — Find which variable drives the outcome
- #18 **#significance** (#significance) — Tell whether the A/B difference is real or noise

**Evaluate reasoning** — `01_critical_thinking/evaluate_reasoning.md`
- #19 **#evidencebased** (#evidencebased) — Talk with log/repro evidence, not guesses
- #20 **#deduction** (#deduction) — Derive necessary results from rules (cover conditional branches)
- #21 **#fallacies** (#fallacies) — Catch flaws in reasoning/attribution
- #22 **#induction** (#induction) — Generalize a rule from multiple cases
- #23 **#sourcequality** (#sourcequality) — Evaluate reliability of docs/StackOverflow/AI answers

**Evaluate claims** — `01_critical_thinking/evaluate_claims.md`
- #24 **#context** (#context) — Put the error back into its full context
- #25 **#critique** (#critique) — Run hostile review on your own solution
- #26 **#estimation** (#estimation) — Estimate order of magnitude (complexity/time/resources) before acting
- #27 **#interpretivelens** (#interpretivelens) — Re-read the same phenomenon from another angle
- #28 **#plausibility** (#plausibility) — Quickly judge whether a hypothesis is plausible
- #29 **#testability** (#testability) — Confirm the claim/fix can be verified

### Creative Thinking (17)

**Problem solving** — `02_creative_thinking/problem_solving.md`
- #30 **#scienceoflearning** (#scienceoflearning) — Use learning science to quickly master a new framework/language
- #31 **#constraints** (#constraints) — Find solutions under perf/compat/schedule constraints
- #32 **#analogies** (#analogies) — Borrow structure from solved problems for new ones
- #33 **#algorithms** (#algorithms) — Design systematic, repeatable solving steps
- #34 **#designthinking** (#designthinking) — Reverse-engineer tech solutions from user needs
- #35 **#heuristics** (#heuristics) — Use rules of thumb to quickly narrow the search space
- #36 **#optimization** (#optimization) — Find the best balance among multiple objectives

**Data and exploration** — `02_creative_thinking/data_and_exploration.md`
- #37 **#hypothesisdevelopment** (#hypothesisdevelopment) — Form testable bug root-cause hypotheses
- #38 **#dataviz** (#dataviz) — Draw out data flow/state changes
- #39 **#modeling** (#modeling) — Build mental/data models of the system

**Applied research methods** — `02_creative_thinking/research_methods.md`
- #40 **#sampling** (#sampling) — Design representative test-case sampling
- #41 **#casestudy** (#casestudy) — Drill into a single extreme case to find the rule
- #42 **#comparisongroups** (#comparisongroups) — Isolate variables with control groups (A/B, before/after)
- #43 **#interventionalstudy** (#interventionalstudy) — Design "change one thing and watch the result" experiments
- #44 **#interviewsurvey** (#interviewsurvey) — Design user-feedback collection
- #45 **#observationalstudy** (#observationalstudy) — Observe behavior from real usage data
- #46 **#studyreplication** (#studyreplication) — Ensure the bug/result reproduces reliably

### Communication Thinking (10)

**Verbal communication** — `03_communication_thinking/verbal_communication.md`
- #47 **#audience** (#audience) — Write for the reader (teammate / future you)
- #48 **#composition** (#composition) — Organize code/docs/PR content effectively
- #49 **#connotation** (#connotation) — Names should carry the right implicit meaning
- #50 **#organization** (#organization) — Build clear code/doc structure
- #51 **#professionalism** (#professionalism) — Professionalism in commits/PRs/communication
- #52 **#thesis** (#thesis) — One sentence stating what this PR/proposal does

**Nonverbal communication** — `03_communication_thinking/nonverbal_communication.md`
- #53 **#communicationdesign** (#communicationdesign) — Design clear error messages/API interfaces
- #54 **#expression** (#expression) — Express intent in the clearest form
- #55 **#medium** (#medium) — Pick the right medium (chart/table/text/code)
- #56 **#multimedia** (#multimedia) — Combine charts + text to explain complex systems

### Interaction Thinking (20)

**Solving ethical problems** — `04_interaction_thinking/ethical_problems.md`
- #57 **#ethicalconsiderations** (#ethicalconsiderations) — Consider ethical impact of tech decisions (privacy/fairness)
- #58 **#ethicalcourage** (#ethicalcourage) — Dare to say "this is wrong" even when inconvenient
- #59 **#ethicaljudgment** (#ethicaljudgment) — Make ethical calls in gray zones

**Complex systems interaction** — `04_interaction_thinking/complex_systems.md`
- #60 **#complexcausality** (#complexcausality) — Trace cross-layer, nonlinear bug causal chains
- #61 **#emergentproperties** (#emergentproperties) — Identify emergent problems from system interactions
- #62 **#levelsofanalysis** (#levelsofanalysis) — Analyze across UI/logic/data/infra layers
- #63 **#networks** (#networks) — Analyze dependency networks between modules/services
- #64 **#systemdynamics** (#systemdynamics) — Understand system dynamic behavior over time (feedback loops)
- #65 **#systemmapping** (#systemmapping) — Draw out system structure/data-flow diagrams

**Negotiation and persuasion** — `04_interaction_thinking/negotiation_persuasion.md`
- #66 **#negotiate** (#negotiate) — Find consensus when tech proposals diverge
- #67 **#persuasion** (#persuasion) — Use evidence to persuade the team to adopt a proposal
- #68 **#shapingbehavior** (#shapingbehavior) — Use tools/process to guide team behavior

**Working with others** — `04_interaction_thinking/collaboration.md`
- #69 **#conformity** (#conformity) — Understand group conformity's impact on tech decisions
- #70 **#differences** (#differences) — Respect teammates' differing skills and perspectives
- #71 **#emotionaliq** (#emotionaliq) — Keep emotional intelligence in code review/conflict
- #72 **#leadprinciples** (#leadprinciples) — Principles for leading tech direction
- #73 **#powerdynamics** (#powerdynamics) — Understand power relations in the team
- #74 **#responsibility** (#responsibility) — Own your code and decisions
- #75 **#selfawareness** (#selfawareness) — Be aware of your blind spots and habitual mistakes
- #76 **#strategize** (#strategize) — Build effective tech/project strategy

### Security Thinking (11) | ⚙️ In-house extension (not from the world-class source; designed for vibe coding security needs)

**Input and trust boundaries** — `05_security_thinking/input_trust_boundaries.md`
- #77 **#untrustedinput** (#untrustedinput) — All external input is toxic by default; validate before use
- #78 **#trustboundary** (#trustboundary) — Mark trusted-internal vs untrusted-external clearly; check on crossing
- #79 **#injectionprevention** (#injectionprevention) — Never let data be executed as code (SQL/command/XSS)

**Secrets and least privilege** — `05_security_thinking/secrets_least_privilege.md`
- #80 **#secretsmanagement** (#secretsmanagement) — Keys/passwords never in code/log/git/frontend
- #81 **#leastprivilege** (#leastprivilege) — Each component gets just enough permission
- #82 **#sensitivedata** (#sensitivedata) — Minimize and encrypt PII/financial data end-to-end

**Auth and attack surface** — `05_security_thinking/auth_attack_surface.md`
- #83 **#authnz** (#authnz) — Distinguish "who you are" from "what you can do"; check at every entry
- #84 **#attacksurface** (#attacksurface) — List exposure points; think like the attacker about where to hit
- #85 **#securebydefault** (#securebydefault) — Fail closed on errors; defaults pick the safest

**Dependencies and supply chain** — `05_security_thinking/dependencies_supply_chain.md`
- #86 **#dependencyaudit** (#dependencyaudit) — Third-party packages are the biggest attack surface; check source/version/CVE
- #87 **#supplychain** (#supplychain) — Your security = your weakest dependency; the whole chain is an attack path

---

## ⚠️ Loading Strategy Reminder (for Sentinel itself)

- One stuck point usually needs only 3-5 habits — **don't read them all**.
- Use the "stuck symptom lookup" or "phase lookup" to pin down 1-2 subcategories; only open those `.md`.
- `#rightproblem` is the default mandatory starting habit (unless the task is entirely outside analysis scope).
- When symptoms are unclear, ask back to fill in data (give 4+ options); don't guess.
