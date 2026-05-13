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

---

# 🔄 二次修補工單（樞機師 5/13 18:00 抽查後 append）

## 抽查結果

樞機師抽查 10 篇後，**7 篇需要二次修補**（70%）。原因：巴別塔修補時對「最核心 audit 標的事實」沒挑戰，補了其他遺漏 / 修了次要 fact 但 critical 結構性錯誤跳過。

## 7 篇必修清單

### 1. 方序中（最嚴重 — 6 項基礎事實全錯）

**Audit 抓到的 6 項全在文章未改**：

| 文中 | 應改 |
|------|------|
| 「1982 年生於台北」（L16/L18）| **1978 年生於屏東東港共和新村** |
| 「實踐大學媒體傳達設計系畢業」（L16/L18/L22）| **私立復興商工 + 國立臺灣藝術大學工藝設計學系金工組夜間部** |
| 「2012 年創立究方社」（L16/L24）| **2013 年（夏）成立究方社** |
| 「2014 年起連續多年為金曲獎操刀」（L16）| **2016 年由陳鎮川邀請合作第 27 屆金曲獎** |
| 「2018 年完成金馬獎品牌再造 + 馬字標誌」 | **金馬 55 主視覺概念為「配角」**（李安、侯孝賢、鞏俐、小野側臉輪廓組成山稜），與膠片/馬字標誌無關 |
| 「作品入選德國紅點設計獎與日本 Good Design Award」 | **無來源**，疑似幻覺，需驗證或拿掉 |
| L51 footnote 實踐大學「方序中校友背景」 | 改 [維基](https://zh.wikipedia.org/zh-tw/%E6%96%B9%E5%BA%8F%E4%B8%AD) + [究方社官網](https://joefangstudio.com/?page_id=2)（取代實踐大學連結）|

**參考**：[audit-results/P1/People-方序中.md](audit-results/P1/People-方序中.md)
**修補建議**：砍至骨幹從維基 + 鏡週刊重建（這篇等於要整篇 rewrite）

### 2. 兆豐金控（critical 結構性偽造身世）

**「1897 台灣銀行血脈」7 處全部要改**：

| 行 | 文中（要改）|
|----|------------|
| L3 description | 「**承襲 1897 年台灣銀行血脈**」 → 改「兆豐金控 2002 由交銀 + 中國商銀 + 倍利證券 + 中興票券四家合併而成」|
| L16 30 秒概覽 | 「**兆豐金控前身是 1897 年的台灣銀行**」 → 改「兆豐金控 2002/8/22 成立，由四家公股行庫合併」|
| L20 | 「**這棟建築的前身，正是日治時期台灣銀行的總行**」 → 重慶南路是兆豐國際商銀總部，**非台銀總行延續** |
| L22 | 「**127 年前，當日本總督府設立台灣銀行時**」 → 不適用兆豐脈絡，重寫 |
| L28-34 「三個名字，一條血脈」整段 | **整段必須重寫** — 台灣銀行（1897 至今仍獨立公股銀行）跟兆豐金控（2002）**沒血脈關係** |
| L60 「**僅次於台灣銀行**」 | 此句揭穿邏輯矛盾 — 確認兆豐 ≠ 台銀 |
| L88 結尾 | 「**從 1897 年的台灣銀行到 2024 年的兆豐金控**」 → 改「2002 至 2024 兆豐金控的二十二年」|

**保留**：L64-68 + footnote [^6] 2016 NT$57 億洗錢罰款（這部分已補上 ✅）

**參考**：[audit-results/P1/Economy-兆豐金控.md](audit-results/P1/Economy-兆豐金控.md)
**修補建議**：重寫 outline 為「2002 四行庫合併 → 2016 紐約事件 → 2020s 全球台商網路」三段式，**拋棄虛構的 1897 血脈**

### 3. 陳映真（critical 事實 + perspective）

**audit 標的 5+ 處重大事實錯，本次只修了部分**：

| 文中 | 應改 |
|------|------|
| L56「**1968 統盟案** 入獄」 | **1968 民主台灣聯盟案**（讀魯迅/馬克思被控組織顛覆）。「中國統一聯盟」是 **1988 才成立**，陳映真擔任創盟主席 — 兩個不同事件 |
| L34「〈將軍族〉**以美軍駐台為背景**，描寫一群台北青年男女圍繞著美國軍官轉」 | **〈將軍族〉劇情完全寫錯**！實寫**退伍老兵（三角臉）與雛妓（小瘦丫頭）悲劇**。可能與〈六月裡的玫瑰花〉混淆 |
| L86「他出生於鶯歌，在北京離世」（但前文 L18 寫「**1937 生於新北市鶯歌**」）| 出生地多數權威來源寫**苗栗竹南**出生後遷鶯歌成長 |
| **缺：北京 10 年（2006-2016）** | 文中一筆帶過。需補：**1988 創立中國統一聯盟並任首任主席** + **中國作協第七屆全國委員會委員（2006 當選）** + **2006 中風後遷居北京** + **2010 二度中風後長期臥床** |
| **缺：1977-78 鄉土文學論戰**（陳映真以「許南村」筆名與葉石濤分歧）|
| **缺：魯迅是決定性影響** |
| **缺：吳濁流文學獎 1979（《夜行貨車》）** |
| L4 footnote 引用 `renjian.com.tw` 真實性可疑 + `hongfan.com.tw`（洪範非陳映真主要出版社，全集在印刻）| 移除疑問引用，補印刻文學《陳映真全集》23 卷 / 趙剛《求索：陳映真的文學之路》|

**Perspective 必填**：whats_excluded 明標排除「中國大陸高規格悼念（八寶山革命公墓安葬、習近平致電）」與「台灣本土派評價複雜」雙視角

**參考**：[audit-results/P1/People-陳映真.md](audit-results/P1/People-陳映真.md)
**Frontmatter hard**：tags 換行 flow array 改 single-line（仍待修）

### 4. 中鋼（critical 事實 + 杜撰對話）

| 文中 | 應改 |
|------|------|
| L32「1972 中鋼與**美國鋼鐵公司**及顧問公司簽約」| **U.S. Steel ≠ McLouth Steel**！實際技術合作對象為**美國 McLouth Steel + C.E. Lummus**（顧問公司） |
| L28 杜撰對話「**台灣有能力操作這麼複雜的工業設備嗎？**」 | **無來源**，刪除或標明來源（可能與 audit 抓的「謝謝，我們不要了」一起是杜撰）|

**確認**：「鐵頭部長」綽號是否時序錯位（趙耀東後任經濟部長 1981-1984 才得綽號，1971 籌建中鋼時尚無此稱號）— 文中**是否仍出現「鐵頭部長」用於 1971 場景**？需檢查

**參考**：[audit-results/P1/Economy-中鋼.md](audit-results/P1/Economy-中鋼.md)

### 5. 陳俊良（春聯已改 ✅ + 其他細節未修）

**春聯→國宴餐具修對 ✅**（L38 已寫「天圓地方」系列餐具獲澳門設計雙年展評審獎）

**仍需修**：
| 文中 | 應改 |
|------|------|
| L3 description「**設計詩人**」 | 天機星已查證**此稱號可能錯掛**（更常稱「設計頑童 / 春聯設計師」），改稱「東方美學設計家」或拿掉稱號 |
| L3/L16/L26 多處「**自由落體設計教室**」 | **正式名稱「自由落體設計（Free Image Design）」非「設計教室」**。改名 |
| L49 footnote [^2] `https://www.freefalldesign.com.tw/` | **幻覺 URL**！改 `https://www.freeimage.com.tw/`（自由落體設計實際官網）|
| L50 footnote [^3] `cdesign.org.tw 設計學報` | **疑似幻覺**，移除或改為他 ref |

**參考**：[audit-results/P1/People-陳俊良.md](audit-results/P1/People-陳俊良.md)

### 6. 台泥（妹婿 vs 姊夫）

| 文中 | 應改 |
|------|------|
| L56「2017 年，辜成允的**妹婿**張安平接任董事長」 | **姊夫**（張安平妻為辜懷如/辜懷群一系，是辜成允的姊妹輩 → 張安平是辜成允姊夫，不是妹婿）|

**仍需驗**：
- 11:11 對稱杜撰是否修了？grep 沒命中可能已修
- 辜成允 2017/1/23 萬豪酒店墜樓細節是否補完整

**參考**：[audit-results/P1/Economy-台泥.md](audit-results/P1/Economy-台泥.md)

### 7. 玉山金控（identity-level 缺陷 + 年齡/職位錯）

**critical missing**：
| 文中 | 應改 |
|------|------|
| **創辦人黃永仁完全沒提名** | 必須補入：**1992 黃永仁帶領 30 位專業金融人士創行玉山銀行**（founding myth）|
| L14/L28「黃男州 2008 年以 **43 歲** 年紀成為台灣史上最年輕**金控總經理**」 | **黃男州 1962 生 2008 為 46 歲（非 43）**。**2008 接的是玉山銀行總經理**（非金控總經理）。**2022 才升金控董事長**，總經理交棒陳茂欽 |
| L75 footnote「黃男州校友接任玉山銀董座」 | 確認 2022 升董座 — 已有 ref，但 L14/L28 年齡與職位錯需修 |

**仍需驗**：
- 「中國 28 家分行」grep 沒命中可能已修
- 「玉山銀 1992 + 台灣首家專業信用卡銀行」是否仍寫成「綜合商業銀行」

**參考**：[audit-results/P1/Economy-玉山金控.md](audit-results/P1/Economy-玉山金控.md)

---

## 二次修補執行策略

| 順序 | 篇 | 預估時間 | 建議 |
|------|----|---------|------|
| 1 | **方序中**（6 項全錯）| ~30 分鐘 | 砍至骨幹從維基重建。最費工 |
| 2 | **兆豐金控**（1897 偽造身世）| ~30 分鐘 | 整篇結構性重寫前半 |
| 3 | **陳映真**（5+ 處事實 + perspective + frontmatter）| ~25 分鐘 | 含 frontmatter hard 修補 |
| 4 | **中鋼**（McLouth Steel + 杜撰對話）| ~10 分鐘 | 兩處改 |
| 5 | **陳俊良**（細節 4 處）| ~10 分鐘 | description + 公司名 + URL + footnote |
| 6 | **台泥**（妹婿→姊夫）| ~5 分鐘 | 一字之差 |
| 7 | **玉山金控**（補黃永仁 + 修黃男州 2008 職位/年齡）| ~15 分鐘 | 補一段 founding myth |

**總時長**：~2 小時

## 二次修補後驗收

每篇雙 gate 自驗（仍需通過）：
```bash
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file}
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py {file} --profile=release-pr
```

二次修補完成後 → Cardinal 抽查（重點看這 7 篇）→ ship PR

## 抽查紀錄與沒抽到的

樞機師 5/13 18:00 抽查 10 篇（席慕蓉 / 楊德昌 / 蕭青陽 / 陳映真 / 陳俊良 / 兆豐金控 / 中鋼 / 人權與性別平等 / 清治時期 / 麵包烘焙 + 額外 6 篇樣本）。

**沒抽到的（28 篇）可能還有未修的事實點**。建議：
- 巴別塔修補這 7 篇時，**順手快速 grep 自己之前的修補**對照 P1-DETAILED-FINDINGS 的每一條 ❌ 是否都在文中改了
- 遇到不確定 → 標 `<!-- TODO: 樞機師 -->` Cardinal 第二輪抽查時看

---

_Append by Cardinal（樞機師）2026-05-13 18:08_
_對應抽查結論：10 抽 7 需二次修補 = 70% rate，sample 限制下實際可能更高_
