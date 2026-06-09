# Communication Thinking / Nonverbal Communication (code context)

> Main category color: blue `#0D7FBF`. The layer of error messages, API interfaces, architecture diagrams, charts — invoke when designing interfaces and visualizations.

---

## #communicationdesign (#communicationdesign)
**Position**: Design clear error messages, API interfaces, logs — make the system "speak human."

**When to use**: When designing APIs, writing error handling, designing log formats.

**How**:
1. Error messages should say "what went wrong, why, what to do" — not just "Error."
2. API interfaces should be intuitive and hard to misuse (a good interface guides correct usage).
3. Logs should carry enough context (who, when, what input, what state) for future debugging.
4. Design from the perspective of the person using this interface.

**Checklist**:
- □ Can someone tell from my error message how to fix it?
- □ Is my API easy to use right, hard to use wrong?
- □ When things break, are my logs enough for me to debug?

**Code smell**: `throw new Error("error")` or `catch {}` that swallows the message → future you debugs blind.

🔗 **Pairs with**: #audience (design for users), #expression (express clearly), #context (logs with context)

---

## #expression (#expression)
**Position**: Express intent in the clearest form — let the code speak for itself.

**When to use**: When writing any code, choosing what structure expresses the logic.

**How**:
1. Let code structure directly reflect logical intent (reads like an explanation of what it does).
2. Use early returns, clear conditions, meaningful intermediate variables to reduce cognitive load.
3. Add a one-line "why" comment for complex logic.
4. Prefer an extra named variable over one line nobody can read.

**Checklist**:
- □ Does this code read like an explanation of its intent?
- □ Any "clever but obscure" code that should become "dumb but clear"?
- □ Did I explain the "why" at the complex spots?

**Code smell**: A one-liner with three nested ternaries → showing off but unreadable, expression fails.

🔗 **Pairs with**: #audience (for the reader), #semantics (naming carries meaning), #organization (clear structure)

---

## #medium (#medium)
**Position**: Pick the right medium — sometimes one diagram beats a thousand lines of explanation, sometimes the code itself is enough.

**When to use**: When explaining complex systems, writing docs, deciding "text or diagram."

**How**:
1. Structure / flow / relationships → use diagrams (architecture, sequence, state machine).
2. Steps / details → use text or lists.
3. Behavior → use runnable examples / tests.
4. Don't force text to do what a diagram should do.

**Checklist**:
- □ The thing I'm forcing into text — would a diagram be clearer?
- □ Would an example snippet beat the prose explanation?
- □ Is the medium I chose right for this kind of information?

**Code smell**: Three paragraphs describing module dependencies → should be a dependency diagram; text can't carry structure.

🔗 **Pairs with**: #datavisualization (visualize data), #systemdepiction (draw the system), #multimedia (integrate text + image)

---

## #multimedia (#multimedia)
**Position**: Integrate diagrams, tables, text, examples — multi-channel explanation of complex systems.

**When to use**: When writing important docs, explaining complex architecture, doing technical presentations.

**How**:
1. Use diagrams for the big picture (architecture / flow), text for details, examples for specifics.
2. Each medium complements rather than duplicates the others.
3. Keep diagrams and text consistent (don't have them say different things).
4. Complex system doc = architecture diagram + key flow description + examples + edge-case notes.

**Checklist**:
- □ Am I using diagram + text + example complementarily, or just piling on text?
- □ Are all media saying the same thing?
- □ Can the reader enter from any door (diagram / text / example) and still understand?

**Code smell**: A pure-text system doc with zero diagrams or examples → readers struggle to build the big picture.

🔗 **Pairs with**: #medium (pick the medium), #datavisualization (diagrams), #organization (integrate layers)
