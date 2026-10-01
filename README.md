# write-agents-md

把 Repo 的 `AGENTS.md` 做成可信、精簡、可維護的工作入口，而不是讓 Agent
掃過專案後，把所有猜測與常識一次寫成永久規則。

版本：1.0.0。網路資料查核日：2026-10-01。
這是根據多個一手來源重新編寫的 Skill，不是任何作者的官方產品或逐字改寫。

## 包含什麼

| 檔案 | 用途 |
| --- | --- |
| `SKILL.md` | 執行流程；包含 audit、create、refactor 與安全邊界。 |
| `references/templates.md` | 最小入口、條件式路由、證據表與前後對照。 |
| `references/compatibility.md` | AGENTS、CLAUDE、persona 與 Skill 的差異；工具載入注意事項。 |
| `references/source-notes.md` | 來源、日期、採用原則、反例與研究限制。 |
| `references/evaluation.md` | 靜態檢查、載入檢查、行為比較與驗收方式。 |
| `evals/evals.json` | 10 個手動／自建 harness 可用的驗收案例，並非已執行測試。 |
| `validation-report.md` | 此發行包的靜態檢查結果與未驗證事項。 |

核心流程只按需讀取 references，不要求每次全讀。

## 安裝

下載或 clone 後保留整個 `write-agents-md` 資料夾，不要只複製 `SKILL.md`，否則參考文件會遺失。
以下是 Repo 範圍安裝；不用全域設定、不需要安裝 Python 或 npm 套件。

在目標 Repo 根目錄執行：

```bash
git clone https://github.com/Suckashi/write-agents-md.git .agents/skills/write-agents-md
```

若只使用 Claude Code，將上述目的地改成 `.claude/skills/write-agents-md`。

### Codex、OpenCode、Kimi Code

將資料夾放到 Repo 根目錄：

```text
.agents/
└── skills/
    └── write-agents-md/
        ├── SKILL.md
        ├── references/
        └── evals/
```

上述三個工具的查核日官方文件均列出 `.agents/skills`。
不要假設更舊版本、不同 worktree、遠端 session 或管理員限制也採相同行為；
安裝後用工具的技能清單／載入資訊確認，必要時重新開啟 session。
來源：[Codex Skills](https://developers.openai.com/codex/skills)、
[OpenCode Skills](https://opencode.ai/docs/skills/)、
[Kimi Code Skills](https://moonshotai.github.io/kimi-code/en/customization/skills)。

### Claude Code

只使用 Claude Code 時，放到 `.claude/skills/write-agents-md/`。
若要多工具共用，先選擇一個真實來源，再依工具支援建立引用或同步機制；
不要各自手動維護兩份已分叉的內容。本套件不自動建立 symlink 或修改設定。
來源：[Claude Code Skills](https://code.claude.com/docs/en/skills)。

## 使用

`mode` 是寫給模型的模式要求，不是另外安裝的程式參數。
建議第一次先 audit，確認沒有把目前 Repo 的真實約束刪掉，再要求 refactor。

Codex：

```text
$write-agents-md
請以 audit 模式檢查這個 Repo 的 AGENTS.md。
只做唯讀審核，列出需要保留、移動、刪除與確認的內容，並附證據路徑。
```

Kimi Code：

```text
/skill:write-agents-md 請以 audit 模式檢查這個 Repo；不要修改檔案。
```

Claude Code：

```text
/write-agents-md 請以 audit 模式檢查這個 Repo；不要修改檔案。
```

OpenCode 或其他支援工具，可明確請 Agent 載入：

```text
請載入 write-agents-md Skill，以 audit 模式檢查目前 Repo 的 agent instructions。
```

上述呼叫方式依各工具官方 Skills 文件；若清單找不到技能，先處理發現／權限問題，
不要僅憑模型說「已使用」就認定有載入。

首次建立：

```text
使用 write-agents-md，以 create 模式建立缺少的 AGENTS.md。
先核實命令與規則；沿用現有文件結構。
沒有證據的政策列為待確認，不要寫進正式指引。
```

重構既有檔案：

```text
使用 write-agents-md，以 refactor 模式整理目前 AGENTS.md。
保留有效約束，詳細知識與流程改成有觸發條件的路由。
不要修改程式或工具設定，也不要自行 commit。
```

## 與既有工作流整合

不取代 `dev-workflow-tdd`、`grill-with-docs` 或 ADR 流程。
已有 `CONTEXT.md`、`docs/agents/`、`docs/adr/` 時沿用；入口只指引何時讀取。
適合在 Repo setup、文件大幅變更、Agent 重複犯同類錯誤後使用；
不必在每一次普通 coding 任務都啟動此 Skill。

## 已驗證與未驗證

已做發行包的靜態結構檢查；詳見 `validation-report.md`。
未在使用者的實際 Repo 或四種 Agent 上執行端到端測試；沒有宣稱任務成功率或 token 成本改善。
本 Skill 是指引，不是權限系統或 sandbox。真正的禁止事項仍需由工具權限與環境保護。

## License

[MIT](LICENSE)。研究來源保留各作者的權利；本專案並非來源作者或工具廠商的官方產品。
