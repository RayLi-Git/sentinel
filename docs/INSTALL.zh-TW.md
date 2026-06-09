<!-- LANG SWITCH -->

[English](./INSTALL.md) | **繁體中文**

# 安裝指南 (Installation Guide)

> Sentinel 由兩個部分組成：**skill 本體**（按需載入的思考知識庫）與一份**可選的 `CLAUDE.md`**（常駐身分檔）。完整體驗建議兩個都裝。

---

## 前置需求

- 已安裝 [Claude Code](https://docs.claude.com)。
- Claude Code 的 **code execution（程式碼執行）** 已啟用（skill 運作需要）。

---

## 一、安裝 skill 本體

skill 的本質是「一個資料夾，裡面有 `SKILL.md`」。安裝就是把它放到 Claude Code 掃描的 skills 目錄。

### 方式 A：全域安裝（推薦，所有專案生效）

```bash
mkdir -p ~/.claude/skills/sentinel

# 若你拿到的是 .skill / .zip 打包檔
unzip sentinel.skill -d ~/.claude/skills/sentinel

# 或若你 clone 了這個 repo，直接複製內容
cp -r SKILL.md references ~/.claude/skills/sentinel/
```

### 方式 B：專案層級安裝（只對單一專案生效）

```bash
mkdir -p .claude/skills/sentinel
cp -r SKILL.md references .claude/skills/sentinel/
```

### 驗證結構（重要）

```bash
ls ~/.claude/skills/sentinel
# 必須看到：SKILL.md  references
```

> ⚠️ 常見錯誤：解壓後變成多包一層 `sentinel/sentinel/SKILL.md`。
> `SKILL.md` 必須**直接**在 `~/.claude/skills/sentinel/` 底下。若多了一層，把內層內容往上搬。

---

## 二、（可選）安裝常駐身分檔 CLAUDE.md

`CLAUDE.md` 讓 Sentinel 的「身分與啟動鐵律」永遠在線，確保它會被觸發。

```bash
mkdir -p ~/.claude
cp CLAUDE.md.example ~/.claude/CLAUDE.md
```

> 若你已經有自己的 `~/.claude/CLAUDE.md`，**不要直接覆蓋**——把 `CLAUDE.md.example` 的內容手動合併進去。
> 專案特有設定請寫在專案根目錄的 `./CLAUDE.md`（會與全域那份合併載入）。

---

## 三、開始使用

1. 開一個**新的** Claude Code session（重開才會掃描到新 skill）。
2. 丟一個工程任務（規劃、寫功能、修 bug），Sentinel 會自動依任務份量啟動對應強度。

### 自我成長病歷會長在哪？

Sentinel 在**你工作的專案目錄**裡自動生成病歷：

```
你的專案/
└── .claude/
    ├── debug-log.md         # 除錯流水帳
    ├── patterns.md          # 高頻坑精華（開工先讀）
    └── root-cause-trees/    # 根因樹 HTML
```

> 💡 建議把專案的 `.claude/`（或至少這幾個檔）加入 git，記憶才能跨 session、跨機器保存——這是「越用越聰明」的前提。

---

## 疑難排解

| 症狀 | 可能原因 | 解法 |
|---|---|---|
| skill 沒被觸發 | 沒開新 session | 重開 Claude Code |
| 找不到 references 檔 | 多包了一層資料夾 | 確認 `SKILL.md` 直接在 sentinel/ 底下 |
| 病歷沒生成 | 任務未達「夠痛門檻」 | 正常——只有夠痛的案例才記，避免灌水 |
| CLAUDE.md 沒生效 | 路徑錯 | 確認在 `~/.claude/CLAUDE.md` |

---

## 解除安裝

```bash
rm -rf ~/.claude/skills/sentinel
# 若有裝 CLAUDE.md 且想移除 Sentinel 相關段落，手動編輯 ~/.claude/CLAUDE.md
```
