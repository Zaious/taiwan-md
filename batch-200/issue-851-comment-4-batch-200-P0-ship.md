# batch-200 P0 完整修補完成 — 4 個 PR 同時 ship

哲宇好，5/4 飯局上你親口認領的「早期 200 batch 是 AI 生成、品質堪憂」這一塊，**P0（最差等級）44 篇全部修補完成**，現在 4 個 PR 同步 ship 你 review。

> 對應 #851 §5「Quality Hard Gate」+ 飯局共識「站方優先處理早期 batch」。

---

## 📦 4 個 PR 同時開（請 review）

| PR | 內容 | 篇數 | 規模 |
|----|------|------|------|
| #TBD-1 | **王建民**（單獨 — 國民級棒球圖騰，深度改寫展示） | 1 | 59 → 131 行 / 0 → 8 fn / 升 A 級 |
| #TBD-2 | **Tier A 嚴重級** 10 篇 | 10 | +917 / -275 行 |
| #TBD-3 | **Tier B 中度級** 24 篇 | 24 | +1637 / -694 行 |
| #TBD-4 | **Tier C 輕度級** 9 篇 | 9 | +519 / -254 行 |
| **合計** | **44/44 P0 全部 ship** | **44** | **+3174 / -1252 行** |

每個 PR 都附：
- 原始幻覺報告（每篇的 ❌ 修正 + URL evidence）
- 前後測對比（行數 / footnote / Tier）
- v5.6 結構紀律展示（三明治 title / anchor / 反向解釋 / 結尾閉環）
- article-health hard=0 通過證明
- 對應原始巴別塔工作的 commit 清單（squash 前的工作量）

> 推薦從 **王建民 PR 先看**（單篇深度展示，最能體現品質基準），再批次看 Tier A/B/C。

---

## 🛠️ 工作流揭露（給其他 contributor 與 AI agent 參考）

batch-200 修補不是「一個 LLM 跑 44 次」，是有架構的分工流程：

```
Phase 0: Cardinal 開 inventory + 200 篇分級（P0/P1/P2/P3）
   ↓
Phase 1: Audit — Haiku sub-agent × 8 waves，每 agent 攜帶 WebSearch 自檢
   - Wave 1-6 (24 篇) ✅
   - Wave 7-8 (14 篇) ❌ sub-agent WebSearch 權限斷裂 → 天機星 Opus 主 session 補完
   - 總 evidence: P0-DETAILED-FINDINGS.md（44 篇 ❌/⚠️ + URL）
   ↓
Phase 2: Cardinal 開 WORK-ORDERS（4 輪補強，主人逐項給 feedback）
   - Tier A 嚴重 (10) / Tier B 中度 (25) / Tier C 輕度 (9)
   - 每篇明列：修正項 + 引用目標 + v5.6 結構紀律分層
   ↓
Phase 3: 巴別塔（語言學家專家）Sonnet session 一篇一篇執行
   - 每篇必過 article-health hard=0 才 commit
   - 36 個 commits（每篇 1 個 + Phase 2 擴寫 + Polish）
   - 對 5 篇邊界文章再努力一輪達 ≥ 100 行
   ↓
Phase 4: Cardinal 抽查 (4 篇 Tier A: 施明德/劉德音/紀政/莊智淵)
   - 確認 v5.6 結構紀律到位、引用 source 正確、沒有空套模板
   - 全數 S/A 級通過
   ↓
Phase 5: 4 個 squashed PR ship（本動作）
```

**Cardinal**（樞機師，A1 system architect）負責流程設計 + 工單 + 抽查。
**巴別塔**（語言學家）負責逐篇執行（保持台灣在地語感 + 策展人語氣）。
**天機星**（首席情報官）負責高知名度文章的深度交叉驗證（fallback 角色）。

成本紀律（從工作中學到的）：
- **量產 audit > 20 篇** → Cardinal spawn Haiku sub-agent（~$0.02/篇）
- **Haiku 掛了的 fallback** → 天機星 Opus 主 session（~$0.17/篇，8.5 倍成本）
- **流程設計 + 品質框架** → Cardinal（不能下放）

完整 OPS NOTE：[`batch-200/audit-results/OPS-NOTE-evidence-補驗作業觀察.md`](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/audit-results/OPS-NOTE-evidence-補驗作業觀察.md)

---

## 🐛 工作中發現的事故（已給方舟工程開 BUG report）

5/6 17:10 主人系統重啟後，**所有新 spawn 的 sub-agent WebSearch 全面 denied**。Wave 7-8 + 重試 = 17 篇缺 evidence。

Fallback：天機星 Opus 主 session 14 分鐘補完 17 篇（成本 8.5 倍但穩定）。

完整事故時間線 + 排查方向：[`batch-200/BUG-subagent-websearch-denied.md`](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/BUG-subagent-websearch-denied.md)

對 Taiwan.md 的影響：**P1 (38 篇) + P2 (98 篇) audit 暫停**，等 sub-agent WebSearch 修復再啟動。如果不修，成本會從 ~$4 爆漲到 ~$34。

---

## 📊 修補前 vs 修補後（44 篇全體）

| 維度 | 修補前 | 修補後 |
|------|-------|-------|
| 行數 < 80 | 44/44 (100%) | **0/44 (0%)** |
| 0 footnote | 44/44 (100%) | **0/44 (0%)** |
| 平均 footnote | 0 | **~6** |
| article-health hard | 未驗 | **44/44 = 0** ✅ |
| 三明治 title | 0 | **44/44** |
| description ≥ 120 字 | 接近 0 | **44/44** |
| 5W1H metadata | 0 | **44/44** |
| 高 stake whats_excluded | 0 | **政治/爭議人物全填** |
| v5.6 核心矛盾 anchor | 0 | **Tier A 全做 / B 半做 / C 輕做** |
| v5.6 結尾閉環 | 0 | **44/44**（不再萬用膠水段）|

特別點名：
- **施明德** 11 fn / S 級展示（「生日到生日」結尾閉環）
- **劉德音** 10 fn / S 級展示（「2022 vs 2024 兩句話的距離」結尾）
- **王建民** B5 升 A 級 / 獨立 PR
- **莊智淵** 「那條線他自己畫完了」收束

---

## 🧬 對哲宇的 Maintainer 紀律承諾

1. **「站方優先處理早期 batch」是飯局共識** — 我把這個承諾兌現為 4 個可 review 的 PR
2. **每篇都有 evidence 鏈**（audit findings → 工單 → commit → article-health hard=0 → PR body 對照）
3. **不裝懂** — 該 hedge 的事實（如紀政 1966 100m 紀錄歧異、莊智淵 2000 雪梨爭議）誠實標 `where_it_hedges`
4. **5W1H metadata** 是 #851 §3 的 prototype — 44 篇 P0 是首批帶 metadata 的文章，先試試水溫，看你 review 後要不要調整 schema
5. **「兩個 information-based agents」** — 工作流揭露不是炫技，是讓你能評估 AI agent 在開源社群的工作品質基準

---

## 🗓️ 下一步

- [x] **P0 (44) 修補 + ship** ← 本動作
- [ ] **P1 (38 篇)** audit + 修補（等 sub-agent WebSearch 修復）
- [ ] **P2 (98 篇)** audit + 修補（等 sub-agent WebSearch 修復）
- [ ] **P3 (20 篇)** 驗引用 + perspective check（量小，不依賴 sub-agent，可直接做）

P1+P2 暫停的原因是成本。如果方舟工程那邊 sub-agent WebSearch 修了，我們可以接著推。否則用 Opus main session 跑也行，就是貴 8.5 倍。

歡迎指教。

🧬

---

_— Cardinal（樞機師）+ 巴別塔（語言學家） / Maintainer Zaious_
