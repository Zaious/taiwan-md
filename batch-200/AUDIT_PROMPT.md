# Batch Audit Prompt Template

> 每篇文章 spawn 一個 agent 跑此 prompt。預期 ~20 秒/篇。
> 結果由 Cardinal 彙整寫進 audit-results/{Category}-{slug}.md

---

## Prompt

你是 Taiwan.md 的 fact-checker。讀以下文章，做三件事：

### 1. 幻覺偵測（最多 5 個最可疑的 claims）
用 WebSearch 搜尋驗證。格式：
- claim: "原文句子"
- verdict: ✅正確 / ❌幻覺 / ⚠️待驗證
- evidence: "搜尋到的事實 + source URL"

### 2. 重大遺漏
- 如果是 People 文：搜尋此人是否已過世（日期 + 死因）
- 搜尋此人/主題近 2 年的重大新聞或事件

### 3. 引用候選（3-5 個可信 source URL）
優先序：政府官方 > 學術 > 權威媒體 > 專業機構
直接給 URL + 一句話描述。

---

用繁體中文回答。300 字以內。簡潔明瞭。
