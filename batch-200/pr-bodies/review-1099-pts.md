# PR #1099 Review — 公視

> 給主人貼到 PR #1099 的 Request changes review comment

---

## 建議 Review action

**Request changes** ❌（path/category 衝突 + frontmatter hard）

---

## Comment body

@idlccp1984 感謝開 PR 寫公視 — 公共媒體是台灣媒體生態裡最重要也最容易被忽略的議題，從《我們與惡的距離》到 2023 修法解鎖緊箍咒這條主軸很對位。但有幾個結構性問題需要先修。

### 🔴 Critical（必修才能 merge）

#### 1. 檔案路徑跟 frontmatter category 衝突

- 當前 path：`knowledge/Lifestyle/公視.md`
- Frontmatter `category: Society`

你 frontmatter 標 Society **是對的**（公視是公共媒體機構，涉及廣電法、媒體獨立、新聞自由），但檔案放在 `Lifestyle/` 路徑。應該對齊到 Society：

```bash
git mv "knowledge/Lifestyle/公視.md" "knowledge/Society/公視.md"
```

`Lifestyle` 偏向「生活方式 / 日常文化」（譬如夜市、KTV、早餐），跟公視的議題定位不對位。

#### 2. Frontmatter 缺必要欄位（hard violation × 4）

跑 `npm run prebuild:dashboard` 抓到：

```
🔴 frontmatter-format hard=4
  hard L1: frontmatter 缺必要欄位 `subcategory`
  hard L1: frontmatter 缺必要欄位 `featured`
  (+ 2 個其他 frontmatter 格式 issue)
```

補：
```yaml
subcategory: '媒體與新聞'   # 或「公共媒體」「廣電政策」等更精確的次分類
featured: false             # PR 不主動標 true，maintainer 統一管理
```

### 🟡 Strong（Society 強制類別 review-gate 應補）

#### 3. 缺 `rationale:` block

`category: Society` 觸發強制 rationale 規範。Plugin 抓到：

```
ⓘ rationale-presence info L1: frontmatter 缺 `rationale:` block — 請補 4 required keys
```

完整 spec：[`docs/editorial/RATIONALE-SPEC.md`](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/RATIONALE-SPEC.md)

公視議題有明確對立陣營，正適合用 rationale 標明：

```yaml
rationale:
  why_this_hook: '...'      # 為什麼從「九億緊箍咒 + 26 年獨立實驗」這 angle 切入
  whats_excluded: '...'     # 譬如：藍營對公視「綠化」的批評 / 媒改派對緊箍咒不夠的批評 / 商業電視台對公廣集團擴張的反對
  where_it_hedges: '...'    # prose 內哪些位置是 hedge 表述
  whos_pushing_back: '...'  # 主要反對者陣營（譬如：藍營 / 商業媒體 / 媒改派）
```

簡填 OK（one-liner 也合法 — 設計目的是「awareness trigger 不是盡職報告」）。

#### 4. 文章篇幅不足 EDITORIAL B 級 baseline

71 行 < B 級 80-120 行下緣（per [EDITORIAL §文章分級](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/EDITORIAL.md)）。

公視 26 年歷史含豐富議題：
- 1998 開播跟《公視法》制定脈絡
- 九億緊箍咒怎麼形成（朝野角力）
- 《我們與惡的距離》引發的社會療癒（具體例子可深化）
- 公廣集團整併（華視 / 客家台 / 原民台）
- 公視台語台 2019 開播
- 2023 修法解鎖

每個都可寫 1-2 段。建議擴到 B 級 80-120 行或 A 級 120-200 行。

### 🟢 Soft（建議改善但不擋路）

#### 5. 塑膠句 + 對位句型偏多

```
⚠️ prose-health
  L54 塑膠句：「不僅是法條的保障，更是台灣公民社會對公共媒體的持續監督」
  L56 塑膠句：「公視不是政府的傳聲筒，而是全民的實驗室」
  L52 對位句：「不只是文字遊戲，而是意味著公視必須...」
  L54 對位句（同上）
  L56 對位句（同上）
```

per [EDITORIAL §六](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/EDITORIAL.md)：
- 「不只是 A，更是 B」是 AI 水印句式（fabricated strawman pattern）
- 「承載著」「象徵著」「彰顯」這類空洞動詞建議替換成具體動詞

#### 6. 0 圖片（建議補 ≥ 2 張）

per [SPORE-PUBLISH §2.4](https://github.com/frank890417/taiwan-md/blob/main/docs/pipelines/SPORE-PUBLISH-PIPELINE.md)，depth article 建議 ≥ 2 張圖。

公視有豐富視覺素材：
- 公視大樓 / 公視標誌
- 《我們與惡的距離》劇照
- 早期公視開播歷史照片
- 公廣集團合影

### ✅ 做得好的

- **Title 三明治抓對核心矛盾**：「九億緊箍咒與全民客廳之間，二十六年的獨立實驗」
- **Description** 含 1998 → 2023 完整弧 + 具體節點（《我們與惡》/ 2023 修法）
- **議題切入點對**：公視法限制 → 社會療癒 → 修法解鎖，narrative 邏輯清楚
- **結尾收束**：「全民的實驗室」呼應 title「全民客廳」
- 議題類文章對位 Taiwan.md 策展精神

---

修完 1-3 我可以 approve。4-6 是改進建議不擋路。

可以本地跑驗證：
```bash
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py knowledge/Society/公視.md --profile=release-pr
```

⚙️ Cardinal × Zaious
