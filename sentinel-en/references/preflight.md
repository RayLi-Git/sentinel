# Pre-flight Protocol — run this before you touch existing code

> **Trigger = an action, not a phase**: any time your hand is about to touch existing, running code (additions that brush against existing logic, bug fixes, refactors, config/dependency changes), **regardless of which of the five phases you are in**, run this protocol first.
> Does not apply to: pure standalone additions (brand-new files, no existing logic touched), comment/copy/typo edits.
>
> Core belief: **writing code fast is not the skill; touching code without breaking what's already there is.** Like a surgeon's three minutes before the incision — every place that could bleed gets opened up in your head first.

---

## Two halves of the protocol: ask inward + project outward

The pre-flight protocol fuses two directions of thinking:

- **Inward (have I thought it through)**: am I asking the right question, symptom vs root cause, can I verify.
- **Outward (what will I crash into)**: blast radius, ripple effects, pre-mortem.

Run both halves — only then have you "thought it through before acting".

---

## Trigger and depth

| Situation | Which version |
|---|---|
| 🟡 Touching existing code but small scope, no shared objects/security surface | **Lite version** (one pass, under 30 seconds) |
| 🔴 Wide reach / **touches shared objects** / **touches security surface** | **Full version** (point by point, produce a protocol checklist) |

**Auto-upgrade to full version (any one trigger):**
- Shared objects: shared functions / shared state / database / API contract / shared type definitions / config files
- Security surface: authentication / authorization / PII / payments / secrets

---

## Lite version (🟡, one pass)

Quick self-check before acting; only proceed when every item is "no issue / no risk":

**Inward:**
1. Right question: what I'm about to touch — real problem, or one I made up in my head?
2. Symptom vs root cause: (for bug fixes) am I touching the source, or the place the error surfaces?

**Outward:**
3. Blast radius: what existing things will this touch? Who uses what I'm about to change?
4. Chain risk: will the things I touch break?
5. Safe approach + verification: how do I avoid breaking existing behavior? Once changed, how do I prove it actually works?

> Any item surfaces "touches shared objects / security surface" or "can't articulate clearly" → upgrade to full version immediately.

---

## Full version (🔴, point by point)

### Inward ── have I thought it through

**A. Right question**
- In one sentence, restate "the real outcome to achieve". If it doesn't match → stop.
- (Bug fix) Symptom vs root cause: am I touching the source or where the error surfaces?
- (Bug fix) Minimum repro: can you state "expected X / actual Y / delta Z"? If not, don't touch.
> Habits: #right-question #gap-analysis #complex-causation

### Outward ── what will I crash into

**B. Blast-radius prediction**
- Which files / functions / components will change?
- Which shared state / global variables will be read or written?
- Will it touch DB schema / API contract / type definitions?
- **Who is calling what I'm about to change?** (walk upstream to callers — most commonly missed)
> Habits: #network-analysis #system-mapping

**C. Ripple-effect prediction**
- For each thing listed in B, **will it break?**
- Does anywhere else depend on its "original behavior"?
- Change a shared function → will other call sites be affected?
- Change a data structure → will existing data / serialization / cache become incompatible?
> Habits: #complex-causation #emergence

**D. Safe-path design**
- Can you **add instead of modify** (new function vs editing the old one)?
- Do you need a compatibility layer / gradual migration / feature flag?
- How do you order the changes so each step is independently verifiable and revertible?
- Which existing tests must still pass?
> Habits: #strategize #constraints #least-privilege

**E. Pre-mortem risk (assume it has already broken in production)**
- Imagine it shipped and broke — looking back, where is it most likely to blow up? (boundaries / concurrency / nulls / large data / network failure)
- Which edge case did I not plan to handle, but actually will occur?
- If upstream / third party returns something unexpected, what happens here?
- On error, fail closed (safe) or fail open (dangerous)?
- After the fix, how do I **prove** it really works rather than looks like it works? (verifiability)
> Habits: #critical #gametheory #sampling #verifiability
> 🔴 Touches security surface → also run the five security habits (#distrust-input #authn-authz #least-privilege #sensitive-data #secure-defaults)

**F. Claude's own additions**
> "Beyond the above, for **this specific situation** I think we should also think ahead about ___"

Proactively call out task-specific concerns the generic checklist doesn't cover (time zones → DST; money → float precision; files → concurrent writes…).

---

## Protocol checklist output (🔴 full version only)

After the full version, before acting, output a short checklist for the user to see:

```
🛫 Pre-flight: {thing being touched}
Inward｜right question: {real goal} (bug fix also lists symptom vs root cause)
② Blast radius: {files/functions/state touched}
③ Chain risk: {what may be affected, and why}
④ Safe approach: {how not to break existing behavior, change order}
⑤ Pre-mortem risk: {most likely failure points + mitigation + how to verify}
⑥ Extra considerations: {Claude's additions for this situation}
→ Confirm direction, then start
```

> If the checklist surfaces a major risk/tradeoff, per user preference offer ≥4 options to let the user pick a direction.

---

## How it links with other mechanisms

- Protocol done → act → if something breaks, enter "Diagnose" → if painful enough, write to the case file.
- If protocol E predicted a risk and it later materializes → mark the case file "predicted by protocol", reinforcing patterns.
- If protocol E did **not** predict it and it blew up → retro on "why the protocol missed it", high-value #self-awareness.
- PRD tasks: protocol B blast radius should align with the PRD section, no expansion beyond what the PRD specifies (echoes Twelve Commandments §10 YAGNI).
- Surface-looping red flags / security red flags (see `self_check.md`) are independent sensors; they can light up mid-action, in parallel with this protocol.
