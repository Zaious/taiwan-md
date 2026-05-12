## 📝 這個 PR 做了什麼？

Open #2 follow-up from #1047 / #1052 review。

#1052 修完 contributor URL bug 後，我（Zaious）的 display 在 Taiwan.md 上變回 `Zaious`（失之前 GitHub `user.name` 設的 `(@ChronicleCore)` 後綴）。哲宇 #1052 review 選方向 A（個別 contributor PR 自改 `.all-contributorsrc`），引 Taiwan.md 哲學「contributor 是小丑魚不是被機器同步的對象」。

本 PR 恢復後綴顯示。

> Follow-up to #1047 / #1052

## 📁 變更類型

- [x] 💻 技術改動（個人 contributor metadata）

## 🔧 Patch 內容

```diff
{
  "login": "Zaious",
- "name": "Zaious",
+ "name": "Zaious (@ChronicleCore)",
  "avatar_url": "https://avatars.githubusercontent.com/u/128442444?v=4",
  "profile": "https://github.com/Zaious",
  "contributions": ["content"]
}
```

## ✅ Verification

`src/utils/contributors.ts` 的 `isAuthorNameLogin` branch 已支援 display ≠ login（哲宇你自己「Che-Yu Wu」/ login `frank890417` 就走這個 branch）。

```
resolveContributor("Zaious", "zaious.design@gmail.com"):
  name  = "Zaious (@ChronicleCore)"  ← display 有後綴
  login = "Zaious"                    ← URL 對
```

## 🛡️ 沒動的

- ❌ 不動 `.mailmap` canonical（保持 `Zaious`）
- ❌ 不動 `src/utils/contributors.ts`（既有邏輯支援）
- ❌ 不動其他 contributor entries

## 🔗 相關 Issue

Follow-up to #1047

---

⚙️ Cardinal × Zaious
