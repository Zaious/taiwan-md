## 📝 這個 PR 做了什麼？

batch-200 古早 200 篇品質整頓 P0 第 2 批 — **Tier A 嚴重級 10 篇**。每篇有 ≥ 3 個事實幻覺 + 多處遺漏（過世/退休/近況）+ 0 footnote。修補為事實正確、引用充足、v5.6 結構紀律全做的 A 級文章。

> 對應 issue [#851](../../issues/851) §5。

## 📁 變更類型

- [x] ✏️ 修改/更新現有文章
- [x] 🐛 修復錯誤（事實更正、引用補充）

## 📊 修補規模

| 項目 | 修補前 | 修補後 |
|------|-------|-------|
| 篇數 | 10 | 10 |
| 平均行數 | < 80 | **~110** |
| 平均 footnote | 0 | **~8** |
| article-health hard | 未驗 | **10/10 = 0** ✅ |

## 🐛 各篇原始幻覺修補

> 完整 evidence + URL 紀錄於 `batch-200/audit-results/P0-DETAILED-FINDINGS.md`

| # | 篇 | 主要 ❌ 修正 | fn |
|---|----|------------|----|
| **A1** | 施明德 | 刪 1994 市長幻覺 + 補 2024 過世（生日當天）+ 補 2000 退黨 + 移除 AI 引言 | 11 |
| **A2** | 劉德音 | 出生年 1952→1954、博士柏克萊（非 MIT）、「現任董事長」→ 2024 卸任 | 10 |
| **A3** | 盧彥勳 | 溫布頓對手索德林→**羅迪克**、4 屆→**5 屆**奧運、退役 2016→**2021** | 8 |
| **A4** | 紀政 | 修 5 項事實（生日 / 200m 地點 / 跨欄成績）+ 補 2024 國策顧問 + 2025 正名運動 | 8 |
| **A5** | 莊智淵 | 修生日 / 奧運屆數 4→**6** / 退役時間 + 補 2024 巴黎終戰 + 2025 中山大學 | 9 |
| **A6** | 葉國一 | 出生年 1936→**1941**、學歷台大→**士林高商**、「現任」→ 2023 交棒 | 7 |
| **A7** | 郭泓志 | 修選秀年矛盾（1999 vs 2000）+ 補 2006 MLB 首登板（台灣第一）| 5 |
| **A8** | 陳昇 | 修 4 項事實 + 移除《新鴛鴦蝴蝶夢》搭檔幻覺 | 7 |
| **A9** | 王永慶 | 移除「1968 輕油裂解廠」幻覺（屬中油）+ 補家族爭產 | 7 |
| **A10** | 楊傳廣 | 補 1963 世界紀錄 9121 分（原文遺漏）+ 補 2025 國寶級致敬 | 7 |

## ✨ v5.6 結構紀律展示（Tier A 全做）

每篇都做完整 v5.6 結構升級：

- ✅ **三明治 title**（「{人名}：{核心張力一句話}」≤ 30 字）
- ✅ **description ≥ 120 字**（具體 scene + 軌跡 + 核心矛盾）
- ✅ **5W1H metadata**（why_this_hook + whats_excluded + where_it_hedges 完整；高 stake 政治人物 whats_excluded 必填）
- ✅ **核心矛盾 anchor 貫穿**（description / 開場 / 中段 / 結尾）
- ✅ **反向解釋編織**（每篇 ≥ 2 處「通行說法是 X，但更精確的讀法是 Y」）
- ✅ **結尾改閉環式或餘韻式**
  - 例：施明德「1980 年... 2024 年... 但他走完了，生日到生日，整整八十三年」
  - 例：劉德音「2022 年他說沒有人能用武力控制台積電；2024 年他說請買台積電；這兩句話的距離，就是他六年任期的全部」
- ✅ **主角直引 ≥ 3 句**（People 文標準）
- ✅ **footnote ≥ 7**（政治人物 ≥ 10）

## 🔄 對應原始工作

此 PR 為 **squashed commit**，對應巴別塔（Sonnet session）原本的 **10 個工作 commits**（每篇一個）：

1. `17dbb24f7` fix(A1): 施明德
2. `ce1503b2f` fix(A2): 劉德音
3. `1f41f5c12` fix(A3): 盧彥勳
4. `01baed85a` fix(people): 紀政 — 修正 5 項事實錯誤，補正名運動 (A4 P0)
5. `49b0fce5c` fix(people): 莊智淵 — 修正 3 項事實錯誤，補巴黎奧運退役 (A5 P0)
6. `821559249` fix(people): 葉國一 — 修正 3 項事實錯誤，補 2023 交棒 (A6 P0)
7. `be6b377fc` fix(people): 郭泓志 — 修正出生日，補台灣第一里程碑 (A7 P0)
8. `d2b2482db` fix(people): 陳昇 — 修正 4 項事實錯誤，移除《新鴛鴦》幻覺 (A8 P0)
9. `7241fb7ca` fix(people): A9 王永慶 P0 hallucination removal + prose fixes
10. `355cda23f` fix(people): A10 楊傳廣 P0 rewrites + add 1963 WR + 2025 national treasure

> Merge 時建議「Squash and merge」保持 main branch 乾淨。

## ✅ 自我檢查

- [x] 文章有完整的 frontmatter（title, description, date, tags, category）
- [x] `category` 用英文 + 對齊路徑（People，canonical）
- [x] `author: 'Taiwan.md'`（既有寫法保留）
- [x] `featured: false`
- [x] **腳註用 canonical 格式**：`[^N]: [標題](URL) — 至少 10 字描述` ✅
- [x] 內容有附上可查證的參考資料來源
- [x] 沒有抄襲或版權問題
- [x] **article-health hard=0 通過**（10/10）

## 🔗 相關 Issue

Closes part of #851 §5（古早 200 篇品質整頓）

完整 batch-200 evidence trail（在 fork 的 `maintainer-workspace` branch，不 PR 回 upstream）：
- [`batch-200/README.md`](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/README.md)
- [`batch-200/audit-results/P0-DETAILED-FINDINGS.md`](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/audit-results/P0-DETAILED-FINDINGS.md)
- [`batch-200/WORK-ORDERS.md`](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/WORK-ORDERS.md)

---

🧬 **Maintainer 主動修補** — 由 Cardinal（樞機師）開單 + 巴別塔（語言學家）Sonnet session 一篇一篇執行 + Cardinal 抽查驗收（施明德/劉德音/紀政/莊智淵）。
