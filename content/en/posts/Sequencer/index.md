---
slug: Sequencer
title: Unreal Sequencer
date: 2025-10-28 12:16:21
tags:
- Unreal

categories:
  - Note
---
slug: Sequencer

Unreal Sequencer
==
Creating a Level Sequence
A Level Sequence is the "container" for your cinematic scene. You must create one before you can start working in the Sequencer Editor. You can create a Level Sequence directly from the **Toolbar** under **Cinematics** (as shown below).

![](https://hackmd.io/_uploads/SJtlgsxB2.png)
You can also access Cinematics and the Sequencer through the **Window** menu.
![](https://hackmd.io/_uploads/rkZWxigr2.png)
![](https://hackmd.io/_uploads/Hy5-gixrn.png)

Any of the above methods will add a sequence to the Level. Once added, you can select it and manipulate its properties in the **Details** panel (similar to a Matinee Actor). In the Details panel (shown below), you can define whether the Level Sequence plays automatically when the Level starts, whether the Sequence should loop, the Play Rate for the Sequence, and other settings.
![](https://hackmd.io/_uploads/ryrMeilrh.png)
Unlike Matinee, a Level Sequence is a self-contained asset — you can embed one Level Sequence inside another. For example, you can create a Level Sequence with animated characters and cameras as a single scene, which is then part of a larger cinematic sequence.

Click the **Add New** button and select **Level Sequence** from the **Animation** menu to use another method of creating a Level Sequence in the **Content Browser**. When you do this, you first create the Level Sequence asset and then place it into the Level.
![](https://hackmd.io/_uploads/HkWXeseB2.png)

Adding Tracks to the Sequencer
==

After creating a Level Sequence, double-click it to open the **Sequencer Editor** so you can start building your cinematic.
![](https://hackmd.io/_uploads/ryeVeseH2.png)


The first thing to do is add a **Track** type, which you can do from the dropdown menu of the **Track** button.
![](https://hackmd.io/_uploads/H1BNgolrn.png)

Adding Audio
==

![](https://hackmd.io/_uploads/BkKcgjeHn.png)


In the image above, we moved the Audio folder to the end of the Tracks list, resulting in what is shown in the next image.
![](https://hackmd.io/_uploads/rJyulslBn.png)
Another way to keep tracks organized is to pin a track to the top of the Sequencer interface tree. A pinned track does not scroll with other tracks, making it easy to keep a specific track in view while working through others. To pin a track, right-click it and check **Pinned**.
![](https://hackmd.io/_uploads/r1qOeilr2.png)
You can also group the sections of a track so that moving any one section moves all sections in the group together. To group a track, right-click it and select **Group**.
![](https://hackmd.io/_uploads/BJBYgslSn.png)


References
==

https://docs.unrealengine.com/4.26/zh-CN/AnimatingObjects/Sequencer/Overview/
