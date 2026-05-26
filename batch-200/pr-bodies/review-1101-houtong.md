# PR #1101 Review — 猴硐貓村

> 給主人貼到 PR #1101 的 Request changes review comment

---

## 建議 Review action

**Request changes** ❌（critical 結構 bug 必修）

---

## Comment body

@idlccp1984 感謝開 PR 寫猴硐 — 議題選得很有意義（黑金煤礦 → 生命教育 → TNR 成功的「溫柔革命」）。但目前狀態有幾個 ship-blocking 問題需要先修，建議修改後我再 approve。

### 🔴 Critical（必修才能 merge）

#### 1. 檔名拼錯 + 缺 `.md` 副檔名

當前 path：`knowledge/Society/猴桐`

兩個 bug：
- 「桐」應該是「**硐**」— 你 frontmatter title 寫「猴硐貓村」是正確漢字，但檔名打成「猴桐」
- **缺 `.md` 副檔名** — astro routing 不會 process 沒副檔名的檔案，build 後 URL 找不到

修法：
```bash
git mv "knowledge/Society/猴桐" "knowledge/Society/猴硐.md"
```

#### 2. Frontmatter 缺必要欄位（hard violation × 2）

跑 `npm run prebuild:dashboard` 會抓到：

```
🔴 frontmatter-format hard=3
  hard L1: frontmatter 缺必要欄位 `subcategory`
  hard L1: frontmatter 缺必要欄位 `featured`
```

修法：
```yaml
subcategory: '社會議題'  # 或更精確的次分類（譬如「地方創生」「動物福利」）
featured: false          # PR 不主動標 true，maintainer 統一管理
```

### 🟡 Strong（Society 強制類別 review-gate 應補）

#### 3. 缺 `rationale:` block

`category: Society` 觸發強制 rationale 規範。Plugin 抓到：

```
⚠️ rationale-presence warn L1: frontmatter 缺 `rationale:` block — 請補 4 required keys
```

完整 spec：[`docs/editorial/RATIONALE-SPEC.md`](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/RATIONALE-SPEC.md)

請補 4 required keys（**簡填 OK，one-liner 也合法** — 設計目的是「awareness trigger 不是盡職報告」）：

```yaml
rationale:
  why_this_hook: '...'      # 為什麼從「從黑金到生命教育」這 angle 切入
  whats_excluded: '...'     # 排除哪些對立論述（譬如：過度商業化批評 / 流浪貓 ethics / 觀光化 vs 在地保育之爭）+ 三選一理由
  where_it_hedges: '...'    # prose 內哪些位置是 hedge 表述
  whos_pushing_back: '...'  # 主要反對者陣營（譬如：動保派 vs 觀光業者 vs 在地居民）
  # which_framing: '...'    # optional — 沒框架可講可留空
```

簡填範例可參考 [蔡英文.md frontmatter](https://github.com/frank890417/taiwan-md/blob/main/knowledge/People/蔡英文.md)。

### 🟢 Soft（建議改善但不擋路）

#### 4. 對位句型 × 5（per EDITORIAL §六 建議上限 3）

Plugin 抓到：

```
⚠️ prose-health 對位句型 (§11 Tier 1) × 5
  L32: 「猴硐的重生並非源於政府的都市計畫，而是源於一雙看見『被遺忘者』的眼睛」
  L40: 「這座橋不只是通道，它更像是一條時間的脊骨」
  L56: 「但這並非轉型的失敗，而是『溫柔革命』的成果」
  L60: 「遊客走進山城不再是為了追逐成群的貓影，而是學習如何與生命相處」
  L62: 「猴硐貓村的『消失』，並非轉型的失敗，而是生命教育成功的標誌」
```

完整紀律：[EDITORIAL §六 對位句型禁忌](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/EDITORIAL.md)。「不是 X，是 Y」是 fabricated strawman pattern — 偶爾用有力，密度高了會帶 AI 水印味。建議：
- 保留最有力的 2-3 處（譬如 L40 時間脊骨那句、L62 收束那句）
- 其他改成直接陳述

#### 5. 79 行 接近 EDITORIAL B 級下緣

per [EDITORIAL §文章分級](https://github.com/frank890417/taiwan-md/blob/main/docs/editorial/EDITORIAL.md)：
- B 級 80-120 行 / 5+ footnote
- A 級 120-200 行 / 7+ footnote

你目前 79 行接近 B 級下緣（5 footnote 達標）。如果想擴充，「2026 年 TNR + 認養計畫減至 30 餘隻」跟「2022 年瑞三整煤廠重新開放」這兩段都還可以深化。

### ✅ 做得好的

- **Title 三明治正確**：「猴硐貓村：從黑金煤礦到生命教育的轉身，與一場關於『消失』的溫柔革命」抓到核心矛盾
- **Description** 含具體年份 + 數字 + 核心張力（30 餘隻 / 1990 停產 / 2009 爆紅）
- **策展人筆記 callout** 用到（B 級必選 ≥ 1 達標）
- **5 個 footnote** 達 B 級下限
- **Narrative arc 完整**：黑金 → 棄養潮 → TNR → 生命教育，跨層連結到位
- **「溫柔讓奇觀落幕」** 這個 framing 是 Taiwan.md 策展精神對位的好範例

---

修完 1-3 我可以 approve。4-5 是改進建議不擋路。

可以本地跑驗證：
```bash
PYTHONIOENCODING=utf-8 python3 scripts/tools/article-health.py knowledge/Society/猴硐.md --profile=release-pr
```

⚙️ Cardinal × Zaious
