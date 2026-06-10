<!-- LANG SWITCH -->

**English** | [繁體中文](./README.zh-TW.md)

# Sentinel — A Thinking OS for Vibe Coding

> A Claude Code skill that acts as a senior engineer's thinking layer — stopping you from patching symptoms, looping at the surface, and shipping security gambles. It thinks *before* the code is written.

![status](https://img.shields.io/badge/status-active-success)
![license](https://img.shields.io/badge/license-MIT-blue)
![habits](https://img.shields.io/badge/thinking_habits-87-purple)

---

## The Problem

"Vibe coding" — building software in fast, conversational loops with an AI — is powerful but has three chronic failure modes:

1. **Surface looping** — patching the symptom where the error *appears*, not where it *originates*.
2. **Alarm-silencing** — `try/except` to swallow errors, `any` to bypass types, a third special-case `if`. The warning goes away; the root cause keeps burning.
3. **Security gambles** — hardcoded keys, unvalidated input, over-broad permissions, all waved through under "ship it first."

Sentinel is a **thinking operating system** that sits underneath the coding process to counter exactly these.

## What It Does

Sentinel turns **87 thinking habits** — 76 world-class thinking habits plus 11 security habits designed for this project (critical / creative / communication / interaction / security) — into an instruction set Claude Code consults across a five-stage loop:

```
Plan → Build → Diagnose → Solve → Retro
  ↑                                  ↓
  └──────  case history feeds back  ─┘
```

Key mechanisms:

- **Three-tier intensity** — trivial edits run free; medium tasks get a quick pre-flight; heavy/architecture/security tasks run the full loop. *Can escalate, never silently skip.*
- **Pre-flight protocol** — before touching existing code, predict blast radius, chain reactions, design a safe path, and run a pre-mortem.
- **Shallow-vs-deep sensor** — red flags ("editing the same code a 3rd time", "adding a 3rd special-case `if`") force a stop and a root-cause hunt.
- **Self-growing case history** — genuinely painful debugging episodes are written to `.claude/debug-log.md`, distilled into `patterns.md`, so the same pit isn't fallen into twice.
- **Three safety nets** — rollback routes, verification-honesty grading (verified / reviewed / assumed), and anti-drift anchoring for long sessions.

## 🧭 Companion skill: Compass

Sentinel has a companion piece, [Compass](https://github.com/RayLi-Git/compass) — Sentinel watches *how you think*, Compass watches *how you execute to spec*.

| Dimension | Sentinel | Compass |
|---|---|---|
| Watches | your thinking | your relationship to the PRD |
| Trigger question | "Have I thought this through?" | "Am I following the PRD?" |
| Applies to | any engineering task | implementation work with a spec |

The two are often used together: think it through with Sentinel first, then execute to spec with Compass.

## Quick Start

```bash
# Install as a user-level skill (applies to all projects)
mkdir -p ~/.claude/skills/sentinel
unzip sentinel.skill -d ~/.claude/skills/sentinel

# Verify structure
ls ~/.claude/skills/sentinel   # → SKILL.md  references
```

Optionally pair it with the always-on identity file:

```bash
cp CLAUDE.md.example ~/.claude/CLAUDE.md
```

See [docs/INSTALL.md](./docs/INSTALL.md) for the full guide.

## Architecture

```
sentinel/
├── SKILL.md                    # Core (always-resident, kept lean)
└── references/                 # Loaded on demand
    ├── 00_index.md             # 87-habit index + symptom & stage lookup
    ├── preflight.md            # Pre-flight protocol (inward + outward)
    ├── safety_nets.md          # Rollback / verification honesty / anchoring
    ├── self_check.md           # Shallow & security red flags + diagnosis steps
    ├── debug_log_template.md   # Case-history format + "painful enough" gate
    ├── html_style_guide.md     # Root-cause-tree HTML spec
    └── 01–05_*/                # The 87 habits, by category
```

## Design Philosophy

The hardest part wasn't listing thinking habits — it was making them **fire at the right moment** without bloating the context window. Read the full set of design decisions and trade-offs in **[docs/DESIGN.md](./docs/DESIGN.md)**.

## License

[MIT](./LICENSE) © Ray_Li

> Built as a portfolio piece exploring how structured thinking can be encoded as an AI coding companion.
