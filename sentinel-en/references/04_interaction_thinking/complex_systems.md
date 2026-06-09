# Interaction Thinking / Complex System Interaction (code context)

> Main category color: green `#0A8A4A`. The layer for tracing cross-layer causality and drawing system maps — the main force for diagnosing complex / cross-module bugs.

---

## #complexcausality　⭐ cross-layer root-cause core
**Position**: trace cross-layer, nonlinear, multi-cause bug causality chains — symptoms and root cause are often far apart.

**When to use**: bug involves multiple modules, symptom and root cause not in the same place, "I changed this — why did that break?" moments. **The main force habit for deep root causes.**

**How**:
1. Don't stop at "where the error popped up" — that's usually the symptom, not the root cause.
2. Trace upstream along data/control flow: where did this wrong value come from?
3. Layer by layer, ask "where did this step's input come from?" until you find the point where the value first went wrong.
4. Watch for nonlinearity: A affects B, B feeds back to A (feedback loop); or it only breaks when A+B happen together.

**Checklist**:
- □ Am I fixing the symptom (where the error occurs) or the root cause (where the error is produced)?
- □ Did I trace upstream along the data flow, or did I stop at the first place that errored?
- □ Is this bug a single cause, or does it require multiple conditions simultaneously?
- □ Is there a feedback loop making causality loop back?

**Code smell**: keep patching the line the error points at but it still breaks → root cause is upstream; that line is just the symptom's stage.

🔗 **Pairs with**: #levelsofanalysis (trace by layer), #systemmapping (draw the causal chain), #gapanalysis (locate where the value went wrong), #variablecontrol (isolate conditions)

---

## #emergentproperties
**Position**: spot emergent problems where "each component looks correct alone, but combined they break."

**When to use**: problems appear after integrating multiple modules, "each was tested but together they break," distributed / concurrent systems.

**How**:
1. When every component's unit test passes but integration breaks → suspect emergence.
2. Look at interactions *between* components: timing, shared state, contended resources.
3. Ask "which component owns this behavior?" — can't answer → it's emergent from interaction.
4. Find the root cause in interactions, not in any single component.

**Checklist**:
- □ Units fine but integration broken — did I look at "interactions"?
- □ Is there shared state / resource contended by multiple parties?
- □ Which component does this bug belong to? (can't answer = emergent)

**Code smell**: "every function is correct but the result is wrong" → emergent problem, root cause is between components, not inside any one.

🔗 **Pairs with**: #complexcausality (trace interactions), #networks (see dependencies), #systemdynamics (timing behavior)

---

## #levelsofanalysis
**Position**: inspect UI / logic / data / network / infrastructure layers separately — don't get stuck on one layer.

**When to use**: bug origin layer unknown, "keep hunting in one layer but can't find it."

**How**:
1. Stratify the system: UI → application logic → data layer → network → infrastructure.
2. Start from the symptom's layer, descend layer by layer asking "is the value/behavior still correct at this layer?"
3. Find the boundary where "upper layer is correct, this layer is wrong" → root cause is at this layer.
4. Don't assume the problem must be in the layer you're familiar with.

**Checklist**:
- □ Am I checking layer by layer, or stuck hammering one layer?
- □ Between which two layers did the value start going wrong?
- □ Am I only hunting in the layer I know well (ignoring others)?

**Code smell**: keep changing the front-end with no effect → root cause may be at the data layer / API; you skipped levels-of-analysis.

🔗 **Pairs with**: #complexcausality (cross-layer tracing), #systemmapping (draw the layers), #perspectives (switch layer to look)

---

## #networks
**Position**: analyze the network structure between modules / services / dependencies — find key nodes and fragile links.

**When to use**: complex dependencies, "change one, break a chain," assessing the blast radius of a change.

**How**:
1. Draw the dependency network (who depends on whom, who calls whom).
2. Find key nodes (depended on by many — changing them has huge impact).
3. Find fragile links (single points of failure, circular dependencies).
4. Before changing, check "what does this node pull on?"

**Checklist**:
- □ Do I know which downstreams this change affects?
- □ Are there circular dependencies / single points of failure?
- □ Which nodes are the "pull one hair, the whole body moves" key nodes?

**Code smell**: changing a shared function without checking who uses it → no network analysis, chain reaction collapse.

🔗 **Pairs with**: #systemmapping (draw the network), #emergentproperties (interaction problems), #complexcausality (trace dependency chain)

---

## #systemdynamics
**Position**: understand the system's dynamic behavior over time — feedback loops, accumulation effects, delayed reactions.

**When to use**: performance degrades over time, memory leaks, "only fails after running a while," when there are feedback loops.

**How**:
1. Observe behavior change over time (not just a single time point).
2. Find feedback loops (positive feedback amplifies, negative feedback stabilizes).
3. Find accumulation effects (memory, queues, connection counts slowly piling up).
4. Watch for delay (cause and effect separated in time, hard to connect directly).

**Checklist**:
- □ Does this problem appear only after "running long / scaling up"?
- □ Is something slowly accumulating (memory / queue / connections)?
- □ Is a feedback loop amplifying the problem?
- □ Is there a time delay between cause and effect?

**Code smell**: "fine at startup, slows / crashes after a few hours" → accumulation effect or leak — a dynamics problem.

🔗 **Pairs with**: #complexcausality (feedback causality), #observationalstudies (long-term observation), #probabilitydistributions (tail behavior)

---

## #systemmapping
**Position**: draw out the system's structure, data flow, causal chains — an external brain for complex problems.

**When to use**: complex system you can't think through, diagnosing cross-module bugs, producing a root-cause tree.

**How**:
1. Draw the system's components, links, data flow as a diagram.
2. Mark each node's expected state vs actual state.
3. Trace the causal chain on the diagram, find where the value started going wrong.
4. That diagram is the foundation of the root-cause-tree HTML.

**Checklist**:
- □ Did I actually draw out the complex system, or rely purely on mental tracing?
- □ Did I mark expected vs actual on the diagram?
- □ Can I point to the root cause's location on the diagram?

**Code smell**: chasing a bug across five files purely in your head → draw the system map; the human brain can't trace that many nodes.

🔗 **Pairs with**: #complexcausality (draw causality), #levelsofanalysis (draw by layer), #datavisualization (visualize), #modelbuilding (externalize the model)
