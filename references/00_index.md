# Sentinel 知識庫索引 — 87 思考習慣 × 工程語境

> Sentinel 觸發後的「第一站」。先讀本檔做定位，再進對應子分類 `.md` 拿完整 code 化內容。
> **雙索引**：習慣按四大類存一份（避免重複），本檔另附「階段→習慣對照表」供五階段流程直接查。

---

## 🔍 卡關症狀 → 該查哪裡（工程語境對照表）

| 你的卡關長這樣 | 大類 | 子分類檔 |
|---|---|---|
| 不知道在解什麼、需求/問題定義不清 | 批判 | 分析問題 |
| 技術選型困難、取捨標準不明、效益沒算對 | 批判 | 分析決策 |
| 有 log/數字但讀不出意義、效能數據判讀錯 | 批判 | 分析資料 |
| 邏輯站不站得住、推理有漏洞、條件覆蓋不全 | 批判 | 評估理由 |
| 一個假設/說法可不可信、有沒有被表象誤導 | 批判 | 評估主張 |
| 想不出新方案、要在限制(效能/相容)下創新 | 創意 | 問題解決 |
| 要從零建假說、把複雜系統視覺化/建模 | 創意 | 資料與探索 |
| 要設計 A/B 測試、驗因果、抽樣比較 | 創意 | 應用研究方法 |
| 命名/文件/PR 描述散亂、不符讀者 | 溝通 | 語言溝通 |
| 架構圖/儀表板/簡報/圖表做不好 | 溝通 | 非語言溝通 |
| 倫理灰色地帶(隱私/資料使用)、需要說真話 | 互動 | 解決道德問題 |
| 因果太複雜、有湧現、要畫系統/依賴圖 | 互動 | 複雜系統互動 |
| 要說服 team 採用方案、跨組協商 | 互動 | 談判和說服 |
| 團隊協作、code review 動力、權責、自我覺察 | 互動 | 與他人合作 |
| 處理外部輸入/拼SQL/組命令、怕被注入 | 資安 | 輸入與信任邊界 |
| 用到金鑰/密碼/token、權限設計、敏感資料 | 資安 | 機密與最小權限 |
| 登入/認證/授權、想攻擊者會打哪、上線前檢查 | 資安 | 認證與攻擊面 |
| 裝第三方套件、CI/CD、部署、供應鏈風險 | 資安 | 依賴與供應鏈 |

---

## 🔄 階段 → 習慣對照表（五階段流程直接查這個）

> 同一習慣可跨階段使用，這裡列「該階段最常調用的」；習慣只存在它的子分類檔一份。

| 階段 | 主力習慣 | 子分類來源 |
|---|---|---|
| 1️⃣ 規劃 Plan | #問對問題 #拆解問題 #差距分析 #制定策略 #限制條件 #目的 ／資安：#信任邊界 #攻擊面思考 #敏感資料 | 分析問題 / 與他人合作 / 問題解決 / 分析決策 / 資安 |
| 2️⃣ 開發 Build | #最佳化 #演算法 #限制條件 #類比 #設計思考 #受眾 #內容組織 ／資安：#不信任輸入 #注入防範 #機密管理 #認證授權 | 問題解決 / 語言溝通 / 資安 |
| 3️⃣ 診斷 Diagnose | #問對問題 #變數控制 #複雜因果關係 #多層次分析 #證據基礎 #建立假說 #相關性 | 分析問題 / 複雜系統互動 / 評估理由 / 資料與探索 / 分析資料 |
| 4️⃣ 解決 Solve | #偏誤檢驗 #偏誤緩解 #可驗證性 #最佳化 #限制條件 #決策樹 #效用理論 ／資安：#預設安全 #最小權限 | 分析決策 / 評估主張 / 問題解決 / 資安 |
| 5️⃣ 復盤 Retro | #自我覺察 #偏誤緩解 #可複製性 #多層次分析 #當責 | 與他人合作 / 分析決策 / 應用研究方法 / 複雜系統互動 |

---

## 📋 完整 87 習慣索引（按五大類）

> 來源說明：批判／創意／溝通／互動四大類共 **76 個，來自世界名校思考習慣框架**；資安思考 **11 個為自創擴充**，專為 vibe coding 資安需求設計。合計 87 個。

### 批判思考（29）

**分析問題** — `01_critical_thinking/analyze_problems.md`
- #1 **#拆解問題** (#breakitdown) — 把巨大模糊的任務切成可逐一處理的小塊
- #2 **#賽局理論** (#gametheory) — 分析多方(使用者/系統/相依服務)互動下的策略
- #3 **#差距分析** (#gapanalysis) — 鎖定「預期行為 vs 實際行為」的最小差距
- #4 **#問對問題** (#rightproblem) — 確認在解真問題，而非腦補或表象需求
- #5 **#變數控制** (#variables) — 一次只動一個變因，隔離出真正肇因

**分析決策** — `01_critical_thinking/analyze_decisions.md`
- #6 **#偏誤檢驗** (#biasidentification) — 揪出「我以為」的認知偏誤
- #7 **#偏誤緩解** (#biasmitigation) — 主動設計流程降低偏誤影響
- #8 **#決策樹** (#decisiontrees) — 把技術選型攤成可比較的分支
- #9 **#心理成因** (#psychologicalexplanation) — 理解使用者/自己行為背後動機
- #10 **#目的** (#purpose) — 先釘死「為什麼做這個」再動手
- #11 **#效用理論** (#utility) — 用成本/效益權衡方案價值

**分析資料** — `01_critical_thinking/analyze_data.md`
- #12 **#信賴區間** (#confidenceintervals) — 用區間而非單點看效能/指標
- #13 **#相關性** (#correlation) — 分辨「同時發生」與「因果」
- #14 **#敘述統計** (#descriptivestats) — 用統計摘要看懂一堆 log/metrics
- #15 **#機率分布** (#distributions) — 理解延遲/錯誤率的分布形狀(不只平均)
- #16 **#機率理論** (#probability) — 用機率估「多常會出事」
- #17 **#迴歸分析** (#regression) — 找出哪個變因驅動了結果
- #18 **#顯著性檢定** (#significance) — 判斷 A/B 差異是真的還是雜訊

**評估理由** — `01_critical_thinking/evaluate_reasoning.md`
- #19 **#證據基礎** (#evidencebased) — 用 log/repro 證據說話，不靠猜
- #20 **#演繹推理** (#deduction) — 從規則推出必然結果(覆蓋條件分支)
- #21 **#邏輯謬誤** (#fallacies) — 揪出推理/歸因裡的破綻
- #22 **#歸納推理** (#induction) — 從多個案例歸納出通則
- #23 **#來源品質** (#sourcequality) — 評估文件/StackOverflow/AI 答案的可靠度

**評估主張** — `01_critical_thinking/evaluate_claims.md`
- #24 **#情境脈絡** (#context) — 把錯誤放回它發生的完整脈絡看
- #25 **#批判** (#critique) — 對自己的解法做敵意審查
- #26 **#估計** (#estimation) — 動手前先估量級(複雜度/工時/資源)
- #27 **#詮釋視角** (#interpretivelens) — 換個角度重讀同一個現象
- #28 **#合理性評估** (#plausibility) — 快速判斷一個假說合不合理
- #29 **#可驗證性** (#testability) — 確認主張/修正能被驗證

### 創意思考（17）

**問題解決** — `02_creative_thinking/problem_solving.md`
- #30 **#科學學習法** (#scienceoflearning) — 用學習科學快速掌握新框架/語言
- #31 **#限制條件** (#constraints) — 在效能/相容/時程限制下找解
- #32 **#類比** (#analogies) — 借用已解問題的結構解新問題
- #33 **#演算法** (#algorithms) — 設計系統化、可重複的解題步驟
- #34 **#設計思考** (#designthinking) — 從使用者需求反推技術方案
- #35 **#捷思法** (#heuristics) — 用經驗法則快速縮小搜尋範圍
- #36 **#最佳化** (#optimization) — 在多目標間找最佳平衡點

**資料與探索** — `02_creative_thinking/data_and_exploration.md`
- #37 **#建立假說** (#hypothesisdevelopment) — 形成可測試的 bug 根因假說
- #38 **#資料視覺化** (#dataviz) — 把資料流/狀態變化畫出來看
- #39 **#模型建構** (#modeling) — 建立系統的心智/資料模型

**應用研究方法** — `02_creative_thinking/research_methods.md`
- #40 **#抽樣** (#sampling) — 設計有代表性的測試案例取樣
- #41 **#個案研究** (#casestudy) — 深挖單一極端案例找通則
- #42 **#比較組** (#comparisongroups) — 用對照組隔離變因(A/B、before/after)
- #43 **#介入性研究** (#interventionalstudy) — 設計「改一個東西看結果」的實驗
- #44 **#訪談式研究** (#interviewsurvey) — 設計使用者回饋收集
- #45 **#觀察性研究** (#observationalstudy) — 從真實使用數據觀察行為
- #46 **#可複製性** (#studyreplication) — 確保 bug/結果能穩定重現

### 溝通思考（10）

**語言溝通** — `03_communication_thinking/verbal_communication.md`
- #47 **#受眾** (#audience) — 為讀者(隊友/未來的你)而寫
- #48 **#內容組織** (#composition) — 有效組織 code/文件/PR 內容
- #49 **#語義內涵** (#connotation) — 命名要傳達正確的隱含意義
- #50 **#組織結構** (#organization) — 建立清晰的程式碼/文件結構
- #51 **#專業素養** (#professionalism) — commit/PR/溝通的專業度
- #52 **#論點陳述** (#thesis) — 一句話講清這個 PR/方案在做什麼

**非語言溝通** — `03_communication_thinking/nonverbal_communication.md`
- #53 **#溝通設計** (#communicationdesign) — 設計清楚的錯誤訊息/API 介面
- #54 **#表達** (#expression) — 用最清楚的形式表達意圖
- #55 **#媒介選擇** (#medium) — 選對溝通媒介(圖/表/文/code)
- #56 **#多媒體運用** (#multimedia) — 整合圖表+文字說明複雜系統

### 互動思考（20）

**解決道德問題** — `04_interaction_thinking/ethical_problems.md`
- #57 **#倫理考量** (#ethicalconsiderations) — 考慮技術決策的倫理影響(隱私/公平)
- #58 **#倫理勇氣** (#ethicalcourage) — 敢指出「這樣做不對」即使不方便
- #59 **#倫理判斷** (#ethicaljudgment) — 在灰色地帶做出合乎倫理的判斷

**複雜系統互動** — `04_interaction_thinking/complex_systems.md`
- #60 **#複雜因果關係** (#complexcausality) — 追溯跨層、非線性的 bug 因果鏈
- #61 **#湧現** (#emergentproperties) — 識別系統互動產生的湧現問題
- #62 **#多層次分析** (#levelsofanalysis) — 在 UI/邏輯/資料/基礎設施各層分析
- #63 **#網絡分析** (#networks) — 分析模組/服務間的依賴網絡
- #64 **#系統動力學** (#systemdynamics) — 理解系統隨時間的動態行為(回饋迴路)
- #65 **#系統描繪** (#systemmapping) — 畫出系統結構/資料流圖

**談判和說服** — `04_interaction_thinking/negotiation_persuasion.md`
- #66 **#談判協商** (#negotiate) — 在技術方案分歧時找共識
- #67 **#說服技巧** (#persuasion) — 用證據說服 team 採用方案
- #68 **#行為塑造** (#shapingbehavior) — 用工具/流程引導團隊行為

**與他人合作** — `04_interaction_thinking/collaboration.md`
- #69 **#一致性** (#conformity) — 理解群體一致性對技術決策的影響
- #70 **#個體差異** (#differences) — 尊重隊友的不同技能與視角
- #71 **#情商** (#emotionaliq) — 在 code review/衝突中保持情緒智商
- #72 **#領導原則** (#leadprinciples) — 帶領技術方向的原則
- #73 **#權力動態** (#powerdynamics) — 理解團隊中的權力關係
- #74 **#當責** (#responsibility) — 為自己的 code 與決策負責
- #75 **#自我覺察** (#selfawareness) — 覺察自己的盲點與慣性錯誤
- #76 **#制定策略** (#strategize) — 制定有效的技術/專案策略

### 資安思考（11）｜⚙️ 自創擴充（非世界名校來源，為 vibe coding 資安需求設計）

**輸入與信任邊界** — `05_security_thinking/input_trust_boundaries.md`
- #77 **#不信任輸入** (#untrustedinput) — 所有外部輸入預設有毒，先驗證再用
- #78 **#信任邊界** (#trustboundary) — 標清楚內部可信 vs 外部不可信，跨界就檢查
- #79 **#注入防範** (#injectionprevention) — 絕不讓資料被當程式碼執行(SQL/命令/XSS)

**機密與最小權限** — `05_security_thinking/secrets_least_privilege.md`
- #80 **#機密管理** (#secretsmanagement) — 金鑰/密碼絕不進 code/log/git/前端
- #81 **#最小權限** (#leastprivilege) — 每個元件只給剛好夠用的權限
- #82 **#敏感資料** (#sensitivedata) — 個資/金流全程最小化與加密

**認證與攻擊面** — `05_security_thinking/auth_attack_surface.md`
- #83 **#認證授權** (#authnz) — 分清「你是誰」與「你能做什麼」，每入口檢查
- #84 **#攻擊面思考** (#attacksurface) — 列出暴露點，站攻擊者角度想會打哪
- #85 **#預設安全** (#securebydefault) — 出錯時 fail closed，預設值選最安全

**依賴與供應鏈** — `05_security_thinking/dependencies_supply_chain.md`
- #86 **#依賴稽核** (#dependencyaudit) — 第三方套件是最大攻擊面，來源/版本/漏洞要查
- #87 **#供應鏈思考** (#supplychain) — 你的安全=最弱的依賴，整條鏈都是攻擊路徑

---

## ⚠️ 載入策略提醒（給 Sentinel 自己）

- 一次卡關通常只需 3-5 個習慣，**不要全部讀完**。
- 用「卡關症狀對照表」或「階段對照表」鎖定 1-2 個子分類，只開那幾個 `.md`。
- `#問對問題` 是預設必含的起點習慣（除非任務完全不在分析範疇）。
- 症狀不明確時，先反問補資料（給 4+ 選項），不要硬猜。
