# Surface Red Flags + Diagnostic Mode (in-action sensors)

> This file is the always-on sensor for "while you're working", parallel to the pre-flight protocol (`preflight.md`):
> - **Before acting**: run the pre-flight protocol in `preflight.md` (inward questions + outward blast radius).
> - **While acting**: the red flags in this file detect surface looping / security shortcuts in real time.
> Core belief: **90% of stuck moments aren't because the solution isn't good enough — you solved the wrong problem or changed the wrong place.**
>
> Note: the original "6 pre-flight self-check questions" have been merged into the "inward" section of `preflight.md` and are not repeated here.

---

## Surface-looping red flag map (detect while working)

| 🚩 You catch yourself… | The real root cause is probably… | Invoke |
|---|---|---|
| Editing the same chunk of code for the 3rd time | Wrong problem definition, not wrong code | #ask-the-right-question #gap-analysis |
| About to add a 3rd `if` special case | Missing an abstraction / data structure designed wrong | #decompose-problem #model-building |
| About to swallow the error with try/except | Muting the alarm, root cause still burning | #evidence-based #complex-causality |
| Adding logs frantically with no direction | No hypothesis, just spray-and-pray | #form-hypothesis #plausibility |
| Tweaking CSS/styles endlessly with no effect | Root cause is in state/render/z-index, not styles | #multi-level-analysis #interpretive-lens |
| Changing the type to `any` to make it pass | Turning off the seatbelt — the type mismatch exists for a reason | #deductive-reasoning #evidence-based |
| Copy-pasting similar code and tweaking it | Missing an abstraction, tech debt is replicating | #decompose-problem #optimization |
| "Just like this for now, fix later" for the Nth time | That "later" is the future root-cause scene | #accountability #ethical-courage |

---

## What to do after a red flag (diagnostic mode steps)

Red flag triggered → **exit "edit-code mode", enter "diagnostic mode"**:

1. **Restate the problem**: write it as "expected X / actual Y / gap Z" (#gap-analysis).
2. **List hypotheses**: list 2-3 possible root causes; don't latch onto one (#form-hypothesis).
3. **Prioritize**: rank investigation order by "plausibility × verification cost" (#plausibility).
4. **Isolate and verify**: with minimal cost and one variable at a time, verify which hypothesis is right (#variable-control #interventional-study).
5. **Confirm root cause**: only return to "edit-code mode" after evidence confirms the root cause (#evidence-based).
6. **🔴 Escalate**: if stuck at heavy tier → produce a root-cause-tree HTML (see html_style_guide.md).

---

## One-line creed

> When you see a red light, don't floor the gas to drive around it; pull over and find out why it's lit.
> Patching the symptom lets you clock out today; fixing the root cause means no overtime later.
