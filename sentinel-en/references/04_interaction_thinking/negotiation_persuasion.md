# Interaction Thinking / Negotiation and Persuasion (code context)

> Main category color: green `#0A8A4A`. The layer for finding consensus in technical disagreements and driving adoption — invoked during collaboration and decision-making.

---

## #negotiate (#negotiate)
**Position**: Find consensus everyone can accept when technical proposals diverge.

**When to use**: Disagreement on tech selection, scope negotiation, cross-team requirement conflicts.

**How**:
1. First understand what the other side actually cares about (the need behind the stated position, not the surface position).
2. Find common goals as the foundation.
3. Distinguish "negotiable" from "non-negotiable" (e.g. security/correctness).
4. Propose expanding the pie rather than splitting it (win-win > zero-sum).

**Checklist**:
- □ Do I understand the real need behind their position?
- □ What is our shared goal?
- □ What can be conceded, what is the bottom line (correctness/security)?

**Code smell**: Technical argument devolves into "who is right or wrong" ego battle → return to shared-goal negotiation.

🔗 **Pairs with**: #problemdefinition (their real need), #persuasion (effective communication), #emotionalintelligence (managing emotions)

---

## #persuasion (#persuasion)
**Position**: Use evidence and clear argument to convince the team to adopt a better technical approach.

**When to use**: Pushing a proposal, changing established practice, defending in technical review.

**How**:
1. Speak with data/evidence (benchmark, case, quantified risk), not just "I feel".
2. Frame from what the other side cares about (saves time / reduces risk / easier to maintain).
3. Acknowledge tradeoffs and costs of the approach — build trust through honesty.
4. Give a concrete actionable next step to lower the adoption threshold.

**Checklist**:
- □ Do I have evidence to back this up, or am I just expressing preference?
- □ Have I explained the benefit from their perspective?
- □ Have I honestly stated the cost of this approach?

**Code smell**: "This one is just better" with zero data backing → weak persuasion, relying on volume not evidence.

🔗 **Pairs with**: #evidencebased (use evidence), #thesis (clear main point), #audience (their angle)

---

## #shapingbehavior (#shapingbehavior)
**Position**: Use tooling, process, and defaults to guide team behavior — not reminders and willpower.

**When to use**: Improving team habits (test coverage / code quality), driving conventions into practice.

**How**:
1. Make the "right way" the default/automatic (linter, CI, template, pre-commit).
2. Make the "wrong way" hard (type checks, must-pass tests before merge).
3. Reduce friction on correct behavior, add friction to wrong behavior.
4. Enforce by tooling > rely on people remembering.

**Checklist**:
- □ Am I relying on "reminding everyone" or on "tooling that auto-guarantees"?
- □ Is the right way the path of least effort?
- □ Is the wrong way blocked by tooling?

**Code smell**: Verbally reminding "remember to add tests" in code review → should be CI-enforced; relying on memory will fail.

🔗 **Pairs with**: #systemsdynamics (process feedback), #optimization (reduce friction), #leadershipprinciples (build culture)
