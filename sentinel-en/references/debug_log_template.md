# Project Case File System — Format, Thresholds, Evidence Checks

> Sentinel's self-improving loop. All files live under the current project's `.claude/` directory; git carries memory across sessions.
> Claude Code forgets every session, so memory must land in real files and be inherited via "read first at start of work".

---

## File Structure

```
.claude/
├── debug-log.md          ← Running log (append-only), accumulates long-term
├── patterns.md           ← Distilled page (high-frequency surface patterns, read first at start of work), always lean
└── root-cause-trees/     ← Root-cause tree HTML library
    └── {date}_{description}.html
```

> ⚠️ This file (debug_log_template.md) is the "format spec for the case file", not the case file itself. It lives under the skill's references/ and is loaded on demand; the real case file grows inside your working project's `.claude/`.

---

## 1. Threshold of Pain (three criteria; meet ANY one to write a case file)

### ① Misidentified root-cause direction
I first **believed** the root cause was in A, modified A, then **confirmed the root cause was actually in B**.
- Key: **wrong direction was committed to**, not "fixed a typo".
- ✅ Example: thought onSubmit wasn't bound, kept changing the binding with no luck; later found it was a stale closure capturing an old value.
- ❌ Example: wrong variable name, one-shot fix.

### ② Adversarial debugging
For the **same bug**, proposed **≥2 hypotheses in different directions** and tested them; earlier ones were **falsified** before the real root cause was found.
- Key: **different-direction hypotheses falsified**, not "edited a few times".
- ✅ Example: bug appears → hypothesis "API is slow" → measured, negated → hypothesis "render order" → tried, no good → hypothesis "state management" → hit.
- ❌ Example: rewrote the same code 3 times because of typos.

### ③ Root cause crosses layers
The **layer** where the symptom appears ≠ the **layer** where the root cause lives.
- Layer examples: UI / application logic / state management / API contract / data layer / infrastructure.
- ✅ Example: symptom is button click does nothing (UI layer); root cause is API response format changed (contract layer).
- ❌ Example: symptom is a function returns wrong; root cause is in the same function.

---

## 2. Cases that Absolutely Don't Count (prevent false triggers, **most important**)

Even if they look qualifying on the surface, these **never** become a case file:

| ❌ Doesn't count | Reason |
|---|---|
| User corrects Claude "you wrote it wrong, fix it" | That's communication correction, not debug stuckness |
| Several unrelated small errors piling up (typo + missing import + typo) | Each independent, each fixed in one shot, no "stuck" |
| Stringing failed attempts together just to qualify for writing a case | Means-ends reversal, violates the spirit of pain threshold |
| Refactoring the same code several times for taste/readability | No "fail → falsify" adversarial element |
| Compile/type errors fixed in one go | One-shot fix doesn't count as stuck |
| Same file edited multiple times in a short window | Edit count ≠ adversarial debugging |
| Multiple adjustments because requirements changed | Requirement changes aren't bugs |
| Back-and-forth while exploring a new framework | Learning is not stuckness |

---

## 3. Case File Format (evidence is built in; the fields themselves act as the threshold check)

> Design principle: **evidence is part of the case-file field** — filling out a case naturally means filling out the evidence; a field you can't fill = this one shouldn't be a case file. The gate is hidden inside the fields.

```markdown
## [YYYY-MM-DD] {one-line problem title}

### 🎯 Pain Threshold Passed
(Tick at least one, **and you MUST fill the matching evidence section**; if you can't bring yourself to tick or can't fill in evidence → don't write this entry)
- [ ] ① Misidentified root-cause direction
- [ ] ② Adversarial debugging
- [ ] ③ Root cause crosses layers

### 📋 Evidence (fill the block matching the threshold ticked; unticked ones may be omitted)

#### If ① ticked: Misidentified root-cause direction
- I first believed the root cause was in: ________________________________
- After changing it (why it was confirmed wrong): ____________________
- Actual root cause is in: ____________________________________

#### If ② ticked: Adversarial debugging (≥2 falsified hypotheses)
- Hypothesis 1: __________________________________
  How falsified: ________________________________
- Hypothesis 2: __________________________________
  How falsified: ________________________________
- (Add 3, 4... as needed)
- Hit root cause: ________________________________

#### If ③ ticked: Root cause crosses layers
- Layer where symptom appeared: __________________________
- Layer where root cause lives: __________________________
- Why the two were conflated (one line): ______________

### ✅ Fix
{Concrete fix targeting the root cause}

### 🚩 Red Flags Triggered (if any)
{Which surface-looping or security red flag was hit}

### 🧠 Thinking Habits That Helped
{#which habits helped}

### 💊 How to Spot It Earlier Next Time
{What signal next time should make me think of this root cause}

### 🌳 Root-Cause Tree
root-cause-trees/{YYYYMMDD}_{description}.html
```

---

## 4. Three Self-Check Questions Before Writing

Before appending to debug-log, Claude must pass these three questions. Any "no" → **do not write**.

1. Did this really involve "**committing to the wrong direction**" or "**multiple different hypotheses falsified**" or "**crossing layers**"? (Was the threshold actually met?)
2. Am I just hitting a count, when it's really independent small things or communication corrections? (Am I padding?)
3. If I don't write this in, will I "step on the same root cause again" next time in a similar situation? (Is there real reuse value?)

> 🟢 Small problems that are obvious at a glance, one-shot fixed, root cause at the symptom site → don't log.
> 🟢 Rather miss one than dilute. `patterns.md` is read every start-of-work; padding it weakens it.

---

## 5. Special Record for Emergency Skips

When stopping the bleeding under emergency, write a one-line placeholder first; complete during retro:
```markdown
🔴[SKIPPED] {YYYY-MM-DD} {problem} — emergency stop-bleed, root cause not investigated, pending retro
```
At retro, pull out all `[SKIPPED]` markers, chase the root cause, and **run through sections 3–4 in full** to rewrite into a complete case file (with evidence section).

---

## 6. Distilled Page Format (patterns.md, read first at start of work)

The high-frequency patterns distilled from debug-log. **Keep it very short** (this page is read every start-of-work):

```markdown
# Common Traps in This Project (read first at start of work)

## 🔥 Top Surface-Looping Patterns
1. {pattern}: symptom "{what you see}" → most-likely root cause "{actual}" → check "{where}" first
2. ...

## 🧱 Project-Specific Traps
- {Specific pitfalls of this codebase / tech stack}

## 📊 My Habitual Blind Spots (self-awareness)
- {Types of judgment errors I repeatedly make}
```

---

## 7. Distillation Trigger Rules (lessons never sleep over)

Distilling from debug-log (running log) → patterns (distilled). **Triggered if ANY of the following holds**:

| Condition | Action |
|---|---|
| A. debug-log has **10 entries** undistilled | Auto formal distillation into patterns.md |
| B. At start of work, **≥3 entries** undistilled and new | Formal distillation before starting work |
| B'. At start of work, **1-2 entries** undistilled and new | No formal distillation, but quickly read these entries and fold into this session's thinking |

> This guarantees: no matter how many entries accumulate, the next start-of-work definitely reads them — no "the lesson is still in the running log while you're already stepping in it".

---

## 8. What to Do When Distilling (#inductive reasoning + #self-awareness)

1. Generalize multiple similar cases into "one pattern".
2. Find recurring root-cause categories → promote to Top Patterns.
3. Find recurring judgment blind spots → write into "Habitual Blind Spots".
4. Keep patterns.md lean; old low-frequency patterns can drop down (kept only in debug-log).

---

## 9. Initialization

If the project doesn't have a `.claude/` case file yet, on the first qualifying case:
1. Create `.claude/debug-log.md` (with a title).
2. Create `.claude/root-cause-trees/` directory.
3. `patterns.md` is created only on first distillation.
4. Remind the user to add `.claude/` to git so memory persists across sessions/machines.
