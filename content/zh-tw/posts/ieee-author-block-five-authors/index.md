---
slug: ieee-author-block-five-authors
copyright: true
title: "IEEE 研討會論文五位作者排版：Department of 縮寫與 author block 重排"
date: 2026-05-26 00:00:00
updated:
tags:
  - LaTeX
  - IEEE
  - 論文寫作
  - IEEEtran
categories:
  - 研究筆記
keywords:
description: "投稿 IEEE 研討會論文時，五位作者用 \\and 排版會跑掉的處理筆記。順便釐清 Department of 該不該縮寫成 Dept. of。"
top_img:
cover:
---

## 問題情境

投 IEEE 研討會論文，五位作者全部來自同一個系所（Department of Digital Media Design, National Yunlin University of Science and Technology）。原本用 `IEEEtran` 預設的 `\IEEEauthorblockN` + `\and` 寫法，但排版會變成 2+2+1，第五位作者單獨一行，看起來不平衡。

一開始想說是不是 `Department of` 太長，把它縮成 `Dept. of` 就好，結果還是跑。

## 一、Department of 在 IEEE 論文要不要縮寫？

**結論：不需要縮寫，完整寫出是標準做法。**

- IEEE 官方 LaTeX 範本（`IEEEtran` demo）本身就是寫 `Department of`，審稿不會挑這個。
- 若版面真的吃緊，實務上可接受 `Dept. of`，這是論文中偶爾會看到的縮寫形式。
- 但**不建議**只寫系名而省略 `Department of`，稍微不正式。

**關鍵理解**：縮寫 `Department of` → `Dept. of` 並不能解決多作者排版問題，因為跑版的根因不是字串長度，而是 `\and` 在五位作者時的折行行為。

## 二、五位作者的真正問題

`IEEEtran` 的 `\and` 機制會嘗試把所有作者排成一列，空間不夠就自動折行，結果常常變成 2+2+1 這種不平衡的格式。

**而且更重要的問題是：五位作者都是同一個系所，卻把
`Dept. of Digital Media Design / National Yunlin University of Science and Technology / Douliu, Taiwan`
重複寫五次，本身就是冗餘的寫法。**

## 三、推薦解法：合併共用 affiliation

當多位作者共享相同 affiliation 時，IEEE 官方就有建議的合併寫法。改成下面這樣：

```latex
\author{
\IEEEauthorblockN{
1\textsuperscript{st} Teng-Wen Chang\IEEEauthorrefmark{1},
2\textsuperscript{nd} Yi-Sheng Wu\IEEEauthorrefmark{2},
3\textsuperscript{rd} Ya-Chen Chang\IEEEauthorrefmark{3},\\
4\textsuperscript{th} Jia-Rong Lotus Li\IEEEauthorrefmark{4},
5\textsuperscript{th} Siao-Rou Jheng\IEEEauthorrefmark{5}
}
\IEEEauthorblockA{
\textit{Department of Digital Media Design},
\textit{National Yunlin University of Science and Technology},
Douliu, Taiwan \\
\IEEEauthorrefmark{1}tengwen@yuntech.edu.tw,
\IEEEauthorrefmark{2}ezrawu.tw@gmail.com,
\IEEEauthorrefmark{3}annieinresearch@gmail.com,\\
\IEEEauthorrefmark{4}lotus.softlab@gmail.com,
\IEEEauthorrefmark{5}seaforest01225@gmail.com
}
}
```

排版結果：

- 第一行：五位作者姓名（可能自然折成兩行）
- 第二行：共用的系所 / 學校 / 地點（只寫一次）
- 第三行：用 `\IEEEauthorrefmark{n}` 對應到每位作者的 email

## 四、為什麼這個寫法比較好

1. **不冗餘**：同系所同學校，affiliation 只需要寫一次。
2. **不跑版**：不再有 2+2+1 的尷尬排版，因為不是用 `\and` 五次去切五個 block。
3. **可以用回完整的 `Department of`**：不需要為了省空間去縮寫。
4. **符合 IEEE 範本慣例**：`IEEEtran` 的 `bare_conf.tex` 範例就有提到多人共享 affiliation 的合併寫法。

## 五、其他可考慮的方案

如果還是想要每位作者保有獨立的 block（例如有些作者其實不同單位），可以：

- 強制在第 4 位作者前加 `\\` 觸發換行，但 `IEEEtran` 不一定吃，因為它會自己重排。
- 把作者分成兩個 `\author` 群，但這違反 `IEEEtran` 設計，不推薦。

## 小結

| 狀況 | 建議 |
|------|------|
| 多位作者同 affiliation | 用 `\IEEEauthorrefmark` 合併寫法 |
| 多位作者不同 affiliation | 用 `\and` 但盡量控制在 4 位以內 |
| 版面真的吃緊 | 可以用 `Dept. of`，但通常不必 |
| 想完全照官方風格 | 寫完整的 `Department of` |

排版問題八成不是字串太長，而是 author block 結構選錯。先從結構面想，再去碰縮寫。
