# Security Thinking / Dependencies & Supply Chain (code context)

> Category color: deep teal-blue `#1E3A8A`. Third-party dependencies are the largest modern attack surface — your security equals your weakest dependency.

---

## #DependencyAudit (#dependencyaudit)
**Position**: Third-party packages are the largest attack surface — source, version, vulnerabilities, permissions all need vetting.

**When to use**: Before installing a new package, during regular maintenance, when `npm install`-ing a library you've never heard of. **vibe coding high-risk zone** (casually installing packages).

**How to use**:
1. Before installing: check maintenance activity, downloads, recent updates, known vulnerabilities (CVE).
2. Watch for malicious lookalike names (typosquatting, e.g. `lodahs`).
3. Lock versions (lockfile), don't blindly auto-upgrade to arbitrary new versions.
4. Run vulnerability scans regularly (npm audit / equivalent), address high-risk items.
5. Ask "is this feature worth pulling in a new dependency?" — if you can write it in a few lines yourself, don't install.

**Checklist**:
- □ Is this package actively maintained and trustworthy? Or did I just install on a whim?
- □ Could the package name be a fake (typosquatting)?
- □ Did I lock the version, or let it auto-upgrade?
- □ Did I run a vulnerability scan?
- □ Pulling a large dependency for a small feature — worth it?

**Code smell**: `npm install` an unvetted package and use it directly, or install a pile of packages on every error → pulling unknown code into your trust boundary.

🔗 **Pairs with**: #SourceQuality (verify source), #SupplyChain (weakest link), #UtilityTheory (worth pulling in)

---

## #SupplyChain (#supplychain)
**Position**: Your security = your weakest dependency. The whole chain (packages, CI, deployment, third-party services) is an attack path.

**When to use**: Designing deployment pipelines, evaluating overall security, using third-party services / CI.

**How to use**:
1. Treat the "whole supply chain" as attack surface: source → dependencies → build → CI/CD → deploy → runtime.
2. At each link ask "if this link is compromised, what happens?"
3. Minimize CI/CD secret permissions (it usually has full deploy rights).
4. Verify source integrity (checksum, signatures), don't download and execute unknown scripts.

**Checklist**:
- □ Does my CI/CD have excessive permissions / exposed secrets?
- □ Does the build process pull in unverified things?
- □ Where's the weakest link in the chain?
- □ Am I `curl | bash`-ing scripts from unknown sources?

**Code smell**: `curl http://... | bash` to execute remote scripts, CI using admin tokens → the most typical supply-chain breach.

🔗 **Pairs with**: #DependencyAudit (vet dependencies), #LeastPrivilege (CI permissions), #NetworkAnalysis (find weakest link), #AttackSurface (whole-chain exposure)
