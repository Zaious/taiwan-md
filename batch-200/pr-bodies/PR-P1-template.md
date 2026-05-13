# PR Body: batch-200 P1 修補（39 篇）

> 模板：4-step structure（主人 5/14 確立）
> 用途：給 P1 ship 用，含 38 P1 + 1 P2 順手做的國家公園

---

## 📝 這個 PR 做了什麼

batch-200 P1 修補 **39 篇**（38 P1 + 1 P2 國家公園順手）。古早 AI batch 生成稿幻覺率高，本批處理：

- 27 Tier A 嚴重級（多重幻覺 + 重大遺漏）
- 11 Tier B 中度級（1-2 幻覺 + 部分遺漏）
- 1 Tier B+/A 級（水彩畫百年流變 — 第一輪即達標）

對應 [#851](../../issues/851) §5 哲宇親口認領「早期 200 batch 是 AI 生成、品質堪憂」工作。

## 🐛 原始幻覺類型（audit 抓出的 5 種共通模式）

| 類型 | 代表篇 + 修正 |
|------|-------------|
| **偽造人物身分** | 長春石化「廖頂立」實際是廖銘昆/林書鴻/鄭信義三條龍；玉山金控創辦人黃永仁完全沒提；陳俊良「設計詩人」稱號疑錯掛 |
| **偽造企業血脈** | 兆豐金控寫成「1897 台灣銀行前身」（兩家獨立公股銀行硬接成血脈）|
| **劇情/事件錯置** | 陳映真〈將軍族〉劇情完全寫錯（實寫退伍老兵與雛妓悲劇）；中鋼技術合作對象 U.S. Steel→McLouth Steel；統盟案 1968 vs 1988 混淆 |
| **引用幻覺** | 冰品文化參考資料 6 條全捏造；麵包烘焙 3 本書名查無；陳俊良 freefalldesign.com.tw 是幻覺 URL（實 freeimage.com.tw）|
| **critical omission** | 兆豐 2016 NT$57 億洗錢罰款全篇 0 字；陳俊良總統府春聯（後查證實際是國宴餐具）；蕭青陽 2023 第 65 屆葛萊美得獎全文沒寫；夜生活 KTV 2020 錢櫃林森北 5 死大火完全沒提 |

## 🔧 我們怎麼做

5-phase 流程（從 P0 經驗確立）：

1. **Phase 1 audit** — Haiku sub-agent × 5 waves 跑 38 篇
2. **Phase 2 triage** — Cardinal 開 WORK-ORDERS（27 個高必證點清單）
3. **Phase 3 修補** — 巴別塔 Sonnet 一篇一篇 + 雙 Gate 自驗
4. **Phase 4 抽查 + 二修** — Cardinal 抽查發現問題後巴別塔二修
5. **Phase 5 ship** — 本 PR

## 🚨 修補過程發現的問題

1. **第一輪 70% critical 漏率**：巴別塔過 Gate 1+2，但 Cardinal 抽 10 篇有 7 篇 critical 結構性錯沒修
2. **根因**：Gate 1+2 只查格式/prose-health 不查事實層 critical 錯誤 + 修補時偏 addition 不偏 replacement（補一段做、整段重寫跳過）
3. **解法**：升 SOP — **Gate 3 = audit findings closed-loop check**（每條 ❌ 都要 grep verification + per-article fix log 必填）
4. **三層 verification 發現 audit 自己有錯**：陳俊良「總統府春聯」是 audit 反向錯誤 — **陳俊良從沒做過春聯**，實際是總統府國宴餐具「天圓地方」系列（澳門設計雙年展評審獎）。Maintainer 自我矯正系統運作

## ✅ 最後做了什麼

- **39 篇全部通過**：article-health Gate 1 hard=0 + Gate 2 prose-health ≤3 + 每篇 ≥5 footnote
- **17 篇幻覺事實 dismantle / replace**（兆豐 1897 血脈 / 長春石化廖頂立 / 陳映真〈將軍族〉劇情等）
- **16 篇重要 section 補入**（兆豐 2016 罰款 / 玉山黃永仁 founding myth / 蕭青陽 2023 葛萊美 / 政治環境 2024 大選後動態 / 國際標示 UN 2758 等）
- **Perspective balance**：陳映真補統派視角 + 國際標示補中國立場 + 鄭南榕補爭議視角 + 人權平等補 2018 公投反方
- 涵蓋 People 11 / Economy 6 / Society 3 / History 2 / Music 2 / Food 3 / Art 3 / Nature 4 / Culture 2 / Lifestyle 1

完整 evidence 在 fork `maintainer-workspace` branch：
- [P1-DETAILED-FINDINGS.md](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/audit-results/P1-DETAILED-FINDINGS.md)
- [WORK-ORDERS-P1.md](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/WORK-ORDERS-P1.md)
- [P1-EXECUTION-REPORT.md](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/P1-EXECUTION-REPORT.md)
- [reports/P1-batch-repair-2026-05-13.md](../tree/fix/batch-200-P1-batch-1/reports/P1-batch-repair-2026-05-13.md)

⚙️ Cardinal × Zaious (Maintainer)
