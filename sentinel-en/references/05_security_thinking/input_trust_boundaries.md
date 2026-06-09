# Security Thinking / Input & Trust Boundaries (code context)

> Main category color: deep teal-blue `#1E3A8A`. Security's first line of defense — separate who is trusted from who is not.
> Core belief: **everything from outside the system is hostile by default, until validated.**

---

## #untrustedinput　⭐security starting point
**Position**: all external inputs (users, APIs, files, env vars, URL params) are poisonous by default — validate/sanitize before use.

**When to use**: **anywhere external data is received**. Forms, API endpoints, file uploads, query strings, third-party responses, even config files.

**How**:
1. Mark "is this value from outside the system?" — yes → treat as untrusted.
2. Validate at the trust boundary: type, length, format, range, allowlist.
3. Use allowlists (only known-good) rather than blocklists (block known-bad).
4. Reject on validation failure; don't "try to fix" suspicious input.

**Checklist**:
- □ Is this value external? Did I just use it as if trusted?
- □ Am I using an allowlist (permitted) or a blocklist (forbidden)?
- □ Did I validate edges (oversized, empty, special chars, encoding attacks)?
- □ On validation failure, do I reject or "guess what they meant"?

**Code smell**: directly using `req.body.xxx` / `params` for string-concat or DB queries → no trust boundary crossed, injection enters here.

🔗 **Pair with**: #trustboundary (mark the boundary), #injectionprevention (sanitize), #gametheory (think malicious input)

---

## #trustboundary
**Position**: explicitly mark "where is internal/trusted vs external/untrusted" — check when data crosses.

**When to use**: designing system architecture, APIs, module interfaces, cross-service comms.

**How**:
1. Draw the system's trust boundaries (frontend↔backend, service↔service, app↔DB, your code↔third-party).
2. For each cross-boundary data flow, mark "trusted to untrusted" or vice versa.
3. Untrusted→trusted direction: must validate/sanitize.
4. Don't assume "everything inside one system is trusted" (internals can be compromised too).

**Checklist**:
- □ Can I draw my trust boundaries?
- □ Does every cross-boundary entry point have a check?
- □ Am I assuming "internal calls are safe"?
- □ Frontend validation — does the backend redo it? (Frontend validation doesn't count.)

**Code smell**: "frontend already validated, backend doesn't need to" → trust-boundary mis-judgment; frontend can be bypassed.

🔗 **Pair with**: #untrustedinput (validate at boundary), #systemmapping (draw boundaries), #leastprivilege (cross-boundary auth)

---

## #injectionprevention
**Position**: unified thinking for SQL/command/XSS/path injection — never let "data" be executed as "code/command".

**When to use**: building SQL, running system commands, assembling HTML, reading file paths, eval, building any string "that will be interpreted".

**How**:
1. Always use "parameterized/prepared" rather than string concat (SQL → prepared statement; commands → arg arrays).
2. Escape contextually before output to HTML.
3. Normalize file paths + restrict to allowed dirs (prevent path traversal).
4. Never run eval / exec / dynamic import on external input.

**Checklist**:
- □ Is my SQL parameterized or string-concatenated?
- □ Could user input be executed as HTML/JS/command?
- □ Could a file path escape the allowed range via `../`?
- □ Did I use eval-like dangerous functions on external input?

**Code smell**: `"SELECT * WHERE id=" + userId` or `exec("cmd " + input)` → textbook injection holes.

🔗 **Pair with**: #untrustedinput (input sanitize), #communicationdesign (safe interfaces), #critical (attack your own concat)
