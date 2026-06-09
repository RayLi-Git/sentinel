# 根因樹 / 思考卡片 HTML 視覺化規範

> Sentinel 的視覺化輸出規範。主產出是**根因樹**（每個夠痛案例一張），存到 `.claude/root-cause-trees/{日期}_{描述}.html`。
> 色票/字體/Material Icons 必須遵守；版型可自由發揮。

---

## 一、何時產出 HTML

| 產出 | 何時 | 存放 |
|---|---|---|
| **根因樹** | 每個寫進病歷的「夠痛案例」順手產一張 | `.claude/root-cause-trees/{日期}_{描述}.html` |
| 思考卡片(選配) | 使用者明確要求某習慣的視覺說明時 | `/mnt/user-data/outputs/` 或專案內 |
| 前後對比(選配) | 使用者想看 before/after 思路升級時 | 同上 |

**核心原則**：HTML 是壓縮複雜思考的工具，不是裝飾。文字能講清楚時不要硬塞。

---

## 二、字體系統（全站統一）

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/icon?family=Material+Icons+Outlined" rel="stylesheet">
```
- font-family：`'Noto Sans TC', sans-serif`
- 字色：`#1a1a1a`(標題)／`#444`(內文)／`#999`(次要)／`#888`(標籤)
- 背景：`#F7F6F3`（Notion 米色）；卡片白 `#fff` + 邊框 `#E0DCD6`
- 字重：900 主標／700-800 次標／500 加粗／400 內文

---

## 三、四大類色票（依習慣主分類選色）

### 批判思考 — 紫（診斷/分析根因，根因樹常用）
```
主色 #6B5CE7  淺底 #EEEBFF/#F5F3FF  邊框 #C4B8FF  漸層 linear-gradient(135deg,#6B5CE7,#9B8AFF)
```
### 創意思考 — 橘黃（解法/假說）
```
主色 #D4900A  淺底 #FFF3D6/#FFF8EC  邊框 #F0D68A  漸層 linear-gradient(135deg,#D4900A,#F0B040)
```
### 溝通思考 — 藍（介面/表達）
```
主色 #0D7FBF  淺底 #D6F0FF/#EBF8FF  邊框 #90CCF0  漸層 linear-gradient(135deg,#0D7FBF,#4BA3D4)
```
### 互動思考 — 綠（系統/因果，根因樹常用）
```
主色 #0A8A4A  淺底 #D6FFE8/#ECFDF5  邊框 #90D8B0  漸層 linear-gradient(135deg,#0A8A4A,#34D399)
```
### 資安思考 — 深青藍（防禦/信任邊界/守護）
```
主色 #1E3A8A  淺底 #DBEAFE/#EFF4FF  邊框 #93B4E8  漸層 linear-gradient(135deg,#1E3A8A,#3B5FC0)
```
### 通用輔助
```
警示紅 #C53030(淺底 #FEF2F2,邊框 #FCA5A5)  ← 症狀/被排除/繞過
成功綠 #16A34A(淺底 #DCFCE7,邊框 #86EFAC)  ← 命中根因/驗證通過
中性灰 #888/#BBB                          ← 已排除假說
```

---

## 四、根因樹版型（主產出，必看）

根因樹是把「症狀 → 假說群 → 排除 → 根因 → 解法 → 驗證」畫成一棵由上而下的樹。

### 結構骨架
```
┌─────────────────────────────────────┐
│ [徽章] Sentinel 根因樹 · {日期}        │
│ [大標 50px/900] {一句話症狀}           │
└─────────────────────────────────────┘
              │
        ┌─ 症狀層（紅）──┐
        │ 預期 X / 實際 Y │
        └────────┬───────┘
                 │ (#差距分析)
     ┌───────────┼───────────┐
  [假說A灰]   [假說B綠]    [假說C灰]
  ❌已排除    ✅命中根因    ❌已排除
  (理由)                  (理由)
                 │
        ┌─ 根因層（綠強調）─┐
        │ {真正根因}        │
        └────────┬─────────┘
                 │
        ┌─ 解法層（橘黃）─┐
        │ {針對根因修正}   │
        └────────┬────────┘
                 │
        ┌─ 驗證層（成功綠）┐
        │ {如何證明已修好} ✓│
        └─────────────────┘

[底部 insight-box] 💊 下次提早識破：{訊號→根因}
[底部 tag] 🧠 命中習慣：#X #Y
```

### 視覺規則
- 症狀層用**警示紅**系（問題）。
- 被排除的假說用**中性灰**(降透明度 + ❌ + 一句排除理由)。
- 命中的假說/根因用**綠色強調**(✅ + 飽和色 + 陰影)。
- 解法層用**橘黃**(創意/解法色)。
- 驗證層用**成功綠** + check_circle icon。
- 節點間用 `↓` 或 Material Icon `arrow_downward` 連接，旁邊可標「(#用了哪個習慣)」。

---

## 五、共用 CSS 骨架

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

## 六、Material Icons 對照

| 用途 | icon |
|---|---|
| 症狀/警示 | `warning` / `error_outline` |
| 假說/分支 | `account_tree` / `alt_route` |
| 根因/命中 | `gps_fixed` / `target` / `check_circle` |
| 解法 | `build` / `lightbulb` |
| 驗證 | `verified` / `task_alt` |
| 診斷 | `query_stats` / `biotech` |
| 系統/因果 | `schema` / `polyline` |

語法：`<span class="material-icons-outlined">icon_name</span>`

---

## 七、輸出檢查清單

- [ ] `<!DOCTYPE html>` + `lang="zh-TW"` + viewport meta
- [ ] 引入 Noto Sans TC + Material Icons Outlined
- [ ] background `#F7F6F3`，container max-width ≤1100px
- [ ] 症狀=紅、根因=綠、解法=橘黃、驗證=成功綠
- [ ] 被排除假說用灰階 + ❌ + 排除理由
- [ ] 節點間有箭頭連接，標注用了哪個習慣
- [ ] 底部有「💊 下次提早識破」insight-box
- [ ] 底部 tag 列出命中的思考習慣
- [ ] 檔名 `{YYYYMMDD}_{簡短英文描述}.html`
- [ ] 不使用 emoji 當主視覺（一律 Material Icons；emoji 僅用於文字標籤如 💊🧠）

---

## 八、什麼時候不該出 HTML

- 🟢 輕級任務、一眼解決的小問題 → 不產樹。
- 未達夠痛門檻的問題 → 不產樹。
- 純文字能講清楚的診斷 → 不硬塞。
- 使用者明確說「只要修好不要圖」→ 尊重。
