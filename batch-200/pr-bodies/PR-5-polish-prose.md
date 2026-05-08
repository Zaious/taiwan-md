## 📝 這個 PR 做了什麼？

**P0 batch-200 第一輪修補 ship 後的 polish follow-up**。處理 5/8 #888-#891 review 中你點名的 §11 對位句型 warn 偏高問題 + 順手修 4 篇 frontmatter hard。

純 polish PR — 不改事實 / 不補引用 / 不重寫結構。

> 對應 #851 §5（古早 200 篇品質整頓）+ PR #892 整合 ship 後的紀律 follow-up。

## 📁 變更類型

- [x] ✏️ 修改/更新現有文章（純 prose polish）
- [x] 🐛 修復錯誤（4 篇 frontmatter hard 違規）

## 📊 修補規模

| 維度 | 修補前（#892 ship 後）| 修補後（本 PR）|
|------|--------------------|---------------|
| 對位句型 warn 跨 P0 | 155 處 / 41 篇 | **88 處** / 41 篇（-43%）|
| 每篇對位句型上限 | 19 處（郭泓志最重）| **≤ 3 處 / 篇**（§11 紀律）|
| frontmatter hard | 4 篇（許文龍/魏德聖/史前時代/AI Labs）| **0 篇** ✅ |
| 全 P0 article-health hard 總和 | 4 | **0** ✅ |
| 篇數 | 44 | 27 polish + 4 frontmatter（14 篇已達標不動）|

## 🎯 具體修了什麼

### Task A：27 篇對位句型 reduce（每篇 ≤ 3 處）

| Tier 重（8 篇 warn ≥ 9）| 改前 → 後 |
|----------------------|----------|
| 郭泓志 | 19 → 3 |
| 王建民 | 16 → 3 |
| 葉國一 | 14 → 3 |
| 許芳宜 | 14 → 3 |
| 伍佰 | 13 → 3 |
| 張艾嘉 | 13 → 3 |
| 羅大佑 | 11 → 3 |
| 紀政 | 10 → 3 |

| Tier 中（10 篇 warn 5-9）| 改前 → 後 |
|----------------------|----------|
| 陳昇 / 朱天文 | 10 → 3 |
| 白先勇 / 鍾理和 | 9 → 3 |
| 陳建仁 / 林百里 | 8 → 3 |
| 簡立峰 | 7 → 2 |
| 張明正 | 7 → 3 |
| 李昂 / 黃春明 | 7 → 3 |

| Tier 輕（9 篇 warn 4-6）| 改前 → 後 |
|----------------------|----------|
| 莊智淵 / 許淑淨 / 鄧雨賢 | 5-6 → ≤ 3 |
| 楊傳廣 | 4 → 2 |
| 魏德聖 | 4 → 2（同時修 frontmatter）|
| 郭台銘 / 謝淑薇 / 幾米 / 明華園 | 已 ≤ 3 不動 |

### Task B：4 篇 frontmatter hard 修補

`tags:` block-style flow array → single-line flow array：

```yaml
# 改前（hard=1）
tags:
  ['科技與企業', '奇美集團', ...]

# 改後（hard=0）
tags: ['科技與企業', '奇美集團', ...]
```

涉及：許文龍 / 魏德聖 / 史前時代與原住民 / 台灣人工智慧實驗室

> 補充：這個 edge case 是 5a1542f66 frontmatter formatter pre-commit hook 沒覆蓋到的（應該之後可以加進 hook 的 fix() 規則）

### 14 篇已達標 — 不動

施明德 3 / 童子賢 3 / 鄭兆村 3 / 林俊傑 3 / 劉德音 2 / 盧彥勳 2 / 張惠妹 2 / 朱經武 2 / 龍應台 2 / 魏哲家 2 / 陽岱鋼 2 / 王永慶 1 / 李宗盛 1 / 民主制度 1

## ✨ 改寫策略（保留張力前提下 reduce）

巴別塔（語言學家）執行時用三招：

1. **直接陳述**（最常用）：「**不是** A，**而是** B」→「就是 B」/「問題在 B」
2. **拆兩段**：把對位句拆成兩個獨立陳述，讓邏輯更明確
3. **保留最有力的 ≤ 3 處**：每篇核心矛盾 anchor 對應的對位句保留（通常 description 那個）

抽樣（郭泓志 19→3）：
- 「問題**不是**有沒有能力，**而是**手肘能不能撐他...」→ 「問題始終是：手肘能不能撐他...」
- 「他**沒有**選擇退出，**而是**在每次手術之後重新出現」→ 「他每次手術之後都重新出現」
- 「**不是**最閃耀的那種，**而是**最紮實的那種」→ 「也是台灣棒球一個紮實的記錄點」

不會做的：
- ❌ 把對位砍光變平淡敘述
- ❌ 改事實 / 補引用 / 重寫結構
- ❌ 動 v5.6 anchor / 三明治 title / 結尾 / 5W1H metadata

## 🔄 對應原始工作

此 PR 對應巴別塔（Sonnet session）原本的 **6 個工作 commits**（自然分批，每批 3-5 篇）：

1. `939b35935` polish(P0/prose): batch-A 郭泓志/王建民/葉國一/許芳宜/伍佰
2. `9abba0563` polish(P0/prose): batch-B 張艾嘉/羅大佑/紀政/陳昇/朱天文
3. `71a18b66b` polish(P0/prose): batch-C 白先勇/鍾理和/陳建仁/林百里/簡立峰
4. `2b1f4a490` polish(P0/prose): batch-D 張明正/李昂/黃春明/莊智淵/許淑淨
5. `84d7d027e` polish(P0/prose): batch-E 鄧雨賢/楊傳廣/魏德聖
6. `ac2aa5b01` fix(P0/frontmatter): 4 篇 multi-line flow array → single-line

> Merge 時建議「Squash and merge」保持 main branch 乾淨。

## ✅ 自我檢查

- [x] 所有 frontmatter 完整且符合 5/8 frontmatter formatter 規範
- [x] `category` 用英文 + 對齊路徑（People / Society / History / Technology canonical）
- [x] `author: 'Taiwan.md'`（保留原值）
- [x] `featured: false`
- [x] 腳註格式 canonical（沒動引用，保留原版）
- [x] **article-health hard=0（44/44 通過）**
- [x] **release-pr profile hard=0**（warn 因 §11 紀律存在但符合 ≤ 3 上限）
- [x] **對位句型 88 行跨 41 篇**（< 122 上限，平均 ~2.1 / 篇）

## 🛠️ 5/7-5/8 的反思 + 紀律升級

5/8 處理 #888-#891 整合 ship 你做了這些非預期的工作：

- fetch + rebase `--strategy-option=theirs` 4 個 PR 解 frontmatter conflict
- merge --no-ff 整合進 PR #892（額外的整合 PR）
- 寫 4 個 thank-you comment 附 merge commit pointer
- review 又抓出對位句型 warn 偏高（這個 PR 處理）

謝謝你的判斷「**根因不是 contributor 的問題、不是維護者的問題，是工具不對齊**」（5/8 elegant-ptolemy diary）— 讓 5a1542f66 frontmatter formatter pre-commit hook 的根因修補有了動力。但客觀來看，我們的 maintainer 紀律確實有 gap，整理三層：

| 層 | 失誤 | 為什麼會發生 |
|---|------|------------|
| **Sync 紀律** | 4 個 PR 開出去前沒先 `git pull upstream main` | 沒有把「PR 開前 sync upstream」寫進 SOP，憑記憶操作就漏了 |
| **驗收 SOP gap** | 原本只跑 default profile（`fail_on=hard`）看 hard=0 就 commit；沒跑 release-pr profile（`fail_on=warn`）看 §11 對位句型紀律 | release-pr profile 是 maintainer review 工具，沒寫進 contributor SOP |
| **修補風格副作用** | Tier A 全做要求「反向解釋編織 ≥ 2 處」，語言學家嚴格執行但沒控制每篇對位句型密度上限 | 工單寫 ≥ 2 下限沒寫 ≤ 3 上限 |

### 下次避免的辦法（已寫進 fork 的 governance 文件）

- **AGENTS §7 PR 開前紀律**：必跑三道 — `fetch upstream` / `rebase main` / 雙 gate 自驗
- **AGENTS §5 雙 gate**：default profile (commit gate) + release-pr profile (ship gate) 都要過才算交付
- **AGENTS §4 frontmatter 規格**：對齊 5/8 5a1542f66 規範（flow array tags + CANONICAL_ORDER）
- **STANCE §11**：5/8 演進記錄入冊（含三層失誤 lessons learned + 對外身份紀律 calibration）

下次 P1 (38 篇) audit 開 PR 前會主動跑那三道 — 不會再撞同樣的 conflict 風暴讓你做手動 rebase。

## 🔗 相關 Issue

Closes part of #851 §5（古早 200 篇品質整頓）

完整 batch-200 evidence trail（在 fork 的 `maintainer-workspace` branch）：
- [`batch-200/WORK-ORDERS-polish-prose.md`](https://github.com/Zaious/taiwan-md/blob/maintainer-workspace/batch-200/WORK-ORDERS-polish-prose.md) — 巴別塔工單（含改寫策略 + 分工 + 5/9 Gate calibration）

---

⚙️ Cardinal × Zaious (Maintainer)
