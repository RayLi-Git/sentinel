# Creative Thinking / Applied Research Methods (code context)

> Primary category color: orange-yellow `#D4900A`. The layer for designing tests, verifying causality, and ensuring reproducibility — invoke during diagnostic verification and A/B testing.

---

## #sampling
**Position**: Design representative test-case samples. Don't only test the happy path.

**When to use**: Writing tests, verifying fixes, when you "tested a few and called it good."

**How**:
1. Don't only test normal values — deliberately sample boundaries, extremes, anomalies, nulls.
2. Sample from the real data distribution, covering situations that actually occur.
3. Make sure samples cover various user/environment/input types.
4. Critical edge cases, though few, need explicit coverage guarantees.

**Checklist**:
- [ ] Did my tests only cover the happy path?
- [ ] Did boundary/extreme/anomalous inputs get sampled?
- [ ] Do my test cases reflect real usage distribution?

**Code smell**: Tests only cover "normal input → correct output" → boundaries untested, blows up after shipping.

🔗 **Pairs with**: #verifiability (test design), #deductivereasoning (case coverage), #significancetesting (sample size)

---

## #casestudy
**Position**: Drill deep into one extreme/typical case, extract generalizable principles.

**When to use**: When facing a particularly tricky or typical bug, when you want to thoroughly understand a class of problems.

**How**:
1. Pick the most representative or most painful case, drill to the bottom.
2. Fully reconstruct its context, root cause, solution.
3. Extract "generalizable lessons for this class of problem."
4. Write into the case file, turn into a pattern.

**Checklist**:
- [ ] Did I really drill to the bottom of this case?
- [ ] Can I extract generalizable lessons from it?
- [ ] Did I record it into the case file for future reference?

**Code smell**: Solving a hard bug and forgetting it without distilling → wasting a high-value case.

🔗 **Pairs with**: #inductivereasoning (generalize from cases), #studyreplication (verify), #selfawareness (settle into case file)

---

## #comparisongroups
**Position**: Use control groups to isolate variables — before/after, A/B, working vs broken.

**When to use**: Hunting root cause of differences, verifying fix effectiveness, "why does this work but that doesn't."

**How**:
1. Set up a "control group" (working version/environment/input).
2. Compare item by item against the "experimental group" (broken one).
3. Find the single key difference.
4. Verify: introduce that difference into the control group, see if it also breaks.

**Checklist**:
- [ ] Do I have a "normal control" for comparison?
- [ ] Did I list and compare the differences between the two groups one by one?
- [ ] Can I reproduce the problem by "manufacturing the difference"?

**Code smell**: "This one works, that one doesn't" yet never comparing the two → leaving a ready-made control group unused.

🔗 **Pairs with**: #variablecontrol (isolate variables), #situationalcontext (compare contexts), #verifiability (before/after)

---

## #interventionalstudy
**Position**: Design "actively change one thing, observe the change in result" experiments to verify causality.

**When to use**: Verifying a root-cause hypothesis, confirming "is it really what caused it."

**How**:
1. Based on hypothesis, design a minimal intervention (change one variable).
2. Predict "if the hypothesis is right, after the intervention we should see…"
3. Execute the intervention, observe whether results match prediction.
4. Match → hypothesis supported; no match → eliminate, try another hypothesis.

**Checklist**:
- [ ] Is my intervention "changing only one variable"?
- [ ] Did I predict the result before executing (rather than rationalize after)?
- [ ] Do results actually support the hypothesis, or am I forcing the interpretation?

**Code smell**: Changing things and watching results, but changing several places at once → unclean intervention, ambiguous causality.

🔗 **Pairs with**: #buildhypothesis (intervention verifies hypothesis), #variablecontrol (single intervention), #comparisongroups (control)

---

## #interviewsurvey
**Position**: Design effective user feedback collection. Ask the right questions to get real information.

**When to use**: Bug came from a user report, understanding requirements, collecting usage info.

**How**:
1. Ask "what specifically happened" rather than "what do you think is wrong" (users often misjudge causes).
2. Have them reconstruct steps, environment, expected vs actual.
3. Distinguish "user-stated cause" from "actual phenomenon."
4. Collect concrete, reproducible info — not vague impressions.

**Checklist**:
- [ ] Am I asking about "phenomena" or letting the user "guess the cause"?
- [ ] Did I get concrete reproducible steps?
- [ ] Did I separate the user's "description" from "actual"?

**Code smell**: Following the user's "I think X is broken" and directly modifying X → users' attributions are often wrong.

🔗 **Pairs with**: #psychologicalcauses (understand user), #gapanalysis (get expected vs actual), #sourcequality (verify reports)

---

## #observationalstudy
**Position**: Observe behavior from real usage data/logs, not just manual tests.

**When to use**: Hunting hard-to-reproduce bugs, understanding real usage patterns, monitoring production behavior.

**How**:
1. Instrument observations (log/metrics/tracing) in the real environment, collect passively.
2. Find patterns and anomalies in real data without disturbing the system.
3. Watch for observation bias (you only see what's logged).
4. Direct observation results toward controlled experiments for verification.

**Checklist**:
- [ ] Do I have real usage data, or am I relying only on my own tests?
- [ ] Does my instrumentation have blind spots (places not logged)?
- [ ] Did I verify causality for patterns I observed?

**Code smell**: Hard-to-reproduce bugs only guessed at locally → should add instrumentation to collect from the real environment.

🔗 **Pairs with**: #descriptivestatistics (analyze observations), #correlation (find patterns), #studyreplication (from observation to reproduction)

---

## #studyreplication
**Position**: Ensure bugs, results, and fixes can be "reliably reproduced" — if you can't reproduce, you can't confirm it's solved.

**When to use**: Throughout debugging, verifying fixes, "only occasionally appears" problems.

**How**:
1. Find the minimal steps that "reliably reproduce" the bug — this is the foundation of debugging.
2. Intermittent bug → first find ways to raise the reproduction rate (load stress, control timing, amplify conditions).
3. After the fix, use the original reproduction steps to confirm it no longer happens.
4. Bake the reproduction steps into a test to prevent regression.

**Checklist**:
- [ ] Can I reliably reproduce this bug? (If not, you're not ready to fix it.)
- [ ] For intermittent issues, did I try to raise the reproduction rate?
- [ ] After the fix, did I verify with the original steps?
- [ ] Did the reproduction steps become an automated test?

**Code smell**: "It breaks sometimes" then starting to guess-and-modify → no reproduction means no verification, modifying is gambling.

🔗 **Pairs with**: #gapanalysis (minimal repro), #verifiability (verify fix), #situationalcontext (reconstruct context)
