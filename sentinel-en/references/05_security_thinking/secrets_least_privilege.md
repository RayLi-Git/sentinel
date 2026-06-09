# Security Thinking / Secrets & Least Privilege (code context)

> Category color: deep teal-blue `#1E3A8A`. Protect secrets, constrain power — minimize damage when things go wrong.

---

## #SecretsManagement (#secretsmanagement)　⭐high-frequency red flag
**Position**: keys, tokens, passwords, connection strings — never put them in code, logs, git, frontend, or error messages.

**When to use**: anytime you touch an API key, database password, token, certificate, or encryption key. **The #1 vibe coding failure spot.**

**How**:
1. Always read secrets from env vars / a secrets-management service, never hardcode in code.
2. Confirm secrets won't be committed to git (use .gitignore, scan .env).
3. Logs and error messages must never print secrets (not even partially).
4. Don't send secrets to the frontend, don't put in URL params, don't store in localStorage.
5. Suspect a leak → rotate immediately, don't just delete.

**Checklist**:
- □ Is any key/password hardcoded in code?
- □ Is `.env` / files containing secrets in .gitignore?
- □ Will my logs print tokens / passwords / PII?
- □ Did secrets leak to frontend / URL / localStorage?
- □ (History) has a secret ever been committed in git history?

**Code smell**: `const apiKey = "sk-..."` hardcoded, or `console.log(user)` printing an object containing a token → secret leaked, and once it's in git it lives forever.

🔗 **Pair with**: #SensitiveData (data protection), #DontTrustInput (boundaries), #Accountability (honest leak handling)

---

## #LeastPrivilege (#leastprivilege)
**Position**: every component, user, and token gets "just enough" permission, no more.

**When to use**: designing permissions, issuing tokens, setting up database accounts, configuring cloud IAM, third-party authorization.

**How**:
1. Default to "grant nothing", then add only what's necessary.
2. Shrink token/account permission scope to the minimum (read-only if no write needed; single table if not whole DB).
3. Set expiry, don't issue permanent credentials.
4. Periodically review and revoke permissions no longer needed.

**Checklist**:
- □ Does this token/account have more permission than it actually needs?
- □ Did I grant admin/full access just for convenience?
- □ Do credentials have an expiry mechanism, or are they permanent?
- □ If it leaks, how much damage can this permission cause? (blast radius)

**Code smell**: granting service account admin permission for convenience, tokens set to never expire → once leaked, blast radius is maximized.

🔗 **Pair with**: #SecureByDefault (default closed), #AuthAuthz (authorization design), #AttackSurfaceThinking (shrink damage)

---

## #SensitiveData (#sensitivedata)
**Position**: PII, financial, health and other sensitive data — minimize and encrypt across collection, storage, transmission.

**When to use**: handling user PII, financial flows, passwords, any private data.

**How**:
1. Minimize collection: if you don't need it, don't collect it (ties to #EthicalConsideration).
2. Encrypt in transit (HTTPS/TLS), encrypt at rest.
3. Hash passwords one-way (bcrypt/argon2), never plaintext or reversible encryption.
4. Provide deletion mechanisms, comply with data protection regulations.

**Checklist**:
- □ Is all the sensitive data I collect actually necessary?
- □ Is it encrypted in transit and at rest?
- □ Are passwords hashed, or plaintext/reversible?
- □ Can users request deletion of their data?

**Code smell**: passwords stored as plaintext or MD5, sensitive data over HTTP → data protection breached.

🔗 **Pair with**: #SecretsManagement (protect secrets), #EthicalConsideration (privacy), #LeastPrivilege (access control)
