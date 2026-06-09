# Creative Thinking / Problem Solving (code context)

> Primary category color: orange-yellow `#D4900A`. The layer of finding solutions under constraints and designing them — invoked during Build and Solve.

---

## #scienceoflearning
**Position**: Use principles from the science of learning to quickly master a new framework/language/unfamiliar codebase.

**When to use**: Taking over an unfamiliar project, learning new tech, "I can't tell what this code is doing".

**How**:
1. Build the big picture (architecture/data flow) first, then drill into details — don't grind line-by-line.
2. Actively recall / get hands on (write a small demo), instead of passively reading docs.
3. Start from "the smallest runnable example" and add complexity step by step.
4. Capture what you learned in your own words/diagrams (feeds the case file).

**Checklist**:
- □ Did I grab the big picture before reading details?
- □ Am I reading passively, or did I verify understanding hands-on?
- □ Can I explain how it works in my own words?

**Code smell**: Open a new framework and grind from line one of the docs → no big picture, learns slow and forgets fast.

🔗 **Pairs with**: #analogies (borrow existing knowledge), #modelbuilding (build mental model), #systemmapping (draw the architecture)

---

## #constraints
**Position**: Treat constraints (performance/compat/timeline/resources) as clues to shrink the solution space, not as obstacles.

**When to use**: Too many options to pick from, designing under hard limits, resource-constrained situations.

**How**:
1. Explicitly list all hard constraints (must satisfy) and soft constraints (nice to satisfy).
2. Use hard constraints to filter out infeasible options.
3. Treat the constraint as a hint: "Under this constraint, what solution is natural?"
4. Distinguish real constraints from "constraints I assumed".

**Checklist**:
- □ Have I clearly separated hard and soft constraints?
- □ Any "I assumed it won't work" pseudo-constraints I never verified?
- □ Does the constraint actually point to a simpler solution?

**Code smell**: Brainstorming options before clarifying constraints → piles of infeasible ideas.

🔗 **Pairs with**: #rightquestion (constraints scope the problem), #optimization (optimize under constraints), #decisiontree (constraints filter options)

---

## #analogies
**Position**: Borrow the structure of "a problem you've already solved" to crack the new one in front of you.

**When to use**: Hitting a problem you haven't solved before, designing a new module, hunting for a mature pattern.

**How**:
1. Ask "Does the structure of this problem resemble one I've solved?"
2. Find the corresponding mature solution / design pattern.
3. Compare differences, adapt (don't force-fit).
4. Watch out for false analogies — "surface looks alike but essence differs".

**Checklist**:
- □ Does this problem map to a known pattern/precedent?
- □ Is my analogy structural, or merely superficial?
- □ When applying it, did I handle the parts that differ?

**Code smell**: Force-fitting a design pattern that "looks like it" → false analogy, gets more tangled the more you push.

🔗 **Pairs with**: #designthinking (find patterns from needs), #scienceoflearning (knowledge transfer), #perspectives (switch angles to find analogies)

---

## #algorithms
**Position**: Design systematic, repeatable, verifiable problem-solving steps — not ad-hoc cobbling.

**When to use**: Writing core logic, processing data, when correctness guarantees matter.

**How**:
1. Write the steps clearly in prose/pseudocode first, then code.
2. Confirm input/output and invariants for each step.
3. Consider complexity and edge cases (empty, singleton, huge).
4. Think it through before touching the keyboard — don't guess as you type.

**Checklist**:
- □ Can I state each step of the algorithm in words?
- □ Did I think through edge cases (empty/singleton/max)?
- □ Is the complexity acceptable?
- □ Am I thinking first then writing, or improvising as I go?

**Code smell**: Write-try-tweak until it runs → no algorithm, just trial-and-error, logic holes everywhere.

🔗 **Pairs with**: #breakitdown (decompose steps), #estimation (estimate complexity), #deduction (cover edge cases)

---

## #designthinking
**Position**: Derive technical solutions from real user needs, not the other way around.

**When to use**: Designing a feature/UI/API, deciding "what should we even build".

**How**:
1. Empathize first: what does the user actually want to accomplish, where does it hurt.
2. Define the real problem (chain to #rightquestion).
3. Brainstorm multiple options, validate with a minimal prototype.
4. Iterate from user feedback — don't aim for perfect on first pass.

**Checklist**:
- □ Am I starting from user needs, or from "the tech I want to play with"?
- □ Did I prototype small before going all-in on implementation?
- □ Will users actually use this design?

**Code smell**: Features driven by "this tech is cool, let me use it" → tech-driven, often builds things nobody uses.

🔗 **Pairs with**: #rightquestion (define real need), #audience (for the user), #psychcauses (understand behavior)

---

## #heuristics
**Position**: Use rules of thumb to quickly narrow the search; make a good-enough call when you don't have time to enumerate.

**When to use**: Debugging fast localization, time-boxed, "try the most likely first".

**How**:
1. Apply 80/20: check the most error-prone spots first (recent changes, external deps, boundary inputs).
2. Use bisection to shrink scope (comment out half, see if it still happens).
3. Accept "good-enough fast solution" over "perfect slow solution" — but tag it as a heuristic.
4. If the heuristic fails, fall back to systematic methods (algorithms / controlled variables).

**Checklist**:
- □ Did I check the "most likely" spot first?
- □ Can I bisect to shrink the range quickly?
- □ What's my fallback if this heuristic fails?

**Code smell**: Read line-by-line from the top hunting a bug → no heuristic (bisection/recent changes), low efficiency.

🔗 **Pairs with**: #gapanalysis (narrow repro), #controlvariables (bisection isolation), #plausibility (rank candidates)

---

## #optimization
**Position**: Find the best balance among multiple objectives (performance/readability/maintainability/timeline), not single-axis maximization.

**When to use**: Optimizing performance, refactoring, "should I sacrifice Y for X".

**How**:
1. Measure first, find the real bottleneck (don't optimize by gut feel).
2. Be explicit about "what to optimize, what to sacrifice".
3. Target the bottleneck; small-change-big-gain first.
4. Measure again after optimizing, confirm it actually helped and you didn't over-sacrifice.

**Checklist**:
- □ Did I measure before optimizing?
- □ Am I optimizing the real bottleneck or "where I thought it was slow"?
- □ Is the readability/maintainability sacrificed for perf worth it?
- □ Did I measure after to confirm the gain?

**Code smell**: Micro-optimizing before measuring → premature optimization, often optimizes the wrong place and hurts readability.

🔗 **Pairs with**: #utility (is it worth it), #descriptivestats (measure first), #regression (find primary bottleneck)
