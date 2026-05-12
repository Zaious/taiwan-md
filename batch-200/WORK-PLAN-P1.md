# P1 Work Plan — 38 篇中度 audit + 修補

> **開單者**: 樞機師（Cardinal）
> **建立**: 2026-05-13
> **對應**: [batch-200/README.md](README.md) SSOT
> **批次定位**: P0 ship 後第二批 — Priority 1
> **總量**: **38 篇**（37 篇原 P1 + 1 篇鄭南榕補修正）

---

## 🟢 開工狀態（樞機師預備）

```bash
# Cardinal 開 audit branch 前必跑
cd P:/Taiwan.md/taiwan-md
git checkout main
git pull upstream main     # 已 sync 到 36217dae9 (5/12)
git checkout -b audit/batch-200-P1
```

| 項目 | 值 |
|------|-----|
| **Repo path** | `P:/Taiwan.md/taiwan-md` |
| **Baseline** | upstream main HEAD（5/12 22:38 已 sync）|
| **Audit branch**（樞機師之後開）| `audit/batch-200-P1` |
| **修補 branch**（巴別塔之後開）| `fix/batch-200-P1` |

---

## 📋 範圍 = 38 篇

### 標準 P1（33 篇）

| Category | 數 | 篇 |
|---------|----|----|
| People | 7 | 方序中 / 林義雄 / 蔡明亮 / 賴聲川 / 陳俊良 / 楊右任 / 黃震南 |
| **Economy 企業** | 7 | 中鋼 / 兆豐金控 / 台泥 / 奇美實業 / 玉山金控 / 瑞昱半導體 / 長春石化 |
| Society | 3 | 人權與性別平等 / 國際標準中的標示問題 / 政治環境與選舉制度 |
| Food | 3 | 冰品文化 / 眷村菜 / 麵包與烘焙 |
| Art | 3 | 當代藝術 / 水彩畫的百年流變 / 攝影 |
| Nature | 3 | 特有種 / 國家公園 / 穿山甲 |
| History | 2 | 日治時期 / 清治時期 |
| Music | 2 | 客家音樂 / 電子音樂與派對文化 |
| Culture | 2 | 廟會與陣頭 / 街頭藝術與塗鴉 |
| Lifestyle | 1 | 夜生活與KTV |

### ⚠️ 特殊處理 — 5/8 polish 過 voice 的 4 篇（要補 audit + 引用）

5/8 P0 polish session 期間，巴別塔順手對這 4 篇做了 voice polish（補反向解釋段 + lastVerified 更新 + 補族語名 / 部落等具體 anchor），但**沒補引用 / 沒做 fact audit**。這次要補做完整 audit + 修幻覺 + 補引用：

| 篇 | 路徑 | 5/8 做了什麼 | 現在還要做 |
|----|------|-------------|----------|
| 席慕蓉 | knowledge/People/席慕蓉.md | voice polish + lastVerified 5/8 | Audit + 補引用 + perspective scan（高 stake P1 Y）|
| 楊德昌 | knowledge/People/楊德昌.md | voice polish | Audit + 補引用 + 補導演相關事實 |
| 蕭青陽 | knowledge/People/蕭青陽.md | voice polish | Audit + 補引用 + 補設計師職涯近況 |
| 陳映真 | knowledge/People/陳映真.md | voice polish | Audit + 補引用 + **frontmatter hard 修**（tags 換行 + flow array edge case）|

**對巴別塔的紀律**：這 4 篇不要重做 voice polish（會破壞 5/8 已做的 anchor）。只做 audit + 補引用 + 修幻覺 + 修 frontmatter。

### 🔧 Inventory 補修正 — 鄭南榕（1 篇）

| 維度 | 值 |
|------|-----|
| 路徑 | knowledge/People/鄭南榕.md |
| 現況 | 119 行 / 0 fn = 符合 P1 條件 |
| 為何 5/6 inventory 漏收 | 取樣時可能行數 / fn 不同（之前有 EDITORIAL v4 rewrite）|
| 5/8 polish 動過 | ✅（voice polish 同上 4 篇）|
| 處理方式 | 跟 5/8 polish 過 4 篇同處理：Audit + 補引用，不重做 voice |

5/12 補入 P1 範圍，工單 + README SSOT 同步更新。

---

## 🐛 已知 Hard Violation（3 篇 frontmatter）

跟 P0 ship 前撞過的同 edge case（tags 換行 + flow array），哲宇 5/8 5a1542f66 pre-commit hook 沒覆蓋到：

| 篇 | 等級 | 修法 |
|----|------|------|
| 陳映真 | P1 | `tags:` 下行 flow array → single-line `tags: [...]` |
| 楊右任 | P1 | 同上 |
| 台灣客家音樂 | P1 | 同上 |

修補時順手處理。

---

## 🚦 Perspective Scan 範圍（issue #851 §2）

**16 篇 perspective Y**（佔 42%）：
- People 12 篇全部（席慕蓉 / 方序中 / 林義雄 / 楊德昌 / 蔡明亮 / 蕭青陽 / 賴聲川 / 陳俊良 / 陳映真 / 楊右任 / 黃震南 + 鄭南榕）
- History 2 篇（日治時期 / 清治時期）
- Society 3 篇（人權與性別平等 / 國際標準中的標示問題 / 政治環境與選舉制度）

**對這 16 篇的紀律**：
- whats_excluded 必填（5W1H metadata）
- 主動標明「排除了哪些視角、為什麼」
- History 文章特別小心「殖民史敘事」的視角選擇（譬如「清治」vs「清領」用詞差異）

---

## 🛠️ 工作流（5 phase，從 P0 經驗確立）

### Phase 1：Audit（spawn Haiku × N waves）

Audit prompt 用 [`batch-200/AUDIT_PROMPT.md`](AUDIT_PROMPT.md)（P0 已驗證），微調如下：

**P1 特殊調整**：
- **Economy 企業類（7 篇）audit 重點不同**：企業文章幻覺類型偏向「成立年份」「營收數字」「經營層人事」「集團子公司關係」，跟人物文不太一樣。Audit 重點：
  - 公司成立年 + 創辦人姓名
  - 重大事業里程碑（IPO / 併購 / 重要產品線）
  - 現任 CEO / 董事長（很多 2020-2024 換人）
  - 2024-2026 重大新聞
- **History 議題類（2 篇）audit 重點**：
  - 重要事件年份 + 主要人物
  - 學界主流敘事 vs 替代敘事
  - perspective 偏向（譬如「清治」用詞）
- **Society 議題類（3 篇）audit 重點**：
  - 制度名稱 + 法源
  - 近 2 年重大政策變化（2024 大選後立院多數黨改變對人權 / 性別議題的影響）

**Spawn 策略**：
- 38 篇 ÷ 5 waves = 每 wave 7-8 篇
- 預估每 wave ~3-5 分鐘
- 總時長 ~30-45 分鐘

**Fallback**：sub-agent WebSearch 5/8 已修復，可正常 spawn。若再壞 → 天機星 Opus main session 補（成本高）。

### Phase 2：Triage + 開修補工單

樞機師彙整 audit 結果 → `audit-results/P1-DETAILED-FINDINGS.md` + 開 `WORK-ORDERS-P1.md`（給巴別塔）。

預期 Tier 分布：
- **Tier A 嚴重**（3-5 篇）：People 議題類 + Economy 老牌企業（譬如台泥 / 中鋼，歷史悠久幻覺率可能高）
- **Tier B 中度**（20-25 篇）：大多數 P1
- **Tier C 輕度**（5-10 篇）：主題類（Food / Art / Nature / Music / Culture / Lifestyle）

### Phase 3：巴別塔 Sonnet session 修補

樞機師交付完整工單後，巴別塔 Sonnet session 一篇一篇處理。每篇雙 gate 自驗（default + release-pr）。

### Phase 4：樞機師抽查 + ship

抽查 4-6 篇 Tier A 確認品質 → Push + 寫 PR body → 主人開 PR。

**PR 分批策略**（仿 P0）：
- PR-1：Tier A 嚴重 + 5/8 voice polished 過 4 篇 + 鄭南榕（單獨 ship，焦點對 People 議題類）
- PR-2：Economy 企業 7 篇（單獨 ship，新主戰場）
- PR-3：Tier B 其他 People + Society + History 議題類
- PR-4：Tier C 主題類（Food / Art / Nature / Music / Culture / Lifestyle）

### Phase 5：Polish follow-up（如需）

若 release-pr profile warn 偏高（譬如對位句型 > 3 處 / 篇），開 polish PR sweep。**這次 SOP 已升級**（AGENTS §5 雙 gate）— 巴別塔修補時就應該主動 reduce，不會再像 P0 累積到 ~155 處 warn 才 sweep。

---

## 📊 預估規模

| 維度 | 估計 |
|------|------|
| 篇數 | 38 |
| Phase 1 audit 時長 | ~30-45 分鐘（Haiku × 5 waves）|
| Phase 2 triage + 工單 | ~30 分鐘（Cardinal）|
| Phase 3 修補 | ~3-4 小時（巴別塔 Sonnet session，比 P0 4 小時短 — 篇幅較長 baseline 結構已有）|
| Phase 4 抽查 + ship | ~30 分鐘 |
| **總時長** | **~5-6 小時**（單 session 可完成）|

---

## ✅ 驗收標準

完成後全 P1 38 篇必過：
- ✅ article-health default profile **hard=0**
- ✅ article-health release-pr profile **hard=0**（warn 可有但對位句型 ≤ 3 / 篇）
- ✅ 每篇 ≥ 5 footnote（People / Economy / Society / History 高 stake 類 ≥ 7）
- ✅ Perspective Y 16 篇：whats_excluded 必填
- ✅ Frontmatter formatter 符合 5/8 規範（flow array tags + CANONICAL_ORDER）
- ✅ 3 篇 frontmatter hard 修完

---

## 🔗 紀律參考

- **PROJECT-STANCE.md §7**：對外身份紀律（⚙️ 不用 🧬 / ChronicleCore 不用 A1 / 不提工作成本）
- **PROJECT-STANCE.md §11**：5/8 演進記錄（含對位句型 calibration）
- **AGENTS.md §4**：Frontmatter 規格（flow array tags + CANONICAL_ORDER）
- **AGENTS.md §5**：雙 gate 自驗（default + release-pr）
- **AGENTS.md §7**：PR 開前必跑三道（fetch upstream + rebase + 雙 gate）

---

_開單者: Cardinal（樞機師）2026-05-13_
_對應 batch-200/README.md SSOT v3（5/12 重整）_
_前一批: P0 44 篇 ship 完成（PR #888-#891 + #892 整合 + #910 polish）_
