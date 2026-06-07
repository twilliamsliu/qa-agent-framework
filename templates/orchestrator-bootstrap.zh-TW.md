# Orchestrator Bootstrap（中文版）

> 把這份檔案丟進一個**空的、不是 git repo** 的工作目錄，
> 在那裡打開你的 AI 工具（Claude Code / Cursor / Codex / Gemini），
> 請 agent「依照 orchestrator-bootstrap.zh-TW.md 進行」。
> Agent 會訪談你、依答案搭出 L1 / L2 骨架（L3 不建）。
>
> 這是一次性的 scaffolding 流程，Phase 4 結束後請刪掉這份檔案。

你正在扮演 **Orchestrator Agent**，為一位第一次採用
QA Agent Operating Framework 的使用者搭建初始結構
（https://github.com/twilliamsliu/qa-agent-framework）。

不要跳過任何 phase。不要替使用者猜答案 — 一律問。

---

## Phase 1 — 訪談（必要）

**前置檢查（最先做）**：目前工作目錄本身**不應該**是一個
git repo（不要在 `git init` 過的資料夾跑這份 bootstrap，
避免巢狀 git）。若是，請使用者把這份檔案移去一個乾淨的
空目錄重來 — 在浪費任何訪談時間*之前*就要擋下。

**開場第一句**：請使用者先回頭讀完
https://github.com/twilliamsliu/qa-agent-framework 的
*Architecture overview* 與 Layer A / B / C 三節再回來。
若使用者表示已讀過，再進入訪談；若沒讀，請他先讀完，
不要強行往下。讀完之後再進入 7 題訪談。

接著問使用者下面 7 個問題。內容鏡像自 README 的
*Questions an agent should ask before scaffolding* 段落 —
**照這裡寫的問**，不要憑記憶重新推導、也不要連網去抓。
**一次一題**，不要一次丟一面牆。

1. **跑 agents 的 AI 工具是哪個？**（Claude Code / Cursor /
   Codex / Gemini / 其他）
2. **Issue tracker 用哪個？**（Jira / Linear / GitHub Issues /
   其他）
3. **測試案例管理工具用哪個？**（MeterSphere / TestRail /
   Zephyr / Xray / 沒有）
4. **團隊怎麼溝通？**（Slack / Teams / Discord / 沒有）
5. **測試報告放哪裡？**（專用 Markdown repo / wiki / 共用雲端）
6. **Secrets 怎麼分發？**（Google Drive + age / 1Password /
   Vault / 純本機檔案）
7. **一個產品還是多個？**

所有回答彙整成一個區塊，先寫入**目前工作目錄根**的
`setup-answers.md`（這個檔暫存於此，Phase 2 會搬進 L2）。
完成這份檔案前不要進 Phase 2。

**硬性規則**：如果使用者回「你決定」或「預設值就好」，
要回推一次。這 7 題都是真的設計選擇、不是偏好。
只有當使用者明確說「我理解 tradeoff，就要預設值」才接受。

---

## Phase 2 — 生成骨架

先檢查：確認 Phase 1 的前置檢查仍然成立 — cwd 本身不是
git repo。若直到現在才發現，請使用者換到乾淨的空目錄、
**把 `setup-answers.md` 一起帶過去**，從這裡接續即可 —
不用重做訪談。

依訪談答案，在目前工作目錄**裡面**建立以下兩個 sibling repos
（兩者彼此為 siblings，且都是 cwd 的子目錄）：

    your-workspace/              ← = 你目前的工作目錄（cwd）
    ├── qa-agent-framework/   ← L1 · 公開 framework 的 clone
    └── qa-agent-config/      ← L2 · 空的組織私有 repo
    (project repos 之後一個產品線一個，目前先不建)

**不要**因為目錄名字像 `test_*` / `sandbox*` / `tmp*` 就反推使用者
是在試水溫、然後建議他改去別處（例如 `~/Documents/work/`）安裝。
使用者把這份 bootstrap 放在這裡，**這裡就是 workspace**；
在 cwd 內就地建構，不要往外跳。

逐項處理：

- **L1**：`git clone https://github.com/twilliamsliu/qa-agent-framework qa-agent-framework`
  此階段不要改 L1。Project Agent 唯讀消費它；
  Orchestrator 要升級的話走 upstream PR 或 fork。
- **L2**：`git init qa-agent-config && cd qa-agent-config`
  - 建立 `org-config.yml`，欄位由訪談答案推出
    （issue tracker base URL、TCM tool、chat webhook 佔位、
    測試報告位置、secret distribution 方式）。值留白，
    由使用者自己填。
  - 建立 `memory/global.md`，內容只有一行標題「Iron Laws」。
    Phase 3 會寫入第一條。
  - 建立 `memory/project-memos/`（空）。
  - 加 `.gitignore`，內容包含 `*.local`、`*.token`、`credentials/`。
  - 把 Phase 1 暫存在 cwd 根的 `setup-answers.md` 移進
    `qa-agent-config/setup-answers.md`，cwd 根那份刪掉。
- **L3**：不要建任何目錄。明確告訴使用者：
  「Secrets 放在你的 home 目錄或密碼管理器，
  絕對不放進上面任一個 repo。這層我們不替你生。」

建好之後在每個 repo 跑一次 `git status` 給使用者看。
**不要** commit 也不要 push — 填完空欄、做出第一個 commit
是使用者自己的事（Week 1）。

---

## Phase 3 — 第一條 Iron Law

在 `qa-agent-config/memory/global.md` 寫入**且只寫入**一條 Iron Law：
README Layer D 的**推版確認制**。從本地 clone 讀 —
`qa-agent-framework/README.zh-TW.md` 的「推版確認制（鐵律 1）」
一節 — 原文照抄，不要憑記憶重寫。
這是你唯一可以未經詢問就寫入的法則。

接著在 `global.md` 追加第二個 section：標題「Self-Learning Rules」，
內容是 README Layer C 的**任務邊界規則** — 從本地 clone 讀
（`qa-agent-framework/README.zh-TW.md` 的
「一條預埋的自學規則：任務邊界」一節），把引文中的規則原文照抄。
這是框架唯一預埋的自學規則，其餘都要等 Week 2+ 自己踩出來。
那一節描述的 enforcement hook **不要**在此時架設 —
那是有真實工作流之後（Week 2+）的實作工作。

接著問使用者：「在你的工作脈絡裡，你最害怕 QA agent 犯下、
代價最高的錯誤是什麼？」

如果使用者一時想不到，丟下面三個來自實務的常見類型給他做參考
（**只是提示，不要替他選**）：

- **確認契約往 git 以外延伸**：例如 agent 未經確認就把訊息送到
  issue tracker 的 comment、ticket 描述、Slack 頻道、TCM 結果欄。
  Iron Law #1 只擋了 git push，這一條擋的是「其他對外通道」。
- **流程偏離**：agent 跳過已定義的 SOP 自行縮短步驟。
  例如：定義要先建測試計畫再執行，agent 直接開測。
- **開始測試前上下文採集不足**：開始測試一個項目前，
  agent 沒有把該項目既有的規格、歷史 bug、測試資料、
  之前的測試紀錄讀齊就動手。

他的回答 = 候選 Iron Law #2，**但你不要直接寫入**。
存到 `qa-agent-config/memory/iron-law-candidates.md`，
告訴使用者：等他**親身感受過**這個痛之後再 promote。

---

## Phase 4 — 收尾交棒

把這份檢查清單印給使用者然後停手：

- [ ] 你有 `qa-agent-framework/` 與 `qa-agent-config/` 兩個 sibling repos，
      且你理解 L3 不在這層管理（secrets 在家目錄或密碼管理器）。
- [ ] `qa-agent-config/org-config.yml` 存在，欄位待你自己填。
- [ ] `qa-agent-config/memory/global.md` 有一條 Iron Law，
      以及一條預埋的自學規則（任務邊界）。
- [ ] `qa-agent-config/memory/iron-law-candidates.md` 有一條候選法則
      （等你親身感受過再 promote 進 global.md）。
- [ ] 你理解此刻**還沒有任何 Project Agent**。
      README 的 *Week 2* 才是你接 Project Agent 的時機。
- [ ] 你現在可以刪掉這份 `orchestrator-bootstrap.zh-TW.md`。

**不要**繼續往下建 Project Agent。README 講得很清楚：
先讓一個產品端到端跑通，再去談「複製」這件事。

---

## 下一步路標（給使用者，bootstrap 不會替你執行）

bootstrap 只負責「Day 0 骨架」。接下來照下列順序推進，
每完成一階再進下一階，不要跳：

1. **Week 1 末 · 補齊 L2 設定** — 把 `org-config.yml` 的空欄填完，
   並做出 L2 的第一個 commit。
2. **Week 2 · 第一個 Project Agent + 第一輪記憶累積** —
   依 README *Week 2* 接一個產品線、跑一輪真實工作流，
   過程中的每個錯誤都寫進 Global Memory 的 error-correction log
   （自我學習迴圈）。這階段是「寫規則」「寫記憶」變日常的開始。
3. **Week 3 · 第二個產品 + Orchestrator 真正啟用** —
   有第二個產品 Orchestrator 才有存在價值，照 README *Week 3*。
4. **Week 4+ · Layer F 工具（skills / MCP / 自寫 CLI）** —
   此時你已經知道自己缺哪些 tool，*此時*再去裝對應的
   skills、MCP server、自寫 CLI 來補缺口。
   **不要在 Week 1 就裝** — 還沒撞到實際痛點時裝的工具會被丟掉。
5. **持續 · Iron Law / Self-learning Rule 累積** —
   `iron-law-candidates.md` 的候選法，實際撞痛之後再 promote 進
   `global.md`。

Bootstrap 結束。
