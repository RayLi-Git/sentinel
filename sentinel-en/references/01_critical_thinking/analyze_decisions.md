# Critical Thinking / Analyze Decisions (code context)

> Primary color: purple `#6B5CE7`. The layer for tech selection, trade-offs, and bias-hunting — the "Solve" phase of the five phases mostly draws from here.

---

## #biasidentification
**Role**: Catch the cognitive biases behind "I assumed" — often the real culprit when debugging goes in circles.

**When to use**: Stuck on a bug for a long time, dead-certain "it must be over there" but keep being wrong, during code review.

**How to do it**:
1. Write down "my most confident current judgment."
2. Ask "why am I so confident? Real evidence or just intuition/habit?"
3. Check common biases: confirmation bias (only collecting supporting evidence), anchoring (stuck on the first idea), recency (blaming the last change).
4. Force yourself to list "if I'm wrong, where would it be?"

**Checklist**:
- □ Am I looking for evidence, or for evidence that "supports my hypothesis"?
- □ Am I locking onto X just because I "just changed X"?
- □ Did I rule out some possibility because I actually checked, or because "no way"?
- □ Once the first cause popped into my head, did I stop considering others?

**Code smell**: Saying "it can't be here" for the second time → 80% chance it's here, confirmation bias is at work.

🔗 **Pairs with**: #biasmitigation (then lower its impact), #critique (adversarial self-review), #evidencebased (replace intuition with evidence)

---

## #biasmitigation
**Role**: Not just spot the bias — actively design process to minimize its effect.

**When to use**: After noticing your own bias, making important tech decisions, wanting to avoid "the same old habitual solution."

**How to do it**:
1. For important judgments, force yourself to write the "opposing hypothesis" and seriously check it.
2. Externalize judgments with checklists/tests, don't rely on mental impression.
3. Get a second opinion (another perspective / rubber duck / re-read the docs).
4. Before deciding, ask "how would future-me criticize this decision?"

**Checklist**:
- □ Did I seriously verify the direction I "feel is impossible"?
- □ Is my judgment written down as something checkable, or only in my head?
- □ Did I only use the solution I'm familiar with, ignoring a better fit?

**Code smell**: Solving different problems with the same move every time (if-everywhere, try-everywhere) → habit bias, needs active mitigation.

🔗 **Pairs with**: #biasidentification (find it first), #decisiontrees (lay options out to break anchoring), #selfawareness (retro on habits)

---

## #decisiontrees
**Role**: Spread tech choices into comparable branches, turning trade-offs from "feeling" into "visible."

**When to use**: Picking framework/database/architecture, "plan A or plan B," any time there are multiple paths.

**How to do it**:
1. List all viable options (at least 3, including "don't do it").
2. For each option list: cost, benefit, risk, reversibility.
3. Mark each path's key uncertainty and worst-case outcome.
4. Prefer paths that are "reversible, worst case bearable."

**Checklist**:
- □ Did I list at least 3 options, or am I just oscillating between 2?
- □ Did I write down the "worst case" for each option?
- □ Is this decision reversible? If irreversible, did I think it through enough?
- □ Is "don't do it / do it later" treated as a real option?

**Code smell**: Installing some package without comparing alternatives → you skipped the decision tree.

🔗 **Pairs with**: #utility (quantify cost-benefit), #estimation (size each option), #constraints (filter out infeasible)

---

## #psychologicalexplanation
**Role**: Understand the psychological motive behind "why does the user (or I) do this" — often unlocks "weird bug reports."

**When to use**: User behavior doesn't match expectation, bug reports that don't make sense, designing UX, understanding why you keep making the same mistake.

**How to do it**:
1. Observe actual behavior (what the user did, not what they said).
2. Ask "what mental state/expectation would lead to this behavior?"
3. Distinguish "the user's mental model" from "the system's actual model" — find the gap.
4. Design the fix from the gap (often it's a UI/affordance issue, not a logic bug).

**Checklist**:
- □ Does what the user "does" match what they "say"?
- □ Where's the gap between what the user thinks the system does and what it actually does?
- □ Is this bug a logic error, or a misled mental model?

**Code smell**: The phrase "how could a user even use it like that" → it's not the user's fault, it's a mental model gap.

🔗 **Pairs with**: #designthinking (reason backward from needs), #audience (design for the reader), #context (put it back in context)

---

## #purpose
**Role**: Nail down "why are we doing this" before touching code — purposeless code is a breeding ground for tech debt.

**When to use**: Before new features/refactors/adding abstraction, when you feel "maybe I should optimize this," before writing any "just in case" code.

**How to do it**:
1. Write in one sentence "the reason this code exists."
2. Ask "what happens if we don't do it?" — if no serious consequence, maybe don't.
3. Confirm this purpose aligns with the upstream real need (link to #askquestions).
4. Put the purpose into commit/comment so future readers get it.

**Checklist**:
- □ Can I state "what happens if we don't do it"?
- □ Is this optimization/abstraction really needed now, or "might be useful later"?
- □ Will three-months-from-now me understand the purpose of this code?

**Code smell**: "Add it first in case we need it later" → YAGNI, pre-emptive design without clear purpose mostly becomes debt.

🔗 **Pairs with**: #askquestions (purpose aligns to the real question), #constraints (purpose bounds scope), #utility (worth it?)

---

## #utility
**Role**: Use cost/benefit weighing to judge whether a plan/optimization is "worth doing."

**When to use**: Optimizing performance, deciding whether to refactor, whether to pay down tech debt, ROI evaluation.

**How to do it**:
1. Estimate the "benefit" (time saved / perf gained / risk reduced).
2. Estimate the "cost" (effort, added complexity, maintenance burden, risk).
3. Compute "benefit/cost" and compare against other things you could do.
4. Benefit far less than cost → don't do it, or defer.

**Checklist**:
- □ Is what this optimization saves worth the complexity it adds?
- □ Am I optimizing "the actually slow part" or "the part I think is slow"? (measure first)
- □ Compared to this, is there higher-ROI work I should do first?

**Code smell**: Writing unreadable code to save 1ms → utility is miscalculated, the cost of readability is ignored.

🔗 **Pairs with**: #decisiontrees (lay out and compare), #estimation (size it), #descriptivestats (measure before optimizing)
