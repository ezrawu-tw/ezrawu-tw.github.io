---
slug: Sequencer
title: Unreal Sequencer
date: 2025-10-28 12:16:21
tags:
- Unreal

categories:
  - Note
---

Unreal Sequencer
==
創建關卡序列
關卡序列（Level Sequence） 是你的過場動畫場景的“容器”，必須創建它才能在序列編輯器（Sequencer Editor）內開始工作。你可以直接從 過場動畫（Cinematics） 下的 工具列（Toolbar） 創建關卡序列（Level Sequence）（如下圖所示）。

![](https://hackmd.io/_uploads/SJtlgsxB2.png)
你也可以通過 視窗（Window） 功能表訪問過場動畫和Sequencer。
![](https://hackmd.io/_uploads/rkZWxigr2.png)
![](https://hackmd.io/_uploads/Hy5-gixrn.png)

以上任何方法都可以把一個序列添加到關卡（Level），此時可以選擇它，並且可以在 詳細資訊（Details） 面板中操縱它的屬性（類似於 Matinee Actor）。在詳細資訊（Details）面板（見下圖）中，你可以定義關卡序列（Level Sequence）是否將在關卡（Level）開始時自動播放，序列（Sequence）是否應迴圈，序列的播放速率（Play Rate for the Sequence）和其他設置。
![](https://hackmd.io/_uploads/ryrMeilrh.png)
與Matinee不同，關卡序列（Level Sequence）是自包含資源，你可以將一個關卡序列（Level Sequence）嵌入到另一個關卡序列（Level Sequence）中。例如，你可以創建具有動畫角色和攝像機的關卡序列（Level Sequence）作為一個場景，而該場景是更大的過場動畫序列的一部分。

單擊 新增（Add New） 按鈕，並從 動畫（Animation） 功能表中選擇 關卡序列（Level Sequence），便可在 內容瀏覽器（Content Browser） 中執行另一種創建關卡序列（Level Sequence）的方法。在執行此操作時，你將先創建關卡序列（Level Sequence）資源，然後再將其放置到關卡（Level）中。
![](https://hackmd.io/_uploads/HkWXeseB2.png)

向Sequencer添加軌跡
==

創建關卡序列（Level Sequence）後，按兩下它以打開 Sequencer 編輯器（Sequencer Editor），這樣你便可以開始創建你的過場動畫。
![](https://hackmd.io/_uploads/ryeVeseH2.png)


你要做的第一件事是添加一個 軌跡（Track） 類型，可以從軌跡（Track） 按鈕的下拉功能表執行此操作。
![](https://hackmd.io/_uploads/H1BNgolrn.png)

加入音訊
==

![](https://hackmd.io/_uploads/BkKcgjeHn.png)


上圖中，我們將音訊（Audio）資料夾移動到軌跡（Tracks）清單的末尾，結果如下圖所示。!
[](https://hackmd.io/_uploads/rJyulslBn.png)
另一個有助於保持軌跡條理的方式將一條軌跡固定在Sequencer介面樹的頂端。被固定的軌跡不會其他軌跡一樣滾動，有助於在其他軌跡中查看特定軌跡。 要固定軌跡，可右鍵點擊它並勾選 固定（Pinned）。
![](https://hackmd.io/_uploads/r1qOeilr2.png)
你也可以將一條軌跡的分段分到一個組，這樣移動任何一個分段，組內的所有分段都會一同移動。要給軌跡分組，可右鍵軌跡並選擇 分組（Group）.
![](https://hackmd.io/_uploads/BJBYgslSn.png)


參考資料
==

https://docs.unrealengine.com/4.26/zh-CN/AnimatingObjects/Sequencer/Overview/

