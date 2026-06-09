# Critical Thinking / Analyze Problems (code context)

> Primary category color: purple `#6B5CE7`. This is the starting layer of any analysis — both "Plan" and "Diagnose" of the five phases call from here.

---

## #breakitdown (#breakitdown)
**Role**: Cut a huge, fuzzy task/bug into small pieces that can each be verified independently.

**When to use**: When facing tasks too big to eat in one bite — "redo the whole module", "this feature is too complex, no idea where to start", "the bug has wide reach".

**How**:
1. Write the task as a one-sentence overall goal.
2. Break it down into 3-7 subtasks that are "mutually independent and individually completable/verifiable".
3. For each subtask ask "can it be broken down further to fit within 30 minutes".
4. Mark dependency order between subtasks, identify "the first piece to touch".

**Checklist**:
- □ Can I individually test whether each sub-piece is correct?
- □ Is any piece still "a blob" that needs further breakdown?
- □ Can I draw out the dependencies between sub-pieces?
- □ Do I know "which piece to touch first"?

**Code smell**: You find yourself touching 5 files and 3 different features in a single commit → no breakdown, back up and chunk it.

🔗 **Pairs with**: #rightproblem (confirm you're breaking down the real problem) → #gapanalysis (define expected for each piece) → #strategize (order execution)

---

## #gametheory (#gametheory)
**Role**: Analyze the strategies and worst cases of multiple parties (users, dependent services, concurrent requests, attackers) under interaction.

**When to use**: Designing APIs/concurrency/cache/permissions, or any scenario where "how the other party reacts" affects correctness; security and race conditions especially need this.

**How**:
1. List all "parties that take actions" (including malicious users, another concurrent request).
2. Ask of each "what's the worst they can do, what's the most selfish thing they'd do".
3. Simulate what state the system enters when these behaviors overlap.
4. Design defenses for the worst combination.

**Checklist**:
- □ Did I assume "the user will operate in the order I expect"?
- □ Will two requests arriving at once collide (race condition)?
- □ Is any party's interest in conflict with my design?
- □ How bad does the system break in the worst case?

**Code smell**: The phrase "this normally won't happen" appearing → that's exactly where the game-theoretic analysis stopped short.

🔗 **Pairs with**: #variables (isolate concurrency variables), #complexcausality (trace interactions), #ethics (malicious parties)

---

## #gapanalysis (#gapanalysis)
**Role**: Lock onto the minimum gap between "expected behavior vs actual behavior" — the starting point of all debugging.

**When to use**: When a bug shows up, a test fails, output doesn't match expectations, or "it just doesn't work". **The first thing to use in the diagnose phase.**

**How**:
1. Write down **expected X**: what I think it should output/do.
2. Write down **actual Y**: what it actually outputs/does (paste real logs/screenshots, no going by impression).
3. Write down **minimum reproduction Z**: the fewest steps to stably reproduce this gap.
4. Lock onto where the gap first appears (which commit / which line / which input value).

**Checklist**:
- □ Can I reproduce this gap with a minimal case?
- □ Is the gap "all wrong" or "only edge cases wrong"?
- □ After which change did this gap first appear?
- □ Am I looking at the actual value, or the value I "assume"?

**Code smell**: The value printed by log ≠ the value you assumed → that delta point is the start of the gap; root cause lies upstream from there.

🔗 **Pairs with**: #rightproblem (confirm the expectation itself is right), #variables (narrow reproduction range), #hypothesis (form hypotheses about the gap)

---

## #rightproblem (#rightproblem)　⭐ default starting point
**Role**: Confirm you're solving the "real problem", not something dreamed up, not just a surface symptom.

**When to use**: **Almost every time.** Pass through it before planning, before touching code, before diagnosing. 90% of stuck moments aren't because the solution sucks — it's that the wrong problem got solved.

**How**:
1. In one sentence, restate "the outcome the user/task really wants to achieve".
2. Ask "why this" three times to climb to the real purpose (the front end of 5-Why).
3. Distinguish "the solution they say they want" from "their real problem" — what they ask for is often a particular solution, not the problem itself.
4. Confirm that what you're changing will actually make that outcome happen.

**Checklist**:
- □ Can I state in one sentence "what really needs to be achieved"?
- □ Is this a real problem, or has a solution been mistaken for the problem?
- □ If I solve it, will the user's real pain disappear?
- □ Am I solving the "easier-to-solve" problem instead of the one that "actually needs solving"?

**Code smell**: You've already started writing code but can't articulate "what this is solving" → stop, ask the right question first.

🔗 **Pairs with**: #purpose (nail down why) → #breakitdown (break down the real problem) → #gapanalysis (define expected). Almost the starting point of every chain.

---

## #variables (#variables)
**Role**: Change one variable at a time to isolate the true cause from noise.

**When to use**: Cause of bug unknown, "I changed a bunch of stuff and it worked but I don't know which one", environment differences (works locally, not in prod).

**How**:
1. List every variable that could affect the result (input, environment, version, config, order, time).
2. Hold everything else fixed, change only one at a time.
3. Record the result change after each move.
4. Find "the one where touching it changes things, not touching keeps things the same" → that is the cause or closest to the cause.

**Checklist**:
- □ Did I only change one thing this time, or several at once?
- □ Did I keep an "unchanged control" to compare against?
- □ Did I list out local vs prod differences and compare one by one?
- □ Can I say "this variable is what caused it" and reproduce?

**Code smell**: "I changed A, B, C and then it worked" → you don't know the root cause, which one fixed it is still a mystery, you'll trip on it again.

🔗 **Pairs with**: #gapanalysis (you need a clear gap before controlling variables works), #controlgroup (build a control), #reproducibility (confirm stability)
