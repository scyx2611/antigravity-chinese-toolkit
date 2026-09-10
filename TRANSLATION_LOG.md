# Antigravity Chinese Toolkit 翻譯變更台帳

這份台帳是 Antigravity Chinese Toolkit 的可重用翻譯索引。它記錄「乾淨 Antigravity bundle 的來源 anchor」與「語言包實際輸出」之間的關係，讓 Antigravity 更新後可以先重用既有定位，再處理真正改版的來源。

## 維護規則

1. 補翻或調整前，先搜尋本台帳的來源 anchor、動態規則與版本範圍。
2. 若台帳已有相同來源，優先確認新 bundle 是否仍命中；不要重新從整個 `main.js` 掃描猜測。
3. 每次修改 `locales/`、`scripts/patcher.js` 或翻譯驗證器，都要在同一個變更中新增或更新台帳紀錄。
4. 來源 anchor 必須抄自乾淨來源；不要把已翻譯的輸出當成下一次的來源 key。
5. 動態文字必須記錄要保留的變數、任務名稱、命令、路徑或數字；固定文字則記錄 exact key 或完整 expression。
6. 尚未提交的紀錄標示為「未提交」；提交後補上 commit，實際部署與桌面畫面驗收則另外標記，不能混為建構成功。
7. 新版本若使 anchor 移動，保留舊紀錄，新增「舊 anchor → 新 anchor」的遷移紀錄；不要刪除歷史定位。

## 紀錄格式

新增紀錄至少包含：日期、Antigravity 版本、狀態、來源 anchor／expression、固定或動態性質、zh-TW 與 zh-CN 輸出、修改檔案、驗證命令、部署／畫面驗收狀態。

可直接複製以下範本：

```text
### YYYY-MM-DD | Antigravity X.Y.Z | 未提交／<commit>
- 範圍：
- 來源 anchor：
- 類型：固定／動態；需保留的變數：
- zh-TW：
- zh-CN：
- 修改檔案：
- 驗證：
- 部署與畫面驗收：未部署／已部署；NOT VERIFIED 項目：
```

## 可重用來源索引

以下是目前 2.12.2 bundle 中最容易被重新尋找的動態來源。細節規則仍以 `skills/antilocale-maintainer/SKILL.md` 與版本更新 runbook 為準。

| ID | 乾淨來源 anchor／模式 | 類型與保留內容 | zh-TW | zh-CN |
| --- | --- | --- | --- | --- |
| ACT-001 | `function tV({prefix:a,content:b,progressMessage:c,customTitle:e}){if(e)return`；`e=typeof b=="string"` | 活動標題 formatter；保留 `content`、命令、路徑與動態說明 | 由 `zhTwActivityTitle` 處理 | 由 `zhCnActivityTitle` 處理 |
| ACT-002 | `a.match(/^(Run|Download) (.+) finished$/)` | 動態完成狀態；保留 `${task}` 原文 | `執行／下載 ${task} 已完成` | `运行／下载 ${task} 已完成` |
| ACT-003 | activity map 中的 `Run Task`／`Running Task`／`Ran Task`／`Task` | 動態任務前綴；保留後面的任務名稱 | `執行任務`／`執行任務中`／`已執行任務`／`任務` | `运行任务`／`正在运行任务`／`已运行任务`／`任务` |
| ACT-004 | activity map 中的 `Canceled`／`Cancelled` | 動態取消前綴；保留後面的任務名稱、命令或路徑 | `已取消` | `已取消` |
| ACT-005 | `Searching web`、`Searched web`、`Searching (.+)`、`Searched (.+)` | 搜尋狀態；保留 `${target}` | `搜尋網路`、`已搜尋網路`、`搜尋中 ${target}`、`已搜尋 ${target}` | `搜索网络`、`已搜索网络`、`搜索中 ${target}`、`已搜索 ${target}` |
| RUN-001 | `replace(/(\\d+) tasks? running/g, ...)` 與 subagent 變體 | 數量與單複數動態；保留 `${count}` | `${count} 個任務執行中`／子代理變體 | `${count} 个任务运行中`／子代理變體 |
| CHAT-001 | `"Thinking"`、`"Thinking..."` | 短狀態與動畫狀態是兩個來源，不能只補其中一個 | `思考中`／`思考中...` | `思考中`／`思考中...` |
| CHAT-002 | `"Proceeded with"`、`"Auto-proceeded with"` | 自動繼續處理狀態 | `已繼續處理`／`已自動繼續處理` | `已继续处理`／`已自动继续处理` |
| MODEL-001 | `var zW=({option:a})=>{var b=xB();return` | 模型 badge 與 Tooltip 的 `tagTitle`／`tagDescription` 必須同步 | `快速`、`限時提供` | `快速`、`限时提供` |
| MODEL-002 | `var J1=({title:a,titleSuffix:b,count:c,badgeCount:e,actions:f,children:g` | 動態 `Skills Used` 標題；保留英文 runtime lookup key | `使用的技能` | `使用的技能` |
| SETTINGS-001 | `title:"General"` 與 `sectionTitle:"General"` | 設定分區查找值必須使用同一目標語言，否則開關整區消失 | 同值翻譯 | 同值翻譯 |
| QUOTA-001 | quota label／bucket renderer 與 `Weekly Limit Remaining`／`Five Hour Limit Remaining` | 後端 `displayName` 動態 lookup；保留英文查找 key | `每週剩餘額度`／`5 小時剩餘額度` | `每周剩余额度`／`5 小时剩余额度` |
| GIT-001 | `` `${t} ${t===1?"file":"files"} changed` `` | Git 變更檔案數量；保留 `${t}`，不可寫死截圖中的數字 | `` `${t} 個檔案已變更` `` | `` `${t} 个文件已更改` `` |
| ASK-001 | `z.createElement("span",null,e.length," question",e.length===1?"":"s")` 與 `prefix:a?"Asking":"Asked",content:\`${e.length} question...` | 提問數量與單複數動態；保留 `${e.length}` | `${e.length} 個問題`；`提問中`／`已提問` | `${e.length} 个问题`；`提问中`／`已提问` |
| AUTH-001 | `Mvb` 組件中的 `Further action is required to use ${a}` 與 `Please verify your account...` | 帳戶資格與進一步動作面板；保留 `${a}` 產品名稱 | `需要採取進一步動作才能使用 ${a}`、`請驗證你的帳戶...`、`驗證`、`重新登入` | `需要采取进一步操作才能使用 ${a}`、`请验证你的账户...`、`验证`、`重新登录` |
| GOAL-001 | `title:p.title||p.key`、`var J1=`、`zhTwActivityText` / `zhCnActivityText` | 側欄累積目標標題（單數 `Goal`／複數 `Goals`）；需以活動字典與 `J1` 雙重攔截 | `目標`；`N 個目標` | `目标`；`N 个目标` |
| SPLIT-001 | `z.createElement("span",null,"Split")` 與 `z.createElement(T,{name:"splitscreen_vertical_add"...` | 側欄對話分割選單項目；2.12.2 minifier 變數更新 | `分割視窗` | `分割窗口` |
| EXPORT-001 | `dialogTitle:"Export Artifact"` 與 `tooltip:k?"Saved!":"Export Artifact"` | 成品右上角操作選單匯出按鈕、對話方塊標題與儲存狀態 | `匯出成品`、`已儲存！` | `导出成品`、`已保存！` |
| ARTIFACT-001 | `function uA(a)` 與 `ba=(0,z.useMemo)(()=>e.length===0?"Proceed with implementation plan"...` | 成品名稱動態格式化（`Implementation Plan` 等）與審核按鈕提示／留言互動 | `實施計畫`、`變更導覽`、`任務`、`便簽`；`繼續執行實施計畫` | `实施计划`、`变更导览`、`任务`、`便签`；`继续执行实施计划` |

## 變更紀錄（2026-09-11）

### 2026-09-11 | Antigravity 2.12.2 | `6963dc9`

- 範圍：補齊側欄對話選單的 `Split`（分割視窗）、成品右上角 `⋮` 操作選單的 `Export Artifact`（匯出成品）與 `Saved!`（已儲存！），以及成品標題 `Implementation Plan`（實施計畫）動態本地化與審核流程介面。
- 來源 anchor：
  - 分割選單：`z.createElement(xR,null,z.createElement(T,{name:"splitscreen_vertical_add",size:16,className:"text-secondary-foreground shrink-0"}),z.createElement("span",null,"Split"))`。
  - 成品操作：`dialogTitle:"Export Artifact"`、`tooltip:k?"Saved!":"Export Artifact"`。
  - 成品名稱動態產生器：`function uA(a)`（產生 `displayName` 與 `sectionName`）。
  - 成品審核提示與按鈕：`ba=(0,z.useMemo)(()=>e.length===0?"Proceed with implementation plan":`Proceed with implementation plan and ${e.length} comment${e.length===1?"":"s"}`,[e.length])`、`z.createElement("span",{className:"flex items-center gap-1 whitespace-nowrap"},"Proceed"...`、`z.createElement("h2",{className:"text-sm font-medium"},"Submit comment"...`、`z.createElement("span",null,"Review ",e.length," comment"...`。
- 原因：
  - `Split`：舊版字典記錄 `y.createElement` 結構，2.12.2 程式碼重構為 `z.createElement`，導致舊 anchor 失效。
  - `Export Artifact`：原本完全未被字典收錄。
  - `Implementation Plan`：成品檔名由 `uA(a)` 進行 Title Case 格式化後動態輸出為 `displayName`；透過在 `uA(a)` 回傳前注入字典映射，可安全本地化畫面名稱，同時不影響底層 `sourceUri` 與檔案系統操作。
- 類型：固定文字與動態映射；保留底層 URI、時間戳記與留言數量。
- zh-TW：
  - `Split` → `分割視窗`。
  - `Export Artifact` → `匯出成品`；`Saved!` → `已儲存！`。
  - `Implementation Plan` → `實施計畫`、`Walkthrough` → `變更導覽`、`Task` → `任務`、`Scratchpad` → `便簽`。
  - `Proceed with implementation plan` → `繼續執行實施計畫`；`Proceed` → `繼續執行`；`Submit comment` → `提交留言`；`Review N comment(s)` → `檢視 N 則留言`。
- zh-CN：
  - `Split` → `分割窗口`。
  - `Export Artifact` → `导出成品`；`Saved!` → `已保存！`。
  - `Implementation Plan` → `实施计划`、`Walkthrough` → `变更导览`、`Task` → `任务`、`Scratchpad` → `便签`。
  - `Proceed with implementation plan` → `继续执行实施计划`；`Proceed` → `继续执行`；`Submit comment` → `提交评论`；`Review N comment(s)` → `查看 N 条评论`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：
  - `npm run check` 通過（zh-TW 3,137 unique exact_properties，zh-CN 3,283 unique exact_properties，全覆蓋無重複）。
  - `node scripts/patcher.js --lang zh-TW` 不部署建構通過（前端替換 2,901 詞條，語法校驗 100% 通過，打包 app.asar.patched 4.32 MB）。
  - `node scripts/patcher.js --lang zh-CN` 不部署建構通過（前端替換 3,000 詞條，語法校驗 100% 通過，打包 app.asar.patched 4.32 MB）。
- 部署與畫面驗收：尚未部署；桌面實際畫面仍為 `NOT VERIFIED`。

## 變更紀錄（2026-09-08）

### 2026-09-08 | Antigravity 2.12.2 | `8fb8399`

- 範圍：修復側欄／累積區段（Accumulated Sections）中複數 `Goals` 漏翻為「目標」，以及工作區複數 `Workspaces` 漏翻為「工作區」。
- 來源 anchor：
  - 後端動態區段：`ph={selector:function(a){return a?.accumulatedSections??[]}}`，`z.createElement(J1,{key:p.key,title:zhTwActivityTitle(p.title||p.key),count:r.length,...})`；後端在目標數量大於 1 或複數時回傳 `p.title = "Goals"`。
  - 容器組件：`var J1=({title:a,...})=>{a=a==="\u0053kills Used"?"使用的技能":a;`。
  - 工作區動態標題：`var v=g.length>1?"Workspaces":"Workspace";`。
- 原因：先前的修正僅處理了單數 `Goal`（`\u0047oal`），未包含複數 `Goals`（`\u0047oals`），導致多個目標時 `zhTwActivityTitle` 查表 fallback 原樣輸出英文 `"Goals"`，且 `J1` 亦未攔截；靜態字典亦缺少 `"Goals"` 與 `"Workspaces"`。
- 類型：動態與固定文字；保留目標數量與後端項目內容。
- zh-TW：
  - `Goals` → `目標`（單複數皆為「目標」；`N goals` → `N 個目標`）。
  - `Workspaces` → `工作區`。
- zh-CN：
  - `Goals` → `目标`（单复数皆为「目标」；`N goals` → `N 个目标`）。
  - `Workspaces` → `工作区`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：
  - `npm run check` 通過（zh-TW 3,124 unique exact_properties，zh-CN 3,270 unique exact_properties，全覆蓋無重複）。
  - `node scripts/patcher.js --lang zh-TW` 不部署建構通過（前端替換 2,894 詞條，語法校驗 100% 通過，打包 app.asar.patched 4.32 MB）。
  - `node scripts/patcher.js --lang zh-CN` 不部署建構通過（前端替換 2,993 詞條，語法校驗 100% 通過，打包 app.asar.patched 4.32 MB）。
  - VM 動態測試驗證：`zhTwActivityTitle("Goals")`、`zhCnActivityTitle("Goals")`、`zhTwRunningSummary("2 goals")`、`zhCnRunningSummary("2 goals")` 均通過。
- 部署與畫面驗收：尚未部署；桌面實際畫面仍為 `NOT VERIFIED`。

## 已提交紀錄（2026-09-07）

### 2026-09-07 | Antigravity 2.12.2 | `ae93055`

- 範圍：補齊帳戶資格限制與驗證錯誤面板（`Further action is required to use <app>`、說明文字、`Verify` 按鈕、`Sign in again` 按鈕、`Submit Appeal` 申訴按鈕、無驗證連結時的資格不符標題與說明）。
- 來源 anchor：
  - `a=e?b||\`Sorry, this account is ineligible to use \${a}\`:\`Further action is required to use \${a}\``：帳戶資格與進一步動作標題。
  - `"Please verify your account, then sign in again to continue. Learn more by visiting our"`：帳戶驗證說明文字。
  - `h=e?h:"Verify"`：驗證按鈕文字。
  - `"Sign in again"`：重新登入按鈕文字。
  - `"Submit Appeal"`：提交申訴按鈕與連結預設文字。
  - `z.createElement("div",{className:"text-lg font-medium mb-1"},"Sorry, this account is ineligible to use ",a)`：資格不符標題。
  - `"Learn more by visiting our"`：資格不符詳情連結前綴。
  - `"We apologize for the inconvenience. Please try again later."`：帳戶設定不便道歉說明。
- 類型：固定文字與模板；保留產品名稱 `${a}` 與 FAQ 連結。
- zh-TW：
  - `Further action is required to use ${a}` → `需要採取進一步動作才能使用 ${a}`
  - `Sorry, this account is ineligible to use ${a}` → `抱歉，此帳戶不符合使用 ${a} 的資格`
  - `Please verify your account, then sign in again to continue. Learn more by visiting our` → `請驗證你的帳戶，然後重新登入以繼續。如需瞭解詳情，請參閱我們的 `
  - `Verify` → `驗證`
  - `Sign in again` → `重新登入`
  - `Submit Appeal` → `提交申訴`
  - `Learn more by visiting our` → `如需瞭解詳情，請參閱我們的 `
  - `We apologize for the inconvenience. Please try again later.` → `造成不便，敬請見諒。請稍後再試。`
- zh-CN：
  - `Further action is required to use ${a}` → `需要采取进一步操作才能使用 ${a}`
  - `Sorry, this account is ineligible to use ${a}` → `抱歉，此账户不符合使用 ${a} 的资格`
  - `Please verify your account, then sign in again to continue. Learn more by visiting our` → `请验证你的账户，然后重新登录以继续。了解详情，请访问我们的 `
  - `Verify` → `验证`
  - `Sign in again` → `重新登录`
  - `Submit Appeal` → `提交申诉`
  - `Learn more by visiting our` → `了解详情，请访问我们的 `
  - `We apologize for the inconvenience. Please try again later.` → `造成不便，敬请谅解。请稍后再试。`
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check` 通過（zh-TW 3,122、zh-CN 3,268 個 unique exact_properties，包含專用斷言）；zh-TW（2,885 個替換）與 zh-CN（2,984 個替換）不部署建構均通過語法檢查並產出 `app.asar.patched`；產出 bundle 驗證確認未翻譯英文降為 0。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-07 | Antigravity 2.12.2 | `f960faf`

- 範圍：補齊提問工具卡片完成標題（`N question(s)`）、未展開／進行中標題（`Asking/Asked N question(s)`）、多選標籤（`Multi-select`）、上一個/下一個問題按鈕（`Previous/Next question`）、未提供回答（`No answer provided`）、自訂回答標籤（`write-in`）、提交/繼續按鈕（`Submit/Continue`）及略過快捷提示。
- 來源 anchor：
  - `z.createElement("span",null,e.length," question",e.length===1?"":"s")`：完成狀態卡片標題。
  - `prefix:a?"Asking":"Asked",content:\`${e.length} question${e.length===1?"":"s"}\``：提問卡片活動標題。
  - `"Multi-select"`：多選模式徽章標籤。
  - `"Previous question"`、`"Next question"`：題目切換按鈕 aria-label 與 tooltip。
  - `"No answer provided"`：完成檢視未回答狀態。
  - `a.writeInResponse&&f.push(\`${a.writeInResponse} (write-in)\`)`：自訂輸入回答備註。
  - `va?"Submit":"Continue"`、`va?\`Submit\${J?" (Enter)":""}\`:\`Continue\${J?" (Enter)":""}\``：提交與繼續按鈕。
  - `J?\`Skip (esc), Skip All (\${fj?"\\u2318esc":"Ctrl+esc"})\`:"Skip"`：略過與全部略過提示。
  - `function tV({prefix:a,content:b` 中的 `zhTwActivityText` / `zhCnActivityText`：支援 `^(\d+) questions?$` 正則與 `"Asking"` / `"Asked"` 前綴映射。
- 類型：固定文字與動態數量模板；保留題目數量 `${e.length}`、快捷鍵變數與自訂回答內容。
- zh-TW：
  - `N question(s)` → `N 個問題`
  - `Asking` / `Asked` → `提問中` / `已提問`
  - `Multi-select` → `多選`
  - `Previous question` / `Next question` → `上一個問題` / `下一個問題`
  - `No answer provided` → `未提供回答`
  - `(write-in)` → `（自訂回答）`
  - `Submit` / `Continue` → `提交` / `繼續`
  - `Skip (esc), Skip All` → `略過 (esc)，全部略過`
- zh-CN：
  - `N question(s)` → `N 个问题`
  - `Asking` / `Asked` → `提问中` / `已提问`
  - `Multi-select` → `多选`
  - `Previous question` / `Next question` → `上一个问题` / `下一个问题`
  - `No answer provided` → `未提供回答`
  - `(write-in)` → `（自定义回答）`
  - `Submit` / `Continue` → `提交` / `继续`
  - `Skip (esc), Skip All` → `略过 (esc)，全部略过`
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check` 通過（zh-TW 3,114、zh-CN 3,260 個 unique exact_properties，包含提問卡片專用斷言）；zh-TW（2,876 個替換）與 zh-CN（2,975 個替換）不部署建構均通過前端／Electron 語法檢查並產出 `app.asar.patched`；產出 bundle 驗證確認各項目標詞條替換數量符合預期。
- 部署與畫面驗收：已成功執行 `--apply --lang zh-TW` 部署並重新啟動客戶端；桌面畫面人工驗收進行中。

## 已提交紀錄（2026-09-06）

### 2026-09-06 | Antigravity 2.12.2 | `2b99392`

- 範圍：補齊登入進階 SSO 面板（分隔線 OR、管理員進階登入設定說明、WIF Config 標籤、SSO 網址說明、Sign in with SSO 按鈕）。
- 來源 anchor：
  - `z.createElement("span",{className:"text-xs text-muted-foreground font-medium uppercase select-none"},"OR")`：登入方式分隔字。使用完整 JSX 避免誤傷終端機 ANSI escape sequence。
  - `"Use this option if your administrator has provided you with advanced login configurations"`：進階設定說明。
  - `"WIF Config"`：WIF 設定標籤。
  - `"Enter the SSO URL provided by your IT admin to connect your work account"`：IT 管理員 SSO 網址說明。
  - `"Sign in with SSO \\u2192"`：SSO 登入按鈕。
- 類型：固定文字與特定上下文 JSX 節點。
- zh-TW：
  - `OR` → `或`
  - `Use this option if your administrator has provided you with advanced login configurations` → `如果管理員提供了進階登入設定，請使用此選項`
  - `WIF Config` → `WIF 設定`
  - `Enter the SSO URL provided by your IT admin to connect your work account` → `輸入 IT 管理員提供的 SSO 網址，以連線你的工作帳戶`
  - `Sign in with SSO \u2192` → `使用 SSO 登入 \u2192`
- zh-CN：
  - `OR` → `或`
  - `Use this option if your administrator has provided you with advanced login configurations` → `如果管理员提供了进阶登录设置，请使用此选项`
  - `WIF Config` → `WIF 设置`
  - `Enter the SSO URL provided by your IT admin to connect your work account` → `输入 IT 管理员提供的 SSO 网址，以连接你的工作账户`
  - `Sign in with SSO \u2192` → `使用 SSO 登录 \u2192`
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check` 通過（zh-TW 3,104、zh-CN 3,250 個 unique exact_properties，簡中覆蓋全部繁中詞條）；包含進階 SSO 面板斷言檢查。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | `0e22b62`

- 範圍：補齊登入流程狀態（等待驗證、成功繼續、繼續使用 Google、求助連結、複製登入連結、登入中）與引導精靈導覽按鈕（上一步、下一步、完成）。
- 來源 anchor：
  - `"Awaiting Authentication..."`：登入按鈕 title 與文字。
  - `"Having trouble? Let us know"`：登入與授權頁面底部反饋連結。
  - `"Continue with Google"`、`"Success, Continuing..."`、`"Copy sign-in link"`、`"Signing in..."`：登入卡片狀態與操作。
  - `Bvb` 引導元件按鈕：`className:\`w-64 px-3 py-2 rounded-lg \${e?"opacity-100 pointer-events-auto":"opacity-0 pointer-events-none"}\`},"Previous")` 與 `className:\`w-64 px-3 py-2 rounded-lg shadow-sm \${f?"opacity-100 pointer-events-auto":"opacity-0 pointer-events-none"}\`},c?"Finish":"Next")`。
- 類型：固定文字與條件 JSX 分支；保留按鈕樣式、屬性與條件判斷。
- zh-TW：
  - `Awaiting Authentication...` → `等待驗證中...`
  - `Having trouble? Let us know` → `遇到問題？請告訴我們`
  - `Continue with Google` → `繼續使用 Google`
  - `Success, Continuing...` → `成功，繼續中...`
  - `Copy sign-in link` → `複製登入連結`
  - `Signing in...` → `登入中...`
  - 引導按鈕：`Previous` → `上一步`、`Next` → `下一步`、`Finish` → `完成`
- zh-CN：
  - `Awaiting Authentication...` → `等待验证...`
  - `Having trouble? Let us know` → `遇到问题？请告诉我们`
  - `Continue with Google` → `继续使用 Google`
  - `Success, Continuing...` → `成功，继续中...`
  - `Copy sign-in link` → `复制登录链接`
  - `Signing in...` → `登录中...`
  - 引導按鈕：`Previous` → `上一步`、`Next` → `下一步`、`Finish` → `完成`
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check` 通過（zh-TW 3,099、zh-CN 3,245 個 unique exact_properties，簡中覆蓋全部繁中詞條）；包含登入狀態與引導按鈕斷言檢查。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | `d3d412f`

- 範圍：補齊活動狀態與自動繼續狀態，並修正取消任務狀態。
- 來源 anchor：
  - `"Thinking"`：與既有 `"Thinking..."` 分開處理。
  - `"Proceeded with"`、`"Auto-proceeded with"`：固定狀態文字。
  - activity formatter 的 `"Run Task":`：在 `tV` helper 注入後，以共同 anchor 加入 `Canceled`／`Cancelled` map，避免全域替換破壞錯誤處理或取消 token。
- 類型：前兩項為固定狀態；`Canceled`／`Cancelled` 為動態前綴，後面的任務名稱、命令與路徑原樣保留。
- zh-TW：`思考中`、`已繼續處理`、`已自動繼續處理`、`已取消`。
- zh-CN：`思考中`、`已继续处理`、`已自动继续处理`、`已取消`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`。
- 驗證：`npm run check`；`node scripts/patcher.js --lang zh-TW`；`node scripts/patcher.js --lang zh-CN`；兩種輸出均通過前端／Electron 語法檢查與 `app.asar.patched` 打包，產出 bundle 確認包含 `"Canceled":"已取消"` 與 `"Cancelled":"已取消"`。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

## 本輪未提交紀錄

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊截圖中 `executeBrowserJavascript` 卡片直接顯示的 `Timed <seconds> seconds` 標題。
- 原因：該 renderer 使用 `b.title` 直接傳給 `tV`；它不是 `dW`／systemMessage／累積活動的標題入口。
- 類型：動態；保留秒數，沿用活動標題 formatter。
- zh-TW：`Timed N seconds` → `已計時 N 秒`。
- zh-CN：`Timed N seconds` → `已计时 N 秒`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 部署與畫面驗收：尚未部署；桌面實際畫面為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊 Goal 相關的兩個動態顯示：聊天區的 1 active goal／多個進行中目標，以及工作區／工具區的 Goal 標題。
- 來源 anchor：function tV({prefix:a,content:b,progressMessage:c,customTitle:e}){if(e)return 活動 formatter；動態標題可能來自 customTitle、titlePrefix 或活動內容，不是單一固定 literal。
- 類型：動態；保留目標數字 count，以 ^(\\d+) active goals?$ 匹配單複數；Goal 由同一個 activity formatter map 處理。
- zh-TW：count 個進行中的目標、目標。
- zh-CN：count 个进行中的目标、目标。
- 修改檔案：locales/zh-TW.json、locales/zh-CN.json、scripts/validate_locales.js、本台帳。
- 驗證：npm run check、node scripts/patcher.js --preflight、node scripts/patcher.js --lang zh-TW、node scripts/patcher.js --lang zh-CN 均通過；兩種輸出均通過前端／Electron 語法檢查與 app.asar.patched 打包，並保留 Goal runtime key 的 Unicode escape。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 NOT VERIFIED。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：將入口收斂為三個 BAT：繁中、簡中與還原；移除互動主選單及多餘的 Build／Apply／AutoDeploy／Status／Preflight 包裝檔。
- 來源 anchor：語言入口固定轉交 `--auto --lang zh-TW`／`--auto --lang zh-CN`；還原入口固定轉交 `--restore`。
- 類型：固定啟動入口；語言代碼固定寫入檔名與轉交參數，不改寫動態任務、命令、路徑或數字。
- zh-TW：`AntiLocaleToolkit-zh_TW.bat`。
- zh-CN：`AntiLocaleToolkit-zh_CN.bat`。
- 共用功能：`AntiLocaleToolkit-Restore.bat`。
- 修改檔案：三個根目錄 `.bat` 入口、`README.md`、`scripts/patcher.js`、`skills/antilocale-maintainer/SKILL.md`、`skills/antilocale-maintainer/references/version-update-runbook.md`、本台帳。
- zh-CN 入口提示：Node.js／首次安裝／安裝失敗訊息輸出為簡體中文；批次檔保持 ASCII 指令並以 UTF-8 code page 輸出，避免 Windows code page 950 直接解析 UTF-8 中文時誤執行命令。
- 驗證：三個入口以 `--help` 做不部署 smoke test；固定參數與 zh-CN 簡中提示檢查通過；語言入口保留 Node／asar 前置檢查與自動安裝；`npm run check`、`git diff --check` 與 `node scripts/patcher.js --preflight` 通過。未執行任何套用或還原入口。
- 部署與畫面驗收：未部署；桌面實際畫面與三個入口的完整安裝流程仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：修正 `zh-CN` 入口執行時仍顯示繁體中文的共用 CLI 輸出。
- 來源 anchor：`scripts/patcher.js` 的 `console.log`／`console.warn`／`console.error`，涵蓋 preflight、備份、建構、套用、還原與錯誤流程。
- 類型：固定 CLI 訊息與動態路徑／版本／數字分離；zh-CN 只轉換工具自身提示，保留路徑、版本、命令與動態內容。
- zh-TW：維持既有繁中 CLI 輸出。
- zh-CN：`前置检查`、`项目依赖组件`、`安装目录`、`应用程序版本`、`文件权限`、`运行状态`、`应用` 等輸出改為簡中對應詞。
- 修改檔案：`scripts/patcher.js`、本台帳。
- 驗證：`node scripts/patcher.js --preflight --lang zh-CN` 輸出無目標繁中 CLI 標記；`npm run check` 通過。
- 部署與畫面驗收：未部署；CLI 輸出已驗證，桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊 "Timed <seconds> seconds" 在工具活動自訂標題與進度訊息路徑的動態翻譯。
- 來源 anchor："function tV({prefix:a,content:b,progressMessage:c,customTitle:e}){if(e)return"；自訂標題的 e 分支與 progressMessage:c 的 text-xs 顯示節點。
- 類型：動態；保留 <seconds> 數字，可接受整數或小數；穩定文字輸出為「已計時／已计时」與「秒」。
- zh-TW："Timed N seconds" → "已計時 N 秒"。
- zh-CN："Timed N seconds" → "已计时 N 秒"。
- 修改檔案：locales/zh-TW.json、locales/zh-CN.json、scripts/validate_locales.js、本台帳。
- 驗證：node scripts/patcher.js --preflight 通過；npm run check 通過（zh-TW 3,080、zh-CN 3,231 個 unique exact_properties，簡中覆蓋全部繁中詞條）；node scripts/patcher.js --lang zh-TW（2,815 個前端替換）與 --lang zh-CN（2,945 個前端替換）均通過前端／Electron 語法檢查並產出 app.asar.patched；輸出 bundle 的 Timed 15 seconds 與 Timed 2.5 seconds 動態測試均通過。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 NOT VERIFIED。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊可供其他使用者使用的前置檢查／自動部署流程，並補翻 Git 動態摘要 `17 files changed`。
- 來源 anchor：`` `${t} ${t===1?"file":"files"} changed` ``；來源來自乾淨 `web_bundle/main.js` 的 Git 變更檔案標題 renderer。
- 類型：動態；保留 `${t}` 數字與檔案數量語意，不把 `17` 寫死。
- zh-TW：`` `${t} 個檔案已變更` ``。
- zh-CN：`` `${t} 个文件已更改` ``。
- 自動化：`--preflight` 唯讀檢查 Node.js、`asar`、安裝目錄、版本、權限、來源 bundle、備份與程序；`--auto` 只有在缺少專案 `asar` 時自動安裝相依元件，通過後才套用，並保留版本不符警告與 `NOT VERIFIED` 邊界。
- 來源候選：加入每位使用者的安裝路徑偵測與 `resources\\web_bundle.backup`，仍保留 `--app-dir`／`--source-web-bundle` 覆寫。
- 修改檔案：`scripts/patcher.js`、`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、`AntiLocaleToolkit.bat`、`AntiLocaleToolkit-Auto.bat`、`README.md`、`skills/antilocale-maintainer/SKILL.md`、`skills/antilocale-maintainer/references/version-update-runbook.md`、本台帳。
- 驗證：`npm run check` 通過（zh-TW 3,078、zh-CN 3,229 個 unique exact_properties，簡中覆蓋全部繁中 key）；`node --check`、Skill 快速驗證與 `git diff --check` 通過；`--preflight` 及 `AntiLocaleToolkit.bat --preflight` 都找到本機 Antigravity 2.12.2、來源與兩份備份；zh-TW／zh-CN 不部署建構均通過前端／Electron 語法檢查與 `app.asar.patched` 打包，輸出分別命中「個檔案已變更／个文件已更改」。
- 部署與畫面驗收：未部署；動態 Git 標題與自動部署的實際桌面流程仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊個人額度錯誤、方案基準額度重設、5 小時額度動態說明與 Tooltip。
- 來源 anchor：`var SI=...`／`userErrorMessage:a?.userErrorMessage`；`g+=...baseline quota...`；`e||"See plans"`；`function Dxb...` 與 `refreshText:a.description||""`。
- 類型：動態；保留重設倒數、重設日期、分鐘／小時數字及模型群組內容，不寫死畫面中的倒數。
- zh-TW：`個人額度已達上限。請升級您的訂閱方案以提高使用上限。將於 <倒數> 後重設。`；`您的方案基準額度將於 <日期> 重設。`；5 小時額度提示使用「您已達到 5 小時額度上限」與「每週額度」。
- zh-CN：`个人配额已达上限。请升级您的订阅方案以提高使用上限。将在 <倒数> 后重置。`；`您的方案基准配额将在 <日期> 重置。`；5 小时配额提示使用「您已达到 5 小时配额上限」与「每周配额」。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check` 與 `git diff --check` 通過；`node scripts/patcher.js --preflight` 通過並偵測 Antigravity 2.12.2；zh-TW（2,819 個前端替換）與 zh-CN（2,949 個前端替換）不部署建構均通過前端／Electron 語法檢查並產出 `app.asar.patched`；額度錯誤、Tooltip、5 小時額度卡片與動態日期／方案文字樣本測試通過。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊聊天框上方的 `1 active goal` 動態摘要，以及未經 `tV` 工具卡片路徑的 `Timed <seconds> seconds` 活動標題。
- 來源 anchor：`var qGb=()=>...` 的 `return m.join(", ")`；`function eUb(a){...}` 的 `a.titlePrefix?`${a.titlePrefix} ${b}`:b`。
- 原因：`qGb` 會直接組合 accumulated section 的數量與標題，原有 `Goal`／`active goal` 規則不會經過 `tV`；`eUb` 在沒有 `titlePrefix` 時也會直接返回英文標題。
- 類型：動態；保留目標數字與秒數，不寫死單一畫面。
- zh-TW：`<count> active goal(s)` → `<count> 個進行中的目標`；活動標題交由 `zhTwActivityTitle` 處理。
- zh-CN：`<count> active goal(s)` → `<count> 个进行中的目标`；活動標題交由 `zhCnActivityTitle` 處理。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 部署與畫面驗收：使用者已套用前一版 bundle；本次摘要入口修正尚未重新部署，需重新建構／套用後驗證桌面畫面。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊一般工具活動卡片直接由 `dW` 組出的 `Timed <seconds> seconds` 標題。
- 原因：該卡片的 `renderInfo.title`／純文字 `titleParts` 會在一般工具 renderer 先由 `dW` 產生；它可能繞過前面已補的 systemMessage、累積項目與 `tV` 進度路徑。
- 類型：動態；保留秒數，沿用活動標題 formatter；混合標題的純文字片段也套用同一規則。
- zh-TW：`Timed N seconds` → `已計時 N 秒`。
- zh-CN：`Timed N seconds` → `已计时 N 秒`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 部署與畫面驗收：尚未部署；桌面實際畫面為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊 `Timed <seconds> seconds` 的 systemMessage 路徑，以及右側累積區段中的 `Goal` 標題。
- 來源 anchor：`b,a):a;if(c)switch(c)`（`Unb` 無 `titlePrefix` 分支）；`K=K.label||(L?`${M}: ${L}`:M);`（執行面板累積項目）；`title:p.title||p.key,count`（側欄累積區段）。
- 原因：`Unb` 將字串包進 React 元件後，`tV` 不會再處理；側欄 `J1` 直接使用後端區段標題，未經活動標題 formatter。
- 類型：動態；保留秒數、區段數量與後端提供的項目內容。
- zh-TW：`Timed N seconds` → `已計時 N 秒`；`Goal` → `目標`。
- zh-CN：`Timed N seconds` → `已计时 N 秒`；`Goal` → `目标`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 部署與畫面驗收：目前安裝版本已包含前一輪 `qGb`／`eUb` 修正；本輪 `Unb`／`uLb` 修正尚未重新部署，需重新套用後驗證畫面。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊錯誤卡片、重試 Tooltip 與瀏覽器錯誤狀態中的 `Retry`。
- 來源 anchor：乾淨 `web_bundle/main.js` 的 `"Retry"`；涵蓋 `primaryAction:v("Retry")`、`content:"Retry"` 與 Browser 錯誤按鈕。
- 類型：固定文字；不改動重試動作、錯誤訊息或動態錯誤內容。
- zh-TW：`重試`。
- zh-CN：`重试`。
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check`、`git diff --check` 與 `node scripts/patcher.js --preflight` 通過；zh-TW（2,821 個前端替換）與 zh-CN（2,951 個前端替換）不部署建構均通過前端／Electron 語法檢查並產出 `app.asar.patched`；乾淨來源命中 3 個 `Retry`，兩種輸出皆確認沒有剩餘的帶引號 `Retry`，並命中「重試／重试」按鈕與 Tooltip。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：補齊個人額度錯誤卡片中直接顯示的 Google AI Ultra 方案升級說明。
- 來源 anchor：`z.createElement("span",null,a?.userTier?.upgradeSubscriptionText)`；此節點直接渲染後端 `upgradeSubscriptionText`，不會經過既有方案頁的替換路徑。
- 類型：動態；只替換完整固定英文句，保留後端其他方案說明內容與 React 節點結構。
- zh-TW：`You can upgrade to a Google AI Ultra plan to receive higher rate limits.` → `您可以升級至 Google AI Ultra 方案，以取得更高的使用上限。`
- zh-CN：`You can upgrade to a Google AI Ultra plan to receive higher rate limits.` → `您可以升级至 Google AI Ultra 方案，以获得更高的使用上限。`
- 修改檔案：`locales/zh-TW.json`、`locales/zh-CN.json`、`scripts/validate_locales.js`、本台帳。
- 驗證：`npm run check` 與 `git diff --check` 通過；zh-TW（2,827 個前端替換）與 zh-CN（2,957 個前端替換）不部署建構均通過前端／Electron 語法檢查並產出 `app.asar.patched`；兩種輸出均確認原始直接渲染式已改為對應語言的動態 `.replace(...)`。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

### 2026-09-06 | Antigravity 2.12.2 | 未提交

- 範圍：統一專案顯示名稱為 `Antigravity Chinese Toolkit`。
- 來源 anchor：`project.json` 的 `name`、`scripts/patcher.js` 的 `PROJECT_NAME`，以及 README／BAT／維護文件中的顯示名稱。
- 類型：固定專案品牌文字；保留 Repository identifier `anti-locale-toolkit`、目錄名稱、套件名稱與既有 BAT 檔名。
- zh-TW／zh-CN：專案品牌均使用 `Antigravity Chinese Toolkit`。
- 修改檔案：`project.json`、`README.md`、`AGENTS.md`、三個 BAT 入口、`scripts/patcher.js`、`scripts/validate_locales.js`、維護 Skill／runbook、本台帳。
- 驗證：`npm run check`、`git diff --check` 通過；舊顯示名稱已無剩餘命中。
- 部署與畫面驗收：未部署；桌面實際畫面仍為 `NOT VERIFIED`。

## 已提交歷史索引

這些 commit 是台帳建立前的既有維護紀錄；新的變更不可只依賴 commit message，仍要依上方格式留下來源定位。

| 日期 | Commit | 範圍 |
| --- | --- | --- |
| 2026-09-06 | `ddf22bc` | Copy Command／Copied tooltip |
| 2026-09-05 | `dfeee45` | active goal 狀態 |
| 2026-09-05 | `83f0a8a` | Timed／動態活動完成狀態 |
| 2026-09-05 | `ccd5d99` | undo、copy 與確認視窗 |
| 2026-09-05 | `5749f90` | 動態活動與設定頁 |
| 2026-09-05 | `96ae6d9` | Antigravity 2.12.2 基線 |
| 2026-09-04 | `0660e2c` | Fast／Skills Used |
| 2026-09-04 | `8d8300f` | feedback confirmation |
| 2026-09-04 | `d8dc940` | 簡體中文 coverage |
| 2026-09-04 | `8ddc8e2` | Thinking 狀態 |
| 2026-09-04 | `c1f5658` | Working 狀態 |
| 2026-09-04 | `94bfcb7` | 動態資料夾與權限 |
