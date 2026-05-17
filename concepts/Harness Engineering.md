---
title: "Harness Engineering"
date: 2026-05-17
tags: ["ai-agent", "infrastructure", "agentic-engineering"]
---

# Harness Engineering (AI 駕馭工程)

**Harness Engineering** 是圍繞大型語言模型 (LLM) 設計的完整系統架構，旨在管理 AI Agent 從意圖捕捉、上下文編譯、工具執行，到結果驗證的全生命週期。

其核心公式為：**Agent = Model + Harness**。

## 核心架構與模組

Harness Engineering 的目標是提供一個安全、可控且高性能的環境，讓模型能夠在生產環境中可靠運行。其關鍵模組包括：

- **[[Context Management]] (上下文管理)**: 決定如何在有限的 Token 視窗內，透過 **[[Compaction]]** 與 **Deferred Loading** 提供最有效的資訊。
- **[[Tool Design]] & [[MCP]] (工具設計與標準)**: 使用如 **[[Model Context Protocol (MCP)]]** 等標準協議，讓 Agent 能透過統一介面與外部世界（資料庫、GitHub、Slack）互動。
- **[[Permission System]] (權限系統)**: 提供「縱深防禦」，透過 **[[Hooks]]** 與不同等級的權限模式（如 `plan`, `default`, `auto`）來控制 Agent 的行為邊界。
- **[[Memory Systems]] (記憶系統)**: 包含處理長對話的 **[[Compaction]]** 以及提供跨會話持久化能力的 **Memory Tool**。
- **[[Sub-agent Architecture]] (子代理架構)**: 透過「主代理 (Lead Agent)」協調多個「子代理 (Sub-agent)」並行執行任務，實現複雜任務的拆解與執行。
- **[[Prompt Caching]] (提示詞快取)**: 透過快取重複的上下文，大幅降低 API 的成本與延遲。

## 工程挑戰

- **[[Prompt Injection]]**: 外部輸入可能攜帶惡意指令，試圖操控 Agent。
- **[[Context Drift]]**: 長期對話壓縮後可能導致資訊損失與記憶模糊。
- **評測標準缺失**: 缺乏統一的基準來衡量不同 Harness 設計的優劣。
- **成本與延遲的權衡**: 在安全性、複雜度與執行速度之間進行工程取捨。

## 相關概念
- [[Context Engineering]]
- [[Prompt Engineering]]
- [[AI Agent]]
