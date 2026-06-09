<!-- LANG SWITCH -->

**English** | [繁體中文](./DESIGN.zh-TW.md)

# Design Decisions

> This document records the key design decisions and trade-offs behind Sentinel, from zero to a finished skill.
> The value of a portfolio piece isn't *what* was built — it's *why it was built this way*. What follows is the reasoning.

---

## Starting point: a misread, and a repositioning

The original idea was to take an existing "76 thinking habits" knowledge base and rewrite it as the substrate for vibe coding. The first key insight was this:

> Thinking habits were originally designed for *humans standing at a whiteboard, slowing down to think*. Turning them into a substrate for AI-written code isn't a **translation** problem — it's a **repositioning** problem.

When a human picks a thinking tool, they naturally "pause and judge." But AI moves at superhuman speed; it sees a problem and starts typing. What it's missing isn't *knowledge* (the blade) — it's the *trigger to slow the hand down before swinging* (the sensor).

**This insight set the tone for the whole project: Sentinel's core value isn't "a knowledge base." It's "a stopping mechanism that fires at the right moment."**

---

## Decision 1: Position as a full-lifecycle thinking OS, not a debugging tool

**Options**: (A) A debug tool that activates when stuck. (B) A thinking OS spanning *plan → develop → diagnose → resolve → retrospect*.

**Chose B.** Reasoning: bugs aren't introduced when code is "finished" — they're seeded in the first sketch and the first architectural decision. Firefighting only at the output end means firefighting forever. Move the thinking upstream and the fire dies at the source.

**Consequence**: the five phases are designed as a **loop**, not a line — the "case file" produced in the retrospect feeds the next round of planning, forming a self-improving cycle.

---

## Decision 2: Trigger philosophy — always-on, with three-tier intensity scaling

**Tension**: the positioning is "full-lifecycle," which ideally means always on. But skills are normally triggered by keyword detection. Set too broad → even fixing a typo runs the full ritual, which is annoying. Set too narrow → back to "fire extinguisher" mode.

**Resolution**: always-on (auto-activates for engineering tasks) + **explicit three tiers** (🟢 light / 🟡 medium / 🔴 heavy), with thinking intensity scaled to task weight.

**Key discipline**: between tiers, **only upward, never downward**. Heavy tasks cannot be downgraded or skipped. This is deliberate — it's designed to bind the future "rushing, looking-for-shortcuts" version of yourself, because rushing is exactly when technical debt gets buried.

**Pressure relief valve**: a narrow "emergency override" — when genuinely urgent, do the minimum to stop the bleeding, but the override **auto-stamps `[SKIPPED]`** and queues a root-cause follow-up in the retrospect. The escape hatch comes with a built-in debt-repayment mechanism.

---

## Decision 3: Context budget — SKILL.md is a doorpost sign, not an encyclopedia

**Insight**: `SKILL.md` is **always loaded into context in full**; only `references/` are loaded on demand. So the main file has to stay lean — its job is "to point the way and decide when to act," not "to hold all the knowledge."

**Three iron rules**:
1. `SKILL.md` only carries "when to trigger + the pause protocol + pointers."
2. The "surface-loop checklist" must be extremely short (it's read every time work starts).
3. The case-log flow file is **never read in full proactively** (a two-file design: at work start, only the condensed `patterns.md` is read).

The final main file is ~225 lines — well under the 500-line safety threshold.

---

## Decision 4: Rewriting the 87 habits — from "analyzing human problems" to "analyzing code problems"

All 76 habits (later expanded to 87) were deeply rewritten in code context, each using the same 6-column template: **positioning / when to use / how to use / checklist / code smells / 🔗 companion habits**.

- The **"code smells"** column is the key — it turns abstract habits into detectable signals: "if this symptom appears, use this habit" (e.g. "one commit touches 5 files," "this normally never happens").
- The **"🔗 companion habits"** column weaves isolated habits into a network — building "don't loop at the surface, chase it to the root" thinking chains.

**Indexed two ways**: habits stored by four categories (avoids cross-phase duplication), plus a "phase → habits cross-reference" table. This resolves the tension that "the same habit gets used across phases" would otherwise either duplicate or lose habits.

**Source attribution — honest labeling**: the original 76 habits come from the world-class thinking habits framework (Critical 29 / Creative 17 / Communication 10 / Interaction 20). The fifth category added later — "Security thinking" with 11 habits — **does not come from that framework. It was designed in-house to address vibe coding's security needs** (input & trust boundaries / secrets & least privilege / authentication & attack surface / dependencies & supply chain). Throughout the documentation we consistently mark this as "76 world-class + 11 original = 87" rather than dressing the in-house additions in someone else's source — that's basic portfolio integrity, and it also lets the contribution "I extended an existing framework with original work" be seen.

---

## Decision 5: Self-improving case files — memory must live in real files

**Technical reality**: Claude Code is amnesic per session and won't remember the last case file. So "auto-recording" can't rely on memory — it has to **write to real files**, and the next session inherits memory by **reading them at work start**.

**Two-file architecture**: `debug-log.md` (running journal, grows over time) + `patterns.md` (condensed essence, always lean, the only thing read at work start). Even with thousands of journal entries, the per-session context stays unaffected.

**Condensation cadence** (closes the "lessons get lost overnight" loophole): auto-condense at 10 entries / condense first if ≥3 entries at work start / quick-read for 1-2 entries. Guarantees that no matter the entry count, the next session reads what matters.

---

## Decision 6: The most important fix — "the threshold of pain" changed from *count-based* to *phenomenon-based*

This was the iteration that **taught the most through actual testing**.

**Problem**: the v1 threshold said "stuck more than once." In testing, the AI misread it as "log it once 3 mistakes pile up," "make consecutive mistakes to hit the bar," and even counted "user corrected me" as one of the strikes.

**Root cause**: the rule was vague. The word "count" is easily misinterpreted.

**Fix**:
1. Changed "stuck more than once" to "**adversarial debugging: ≥2 hypotheses in different directions were falsified**" — replacing "count" with "adversarial."
2. Added an 8-item "**absolutely doesn't count**" list, explicitly blocking misfires (including "user correction").
3. Promoted to "**evidence as a required field**" — the case-file schema itself requires you to fill in "which hypotheses were falsified," **and if you can't produce the evidence, you can't produce a valid case file**. This turns an abstract judgment into a checkable procedural gate.

**Lesson**: rules that depend on the AI's subjective judgment misfire when boundaries are fuzzy. **Procedural enforcement** (requiring externalized evidence) is far stronger than rule statements.

---

## Decision 7: The rehearsal protocol — bound to "action," not "phase"

Originally, the "pre-action rehearsal" was bound to "adding a feature." But one counter-question overturned it: **doesn't bug-fixing also need rehearsal?**

**Insight**: bug-fixing means "touching existing, *running* code" — the risk of breaking existing behavior is **higher than adding features**. The real trigger isn't "adding a feature," it's "**am I about to touch existing code?**"

**Final design**: the rehearsal protocol is bound to **action** (touching existing code triggers it), not phase or scenario — no blind spots. And the previously separate "6-question self-check (inward)" and "5-action rehearsal (outward)" are fused: ask inward "have I thought this through?" and project outward "what am I about to crash into?"

---

## Decision 8: Three safety nets — the line of defense when "doing it right" fails

The final insight: every mechanism above is about **doing it right**. But the real hazards in vibe coding lurk in **after something goes wrong** and **drift while you're working**.

So three safety nets were added:
- **Retreat route** (the lifeboat): when something breaks, you can safely roll back — no patching on top of the bug to "rescue" it.
- **Evidence grading** (the honest captain's log): any "done" claim must be tagged "verified / reviewed / inferred" — closing the gap of "didn't actually run it but said I did."
- **Re-anchoring** (the chart): in long sessions, prevent drift; commit major decisions to `progress.md` instead of trusting conversation memory.

---

## Overall architecture: two always-on files + one on-demand library

| Layer | Role | Analogy |
|---|---|---|
| `CLAUDE.md` | Always-on identity & startup rules | ID badge (always worn) |
| `SKILL.md` | Always-on pointers + trigger protocol | Doorpost sign (points the way) |
| `references/` | On-demand detailed knowledge | Library stacks (visited when needed) |

The principle runs through everything: **"identity and rules always on, detail loaded on demand"** — making sure the mechanism *will* fire while not blowing up the context.

---

## Scope & Future Work

> The list below is *not* a TODO. The current Sentinel is complete and usable. This section records where the design's boundaries currently sit and what directions further evolution could take. It's a deliberate reflection, not a gap.

- **Empirically driven**: the misread of the threshold of pain was only caught by real testing (the v1 "stuck more than once" was misread as a count). Earlier small-scale testing would have caught the fuzziness sooner — that's the most honest lesson from the process.
- **Measurability**: the "surface-loop" detection still depends on AI judgment. A future direction is to explore more programmatically verifiable signals (e.g., reading `git log` to count how many times the same file gets re-edited), making triggers more objective.
- **Cross-project learning**: case files currently accumulate per project. A future design could introduce "cross-project shared patterns" so experience transfers across projects — but this first requires handling privacy (project-specific sensitive info) and noise (project A's pitfall may not apply to project B). Deferred for now as a deliberate complexity trade-off.
