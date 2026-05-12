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

A+B 解了現有的 bug，audit 過程順帶看到兩個結構性 open item，列在這給你決定怎麼處理 — **這次 PR 不做，是 observation + 問你方向**。

### Open #1 — Silent breakage risk

contributor 正確顯示**依賴兩個檔案同步維護**：
- `.mailmap` — 把同人多 commit identity 變體統一到 canonical name
- `.all-contributorsrc` — canonical name → `login` + display 的 lookup 表

如果未來有 contributor：
- 進了 `.mailmap` 但漏進 `.all-contributorsrc` → profile lookup fail → fallback 把 mailmap canonical name 當 login（含空格或特殊字元 → URL 壞）
- 進了 `.all-contributorsrc` 但 commit author 有變體沒進 `.mailmap` → profile lookup miss（key 對不上）→ 同樣 fallback

這次 #1047 就是這種 gap（`.mailmap` entries 都對但 `contributors.ts` 用 `%an` 沒讀 mailmap，沒人發現直到 issue raise）。

**提案 D**：build-time / pre-commit verify script：

```
1. git log --use-mailmap 拿所有 canonical authors
2. 對照 .all-contributorsrc 用 contributorKey lookup
3. 列出 missing：
   - canonical author 在 .all-contributorsrc 沒 entry → 提示用 bot 補
   - canonical author 本身 URL-unsafe → profile.login 必須 set
4. 出 warning（不 auto-add，避免侵犯 bot 工作流）
```

可接進 `npm run prebuild`（跟 sync.sh 一起），cron routine 也能呼叫。

### Open #2 — 自定義 display name 的維護模型

A+B 後我的 display 變回「Zaious」（失去之前 `(@ChronicleCore)` 後綴）。修了 URL 也失了我自選的對外 display name。

`contributors.ts` 邏輯**已經支援 display ≠ login**（譬如你的 display「Che-Yu Wu」/ login `frank890417` 就是走這個 branch）— 只要在 `.all-contributorsrc` entry 的 `name` 設想要的顯示名就好。

但這個 case 浮現一個問題：**自定義 display name 該怎麼維護？**

兩個可能方向（你的偏好）：

| 方向 | 怎麼做 | trade-off |
|------|--------|----------|
| **A. 想改的 contributor 自己 PR 改 `.all-contributorsrc`** | 譬如我要恢復 `Zaious (@ChronicleCore)`，自己開 PR 改 `name` field | 簡單，但每人個別維護，沒統一機制 |
| **B. 做新機制（譬如 build-time 拉 GitHub `user.name`）**| 自動同步 GitHub display name 變動 | 一致性高，但加 build 依賴（API rate limit）+ 失去本地 override 自由 |

兩個 open item 我都可以接案做，等你給方向。

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
