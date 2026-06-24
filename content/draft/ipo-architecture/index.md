---
slug: ipo-architecture
copyright: true
title: "「老師說，你寫的是商標」——從被修正到被要求 IPO 的完整過程"
date: 2026-05-26 00:00:00
updated:
tags:
  - LaTeX
  - 學術寫作
  - 架構設計
  - 論文筆記
  - 系統設計
categories:
  - 研究筆記
keywords:
description: "老師說我的系統架構圖「寫死了」未來無法替代——這篇記錄我怎麼從那句話，把架構圖重構成 IPO 規格表的完整過程，包括 LaTeX 範本與各種改寫細節。"
top_img:
cover:
---

## 起點：那句聽不懂的評語

老師看完我精心繪製的系統架構圖（一張標著「Frontend / Backend / Orchestrator / 五個 Agents / Database」方塊圖），說了三句話：

> 「PWA 是商標」
>
> 「你沒有把系統架構圖變成可以對應到技術模組，或 IPO（Input / Process / Output）」
>
> 「這樣未來無法替代的選項就寫死了」

我當下只能接受第一句字面意思，後面兩句完全是電話。我跑去學姐解釋我的理解，「他大概是想要我寫更底層的語言，好讓每件語言互通吧」——後來驗實這個理解**方向對但不精準**。

這篇文章記錄我怎麼從那句誤解，一路走到補完整張符合 IEEE 投稿可用的 IPO 規格表，包括 LaTeX 範本與各種改寫細節。

## 老師其實在說什麼

PWA 嚴格說不是被認定商標，是 Google 在 2015 年提出的技術概念。但老師說「商標」的精神是對的——**它代表了某個特定的產品**。

更核心的問題是：我的架構圖**幾乎每一格都是品牌/產品名**：

| 我寫的 | 老師指的問題 |
|---|---|
| PWA、Next.js、Chart.js | 這是「前端技術選擇」，不是「前端要做什麼」 |
| FastAPI、Node.js | 這是「後端框架」，不是「後端的職責」 |
| A2A | 這是 Google 特定協議名稱 |
| NumPy + FFT | 這是「工具」，不是「HRV Agent 的 IPO」 |
| DeepFace + OpenCV | 同上 |
| BERT + Hugging Face | 同上 |
| SQLite + WAL | 這是「資料庫產品」，不是「儲存層規格」 |

老師說「寫死了」未來無法替代」就是這個意思——5 年後 PWA 被淘汰、A2A 沒人用、SQLite 換成 PostgreSQL，**整張圖就要重做**。因為我寫的是「實體」，不是「架構」。

## 一個讓我徹底大悟的比喻

我跟老師說，「我要用 iPhone 來拍影片」。

老師說，「不對，你要說『我需要一個可攜式影像捕捉裝置，輸入是場景光線，輸出是數位影像檔』，這樣有天 iPhone 換了你還能換 Android」。

問題不是「用什麼底層語言」，而是**抽象層級**。架構圖應該描述「做什麼」（What），而不是「用什麼做」（How with which brand）。

## 老師給我的範本

老師給我看了一個範例表格。範例本身是一個 HRV — 羽毛裝置的完整系統 IPO 解讀，但**形式**才是重點：

- 表頭顏色分區
- 三欄：**Module / Component** | **Function / Processing Method** | **Output Result**
- 四行：**Input** | **Processing** | **Output**
- 每一格都要填滿

差異在哪：

| 一般方塊圖 | IPO 規格表 |
|---|---|
| 視覺上好、好看 | 規格上好、可審視 |
| 每個模組一段話 | 每個模組一張表，可以**逐格檢查有沒有缺漏** |
| 比較像 architecture diagram | 比較像 specification sheet |

學術上，**表格比方塊圖更「硬核」**——因為它強迫你每一格都填，缺一格就穿幫。老師要的是這種「無從規避」的規格描述。

而且橫看剛好（M1 → M2 → M3 → M5）剛好也是資料流方向，一眼就懂。

## 我們做了哪些事

### 1. 辨認出最小可分模組

我從原本的架構圖識別出五個模組：

- **M1** — 使用者介面（資料進入系統的地方）
- **M2** — Gateway / 後端（授權、轉發）
- **M3** — Orchestrator（協調各頻道輸出並統一結果）
- **M4** — 分析頻道插槽（這是 plug-in slot）
- **M5** — Persistence（儲存）

關鍵判斷：**如果兩個模組永遠要一起改，它們其實是同一個模組；如果一個模組在兩件不相關的事，要拆開。**

### 2. 每個模組寫 IPO 約定

對每個模組寫一句話：

- **Input** — 接受什麼信號（功能語言）
- **Process** — 做什麼處理
- **Output** — 輸出什麼

**約束**：每一句都要在實作被替換後仍然成立。

✅ 好：「Receives heart rate variability (HRV) data via serial or manual input」

❌ 壞：「Receives HRV data from `apple_watch.py`」

### 3. 將 M4 設計成 plug-in slot

我的論文核心 claim 是「可整合多模態」，所以 M4 不能只有「中間那中間一格」，要有視覺感知的**開放插槽**：

```
M4 · Analytical channels (N slots)
──────────┬───────────┬───────────
│  HRV   │  Face  │  Text  │  ← 目前 k=3
│physio  │visual  │linguis │
──────────┴───────────┴───────────
        + k=4 speech, k=5 gaze (未來)
```

讓讀者一眼就知道，「這是可以加東西的地方，加了之後其他個模組都不用動」。

### 4. 選擇形式——選表格而非方塊圖

兩個選擇：

1. **方塊圖加 IPO 標籤** —— 看起來像架構圖，較輕，但容易讓人看成就是那個方塊
2. **橫式 IPO 規格表** —— 模組做為欄、IPO 做為行，實作放最下面一列

**選表格**。老師的評語是關於規格嚴謹度，表格強迫每格都填、無從規避。

而且橫式格式時（M1 → M2 → M3 → M5）剛好也是資料流方向，一眼就懂。

### 5. 視覺上分開「約定」與「實作」

表格的下面加一行「**Ref. impl. (replaceable)**」，把原本的（PWA、FastAPI、A2A、NumPy、DeepFace、BERT、SQLite）都被隔離到這個格裡，用淺色底色。

這一個設計決定就完成了大半工作——審稿人一眼就看到，「上面是架構，下面是當前實作，兩者解耦」。

### 6. 跟論文題目對齊

我的題目是：

> **Beyond Semantic Distance: Fusing Physiological and Linguistic Signals for Multimodal Coordination Assessment in Cross-Disciplinary Design**

老師把題目拆解出來：

| 題目關鍵詞 | 表達要視覺化的信息 |
|---|---|
| Beyond Semantic Distance | 不只看文字，超越單模態 |
| Fusing Physiological and Linguistic Signals | 生理（HRV）+ 語言（Text）必須**對等並列** |
| Multimodal Coordination Assessment | Late fusion 是核心方法 |
| Cross-Disciplinary Design | 輸出對象是設計領域 |

所以表格裡 HRV 標 `physiological`、Text 標 `linguistic`——**直接從題目本詞**過來。寬度相同。

審稿人看完就確認了，「題目指到的東西，表裡放得到啊」。放得到。

### 7. 改寫前後文的段落

最後，論文裡所有提到 Fig. 1 的句子都要跟著改：

- `Fig.~\ref{fig:arch}` → `Table~\ref{tab:arch}`
- 把「The platform is implemented in FastAPI, SQLite, ...」改成「The platform is **specified** as five modules with IPO contracts (Table 1), currently realized in FastAPI, SQLite, ...」

這步驟機器做不到的「如果後文有遺跡文字還是會被察覺」。

## LaTeX 範本

這是我最後產出的 LaTeX。如果你也在寫 IEEE 這本論文遇到一樣的問題，可以直接拿去改。

### Preamble

```latex
\usepackage{xcolor}
\usepackage{colortbl}
\usepackage{booktabs}
\usepackage{array}

\definecolor{ipoHeader}{HTML}{1D9E75}
\definecolor{ipoSubHeader}{HTML}{9FE1CB}
\definecolor{ipoFooter}{HTML}{E1F5EE}
\definecolor{ipoText}{HTML}{04342C}
```

### 表格本體

```latex
\begin{table*}[t]
\caption{IPO specification of the five-module architecture.
Columns list the five modules in dataflow order. Rows specify
the input--process--output contract for each module. The bottom
row lists the current reference implementation, which is
replaceable without altering the contracts. Module~M4 is shown
as a plug-in slot currently realizing $k{=}3$ analytical channels
and is extensible to $k{=}N$ by adding new agents at this slot.}
\label{tab:arch}
\centering
\renewcommand{\arraystretch}{1.15}
\setlength{\tabcolsep}{4pt}
\footnotesize
\begin{tabular}{|>{\centering\arraybackslash}m{0.06\textwidth}
                |>{\raggedright\arraybackslash}m{0.11\textwidth}
                |>{\raggedright\arraybackslash}m{0.11\textwidth}
                |>{\raggedright\arraybackslash}m{0.12\textwidth}
                |>{\raggedright\arraybackslash}m{0.07\textwidth}
                |>{\raggedright\arraybackslash}m{0.07\textwidth}
                |>{\raggedright\arraybackslash}m{0.07\textwidth}
                |>{\raggedright\arraybackslash}m{0.10\textwidth}|}
\hline
\rowcolor{ipoHeader}
\multicolumn{1}{|c|}{\textbf{\textcolor{white}{Stage}}} &
\multicolumn{1}{c|}{\textbf{\textcolor{white}{M1 Capture}}} &
\multicolumn{1}{c|}{\textbf{\textcolor{white}{M2 Gateway}}} &
\multicolumn{1}{c|}{\textbf{\textcolor{white}{M3 Fusion}}} &
\multicolumn{3}{c|}{\textbf{\textcolor{white}{M4 Channels ($N$ slots)}}} &
\multicolumn{1}{c|}{\textbf{\textcolor{white}{M5 Persist}}} \\
\cline{5-7}
\rowcolor{ipoSubHeader}
& & & &
\multicolumn{1}{c|}{\textcolor{ipoText}{\textbf{HRV} \scriptsize physio}} &
\multicolumn{1}{c|}{\textcolor{ipoText}{\textbf{Face} \scriptsize visual}} &
\multicolumn{1}{c|}{\textcolor{ipoText}{\textbf{Text} \scriptsize linguis.}} & \\
\hline
\textbf{Input}   & ... & ... & ... & ... & ... & ... & ... \\ \hline
\textbf{Process} & ... & ... & ... & ... & ... & ... & ... \\ \hline
\textbf{Output}  & ... & ... & ... & ... & ... & ... & ... \\ \hline
\rowcolor{ipoFooter}
\textbf{\textcolor{ipoText}{Ref. impl.}}
\scriptsize\textcolor{ipoText}{(replaceable)} &
\textcolor{ipoText}{PWA, Apple Watch} &
\textcolor{ipoText}{FastAPI, WebSocket} &
\textcolor{ipoText}{Google A2A, weighted rule} &
\textcolor{ipoText}{NumPy + FFT} &
\textcolor{ipoText}{DeepFace + OpenCV} &
\textcolor{ipoText}{BERT-base-chinese} &
\textcolor{ipoText}{SQLite (WAL)} \\
\hline
\end{tabular}
\end{table*}
```

### Section III 開頭段落改寫

原本「實作描述」的開頭：

> The proposed platform is a multimodal, multi-agent affective analysis system... It adopts a frontend--backend microservice design coordinated through Google's Agent-to-Agent (A2A) protocol, with four specialized agents... working over a FastAPI gateway and an SQLite store...

改成「規格描述」的開頭：

> The proposed platform is **specified** as five modules with explicit input--process--output (IPO) contracts (Table~\ref{tab:arch}), with the main streaming pipeline running M1 → M2 → M3 → M5 and Module M4 dispatched from M3 as a plug-in slot holding $N$ parallel analytical channels. Each module is defined by the signals it accepts (Input), the operations it performs (Process), and the artifact it produces (Output); the bottom row of Table~\ref{tab:arch} lists the current reference implementation under each module, which can be replaced without altering the contracts.

關鍵差異：**先說架構規格（What），再說實作選擇（How）**。這就是老師要的「不對應到技術模組」的學術寫法。

## 一些反思

### 學術圖的兩種角色

我之前以為架構圖就是「立起我的系統長什麼樣子」。但老師讓我認清，學術論文的架構圖不是**炫技快照**，是**設計諾諾**。

炫技快照 5 年後就過期了，設計諾諾即使實作過時，論文還能讀。

### 「商標」這個用詞的精神

老師用「商標」這個詞其實很精準——不是想找有意義的商標，而是**「代表特定依賴的標記」**。當表裡每一格都是這種標記，那就失去了通用性。

我原本以為這是「用什麼軟體」的問題，後來發現是「**到底在說誰的故事**」的問題。

### 我的盲點

我犯的錯是把「當前實作」當「架構描述」。在工程實作裡兩者常常混用沒有關係，但在學術寫作裡兩者必須分離。

這也是為什麼很多工程師背景的人寫論文時架構章節寫不好——把 README 當論文寫了。

## 給有類似處境的人

如果你也聽到老師說：

- 「寫死了」 / 「綁死了」
- 「沒有對應到」 / 「沒對應到技術模組」
- 「未來無法替代」
- 「IPO 呢」
- 「你寫的是商標」 / 「technology-agnostic」 / 「plug-in」

不要慌，「這些話**都是同一個評語**——你的架構圖太依賴特定技術」。

解法就是這篇記錄的步驟：辨認模組 → 寫 IPO 約定 → 設計 plug-in slot → 改成表格 → 分離約定與實作 → 對齊題目 → 改寫段落。

希望這篇對你有幫助。
