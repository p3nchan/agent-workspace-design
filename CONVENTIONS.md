# CONVENTIONS.md — 命名與結構規範

> Cleanup cron 和 agent 依此檔判斷合規性。修改需主 session 確認。

## 檔案命名

### memory/
- 主筆記：`YYYY-MM-DD.md`（一天一個，不帶 slug）
- Sub-agent notes：`YYYY-MM-DD-<kebab-case-slug>.md`（例：`2026-03-06-cron-review.md`）
- 時間戳 notes：`YYYY-MM-DD-HHMM.md`（例：`2026-03-06-0813.md`，cron 或快速記錄用）
- 根目錄 `.md` 上限：**15 個**（不含子目錄），超過歸檔最舊的
- `experiments.md`：實驗記錄（不歸檔，長期保留）

### memory/topics/
- 格式：`kebab-case.md`（不含日期前綴）
- 例：`penchan.md`, `tools.md`, `discord.md`, `practices.md`
- 大小目標：≤1KB / 硬上限：1.5KB（超過必須壓縮或拆分）
- 數量上限：**10 個**（超過建議合併相關主題）
- Daily cleanup **不碰**；weekly cleanup 可依記憶精煉 SOP 更新

### memory/archive/
- 子目錄格式：`YYYY-MM-early/` 或 `YYYY-MM-late/`（15 號為分界）
- 特例：`YYYY-MM/`（整月一包，用於早期/量少月份，如 `2026-01`）
- 主題性子目錄允許：`<kebab-case>/`（如 `agent-sociology`，需有明確歸檔原因）
- 內部檔案保留原始命名

### projects/
- 目錄名：`kebab-case`（例：`workspace-redesign`, `penchan-co`, `white-cat-planet`）
- 必備檔案：`context.md`（背景/策略）+ `status.md`（執行進度）
- 可選子目錄：`decisions/`, `research/`, `drafts/`, `workflows/`, `tools/`, `departments/`
- ADR 檔案：`decisions/NNNN-title.md`（流水號 + kebab-case）
- Sub-agent 產出寫入對應 `projects/<name>/` 子目錄，不放 memory/

### skills/
- 目錄名：`kebab-case`（例：`workflow-runner`, `discord-latex`, `canvas-design`）
- 必備檔案：`SKILL.md`（技能定義）
- 可選：`scripts/`, `references/`, `STYLE-GUIDE.md`

### workflows/
- 根目錄 `workflows/` 僅放**跨專案通用流程**
- 專案專屬流程放 `projects/<name>/workflows/`
- 檔名：`kebab-case.md`（例：`forum-automation.md`, `content-pipeline.md`）

### maintenance/
- 檔名：`kebab-case.md`（例：`daily-cleanup.md`, `weekly-cleanup.md`）
- 版本備份：`<name>-v1.bak`（保留前版供 rollback）
- 清理規則檔：`cleanup-rules.md`（可調參數，cleanup agent 啟動時載入）
- 清理建議檔：`cleanup-suggestions.md`（weekly cleanup 產出，下次執行時消化）

### logs/
- Session transcripts：`logs/sessions/`
- 系統日誌：`logs/<service>.log` 或 `logs/<service>.err.log`
- 帶日期的 log：`logs/<name>-YYYY-MM-DD.log`

## 根目錄系統檔

全大寫 + `.md`，僅主 session 可修改（sub-agent 禁寫）：
- `AGENTS.md`, `SOUL.md`, `USER.md`, `IDENTITY.md`
- `MEMORY.md`（純索引，<600 bytes）
- `CONVENTIONS.md`（本檔）, `ORCHESTRATION.md`, `TOOLS.md`
- `brain.md`（全局即時視圖，小寫是刻意的）

## 目錄結構白名單

```
~/.openclaw/
├── memory/           # 記憶系統
│   ├── topics/       # 穩定知識主題檔（≤10 個）
│   ├── archive/      # 歸檔舊筆記
│   └── state/        # 狀態快照
├── projects/         # 專案（每個含 context.md + status.md）
├── skills/           # 技能（每個含 SKILL.md）
├── workflows/        # 跨專案通用流程
├── maintenance/      # 清理/維護腳本與規則
├── logs/             # 日誌
│   └── sessions/     # Session transcripts
├── cron/             # 排程任務
├── media/            # 媒體檔案
│   └── inbound/      # 暫存（7 天自動清理）
├── browser/          # 瀏覽器環境
├── canvas/           # 設計畫布
├── config/           # 設定檔
├── credentials/      # 憑證（敏感）
├── tools/            # 工具腳本
└── ...系統檔.md      # 根目錄 markdown
```

## 通用規則

- **slug 格式**：一律 kebab-case（小寫 + 連字號），不用 snake_case 或 camelCase
- **目錄名複數**：`projects/`, `skills/`, `workflows/`, `logs/`（慣例）
- **Single Source of Truth**：每個知識只有一個權威檔案，其他地方放相對路徑連結
- **Sub-agent 寫入範圍**：`projects/` 和 `memory/YYYY-MM-DD*.md`，其他區域禁寫

## 版本
- v1.0 — 2026-03-07 — 初版，基於 workspace-redesign 合成結論
