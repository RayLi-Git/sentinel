# Root-Cause Tree / Thinking Card HTML Visualization Spec

> Sentinel's visualization output spec. Main deliverable is the **root-cause tree** (one per painful-enough case), saved to `.claude/root-cause-trees/{date}_{description}.html`.
> Palette/font/Material Icons are mandatory; layout is free.

---

## 1. When to produce HTML

| Output | When | Location |
|---|---|---|
| **Root-cause tree** | Produce one alongside every "painful-enough case" written to the case file | `.claude/root-cause-trees/{date}_{description}.html` |
| Thinking card (optional) | When the user explicitly asks for a visual explanation of a specific habit | `/mnt/user-data/outputs/` or inside the project |
| Before/after (optional) | When the user wants to see a before/after thinking upgrade | Same as above |

**Core principle**: HTML is a tool for compressing complex thinking, not decoration. If plain text says it clearly, don't force it.

---

## 2. Font system (site-wide)

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Icons+Outlined" rel="stylesheet">
```
- font-family: `'Noto Sans TC', sans-serif`
- Text color: `#1a1a1a` (headings) / `#444` (body) / `#999` (secondary) / `#888` (labels)
- Background: `#F7F6F3` (Notion beige); card white `#fff` + border `#E0DCD6`
- Weights: 900 main heading / 700-800 subheading / 500 bold / 400 body

---

## 3. Four-category palette (pick by habit's main category)

### Critical thinking — Purple (diagnosis/root-cause analysis, common in root-cause trees)
```
Main #6B5CE7  Light #EEEBFF/#F5F3FF  Border #C4B8FF  Gradient linear-gradient(135deg,#6B5CE7,#9B8AFF)
```
### Creative thinking — Orange-yellow (solutions/hypotheses)
```
Main #D4900A  Light #FFF3D6/#FFF8EC  Border #F0D68A  Gradient linear-gradient(135deg,#D4900A,#F0B040)
```
### Communication thinking — Blue (interface/expression)
```
Main #0D7FBF  Light #D6F0FF/#EBF8FF  Border #90CCF0  Gradient linear-gradient(135deg,#0D7FBF,#4BA3D4)
```
### Interaction thinking — Green (systems/causality, common in root-cause trees)
```
Main #0A8A4A  Light #D6FFE8/#ECFDF5  Border #90D8B0  Gradient linear-gradient(135deg,#0A8A4A,#34D399)
```
### Security thinking — Deep teal-blue (defense/trust boundary/guarding)
```
Main #1E3A8A  Light #DBEAFE/#EFF4FF  Border #93B4E8  Gradient linear-gradient(135deg,#1E3A8A,#3B5FC0)
```
### Generic auxiliary
```
Alert red #C53030 (light #FEF2F2, border #FCA5A5)  ← symptom / ruled out / bypass
Success green #16A34A (light #DCFCE7, border #86EFAC)  ← root cause hit / verified
Neutral gray #888/#BBB                              ← ruled-out hypothesis
```

---

## 4. Root-cause tree layout (main deliverable, must read)

A root-cause tree draws "symptom → hypothesis group → elimination → root cause → solution → verification" as a top-down tree.

### Skeleton structure
```
┌─────────────────────────────────────┐
│ [badge] Sentinel root-cause tree · {date} │
│ [title 50px/900] {one-line symptom}        │
└─────────────────────────────────────┘
              │
        ┌─ Symptom layer (red) ──┐
        │ Expected X / Actual Y  │
        └────────┬───────────────┘
                 │ (#gap analysis)
     ┌───────────┼───────────┐
  [Hyp A gray] [Hyp B green] [Hyp C gray]
  ❌ ruled out  ✅ root cause hit  ❌ ruled out
  (reason)                  (reason)
                 │
        ┌─ Root-cause layer (green emphasis) ─┐
        │ {true root cause}                   │
        └────────┬────────────────────────────┘
                 │
        ┌─ Solution layer (orange-yellow) ─┐
        │ {fix targeting root cause}        │
        └────────┬─────────────────────────┘
                 │
        ┌─ Verification layer (success green) ┐
        │ {how to prove it's fixed} ✓         │
        └─────────────────────────────────────┘

[Bottom insight-box] 💊 Next-time early detection: {signal → root cause}
[Bottom tag] 🧠 Habits hit: #X #Y
```

### Visual rules
- Symptom layer uses **alert red** (the problem).
- Ruled-out hypotheses use **neutral gray** (reduced opacity + ❌ + one-line reason for elimination).
- Hit hypothesis / root cause uses **green emphasis** (✅ + saturated color + shadow).
- Solution layer uses **orange-yellow** (creative/solution color).
- Verification layer uses **success green** + check_circle icon.
- Connect nodes with `↓` or Material Icon `arrow_downward`; alongside, optionally label "(#which habit used)".

---

## 5. Shared CSS skeleton

```css
* { margin:0; padding:0; box-sizing:border-box; }
body { min-height:100vh; background:#F7F6F3; font-family:'Noto Sans TC',sans-serif; color:#1a1a1a; }
.container { max-width:1100px; margin:0 auto; padding:48px 32px 80px; }
.node {
  background:#fff; border-radius:14px; padding:22px 28px;
  border:1px solid #E0DCD6; border-left:4px solid var(--accent);
  box-shadow:0 2px 8px rgba(0,0,0,0.04); margin:0 auto; max-width:560px;
}
.insight-box {
  background:var(--light); border-left:4px solid var(--accent);
  border-radius:0 12px 12px 0; padding:22px 26px;
}
.tag { background:var(--light); color:var(--accent); border-radius:14px; padding:6px 14px; font:700 15px/1 'Noto Sans TC'; }
.arrow-down { text-align:center; color:#BBB; font-size:28px; margin:6px 0; }
```

---

## 6. Material Icons reference

| Use | icon |
|---|---|
| Symptom / alert | `warning` / `error_outline` |
| Hypothesis / branch | `account_tree` / `alt_route` |
| Root cause / hit | `gps_fixed` / `target` / `check_circle` |
| Solution | `build` / `lightbulb` |
| Verification | `verified` / `task_alt` |
| Diagnosis | `query_stats` / `biotech` |
| System / causality | `schema` / `polyline` |

Syntax: `<span class="material-icons-outlined">icon_name</span>`

---

## 7. Output checklist

- [ ] `<!DOCTYPE html>` + `lang="zh-TW"` + viewport meta
- [ ] Load Noto Sans TC + Material Icons Outlined
- [ ] background `#F7F6F3`, container max-width ≤1100px
- [ ] Symptom = red, root cause = green, solution = orange-yellow, verification = success green
- [ ] Ruled-out hypotheses use grayscale + ❌ + reason for elimination
- [ ] Nodes connected by arrows, labeled with which habit was used
- [ ] Bottom has "💊 Next-time early detection" insight-box
- [ ] Bottom tag lists the thinking habits hit
- [ ] Filename `{YYYYMMDD}_{short English description}.html`
- [ ] Don't use emoji as primary visual (always Material Icons; emoji only for text labels like 💊🧠)

---

## 8. When NOT to produce HTML

- 🟢 light tasks, small problems solved at a glance → no tree.
- Problems below the threshold of pain → no tree.
- Diagnoses that plain text can state clearly → don't force it.
- User explicitly says "just fix it, no diagram" → respect it.
