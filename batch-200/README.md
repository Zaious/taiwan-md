# batch-200 — 古早 200 篇品質整頓

> **對應 issue**: [#851 §5](https://github.com/frank890417/taiwan-md/issues/851)
> **觸發**: 飯局哲宇親口「早期 200 batch 是 AI 生成、品質堪憂」
> **模式**: **基底 + 引用 − 幻覺**（不是全部重寫）
> **建立**: 2026-05-06 by Cardinal
> **主人**: Zaious

---

## 操作原則

**保留原文作為基底** — AI 生成的內容結構不一定差，缺的是引用支撐。

| 操作 | 做什麼 |
|------|--------|
| ✅ 補引用 | 找真實 source 支撐原文 claims |
| ✅ 移幻覺 | 事實錯誤 / 捏造 claims → 移除或修正 |
| ✅ 補具體 | v5.6 anchor noun / 反向解釋 / 結尾 |
| ✅ 5W1H | 修完順帶附 metadata |
| ✅ perspective scan | 高 stake 子集（People/Society/History） |
| ❌ 不全部重寫 | 除非 P0 且內容空泛到無法補救 |

---

## 前 200 篇畫像

- **時間範圍**: 2026-03-17 ~ 2026-03-20（三天內 AI batch 生成）
- **總數**: 200 篇（全站 662 篇的 30%）
- **90% 零 footnote** — 核心問題

### Severity 分級

| 等級 | 條件 | 數量 | 處理方式 |
|------|------|------|---------|
| **P0** | 0 footnote + < 80 行 | **44** | 大改：補引用 + 補具體 + 結構修正（部分可能要 flag for rewrite） |
| **P1** | 0 footnote + 80-119 行 | **38** | 中改：補引用 + minor polish |
| **P2** | 0 footnote + ≥ 120 行 | **98** | 輕改：補引用為主 |
| **P3** | ≥ 1 footnote | **20** | 驗引用 + perspective check |

### Perspective scan 需求（#2 多元觀點）

| 需要 | 數量 | Category |
|------|------|----------|
| **Y** | **87** | People (67) + Society (11) + History (9) |
| N | 113 | Economy / Music / Technology / Culture / Nature / Food / Art / Geography / About / Lifestyle |

### Category 分布

| Category | 數量 |
|----------|------|
| **People** | **67** |
| Economy | 29 |
| Music | 14 |
| Technology | 13 |
| Culture | 13 |
| Nature | 12 |
| Society | 11 |
| Food | 11 |
| History | 9 |
| Art | 9 |
| 其他 | 12 |

---

## 目錄結構

```
batch-200/
├── README.md                    ← 本檔（任務說明 + 進度）
├── inventory-raw.txt            ← 200 篇原始清單（date|path）
├── inventory-enriched.txt       ← 加行數 + footnote
├── inventory-graded.txt         ← 加 P0-P3 等級 + perspective scan flag
├── audit-results/               ← spawn-agent audit 結果（每篇一個 .md）
├── citations/                   ← 找到的引用候選（分 category 或主題）
└── pr-batches/                  ← 每批 PR 的 diff + commit message
```

---

## 作業流程

```
Phase 0: ✅ 產出 inventory + 分級（本檔）

Phase 1: spawn-agent batch audit（~200 篇）
  └── 每篇抽 claims + 找候選引用 + AI 味分析 + v5.6 結構 check
  └── 先跑 5 篇 prototype 確認 prompt + output 格式
  └── 結果存 audit-results/{category}/{slug}.md

Phase 2: 人類 triage（主人 + Cardinal）
  └── 看 audit 結果決定每篇 action（augment / rewrite / skip）
  └── 標記 perspective-scan 子集的處理策略
  └── 更新 inventory-graded.txt

Phase 3: 修補（分批 ship PR）
  └── 每批 ~20 篇 → 1 PR
  └── 補引用（spawn-agent 找候選 → 人類驗證 URL）
  └── 移幻覺 + 補具體 + 5W1H 附帶
  └── PR draft 存 pr-batches/

Phase 4: 驗證 + ship
  └── 每 PR 跑 article-health 確認
  └── reviews/ 紀錄
```

---

## 進度追蹤

| Phase | 狀態 | 日期 |
|-------|------|------|
| Phase 0 inventory | ✅ 完成 | 2026-05-06 |
| Phase 1 prototype (5 篇) | ⬜ | — |
| Phase 1 full batch audit | ⬜ | — |
| Phase 2 triage | ⬜ | — |
| Phase 3 batch 1 (PR) | ⬜ | — |
| ... | ... | ... |

---

## P0 最差的前 10 篇（最先處理）

| 檔案 | 行數 | Footnote |
|------|------|----------|
| knowledge/People/張艾嘉.md | 43 | 0 |
| knowledge/People/明華園.md | 44 | 0 |
| knowledge/People/伍佰.md | 50 | 0 |
| knowledge/People/劉德音.md | 51 | 0 |
| knowledge/People/張惠妹.md | 55 | 0 |
| knowledge/History/史前時代與原住民.md | 58 | 0 |
| knowledge/People/幾米.md | 59 | 0 |
| knowledge/People/張明正.md | 63 | 0 |
| knowledge/People/施明德.md | 79 | 0 |
| knowledge/Society/民主制度.md | 79 | 0 |

---

_建立 by Cardinal（樞機師）2026-05-06_
_對應 issue #851 §5 + 飯局共識「哲宇認領早期 200 batch 品質堪憂」_
