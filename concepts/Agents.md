# 代理 (Agents) | OpenCode

## 概述 (Overview)
設定和使用專門的代理。代理是針對特定於任務和工作流程設定的 AI 助手，允許自訂提示詞、模型和工具存取權限。

## 類型 (Types)
OpenCode 中的代理分為兩種類型：
1. **主代理 (Primary Agents)**: 直接互動的主要助手。可以使用 **Tab** 鍵循環切換。
   - **Build**: 預設主代理，啟用所有工具，適用於開發工作。
   - **Plan**: 用於規劃和分析的受限代理，預設不允許檔案編輯和 bash 命令。
2. ** 子代理 (Subagents)**: 專門執行特定任務的助手，可透過 **@ 提及** 呼叫。
   - **General**: 用於研究複雜問題和執行多步驟任務的通用代理。
   - **Explore**: 快速唯讀代理，用於查找檔案和搜尋程式碼。
   - **Scout**: 唯讀代理，用於研究外部文件與依賴。

## 使用方法 (Usage)
1. **切換主代理**: 在工作階段期間使用 **Tab** 鍵或 `switch_agent` 快速鍵。
2. **呼叫子代理**:
   - 由主代理根據任務自動呼叫。
   - 在訊息中使用 **@ 提及** 手動呼叫（例如：`@general help me...`）。
3. **工作階段導覽**: 使用 `<Leader>+Right` 或 `<Leader>+Left` 在父工作階段與子工作階段之間切換。

## 設定 (Configuration)
代理可以透過以下兩種方式進行設定：

### JSON 設定 (`opencode.json`)
在設定檔中定義代理的模式、模型、工具權限等。
範例：
```json
{
  "agent": {
    "build": {
      "mode": "primary",
      "model": "anthropic/claude-sonnet-4-20250514",
      "tools": { "write": true, "edit": true, "bash": true }
    }
  }
}
```

### Markdown 設定
將代理定義在 Markdown 檔案中。
- **全 域**: `~/.config/opencode/agents/`
- **專案級**: `.opencode/agents/`
檔案名稱即為代理名稱（例如 `review.md` 建立 `review` 代理）。

## 關鍵設定選項 (Key Options)
- **description**: 代理的功能描述（必需）。
- **temperature**: 控制回應的隨機性 (0.0 - 1.0)。
- **steps**: 最大代理迭代次數（控制成本）。
- **model**: 覆寫代理使用的模型。
- **tools**: 控制可用工具（`write`, `edit`, `bash` 等）。
- **permission**: 管理工具權限（`ask`, `allow`, `deny`）。
- **mode**: 設定模式 (`primary`, `subagent`, `all`)。
- **color**: 自訂 UI 顯示顏色。

## 建立代理 (Creating Agents)
使用指令產生成代理：
```bash
opencode agent create
```

## 常用場景 (Use Cases)
- **Build**: 完整開發。
- **Plan**: 分析與規劃。
- **Review**: 程式碼審查。
- **Debug**: 問題排查。
- **Docs**: 文件編書寫。
