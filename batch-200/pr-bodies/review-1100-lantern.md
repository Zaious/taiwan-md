# PR #1100 Review — 天燈

> 給主人貼到 PR #1100 的 Request changes review comment

---

## 建議 Review action

**Request changes** ❌（frontmatter hard + prose quality 嚴重）

---

## Comment body

@idlccp1984 感謝開 PR 寫天燈 — 題材很有意義（文化傳承 vs 環境永續 + 從烽火信號到觀光符號的歷史漂流）。但目前 prose 品質有比較多需要修的地方。

### 🔴 Critical（必修才能 merge）

#### 1. Frontmatter 缺必要欄位（hard violation × 2）

跑 `npm run prebuild:dashboard` 抓到：

```
🔴 frontmatter-format hard=3
  hard L1: frontmatter 缺必要欄位 `subcategory`
  hard L1: frontmatter 缺必要欄位 `featured`
```

補：
```yaml
subcategory: '民俗與信仰'   # 或「節慶文化」「平溪文化」等更精確
featured: false             # PR 不主動標 true，maintainer 統一管理
```

### 🟡 Strong（quality threshold 嚴重未達）

#### 2. 塑膠句 + 對位句型 + 抽象 metaphor 嚴重偏多

plugin 抓到 16 處 violations：

```
⚠️ prose-health hard=0 warn=12
  prose-health score: 6 (≤ 3 = pass) — 翻倍超標

塑膠句 × 4:
  L16: 「不僅承載著人們對來年的美好祝願，更是一部活生生的台灣史詩」
  L34: 「不僅是單純的通訊工具，更承載著亂世中對家人安危的深切掛念」
  L58: 「這不僅是技術問題，更是價值觀的權衡」
  L72: 「承載著避難信號與祈福心願的燈火」

對位句型 × 6:
  L13: 「不僅是文化傳承的象徵，更是一道考驗台灣社會如何在傳統與永續之間取得...」
  L16: 「不僅承載著人們對來年的美好祝願，更是一部活生生的台灣史詩」
  L36: 「天燈的起源並非浪漫的祈願，而是亂世中求生存的智慧與親情連結的象徵」
  L58: 「這不僅是技術問題，更是價值觀的權衡」
  L72: 「不僅是平溪地區重要的文化地標，更是台灣向世界展現其豐富民俗的窗口」
  L74: 「這並非是單純地選擇保留傳統或擁抱環保，而是在兩者之間尋求一個動態的平衡點」

抽象 metaphor 密度 × 6:
  「承載著」「象徵」「彰顯」「漂流」 等空洞動詞
```

per [EDITORIAL §六 對位句型禁忌 + §quality-scan 塑膠句](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/EDITORIAL.md)：

- **「不只是 A，更是 B」是 fabricated strawman**：偶爾用有力，密度高了就是 AI 水印
- **空洞動詞**「承載著」「象徵著」「彰顯」要替換成具體動詞

建議全文 reduce：
- 對位句型保留最有力的 2-3 處（譬如 L36 起源歷史那句）
- 「不只是 A 更是 B」改成「A 跟 B 」並列陳述
- 「承載著 X」改成「X」直接陳述（譬如「承載著親情連結」→「親情連結」or 具體場景）

修完後再跑 `--profile=release-pr` 確認 `prose-health score ≤ 3`。

### 🟢 Soft（建議改善但不擋路）

#### 3. Culture 是建議級 — 但天燈有 controversy 維度可補 rationale

`category: Culture` 是 [RATIONALE-SPEC](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/RATIONALE-SPEC.md) 建議級不強制。但天燈題材含明顯對立論述：

- 環境派 vs 文化傳承派
- 平溪地方居民 vs 觀光客
- 動物受傷 / 失火爭議 / 飄落物
- 環保替代方案（環保天燈）vs 傳統派

適合補 `rationale:` block 標明排除了哪些角度（簡填 OK）：

```yaml
rationale:
  why_this_hook: '...'
  whats_excluded: '...'   # 譬如：環保派完全廢除主張 / 觀光客體驗派
  where_it_hedges: '...'
  whos_pushing_back: '...'
```

#### 4. 0 圖片（建議補 ≥ 2 張）

天燈有絕佳視覺素材：
- 平溪元宵節橙黃光點夜空
- 天燈書寫祈願細節
- 環境問題照片（落地殘骸 / 山林清理）
- 環保天燈替代方案

per [SPORE-PUBLISH §2.4](https://github.com/frank890417/taiwan-md/blob/main/docs/pipelines/SPORE-PUBLISH-PIPELINE.md) depth article 建議 ≥ 2 張。圖文配 narrative 大幅提升感染力。

#### 5. 行數 91 行 OK（B 級範圍內）

per [EDITORIAL §文章分級](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/EDITORIAL.md) B 級 80-120 行，你 91 行在範圍內。✅

### ✅ 做得好的

- **Title 三明治對位**：「從烽火狼煙到環境爭議，一盞祈福燈的百年漂流」抓到歷史 + 議題雙弧
- **起源具體年代**：清道光年間避難信號（不是模糊「古代」）
- **環境爭議段平衡**：沒一面倒批評環保派或傳統派
- **百年漂流** framing 對位 Taiwan.md 策展精神
- **跨層連結**：信號 → 祈福 → 觀光 → 環境，narrative arc 完整

---

修完 1-2 我可以 approve。3-5 是改進建議不擋路。

可以本地跑驗證：
```bash
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py knowledge/Culture/天燈.md --profile=release-pr
```

⚙️ Cardinal × Zaious
