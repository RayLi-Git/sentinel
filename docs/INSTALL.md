<!-- LANG SWITCH -->

**English** | [繁體中文](./INSTALL.zh-TW.md)

# Installation Guide

> Sentinel ships in two parts: the **skill itself** (an on-demand thinking knowledge base) and an **optional `CLAUDE.md`** (always-on identity file). For the full experience, install both.

---

## Prerequisites

- [Claude Code](https://docs.claude.com) installed.
- Claude Code **code execution** enabled (the skill needs it).

---

## 1. Install the skill itself

A skill is fundamentally "a folder containing `SKILL.md`." Installation just means placing that folder under the directory Claude Code scans for skills.

### Option A: Global install (recommended — applies to all projects)

```bash
mkdir -p ~/.claude/skills/sentinel

# If you have the .skill / .zip bundle
unzip sentinel.skill -d ~/.claude/skills/sentinel

# Or if you cloned this repo, copy the contents directly
cp -r SKILL.md references ~/.claude/skills/sentinel/
```

### Option B: Per-project install (single project only)

```bash
mkdir -p .claude/skills/sentinel
cp -r SKILL.md references .claude/skills/sentinel/
```

### Verify the structure (important)

```bash
ls ~/.claude/skills/sentinel
# You should see: SKILL.md  references
```

> ⚠️ Common mistake: after unzipping, you may end up with an extra nested layer like `sentinel/sentinel/SKILL.md`.
> `SKILL.md` must be **directly** under `~/.claude/skills/sentinel/`. If there's an extra layer, move the inner contents up.

---

## 2. (Optional) Install the always-on identity file `CLAUDE.md`

`CLAUDE.md` keeps Sentinel's "identity and startup rules" always live, ensuring it actually gets triggered.

```bash
mkdir -p ~/.claude
cp CLAUDE.md.example ~/.claude/CLAUDE.md
```

> If you already have your own `~/.claude/CLAUDE.md`, **don't overwrite it** — manually merge the content of `CLAUDE.md.example` into it.
> Project-specific settings go in `./CLAUDE.md` at your project root (it's loaded merged with the global one).

---

## 3. Start using it

1. Open a **new** Claude Code session (a restart is required to pick up the new skill).
2. Drop in an engineering task (planning, building a feature, fixing a bug). Sentinel will auto-activate at the intensity that matches the task's weight.

### Where does the self-improving case file live?

Sentinel auto-generates the case file inside **the project directory you're working in**:

```
your-project/
└── .claude/
    ├── debug-log.md         # debugging journal
    ├── patterns.md          # condensed high-frequency pitfalls (read first at work start)
    └── root-cause-trees/    # root-cause tree HTML files
```

> 💡 Consider committing the project's `.claude/` (or at least those files) to git, so the memory survives across sessions and machines — this is what makes "smarter with use" possible.

---

## Troubleshooting

| Symptom | Likely cause | Fix |
|---|---|---|
| Skill never triggers | Didn't start a new session | Restart Claude Code |
| `references` files not found | Extra nested folder | Make sure `SKILL.md` sits directly under `sentinel/` |
| No case file appears | Task didn't hit the "threshold of pain" | Normal — only painful enough cases get logged, to keep the file honest |
| `CLAUDE.md` has no effect | Wrong path | Confirm it's at `~/.claude/CLAUDE.md` |

---

## Uninstall

```bash
rm -rf ~/.claude/skills/sentinel
# If you installed CLAUDE.md and want to remove the Sentinel-related sections, edit ~/.claude/CLAUDE.md by hand.
```
