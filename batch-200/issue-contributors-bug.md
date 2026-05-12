# Issue: 文章貢獻者顯示異常（壞 URL + 同人重複）

> **狀態**: 草稿 → 待主人開 issue
> **建立**: 2026-05-12 by Cardinal
> **預定 issue 目標 repo**: frank890417/taiwan-md

---

## 🎯 Title 候選（主人挑一個）

### A. 簡短版（推薦）
```
🐛 文章貢獻者顯示異常：壞 URL + 同人重複（long-standing bug）
```

### B. 帶 root cause 版
```
🐛 文章貢獻者顯示異常 — user.name 含特殊字元觸發 fallback 路徑（壞 URL + 重複）
```

### C. 英文標準版
```
🐛 Article contributors: broken URL + duplicate when GitHub user.name has special chars
```

---

## 📝 Body

複製以下 markdown 到 GitHub issue。

---

## 觀察

**Case A：早期文章** [`technology/台灣VR元宇宙興衰史`](https://taiwan.md/technology/%E5%8F%B0%E7%81%A3VR%E5%85%83%E5%AE%87%E5%AE%99%E8%88%88%E8%A1%B0%E5%8F%B2/)

| 顯示 | URL | 狀態 |
|------|-----|------|
| Che-Yu Wu | `github.com/frank890417` | ✅ 正確 |
| **Zaious (@ChronicleCore)** | `github.com/Zaious (@ChronicleCore)` | ❌ 壞 link |

**Case B：近期文章** [`people/王建民`](https://taiwan.md/people/%E7%8E%8B%E5%BB%BA%E6%B0%91/)

| 顯示 | URL | 狀態 |
|------|-----|------|
| **Zaious (@ChronicleCore)** | `github.com/Zaious (@ChronicleCore)` | ❌ 壞 link |
| Che-Yu Wu | `github.com/frank890417` | ✅ 正確 |
| **Zaious** | `github.com/Zaious` | ✅ 正確（重複）|
| **Wu Che Yu** | `github.com/Wu Che Yu` | ❌ 壞 link（重複）|
| ytw | — | ? |

## 1. 機制 RCA

GitHub API 上我（Zaious）的 user.name 設定：

```
login: Zaious
name:  Zaious (@ChronicleCore)   ← 含括弧、@ 等特殊字元
```

這個 display name 已用很久（不是最近改的），所以這個 bug 是 long-standing。

從兩個 case 表現不同推測 site 有兩條 derive contributor 的路徑：

| 路徑 | 用什麼當 URL | 用什麼當 display | 結果 |
|------|------------|----------------|------|
| **正確路徑** | `user.login` | `user.name` | URL 對，display 對（VR 元宇宙 Che-Yu Wu）|
| **Fallback 路徑** | `git author name`（同時當 login + display）| 同左 | URL 含特殊字元 → 壞 link |

王建民同時走兩條路徑各 derive 一次沒去重，導致 Zaious 重複顯示。

## 2. 受影響範圍

不只 batch-200 修補的近期文章：

- ✅ 確認：我的早期 contribute 文章也撞（VR 元宇宙是這次抽到的 sample）
- 🟡 推測：**其他 contributor 設了特殊字元 user.name 的人都會撞**（不只我）
- 🟡 推測：所有觸發 fallback 路徑的 commits 都會撞，可能跨 hundreds of articles

需要全站 scan 才能確認規模。

## 3. 修正方向

主要修法（推測涉及 `src/templates/article.template.astro` + `src/components/ArticleSidebar.astro` + `getGitInfoForLang()` helper）：

- **A**：URL 構造永遠用 `login`，display 用 `name`。Fallback 路徑要先補上 login 查詢
- **B**：去重邏輯改 login-based（同 login 只顯示一次，preferred display 規則待定 — 譬如 prefer GitHub `name` 而不是 git author name）
- **C**：A + B 一起做（推薦）

## 4. 回溯性審計需求

修完 src/ 邏輯後，已 ship 的文章 contributor 顯示會自動修正（site rebuild 重新從 git log derive）— **不需要碰 knowledge/ 文章本身的 frontmatter / 內容**。

但需要驗證：

- 全站 audit 哪些文章被撞（多少篇）
- Rebuild 後抽樣驗證每個受影響 contributor 都顯示正確

> ⚠️ **紀律**：修補 contributor 顯示 bug **必須限制在 site infrastructure 層**（`src/` + `scripts/` + build pipeline），**禁止觸碰 `knowledge/*.md` 文章本身**。任何對文章 frontmatter / 內容的 commit 都會讓我們再次出現在那篇文章的 contributor list — 變成「為了修 bug 反而把自己加進貢獻者」的迴圈。Fix 只能在 src/ 層，不能在 knowledge/ 層。

## 5. 我這邊可以接這個 case 嗎？

如果方向 OK，我可以打 PR：

- Fix `src/` 邏輯（修法方向 A+B）
- 寫 audit script 跑全站確認受影響範圍
- Build 後抽樣驗證

不直接 PR 是因為這涉及 site infrastructure，你可能有更深的設計考量（譬如 GitHub API rate limit handling / build-time cache 等）。等你給方向我來打 PR，或你想自己處理也行。

⚙️ Cardinal × Zaious
