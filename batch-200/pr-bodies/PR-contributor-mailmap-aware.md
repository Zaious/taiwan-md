## 📝 這個 PR 做了什麼？

修 issue #1047 — 文章貢獻者顯示有壞 URL + 同人重複的 long-standing bug。

兩個 patch：

| Patch | 內容 | 解的 case |
|-------|------|----------|
| **A** | `src/utils/contributors.ts` 改 `%an/%ae` → `%aN/%aE`（git log 走 `.mailmap`）| `Wu Che Yu` / `frank890417` 等變體被既有 `.mailmap` 統一為 `Che-Yu Wu` |
| **B** | `.mailmap` 補 Zaious alias | `Zaious (@ChronicleCore)` 統一為 `Zaious` |

你之前 ship 的 `.mailmap` 機制（Che-Yu Wu entries）已經就位，但 `contributors.ts` 用 `%an` 不是 `%aN` — 一字之差讓 mailmap 全程沒生效。

> Closes #1047

## 📁 變更類型

- [x] 🐛 修復錯誤（site infrastructure bug）
- [x] 💻 技術改動

## 📊 現況（解完之後）

| Author 變體 | 解前 URL | 解後 URL | Display |
|-----------|---------|---------|---------|
| `Zaious (@ChronicleCore)` | ❌ `github.com/Zaious (@ChronicleCore)` | ✅ `github.com/Zaious` | `Zaious` |
| `Zaious` | ✅ | ✅（不變） | `Zaious` |
| `Wu Che Yu` | ❌ `github.com/Wu Che Yu` | ✅ `github.com/frank890417` | `Che-Yu Wu` |
| `Che-Yu Wu` | ✅ | ✅（不變） | `Che-Yu Wu` |
| `frank890417` | ✅ | ✅（不變） | `Che-Yu Wu` |

同人去重也自動修：dedup 邏輯本來就用 `contributor.login`，A+B 統一 login 後同人多 variant 自動只顯示一次。

全站 48 篇 `knowledge/*.md` 含我（Zaious）的 commits，rebuild 後 contributor 顯示自動修正 — **不動 `knowledge/*.md` 文章本身**，僅修 site infrastructure 層。

## ⚠️ 未解的問題

A+B 解了現有的 bug，但現有機制有結構性 silent breakage risk：

contributor 正確顯示**依賴兩個檔案同步維護**：
- `.mailmap` — 把同人多 commit identity 變體統一到 canonical name
- `.all-contributorsrc` — canonical name → `login` + display 的 lookup 表

如果未來有 contributor：
- 進了 `.mailmap` 但漏進 `.all-contributorsrc` → profile lookup fail → fallback 把 mailmap canonical name 當 login（含空格或特殊字元 → URL 壞）
- 進了 `.all-contributorsrc` 但 commit author 有變體沒進 `.mailmap` → profile lookup miss（key 對不上）→ 同樣 fallback

這次 audit 就發現 5/7 PR #884 / `.mailmap` ship 跟 `contributors.ts` 之間有 silent gap（mailmap entries 都對但邏輯沒讀）— **沒人發現直到 issue #1047**。

## 💡 提案 Patch D — 自動化 sync verification

build-time（或 pre-commit hook）跑 verification script：

```
1. 跑 git log --use-mailmap 拿所有 canonical authors
2. 對照 .all-contributorsrc 用 contributorKey lookup
3. 列出兩種 case：
   - canonical author 在 .all-contributorsrc 沒 entry → 該補（提示用 @all-contributors bot）
   - canonical author 本身 URL-unsafe（含 ( ) space @ 等）→ profile.login 必須 set
4. 出 warning（不 auto-add，避免侵犯 bot 工作流）
```

可以接進 `npm run prebuild`（跟 sync.sh 一起），cron routine 也可以呼叫。

**要不要我們接案做？** 如果你想做，我這邊可以打第二個 PR：
- script 本身（~50-80 行 JS）
- prebuild 整合
- 文件化「新 contributor onboarding 要動哪些檔案」

或你想自己定方向 / 設計細節我們再做 / 不做都行 — 等你的判斷。

## 🛡️ 紀律守住

Issue #1047 §4 紀律明寫：

> 修補 contributor 顯示 bug **必須限制在 site infrastructure 層**（`src/` + `scripts/` + build pipeline），**禁止觸碰 `knowledge/*.md` 文章本身**

本 PR 嚴格符合：
- ✅ 只動 `src/utils/contributors.ts` + `.mailmap`
- ✅ 沒動任何 `knowledge/*.md`
- ✅ Rebuild 後 48 篇文章 contributor 顯示**自動**修正

## 🔗 相關 Issue

Closes #1047

---

⚙️ Cardinal × Zaious
