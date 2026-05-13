# P1 修補工單 — 給巴別塔（Sonnet session）

> **開單者**: 樞機師（Cardinal）
> **執行者**: 巴別塔（語言學家）— Sonnet，一篇一篇改
> **建立**: 2026-05-13
> **總量**: **38 篇 P1**（27 Tier A 嚴重 + 10 Tier B 中度 + 1 Tier B+/A）
> **參考**: [`batch-200/audit-results/P1-DETAILED-FINDINGS.md`](audit-results/P1-DETAILED-FINDINGS.md) + `audit-results/P1/{Category}-{slug}.md` 38 個單篇

---

## 🟢 開工指令（直接複製跑）

```bash
cd P:/Taiwan.md/taiwan-md
git checkout fix/batch-200-P1-batch-1
git status   # 應該 clean，HEAD 已從 upstream main checkout
```

| 項目 | 值 |
|------|-----|
| **Branch** | `fix/batch-200-P1-batch-1`（已開好，從乾淨 upstream main checkout）|
| **Baseline** | upstream main 5/13 07:48 sync 後 + Cardinal 5/13 開 branch |
| **不需要做** | git pull / 開 branch（樞機師預備好了）|
| **完成後不要做** | git push / gh pr create（交給 Cardinal 收尾）|

---

## ⚠️ 開工前必讀（從 P0 經驗學到的紀律）

### 1. P1 比 P0 嚴重得多

| 維度 | P0 | P1 |
|------|----|----|
| Tier A 嚴重 | 25% (10/44) | **71% (27/38)** |
| 修補性質 | 「保留基底 + 補引用 + 移幻覺」 | 多篇**需要 rewrite 骨幹**（不只是補引用）|
| 平均修補工作量 | ~10-15 分鐘/篇 | **預估 15-25 分鐘/篇** |
| 預估總時長 | 4 小時 | **7-10 小時** |

### 2. 三類特殊處理

| 類型 | 處理紀律 |
|------|---------|
| **5/8 voice polished 4 篇**（席慕蓉 / 楊德昌 / 蕭青陽 / 陳映真）| 補事實 + 補引用，**不重做 voice polish**（避免破壞 5/8 已做的 anchor）|
| **鄭南榕（inventory 5/13 補入）**| 已 5/8 polish。本次補 perspective 平衡 + 葉菊蘭職銜 + 微調 prose（~30 分鐘升 A）|
| **3 篇 frontmatter hard=1** | 陳映真 + 楊右任 + 客家音樂 — tags 換行 flow array → single-line |

### 3. 雙 gate 自檢（AGENTS.md §5 升級）

每篇 commit 前必跑：
```bash
# Gate 1: default profile (commit gate)
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file}

# Gate 2: release-pr profile (ship gate)
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file} --profile=release-pr
```

- Gate 1 hard=0 必過才 commit
- Gate 2 對位句型 ≤ 3 / 篇（§11 紀律）— **修補時主動控制密度**，不要累積到 polish 階段才 sweep

---

## 工作原則

1. **修事實為主** — P1 大多是事實層面結構性錯（多重幻覺），不是 voice 問題
2. **引用為先** — Cardinal 已在 P1-DETAILED-FINDINGS 提供每篇 3-7 個引用候選 URL，**自己 WebSearch 驗證後使用**
3. **遇到不確定 → 標 `<!-- TODO: 天機星深度查證 -->` comment**，Cardinal 抽查時看
4. **每篇改完跑雙 gate** — Gate 1 + Gate 2 都過才能 commit
5. **frontmatter 修正** — author 統一 `'Taiwan.md Contributors'`（5/8 PR template 紀律）+ tags 用 single-line flow array
6. **title 改三明治結構** —「{篇名}：{核心張力一句話}」≤ 30 字
7. **description 擴到 120-160 字** — 具體 scene + 軌跡 + 核心矛盾
8. **整合 issue #851 框架**：
   - **#2 perspective check**：高 stake 文（People 政治/Society/History）whats_excluded 必填
   - **#3 5W1H metadata**：每篇順帶填 (why_this_hook + whats_excluded + where_it_hedges)
   - **#5 Hard Gate**：article-health hard=0

---

## 🔭 27 個天機星查證點 — 修補時的紀律

Cardinal 在 P1-DETAILED-FINDINGS 列了 27 個建議天機星補驗的事實點。**這次的工作方式**：

- 巴別塔修補時，**用 WebSearch 直接驗證** Cardinal 提供的引用候選 URL
- 遇到**高敏感點**（譬如長春石化「廖頂立」「林書鴻」、兆豐金控 1897 vs 2002 血脈、陳映真〈將軍族〉劇情）→ 至少**三源確認**（維基 + 一手官網 + 權威媒體）才下筆
- 遇到**搜尋仍不確定** → 標 `<!-- TODO: 天機星 -->` comment 留位置，**不硬寫**
- Cardinal 抽查時會集中查 TODO comment

---

## 分級總覽

### Tier A 嚴重（27 篇）— 多重幻覺 + 重大遺漏 + perspective 失衡

#### People（11 篇）

| # | 篇 | 路徑 | 重點修補（詳見 audit-results/P1/）|
|---|----|------|------------|
| A1 | 席慕蓉 | knowledge/People/席慕蓉.md | 留學魯汶大學→**布魯塞爾皇家藝術學院** / 父母蒙古族真相 / 2017 金唱片獎 / 2019《我給記憶命名》|
| A2 | 方序中 | knowledge/People/方序中.md | 6 項基礎事實全錯（生年地/學歷/究方社年/金曲合作年/金馬 55 概念）|
| A3 | 林義雄 | knowledge/People/林義雄.md | 1977 省議員（非縣議員）/ 1998 主席（非 1989）/ **2006 退民進黨重大遺漏** / perspective bias |
| A4 | 楊德昌 | knowledge/People/楊德昌.md | 生日 11/6（非 11/14）/ 補南加大電影學院 / 2023 北美館回顧展 / 追風遺作 |
| A5 | 蕭青陽 | knowledge/People/蕭青陽.md | 5/5 claim 全錯 + akibo.com.tw 張冠李戴李明道 + **2023 第 65 屆葛萊美得獎遺漏** |
| A6 | 蔡明亮 | knowledge/People/蔡明亮.md | 拉夫·迪亞茲/貝拉·塔爾因果反向錯 / 國家文藝獎 2014 缺 / 2020 後新作《何處》《無所住》缺 |
| A7 | 賴聲川 | knowledge/People/賴聲川.md | 烏鎮戲劇節聯合創始人 2013 缺 / 國家文藝獎年份錯 / 多作品年份錯 |
| A8 | 楊右任 | knowledge/People/楊右任.md | 書名《失控》查無 + 數字自相矛盾 + H3 模板殘留 / frontmatter hard |
| A9 | 陳俊良 | knowledge/People/陳俊良.md | **總統府春聯 2017-2024 完全缺** + freefalldesign.com.tw 幻覺域名 + 設計詩人疑錯掛 |
| A10 | 陳映真 | knowledge/People/陳映真.md | **〈將軍族〉劇情錯 + 統盟案 1968 vs 1988 誤植 + 統派立場缺 + 北京 10 年缺** / frontmatter hard |
| A11 | 黃震南 | knowledge/People/黃震南.md | 12 項可疑 / 800 字 + brief vs 內文打架 + **Semiont 自指涉滲入** |

#### Economy（5 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A13 | 中鋼 | knowledge/Economy/台灣企業：中鋼.md | 鐵頭部長時序錯 / **U.S. Steel vs McLouth Steel** / 杜撰對話 / 現任管理層缺 |
| A14 | 兆豐金控 | knowledge/Economy/台灣企業：兆豐金控.md | **1897 台灣銀行偽造身世** + **2016 NT$57 億洗錢罰款全篇 0 字** |
| A15 | 台泥 | knowledge/Economy/台灣企業：台泥.md | **11:11 對稱杜撰** + 妹婿 vs 姊夫 + 辜家爭產缺 + NHOA/能元缺 |
| A16 | 玉山金控 | knowledge/Economy/台灣企業：玉山金控.md | **創辦人黃永仁完全沒提** + 中國 28 家分行嚴重不符 |
| A17 | 長春石化 | knowledge/Economy/台灣企業：長春石化.md | **創辦人「廖頂立」可能是幻覺人物** + **林書鴻 2024 仍在世**（文中寫過世）+ PVA 全球第一隱形冠軍缺 |

#### Society（2 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A18 | 人權與性別平等 | knowledge/Society/人權與性別平等.md | **《人權保障基本法》幻覺** + **2018 公投 765 萬反方完全消失** + 兩公約 + CEDAW + 釋字 791 全缺 |
| A19 | 國際標示 | knowledge/Society/台灣在國際標準中的標示問題.md | 題不對文（80% 寫 bug）+ 2758 決議完全缺 + perspective 失衡 |

#### History（2 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A20 | 日治時期 | knowledge/History/日治時期.md | 蔣渭水 / 林獻堂 / 八田與一全缺 + 議會請願 + 治警事件 + 西來庵 + 「日治 vs 日據」用詞 |
| A21 | 清治時期 | knowledge/History/清治時期.md | 施琅 / 沈葆楨 / 唐景崧 0 字 + 與延伸閱讀自我矛盾 + 「清治 vs 清領」用詞 |

#### Music（1 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A22 | 電子音樂與派對文化 | knowledge/Music/台灣電子音樂與派對文化.md | Taicoclub Records 誤植（日本千葉非台灣）+ Dizzy Dizzo 身份錯置 + Korner/Pawnshop/林強完全缺 |

#### Food（2 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A23 | 冰品文化 | knowledge/Food/台灣冰品文化.md | **參考資料 6 條全捏造**（黃智慧 / 蔡珠兒書名等）+ 雪花冰輸出韓國結構性錯 |
| A24 | 麵包與烘焙 | knowledge/Food/台灣麵包與烘焙.md | **吳寶春賽事名稱錯**（Coupe du Monde vs Mondial du Pain）+ 三世界冠軍全缺（武子靖 2015 / 陳耀訓 2017 / 王鵬傑 2022）|

#### Culture（1 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A25 | 街頭藝術與塗鴉 | knowledge/Culture/台灣街頭藝術與塗鴉文化.md | **黃永福 vs 黃永阜** + 彩虹村**霧峰 vs 南屯** + 4 位代表藝術家全缺（BBROTHER/ANO/Candy Bird/ECB）|

#### Lifestyle（1 篇）

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| A26 | 夜生活與KTV文化 | knowledge/Lifestyle/夜生活與KTV文化.md | **2020 錢櫃林森北大火 5 死完全沒提** + 條通在東區（實際中山區）+ 誠品全球第一書店錯 + 3 處假引文 |

### Tier B 中度（10 篇）— 1-2 個幻覺 + 補引用 + 修近況

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| B1 | 鄭南榕（補入） | knowledge/People/鄭南榕.md | 0 hard hallucination + 補 perspective 平衡 1 段 + 改「施暴者」用詞 + 葉菊蘭職銜 / **預估 30 分鐘** |
| B2 | 奇美實業 | knowledge/Economy/台灣企業：奇美實業.md | 許文龍 2023 過世接班補 + 奇美電子 2010 合併群創補 / 時態錯位修 |
| B3 | 瑞昱半導體 | knowledge/Economy/台灣企業：瑞昱半導體.md | 2024 營收 800→1,150 億 / 現任董事長邱順建 / 1998 上市代號 2379 |
| B4 | 政治環境 | knowledge/Society/台灣政治環境與選舉制度.md | 補 2024 大選後動態整段（賴清德 / 韓國瑜院長 / 大法官 7 人否決 / 大罷免潮）|
| B5 | 客家音樂 | knowledge/Music/台灣客家音樂.md | 金曲獎時序錯（2007→2003）+ **林生祥拒獎事件補** + 謝宇威補 / frontmatter hard |
| B6 | 眷村菜 | knowledge/Food/台灣眷村菜.md | 參考資料（毛奇/焦桐書名）核實 + 補族群雙向視角 + 補眷村園區名單 |
| B7 | 當代藝術 | knowledge/Art/當代藝術.md | **臺南國家美術館 2026/1 一手公文驗** + 袁廣鳴 2024 威尼斯補 + 商業藝廊補 |
| B8 | 攝影 | knowledge/Art/台灣攝影.md | NCPI 開幕年份 2019→2021 + **攝影三劍客**（鄧南光/張才/李鳴鵰）補 + 張乾琦補 |
| B9 | 特有種 | knowledge/Nature/特有種.md | **黑長尾雉 = 帝雉**修同物種錯 + 寬尾鳳蝶非世界最大 + 機構名（林務局→林業署）|
| B9' | 穿山甲 | knowledge/Nature/台灣穿山甲.md | CITES 2016 vs 2017 + 4 種 CR vs 3 種 CR + 220 萬螞蟻跨種挪用 + 補孫敬閔 |
| B10 | 廟會 | knowledge/Culture/台灣廟會與陣頭文化.md | 西來庵 vs 皇民化因果修 + 補白沙屯對照 + 四大慶典簡表 |
| B11 | 國家公園 | knowledge/Nature/台灣國家公園.md | **壽山 2011 而非 2024** + 補 2023 國公署成立 + 補 2024/4/3 太魯閣地震 |

### Tier B+ 接近 A 級（1 篇）— 微調升 A

| # | 篇 | 路徑 | 重點修補 |
|---|----|------|------------|
| C1 | 水彩畫百年流變 | knowledge/Art/台灣水彩畫的百年流變.md | 補鹽月桃甫（日治四大師缺一）+ 臺陽美協 1934 + 修 typo「証→證」+ 核 1971 引用 |

---

## 每篇工單格式（巴別塔用）

```markdown
### 工單 {#}: {篇名}

**檔案**: `knowledge/{Category}/{篇名}.md`
**Tier**: A / B / B+
**Audit 原檔**: `batch-200/audit-results/P1/{Category}-{slug}.md`

#### 修正項（❌ → 改成什麼）
1. [原文句子] → [正確事實] — Source: [URL]
（從 audit-results/P1/{slug}.md 複製，照表逐項改）

#### 補引用（0 fn → 目標 ≥ N）
- 引用候選 URL 清單（從 audit findings 複製）
- WebSearch 驗證 URL 還活 + 內容對應 claim
- 原文中加 `[^N]` footnote 的位置

#### 遺漏補充
- [近況/過世/退休/重大事件] — Source: [URL]

#### title 三明治 + description
- title 從原版 →「{篇名}：{核心張力一句話}」≤ 30 字
- description 擴到 120-160 字（具體 scene + 軌跡 + 核心矛盾）

#### 5W1H metadata（issue #851 §3）
- why_this_hook / whats_excluded / where_it_hedges 完整
- 高 stake People/Society/History：whats_excluded 必填

#### v5.6 結構紀律（分層）
| Tier | 做什麼 |
|------|--------|
| **A 嚴重** | **全做**：核心矛盾 anchor 貫穿 / 反向解釋編織 / 結尾閉環 / People 文直引 ≥ 3 / 對位句型 ≤ 3 / 篇 |
| **B 中度** | **做 anchor + 結尾**：找出核心矛盾 + 結尾改善 + 對位句型 ≤ 3 |
| **B+ 接近 A** | **微調補強**：補缺失要素 + 微改 prose |

#### frontmatter 修正
- `author: 'Taiwan.md Contributors'`（5/8 PR template 紀律）
- `tags: ['標籤1', '標籤2']` flow array single-line
- 3 篇 hard=1（陳映真/楊右任/客家音樂）：手動改 `tags:` 換行 → single-line

#### 雙 gate 自檢（巴別塔開工守則）
```bash
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file}
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file} --profile=release-pr
```
- Gate 1 hard=0 必過才 commit
- Gate 2 prose-health 對位句型 ≤ 3 / 篇

#### 不確定就標 TODO
- 遇到事實層面不確定 → `<!-- TODO: 天機星深度查證 -->` comment
- Cardinal 抽查時看
```

---

## 執行策略

### 推薦修補順序（由易到難）

| 批次 | 內容 | 篇數 | 建議節奏 |
|------|------|------|---------|
| **batch 1** | Tier B+ 水彩畫 + Tier B 簡單者（鄭南榕 / 客家音樂 / 廟會）| 4 | 暖身，快速順手 |
| **batch 2** | Tier B 其餘（奇美 / 瑞昱 / 攝影 / 穿山甲 / 特有種 / 國家公園 / 眷村菜 / 當代藝術 / 政治環境）| 9 | 中段穩定 |
| **batch 3** | Tier A People 補引用容易者（席慕蓉 / 楊德昌 / 蕭青陽 / 蔡明亮 / 黃震南）| 5 | 5/8 polished 過 3 篇 + 黃震南 |
| **batch 4** | Tier A People 高 stake（林義雄 / 陳映真 / 賴聲川 / 方序中 / 陳俊良 / 楊右任）| 6 | perspective 敏感 + 大改寫 |
| **batch 5** | Tier A Economy（中鋼 / 兆豐 / 台泥 / 玉山 / 長春石化）| 5 | 企業類 5 篇 |
| **batch 6** | Tier A Society + History + Music + Food + Culture + Lifestyle | 9 | 議題類 + 主題類雜項 |

每批完成 → Cardinal review → commit batch → 下一批

### 預估時間

- 平均每篇 15-25 分鐘（比 P0 久，因為 Tier A 比例高）
- 38 篇 × 平均 20 分鐘 = **~13 小時工作量**
- 建議**分多個 session** 完成

---

## 對巴別塔的話

1. **這次比 P0 嚴重 — 不要慌**：71% Tier A 是 audit 抓出的，巴別塔修補時要有心理準備
2. **天機星可能還會補驗**：Cardinal 在 P1-DETAILED-FINDINGS 列了 27 個高必證點 — 修補時遇到不確定的，**標 TODO，別硬寫**
3. **特別注意 5/8 polished 4 篇**：席慕蓉 / 楊德昌 / 蕭青陽 / 陳映真 — **不要重做 voice polish**，5/8 已經做完 anchor，這次只補事實 + 引用
4. **鄭南榕簡單**：30 分鐘升 A，先做暖身
5. **每篇修完跑雙 gate 才 commit**：default + release-pr 都過
6. **不確定就標 TODO**：Cardinal 會幫忙處理高敏感點

完成後樞機師抽 6-8 篇 Tier A review 品質，OK 就 ship PR。

---

## ✅ 驗收標準（巴別塔交付前）

全 38 篇必過：
- ✅ article-health **default profile hard=0**
- ✅ article-health **release-pr profile**（warn 可有但對位句型 ≤ 3 / 篇）
- ✅ 每篇 ≥ 5 footnote（People / Economy / Society / History 高 stake 類 ≥ 7）
- ✅ Perspective Y 17 篇：whats_excluded 必填
- ✅ Frontmatter formatter 符合 5/8 規範（flow array tags + author 'Taiwan.md Contributors'）
- ✅ 3 篇 frontmatter hard 修完（陳映真 / 楊右任 / 客家音樂）

---

## 🔗 紀律參考

- **PROJECT-STANCE.md §7** (紅線 12-14)：對外身份紀律（⚙️ 不用 🧬 / ChronicleCore 不用 A1 / 不提工作成本）
- **PROJECT-STANCE.md §11** (5/8 演進)：含對位句型 calibration
- **AGENTS.md §4**：Frontmatter 規格（flow array tags + CANONICAL_ORDER）
- **AGENTS.md §5**：雙 gate 自驗（default + release-pr）
- **AGENTS.md §7**：PR 開前必跑三道（巴別塔不需要做，Cardinal 收尾做）
- **batch-200/AUDIT_PROMPT-P1.md**：audit prompt 範本（供參考）
- **batch-200/audit-results/P1-DETAILED-FINDINGS.md**：38 篇完整 audit 彙整 + 27 天機星查證點

---

_開單者: Cardinal（樞機師）2026-05-13_
_對應 batch-200/README.md SSOT v4 + WORK-PLAN-P1.md + P1-DETAILED-FINDINGS.md_
_前一批: P0 44 篇 ship 完成（PR #888-#891 + #892 整合 + #910 polish）_
