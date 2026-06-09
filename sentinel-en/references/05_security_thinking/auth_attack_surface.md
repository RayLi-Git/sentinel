# Security Thinking / Auth & Attack Surface (code context)

> Category color: deep teal-blue `#1E3A8A`. Guard the entrances, imagine the attacker, secure by default — the proactive defense layer.

---

## #authnz
**Role**: Separate "who you are (authn)" from "what you can do (authz)". Check at every entrance.

**When to use**: Designing login, API permissions, or any operation that requires identity.

**Actions**:
1. Design authentication (who you are) and authorization (what you can do) separately. Don't conflate them.
2. Check authorization at **every** sensitive endpoint. Don't just hide buttons on the frontend (the backend still has to block).
3. Check "does this logged-in user have permission to access this specific record" (prevent IDOR).
4. Use mature auth schemes. Don't invent your own crypto / session mechanism.

**Checklist**:
- □ Am I treating "logged in" as "permitted to do anything"?
- □ Does the backend verify authz on every sensitive operation, or am I only relying on frontend hiding?
- □ Can user A change an id and access user B's data? (IDOR)
- □ Am I rolling my own crypto / token? (Don't.)

**Code smell**: `/api/user/123` only verifies "logged in" but not "is this the actual owner" → change the id and you see someone else's data (IDOR).

🔗 **Pairs with**: #leastprivilege (authz scope), #trustboundary (check every entrance), #untrustedinput (verify id ownership)

---

## #attacksurface　⭐ extends game theory
**Role**: Enumerate all externally exposed points and think like an attacker — "where would I hit?"

**When to use**: Designing new features/endpoints, pre-ship review, evaluating security risk.

**Actions**:
1. Enumerate every external surface: APIs, forms, uploads, URL params, files, third-party webhooks, environment.
2. For each surface, ask "how would an attacker abuse this?"
3. Think through typical attacks: injection, privilege escalation, brute force, DoS, replay, malicious file upload.
4. Shrink the attack surface (close unused endpoints / features / ports).

**Checklist**:
- □ Can I enumerate every external surface?
- □ For each surface, how could an attacker abuse it?
- □ Any "forgot to close" test endpoints / debug interfaces still exposed?
- □ Can I shrink the attack surface (remove unnecessary exposure)?

**Code smell**: Debug endpoints, `/test`, an open admin interface forgotten and shipped → attack surface wide open.

🔗 **Pairs with**: #gametheory (think adversarial), #critical (attack yourself), #leastprivilege (limit damage)

---

## #securebydefault
**Role**: On failure, "fail closed". All defaults pick the safest option.

**When to use**: Designing error handling, default settings, permission checks, exception handling.

**Actions**:
1. When a permission check errors / is uncertain, default to "deny", not "allow".
2. On exception, do not fall back to "skip the check and let it through".
3. All default settings pick the safest (strictest) option. Loosening requires the user to opt in.
4. Error messages: terse externally (don't leak system details), detailed internally (for debug).

**Checklist**:
- □ When an authz check errors, does it default-deny or default-allow?
- □ Does the try/catch contain a dangerous "treat error as pass" fallback?
- □ Are my defaults the safest, or the most convenient?
- □ Could error messages leak internal system info to an attacker?

**Code smell**: `try { checkAuth() } catch { /* let through */ }` → fail open. An auth error blows the door wide open instead.

🔗 **Pairs with**: #leastprivilege (default deny), #authnz (fail closed), #communicationdesign (safe error messages)
