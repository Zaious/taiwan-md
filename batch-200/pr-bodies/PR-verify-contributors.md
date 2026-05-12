## 📝 這個 PR 做了什麼？

Open #1 Patch D follow-up from #1047 / #1052 review。

#1052 review 你接受 Patch D 提案（build-time `git log --use-mailmap` vs `.all-contributorsrc` sync verify script），引 DNA #52 fail-loud + DNA #43 derived 資料儀器化進生命週期觸發點。

本 PR 實作：
- **verify script** — 跑 git log + `.all-contributorsrc` 對照
- **prebuild 整合** — 跟 `generate-contributors-data` 同 lifecycle
- **maintainer doc** — `docs/factory/contributors-maintenance.md`

> Follow-up to #1047 / #1052

## 📁 變更類型

- [x] 💻 技術改動（site infrastructure verify script）
- [x] 📚 文件更新（contributor maintenance 紀律）

## 🔧 三個檔案

### 1. `scripts/tools/verify-contributors.mjs`（new, ~160 行）

邏輯：

```
1. git log --all --format=%aN|%aE  (走 .mailmap, spawnSync 避 Windows shell)
2. .all-contributorsrc 用 contributorKey lookup
   (跟 src/utils/contributors.ts 同 normalization)
3. 列出：
   - canonical author 在 .all-contributorsrc 沒 entry → missing
   - profile.login URL-unsafe → unsafe
4. WARN-only (exit 0)，不 fail build
```

**設計紀律**：
- ✅ WARN-only — 避免 contributor onboarding 卡 build
- ✅ 不 auto-add — 不侵犯 all-contributors bot 工作流
- ✅ Skip GitHub noreply email（contributors.ts 既有 regex 已 cover）
- ✅ Skip `[bot]` suffix（譬如 `houston[bot]`）

### 2. `package.json` — 接進 `npm run prebuild`

```diff
- "prebuild": "... run-p ... prebuild:contributors prebuild:supporters ...",
+ "prebuild": "... run-p ... prebuild:contributors prebuild:verify-contributors prebuild:supporters ...",
+ "prebuild:verify-contributors": "node scripts/tools/verify-contributors.mjs",
```

跟 `prebuild:contributors`（既有的 `generate-contributors-data`）平行跑同 lifecycle。CF Pages build / 本地 dev / routine 都自動觸發。

### 3. `docs/factory/contributors-maintenance.md`（new, ~90 行）

短 doc 紀錄：
- 兩個 standard layer 各管職責（`.mailmap` git tooling layer + `.all-contributorsrc` recognition layer）
- 新 contributor onboarding 流程（用 all-contributors bot）
- Verify warning 怎麼處理（常規 vs edge case）
- 自定義 display name 的支援機制（哲宇 Che-Yu Wu + Zaious (@ChronicleCore) 範例）

## 📊 Baseline Audit

跑 verify 揭露 **11 個 silent breakage cases**：

```
   Missing .all-contributorsrc entries (11):
     "ytw" <a9600125a@gmail.com>
     "JacobMei" <jacobmei@gmail.com>
     "pingu" <pingu@Pen-Book-M1.local>
     "Claude" <noreply@anthropic.com>
     "Howie" <howie0417@gmail.com>
     "Bugn!i!" <sunnieqqqq17@gmail.com>
     "yu-heng huang" <jamesyhh@gmail.com>
     "So͘ Bîn-hiân" <minsiansu@gmail.com>
     "Hans" <hans@groupg.org>
     "Freddy" <freddy.luo@cedarsdigital.io>
     "Jekyll Chen" <jekyll530@hotmail.com>
```

這些 contributor **可能在 `.all-contributorsrc` 已有 entry**（譬如 `jekyll530` / `bugnimusic`），但 commit author name normalize 後 key 對不上 — silent break 直到 verify script 跑出來。

建議用 `@all-contributors please add @<login>` 逐一補（bot 工作流不破壞）。如果是同一人多 commit identity 變體，補 `.mailmap` alias 統一即可（譬如 `Jekyll Chen` → `jekyll530` 的 alias）。

> 本 PR 不主動補這 11 個 entries — 留給你的 bot 工作流。

## ✅ Verification

```bash
$ npm run prebuild:verify-contributors

> taiwan-md@1.4.0 prebuild:verify-contributors
> node scripts/tools/verify-contributors.mjs

⚠️  verify-contributors: found missing/unsafe contributor entries
   ...11 entries...
   (WARN-only — does not fail build. See docs/contributors-maintenance.md)
```

Exit code 0，prebuild 繼續跑。

## 🛡️ 紀律守住

- ✅ 只動 `scripts/tools/` + `package.json` + `docs/factory/`
- ✅ 沒動 `src/utils/contributors.ts`（保持單一變更原則 vs PR #1052）
- ✅ 沒動 `knowledge/*.md`（對齊 #1047 §4）
- ✅ 沒動 `.all-contributorsrc`（recognition layer 還是 bot 領域）

## 🔗 相關 Issue

Follow-up to #1047 / #1052

---

⚙️ Cardinal × Zaious
