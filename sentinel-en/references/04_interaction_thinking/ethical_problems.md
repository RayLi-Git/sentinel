# Interaction Thinking / Solving Ethical Problems (code context)

> Primary color: green `#0A8A4A`. The ethical side of technical decisions — invoke when handling privacy, data, security, or fairness.

---

## #ethicalconsiderations
**Position**: Consider the ethical impact of technical decisions — privacy, security, fairness, harm to users.

**When to use**: When handling user data, designing algorithms, collecting/storing information, or designing permissions.

**How**:
1. Ask "could this design harm users or some group".
2. Check data: collect only what's necessary, store securely, disclose clearly, allow deletion.
3. Check algorithms: do they amplify bias/discrimination.
4. Default to the most user-protective approach (privacy-first, least privilege).

**Checklist**:
- □ Is the data I collect necessary? Am I over-collecting?
- □ Is sensitive data (passwords / PII / payments) handled securely?
- □ Could this logic be unfair to a certain group of users?
- □ Is the default "protect the user" or "convenient for me"?

**Code smell**: Logs print full user PII / tokens → ethical and security double failure.

🔗 **Paired habits**: #ethicaljudgment (gray areas), #gametheory (malicious actors), #accountability (own the impact)

---

## #ethicalcourage
**Position**: Dare to say "this is wrong" even when inconvenient or it slows progress.

**When to use**: When you spot a security hole / privacy issue / are pressured to cut corners or "ship first, fix later".

**How**:
1. When you spot a problem, call it out clearly — don't go silent because it's "annoying / time-pressed".
2. Explain with facts and consequences, not moral accusation.
3. Propose viable alternatives, not just objection.
4. Say no to the dangerous "do it this way and fix later" shortcut.

**Checklist**:
- □ Am I pretending not to see a known problem just to save effort?
- □ When I point out a problem, do I also give an alternative?
- □ For this "fix later" shortcut, have I made the risk clear?

**Code smell**: Knowing there's an SQL injection risk but wanting to "ship it like this" → time to summon ethical courage and block it.

🔗 **Paired habits**: #ethicalconsiderations (see the problem), #persuasion (express it effectively), #accountability (own it)

---

## #ethicaljudgment
**Position**: In gray areas without a standard answer, make ethically sound tradeoff judgments.

**When to use**: When privacy vs feature, efficiency vs fairness, business vs user interest conflict.

**How**:
1. List each party's interests (users, company, society) and the friction points.
2. Ask "if this were reported publicly, would it stand up".
3. Look for a "balances multiple sides" design instead of binary choice.
4. When forced to choose, lean toward protecting the weaker party / the user.

**Checklist**:
- □ Have I clearly seen each party's points of conflict?
- □ Held up to sunlight, does this decision stand?
- □ Is there a third path that balances multiple sides?

**Code smell**: The thought "the user won't notice anyway" surfaces → red light for ethical judgment.

🔗 **Paired habits**: #ethicalconsiderations (impact surface), #decisiontree (lay out tradeoffs), #interpretiveperspectives (multiple angles)
