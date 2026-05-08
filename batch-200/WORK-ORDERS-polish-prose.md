# P0 Polish 工單 — 對位句型 sweep + frontmatter hard 修補

> **開單者**: 樞機師（Cardinal）
> **執行者**: 巴別塔（語言學家）— Sonnet，一篇一篇改
> **建立**: 2026-05-08
> **總量**: 27 篇 polish + 4 篇 frontmatter hard 修補
> **對應**: PR #888-#891 (4 個 P0 PR) 的 follow-up，哲宇 5/8 review 點名

---

## 🟢 開工指令（直接複製跑）

```bash
cd P:/Taiwan.md/taiwan-md
git checkout polish/p0-prose-anti-pattern
git status   # 應該 clean，且 HEAD 已從乾淨 upstream main checkout
```

| 項目 | 值 |
|------|-----|
| **Branch** | `polish/p0-prose-anti-pattern`（已開好，從乾淨 main HEAD `36217dae9` checkout）|
| **Repo path** | `P:/Taiwan.md/taiwan-md` |
| **Baseline** | upstream main `36217dae9`（Cardinal 5/8 22:48 已 sync + 核對穩定）|
| **不需要做** | git pull / git fetch / 開 branch（樞機師預先準備好了）|
| **完成後不要做** | git push / gh pr create（交給 Cardinal 收尾）|

如果 branch 不存在或 baseline 跟工單清單對不上 → **停下通知 Cardinal**，不要自己 sync / rebase。

---

## 狀況說明

### 為什麼有這個工單

batch-200 P0 44 篇修補 5/8 早上透過哲宇 PR #892 整合 ship 進 main。哲宇 review 給了高度肯定（「整體執行非常紮實」「期待 P1」），但點名一個 follow-up：

> **§11 對位句型 warn 偏高**（「不是 X，而是 Y」變種太多）：
> - PR-1 王建民: 18 處
> - PR-2 Tier A: 87 處（top: 郭泓志 21 / 葉國一 16 / 紀政偏多）
> - PR-3 Tier B: ~140 處（top: 許芳宜 16 / 伍佰 15 / 張艾嘉 15）
> 
> 建議下次 P1 一起 batch heal。

樞機師重新跑 article-health 統計，實際對位句型 warn **155 處跨 41 篇**（哲宇估的 245 是含其他 §11 warn 種類）。

### 為什麼這次有這個工單（這不是偷懶）

事後復盤，責任分布是這樣：

1. **Cardinal（樞機師）的鍋**：開 P0 工單時沒寫「自檢要跑 `--profile=release-pr`」。SOP 只寫了 default profile（fail_on=hard），所以巴別塔修完看 hard=0 就 commit。AGENTS.md §5 雙自檢已升級補上（5/8 升級）
2. **upstream 機制在升級中**：
   - §11 對位句型紀律 2026-04-21 γ session 才立的（MANIFESTO §11.1）
   - article-health prose-health Tier 1 偵測規則升級中
   - `release-pr` profile (fail_on=warn) 是 maintainer review 工具，沒寫進 contributor SOP
3. **巴別塔的風格副作用**：Tier A 標準要求「反向解釋編織 ≥ 2 處」，你嚴格執行了。但「對位句型」是反向解釋的常見載體，沒控制密度上限就會堆出 5-19 處 / 篇

**所以**：這不是「你偷懶」。是 SOP 沒跟上 + upstream 紀律演化中 + 修補風格自然副作用三層疊加。下次工單開始 SOP 已對齊（AGENTS.md §5 加 release-pr profile），未來不會再撞同問題。

這次 polish 是把 5/4 §11 確立 + 5/8 SOP 升級之前的「殘留 warn」掃乾淨。

### 為什麼現在做（不等 P1）

兩個獨立工作：
- **這個工單**：純 polish 對位句型（無事實校正、無 audit、無新引用）
- **P1 audit**：38 篇新文章 audit + 修補（要 sub-agent + WebSearch）

合併會讓 PR diff 巨大（~140+ 篇），哲宇 review 累。獨立 PR 工作分工乾淨。

### 額外發現：4 篇 hard=1（frontmatter 邊界問題）

main 上有 4 篇 P0 文章現在 article-health hard=1：
- `knowledge/People/許文龍.md`
- `knowledge/People/魏德聖.md`
- `knowledge/History/史前時代與原住民.md`
- `knowledge/Technology/台灣人工智慧實驗室.md`

**錯誤**：`frontmatter `tags` 必須是 YAML array，不可為字串`

**根因**：tags 用了「block scalar + flow array」的混合格式：
```yaml
tags:
  ['科技與企業', '奇美集團', '企業家']    # ← 這格式 frontmatter-format check 認為是字串
```

正確格式（CANONICAL）：
```yaml
tags: ['科技與企業', '奇美集團', '企業家']    # ← single-line flow array
```

這是哲宇 5/8 frontmatter formatter pre-commit hook (5a1542f66) 沒覆蓋到的 edge case。順手修。

---

## 工作目標

### 主任務 A：對位句型 sweep（27 篇）

每篇對位句型 warn **降到 ≤ 3 處**（哲宇 §11 紀律 hard 上限）。

### 主任務 B：修 4 篇 frontmatter hard（順手）

把 4 篇的 tags 從 multi-line `tags:\n  [...]` 改成 single-line `tags: [...]`。

### 不做什麼

- ❌ 不改事實（這 44 篇事實校正已 ship 在 main，不再動）
- ❌ 不補新引用（footnote 已足夠）
- ❌ 不重寫結構（v5.6 anchor / 結尾 / 三明治 title 都 OK）
- ❌ 不改 5W1H metadata
- ✅ 只 reduce 對位句型 + 修 frontmatter

---

## 主任務 A：標的清單（27 篇）

按 warn 數降冪排序，每篇要 reduce 到 ≤ 3。

### Tier 重 (8 篇，warn ≥ 9)

| 篇 | 路徑 | warn | reduce 到 |
|----|------|------|----------|
| 郭泓志 | knowledge/People/郭泓志.md | 19 | ≤ 3（要砍 16+ 處）|
| 王建民 | knowledge/People/王建民.md | 16 | ≤ 3（要砍 13+ 處）|
| 葉國一 | knowledge/People/葉國一.md | 14 | ≤ 3 |
| 許芳宜 | knowledge/People/許芳宜.md | 14 | ≤ 3 |
| 伍佰 | knowledge/People/伍佰.md | 13 | ≤ 3 |
| 張艾嘉 | knowledge/People/張艾嘉.md | 13 | ≤ 3 |
| 羅大佑 | knowledge/People/羅大佑.md | 11 | ≤ 3 |
| 紀政 | knowledge/People/紀政.md | 10 | ≤ 3 |

### Tier 中 (10 篇，warn 5-9)

| 篇 | 路徑 | warn | reduce 到 |
|----|------|------|----------|
| 陳昇 | knowledge/People/陳昇.md | 10 | ≤ 3 |
| 朱天文 | knowledge/People/朱天文.md | 10 | ≤ 3 |
| 白先勇 | knowledge/People/白先勇.md | 9 | ≤ 3 |
| 鍾理和 | knowledge/People/鍾理和.md | 9 | ≤ 3 |
| 陳建仁 | knowledge/People/陳建仁.md | 8 | ≤ 3 |
| 林百里 | knowledge/People/林百里.md | 8 | ≤ 3 |
| 簡立峰 | knowledge/People/簡立峰.md | 7 | ≤ 3 |
| 張明正 | knowledge/People/張明正.md | 7 | ≤ 3 |
| 李昂 | knowledge/People/李昂.md | 7 | ≤ 3 |
| 黃春明 | knowledge/People/黃春明.md | 7 | ≤ 3 |

### Tier 輕 (9 篇，warn 4-6)

| 篇 | 路徑 | warn | reduce 到 |
|----|------|------|----------|
| 莊智淵 | knowledge/People/莊智淵.md | 6 | ≤ 3 |
| 許淑淨 | knowledge/People/許淑淨.md | 6 | ≤ 3 |
| 郭台銘 | knowledge/People/郭台銘.md | 6 | ≤ 3 |
| 鄧雨賢 | knowledge/People/鄧雨賢.md | 5 | ≤ 3 |
| 謝淑薇 | knowledge/People/謝淑薇.md | 5 | ≤ 3 |
| 楊傳廣 | knowledge/People/楊傳廣.md | 4 | ≤ 3 |
| 幾米 | knowledge/People/幾米.md | 4 | ≤ 3 |
| 明華園 | knowledge/People/明華園.md | 4 | ≤ 3 |
| 魏德聖 | knowledge/People/魏德聖.md | 4 | ≤ 3（同時修 frontmatter）|

### 已達標（14 篇，不用改）

施明德 3 / 童子賢 3 / 鄭兆村 3 / 林俊傑 3 / 劉德音 2 / 盧彥勳 2 / 張惠妹 2 / 朱經武 2 / 龍應台 2 / 魏哲家 2 / 陽岱鋼 2 / 王永慶 1 / 李宗盛 1 / 民主制度 1

---

## 主任務 B：4 篇 frontmatter hard 修補

| 篇 | 路徑 | 修法 |
|----|------|------|
| 許文龍 | knowledge/People/許文龍.md | tags: 那行下面的 flow array 移上去同一行 |
| 魏德聖 | knowledge/People/魏德聖.md | 同上 |
| 史前時代與原住民 | knowledge/History/史前時代與原住民.md | 同上 |
| 台灣人工智慧實驗室 | knowledge/Technology/台灣人工智慧實驗室.md | 同上 |

修法（範例 — 許文龍）：

**改前**：
```yaml
tags:
  ['科技與企業', '奇美集團', '企業家', '音樂藝術', '博物館', '文化推廣', '台南']
```

**改後**：
```yaml
tags: ['科技與企業', '奇美集團', '企業家', '音樂藝術', '博物館', '文化推廣', '台南']
```

---

## 改寫策略（給巴別塔）

對位句型 warn 抓的是「不是 X，而是 Y」「不只是 X，是/也是 Y」這類 pattern。

### 策略 1：直接陳述（最常用）

**改前**：「他的成功**不是**棒球文化的累積，**而是**個人天賦的單一突破。」
**改後**：「他的成功源於個人天賦的單一突破，而非建立在台灣棒球文化的厚實累積之上。」

或更直接：
**改後**：「他的成功是個人天賦的單一突破。台灣棒球文化的厚度此時還沒到位。」

### 策略 2：拆成兩段

**改前**：「2012 年倫敦銅牌戰的失利，**不是**缺席，**而是**到達了終點前最後一個路標，然後停在那裡。」
**改後**：「2012 年倫敦銅牌戰的失利，是抵達終點前最後一個路標然後停下來。他到了那裡，但沒過去。」

### 策略 3：保留少數最有力的 ≤ 3 處

每篇可以保留 2-3 處對位句型 — **挑選最關鍵的核心矛盾 anchor**（通常 description 對應的那個）保留。

例：施明德留「**幫民進黨打下江山的人，轉身發起倒扁紅衫軍**」這種對位（核心矛盾 anchor），刪其他變種。

### 不要做的

- ❌ 不要把對位句型砍光變成平淡敘述（會失去張力）
- ❌ 不要為了改而改變事實
- ❌ 不要動引用、footnote、frontmatter（除 4 篇 hard）
- ❌ 不要改 v5.6 結構（anchor / 結尾 / 三明治 title）

---

## 工作流（含分工）

### 🔵 Cardinal 預先準備（巴別塔開工前已完成）

樞機師在開單前已做完三件事，巴別塔不用碰：

1. **Sync upstream main**（核對 baseline 穩定，無新規則演化）
2. **Open branch `polish/p0-prose-anti-pattern`**（從乾淨 main checkout）
3. **Baseline 重跑驗證**（44 篇現狀已紀錄在工單清單）

巴別塔開 session 時直接 checkout 該 branch 即可：
```bash
cd P:/Taiwan.md/taiwan-md
git checkout polish/p0-prose-anti-pattern
git status   # 應該是 clean
```

如果 branch 不存在 → 通知 Cardinal（不要自己創）。

---

### 🟢 巴別塔執行（你的工作）

#### Step 1：一篇一篇 polish

對每篇（按工單清單 Tier 重 → 中 → 輕順序）：

1. 跑 `PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py knowledge/People/{篇}.md --check=prose-health`
2. 看具體 warn 位置
3. Edit 改寫對位句型（用 §「改寫策略」三招）
4. 重跑確認 warn 數 ≤ 3
5. 確認 hard=0（如果原本是 1，要修到 0）

#### Step 2：Commit 紀律

**批量 commit**（每 5 篇一個 commit）。message 格式：
```
polish(P0/prose): batch-A {篇1}/{篇2}/{篇3}/{篇4}/{篇5} — 對位句型 reduce

詳細：
- {篇1}: 19→3
- {篇2}: 14→2
- ...
```

4 篇 frontmatter hard 修補單獨 commit：
```
fix(P0/frontmatter): 4 篇 multi-line flow array → single-line (hard=1→0)

- 許文龍 / 魏德聖 / 史前時代與原住民 / 台灣人工智慧實驗室
- tags 從 block-style 改 single-line flow array
```

每個 commit 前自己跑 article-health 確認 hard=0（**不要 commit 沒過自檢的檔案**）。

#### Step 3：全部完成後跑兩道驗證

> ⚠️ **2026-05-09 calibration**（巴別塔指出原指令兩個 bug）：
> 1. **Gate 1 範圍**：用 `knowledge/People/*.md` 會掃 213 篇（含 P1/P2 未處理 169 篇），數字會看似爆炸。**只掃 44 篇 P0** 路徑才正確
> 2. **Gate 2 解讀**：release-pr profile `fail_on=warn`，任何 warn 都讓 `passed=False`。**正確 metric 是 hard=0**（不是 `grep passed=True`）

```bash
# 44 篇 P0 路徑變數（避免重複）
P0_FILES="knowledge/People/施明德.md knowledge/People/劉德音.md knowledge/People/盧彥勳.md knowledge/People/紀政.md knowledge/People/莊智淵.md knowledge/People/葉國一.md knowledge/People/郭泓志.md knowledge/People/陳昇.md knowledge/People/王永慶.md knowledge/People/楊傳廣.md knowledge/People/伍佰.md knowledge/People/張艾嘉.md knowledge/People/李宗盛.md knowledge/Society/民主制度.md knowledge/People/王建民.md knowledge/People/童子賢.md knowledge/People/簡立峰.md knowledge/People/鄭兆村.md knowledge/People/陳建仁.md knowledge/People/幾米.md knowledge/People/張惠妹.md knowledge/People/張明正.md knowledge/People/明華園.md knowledge/People/朱天文.md knowledge/People/朱經武.md knowledge/People/李昂.md knowledge/People/白先勇.md knowledge/People/羅大佑.md knowledge/People/許芳宜.md knowledge/People/鄧雨賢.md knowledge/People/鍾理和.md knowledge/People/黃春明.md knowledge/People/許淑淨.md knowledge/People/郭台銘.md knowledge/People/謝淑薇.md knowledge/People/林俊傑.md knowledge/People/林百里.md knowledge/People/許文龍.md knowledge/People/龍應台.md knowledge/People/魏哲家.md knowledge/People/魏德聖.md knowledge/People/陽岱鋼.md knowledge/History/史前時代與原住民.md knowledge/Technology/台灣人工智慧實驗室.md"

# Gate 1: 44 篇對位句型總數（修正範圍）
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py $P0_FILES 2>&1 | grep "對位句型" | wc -l

# Gate 2: 44 篇 hard=0（修正解讀 — 不看 passed=True 而看 hard 總和）
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py $P0_FILES --profile=release-pr 2>&1 | grep "Summary" | awk '{gsub(/[^0-9]/,"",$2); h+=$2} END{print "44 篇 hard 總和: " h}'
```

目標：
- **Gate 1**: 對位句型行 ≤ 122（≤ 3 × 41 篇 + 0 已達標 14 篇 + 0 frontmatter only 3 篇）。實際做完應該更低
- **Gate 2**: 44 篇 hard 總和 = **0**（含 4 篇 frontmatter hard 修完）

#### Step 4：交付給 Cardinal

跑完兩道 gate 通過後，**通知 Cardinal**（不要自己 push、不要自己開 PR）。

交付包：
- 兩道 gate 結果摘要
- 你修了哪些篇 / 哪些不動
- 任何 `<!-- TODO: Cardinal 確認 -->` comment 標的位置

---

### 🔵 Cardinal 收尾（巴別塔交付後）

樞機師在巴別塔交付後做：

1. **抽查 4-6 篇 polish 品質**（確認張力沒被砍光）
2. **跑兩道 gate 自驗**（雙保險）
3. **Push branch 到 origin**
4. **寫 PR body**（含 before/after metric + 對應原始 commits）
5. **執政官（Zaious）GitHub web UI 開 PR**

---

### 驗收門檻

- 27 篇對位句型 warn ≤ 3
- 4 篇 frontmatter hard=0
- 14 篇已達標的**不要動**
- 全 P0 44 篇 article-health default + release-pr 雙 profile 通過

---

## 預估規模

| 維度 | 估計 |
|------|------|
| 篇數 | 27 篇主任務 + 4 篇 frontmatter |
| 平均每篇砍 warn | ~5 處 |
| 總工作量 | ~135 處對位句型改寫 + 4 篇 frontmatter |
| 預估時間 | Sonnet session ~2-3 小時（純改寫不查 source 比 audit 快很多）|
| 預估 commits | 6-10 個（批量分組）|

---

## 對巴別塔的話

1. **這次不是你的鍋**。Cardinal 的工單 SOP 沒寫「自檢要跑 release-pr profile」 + upstream §11 紀律還在演化中。三層疊加讓 warn 累積。AGENTS.md §5 已升級，未來工單會明確要求兩道 gate
2. **保留最有力的 ≤ 3 處**，不要全砍 — 對位句型本身是好工具，密度才是問題
3. **改完跑兩道自檢**（這次明確要求）：
   ```bash
   # Gate 1（必過）
   PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file} --check=prose-health
   # Gate 2（必過）
   PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file} --profile=release-pr
   ```
   每篇 prose-health Tier 1 對位句型 warn ≤ 3 + 全 release-pr profile 通過才算合格
4. **哲宇對 P0 整體品質給高度肯定**（「結尾閉環收束抓得極好」「把人物從教科書條目重新拉回有血肉的當下」）— 你的修補品質沒問題，這次純粹是把 §11 殘留 warn 掃乾淨
5. **遇到改不下手的**（覺得砍了張力會掉）→ 標 `<!-- TODO: Cardinal 確認 -->` comment，我抽查時看

完成後樞機師抽 4-6 篇 review 品質，OK 就 ship PR。

---

_開單者: Cardinal（樞機師）2026-05-08_
_對應 PR #888-#891 ship 後的 follow-up，哲宇 review feedback_
