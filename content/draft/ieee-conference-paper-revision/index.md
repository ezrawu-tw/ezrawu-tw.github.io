---
slug: ieee-conference-paper-revision
copyright: true
title: "IEEE 短篇會議論文修稿全指南：MIPR 投稿實戰記錄"
date: 2026-05-26 00:00:00
updated:
tags:
  - LaTeX
  - IEEE
  - 論文寫作
  - 學術寫作
  - AI 協作
  - MIPR
categories:
  - 研究筆記
keywords:
description: "從 LaTeX 格式錯誤、廢話文學偵測、Limitations 策略、頁數壓縮，到多模態系統的四種審稿弱點防禦——一篇 IEEE MIPR 投稿的完整修稿紀錄，整理給未來的自己和有需要的人。"
top_img:
cover:
---

## 前言

這是一篇 IEEE MIPR 投稿的 conference paper 的修稿全記錄。論文題目是 *Beyond Semantic Distance: Fusing Physiological and Linguistic Signals for Multimodal Coordination Assessment in Cross-Disciplinary Design*，系統是 HRV + 臉部表情 + BERT 文字三模態的 multi-agent late fusion，用 Research-through-Design（RtD）方法論。

格式：`\documentclass[conference]{IEEEtran}`，6 頁硬上限，雙欄。

---

## 第一課：格式問題先處理

格式問題優先，因為視覺異常會讓審稿人或合作者誤以為論文水準有問題。

### Table caption 與 Figure caption 的差異

IEEE 規範是：
- **Table caption**：`TABLE I` + 標題用 small caps、置中、放在表格**上方**
- **Figure caption**：`Fig. 1.` + 一般字體、放在圖**下方**

IEEEtran 把 Table caption 渲染成 small caps 是正確的，不是搞錯。

Title Case 微調：依 IEEE Editorial Style Manual，逗號後新子句的首字要大寫、四個字母以上的介系詞要大寫。`with M4 Expanded into the Three...` 嚴格來說應該是 `With M4 Expanded Into the Three...`，但這是潤稿級別、非格式錯誤。

### Figure 浮動到奇怪位置

`\begin{figure*}[!t]` 是雙欄寬圖、浮動到頁頂，但宣告位置太晚，LaTeX 找不到合適空間，就擠到最後一頁夾在 References 中間。

**修法**：把整個 `figure*` 區塊**搬到第一次引用它的小節之前**。若仍跑掉，把 `[!t]` 改成 `[!htbp]`，讓 LaTeX 多一些位置可選。

### 未定義的 `\ref`：最常見卻最嚴重的錯誤

```
LaTeX Warning: Reference `tab:mapping' on page 2 undefined on input line 318.
```

文中宣告了 `\ref{tab:mapping}` 但**整篇沒有對應的 `\label{tab:mapping}`**，PDF 顯示為 "Table ??"。

這是個很糟的錯誤——讀者點進來會立刻發現論文有破洞。

**原則**：寫論文時，每個 `\ref{}` 都要有配對的 `\label{}`。務必兩遍編譯 + grep 全文檢查。

**該補表還是該刪？** 如果這張表是方法論的核心（case study 的數字就是靠這張表算出來的），絕對要補，不要為了省事刪。可以做反推驗證確認權重合理後再補。

---

## 第二課：廢話文學偵測

論文寫久了會在很多地方出現「廢話文學」——句子讀起來通順，但實際上沒貢獻新資訊或迴避了問題。

### 徵兆 1：「Can a system be constructed...?」型 RQ

> "Can a unified real-time architecture be constructed in which physiological (HRV), facial-expression, and text-emotion channels are processed by independent analytical agents and fused without coupling the modalities at the model level?"

問題：答案幾乎一定是 yes（不然論文不會存在）。這是 feasibility framing，不是研究問題。而且「fused without coupling at model level」是**設計選擇**，不是研究問題。研究問題應該是你**不知道答案**的東西。

### 徵兆 2：「向未來借意義」

> "The architecture is reusable and provides a foundation for subsequent large-scale studies..."
> "...is a subsequent direction that the architecture was designed from the outset to support."

審稿人會想：「那如果後面沒人做大規模研究，你的論文就沒價值嗎？」論文的價值不應該靠未來的研究來背書。

### 徵兆 3：「rather than 道歉句」

> "...a deep case study aimed at operational viability and architectural stability, **rather than** through large-sample statistical inference."

「rather than」天生帶防禦感——你在強調自己「沒做」什麼。改成正面表述：

> "...examined through a deep case study **that yields** a high density of observable streaming behavior across modalities, surfacing operational details that large-sample comparisons typically average out."

同樣的事實，語氣從「我承認我沒做大樣本」變成「我選 deep case 是因為它能看到別的方法看不到的東西」。

### 徵兆 4：元評論（meta-comment）

> "In Table~\ref{tab:arch}, the three M4 channels are deliberately displayed as visually equal sub-columns **to reflect the paper's title claim**..."

讀者不關心「你為什麼這樣畫表」，只關心「這個系統是什麼」。

### 徵兆 5：「leaving X without Y」循環論證

> "...has not been integrated..., **leaving subsequent larger studies without a common system foundation**..."

「沒有 X 所以後續研究缺少 foundation」= **我做的事還沒人做過，所以我做了它**。應該升級為：「沒有 X 導致我們無法回答 Y 問題」。

---

## 第三課：Reviewer 是對抗性的——Limitations 不要開獨立段落

這是整個修稿過程最大的體會。

原本把 Limitations 段寫得很詳細：四個 layer（measurement / model / context / sample），每個都坦承哪些沒做、哪些不夠嚴謹。

教授看完一句話：**「整段拔掉。容易被抓漏洞。」**

道理是：短篇會議論文 6 頁的篇幅，你寫 Limitations 不是在「展示嚴謹」，而是在**主動提供 reviewer 一份打你的清單**。

### 正確的處理方式：把限制內化到技術描述的當下

- 時間對齊用 reception timestamp → 在 III.B 串流管線那段**就**寫清楚，定位成「architectural simplification, planned refinement for future iterations」。不要等到 Limitations 才講。
- 設計師戴眼鏡可能讓 DeepFace 誤判 → 在 Table II 的 caption 加 `†` 小註腳，**一句話**帶過，把「paired-control experiment」移到 Conclusion 的 future work 句。

差別：**reviewer 看到「在技術描述當下就交代」的限制，會覺得作者考慮周到；看到「另設一節列舉自己缺點」的限制，會抄下來當拒稿理由**。

### 三個弱點的分散處理

| 弱點 | 處理位置 |
|---|---|
| n=1 單案例 | Introduction 末段：「single-pair architectural proof-of-concept, not population-level claim」 |
| W 權重未經實證校準 | Table II 說明：「Weights are theoretically derived; calibration is future work」 |
| 99.8 BPM 高心率無 baseline | Discussion V-A：「session-state indicator; future work will incorporate pre-session baselines」 |

三個弱點分散在三個不同章節，沒有獨立段落讓人集中火力，但該交代的點都交代了。

### 學姊建議 vs. 教授禁令的衝突

學姊建議加 Limitations 章節，教授明確禁止。**教授是論文掛名指導，指示優先**。

但學姊的擔心是合理的，處理方式：**論點不獨立成節，但散在內文裡 hedge**：

```latex
With respect to RQ2, the present work provides an architecture-level
demonstration that cross-modal disagreement is renderable as a first-class
diagnostic; quantifying the added information value of fusion over single
channels...requires multi-pair calibration and is left to future work.
```

這是「future-work qualifier」單句，不是 Limitation 章節。學姊擔心的問題被回答了，但沒違反教授禁令。

---

## 第四課：頁數壓縮的優先順序

從 7 頁壓到 6 頁，**字體調整是最後手段，不是第一手段**：

1. **無損改寫（prose tightening）**——「in order to」→「to」、「It is worth noting that X」→「X」
2. **Caption 內容搬到內文**——圖表 caption 應該 ≤ 2 行，超過的描述移到正文
3. **刪重複圖**——如果兩張圖有明顯內容重疊，刪掉較弱的
4. **拔掉 Limitations 段**（見第三課）——威力最大，省約 25 行
5. **合併重複引用**——同主題三篇文獻取最強的一篇
6. **刪次要文獻**——與教授確認後，從 23 篇刪到 17 篇
7. **References 排版壓縮**——`\scriptsize` + `\setlength{\itemsep}{-2pt}`
8. **最後才動字體**

每改完一輪都要重新 compile + 看最後一頁，不能只看頁數。有時頁數沒變但 layout 改了，新的洞跑出來。

### 判斷原則

每次想加一段話之前先問：

> 「這句話是在支撐論文的核心主張，還是只是在描述系統？」

描述系統的句子可以刪；支撐核心主張的句子必須留。

---

## 第五課：多模態系統的四種典型審稿攻擊

審稿人在看多模態/HCI/Agent 系統論文時，有固定的攻擊面。提前準備好答案。

### 攻擊一：時間對齊

「你的兩個訊號通道速率不同（HRV 1Hz，影像 0.67Hz），你怎麼對齊？用伺服器接收時間，不就是把不知道幾秒前的生理事件配上現在這幀畫面？」

**對策**：在 III.B（串流管線）**主動**揭露：「目前用 server reception timestamp，屬於 architectural simplification；generation timestamp 同步是規劃中的 next iteration。」放在技術描述當下，reviewer 會覺得作者考慮周到。

### 攻擊二：模態 bias confound

「設計師受試者戴眼鏡，DeepFace 在眼鏡遮擋下系統性誤判 `angry`。你說的『跨模態方向對應』，有沒有可能只是模型 bias 配上自己？」

**對策**：
- 把「跨模態對應」的語氣**主動弱化**為「preliminary phenomenological observation, not confirmatory evidence」
- Table II caption 用 `†` 承認（一句話）
- Conclusion future work 列上「paired-control experiment（同受試者戴/不戴眼鏡）」

這樣 reviewer 看到「承認 + 有計劃排除」，反而會給高分。**自相矛盾（IV.C 信誓旦旦講方向對應，V.C 又自承眼鏡 bias）才是最糟的**。

### 攻擊三：「兩個算多模態嗎」

系統只用 2 個 channel，reviewer 質疑「Multimodal 是否言過其實」。

**不要訴諸權威**（「學術界定義 ≥2 就算」），而是**訴諸方法論**：

> "Multimodal fusion 的核心方法論挑戰不是來自模態數量，而是來自模態間的 heterogeneity。連續低取樣率的生理時序 + 離散高取樣率的視覺影格，於資料結構、取樣頻率、時序解析度上的差異，本身就構成融合架構的核心問題。兩個 heterogeneous channel 已是多模態研究的最小完整實作。"

放在 Related Work 的 Multimodal Fusion 段。

### 攻擊四：架構為什麼是 Agent 而不是 end-to-end

「如果只是 HRV + Face 融合，為什麼不直接訓一個 multi-input neural network？搞 Agent-to-Agent 不是過度設計嗎？」

**對策**：在 III.A 系統概覽明確說設計理由是 **modular maintainability**——各模態可獨立替換/擴充/除錯，新模態加入只需新增一支 analytical agent，不影響其他元件。換句話說，這是**研究系統**的架構，不是**生產系統**的最佳化。

---

## 第六課：LaTeX 細節

### Em dash 不要用 sed 一次清光

某一輪我說「拿掉所有奇怪的 `---`」，結果用 `sed s/---//g` 全部清掉，產生了一堆爛句：

```
challenges HRV signal noise from bodily motion  (原本是 challenges---HRV signal noise)
team the moment when affective friction tends   (原本是 team---the moment when...)
```

`---` 在英文裡是 em dash，用來「插入子句」或「強調轉折」。直接刪掉就會留下兩個鬆散的名詞，文法壞掉。

正確處理：**逐個讀 context**，根據語意換成適當標點：
- 插入子句 → 逗號：`challenges---X` → `challenges, including X`
- 強調轉折 → 改寫完整子句：`cues---yet analysis` → `cues, although analysis`
- 因果關係 → 冒號：`converge---platform reports` → `converge: the platform reports`
- 補充說明 → 分號或分句

而且要分清楚：
- 內文 em dash（`---`）→ 該清的就清
- **數值範圍** en dash（`0.04--0.15 Hz`）→ 保留
- **複合詞** en dash（`engineer--designer`）→ 保留
- **表格內**作為空格的 `---` → 絕對保留
- **References 頁碼**（`pp. 121--132`）→ 絕對保留

### `\hyphenation{}` 防禦性設定

Preamble 加這段，零成本換取「任何改動都不會出現難看斷字」的保證：

```latex
\hyphenation{
  par-tic-i-pants
  par-tic-i-pant
  WebSocket
  AppleWatch
  DeepFace
  RMSSD
  SDNN
}
```

給連字號的條目告訴 LaTeX「只能在這些位置斷字」；**沒給連字號的條目**（`RMSSD`、`SDNN`）告訴 LaTeX「絕對不要斷這個字」。

### `\vspace` 不要超過 `-6pt`

負 vspace 超過 `-6pt` 容易把表格底部撞到下一段文字。調整間距用 `-4pt` 比較安全。

### Compile loop SOP

```bash
cd <paper_dir>
rm -f main.aux main.bbl main.blg main.log main.out main.pdf
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex 2>&1 | grep -E "Output|Error"
pdftoppm -jpeg -r 100 main.pdf preview
```

兩次 `pdflatex` 因為 cross-reference 需要第二 pass 解析。每輪結束都要看第一頁（標題/Abstract）和最後一頁（References 有沒有溢出）。

**Underfull `\hbox` 警告可以忽略**（只是 LaTeX 對行寬不滿意）；**Overfull `\hbox` 是真實溢出**，要處理。

### Cross-reference grep SOP

刪任何 `\section` 或 `\subsection` 前，先：

```bash
grep -n "sec:被刪的label" main.tex
```

把所有 cross-reference 列出來，逐一處理（刪句子、改寫成中性描述、移到 future work）。

---

## 第七課：審稿意見要先 grep，不要先改

審稿意見裡，**有一半問題可能在你的 LaTeX 原始碼裡根本不存在**。

例子：
- 「公式 (1) 的變數寫成 `$SSD$`，應該是 `$RMSSD$`」→ 原始碼一直是 `\mathrm{RMSSD}`，渲染出來也是 RMSSD
- 「向量 `p` 的方括號漏掉，變成 `Pangry, Pdisgust Prear Phappy...`」→ 原始碼是 `\mathbf{p} = [p_\text{angry}, p_\text{disgust}, p_\text{fear}, ...]`，完整正確

這些錯誤大概是 reviewer 看的是 PDF 文字提取版本（OCR 把 `p_\text{disgust}` 認成 `Pdisgust`、把 `fear` 認成 `rear`）。

**教訓**：每個 reviewer 意見進來，先 grep 原始碼確認問題是否存在。如果不存在，在回信裡說明「這個問題在我們的版本不存在，可能是 OCR/版本差異」。誠實比盲目修改更有價值，**盲目修改有時候會把對的改錯**。

---

## 第八課：AI 痕跡清理

### 常見的 AI 寫作痕跡

| 類型 | 例子 | 問題 |
|---|---|---|
| 過度副詞 | `Crucially,` `Moreover,` `Notably,` | ChatGPT/Claude 招牌開頭副詞 |
| 累贅強調 | `in its own right` `first and foremost` | 讀起來翻譯腔 |
| 雙破折號夾注 | `term---definition---continues` | 在列舉或斷句時用 `---` 顯做作 |
| 過度斜體 | 列舉時每個項目都 `\emph{}` | 正常英文只在「術語首次定義」時斜體 |
| 雙重強調 | `\textit{``a bit uneasy''}` | 引號已標示引用，再加斜體是過度強調 |

### 哪些斜體要保留？

正當的學術用法：
- 術語首次定義（`\emph{modality-consistency flag}`）
- UI 標籤引用（`\emph{Consistent}`、`\emph{Inconsistent}`）
- 引用論文標題
- 系統角色名稱（`\emph{Orchestrator Agent}`）

**判斷原則**：斜體一次就好，第二次出現同一術語就不用再斜體。

---

## 第九課：對齊 Special Session

### 為什麼引用 special session 自家論文

不是討好，是訊號。審稿者大多是該會議系列的常客，看到引用自家系列，會更願意 accept。MIPR 三篇連年覆蓋（2022/2023/2025）是相對自然的方式。

### 不要把已對齊的東西弄壞

MIPR SS2 的三條 CFP bullet 與 Discussion V.A/B/C 標題逐字對應——這是最有效的訊號。但在某一輪壓 6 頁時，我把 V.C 標題從 SS2 CFP 逐字版縮短了，等於主動把這個訊號自己刪掉了。

**對齊 special session 最有效的修正常常是「不要把已對齊的東西弄壞」**，而不是加新東西。

### RQ 措辭和你能提供的證據要在同一個答案類別

```diff
- "...do they yield coordination diagnostics that are richer
-  than what any single channel surfaces?"
```

"richer than" 需要量化定義，但 n=1 個案研究無法提供量化比較。

```diff
+ "...can the resulting cross-channel agreement or disagreement
+  reveal coordination signals that any single channel,
+  considered alone, would not surface as a first-class diagnostic?"
```

核心主張沒弱化，但論證負擔大幅降低——案例研究直接可回答，不需要 ablation study。

---

## 總結：給未來的自己

如果再寫一篇 IEEE 短篇會議論文，我會：

1. **第一稿不寫 Limitations 段**。把每個限制直接內化到技術描述當下。
2. **三點貢獻寫成完整句子**，每點開頭 `we propose / we transform / we conduct`，不要寫成名詞 fragment。
3. **第一輪就建立 6 頁的紀律**。每加一段問自己「有空間嗎」，而不是寫到 7 頁才回頭壓。
4. **圖表 caption 最多 2 行**，方法論都放在正文。
5. **HRV 標準引用** Task Force 1996 *Circulation* 不要忘。BERT 要引 Devlin 2018 原論文。Russell circumplex 1980 要引。這些是「不引就被抓」的 foundational 引用。
6. **多模態系統的四個 logic-defense pattern** 從第一稿就寫好對策。
7. **跟 AI 協作時**，每輪先 diff、後 compile、再 review，順序不要顛倒。不要假設你記得的版本是當前的。

6 頁限制不是束縛，是壓力測試——被迫每句話都要做事，反而把論文寫得更精準。

---

*寫於 2026 年 5 月，投稿 IEEE MIPR 2026 SS2 期間。*
