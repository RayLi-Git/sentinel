# Communication Thinking / Verbal Communication (code context)

> Primary category color: blue `#0D7FBF`. The layer of naming, docs, PRs, commits — invoked during development and collaboration.
> In vibe coding, "write for future-you and your teammates" is core: code is written for humans to read, and incidentally for machines to run.

---

## #audience (#audience)
**Positioning**: Write for the reader (teammate, you-in-three-months, AI), not for "it runs right now".

**When to use**: Naming, writing comments/docs, designing APIs, writing commits.

**How**:
1. Before writing, ask "who will read this, and what do they need to know".
2. Use vocabulary and abstraction levels familiar to the reader.
3. Write out the "why" (the what is obvious from code; the why depends on you saying it).
4. Assume the reader does not have the context currently in your head.

**Checklist**:
- □ Three months from now, will I understand what this does and why?
- □ Did I write down "why this approach"?
- □ Can a reader with the right background understand my names/abstractions?

**Code smell**: Names like `temp`, `data2`, `handleStuff` → no consideration of audience; future-nobody (including you) will get it.

🔗 **Pairs with**: #connotation (names carry meaning), #organization (readable structure), #design-thinking (for the user)

---

## #composition (#composition)
**Positioning**: Effectively organize code / docs / PRs so readers can understand them step by step.

**When to use**: Writing a module, organizing a PR, writing technical docs.

**How**:
1. Put the important stuff up front (key logic and main flow prominent).
2. Keep related things together (high cohesion); separate unrelated things (low coupling).
3. One unit (function/file/PR) does one thing.
4. Top-down: outline first, details after.

**Checklist**:
- □ Does this function/file/PR do exactly one thing?
- □ Are related things grouped together?
- □ Can the reader follow it top-down in order?

**Code smell**: A 200-line function doing five things → no composition, split it. A PR mixing refactor + feature + bugfix → split it.

🔗 **Pairs with**: #organization (structure), #problem-decomposition (split units), #thesis (one main point)

---

## #connotation (#connotation)
**Positioning**: Names must convey the right "implied meaning". When the name misleads, bugs follow.

**When to use**: Naming variables/functions/types, designing APIs.

**How**:
1. Names must state "what it is / what it does / what it returns".
2. Avoid misleading names (`getX` with side effects, `isReady` that returns non-boolean).
3. Follow conventions (plural = collection, is/has = boolean, verb = function).
4. When name and behavior disagree, change the name or the behavior — don't leave it.

**Checklist**:
- □ Does the name accurately reflect behavior/type?
- □ Any "name says A but actually does B" misleads?
- □ Did I follow naming conventions?

**Code smell**: `getUser()` secretly writes to the database → name lies, callers step on the mine.

🔗 **Pairs with**: #audience (name for the reader), #professionalism (conventions), #critical (check for misleads)

---

## #organization (#organization)
**Positioning**: Build clear code/project structure so people know at a glance where things go.

**When to use**: Planning project structure, refactoring, when "files are getting messy".

**How**:
1. Use a consistent, predictable structure (by feature / by layer).
2. Make "where this should go" a clear rule, not something you memorize.
3. Structure reflects the mental model of the system.
4. Reorganize periodically; don't let structure rot.

**Checklist**:
- □ Can a new person guess where something belongs / where to find it?
- □ Does the structure follow consistent rules, or is it ad-hoc?
- □ Does the structure reflect what the system actually is?

**Code smell**: utils.js stuffed with 50 unrelated functions → structure rot, junk drawer.

🔗 **Pairs with**: #composition (content layering), #system-mapping (structure mirrors system), #model-building (structure reflects model)

---

## #professionalism (#professionalism)
**Positioning**: Professionalism in commits, PRs, communication — makes collaboration smooth and history traceable.

**When to use**: Writing commits/PRs, code review, communicating with teammates.

**How**:
1. Commit messages explain "why changed", not just "what changed".
2. PR descriptions include context, approach, how to test, risks.
3. Reviews are about the work, not the person; give concrete, actionable suggestions.
4. Follow team conventions and standards.

**Checklist**:
- □ Do my commits/PRs convey context and intent?
- □ In review, am I giving concrete suggestions or vague criticism?
- □ Did I follow team standards?

**Code smell**: Commit messages all "fix" / "update" / "wip" → history untraceable, future debugging painful.

🔗 **Pairs with**: #audience (for the reader), #emotional-intelligence (review EQ), #accountability (own your changes)

---

## #thesis (#thesis)
**Positioning**: State in one sentence "what this PR/proposal/function does, and why".

**When to use**: Opening a PR, pitching a proposal, writing a function docstring, explaining to someone.

**How**:
1. Force yourself to summarize the core in one sentence.
2. Can't say it in one sentence → this unit does too much, or you haven't thought it through.
3. Put that sentence in the most prominent place (PR title, top of function comment).
4. Everything else exists to support that sentence.

**Checklist**:
- □ Can I state what this does + why in one sentence?
- □ If not, is it because it does too much?
- □ Is my core thesis in the most prominent place?

**Code smell**: A PR title that needs three lines to explain → can't fit in one sentence, split it.

🔗 **Pairs with**: #ask-the-right-question (thesis aligned with purpose), #composition (built around the thesis), #purpose (why you're doing it)
