## 📝 這個 PR 做了什麼？

batch-200 古早 200 篇品質整頓 P0 第 1 批 — **王建民單篇深度改寫**。從 59 行 / 0 footnote 的 AI 生成稿，升級為 131 行 / 8 footnote 的 A 級深度文章。

> 對應 issue [#851](../../issues/851) §5 哲宇親口認領「早期 200 batch 是 AI 生成、品質堪憂」的修補工作。

## 📁 變更類型

- [x] ✏️ 修改/更新現有文章
- [x] 🐛 修復錯誤（事實更正、引用補充）

## 📊 修補規模

| 項目 | 修補前 | 修補後 |
|------|-------|-------|
| 行數 | 59 | **131** (+122%) |
| Footnote | 0 | **8** |
| Tier | B5 中度 | **升 A 級**（深度改寫）|
| article-health hard | 未驗 | **0** ✅ |
| frontmatter 完整度 | 缺 readingTime / lastVerified | 完整 + 5W1H metadata |

## 🐛 原始幻覺報告（從 P0 audit 抓出）

來源 evidence 完整紀錄於 `batch-200/audit-results/P0-DETAILED-FINDINGS.md`

| # | 原文 | 正確事實 | 來源 |
|---|------|---------|------|
| ❌ 1 | 國中：善化國中 | **建興國中**（教練張錫杰，亦培養出郭泓志、胡金龍、羅錦龍）| [zh.wikipedia.org/王建民](https://zh.wikipedia.org/wiki/王建民_(棒球運動員)) |
| ❌ 2 | 2006「勝投王亞軍」 | **19 勝 6 敗，與桑塔納並列美聯勝投王** | [udn.com/news/story/6999/8309919](https://udn.com/news/story/6999/8309919) |

## ➕ 補充內容（原文遺漏）

- 補 2008/6/15 跑壘扭傷右腳踝（蹠跗韌帶拉傷）+ 來源 evidence
- 補 2016 重返大聯盟（堪薩斯皇家）+ 來源 evidence
- 補 2017 經典賽參與情況
- 補退役時間 + 富邦悍將投手教練身份

## ✨ v5.6 結構紀律展示（Tier A 全做）

| 維度 | 展示 |
|------|------|
| **三明治 title** | 「王建民：建興國中到洋基王朝，棒球國民圖騰的雙年榮光」 |
| **description** | 擴至 ~140 字（具體 scene + 軌跡 + 核心矛盾）|
| **核心矛盾 anchor** | 「英雄敘事 vs 巔峰墜落 vs 國民圖騰」三層張力 |
| **反向解釋編織** | 「不是棒球文化的累積，而是…」「不是英雄敘事，而是…」（5 處）|
| **結尾** | 閉環式收束（呼應開頭建興國中）|
| **主角直引** | ≥ 3 句 |
| **5W1H metadata** | why_this_hook / whats_excluded / where_it_hedges 完整 |

## 🔄 對應原始工作

此 PR 為 **squashed commit**，對應巴別塔（Sonnet session）原本的 **2 個工作 commits**：

1. `688d9958a` fix(people): B5 王建民+B6 童子賢+B7 簡立峰 事實修正+v5.6 rewrite
2. `503033d8b` feat(people): 5 篇邊界檔案補強 — 王建民升 A-tier + 郭台銘/幾米/鄭兆村達 B-tier + 郭泓志補 fn

> Merge 時建議「Squash and merge」保持 main branch 乾淨。

## ✅ 自我檢查

- [x] 文章有完整的 frontmatter（title, description, date, tags, category）
- [x] `category` 用英文 + 對齊路徑（People，canonical）
- [x] `author: 'Taiwan.md'`（既有寫法保留，未改）
- [x] `featured: false`
- [x] **腳註用 canonical 格式**：`[^N]: [標題](URL) — 至少 10 字描述` ✅
- [x] 內容有附上可查證的參考資料來源
- [x] 沒有抄襲或版權問題
- [x] **article-health hard=0 通過**

## 🔗 相關 Issue

Closes part of #851 §5（古早 200 篇品質整頓）

完整 batch-200 任務文件：
- [`batch-200/README.md`](../tree/main/batch-200/README.md) — 200 篇分級 + 流程
- [`batch-200/audit-results/P0-DETAILED-FINDINGS.md`](../tree/main/batch-200/audit-results/P0-DETAILED-FINDINGS.md) — 44 篇完整 audit 證據
- [`batch-200/WORK-ORDERS.md`](../tree/main/batch-200/WORK-ORDERS.md) — 巴別塔工單

---

🧬 **Maintainer 主動修補** — 由 Cardinal（樞機師，A1 system architect）開單 + 巴別塔（語言學家）Sonnet session 一篇一篇執行 + Cardinal 抽查驗收。
