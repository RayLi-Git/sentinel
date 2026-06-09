# Critical Thinking / Evaluate Reasoning (code context)

> Main category color: purple `#6B5CE7`. The layer that checks whether reasoning holds up and whether conditions are fully covered — invoked during diagnosis and code review.

---

## #evidencebased
**Position**: Speak with logs, repros, real measurements — not "I feel" or "it should be".

**When to use**: Throughout debugging, when making technical calls, when someone says "I guess it's...". **The golden rule of diagnosis**.

**How to operate**:
1. For any "I think the root cause is X", ask "where's the evidence?"
2. Get evidence via actual logs / breakpoints / minimal repro before concluding.
3. Before evidence is in, mark every judgment as a "hypothesis", not a verdict.
4. When evidence conflicts with hypothesis, trust the evidence.

**Checklist**:
- □ Does this judgment have actual evidence, or am I just guessing?
- □ Have I actually "seen" that value/state, or am I "assuming" it?
- □ When evidence conflicts with my assumption, do I stubbornly hold the assumption?

**Code smell**: "Probably here" then immediately edit → unverified edits often create new bugs without fixing the old one.

🔗 **Pairs with**: #hypothesis (hypotheses need evidence), #gapanalysis (gaps are the start of evidence), #biascheck (break unverified certainty)

---

## #deduction
**Position**: Derive necessary consequences from certain rules — ensures condition branches and logic coverage are complete.

**When to use**: Writing conditional logic, checking edge cases, confirming "all cases are handled".

**How to operate**:
1. List every possible input state (incl. null, empty, boundary, oversized).
2. For each state, deduce "how the program will flow, whether the result is correct".
3. Find states "not handled by any branch".
4. Add the missing branches.

**Checklist**:
- □ Are all input states (null/empty/boundary/negative/oversized) handled?
- □ Does if/else have missed cases falling into default behavior?
- □ Can I prove "unreachable branches really are unreachable"?

**Code smell**: if handles normal values, else assumes "everything else is the other kind" → missed cases silently go wrong.

🔗 **Pairs with**: #breakdown (enumerate all cases), #testability (write a test for each case), #fallacies (check the reasoning)

---

## #fallacies
**Position**: Catch flaws in reasoning and attribution, especially mis-attribution during debugging.

**When to use**: Attributing a bug, evaluating "why did that fix it?", reading technical claims.

**How to operate**:
1. Watch for common fallacies: post hoc (after ≠ because of), hasty generalization, appeal to authority (docs aren't necessarily right for your context).
2. For "B happened after A, so A caused B", demand isolated verification.
3. Stay skeptical of "it's always been fine before" (silent evidence).

**Checklist**:
- □ Did "it was fixed after the change" really fix it, or just mask the symptom?
- □ Did I derive a general rule from a single case?
- □ Does what "the docs / a senior said" apply to my specific context?

**Code smell**: "Adding sleep fixed it" → post hoc plus masking a race; root cause remains.

🔗 **Pairs with**: #correlation (correlation ≠ causation), #evidencebased (demand evidence), #critique (hostile review)

---

## #induction
**Position**: Generalize from multiple concrete cases — but beware overgeneralization.

**When to use**: Spotting a common pattern across several bugs, summarizing best practices, writing case-file patterns.

**How to operate**:
1. Collect multiple cases of the same kind (at least 3).
2. Find their shared structure / root cause.
3. Propose the general rule, but annotate "under what conditions it holds".
4. Actively hunt counter-examples to test the boundary.

**Checklist**:
- □ My general rule is based on how many cases? Enough?
- □ Is there a counter-example that would overturn this rule?
- □ Have I clearly stated the boundary of where this pattern applies?

**Code smell**: Hit one error once and erect an "iron rule" applied everywhere → overgeneralization from too small a sample.

🔗 **Pairs with**: #replicability (verify the rule is stable), #casestudy (deep-dive cases), #selfawareness (induct from retros into the case file)

---

## #sourcequality
**Position**: Evaluate the reliability and applicability of docs, StackOverflow, AI answers, tutorials.

**When to use**: Looking up a fix, before copy-pasting code, before adopting a library/approach.

**How to operate**:
1. Check source: official docs > well-maintained library > high-vote SO > random blog > outdated answers.
2. Check timeliness: which version is this answer for? Still applicable?
3. Check context: is its scenario the same as mine?
4. Before copying any code, understand "why it's written that way".

**Checklist**:
- □ Is this answer for my version / context?
- □ Is it outdated? (check the date, check if the API still exists)
- □ Do I understand what this copied code does, or just that it "looks like it runs"?

**Code smell**: Paste a chunk of code you don't understand, "it runs, good enough" → source quality not vetted, debt buried.

🔗 **Pairs with**: #evidencebased (verify yourself), #critique (question the source), #context (applicability)
