# PR #1077 Review — dreamline2 麟洋配 footnotes parity

> 給主人貼到 PR #1077 的 Approve review comment

---

## 建議 Review action

**Approve** ✅

---

## Comment body

LGTM @dreamline2 🙏 又一輪乾淨的 footnotes parity — 跟 #1075 同樣 pattern，6 語系（zh + en + ko + fr + ja + es）腳註齊一。

我這邊 verify 過全部 8 個 URL：

| Footnote | Source | Status |
|---|---|---|
| `[^1]` | CNA 東京男雙首金 | **200** ✅ |
| `[^2]` | Mirror 鏡週刊（34 分鐘決賽） | **200** ✅ |
| `[^3]` | Yahoo 體育東奧決賽 | **200** ✅ |
| `[^4]` | 維基王齊麟 | **200** ✅ |
| `[^5]` | 維基李洋（羽球） | **200** ✅ |
| `[^6]` | EN Wiki 2020 男雙 | **200** ✅ |
| `[^7]` | EN Wiki 2024 男雙 | **200** ✅ |
| `[^8]` | ELLE 李洋退役 | **200** ✅ |

zh-TW SSOT 從原本「參考資料」bullet list 改成 canonical `[^N]: [標題](URL) — 描述` 格式 ✅，內文也補了 8 個位置標註對位事實。巴黎 CNA 專稿 404 → 用英文奧運條目 `[^7]` 交叉的判斷也合理。

CI `review` workflow 紅燈跟 #1075 同樣 false positive（`en` 被當 invalid category，已知工具 bug），不擋 merge。

### 一個 minor observation（非 blocker）

李洋家庭背景段尾「一家人都與羽球緊密相連」引語標 `[^5]`（李洋維基）— 維基條目有家庭背景但「一家人都與羽球緊密相連」這句直引可能更貼合 `[^8]` ELLE 退役訪問的 source。整段 `[^5]` 涵蓋家族脈絡是 OK 的，只是如果未來想精準到引語層，可以考慮 swap。

⚙️ Cardinal × Zaious

---

## Review 過程紀錄

對齊 5/12「verify 實際內容才能寫結論」紀律：

1. **URL verify** 用 curl -IL follow redirect，8 個 source 全 200
2. **Diff inspection** 6 個檔案（zh-TW SSOT + 5 個語言）
3. **CI status** check-translation pass / review false positive（同 #1075 已知）
4. **Minor observation** [^5] vs [^8] 引語對位（不擋 merge）

跟 #1075 同樣 review pattern — dreamline2 在做 footnotes parity 系列工作，品質可信。
