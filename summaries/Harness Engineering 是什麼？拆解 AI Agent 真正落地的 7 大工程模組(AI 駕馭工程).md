---
title: "Harness Engineering 是什麼？拆解 AI Agent 真正落地的 7 大工程模組(AI 駕馭工程)"
date: 2026-05-17
source: "https://www.blocktempo.com/harness-engineering-ai-agent-context-tools-permission-cache-claude-code-cursor-codex/"
tags: ["ai-agent", "harness-engineering", "mcp", "context-engineering"]
---

# Harness Engineering 是什麼？拆解 AI Agent 真正落地的 7 大工程模組

本文系統拆解 Harness Engineering（AI Agent 駕馭工程）的七大模組，探討如何圍繞 LLM 建立完整的系統架構，以實現 AI Agent 在生產環境中的安全與可靠執行。

## 核心概念：Agent = Model + Harness

**Harness Engineering (駕馭工程)** 指的是圍繞 LLM 設計的完整系統架架構，負責管理 Agent 從意圖捕捉、上下文編譯、工具執行，到結果驗證的全生命週期。

- **Prompt Engineering**: 最小的圓，研究如何寫出好的單次提示。
- **Context Engineering**: 中間的圓，研究如何在上下文視窗裡填入最有效的資訊。
- **Harness Engineering**: 最大的圓，涵蓋前兩者，再加上系統架構、工具整合、安全控制、記憶管理、多 Agent 協作等。

## 七大工程模組

### 1. Context 管理 (Context Management)
核心戰場：如何在有限的視窗內塞入最有用的資訊。
- **System Prompt 層**: 定義角色與規則。
- **專案設定層 (CLAUDE.md / AGENTS.md)**: 提供專案結構與規範。
- **工具清單層**: 採用 **Deferred Loading (延遲載入)** 策略，保護 Prompt Cache 命中率。
- **對話歷史層**: 使用 **Compaction (壓縮)** 機制，將舊對話摘要化以釋放空間。

### 2. Tool 設計與 MCP 標準
Tool 是 Agent 與外部世界互動的唯一介面。
- **MCP (Model Context Protocol)**: Anthropic 發布的開放標準，讓不同系統（資料庫、GitHub、Slack）能透過統一協議接入。
- **設計原則**: 
    - **LLM-friendly**: 清楚說明工具用途與輸出格式。
    - **數量上限意識**: 避免工具描述佔滿上下文。
    - **命名規範**: 使用具備功能描述性的名稱。

### 3. Permission 系統 (Permission System)
確保 Agent 在安全範圍內執行任務，「縱深防禦」設計原則。
- **Claude Code 的 7 種模式**: 從最保守的 `plan` (需人工確認) 到最開放的 `bypassPermissions`。
- **PreToolUse Hook**: 在工具執行前攔截，可執行 `allow`, `deny`, `ask`, 或 `defer`，並能修改工具輸入（例如將生產資料庫寫入重新定向到測試環境）。

### 4. Memory 與 Compaction
解決跨會話記憶與長對話視窗管理問題。
- **Compaction**: 處理長對話的視窗管理，透過多階段壓縮釋放空間。
- **Memory Tool**: 提供工具呼叫式的跨會話記憶管理，讓 Agent 能主動決定記憶與忘記的事項。

### 5. Hook 系統 (Hook System)
Harness 的神經系統，在 Agent 生命週期的關鍵時刻插入自定義邏輯。
- **功能**: 記錄日誌、通知、攔截危險操作、修改輸入輸出。
- **擴充層次**: `hooks` $\to$ `skills` $\to$ `plugins` $\to$ `MCP Server`。

### 6. Sub-agent 架構
實現「AI 管理 AI」的高階形態。
- **架構**: 使用 **Lead Agent** 進行任務規劃，並派發給多個 **Sub-agent** 並行執行。
- **優點**: 任務隔離、上下文精簡、提升 Cache 命中率。

### 7. Prompt Cache
降低 API 成本與延遲的核心技術。
- **效益**: 透過快取重複的上下文，使寫入成本降低至 25%，讀取成本僅 10%，並大幅降低延遲。

## 面臨的挑戰
- **安全性**: Prompt Injection（提示詞注入）攻擊。
- **Context Drift**: 多輪壓縮導致的資訊損失與記憶模糊。
- **評測標準缺失**: 缺乏統一的衡量 Agent 性能的基準。
- **工程取捨**: Cost vs. Latency (成本與延遲) 的權衡。
- **可重現性**: LLM 輸出的機率性導致 Debug 困難。

## 總結
Harness Engineering 是 2026 年 AI Agent 落地團隊的核心課題。工程師應專注於 Prompt Cache 優化、Hook 系統開發及 Memory 管理；PM 則應關注 Permission 邊界與評測機制。
