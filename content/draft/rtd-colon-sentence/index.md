---
slug: rtd-colon-sentence
copyright: true
title: "論文寫作筆記：RtD 引用後的冒號句該怎麼接"
date: 2026-05-26 00:00:00
updated:
tags:
  - 論文寫作
  - 學術寫作
  - Research-through-Design
  - 英文修辭
categories:
  - 研究筆記
keywords:
description: "一個小段落、一個冒號，牽出三個寫作問題：術語沒鋪陳、主詞跳接、語意斷層。記錄修改前後的版本與思考過程。"
top_img:
cover:
---

## 起因

在寫一篇論文的 *Validation Design* 小節時，初稿是這樣寫的：

> Our validation follows the Research-through-Design (RtD) tradition [17]: a system at the stabilization phase is examined through a deep case study that yields a high density of ob...

讀起來覺得怪，特別是 `[17]` 後面那個冒號接的句子。把這段丟給 Claude 看，得到了一些有用的診斷與改寫建議，整理在這篇。

## 問題在哪裡

冒號後面接 "a system at the stabilization phase is examined..." 有三個問題：

**1. `stabilization phase` 沒有先說明**

RtD 傳統裡並沒有一個眾所周知、叫做 "stabilization phase" 的階段。讀者會疑惑：這是哪來的階段？是 RtD 本身的階段，還是作者自己研究流程的某個階段？術語直接丟出來，沒有鋪陳。

**2. 冒號用法暗示「接下來是 RtD 的定義或核心做法」**

但實際接的卻是研究的具體操作，語意上有斷層。冒號前後的邏輯關係被打斷了。

**3. 主詞跳得太快**

從「我們的驗證遵循 RtD 傳統」直接跳到「一個處於穩定化階段的系統被檢視」，中間缺一個橋接。被動語態又讓主詞模糊化，讀者不確定誰在做這件事。

## 三種改寫方向

### 方向一：保留冒號，改主動語態、統一主詞

> Our validation follows the Research-through-Design (RtD) tradition [17]: **we examine a system that has reached the stabilization phase** through...

主詞一致（we → we），讀起來順。

### 方向二：拆成兩句，把 stabilization phase 解釋清楚

> Our validation follows the Research-through-Design (RtD) tradition [17]. **Once our system reached a stable state**, we examined it through...

避免在冒號後立刻丟術語，改用自然語言描述狀態。

### 方向三：更貼近 RtD 文獻常見講法

> Following the Research-through-Design (RtD) tradition [17], we examine our stabilized system through...

用分詞片語開頭，整句更緊湊，也更接近這個領域常見的寫法。

## 帶走的心得

冒號在學術寫作裡常被當成「進一步說明」的工具，但它對前後文的邏輯一致性要求其實很高。冒號前是一個 claim，冒號後最好是：

- 對 claim 的**定義**、
- 對 claim 的**展開或例子**、
- 或對 claim 的**直接後果**。

如果冒號後是「我們自己研究的具體操作」，通常更適合分成兩句，或者用 "Following X, we..." 這種分詞結構。

另一個小心得：**自己造的術語要先鋪陳**。"stabilization phase" 如果是這篇論文自己定義的概念，就要在它第一次出現時加一句說明；如果是引用文獻裡的概念，就要在 cite 的位置講清楚。不能假設讀者跟你一樣熟悉自己的研究脈絡。
