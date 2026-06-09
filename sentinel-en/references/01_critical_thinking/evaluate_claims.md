# Critical Thinking / Evaluating Claims (code context)

> Primary category color: purple `#6B5CE7`. The layer that judges whether a hypothesis/claim is credible and whether you're being misled by surface appearances — invoked during Diagnose and Solve.

---

## #context (#context)
**Role**: Put the error/phenomenon back into the full context where it occurred — don't fix it in isolation.

**When to use**: Bug only shows up in specific environments/times/users; "it just doesn't happen on my machine."

**Operation**:
1. Record the full context of the error: environment, version, input, prior actions, time, user state.
2. Compare the context differences between "happens" vs "doesn't happen."
3. Narrow the root cause from the context differences.

**Checklist**:
- □ Did I record the full context where this bug occurred?
- □ Where does the "happens vs doesn't" context differ?
- □ Am I only testing in "my clean environment" and ignoring real context?

**Code smell**: "Works fine locally" → detached from real context (data volume / network / permissions / concurrency).

🔗 **Pairs with**: #variablecontrol (compare context differences), #complexcausality (context interactions), #reproducibility (rebuild the context)

---

## #critique (#critique)
**Role**: Run a hostile review of your own solution; actively hunt where it will blow up.

**When to use**: After finishing an important chunk of code, before opening a PR, when you feel "should be fine."

**Operation**:
1. Pretend you're the one trying to break this code — find its weak spots.
2. Ask "what input would blow this up," "what ordering breaks it," "what scale crushes it."
3. Question every assumption: "I assume this is non-null / sorted / single-threaded… really?"
4. Patch or document the weaknesses you find.

**Checklist**:
- □ Did I genuinely try to "break" my own solution?
- □ Do my implicit assumptions (non-null, sorted, single-thread, stable network) all hold?
- □ The phrase "should be fine" — did I verify it or just hope?

**Code smell**: Ship without self-attack → you outsourced bug-hunting to your users.

🔗 **Pairs with**: #biascheck (break self-conviction), #deduction (cover cases), #testability (prove with tests)

---

## #estimation (#estimation)
**Role**: Estimate the order of magnitude before acting — complexity, hours, data volume, performance — so you don't realize the direction is wrong after you've already built it.

**When to use**: Picking an algorithm, evaluating feasibility, "can the data volume hold up."

**Operation**:
1. Order-of-magnitude estimates on key dimensions (Big-O, data volume, QPS, memory).
2. Use rough numbers to quickly rule out obviously infeasible options.
3. Estimate "worst case" magnitude, not just the average case.
4. Compare estimates to measurements afterward; calibrate intuition.

**Checklist**:
- □ At max data volume, does this approach hold up in order of magnitude?
- □ Did I dive into implementation without estimating first?
- □ How far off were my estimates? (calibration)

**Code smell**: Using O(n²) on data that will grow to millions of rows → no magnitude estimate; it explodes at scale.

🔗 **Pairs with**: #utilitytheory (cost-benefit), #decisiontree (compare options), #optimization (target bottlenecks)

---

## #interpretivelens (#interpretivelens)
**Role**: Re-read the same phenomenon from a different angle — often unsticks frozen thinking.

**When to use**: Stuck inside the same assumption, "I'm racking my brain and still wrong," need a creative breakthrough.

**Operation**:
1. Deliberately shift perspective: from the data side? user side? timeline? the opposite direction?
2. Ask "what if this isn't a bug but by design — what does that mean?"
3. Re-examine the same phenomenon from another layer (UI → logic → data → infrastructure).

**Checklist**:
- □ Have I been looking from the same angle the whole time and gotten stuck?
- □ Would viewing it "from data flow / from user / from time order" change it?
- □ I'm assuming it's a class-X problem — could it actually be class Y?

**Code smell**: Tried the same line of thought ten times and still wrong → switch interpretive lens, don't try harder.

🔗 **Pairs with**: #multilevel (switch layers), #analogy (borrow structure), #biascheck (break anchoring)

---

## #plausibility (#plausibility)
**Role**: Quickly judge whether a hypothesis is "plausible" — decide if it's worth time to verify.

**When to use**: After listing multiple root-cause hypotheses, deciding which to check first, prioritizing under time pressure.

**Operation**:
1. For each hypothesis, quickly assess "for it to be true, what prerequisites must all hold."
2. More prerequisites, more demanding → less plausible → push back in queue.
3. Prioritize the "most plausible + easiest to verify" hypothesis.
4. But keep "implausible but cheap" ones for quick elimination.

**Checklist**:
- □ Did I check the most plausible hypothesis first, not the one I thought of first?
- □ How many coincidences must hold for this hypothesis? (more = less plausible)
- □ Did I order verification by "plausibility × verification cost"?

**Code smell**: Investigating the rarest, weirdest possibility first while ignoring the most obvious → plausibility ordering is wrong.

🔗 **Pairs with**: #hypothesis (have a hypothesis set first), #estimation (estimate verification cost), #probabilitytheory (estimate likelihood)

---

## #testability (#testability)
**Role**: Confirm that your fix/claim "can be verified" — after changing, you must be able to prove it's actually fixed.

**When to use**: Wrapping up the Solve phase, when "I think it's fixed," when designing testable code.

**Operation**:
1. Before fixing, think "how will I prove it's fixed."
2. Use the minimal case that reproduces the original bug; verify it no longer occurs after the fix.
3. Make sure verification is "objectively repeatable," not "I clicked around and it looked ok."
4. Settle the verification into automated tests to prevent regression.

**Checklist**:
- □ Can I prove it's fixed with a definite step?
- □ Did I verify with "a case that originally broke"?
- □ Can someone else reproduce this verification next time?
- □ Did I turn it into a test to prevent regression?

**Code smell**: Closing the case with "I clicked around manually and it looks normal" → no repeatable verification; regression will come knocking anytime.

🔗 **Pairs with**: #reproducibility (reproduce the bug), #gapanalysis (verify the gap is closed), #controlgroup (before/after comparison)
