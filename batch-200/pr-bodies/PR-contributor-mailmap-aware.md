## 📝 這個 PR 做了什麼？

修 issue #1047 — 文章貢獻者顯示有壞 URL + 同人重複的 long-standing bug。

完整回溯後發現有 3 個 author name 含特殊字元 (URL-unsafe)：
- `Zaious (@ChronicleCore)`（我的 GitHub display name）
- `Wu Che Yu`（你的 author name 變體，已有 `.mailmap` 但沒生效）
- `Chao-Chun (Joe) Hsu`（其他 contributor）

需要三層 patch 才能完整修：

| Patch | 修什麼 | 對應 case |
|-------|--------|---------|
| **A** | `%an` → `%aN`（git log 走 .mailmap） | Wu Che Yu（觸發既有 .mailmap entry）|
| **B** | `.mailmap` 補 Zaious alias | Zaious (@ChronicleCore) |
| **C** | `resolveContributor()` 加 email-derive fallback | Chao-Chun (Joe) Hsu + 未來新 case |

哲宇之前已 ship `.mailmap` 機制（在 `Che-Yu Wu` entries 那段），但 `contributors.ts` 用 `%an`（raw）而不是 `%aN`（mailmap-aware）— 一字之差讓 mailmap 完全沒生效。

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

### Patch C — `src/utils/contributors.ts` `resolveContributor()` 加 sanitize fallback

當 authorName 含 URL-unsafe 字元時，從 email local-part derive login（many maintainers use `email prefix == GitHub login`）。

```typescript
// New helpers
const GITHUB_LOGIN_REGEX = /^[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,37}[a-zA-Z0-9])?$/;
function isUrlSafeLogin(s: string): boolean { return GITHUB_LOGIN_REGEX.test(s); }
function deriveLoginFromEmail(email: string): string | null { ... }

// Updated fallback chain
const fallbackLogin = isUrlSafeLogin(authorName)
  ? authorName
  : deriveLoginFromEmail(authorEmail) || authorName;
const login = githubLogin || profile?.login || fallbackLogin;
```

設計考量：
- ✅ 不擅自改 `.mailmap` 別人的 canonical name（每個人選擇自己的 display name）
- ✅ 不擅自改 `.all-contributorsrc`（all-contributors bot 維護領域）
- ✅ 未來新 contributor 設特殊字元 user.name 也自動救到，不需手動 patch

## 📊 Audit — 全站受影響範圍

跑 `git log --pretty='%H|%an'` 完整回溯：

| 受害 author name | Email | 修法 |
|------------------|-------|------|
| `Zaious (@ChronicleCore)` | zaious.design@gmail.com | Patch B（.mailmap）|
| `Wu Che Yu` | frank890417@gmail.com | Patch A（觸發既有 .mailmap）|
| `Chao-Chun (Joe) Hsu` | joe32140@gmail.com | Patch C（email-derive → `joe32140`）|

含特殊字元觸及 `knowledge/*.md` 篇數 ≥ 48（Zaious 變體）+ 散見 site infrastructure commits（Wu Che Yu / Chao-Chun）。

**本 patch 不動文章本身**，僅修 site infrastructure 層 — 重 build 後 contributor 顯示自動修正。

## ✅ Verification

### 1. `.mailmap` 生效（Patch A+B）

```bash
# 修補前（用 %an raw）
$ git log --all --pretty='%an' | grep -i zaious | sort -u
Zaious
Zaious (@ChronicleCore)              ← 兩個變體

# 修補後（用 %aN mailmap-aware）
$ git log --all --pretty='%aN' | grep -i zaious | sort -u
Zaious                                ← 統一 ✅
```

### 2. `resolveContributor()` 5 個 case 驗證（Patch C）

跑 `node test-resolve.mjs`（test 檔 PR 後刪除）：

| Author | Email | 預期 login | 實際 | Pass |
|--------|-------|----------|------|------|
| Zaious | zaious.design@gmail.com | `Zaious` | `Zaious` | ✅ |
| Chao-Chun (Joe) Hsu | joe32140@gmail.com | `joe32140` | `joe32140` | ✅ |
| houston[bot] | astrobot-houston@users.noreply.github.com | `astrobot-houston` | `astrobot-houston` | ✅ |
| Che-Yu Wu | cheyu.wu@monoame.com | `frank890417` | `frank890417` | ✅ |
| Wu Che Yu | frank890417@gmail.com | `frank890417` | `frank890417` | ✅ |

**5/5 passed**。

## 🛡️ 為什麼這 patch 不會踩到「變成文章修改者」迴圈

Issue #1047 §4 紀律明寫：

> 修補 contributor 顯示 bug **必須限制在 site infrastructure 層**（`src/` + `scripts/` + build pipeline），**禁止觸碰 `knowledge/*.md` 文章本身**

本 patch 嚴格符合：
- ✅ 只動 `src/utils/contributors.ts` + `.mailmap`
- ✅ 沒動任何 `knowledge/*.md`
- ✅ 重 build 後 48 篇文章 contributor 顯示**自動**修正

## 🔗 相關 Issue

Closes #1047

---

⚙️ Cardinal × Zaious
