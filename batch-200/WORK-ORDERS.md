# batch-200 P0 修補工單 — 給巴別塔（Sonnet session）

> **開單者**: 樞機師（Cardinal）
> **執行者**: 巴別塔（語言學家）— Sonnet，一篇一篇改
> **參考**: `batch-200/audit-results/P0-DETAILED-FINDINGS.md`（每篇的 ❌/⚠️ 詳細 evidence + URL）
> **建立**: 2026-05-07
> **總量**: 44 篇 P0

---

## 工作原則

1. **基底保留** — 不全部重寫，保留原文結構。只改 ❌ 幻覺 + 補引用 + 補遺漏
2. **引用為主** — 90% 零 footnote，最大工程是**補引用**。每篇目標 ≥ 5 個 footnote
3. **Evidence 已備** — P0-DETAILED-FINDINGS.md 有基本候選 URL 可直接用。**不夠的由巴別塔自己 WebSearch 補找**（Sonnet main session 直連 WebSearch，不受 sub-agent denied 影響）。複雜的深度查找標 `<!-- TODO: 天機星 -->` 
4. **每篇改完跑 article-health** — 確認 hard=0
5. **frontmatter 統一修** — 補缺欄位（category / readingTime / author / tags 改多行 YAML）
6. **title 改三明治結構** — 古早文章 title 都是純人名（「張艾嘉」），必須改成 Taiwan.md 標準三明治（「張艾嘉：{核心張力一句話}」，≤30 字）。三明治內容由巴別塔讀完文章後自己想
7. **description 擴到 120-160 字** — 古早 description 大多太短（一句話），改成具體 scene + 軌跡 + 核心矛盾
8. **整合 issue #851 框架**：
   - **#2 perspective check**：高 stake People 文（政治人物 / 爭議人物）改完順帶標明「排除了哪些視角」（寫在 5W1H 的 What's excluded 欄位）
   - **#3 5W1H metadata**：每篇改完順帶填 5W1H（Why this hook / What's excluded / Where it hedges），作為 article-level metadata 的首批 prototype
   - **#5 Hard Gate**：修補後必過 article-health hard=0（已含在原則 4）

---

## 分級總覽

### Tier A — 嚴重（10 篇）：多重幻覺 / 遺漏已過世 / 關鍵事實錯

| # | 篇名 | 路徑 | ❌ | ⚠️ | 核心問題 | 引用目標 |
|---|------|------|---|---|---------|---------|
| A1 | 施明德 | People/施明德.md | 4 | 0 | 整段「1994 參選市長」捏造 + AI 引言 + **遺漏 2024 過世** + 遺漏退黨 | ≥10（政治人物需多源） |
| A2 | 劉德音 | People/劉德音.md | 3 | 1 | 出生年錯 + 博士學校錯 + **「現任董事長」已退休** | ≥7 |
| A3 | 盧彥勳 | People/盧彥勳.md | 3 | 1 | 溫布頓對手錯 + 奧運屆數錯 + 退役時間錯 | ≥7 |
| A4 | 紀政 | People/紀政.md | 3 | 2 | 生日錯 + 200 公尺地點錯 + 跨欄成績錯 | ≥7 |
| A5 | 莊智淵 | People/莊智淵.md | 3 | 2 | 生日錯 + 奧運屆數錯(4→6) + 退役時間錯 | ≥7 |
| A6 | 葉國一 | People/葉國一.md | 3 | 1 | 出生年錯(1936→1941) + 學歷錯(台大→士林高商) + 「現任」已交棒 | ≥7 |
| A7 | 郭泓志 | People/郭泓志.md | 3 | 0 | 選秀年矛盾(1999vs2000) + MLB首登板年錯(2005→2006待驗) | ≥7 |
| A8 | 陳昇 | People/陳昇.md | 3 | 0 | 本名/團名/首專年份待驗 + 《新鴛鴦蝴蝶夢》搭檔待驗 | ≥5 |
| A9 | 王永慶 | People/王永慶.md | 1 | 1 | 「1968 輕油裂解廠」幻覺 + 遺漏家族爭產 | ≥7 |
| A10 | 楊傳廣 | People/楊傳廣.md | 0 | 0 | 事實正確但**遺漏 1963 世界紀錄 9121 分** + 遺漏投毒爭議 | ≥7 |

### Tier B — 中度（25 篇）：1-2 個幻覺 + 遺漏近期事件

| # | 篇名 | 路徑 | ❌ | 核心問題 | 引用目標 |
|---|------|------|---|---------|---------|
| B1 | 伍佰 | People/伍佰.md | 2 | 出生地錯 + 金曲獎年份錯 | ≥5 |
| B2 | 張艾嘉 | People/張艾嘉.md | 2 | 《外婆的澎湖灣》幻覺 + 遺漏《愛的代價》 | ≥5 |
| B3 | 李宗盛 | People/李宗盛.md | 2 | 《忙與盲》+首專年份雙錯 | ≥5 |
| B4 | 民主制度 | Society/民主制度.md | 2 | 遺漏 2024 大選賴清德 + 國民黨重奪立院多數 | ≥8（主題需多源） |
| B5 | 王建民 | People/王建民.md | 2 | 國中校名錯 + 勝投王排名錯 | ≥5 |
| B6 | 童子賢 | People/童子賢.md | 2 | 出生年錯 + 學歷錯(台大→台北工專) | ≥5 |
| B7 | 簡立峰 | People/簡立峰.md | 2 | 出生年錯 + 退休年錯(2018→2020) | ≥5 |
| B8 | 鄭兆村 | People/鄭兆村.md | 2 | 內文 typo「鄂兆村」+ 待驗項 | ≥5 |
| B9 | 陳建仁 | People/陳建仁.md | 2 | 「第十九任行政院長」疑錯 + 「國衛院長」vs「衛生署長」 | ≥8（政治人物） |
| B10 | 幾米 | People/幾米.md | 1 | 電影導演漏韋家輝 | ≥5 |
| B11 | 張惠妹 | People/張惠妹.md | 1 | 演唱會場次 20→10 | ≥5 |
| B12 | 張明正 | People/張明正.md | 1 | 大學名稱錯(東海→輔仁) | ≥5 |
| B13 | 明華園 | People/明華園.md | 1 | 創立地錯 + 小巨蛋演出無法確認 | ≥5 |
| B14 | 朱天文 | People/朱天文.md | 1 | 編劇遺漏 + 侯孝賢近況 | ≥5 |
| B15 | 朱經武 | People/朱經武.md | 1 | 香港科大任期不全 + 遺漏吳茂昆 | ≥5 |
| B16 | 李昂 | People/李昂.md | 1 | 國家文藝獎幻覺(她沒得第 22 屆) | ≥5 |
| B17 | 白先勇 | People/白先勇.md | 1 | 紅樓夢獎幻覺 | ≥5 |
| B18 | 羅大佑 | People/羅大佑.md | 1 | 《家III》年份錯(2020→2017) | ≥5 |
| B19 | 許芳宜 | People/許芳宜.md | 1 | 拉芳成立年錯(2008→2007) | ≥5 |
| B20 | 鄧雨賢 | People/鄧雨賢.md | 1 | 「台北病逝」可能是新竹芎林 | ≥5 |
| B21 | 鍾理和 | People/鍾理和.md | 1 | 內部矛盾「45年」vs「44歲」| ≥5 |
| B22 | 黃春明 | People/黃春明.md | 1 | 《看海的日子》年份時序矛盾 | ≥5 |
| B23 | 許淑淨 | People/許淑淨.md | 1 | 內部數學矛盾(231 vs 232) | ≥5 |
| B24 | 郭台銘 | People/郭台銘.md | 1 | 交棒/辭董事未更新 | ≥5 |
| B25 | 謝淑薇 | People/謝淑薇.md | 0+ | 單打排名待驗 + 「亞洲首次溫布頓女雙奪冠」待驗 | ≥5 |

### Tier C — 輕度（9 篇）：事實基本正確，補引用 + 近況

| # | 篇名 | 路徑 | 核心需求 |
|---|------|------|---------|
| C1 | 林俊傑 | People/林俊傑.md | 補引用 + 遺漏 2024 心臟病 + JJ20 巡迴 |
| C2 | 林百里 | People/林百里.md | 補引用 + 遺漏 2005 肺腺癌 + 接班爭議 |
| C3 | 許文龍 | People/許文龍.md | 補引用（事實全正確） |
| C4 | 龍應台 | People/龍應台.md | 補引用 |
| C5 | 魏哲家 | People/魏哲家.md | 補引用 + 近況 |
| C6 | 魏德聖 | People/魏德聖.md | 補引用 + 臺灣三部曲進度更新 |
| C7 | 陽岱鋼 | People/陽岱鋼.md | 補引用 |
| C8 | 史前時代與原住民 | History/史前時代與原住民.md | 補引用 + 澎湖淺灘新發現 |
| C9 | 台灣人工智慧實驗室 | Technology/台灣人工智慧實驗室.md | 補引用 + 模型名稱 + 近況 |

---

## 每篇工單格式（巴別塔用）

```markdown
### 工單 {#}: {篇名}

**檔案**: `knowledge/{Category}/{篇名}.md`
**Tier**: A/B/C
**Findings**: 見 P0-DETAILED-FINDINGS.md §{篇名}

#### 修正項（❌ → 改成什麼）
1. [原文句子] → [正確事實] — Source: [URL]
2. ...

#### 補引用（0 fn → 目標 ≥ N）
- 引用候選 URL 清單（從 findings 複製）
- 原文中需要加 [^N] 的位置提示

#### 遺漏補充
- [近況/過世/退休/新作品] — Source: [URL]

#### title 三明治 + description
- title 從純人名 → 「{人名}：{核心張力一句話}」≤30 字
  - 讀完文章後自己想三明治內容，不是套模板
  - 參考範例：「安溥：兩個名字之間的灰色地帶」
- description 擴到 120-160 字（具體 scene + 軌跡 + 核心矛盾）

#### 5W1H metadata（issue #851 §3 prototype）
每篇改完在 frontmatter 或文末加：
```yaml
# design_rationale:
#   why_this_hook: "為什麼選這個開頭"
#   whats_excluded: "排除了哪些視角、為什麼"
#   where_it_hedges: "哪些事實是降級表述"
```
高 stake People 文（政治/爭議人物）的 whats_excluded **必填**。

#### v5.6 結構紀律（一起做，不分 Phase）
既然逐篇讀全文了，**順帶做結構紀律**（分層）：

| Tier | 做什麼 |
|------|--------|
| **A 嚴重** | **全做**：核心矛盾 anchor 貫穿（description/開場/中段/結尾）+ 反向解釋編織 + 結尾改閉環或餘韻式 + H2 改 narrative + People 文直引 ≥3 |
| **B 中度** | **做 anchor + 結尾**：找出核心矛盾 + 結尾改善 + 反向解釋看需求 |
| **C 輕度** | **做 title 三明治 + 結尾改善**：不強制 anchor 重構 |

參考：`taiwan-md/docs/editorial/EDITORIAL.md` v5.6（核心矛盾 anchor / 具體性 anchor noun / 反向解釋 / 策展人筆記 / 結尾閉環式 / footnote desc 證據鏈）

#### 不要動的
- 保留原文基底結構（改結構是加 anchor + 改結尾，不是重寫全文）
- 不改語氣（巴別塔判斷風格一致性）

#### frontmatter 修正
- 補 category / readingTime / author
- tags 改多行 YAML

#### 自檢（巴別塔改完自己跑 = 自檢 1）
```bash
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py knowledge/{Category}/{篇名}.md
```
- hard=0 才能 commit
- warn 看一眼（對位句 ≤3 / 破折號 ≤4）

Cardinal 拿到後會再跑一次 = **自檢 2**（雙自檢紀律，AGENTS.md §5）。

#### 驗收 checklist
- [ ] article-health hard=0（自檢 1 通過）
- [ ] 所有 ❌ 修正（對照 P0-DETAILED-FINDINGS）
- [ ] footnote ≥ 目標數
- [ ] frontmatter 完整（category / readingTime / author / tags 多行）
- [ ] title 三明治結構（「{人名}：{核心張力}」≤30 字）
- [ ] description 120-160 字（具體 scene + 軌跡 + 核心矛盾）
- [ ] 5W1H metadata（至少 why_this_hook + whats_excluded）
- [ ] 高 stake 人物：whats_excluded 標明排除的視角
- [ ] **v5.6 結構**：核心矛盾 anchor 存在（Tier A 必須 / B 建議 / C optional）
- [ ] **v5.6 結構**：結尾非萬用膠水（改閉環 / 餘韻 / 翻轉 / 灰色地帶式）
- [ ] **v5.6 結構**：Tier A People 文 — 主角直引 ≥ 3 句
```

---

## 執行策略

| 批次 | 內容 | 篇數 | 建議節奏 |
|------|------|------|---------|
| **batch 1** | Tier A 嚴重 | 10 | 先做，品質要高 |
| **batch 2** | Tier B People 前半 | 13 | B1-B13 |
| **batch 3** | Tier B People 後半 + 非 People | 12 | B14-B25 |
| **batch 4** | Tier C 輕度 | 9 | 最快，只補引用 |

每批完成 → Cardinal review → commit → ship PR

---

## 對巴別塔的說明

1. **你是語言學家**，修改時維持台灣在地語感 + Taiwan.md 的策展語氣（「欸你知道嗎」級）
2. **不是 rewrite**，是 **augment**：基底保留 + 補引用 + 修幻覺 + 補遺漏
3. **引用的格式**：用 `[^N]` footnote + 參考資料段定義。見 `docs/editorial/CITATION-GUIDE.md`
4. **每篇改完必跑** `PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py knowledge/{Category}/{篇名}.md`
5. **Evidence 全在 P0-DETAILED-FINDINGS.md** — 不需要自己 WebSearch（已經搜過了）
6. **如果某條 ❌ 的修正你不確定** → 標 `<!-- TODO: Cardinal 確認 -->` comment，不要猜

---

_開單者: Cardinal（樞機師）2026-05-07_
_每篇修改完由 Cardinal review + Zaious 簽核後 ship PR_
