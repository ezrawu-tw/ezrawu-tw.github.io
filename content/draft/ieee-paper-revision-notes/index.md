---
slug: ieee-paper-revision-notes
copyright: true
title: "論文改稿筆記：Beyond Semantic Distance 的論述精準化"
date: 2026-05-26 00:00:00
updated:
tags:
  - 論文寫作
  - 多模態情感運算
  - 跨領域協作
  - HRV
  - 學術寫作
categories:
  - 研究筆記
keywords:
description: "針對〈Beyond Semantic Distance〉草稿做版本比較與論述診斷，從教授視角檢視核心問題，提供 Introduction 末段與 Discussion 三節的具體中英改寫版本。"
top_img:
cover:
---

## 背景

針對手上兩個版本的論文草稿（V1 = `main(4).pdf`，V2 = 修訂版）做版本比較與論述診斷，目標是讓讀者能在 30 秒內抓到這篇論文的核心問題。

---

## 一、兩版差異盤點

### V1 多出來的內容

1. **Abstract 最後一句**：明確加上「single-pair architectural proof-of-concept」的範圍宣告
2. **RQ2 寫法不同**：V1 強調「first-class diagnostic」
3. **Related Work II.B**：V1 多了一整段關於 retrospective bias、social desirability、Kihlstrom 引用的論述
4. **III.C Late Fusion**：V1 詳細解釋四象限與 Russell circumplex 的對應
5. **V.B Discussion**：V1 多了 future work 邊界的說明

### V2 的優勢

- 結構較緊湊，圖表排版較順
- 沒有 V1 那些「自我設限」的長句，閱讀流較快

### 結論：V1 整體較佳

V1 在三個關鍵位置補上了「學術防禦」：proof-of-concept 的明示、semantic distance 的理論基礎、RQ2 的 future work 邊界。但 V1 也染上一個毛病：**論述開始繞**，給人「作者很心虛、一直自保」的觀感。

---

## 二、教授視角：核心問題診斷

如果目標是「讓讀者在 30 秒內抓到這篇的重要問題」，現有版本有四個結構性問題：

### 問題 1：核心 claim 被埋在第三段才出現

現在 Abstract 的順序：背景 → 三個 modality 的現況 → 我們提出系統 → 架構細節 → case study 結果 → 自我設限。讀者要讀到第 5 句才知道這篇真正主張的是什麼。

→ 建議改成**倒金字塔**：第一句就把 claim 講完。

### 問題 2：「Beyond Semantic Distance」標題承諾沒在 Abstract 兌現

標題用了帶有強烈論證感的詞（beyond），但 Abstract 沒有清楚定義「semantic distance 是什麼、為什麼要 beyond」。

### 問題 3：三個 RQ 與兩個 contribution 的對應關係不清

讀者很難一眼看出「哪個 RQ 對應哪個 contribution、由哪個章節回答」。

### 問題 4：單一 case study 的論證強度被過度防禦

V1 在 Abstract、Introduction、Discussion V.B 三個地方都重複「single-pair proof-of-concept, not statistical prevalence」。寫三次反而讓讀者懷疑論文證據很弱。

→ 建議只在 Introduction 末段講一次，講得乾淨俐落，Discussion 不要再道歉。

---

## 三、Abstract 改寫示範

> This paper argues that the disagreement between semantic self-report and physiological/visual signals during cross-disciplinary collaboration is itself a coordination diagnostic, not measurement noise to be averaged away. We define *semantic distance* as the gap between what participants articulate in retrospective interview and what they physiologically and visually expressed in-session — a gap that text-based coordination assessment, the dominant paradigm for engineer–designer teams, cannot recover. To render this gap observable, we propose a real-time multi-agent system that streams HRV, facial expression, and BERT-based interview-text emotion through Google's Agent-to-Agent (A2A) protocol, fuses them via a replaceable late-fusion rule into a four-state affective output, and externalizes the merged state through a bio-inspired wing device. The architectural contribution is the elevation of the modality-consistency flag — the agreement or disagreement among the three independent channels — from an internal feature to a first-class diagnostic output. In a deep case study with an engineer–designer pair, the designer's session showed a cross-modal divergence (facial: anxious 87.8% vs. text: calm 71.2%) that no single channel would have surfaced; we present this as an architectural proof-of-concept that the diagnostic class is observable at all.

**改寫策略**：開門見山 → 定義 semantic distance → 架構貢獻 → 證據 → 一次性說明範圍。沒有重複自保語句。

---

## 四、Introduction 末段改寫

### 英文版

> This work makes one architectural and one empirical contribution, jointly answering the three RQs above.
>
> **Architectural contribution (addresses RQ1 and RQ2).** We propose a real-time, agent-based late-fusion architecture in which HRV, facial, and BERT-based text-emotion channels are processed by independent analytical agents and reconciled by an Orchestrator Agent through Google's Agent-to-Agent (A2A) protocol. The innovation is not the fusion itself — late fusion is well-established — but the elevation of the **modality-consistency flag** to a first-class system output: rather than collapsing the three channels into a single fused score, the architecture preserves and surfaces their disagreement as a diagnostic. This makes RQ1 testable in a real two-person setting and operationalizes RQ2 by exposing cross-channel agreement and disagreement as a directly readable system output.
>
> **Empirical contribution (addresses RQ3).** We use the term *semantic distance* to refer to the discrepancy diagnosable from text-based self-report alone — the dominant paradigm in coordination assessment for cross-disciplinary teams. Through a deep case study with an engineer–designer pair, we show that a purely semantic reading would classify the designer's session as calm/relaxed (71.2%), whereas the addition of physiological and visual channels reclassifies it as anxious (50.7%) and triggers a modality-inconsistency flag. The 71.2% / 50.7% gap is the operational content of *beyond semantic distance*. The empirical content is presented as a single-pair proof-of-concept; statistical prevalence across pairs is left to future work.

### 中文版

> 本研究做出一項架構性貢獻與一項實證性貢獻，兩者共同回應前述三個研究問題。
>
> **架構性貢獻（回應 RQ1 與 RQ2）。** 我們提出一套即時、基於 agent 的後期融合架構：HRV、臉部、以及基於 BERT 的文字情緒三個通道，分別由獨立的分析型 agent 處理，並由一個 Orchestrator Agent 透過 Google 的 A2A 協定加以整合。本架構的創新並不在於「融合」本身，而在於將**模態一致性旗標**提升為系統的第一級輸出：架構不是將三個通道塌縮為單一融合分數，而是保留並顯化它們之間的不一致，作為一項診斷訊號。
>
> **實證性貢獻（回應 RQ3）。** 我們以**語義距離**一詞指稱「僅由文字自陳即可診斷出的落差」。透過一組工程師–設計師配對的深度個案研究，我們顯示：純粹以語義通道閱讀，會將設計師該場次判為 calm/relaxed（71.2%）；但一旦納入生理與視覺通道，同一場次便被重新判讀為 anxious（50.7%），並觸發模態不一致旗標。71.2% / 50.7% 這個落差，就是「beyond semantic distance」的操作性內涵。本實證以單一配對作為概念驗證；跨配對的統計普遍性留作未來工作。

### 改寫重點

- 第一句就鎖死對應關係：「one architectural and one empirical contribution, jointly answering the three RQs」
- 每個 contribution 段落標註對應 RQ
- 把 semantic distance 的定義往前提
- proof-of-concept 設限只講一次、放在末句
- 把 71.2% / 50.7% 數字搬到 Introduction，讓讀者進入 Related Work 前就抓到 punch line

---

## 五、Discussion 三節標題與首句改寫

### V.A → 回應 RQ1

**英文：**

> **A. RQ1: Wearable HRV is operationally viable as a real-time affective channel in two-person collaboration.**
>
> The pipeline streamed HRV throughout the pre-consensus ideation phase via a wrist-worn sensor without loop interruption, and both participants yielded continuously computable time-domain features under realistic motion, speech, and device-interaction load. E01's SDNN of 46.61 ms falls within the normative range for an active adult, while D01's markedly lower RMSSD of 6.17 ms is consistent with sustained sympathetic dominance rather than motion artifact — D01's HRV co-varied with the facial agent's anxious reading, whereas a noise-driven signal would fluctuate without directional consistency across modalities.

**中文：**

> **A. RQ1：穿戴式 HRV 在二人協作情境中具有作為即時情感通道的操作可行性。**
>
> 在 pre-consensus ideation 階段中，本系統以腕戴式裝置持續串流 HRV，整段流程無中斷；兩位受測者在實際的身體動作、語音、與裝置操作負載下，皆可被連續計算出時域 HRV 特徵。E01 的 SDNN 為 46.61 ms，落在活躍成年人的常模範圍內；D01 的 RMSSD 僅 6.17 ms，且與「持續性交感神經主導」的解讀一致，而非單純的動作雜訊——D01 的 HRV 走向與臉部 agent 判讀為 anxious 的結果同向變化，雜訊驅動的訊號不會在不同模態間呈現一致方向。

### V.B → 回應 RQ2

**英文：**

> **B. RQ2: Cross-modal disagreement is renderable as a first-class diagnostic, not only an analyst-side interpretation.**
>
> The present architecture keeps the channels decoupled at the model level, so the modality-consistency flag — the agreement or disagreement among independent channels — is emitted as a system output alongside the fused state, rather than collapsed into a single score. We present this as an architecture-level demonstration that the diagnostic is observable; quantifying the added information value of fusion over single channels requires multi-pair calibration and is left to future work.

**中文：**

> **B. RQ2：跨模態的不一致本身可被渲染為第一級診斷輸出，而非僅止於分析者的事後詮釋。**
>
> 本架構讓各通道在模型層面保持解耦，使**模態一致性旗標**得以作為系統輸出，與融合後的狀態並列輸出，而不被塌縮為單一分數。本研究將此呈現為架構層級的概念驗證；至於融合相對於單一通道在資訊量上究竟多出多少，則需要多配對校準，留作未來工作。

### V.C → 回應 RQ3

**英文：**

> **C. RQ3: The temporal gap between in-session and retrospective signals is itself an informative observable.**
>
> By treating the in-session physiological/visual signals and the retrospective text-based self-report as outputs of independent agents fused at the granularity of *same participant, same phase*, the platform emits a modality-consistency flag whenever the two diverge. The D01 session is the concrete instance: the linguistic channel returned calm/relaxed (71.2%) while the physiological and visual channels reclassified the session as anxious (50.7%). Rather than reconciling this divergence away as measurement error, the architecture preserves it and surfaces it as a coordination diagnostic.

**中文：**

> **C. RQ3：現場訊號與回溯性訊號之間的時間落差，本身即為一項具有資訊量的可觀察變項。**
>
> 本平台將現場的生理／視覺訊號與事後的文字自陳，視為各自獨立 agent 的輸出，並在「同一受測者、同一階段」的粒度上加以融合；只要兩者出現分歧，平台即發出模態一致性旗標。D01 場次即為具體實例：語言通道回傳 calm/relaxed（71.2%），而生理與視覺通道則將該場次重新判讀為 anxious（50.7%）。本架構並未將此分歧視為量測誤差而加以「調和」，而是保留並將其顯化為一項協作診斷。

---

## 六、結構對齊檢查表

改完後，整篇論文「Abstract → Introduction RQs → Introduction Contributions → Discussion 標題」應該形成一條對齊的鏈：

| 位置 | RQ1 | RQ2 | RQ3 |
|---|---|---|---|
| Intro RQ 段 | real-time feasibility | semantic–physiological fusion | in-session vs. retrospective |
| Intro Contribution 段 | Architectural | Architectural | Empirical |
| Discussion 標題 | V.A | V.B | V.C |

審稿人或讀者在任何一個位置 drop in，都能立刻定位回另外兩處。

---

## 七、關鍵詞中譯對照備忘

| 英文 | 採用譯法 | 備註 |
|---|---|---|
| late fusion | 後期融合 | 也可譯「晚期融合」，需全文統一 |
| modality-consistency flag | 模態一致性旗標 | 也可譯「模態一致性標記」 |
| first-class output / diagnostic | 第一級輸出 / 第一級診斷 | 中文無完全對應習慣譯法 |
| proof-of-concept | 概念驗證 / 保留英文 | 兩種皆可 |
| semantic distance | 保留英文 | 論文標籤式概念，建議不中譯 |

---

## 八、核心改稿策略

1. **倒金字塔**：把最重要的 claim 放在最前面，不要讓讀者讀到第三段才知道論文在主張什麼
2. **顯化對應**：用標題與粗體把「RQ ↔ Contribution ↔ Discussion section」三層對應關係寫死
3. **設限只講一次**：proof-of-concept 的範圍說明只在 Introduction 末段宣告一次，Discussion 不再重複
