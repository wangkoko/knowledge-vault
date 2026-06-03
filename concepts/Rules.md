# 規則 (Rules) | OpenCode

## 概述 (Overview)
為 opencode 設定自訂指令。

您可以透過建立 `AGENTS.md` 檔案來為 opencode 提供自訂指令。這類似於 Cursor 的規則功能。該檔案包含的指令會被納入 LLM 的上下文中，以便針對您的特定專案自訂其行為。

## 初始化 (Initialization)
要建立新的 `AGENTS.md` 檔案，您可以在 opencode 中執行 `/init` 指令。

提示：
您應該將專案的 `AGENTS.md` 檔案提交到 Git。
該指令會掃描您的專案及其所有內容，了解專案的用途，並據此產生一個 `AGENTS.md` 檔案。

## 範例 (Example)
AGENTS.md
```
# SST v3 Monorepo Project
This is an SST v3 monorepo with TypeScript. The project uses bun workspaces for package management.
## Project Structure
- `packages/` - Contains all workspace packages (functions, core, web, etc.)
- `infra/` - Infrastructure definitions split by service (storage.ts, api.ts, web.ts)
- `sst.config.ts` - Main SST configuration with dynamic imports
## Code Standards
- Use TypeScript with strict mode enabled
- Shared code goes in `packages/core/` with proper exports configuration
- Functions go in `packages/functions/`
- Infrastructure should be split into logical files in `infra/`
## Monorepo Conventions
- Import shared modules using workspace names: `@my-app/core/example`
```

## 類型 (Types)
opencode 還支援從多個位置讀取 `AGENTS.md` 檔案。

### 專案級 (Project-level)
在專案根目錄放置一個 `AGENTS.md` 檔案，用於定義專案特定的規則。這些規則僅在您於該目錄或其子目錄中工作時生效。

### 全域級 (Global-level)
您還可以在 `~/.config/opencode/AGENTS.md` 檔案中設定全域規則。這些規則會套用於所有 opencode 工作階段。

### Claude Code 相容性 (Claude Code Compatibility)
對於從 Claude Code 遷移過來的使用者，OpenCode 支援 Claude Code 的檔案慣例作為備援方案：
- 專案規則：專案目錄中的 `CLAUDE.md`（在沒有 `AGENTS.md` 的情況下使用）
- 全域規則：`~/.claude/CLAUDE.md`（在沒有 `~/.config/opencode/AGENTS.md` 的情況下）
- 技能：`~/.claude/skills/`

## 優先順序 (Precedence)
1. 本機檔案 (`AGENTS.md`、`CLAUDE.md`)
2. 全域檔案 (`~/.config/opencode/AGENTS.md`)
3. Claude Code 檔案 (`~/.claude/CLAUDE.md`)

## 自訂指令 (Custom Instructions)
您可以在 `opencode.json` 或全域設定檔中指定自訂指令檔案。
範例 `opencode.json`:
```
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["CONTRIBUTING.md", "docs/guidelines.md"]
}
```

## 參照外部檔案 (Referencing External Files)
透過 `opencode.json` 的 `instructions` 欄位或在 `AGENTS.md` 中手動指定（使用 `@path/to/file` 模式並配合 Read 工具）來引用外部檔案。
