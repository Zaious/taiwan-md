# BUG: Sub-agent WebSearch 權限繼承斷裂

> **報告者**: 樞機師（Cardinal）
> **日期**: 2026-05-07
> **轉交**: 方舟工程（Ark IDE team）
> **嚴重度**: 影響 batch 工作流程的穩定性

---

## 症狀

Claude Code 的 Agent tool spawn 出的 background sub-agent，在某個時間點後**全面 WebSearch denied**。Main session 自己的 WebSearch 正常。

Sub-agent 回報：
```
"Permission to use WebSearch has been denied"
```
或：
```
"因權限限制無法執行線上驗證"
```

## 時間線

| 時間 | 狀態 |
|------|------|
| **2026-05-06 15:00–17:10** | Wave 1-6 haiku sub-agents（24 篇）正常使用 WebSearch ✅ |
| **~17:10** | 主人系統當機重啟 |
| **17:33 起** | 所有新 spawn 的 sub-agent **全部 WebSearch denied** ❌ |
| **17:39** | Wave 7（7 篇 **sonnet**）：全部 denied |
| **17:45** | Wave 8（7 篇 **haiku**）：全部 denied |
| **23:27** | 單獨 retry 1 個 haiku（同 Wave 1-5 一模一樣 prompt）：仍然 denied |
| **2026-05-07 09:16** | 隔天早上再試 1 個 haiku：仍然 denied |
| **09:25** | 天機星用 **Opus main session** WebSearch：**正常** ✅ |

→ **Main session WebSearch 正常，sub-agent WebSearch 全面 denied**。不是 WebSearch 本身壞掉。

## 環境

| 項目 | 值 |
|------|---|
| 平台 | Claude Code（Windows 11） |
| Project | `P:/Taiwan.md/` |
| Main session model | Opus 4.6 (1M context) |
| Sub-agent model | 測試過 haiku / sonnet — **都** denied |
| WebSearch tool | ToolSearch 載入後 main session 可用 |
| WebFetch tool | Sub-agent 也 denied（同一 permission 層） |

## 重現步驟

```
1. 在 Claude Code main session：
   - ToolSearch("select:WebSearch") → 載入成功
   - WebSearch("test query") → 正常回結果 ✅

2. 在同一 main session spawn sub-agent：
   Agent({
     description: "test WebSearch",
     model: "haiku",
     run_in_background: true,
     prompt: "用 WebSearch 搜尋『台灣 2024 總統大選』，回報結果。"
   })

3. Sub-agent 回報：
   "WebSearch 權限被拒" / "Permission denied"
   不是 rate limit（第一次就被拒）
   不是 model 問題（haiku / sonnet 都一樣）

4. 對照：系統當機重啟前（同日 15:00-17:10）同樣寫法可正常使用
```

## 影響

- batch-200 Phase 1 audit 原設計：spawn Haiku sub-agent × N 篇 parallel + WebSearch 驗證
- Wave 1-6（24 篇）成功，品質經天機星抽查確認良好
- Wave 7-8（14 篇）+ 3 篇重試 = **17 篇全部缺 WebSearch evidence**
- Fallback：天機星用 Opus main session 手動補完（成本 8.5 倍：$0.17/篇 vs $0.02/篇）
- P1 (38 篇) + P2 (98 篇) audit 尚待執行，如果 sub-agent WebSearch 不修復，成本從 ~$4 爆漲到 ~$34

## 排查方向

1. **系統重啟後 sub-agent 的 tool permission 配置是否重置？**
   - 重啟前 sub-agent 可用 WebSearch / WebFetch
   - 重啟後全部 denied
   - 可能是某個 session-level permission cache 被清空

2. **Sub-agent 是否繼承 main session 的 tool allowlist？**
   - 如果 tool allowlist 是 session-specific 的（不是 persist 在 settings.json），重啟後就會遺失
   - `ToolSearch("select:WebSearch")` 只載入到 main session 的 context，sub-agent 可能看不到

3. **Sub-agent 是否有獨立的 tool permission 設定？**
   - `.claude/settings.json` 的 `allow` / `deny` array 是否影響 sub-agent？
   - 是否有 `subagent.tools.allow` 之類的設定？

4. **Rate limit 觸發？**
   - Wave 1-6 一共跑了 ~24 個 sub-agent × 6 WebSearch/agent = ~144 次
   - 是否觸發了某種 rate limit 讓後續全部 deny？
   - 但隔天（12 小時後）仍然 denied = 不像 rate limit

## 期望修復

Sub-agent spawn 後能正常繼承 main session 可用的 tool set（至少 WebSearch / WebFetch），不需要在每個 sub-agent 的 prompt 裡手動 ToolSearch。

---

_樞機師 2026-05-07_
