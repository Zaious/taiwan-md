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

## ⚠️ 二次修補新紀律（5/13 SOP 升級）

從第一輪修補的失敗根因（70% critical 漏修）導出以下強制流程：

### 紀律 1：每條 audit ❌ 必須 grep verification

修補每篇時，**對每條 audit ❌→改 Y**，跑：
```bash
grep "原版本字串" knowledge/{Category}/篇.md  # 不該命中
grep "新版本字串" knowledge/{Category}/篇.md  # 應該命中
```
**兩個 grep 都符合預期才算修對**。憑記憶/憑感覺修補 → 70% 漏率，這次絕對不再犯。

### 紀律 2：交付前每篇強制 per-article fix log

巴別塔交付這 7 篇時，必須附 fix log。每條 audit ❌ 都要有狀態：

| 狀態 | 意思 | 必填欄位 |
|------|------|---------|
| ✅ **修了** | 改成新版本 | Grep 驗證證據 |
| ❌ **跳過** | 評估後決定不改 | **必填理由**（不可隱瞞）|
| ⚠️ **TODO** | 查不到/不確定 | 留 `<!-- TODO: 樞機師 -->` comment |

**Cardinal 用 fix log 直接反查**，不再 random 抽。系統性 verification。

### 紀律 3：addition vs replacement 工單明標

下面 7 篇每條都標 **[REPLACE]**（要刪/改原文）或 **[ADD]**（純補充）。**[REPLACE] 是最容易漏的紀律盲區**，這次嚴格做。

---

## 7 篇必修清單（含 grep checklist）

### 1. 方序中（最嚴重 — 6 項基礎事實全錯）

**檔案**: `knowledge/People/方序中.md`
**Audit**: [audit-results/P1/People-方序中.md](audit-results/P1/People-方序中.md)
**第一輪修補**: ❌ 6 項全沒改任何一個

#### Audit ❌ → 改成 Y 全清單（含 grep verification）

| # | 操作類型 | 原文中 | 應改成 | Grep verification |
|---|---------|-------|--------|-------------------|
| 1 | **[REPLACE]** | 「1982 年生於台北」(L16/L18) | **「1978 年生於屏東東港共和新村」** | `grep "1982" 不該命中` + `grep "屏東東港" 應命中` |
| 2 | **[REPLACE]** | 「實踐大學媒體傳達設計系畢業」(L16/L18/L22) | **「私立復興商工 + 國立臺灣藝術大學工藝設計學系金工組夜間部」** | `grep "實踐大學" 不該命中` + `grep "復興商工" 應命中` |
| 3 | **[REPLACE]** | 「2012 年創立究方社」(L16/L24) | **「2013 年（夏）成立究方社」** | `grep -c "2012 年" 從 N→0` + `grep "2013 年" 應命中` |
| 4 | **[REPLACE]** | 「2014 年起連續多年為金曲獎操刀」(L16) | **「2016 年由陳鎮川邀請合作第 27 屆金曲獎」** | `grep "2014 年" + 金曲 不該共現` + `grep "陳鎮川" 應命中` |
| 5 | **[REPLACE]** | 「2018 年完成金馬獎品牌再造，以電影膠片為靈感設計『馬』字標誌」 | **「2018 年操刀金馬 55 主視覺，概念為『配角』 — 李安、侯孝賢、鞏俐、小野側臉輪廓組成山稜」** | `grep "馬字標誌" OR "膠片" 不該命中` + `grep "配角" OR "山稜" 應命中` |
| 6 | **[REPLACE 或標 ⚠️ TODO]** | 「作品入選德國紅點設計獎與日本 Good Design Award」 | **若搜不到一手來源** → 拿掉/改「曾入圍多項設計獎項」 OR 標 TODO | `grep "紅點" OR "Good Design"` — 改完後若仍命中需確認有 source |
| 7 | **[REPLACE footnote]** | L51 footnote 連結 `https://www.usc.edu.tw/design/`（實踐大學）| 改 `[維基](https://zh.wikipedia.org/zh-tw/%E6%96%B9%E5%BA%8F%E4%B8%AD)` + `[究方社官網](https://joefangstudio.com/?page_id=2)` | `grep "usc.edu.tw" 不該命中` + `grep "joefangstudio.com" 應命中` |

**Cardinal 註**：這 6 項全錯 = 等於要 rewrite 整篇 description + 開頭兩段。**砍至骨幹從維基 + 鏡週刊重建**。
**參考來源**：
- [方序中 — 維基](https://zh.wikipedia.org/zh-tw/%E6%96%B9%E5%BA%8F%E4%B8%AD)
- [究方社官網](https://joefangstudio.com/?page_id=2)
- [鏡週刊三金深度報導](https://www.mirrormedia.mg/story/20190125insight001/)
- [金馬獎官方：方序中再度操刀金馬 55 主視覺](https://www.goldenhorse.org.tw/news/detail/1006)

### 2. 兆豐金控（critical 結構性偽造身世）

**檔案**: `knowledge/Economy/台灣企業：兆豐金控.md`
**Audit**: [audit-results/P1/Economy-兆豐金控.md](audit-results/P1/Economy-兆豐金控.md)
**第一輪修補**: ⚠️ 補了 2016 罰款（add ✅），但 1897 偽造身世（replace）整段沒挑戰

#### Audit ❌ → 改成 Y 全清單（含 grep verification）

| # | 操作類型 | 文中 | 應改 | Grep verification |
|---|---------|------|------|-------------------|
| 1 | **[REPLACE]** | L3 description「承襲 **1897 年台灣銀行血脈**」 | **「兆豐金控 2002 年由四家公股行庫合併而成」** | `grep "1897 年台灣銀行血脈"` 不該命中 |
| 2 | **[REPLACE]** | L16 30 秒概覽「兆豐金控**前身是 1897 年的台灣銀行**」 | **「兆豐金控 2002/8/22 成立，由交銀 + 中國商銀 + 倍利證券 + 中興票券四家合併」** | `grep "前身是 1897"` 不該命中 + `grep "倍利證券"` + `grep "中興票券"` 應命中 |
| 3 | **[REPLACE]** | L20「這棟建築的前身，正是**日治時期台灣銀行的總行**」 | 重慶南路是兆豐國際商銀總部，**非台銀總行延續**。改成「兆豐國際商銀總部位於重慶南路」 | `grep "台灣銀行的總行"` 不該命中 |
| 4 | **[REPLACE]** | L22「**127 年前，當日本總督府設立台灣銀行時**」 | 整句刪除，重寫脈絡為「2002 由四家公股行庫合併」 | `grep "127 年前.*日本總督府"` 不該命中 |
| 5 | **[REPLACE 整段]** | L28-34「三個名字，一條血脈」整段 | **整段重寫** — 台灣銀行至今仍是獨立公股銀行，跟兆豐金控 2002 合併**沒血脈關係**。改寫成「兆豐金控成員行的歷史」(交銀 1907 北京/中國商銀 1971 重組/倍利證券/中興票券)，**不可寫成「台灣銀行 → 兆豐」血脈** | `grep "一條血脈"` 不該命中 + 段內不該再有「兆豐前身是台灣銀行」claim |
| 6 | **[REPLACE]** | L60「資產規模...**僅次於台灣銀行**」 | 此句揭穿 L28 偽造邏輯（前後矛盾）。保留「僅次於台灣銀行」（這是事實），同時前文「兆豐前身是台銀」必須拿掉 | 修對後 grep 「僅次於台灣銀行」 應仍命中（這是 OK），同時 L28 沒有「兆豐前身是台銀」 |
| 7 | **[REPLACE]** | L88 結尾「**從 1897 年的台灣銀行到 2024 年的兆豐金控，127 年的金融歷史**」 | 「2002 年至 2024 年兆豐金控的二十二年金融服務」或類似 | `grep "127 年的金融"` 不該命中 + `grep "從 1897"` 不該命中 |

**[保留 ✅ 第一輪已對的]**：L64-68 + footnote [^6] 2016 NT$57 億洗錢罰款段不要動

**Cardinal 註**：第一輪 add 對了（2016 罰款），但這次必須做 [REPLACE] 動作。**「1897 台銀血脈」是 audit 的最大發現**，不能跳過。
**重寫 outline 建議**：「2002 四行庫合併（含成員行歷史）→ 2016 紐約 NT$57 億罰款 → 2020s 全球台商網路」三段式

### 3. 陳映真（critical 事實 + perspective）

**檔案**: `knowledge/People/陳映真.md`
**Audit**: [audit-results/P1/People-陳映真.md](audit-results/P1/People-陳映真.md)
**第一輪修補**: ⚠️ 補了部分 fact，但 5+ critical 結構性錯沒修

#### Audit ❌ → 改成 Y 全清單

| # | 操作 | 文中 | 應改 | Grep verification |
|---|------|------|------|-------------------|
| 1 | **[REPLACE]** | L56「1968 涉及『**統盟案**』被捕」 | **「1968 涉及『民主台灣聯盟案』被捕」**（讀魯迅/馬克思被控組織顛覆）。「中國統一聯盟」是 1988 創立的另一個組織 | `grep "統盟案"` 不該命中 + `grep "民主台灣聯盟案"` 應命中 |
| 2 | **[REPLACE]** | L34〈將軍族〉「**以美軍駐台為背景，描寫一群台北青年男女圍繞著美國軍官轉**」 | **〈將軍族〉實寫退伍老兵（三角臉）與雛妓（小瘦丫頭）的悲劇**。整段重寫劇情敘述 | `grep "美軍駐台.*將軍族" OR "美國軍官"` 不該命中 + `grep "三角臉" OR "小瘦丫頭" OR "退伍老兵"` 應命中 |
| 3 | **[REPLACE]** | 出生地「1937 生於**新北市鶯歌**」 | 多數權威來源寫**苗栗竹南**出生後遷鶯歌成長 | `grep "鶯歌"` 命中可降（除非寫成長地）+ `grep "苗栗竹南"` 應命中 |
| 4 | **[ADD]** | 北京 10 年（2006-2016）一筆帶過 | **補：1988 創立中國統一聯盟並任首任主席 + 中國作協第七屆全國委員會委員（2006 當選）+ 2006 中風後遷居北京 + 2010 二度中風後長期臥床** | `grep "中國統一聯盟"` 應命中 + `grep "中國作協"` 應命中 + `grep "2006.*北京"` 應命中 |
| 5 | **[ADD]** | 1977-78 鄉土文學論戰缺 | **補：陳映真以「許南村」筆名介入論戰，與葉石濤就「台灣意識 vs 中國意識」分歧** | `grep "許南村"` 應命中 + `grep "葉石濤"` 應命中 |
| 6 | **[ADD]** | 魯迅影響缺 | **補：除俄國文學外，魯迅是決定性影響** | `grep "魯迅"` 應命中 |
| 7 | **[ADD]** | 獎項：吳濁流文學獎 1979 缺 | **補：1979 吳濁流文學獎《夜行貨車》+ 花蹤世界華文文學獎 2009** | `grep "吳濁流文學獎"` 應命中 |
| 8 | **[REPLACE footnote]** | `renjian.com.tw` + `hongfan.com.tw` 真實性可疑 | 移除，補印刻文學《陳映真全集》23 卷（2017）+ 趙剛《求索：陳映真的文學之路》（聯經 2011）— 統派視角學術 | `grep "renjian.com.tw"` 不該命中 + `grep "印刻"` 應命中 |
| 9 | **[ADD perspective]** | whats_excluded 5W1H metadata | **必填**：排除「中國大陸高規格悼念（八寶山革命公墓安葬、習近平致電）」與「台灣本土派評價複雜」雙視角 | grep frontmatter `whats_excluded` 應有上述內容 |
| 10 | **[REPLACE frontmatter]** | tags 換行 flow array | **單行 flow array** `tags: ['標籤1', '標籤2', ...]` | 跑 Gate 1 hard=0 (frontmatter-format 必過) |

**Cardinal 註**：陳映真是兩岸高度爭議人物，**perspective 失衡是 audit 抓到的核心**。第一輪沒做 [REPLACE 將軍族劇情] 是最 critical 的漏修。

### 4. 中鋼（critical 事實 + 杜撰對話）

**檔案**: `knowledge/Economy/台灣企業：中鋼.md`
**Audit**: [audit-results/P1/Economy-中鋼.md](audit-results/P1/Economy-中鋼.md)

#### Audit ❌ → 改成 Y 清單

| # | 操作 | 文中 | 應改 | Grep verification |
|---|------|------|------|-------------------|
| 1 | **[REPLACE]** | L32「1972 中鋼與**美國鋼鐵公司**及顧問公司簽約」 | **「1972 中鋼與美國 McLouth Steel 簽訂技術合作協議，並聘 C.E. Lummus 顧問公司」** | `grep "美國鋼鐵公司"` 不該命中 + `grep "McLouth"` 應命中 |
| 2 | **[REPLACE / DELETE]** | L28 杜撰對話「**台灣有能力操作這麼複雜的工業設備嗎？**」 | **無 source，刪除整段對話**。改成中性敘述「美國鋼鐵業對台灣方案最初保持懷疑」 | `grep "台灣有能力操作這麼複雜"` 不該命中 |
| 3 | **[CHECK]** | 趙耀東「鐵頭部長」綽號用於 1971 場景 | **時序錯位** — 綽號來自後任經濟部長（1981-1984）。1971 籌建中鋼時尚無此稱號 | `grep "鐵頭部長"` 命中後**檢查上下文**：若指 1971 中鋼籌建期間 → 改「趙耀東」即可，**綽號保留給後文 1981 部長段** |

**[保留 ✅]**：補上的 2024 後管理層 / 子公司 / 環保爭議（如有）

**Cardinal 註**：兩個 [REPLACE] 都是「砍除幻覺對話 + 換正確技術夥伴名」— 工作量小但漏了影響全篇可信度。

### 5. 陳俊良（春聯已改 ✅ + 其他細節未修）

**檔案**: `knowledge/People/陳俊良.md`
**Audit**: [audit-results/P1/People-陳俊良.md](audit-results/P1/People-陳俊良.md)
**第一輪修補**: ✅ 春聯→國宴餐具修對 (L38)，但 description + footnote 仍幻覺

#### Audit ❌ → 改成 Y 清單

| # | 操作 | 文中 | 應改 | Grep verification |
|---|------|------|------|-------------------|
| 1 | **[REPLACE]** | L3 description「**設計詩人**」 | 天機星已查證**疑錯掛**。改成「東方美學設計家」或拿掉「設計詩人」稱號 | `grep "設計詩人"` 命中數應降低（保留若有 source 引用，否則拿掉）|
| 2 | **[REPLACE]** | L3/L14/L16/L26 多處「**自由落體設計教室**」 | **正式名稱「自由落體設計 (Free Image Design)」非「設計教室」** | `grep "自由落體設計教室"` 不該命中 + `grep "自由落體設計"` 應命中 |
| 3 | **[REPLACE footnote]** | L49 footnote [^2] `https://www.freefalldesign.com.tw/` | **幻覺 URL**！改 `https://www.freeimage.com.tw/`（一手官網）| `grep "freefalldesign"` 不該命中 + `grep "freeimage.com.tw"` 應命中 |
| 4 | **[REPLACE footnote]** | L50 footnote [^3] `cdesign.org.tw 設計學報` | 疑似幻覺，移除改為其他 ref（例如 Shopping Design 或 La Vie 媒體報導）| `grep "cdesign.org.tw"` 不該命中 |
| 5 | **[CHECK]** | L48 footnote [^1] `https://www.tdc.org.tw/` | 台灣設計館實際為 `tdri.org.tw`。但 tdc 是台灣設計師連線，**不是台灣設計館典藏資料庫** | `grep "tdc.org.tw"` 改成 `tdri.org.tw` 或拿掉 |

### 6. 台泥（妹婿 vs 姊夫）

**檔案**: `knowledge/Economy/台灣企業：台泥.md`
**Audit**: [audit-results/P1/Economy-台泥.md](audit-results/P1/Economy-台泥.md)

#### Audit ❌ → 改成 Y 清單

| # | 操作 | 文中 | 應改 | Grep verification |
|---|------|------|------|-------------------|
| 1 | **[REPLACE]** | L56「2017 年，辜成允的**妹婿**張安平接任董事長」 | **「姊夫」**（張安平妻為辜懷如/辜懷群一系，是辜成允的姊妹輩 → 張安平是辜成允姊夫）| `grep "妹婿"` 不該命中 + `grep "姊夫"` 應命中 |
| 2 | **[CHECK]** | 11:11 對稱杜撰 | grep 「11 點 11 分」OR 「11:11」應已修（若仍命中需重寫）| `grep "11 點 11 分" OR "11:11"` 不該命中 |
| 3 | **[CHECK]** | 辜成允 2017/1/23 萬豪酒店墜樓細節 | 是否補完整 | `grep "萬豪"` OR `grep "2017/1/23"` 確認 |
| 4 | **[CHECK]** | 「林柏壽協理」vs「常務董事」 | 1954 民營化後職稱 | grep 文中對應段確認 |

### 7. 玉山金控（identity-level 缺陷 + 年齡/職位錯）

**檔案**: `knowledge/Economy/台灣企業：玉山金控.md`
**Audit**: [audit-results/P1/Economy-玉山金控.md](audit-results/P1/Economy-玉山金控.md)

#### Audit ❌ → 改成 Y 清單

| # | 操作 | 文中 | 應改 | Grep verification |
|---|------|------|------|-------------------|
| 1 | **[ADD 整段]** | **創辦人黃永仁完全沒提名** | 必須補入 founding myth：**「1992 黃永仁帶領 30 位專業金融人士創立玉山銀行，是台灣解嚴後新銀行潮中專業金融人主導的代表」** | `grep "黃永仁"` 應命中 + `grep "founding" OR "創辦人"` 應跟黃永仁對應 |
| 2 | **[REPLACE]** | L14「黃男州 2008 年以 **43 歲**年紀成為台灣史上最年輕**金控總經理**」 | **「黃男州 1962 生，2008 年（46 歲）接任玉山銀行總經理」**（不是 43、不是金控總經理）| `grep "43 歲"` 不該命中（除非別段）+ `grep "金控總經理" + 2008` 不該共現 + `grep "玉山銀行總經理"` 應命中 |
| 3 | **[REPLACE]** | L28「2008 年是玉山發展史上的轉折點。當時 **43 歲**的黃男州接任玉山**金控總經理**」 | 同上修法 | 同上 |
| 4 | **[ADD]** | 缺：**黃男州 2022 升金控董事長 + 總經理交棒陳茂欽** | **補上：「2022 黃男州升任金控董事長，總經理交棒陳茂欽」** | `grep "2022.*董事長" OR "陳茂欽"` 應命中 |
| 5 | **[CHECK]** | 「中國 28 家分行」 | grep 是否仍命中？實際個位數 | `grep "28 家"` 確認，若仍命中改正確數字 |
| 6 | **[CHECK]** | 「玉山銀 1992 + 台灣首家專業信用卡銀行」 | 多源指 1992 新銀行多為綜合商業銀行 | grep 看是否仍寫「專業信用卡銀行」|

**Cardinal 註**：identity-level 缺陷（創辦人完全沒提）是 audit 最大發現。必須 [ADD] founding myth 段。

---

---

## 🆕 強制交付清單（per-article fix log）

巴別塔修完 7 篇後，**對每篇寫一個 fix log**：

```markdown
### 方序中 fix log

對應 audit-results/P1/People-方序中.md 每條 ❌：

| # | Audit ❌ | 修補狀態 | Grep verification |
|---|---------|---------|-------------------|
| 1 | 「1982 生於台北」 | ✅ 改「1978 屏東東港」 | `grep "1982"` 不命中 ✓ / `grep "屏東東港"` 命中 ✓ |
| 2 | 「實踐大學媒傳系」 | ✅ 改「復興商工+台藝大金工夜間部」 | `grep "實踐大學"` 不命中 ✓ |
| 3 | 「2012 創立究方社」 | ✅ 改「2013」 | `grep "2012"` 上下文不是究方社 ✓ |
| 4 | 「2014 金曲」 | ✅ 改「2016 陳鎮川邀請」 | `grep "陳鎮川"` 命中 ✓ |
| 5 | 「馬字標誌」 | ✅ 改「金馬 55 配角概念」 | `grep "馬字標誌"` 不命中 ✓ |
| 6 | 紅點 / Good Design | ⚠️ 標 TODO（搜不到一手 source）| — |
| 7 | footnote usc.edu.tw | ✅ 改維基 + 究方社官網 | `grep "usc.edu.tw"` 不命中 ✓ |
```

**每篇 fix log 必填**：
- 對應每條 audit ❌ 列**狀態**（✅ 修 / ❌ 跳過 / ⚠️ TODO）
- ❌ 跳過項**必填理由**（不可隱瞞 — 第一輪 70% 漏率是隱瞞造成的）
- Grep verification 結果（修對的舊版本字串不在 + 新版本字串在）

Fix log 寫進 `batch-200/P1-EXECUTION-REPORT.md` 末段（5/13 二次修補 section）。

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
