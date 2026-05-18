# PR #1075 Review — dreamline2 yoga-lin footnotes parity

> 給主人貼到 PR #1075 的 Approve review comment

---

## 建議 Review action

**Approve** ✅

---

## Comment body

LGTM @dreamline2 🙏 footnotes parity + 失效連結替換做得乾淨。

我這邊 verify 過四個 URL：

| URL | Status |
|-----|--------|
| 原 `[^1]` Apple Daily | **404** ✅ 確實失效 |
| 新 `[^1]` Mirror Media（同日同事件） | **200** ✅ 有效 |
| 原 `[^11]` UDN money | **404** ✅ 確實失效 |
| 新 `[^11]` TVBS 2024 | **200** ✅ 有效 |

ko 版本補完截斷段落（「그 몸이」→ 完整收束 + 더 읽기 + footnote [^1]-[^16]）特別讚 — 韓文之前 footnote 定義缺漏的 silent break 一次處理乾淨。5 語言（en/ja/ko/es/fr）跟 zh-TW SSOT 對齊也做到位。

CI `review` 那個 failure 看起來是 bot「Comment review result」step infrastructure issue（不是 PR 內容問題），可以忽略。

⚙️ Cardinal × Zaious

---

## Review 過程記錄

樞機師 maintainer review 跑了：

1. **Fetch PR metadata + diff via GitHub API**（local checkout 卡 git permission 但不影響）
2. **URL verify** 用 curl HEAD + redirect follow
3. **Diff inspection** 6 個檔案的 patch（zh-TW SSOT + 5 個語言版本）
4. **CI 狀態確認** check-translation pass / review bot infra fail（不擋）

對齊 5/12 「verify 實際內容才能寫結論」紀律：4 個 URL claim 都實際 curl 過。
