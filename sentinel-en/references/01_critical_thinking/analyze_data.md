# Critical Thinking / Analyzing Data (code context)

> Main category color: purple `#6B5CE7`. The layer that reads logs, metrics, and performance numbers — invoked during diagnosis and performance tuning.
> Statistical habits in engineering mostly serve "performance analysis, A/B testing, error-rate interpretation"; no need to force academic rigor.

---

## #confidenceintervals
**Position**: Look at performance and metrics as a "range" rather than a single number, so a single measurement doesn't fool you.

**When to use**: Running benchmarks, looking at API latency, comparing before/after optimization.

**How**:
1. Run the same measurement multiple times (don't conclude from one run).
2. Look at the range and variance of the data, not just the average.
3. When comparing two groups, ask "do their intervals overlap" — if they overlap, there may be no real difference.

**Checklist**:
- □ Is this perf number from one run or many?
- □ Could the before/after delta just be measurement noise?
- □ Am I looking at the average, or also at the worst case (p95/p99)?

**Code smell**: "3ms faster after optimization" but only measured once → could be noise, needs an interval to back it up.

🔗 **Pair with**: #descriptivestats (summarize first), #significance (real diff or not), #distributions (look at shape)

---

## #correlation
**Position**: Distinguish "two things happen together" from "one causes the other" — the biggest source of attribution errors.

**When to use**: "Y broke ever since I changed X", hunting bug-related leads, attributing perf regressions.

**How**:
1. When you observe A and B changing together, tag it as "correlated" first; don't rush to "A causes B".
2. Ask "could there be a third factor C causing both A and B".
3. Use #variablecontrol to actually isolate: move only A and see whether B changes.
4. Only upgrade to causation when you can reproduce "move A → B changes; don't move → no change".

**Checklist**:
- □ Am I saying "correlated" or "causal"? Have I actually isolated it?
- □ Could there be a common cause behind both phenomena?
- □ Is "ever since … then …" real causation, or just coincidental timing?

**Code smell**: Locking onto "the bug appeared after this commit" → could just be timing, no isolation done.

🔗 **Pair with**: #variablecontrol (isolate to verify causation), #complexcausality (trace the real causal chain), #logicalfallacies (avoid post hoc fallacy)

---

## #descriptivestats
**Position**: Use statistical summaries to compress piles of logs/metrics into a few readable numbers.

**When to use**: Facing massive logs, perf data, error distributions — "too much data, can't see anything".

**How**:
1. First look at total, mean, median, max, min.
2. Look at the distribution (how much falls in each range), find anomaly clusters.
3. Use median rather than mean for "typical case" (mean gets pulled by extremes).
4. Visualize the summary (chain into #datavisualization).

**Checklist**:
- □ Am I being misled by the mean — should I look at the median?
- □ Have I looked at max/min (extreme cases)?
- □ Are there obvious anomaly clusters or long tails in the data?

**Code smell**: Staring only at average response time → average gets pulled by a few slow requests; p50/p99 is the truth.

🔗 **Pair with**: #distributions (look at shape), #datavisualization (draw it), #confidenceintervals (look at variance)

---

## #distributions
**Position**: Understand the "shape" of latency, error rates, and load — not just a single average.

**When to use**: Perf analysis (tail latency), capacity planning, judging "how rare is this rare bug".

**How**:
1. Plot the data as a distribution (histogram), check if it's normal, long-tail, or bimodal.
2. Long tail → focus on p95/p99; the few slowest requests are the user's pain point.
3. Bimodal → likely two different scenarios mixed together, should be separated.

**Checklist**:
- □ Is my latency concentrated or long-tail?
- □ Is it bimodal (hinting at two hidden scenarios)?
- □ Am I focused on the typical value or the tail (what users actually feel)?

**Code smell**: "Average is fast" but users complain it's slow → the long tail is biting, the mean hides p99.

🔗 **Pair with**: #descriptivestats (summarize first), #confidenceintervals (look at variance), #multilevelanalysis (split by scenario)

---

## #probability
**Position**: Use probabilistic thinking to estimate "how often this error happens" or "how many retries succeed".

**When to use**: Designing retry/fault-tolerance, estimating blast radius of intermittent bugs, evaluating race-condition probabilities.

**How**:
1. Estimate the failure probability of a single event.
2. Derive the cumulative probability of "at least one failure" over N operations.
3. Use it to decide retry counts, timeout settings, whether idempotent design is needed.

**Checklist**:
- □ How many times will this "rare" error happen across a million requests?
- □ Does my retry strategy account for cumulative failure probability?
- □ "Intermittent" = truly rare, or just hasn't been triggered enough yet?

**Code smell**: "Probability is low, no need to handle" → at scale, low-probability events happen daily.

🔗 **Pair with**: #distributions (distribution backs the estimate), #gametheory (worst case), #estimation (sense of magnitude)

---

## #regression
**Position**: Find "which variable drives the outcome", identifying the main cause from many possible factors.

**When to use**: Perf is affected by many factors, you want to know "which input most affects output", capacity and cost attribution.

**How**:
1. List all input variables that could affect the outcome.
2. Observe/experiment the strength of each variable's relationship to the outcome.
3. Find the few highest-impact variables (80/20) and tackle those first.
4. Watch for variables that influence each other (collinearity).

**Checklist**:
- □ Do I know which factor most affects the outcome?
- □ Am I optimizing factors with tiny impact?
- □ Could multiple factors be entangled, hard to attribute separately?

**Code smell**: Tweaking everywhere without first finding "the biggest bottleneck" → no attribution done, optimizing secondary variables.

🔗 **Pair with**: #correlation (look at association first), #variablecontrol (isolate the main cause), #optimization (optimize against the main cause)

---

## #significance
**Position**: Decide whether a "two-group difference" is real or just random noise.

**When to use**: A/B testing, before/after optimization comparison, "did this change actually work".

**How**:
1. Confirm the sample size is large enough (small-sample differences aren't trustworthy).
2. When comparing two groups, ask "could this difference be purely random".
3. Big interval overlap + small sample → don't rush to claim "it works".
4. Look at both "statistical significance" and "practical significance" (0.1% diff can be statistically significant but meaningless).

**Checklist**:
- □ Is my sample size large enough to make the conclusion credible?
- □ Could this difference just be luck?
- □ Even if statistically different, is the magnitude practically meaningful?

**Code smell**: "New version's conversion rate is higher, ship it!" but only one day of low traffic → undersized sample, probably noise.

🔗 **Pair with**: #confidenceintervals (check overlap), #sampling (sample design), #comparisongroups (control design)
