# OpenCode Rules | OpenCode

## 概述 (Overview)
為 opencode 設定自訂指令。您可以透過建立 `AGENTS.md` 檔案來為 opencode 提供自訂指令。

## 類型 (Types)
- **專案級 (Project-level)**: 位於專案根目錄。
- **全域級 (Global-level)**: 位於 `~/.config/opencode/AGENTS.md`。
- **Claude Code 相容性**: 支援 `CLAUDE.md`。

## 優先順序 (Precedence)
1. 本機檔案 (`AGENTS.md`、`CLAUDE.md`)
2. 全域檔案 (`~/.config/opencode/AGENTS.md`)
3. Claude Code 檔案 (`~/.claude/CLAUDE.md`)

## 自訂指令 (Custom Instructions)
透過 `opencode.json` 的 `instructions` 欄位或在 `AGENTS.md` 中使用 `@path/to/file` 模式來引用外部檔案。
