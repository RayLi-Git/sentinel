# Three Safety Nets — Defenses for When "Doing It Right" Fails

> Most of Sentinel's mechanisms aim at "doing things right" (protocol foresight, root-cause diagnosis, case files preventing repeats).
> But the real hidden reefs of vibe coding lie in "**after you've already done it wrong**" and "**losing control mid-flight**".
> These three safety nets don't patch "how to write it right" — they patch "**not capsizing during the writing**". Lifeboats, an honest logbook, a chart.

---

## 🪂 1. Retreat Route (Rollback & Recovery)

**The pain**: AI keeps changing things, halfway through realizes the direction was completely wrong, but there's no clean rollback point — only option is to dump everything and restart.

### Before acting: make sure you can retreat
1. Confirm you're at a **clean rollback point** (git status clean / already committed).
   - If not clean → commit or stash first. **Don't pile new changes on a dirty working tree** (when things break, you can't tell what's new).
2. Before big changes, explicitly state a **rollback anchor**:
   > "If this change fails, return to commit `{hash}` / this state."
3. **Split changes into small steps**, each independently verifiable and independently reversible (echoes Iron Rule #5 of the Twelve Commandments: "commit per chunk").

### During the work: when you realize the direction is wrong
4. **Don't keep piling patches on the wrong direction** — this is the sunk-cost fallacy: "I've already changed so much, just a bit more should do it" usually digs the hole deeper.
5. Call a clear stop:
   > "This direction has drifted. Recommend rolling back to `{anchor}` and restarting, because ___. Forcing the save would require fixing ___, more effort than rolling back."

### Judgment: roll back vs keep fixing
| Signal | Decision |
|---|---|
| Tried ≥2 directions, still drifting, changes getting dirtier/more hack-laden | **Roll back** |
| Root cause clear, only finishing touches left, changes still clean | Keep fixing |
| Already changing more places "just to make the earlier mistakes work" | **Roll back** (classic getting-worse-by-rescuing) |

### Connections
- Twelve Commandments #5 (commit per chunk), #12 (commit + progress.md before interruption).
- If a rollback case hits the threshold of pain (misjudged direction / adversarial debugging) → write a case file.
> Matching habits: #UtilityTheory (cost of rollback vs continue) #CriticalThinking (honestly facing a wrong direction) #Accountability (don't shield your own mistakes)

---

## 🔬 2. Evidence Grading (Verification Honesty)

**The pain**: AI loves to say "should be fine" / "I think this is right", but never actually ran it. Conflating "I think" with "I verified" is vibe coding's biggest trust killer.

### Before claiming "done / fixed / should work", you must mark the evidence grade

**🟢 Verified**
- Definition: I **actually executed/tested it** and saw the expected result with my own eyes.
- Must include: what was run (command / test / action), what output was seen.
- Example: "Verified: ran `npm test`, all green; manually submitted the form, new record appeared in DB."

**🟡 Reviewed**
- Definition: I **read the code logic** and confirmed it's correct, but **didn't actually execute**.
- Must include: explicit "haven't actually run it, suggest you run once to confirm".
- Example: "Reviewed: logically should be correct, but I didn't run it — suggest you execute and confirm edge cases."

**🔴 Inferred**
- Definition: I **think it should be right**, but neither verified nor closely inspected.
- Must include: mark `⚠️inferred` + explain how to verify.
- Example: "⚠️inferred: this change should solve it, but I didn't verify; please run ___ to confirm."

### Iron rules
- ❌ Do not use the tone of 🟢 "verified" for 🔴 inferred claims.
- ❌ Saying "I ran it / I tested it" when you didn't — this is the worst breach of trust, worse than the bug itself.
- ✅ When unsure whether you can verify, say it honestly: "I can't verify here, I need you to ___."
- ✅ Environment limits (can't run, can't connect) force you to stop at 🟡/🔴 → state the limit, don't fake 🟢.

### Connections
- Reinforces existing #Verifiability #EvidenceBased.
- Case file "solution" field should mark evidence grade (🟢/🟡/🔴).
- The existing `⚠️inferred` / `‼️missing-data` markers in CLAUDE.md.
> Matching habits: #Verifiability #EvidenceBased #Accountability (honest labeling) #Professionalism (no false reporting)

---

## ⚓ 3. Re-anchoring (Anti-Drift)

**The pain**: As the conversation grows long, AI forgets the original requirement, forgets earlier decisions, contradicts itself, even forgets things it edited just a few turns ago. This is vibe coding's **most lethal and most unique** problem — case files solved "cross-session" memory, but this one solves "**drifting further the longer you talk within one session**".

### When to re-anchor (any of these triggers)
- Conversation already very long / context nearly full.
- About to start a new subtask.
- Feel "I forget what I was originally doing".
- User says "wait, weren't we doing X?" ← **alarm that drift has already happened**.
- Notice your own statements contradict earlier ones.

### Re-anchoring action (30 seconds, output a short alignment)
```
📍 Re-anchor:
· Original goal: {what this task/session was originally to achieve}
· Current progress: {what's done, what step we're on}
· Todo: {what remains}
· Any drift?: {is what we're doing now still aligned with the original goal? If drifted, say so and pull back}
```

### Anti-drift iron rules
- Major decisions and progress get written into `.claude/progress.md` (echoes Commandment #12), **not relying on conversation memory**.
- When self-contradicting, the **written record** wins, not "what was just said".
- Before context fills up, **proactively re-anchor** + remind the user: "Suggest opening a new session and bringing `progress.md` so I can pick up."
- On long tasks, re-anchor at the end of each subphase — don't wait until you're lost to look for the route.

### Connections
- Commandment #12 (progress.md), #1 (PRD is the contract — re-anchor by aligning with PRD).
- Same philosophy as case files: memory belongs in real files, not LLM memory.
- Emergency override: context filling up is also a "stop the bleeding" situation (save first).
> Matching habits: #AskingTheRightQuestion (re-anchor to the real goal) #SelfAwareness (notice you've drifted) #StrategyDevelopment (progress tracking) #OrganizationalStructure (progress.md structure)

---

## The shared spirit of the three

| Safety net | Like what | Solves what |
|---|---|---|
| Retreat route | Lifeboat | When you break things, you can back out — don't sink |
| Evidence grading | Honest logbook | Don't lie about "where I am" |
| Re-anchoring | Chart | Don't lose direction on a long voyage |

> In one line: Sentinel's other mechanisms teach you **how to build the ship well**; these three safety nets teach you **how not to capsize in a storm**.
