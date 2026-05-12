# batch-200 — 古早 200 篇品質整頓

> **對應 issue**: [#851 §5](https://github.com/frank890417/taiwan-md/issues/851)
> **觸發**: 飯局哲宇親口「早期 200 batch 是 AI 生成、品質堪憂」
> **模式**: **基底 + 引用 − 幻覺**（不是全部重寫）
> **建立**: 2026-05-06 by Cardinal
> **SSOT 更新**: 2026-05-12（P0 ship 後 重整定義 / 範圍 / 現況）
> **主人**: Zaious

---

## 🎯 任務範圍

200 篇 AI 生成文章（2026-03-17 ~ 03-20 三天內 batch 生成），佔全站 662 篇的 30%。**90% 零 footnote 是核心問題**。

**全 200 篇都該做** — 哲宇親口認的「品質堪憂」。我們分四個 priority 階段執行，**不是 cherry-pick 子集，是順序問題**。

---

## ⚠️ 命名 calibration（避免雞同鴨講）

「P0 / P1 / P2 / P3」是**修補執行順序**，不是「critical vs not」。**全部 200 篇都會做**。

| 命名 | 意思 | 容易誤讀為 |
|------|------|----------|
| **P0** | priority 0，最先做的子集（44 篇）| ❌「全部 critical 的篇」/「ship 完 = 任務完成」 |
| **P1** | priority 1，第二批（38 篇）| ❌「次要」「可做可不做」 |
| **P2** | priority 2，第三批（98 篇）| ❌ 同上 |
| **P3** | priority 3，最後批（20 篇，已有 fn 的）| ❌「不用做」 |

**對外溝通注意**：跟哲宇 / 別 contributor 對話時，不要只說「P0 ship 完了」，要說「P0（44 篇）ship 完，P1+P2+P3 共 156 篇陸續處理中」。

---

## 操作原則

**保留原文作為基底** — AI 生成的內容結構不一定差，缺的是引用支撐。

| 操作 | 做什麼 |
|------|--------|
| ✅ 補引用 | 找真實 source 支撐原文 claims |
| ✅ 移幻覺 | 事實錯誤 / 捏造 claims → 移除或修正 |
| ✅ 補具體 | v5.6 anchor noun / 反向解釋 / 結尾 |
| ✅ 5W1H | 修完順帶附 metadata（issue #851 §3）|
| ✅ perspective scan | 高 stake 子集（People/Society/History）（issue #851 §2）|
| ❌ 不全部重寫 | 除非 P0 且內容空泛到無法補救 |

---

## 📋 Severity 分級定義（SSOT）

```
總計: 200 篇
├── P0 (22%) — 0 footnote + < 80 行    → 44 篇
├── P1 (19%) — 0 footnote + 80-119 行  → 38 篇
├── P2 (49%) — 0 footnote + ≥ 120 行   → 98 篇
└── P3 (10%) — ≥ 1 footnote 已有部分 source → 20 篇
```

**Priority 邏輯**：
- P0 最先做：篇幅最短 + 0 fn = 內容最薄 + 無 source，**修補時要從骨架重建**
- P1 第二批：篇幅中等 + 0 fn = 內容有體但無 source
- P2 第三批：篇幅長 + 0 fn = 內容多但無 source（修補主要是補引用）
- P3 最後批：已有 ≥ 1 fn = 比較簡單，驗證 + 補強

完整清單：[`inventory-graded.txt`](inventory-graded.txt)

---

## 📦 各階段範圍 + Category 分布（實算）

### P0 — 44 篇（已 ship）

| Category | 篇數 | % |
|---------|------|---|
| **People** | **41** | 93% |
| Society | 1 | 2% |
| History | 1 | 2% |
| Technology | 1 | 2% |

**特性**：93% 是人物名片型文章，篇幅短 + 無引用 = 最容易出幻覺的子集。
**工作量**：實際做出來分 Tier A (10 嚴重幻覺) + Tier B (25 中度) + Tier C (9 輕度)。

### P1 — 38 篇（5/12 baseline 核對完成，未開動）

| Category | 篇數 | % |
|---------|------|---|
| **People** | **11** | 29% |
| **Economy 企業** | **7** | 18% |
| Society | 3 | 8% |
| Food | 3 | 8% |
| Art | 3 | 8% |
| Nature | 3 | 8% |
| History | 2 | 5% |
| Music | 2 | 5% |
| Culture | 2 | 5% |
| About | 1 | 3% |
| Lifestyle | 1 | 3% |

**特性**：跟 P0 對比，**主題多元化**。People 比例從 93% 降到 29%，Economy 企業類 (7 篇) 是新主戰場。Society / History 議題類比例上升 (5 篇 = 13%)。
**Frontmatter hard 待修**：3 篇（陳映真 / 楊右任 / 台灣客家音樂 — 同 P0 那 4 篇的 edge case）。

### P2 — 98 篇（未開動，僅統計）

| Category | 篇數 | % |
|---------|------|---|
| **Economy 企業** | **22** | 22% |
| Technology | 11 | 11% |
| Music | 11 | 11% |
| People | 10 | 10% |
| Culture | 9 | 9% |
| Nature | 8 | 8% |
| Society | 7 | 7% |
| Geography | 6 | 6% |
| Art | 4 | 4% |
| History | 3 | 3% |
| Food | 3 | 3% |
| About | 2 | 2% |
| Lifestyle | 1 | 1% |
| resources | 1 | 1% |

**特性**：篇幅長（≥ 120 行）+ 0 fn = 內容多但無 source。Economy 企業類最多 (22 篇)，跟 P1 的 7 篇企業相加 = 29 篇企業文章是「修補主戰場」。

### P3 — 20 篇（未開動，已有部分 fn）

| Category | 篇數 |
|---------|------|
| People | 5 |
| Food | 5 |
| History | 3 |
| Culture | 2 |
| Art | 2 |
| Technology | 1 |
| Nature | 1 |
| Music | 1 |

**特性**：已有 ≥ 1 footnote = 比較簡單。主要工作是「驗證現有引用 URL 還活 + perspective check」。

---

## 🚦 現況進度

| 階段 | 篇數 | 狀態 | PR / commit | 日期 |
|------|------|------|------------|------|
| **Phase 0 inventory + 分級** | 200 | ✅ 完成 | commit `6c7b4f4` | 2026-05-06 |
| **P0 audit (Phase 1)** | 44 | ✅ 完成 | 8 waves Haiku spawn / 17 篇 Opus 補驗 / P0-DETAILED-FINDINGS | 2026-05-06~07 |
| **P0 修補 (Phase 2-3)** | 44 | ✅ 完成 | 巴別塔 Sonnet 36 commits | 2026-05-08 |
| **P0 ship** | 44 | ✅ 完成 | PR #888 王建民 / #889 Tier A / #890 Tier B / #891 Tier C / #892 哲宇整合 merge | 2026-05-08 |
| **P0 polish (對位句型 follow-up)** | 27 (對位) + 4 (frontmatter) | ✅ 完成 | PR #910 polish ship | 2026-05-09 |
| **P1 baseline 核對** | 38 | ✅ 完成 | 全 38 篇仍在 P1 狀態（80-119 行 + 0 fn），3 篇 frontmatter hard 待修 | 2026-05-12 |
| **P1 audit (Phase 1)** | 38 | ⬜ 待開動 | — | — |
| **P1 修補 (Phase 2-3)** | 38 | ⬜ | — | — |
| **P1 ship** | 38 | ⬜ | — | — |
| **P2 audit / 修補 / ship** | 98 | ⬜ | — | — |
| **P3 audit / 修補 / ship** | 20 | ⬜ | — | — |

**已 ship 比例**：44/200 = 22%

---

## 📂 目錄結構

```
batch-200/
├── README.md                                  ← 本檔（SSOT — 定義 / 範圍 / 現況）
├── inventory-raw.txt                          ← 200 篇原始清單（date|path）
├── inventory-enriched.txt                     ← 加行數 + footnote
├── inventory-graded.txt                       ← 完整 P0-P3 等級 + perspective scan flag
├── AUDIT_PROMPT.md                            ← Phase 1 audit prompt 範本
├── WORK-ORDERS.md                             ← P0 巴別塔工單（已完成）
├── WORK-ORDERS-polish-prose.md                ← P0 polish 工單（已完成）
├── BUG-subagent-websearch-denied.md           ← 方舟工程 bug report（已修復 5/8）
├── audit-results/                             ← P0 audit evidence
│   ├── P0-DETAILED-FINDINGS.md                ← 44 篇完整 audit + URL
│   ├── OPS-NOTE-evidence-補驗作業觀察.md       ← 量產 vs fallback 分工分析
│   ├── batch{1-5}-summary.md                  ← wave audit 進度
│   └── People-{張艾嘉,施明德}.md              ← prototype audit 範本
├── pr-bodies/                                 ← 各 PR body draft
│   ├── PR-1-wang-jian-min.md
│   ├── PR-2-tier-A.md
│   ├── PR-3-tier-B.md
│   ├── PR-4-tier-C.md
│   └── PR-5-polish-prose.md
└── issue-851-comment-4-batch-200-P0-ship.md   ← #851 工作總結 comment
```

---

## 🛠️ 作業流程（從 P0 經驗確立）

每個 priority 階段（P0/P1/P2/P3）都走相同的 5 phase 流程：

```
Phase 0: Cardinal 預備
  └── git pull upstream main + 開 branch + baseline 核對

Phase 1: Audit
  └── 量產 (>20 篇) → spawn Haiku sub-agent × N waves
  └── Fallback → 天機星 Opus main session（成本高，僅 sub-agent 掛時用）
  └── 結果存 audit-results/

Phase 2: Triage + 工單
  └── Cardinal 開 WORK-ORDERS（Tier A/B/C 分級 + 修正項 + 引用候選）

Phase 3: 修補
  └── 巴別塔（語言學家）Sonnet session 一篇一篇執行
  └── 每篇必過 article-health 雙 gate（default + release-pr）才 commit

Phase 4: Cardinal 抽查 + ship
  └── 抽查 4-6 篇 Tier A 確認品質
  └── 雙 gate 自驗 + push + 寫 PR body
  └── Zaious GitHub web UI 開 PR

Phase 5: Polish follow-up（如需）
  └── 若 release-pr profile warn 偏高 → 開 polish PR sweep
```

---

## 🌟 從 P0 學到的（給 P1+ 帶入）

### 紀律升級（已寫進 PROJECT-STANCE / AGENTS）

1. **AGENTS §7**：PR 開前必跑三道 — `git pull upstream main` + `git rebase main` + 雙 gate 自驗
2. **AGENTS §5**：default profile + release-pr profile **雙 gate** 為交付必過
3. **AGENTS §4**：frontmatter 規格對齊 5/8 formatter（flow array tags + CANONICAL_ORDER）
4. **STANCE §7 紅線 12-14**：對外身份紀律（⚙️ 不用 🧬 / ChronicleCore 不用 A1 / 不提工作成本）

### 工具狀態（5/12 確認）

| 工具 | 狀態 |
|------|------|
| Frontmatter formatter pre-commit hook (5a1542f66) | ✅ 生效，未來 commit 不會撞 conflict |
| Sub-agent WebSearch | ✅ 5/8 22:42 已修復（5/6-5/8 期間斷裂）|
| article-health 13 plugin | ✅ 含 spore-writing plugin（only apply spore 路徑，不影響 article 工作）|

### 跟哲宇 routine 的協調

哲宇有自己的 trend-driven priority queue（5/8-5/12 自己 rewrite 盧秀燕 / 季麟連 / 徐巧芯 / 沈文程 等 = 不在我們 batch-200 清單）。**我們做古早 batch 不跟他撞**，他做新聞時事人物。

---

_建立 by Cardinal（樞機師）2026-05-06_
_SSOT 重整 2026-05-12（P0 ship 後）_
_對應 issue #851 §5 + 飯局共識「哲宇認領早期 200 batch 品質堪憂」_
