# 台灣在國際標準中的標示問題 audit (P1, Society, perspective Y — **SOVEREIGNTY 核心議題**)

> **Cardinal Tier 判定**：**Tier A 嚴重重寫**（題不對文 — 標題承諾國際標準但 80% 寫開源 bug + 五大遺漏 + perspective 失衡 + 缺 sovereignty 框架對接）

## Fact verdicts

| Verdict | Claim | 修正 | Risk |
|---------|-------|------|------|
| ⚠️ | 「ISO 3166-1 自 1974 起就存在」 | TW 代碼確存在 ISO 3166-1，但「Taiwan, Province of China」short name 確切起始年份需查證；ISO 3166 第一版確 1974 發布 | MEDIUM |
| ✅ | bug 編號（Ubuntu / FreeBSD / Drupal / GitHub Issue）+ hackmd | 硬證據可驗證，幻覺風險低 | — |
| ⚠️ | 「WHO 常使用『Chinese Taipei』」 | 不精確。WHO 對台灣稱呼歷史複雜：2009-2016 觀察員身份用 CT，更早文件出現「Taiwan, Province of China」，2017 後幾乎不被列入。**單一化失真** | MEDIUM |
| ✅ | 「奧運『Chinese Taipei』」 | 對（1981 洛桑協議）但只一句帶過 | — |

## 🔥 重大遺漏（高 stake，本文最弱）

- ❗ **完全沒有 ISO 3166 機制本身的解釋**：ISO 3166-1 country name source 是 UN Terminology Bulletin，UN 跟 2758 走 — 這是「Province of China」標示的**根因**。不提根因 = 把問題講成單純軟體 bug
- ❗ **沒有聯合國第 2758 號決議**（1971/10/25）— 缺這條，讀者無法理解為何 ISO 標示如此
- **沒有 ICAO（民航組織）排除台灣的議題**
- **沒有 2024 年動態**：
  - 2024 巴黎奧運中華台北爭議
  - 2024 美國國務院 + 立陶宛 + 捷克 + 澳洲 + 荷蘭等對 **2758 決議「不等於對台灣主權的判決」新詮釋**
  - WHA 2024 台灣未獲邀
- **沒有護照封面 2020 變更**（"REPUBLIC OF CHINA" 縮小、TAIWAN 放大）
- **跨國公司標示爭議完全缺席**：航空公司（華航 / 國泰 / 達美被中國民航局施壓改標）、星巴克、ZARA、Gap、Marriott、Versace、Calvin Klein 等案例
- **沒有 PRC 對國際組織的施壓機制**（NGO 改名、學術期刊改作者單位、Apple 地圖、Google 商店地區）
- ❗ **缺 sovereignty preservation 框架對接** — 本應自然連到 MANIFESTO §主權的巴別塔

## ⚠️⚠️⚠️ Perspective 嚴重失衡（高度敏感）

- **單一立場**：從頭到尾以「Taiwan = 正確標示」「Province of China = 有缺陷」為前提，**未陳述爭議的多元立場**
- 中國「一個中國原則」立場為何（即使不認同也應陳述）— 缺
- 「中華台北」(Chinese Taipei) 是 1981 洛桑協議**兩岸共同接受**的妥協（雖在台常被批評矮化）— 完全沒提
- 「中華民國」與「台灣」兩種台灣內部立場差異 — 完全沒處理
- 「無法接受」「有缺陷」措辭雖引述他人，但作者未加距離 = 立場代言
- **g0v 社群被刻畫成單一英雄敘事**，未平衡呈現另一面（許多開發者認為應遵循 ISO 標準不另創分支）
- 文末「多元價值觀的體現」與整篇單一立場**自相矛盾**

## 引用候選

- ISO 3166 Maintenance Agency 官網 + UN Terminology Bulletin
- 聯合國第 2758 號決議原文（UN Digital Library）
- 中華民國外交部官網對 ISO / WHO / ICAO 立場聲明
- 中華奧會 1981 洛桑協議文件
- 美國國務院 2024 對 2758 決議聲明
- WHO WHA 歷年台灣參與紀錄
- BBC / Reuters / Bloomberg 2018 航空公司事件報導
- 行政院 2020/9/2 護照改版新聞稿

## Prose flag

- **塑膠句 ≥ 8 處 ⚠️⚠️⚠️**
  - 「牽動著政治與認同的敏感神經」/「持續不斷的討論與修正行動」
  - 「反映了數位時代的主權表達議題」/「認同、尊重與包容的深層議題」
  - 「數位時代多元價值觀的體現」雞湯結語
  - 結語整段（##結語）幾乎全是塑膠句
- **Cardinal Tier 判定**：**Tier A 嚴重重寫**
- **修補建議**：
  1. **大幅 expand**（補 2758 + WHO + ICAO + 跨國公司 + 護照 + 2024 動態）**或**
  2. 改標題「開源軟體中的台灣標示修正：g0v 社群案例」收斂題目以匹配內容深度
  3. 結語整段重寫（去塑膠化）
  4. 補 perspective balance section（中國立場 / 中華台北妥協 / 內部立場差異）並**對接 §主權的巴別塔**
