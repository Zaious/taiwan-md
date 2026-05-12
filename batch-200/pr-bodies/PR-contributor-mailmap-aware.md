## 📝 這個 PR 做了什麼？

修 issue #1047 — 文章貢獻者顯示有壞 URL + 同人重複的 long-standing bug。

**最小變更修整體 bug**：1 行 patch (`%an` → `%aN`) + `.mailmap` 補 alias。哲宇之前已 ship `.mailmap` 機制（在 `Che-Yu Wu` entries 那段），但 `contributors.ts` 用 `%an`（raw）而不是 `%aN`（mailmap-aware）— 一字之差讓 mailmap 完全沒生效。

> Closes #1047

## 📁 變更類型

- [x] 🐛 修復錯誤（site infrastructure bug）
- [x] 💻 技術改動（contributors.ts + .mailmap）

## 🐛 Root cause

從 issue #1047 確認 RCA 後，找到三層 gap：

| 層 | Gap | Evidence |
|---|------|---------|
| **資料層** | `git log` 用 `%an`（raw author name）不走 mailmap | `src/utils/contributors.ts:88` |
| **canonical 層** | `.mailmap` 沒涵蓋 Zaious 的兩個 author name 變體 | `.mailmap` 只有 Che-Yu Wu entries |
| **顯示層** | `resolveContributor()` fallback 把 authorName 當 login → 含特殊字元 → URL 壞 | `src/utils/contributors.ts:62` |

具體：我的 commits 在 git log 有兩種 author name：
- `Zaious` ← 正常
- `Zaious (@ChronicleCore)` ← GitHub 端某些 squash merge 流程把 user.name 寫進 author，含括弧、@ 等特殊字元

第二種被 fallback 寫進 `contributor.login`，URL 變成 `https://github.com/Zaious (@ChronicleCore)` 壞 link。

哲宇之前已經建立 `.mailmap` 機制（commit message 寫「git natively honors this」）— 但 `contributors.ts` 用 `%an` 沒觸發 mailmap，所以效果沒落地。

## 🔧 Patch 內容

### Patch A — `src/utils/contributors.ts`

```diff
-      `git log --full-history -z --name-only --format="COMMIT|%H|%aI|%an|%ae" -- "${knowledgePath}"`,
+      `git log --full-history -z --name-only --format="COMMIT|%H|%aI|%aN|%aE" -- "${knowledgePath}"`,
```

`%an/%ae` → `%aN/%aE`（capital N/E）讓 git log 自動讀 `.mailmap` 規範化 author name + email。

### Patch B — `.mailmap`

```diff
+ # ── Zaious ────────────────────────────────────────────────
+ # GitHub user.name 含 "(@ChronicleCore)" 不適合當 URL slug，
+ # 統一為 canonical "Zaious" (對應 GitHub login 同名)。
+ Zaious <zaious.design@gmail.com> Zaious (@ChronicleCore) <zaious.design@gmail.com>
```

## 📊 Audit — 全站受影響範圍

跑 `git log --pretty='%H|%an'` 統計後：

| 受害 author name | knowledge/*.md 觸及篇數 |
|------------------|------------------------|
| `Zaious (@ChronicleCore)` | **48** |
| `Chao-Chun (Joe) Hsu` (potential) | 0（不觸及 knowledge/）|

48 篇含：batch-200 P0 修補 + #852 道德課 + #708 教會公報 + #702 活俠傳 + #599 VR/麻將/X-Legend + #625 citations retroactive audit 21 篇 + #910 polish PR 31 篇（去重 48）。

**本 patch 不動文章本身**，僅修 site infrastructure 層 — 重 build 後 contributor 顯示自動修正。

## ✅ Verification

```bash
# 修補前（用 %an raw）
$ git log --all --pretty='%an' | grep -iE 'zaious' | sort -u
Zaious
Zaious (@ChronicleCore)              ← 兩個變體

# 修補後（用 %aN mailmap-aware）
$ git log --all --pretty='%aN' | grep -iE 'zaious' | sort -u
Zaious                                ← 統一 ✅
```

## 🛡️ 為什麼這 patch 不會踩到「變成文章修改者」迴圈

Issue #1047 §4 紀律明寫：

> 修補 contributor 顯示 bug **必須限制在 site infrastructure 層**（`src/` + `scripts/` + build pipeline），**禁止觸碰 `knowledge/*.md` 文章本身**

本 patch 嚴格符合：
- ✅ 只動 `src/utils/contributors.ts` + `.mailmap`
- ✅ 沒動任何 `knowledge/*.md`
- ✅ 重 build 後 48 篇文章 contributor 顯示**自動**修正

## 🤔 沒做的（留給後續討論）

**Patch C（深度防衛）**：`resolveContributor()` fallback 加 sanitize 邏輯 — 當 authorName 含 `(`、`@`、空格等 URL 不安全字元時不當 login。

Patch A+B 已 fix 我這邊（Zaious）的 case。Patch C 是預防未來其他 contributor 也設了特殊字元 user.name 撞同問題。沒做是因為：

- 目前只觀察到 1 個其他 raw author 含特殊字元（`Chao-Chun (Joe) Hsu`），但他的 commits 不觸及 `knowledge/`，site 沒實際顯示問題
- 防衛性邏輯設計需要更謹慎（哪些字元算 unsafe / 怎麼 fallback / 是否需要 warning），這應該另開 issue 討論

如果你想一起做 Patch C 也行，告訴我方向。

## 🔗 相關 Issue

Closes #1047

---

⚙️ Cardinal × Zaious
