# Interaction Thinking / Collaborating with Others (code context)

> Main category color: green `#0A8A4A`. Team collaboration, self-awareness, accountability layer — invoked during collaboration and retro.
> Even in solo vibe coding, #selfawareness #responsibility #strategize are core to the retro loop.

---

## #conformity (#conformity)
**Position**: Understand how group conformity affects technical decisions — don't follow blindly just because "everyone does it this way".

**When to use**: Adopting a practice because "the industry does it this way", when team consensus may be a blind spot.

**Operation**:
1. For "everyone does this" ask "does it fit our context?"
2. Watch out for groupthink (the consensus nobody questions is the most dangerous).
3. Distinguish "validated convention" from "inertia nobody thought about".
4. Speak up when contrarianism is warranted (links to #ethicalcourage).

**Checklist**:
- □ Is this practice validated as fitting, or just "everyone does it"?
- □ Has anyone seriously questioned the team consensus?
- □ Do I agree because it's right, or because I don't want to be the odd one out?

**Code smell**: "Best practice says write it this way" without thinking whether it applies → conformity blind-following.

🔗 **Paired habits**: #sourcequality (validate conventions), #critique (question consensus), #context (applicability)

---

## #differences (#differences)
**Position**: Respect and leverage the different skills, perspectives, and thinking styles of teammates (and AI).

**When to use**: Team collaboration, task division, code review, asking for help.

**Operation**:
1. Recognize each person has different strengths; assign work accordingly.
2. Different perspectives are an asset (they see your blind spots), not a hassle.
3. When asking for help/review, find people with complementary perspectives.
4. Adjust communication to a form the other party can receive.

**Checklist**:
- □ Am I leveraging teammates' complementary strengths?
- □ Do I treat "different opinions" as an asset or as an obstacle?
- □ When seeking review, did I find someone who can see my blind spots?

**Code smell**: Only seeking review from people who'll agree with you → wasting the blind-spot-covering value of differences.

🔗 **Paired habits**: #perspectives (multi-perspective), #emotionaliq (collaboration), #debiasing (others cover blind spots)

---

## #emotionaliq (#emotionaliq)
**Position**: Maintain emotional intelligence during code review, technical conflict, and under pressure.

**When to use**: Being criticized on code, reviewing others, technical arguments, debugging to the breaking point.

**Operation**:
1. Issues not people: criticizing code isn't criticizing the person.
2. When receiving criticism, understand before responding — don't get defensive.
3. Under stress/stuck, notice the emotion; if necessary, step away then come back.
4. When reviewing others, give constructive, specific, respectful feedback.

**Checklist**:
- □ Am I treating "my code being criticized" as an attack on me?
- □ When I'm frustrated debugging, has my judgment dropped?
- □ Is the review I gave issue-focused, not person-focused?

**Code smell**: Debugging in a rage, randomly changing things → emotion has taken over judgment; should stop.

🔗 **Paired habits**: #selfawareness (notice emotion), #professionalism (review attitude), #biascheck (emotional bias)

---

## #leadprinciples (#leadprinciples)
**Position**: Principles for leading technical direction — even without a title, you can influence decisions through principles.

**When to use**: Driving technical decisions, mentoring newcomers, building team technical culture.

**Operation**:
1. Guide decisions with clear principles (not case-by-case), making the team predictable.
2. Lead by example (the code you write is the standard).
3. Empower rather than micro-manage (teach to fish).
4. Take responsibility for the team's long-term health (not short-term speed).

**Checklist**:
- □ Do my technical decisions follow consistent principles?
- □ Do I follow the standards I demand from others?
- □ Am I empowering the team, or doing everything myself?

**Code smell**: Demanding others write tests but not writing them yourself → leadership principles broken, nobody will follow.

🔗 **Paired habits**: #strategize (direction), #behaviorshaping (build culture), #responsibility (accountability)

---

## #powerdynamics (#powerdynamics)
**Position**: Understand power relationships in the team so good technical ideas don't get buried.

**When to use**: Good ideas can't gain traction, decisions driven by seniority rather than reasoning, cross-level communication.

**Operation**:
1. Recognize decisions are influenced by power/seniority, not just reasoning.
2. Present good ideas in "the language the decision-maker cares about".
3. Find allies, build trust, then push for big changes.
4. Watch for voices (newcomers/minorities) being suppressed by power.

**Checklist**:
- □ Is my good idea expressed in "the way the decision-maker cares about"?
- □ Are there voices in the team being suppressed by power (that should be heard)?
- □ Before pushing big changes, have I built enough trust/allies?

**Code smell**: A good technical suggestion ignored because "you're junior" → power dynamics at work; need strategy.

🔗 **Paired habits**: #persuasion (effective presentation), #negotiation (find consensus), #conformity (break groupthink)

---

## #responsibility (#responsibility)　⭐retro core
**Position**: Take responsibility for your own code and technical decisions — including admitting mistakes and following up on skipped root causes.

**When to use**: When bugs occur, during retros, follow-up after emergency skips, when decisions go wrong. **The attitudinal foundation of the retro loop.**

**Operation**:
1. When something goes wrong, first ask "what can I improve on my end?" rather than excuses.
2. Things skipped in emergencies (`[SKIPPED]`) — honestly follow up during retro; don't pretend it didn't happen.
3. Admit "my judgment was wrong back then"; write the lesson into the case file.
4. Take responsibility for long-term quality, not just getting it done.

**Checklist**:
- □ When something goes wrong, do I self-examine first or look for excuses?
- □ Have I honestly followed up on the root cause I skipped in an emergency?
- □ Did I honestly record my misjudgment in the case file?
- □ Am I accountable for "getting it done" or for "long-term quality"?

**Code smell**: `[SKIPPED]` markers left unaddressed, blaming bugs on environment/others → responsibility missing, the brain won't grow.

🔗 **Paired habits**: #selfawareness (see yourself), #reproducibility (follow-up verification), #ethicalcourage (honest reckoning)

---

## #selfawareness (#selfawareness)　⭐retro core
**Position**: Be aware of your own blind spots, habitual mistakes, and thinking preferences — this is the engine of case-file growth.

**When to use**: Retro, noticing yourself repeating mistakes, wanting to upgrade thinking. **The core habit of retro.**

**Operation**:
1. In retro, ask "why did I misjudge at the start this time?"
2. Find your habitual mistake patterns (always blame a certain layer first? Always love a certain solution?).
3. Write "pits I commonly fall into" into case-file patterns; read first thing next time you start work.
4. Notice how current state (tired/rushed/frustrated) affects judgment.

**Checklist**:
- □ What habitual blind spot does this misjudgment reflect?
- □ Have I made a similar mistake before? (Check the case file.)
- □ Did I record this self-insight into patterns?
- □ Is my current state (tired/rushed) affecting judgment?

**Code smell**: Same kind of mistake repeated without noticing → self-awareness missing, the case file isn't working.

🔗 **Paired habits**: #responsibility (honest reckoning), #debiasing (correct habits), #induction (induct your own pits), #reproducibility (settle into pattern)

---

## #strategize (#strategize)
**Position**: Form effective technical/project strategy — work backward from the goal, not one step at a time.

**When to use**: Project planning, prioritization, facing big goals.

**Operation**:
1. Work backward from the end goal (to get there, what needs to exist first?).
2. Prioritize: high-value × low-cost × unlocks-other first.
3. Identify key risks and milestones; validate the most uncertain first.
4. Stay flexible; adjust strategy based on feedback.

**Checklist**:
- □ Did I work backward from the goal, or am I going one step at a time?
- □ Is what I'm doing first "high-value and unlocks downstream"?
- □ Have I validated the most uncertain/highest-risk parts first?

**Code smell**: Diving into the fun part first, leaving the highest-risk part for last → strategy error; by the time risk explodes, it's too late.

🔗 **Paired habits**: #rightquestion (goal alignment), #breakdown (decompose path), #decisiontree (prioritize), #estimation (assess risk)
