# Creative Thinking / Data and Exploration (code context)

> Main category color: orange-yellow `#D4900A`. The layer for forming hypotheses and visualizing abstract systems — the core engine during diagnosis.

---

## #hypothesisdevelopment　⭐diagnostic core
**Role**: Form "testable hypotheses" about a bug's root cause, instead of diving in and hacking randomly.

**When to use**: cause of bug unknown, diagnostic phase, when "don't know where it went wrong". **The engine of diagnosis.**

**How to do it**:
1. Based on #gapanalysis's "expected X / actual Y", list **2-3 possible root-cause hypotheses** (don't lock onto just one).
2. Write each hypothesis as "if the root cause is A, then I should observe B".
3. Design the "cheapest, most discriminating" verification (links to #testability).
4. Eliminate/confirm one by one with evidence, leaving the only one that stands.

**Checklist**:
- □ Did I list at least 2-3 hypotheses, or did I bite down on one?
- □ For each hypothesis, did I write "if true, what would I see"?
- □ Did I first verify the one "most able to distinguish true from false"?
- □ Am I verifying hypotheses, or just searching for evidence to support my favorite?

**Code smell**: Only one guess and you start changing code → no hypothesis set, you won't know if you fixed the wrong thing — it's shooting in the dark.

🔗 **Pairs with**: #gapanalysis (starting point of hypotheses), #evidencebased (verify with evidence), #plausibility (rank hypotheses), #variablecontrol (isolate to verify)

---

## #dataviz
**Role**: Draw out data flow, state transitions, system behavior — eyes catch anomalies better than the brain.

**When to use**: complex state transitions, tangled data flow, when "I can't think clearly about how the data flows".

**How to do it**:
1. Draw abstract data/state flows as diagrams (sequence diagrams, state machines, data flow).
2. Mark each node's "expected value vs actual value".
3. From the diagram, find "at which step the value first goes wrong".
4. For complex systems, pair with #systemmapping.

**Checklist**:
- □ Did I draw out the data flow / state transitions to look at?
- □ At which node does the value start diverging from expectation?
- □ Are there paths/branches on the diagram I previously overlooked?

**Code smell**: Staring at a pile of nested data/state purely thinking → should draw it out, brain capacity is limited.

🔗 **Pairs with**: #systemmapping (draw the system), #descriptivestats (data summary), #breakitdown (layered drawing)

---

## #modeling
**Role**: Build a mental model / data model of the system, so complex behavior becomes reason-able.

**When to use**: understanding complex systems, designing data structures, when "behavior is hard to predict".

**How to do it**:
1. Build a simplified model of the system (what states it has, how they transition).
2. Use the model to predict "given input, what should happen".
3. Compare model prediction vs actual behavior — the gap is either the model wrong or a bug.
4. If the model is wrong, correct the mental model (you misunderstood the system).

**Checklist**:
- □ Do I have a clear mental model of this system?
- □ Does my model's prediction match actual behavior?
- □ Is the gap a bug, or is my model (understanding) wrong to begin with?

**Code smell**: "Its behavior is so hard to predict" → you haven't built the right model yet; model first, debug second.

🔗 **Pairs with**: #systemmapping (externalize the model), #scientificmethod (build the big picture), #complexcausality (model includes causality)
