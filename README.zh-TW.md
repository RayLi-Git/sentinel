<!-- LANG SWITCH -->

[English](./README.md) | **繁體中文**

# Sentinel — Vibe Coding 的思考作業系統

> 一個 Claude Code skill，扮演資深工程師的「思考層」——在你貼補丁、在淺層打轉、賭資安僥倖之前先喊停。讓AI在正式 coding**之前**就開始思考。配對 [Compass](https://github.com/RayLi-Git/compass) 形成完整工具組：Sentinel 看「怎麼想」，Compass 看「怎麼照規格執行」。

![status](https://img.shields.io/badge/status-active-success)
![license](https://img.shields.io/badge/license-MIT-blue)
![habits](https://img.shields.io/badge/思考習慣-87-purple)

---

## 它解決的問題

「Vibe coding」——用 AI 在快速對話中迭代寫程式——很強大，但有三個隱性問題：

1. **淺層打轉** — 在錯誤「出現」的地方修補，而非「產生」的地方。
2. **關掉警報** — 用 `try/except` 吞掉錯誤、用 `any` 繞過型別、加第三個特例 `if`。警告消失了，根因還在燒。
3. **資安僥倖** — 金鑰寫死、輸入不驗證、權限給太大，全在「先上線再說」下被放行。

Sentinel 是一套寫在程式底層的**思考作業系統**，專門對治這三點。

## 它做什麼

Sentinel 把 **87 個思考習慣**——76 個世界名校思考習慣,加上 11 個為本專案自創的資安習慣(批判／創意／溝通／互動／資安)——變成一套指令集,讓 Claude Code 在五階段中循環調用：

```
規劃 → 開發 → 診斷 → 解決 → 復盤
  ↑                          ↓
  └──────  病歷回饋下一輪  ────┘
```

核心機制：

- **三級強度** — 小修正直接做；中型任務跑快速預演；重型/架構/資安任務跑完整流程。**只能升級，不能默默跳過**。
- **動手前協定** — 動既有 code 前，先預測影響範圍、連鎖反應、設計安全路徑，並做 pre-mortem 風險預想。
- **淺層 vs 深層感測器** — 紅旗（「同段 code 改第 3 次」「加第 3 個特例 if」）強制停下追根因。
- **會自我成長的病歷** — 真正夠痛的除錯經驗寫進 `.claude/debug-log.md`，濃縮成 `patterns.md`，讓同一個坑不踩第二次。
- **三條安全網** — 撤退路線、證據強度分級（已驗證／已檢視／推測）、長對話防漂移回錨。

## 🧭 配對 skill：Compass

Sentinel 有個配對作品 [Compass](https://github.com/RayLi-Git/compass)——Sentinel 看「怎麼想」，Compass 看「怎麼照規格執行」。

| 維度 | Sentinel | Compass |
|---|---|---|
| 看什麼 | 你的思考 | 你跟 PRD 的關係 |
| 觸發問題 | 「我有想清楚嗎？」 | 「我有照 PRD 走嗎？」 |
| 適用 | 任何工程任務 | 有 spec 的實作工作 |

兩個常一起用：拿到 PRD 先用 Sentinel 想清楚，再用 Compass 照規格執行。

## 快速開始

```bash
# 安裝為使用者層級 skill（所有專案生效）
mkdir -p ~/.claude/skills/sentinel
unzip sentinel.skill -d ~/.claude/skills/sentinel

# 驗證結構
ls ~/.claude/skills/sentinel   # → SKILL.md  references
```

可選擇搭配常駐身分檔：

```bash
cp CLAUDE.md.example ~/.claude/CLAUDE.md
```

完整教學見 [docs/INSTALL.zh-TW.md](./docs/INSTALL.zh-TW.md)。

## 架構

```
sentinel/
├── SKILL.md                    # 本體（常駐，維持精簡）
└── references/                 # 按需載入
    ├── 00_index.md             # 87 習慣索引 + 症狀/階段對照
    ├── preflight.md            # 動手前協定（向內問 + 向外推）
    ├── safety_nets.md          # 撤退路線/證據強度/回錨
    ├── self_check.md           # 淺層+資安紅旗 + 診斷步驟
    ├── debug_log_template.md   # 病歷格式 + 夠痛門檻
    ├── html_style_guide.md     # 根因樹 HTML 規範
    └── 01–05_*/                # 87 個習慣，分五大類
```

## 設計理念

最難的不是「列出思考習慣」，而是讓它們**在對的時機被觸發**，又不撐爆 context window。完整的設計決策與取捨記錄在 **[docs/DESIGN.zh-TW.md](./docs/DESIGN.zh-TW.md)**。

## 授權

[MIT](./LICENSE) © Ray_Li

> 本專案是一個作品集，探索「如何把結構化思考編碼成 AI 寫程式的夥伴」。
