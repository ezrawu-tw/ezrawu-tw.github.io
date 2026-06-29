---
slug: git
title: git
date: 2025-10-28 12:25:03
tags:
- git
- version_control
categories:
  - Note
---

# git 

基本介紹 GIT 簡略歷史、使用緣由、何為版本控制？
==
* 歷史：於2005年以GPL授權條款釋出，由林納斯·托瓦茲創作
* 使用緣由：如果團隊協作時，只要使用git指令，就能做到即時更新，不用像傳統還要特別丟到雲端，再download下來，那麼麻煩。
* 版本控制：一段時間內協助追蹤程式碼變更的軟體

版本控制的邏輯說明
==
![](https://i.imgur.com/Sokaxmb.png)

![](https://i.imgur.com/dRboRYj.png)



1. 設定自己的 Git
```
因為每一次提交 ( commit ) 修改，都會紀錄作者的訊息，因此必須先編輯自己的 Name 以及 E-mail。
git config --global user.name "xxxxxxx"
git config --global user.email "xxxx@xxxx"
設定完成後，可查詢設定內容
git config --list
```
2.建立新的 Repository
```
git init
```
1. 從 Github 複製別人的 Repository
* GitHub 有提供兩種路徑，分別是 https 、 ssh  ，官方推薦使用https，差別在於 ssh 必須先設定金鑰。
```
git clone (網址https://github.com/monosparta/eason-git-practice.git)
```
1. 將修改的檔案加入版控
```
git add file.txt  // 加入file.txt
git add .         // 加入所有檔案
```
1. 提交修改的檔案
```
記得必須先執行 $ git add 將修改檔案加入版控才可以提交。
git commit               
git commit -m "修改file.txt內容"  
// 可同時送出這次 commit 的訊息
```

1. 查詢過去 commit 紀錄

```
git log
git log --stat // --stat 參數可看到詳細內容
git log -p     // -p 可看到檔案更詳細的變更內容
```
7.建立分支
```
git branch 分支名稱
```

8. 切換分支
```
git checkout 分支名稱
```
9. 合併分支
```
git merge 分支名稱
```
10. 更新遠端資料至本地端
```
git pull
```
11. 查詢目前 Git 的狀態
```
git status
```
12. 回復到上一次提交，並取消當前提交
```
git reset HEAD^ --hard
```

Git 常用指令集介紹
==
操作步驟
1. git clone 克隆你的協作專案
>抄別人的作業
2. git pull 與遠端專案同步
>google雲端中表單的共筆，以保證這筆記不會是A寫A的，B寫B的，兩個是各自作自己的事情，這樣就迷有協作的概念了
3. git status 確認本地端專案更動狀態
>git就像你的管家，問她準沒錯，這是灰常好用的功能，隨時給她查看一下
4. git add <檔案名稱>
>向世界大聲宣告你做了哪些事吧!
5. git branch 確認目前所在分支
>你要交作業，總該知道這份作業是要給哪個老師的吧?
6. git branch <分支名>
>新增分支。就如同你會有學校的資料夾，學校的資料夾又有每個不同科目的資料夾，奪細心r，快稱讚我٩(๑❛ᴗ❛๑)۶
7. git checkout <分支名>
>切換到你想推上去的分支，在提交commit前，一定要先切，否則你會是無家可歸的小孩 (ఠ్ఠ ˓̭ ఠ్ఠ)
8. git commit -m “註解”
>也許你可以記得昨天吃了什麼早餐，不過你絕對不會記得前年的今天吃了什麼早餐。多下一個註解讓自己可以回朔曾經幹了哪些(蠢事)功能拔≖‿≖
9. git push --set-upstream origin <分支名>
 >成功繳交作業٩(●˙▿˙●)۶…⋆ฺ恭喜你突破麻瓜 git 訓練

.gitignore 配置
==
* 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
* 可以使用标准的 glob 模式匹配。
* 匹配模式可以以（/）开头防止递归。
* 匹配模式可以以（/）结尾指定目录。
* 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
  
分支的使用方法
==

1. 列出分支
    列出分支基本命令：
```
git branch
```
* 沒有參數時，git branch 會列出你在本地的分支。

```
git branch
* master
```


2. 刪除分支
刪除分支命令：

git branch -d (branchname)
例如我們要刪除 testing 分支：
```
git branch
* master
  testing
git branch -d testing
Deleted branch testing (was 85fc7e7).
git branch
* master
```

3. 分支合併
一旦某分支有了獨立內容，你終究會希望將它合併回到你的主分支。 你可以使用以下命令將任何分支合併到當前分支中去：
```
git merge
```

Commit 介紹及使用
==

##### git commit ：將暫存區的內容提交到儲存庫（Repository）保留
git commit -m "修改記錄"
```
git commit -m"init commit" ＃ 說明這次的 commit 做了什麼事
```
git commit 指令後面常搭配 -m"修改記錄" ，引號裡面代表註解，告訴我們這一次 Git 做了什麼更新、新增什麼到本地端。

注意：註解可使用中、英文表示，但記得最主要是**「清楚」**，目的是讓自己或其他合作者明白這次做了什麼動作，因此使用簡單的文字說明即可。

💡 使用 git commit 指令請一定要加上 -m"修改紀錄“ 訊息

如果沒有輸入 -m 參數說明動作， Git 的預設是不會讓你執行 Commit 這個動作。因為這則執行的目的是要告訴自己及其他人「這次的修改做了什麼」。

GitHub 使用方法：push, pull 實作
==
![](https://i.imgur.com/v4RAFuJ.png)

## push
加入本地數據庫的方法：

1. 新建本地數據庫（Local Repository 只需要新建一次就好）
```
git init
```
2. 將檔案移入索引中
```
git add .
```
3. 將索引內的檔案提交至本地數據庫
```
git commit -m "message"
```
4. 加入遠端數據庫（GitHub）的方法：
先自行新建好 GitHub 的 Repository，開啟終端機，在該目錄下輸入以下指令
```
這行指令只需要輸入第一次即可
git remote add origin <your url>
```

5. 分支
```   
git branch -M main
git push -u origin main
```

![](https://i.imgur.com/HNm5gcC.png)
![](https://i.imgur.com/yiAQOJ7.png)
## pull
* Pull 指令是拉回本機更新

fork = git clone 到地端
* 先將檔案clone 下來再用pull 拉取進行同步更新

![](https://i.imgur.com/f1VB1yX.png)


GitFlow 介紹
==
Gitflow 是一種規範，是一種推薦的實作方法，這也意味著團隊可以依照需求去改動，而既然是規範，自然會有幾個要點，這裡逐一介紹:

Gitflow 的概念是由五個分支: master、developer、hotfixes、release、frature 組成
Gitflow 中 master 和 developer 兩個分支，是永久的，不會被刪除
Gitflow 中 hotfixes、release、frature 是臨時分支，在完成特定任務後會被 merge 回永久分支內
而這五個分支會個別負責幾個功能:

Developer:
Dev 分支是開發的核心，在操作上其實與 master 類似，PG 不會主動在 Dev 分支上進行開發，取而代之的是從 Dev 分支內創建一個 Feature 分支來完成需求，當 Feature 分支完成後，才合併回 Dev 內。

而 Dev 分支通常會掛上 Webhook 並執行自動化的編譯、測試、打包與部署，而部署的環境通常為 SIT，用於團隊直接操作驗證。

Featrue:
Feature 是從 Dev 中創建出來的分支，用於完成特定的功能開發，當完成的時候會被合併回 Dev 內。一般而言，每個 Feature 的生命週期會和每期 Sprint 一致，Product Owner 會訂定這一起的 Sprint 要完成的目標，而當期開出來的 Featrue 則是完成該目標下的功能。

而當 Featrue 無法在 Sprint 期限內完成時，Product Owner 則應該調查團隊內部是否有需要協助，或是審視 Featrue 是否包含了太多的功能。當團隊數量到達一定規模時，在同一期的 Sprint 其實可以開立多個 Featrue，藉由併行的方式完成多個功能。

Featrue 通常對應的是開發者自身的電腦，等於是在本機上完成測試後推送。

Release
Release 則是當 Developer 分支已經完成到能夠滿足一系列的需求時，從 Developer 中開出的分支，用於做進一步的測試。在某些情況下，Release 也會對應到一個臨時的環境，如模擬壓力測試的環境。

當 Release 的測試結束後，則將他 merge 到 master 分支；若 Release 測試發現一些問題，並在上面修正後，除了 merge 到 master 外，亦會 merge 到 developer 上。

Master:
master 會放置最穩定的程式碼版本，並且是可以隨時上線的(當不幸發生問題的時候可以立即退回上一個 master 版本止血)，也因此，程式碼要上到 master，必須先在其他的分支完成檢驗，然後 merge 進來，絕對不會讓 PG 在 master 上修改並 commit (因為可能會忽略驗證導致破洞越來越大)。

通常，我們會對永久分支掛上 Webhook，當分支的程式碼更新時觸發一些事件，而 master 更新可以設置為觸發自動將新的版本部署到正式生產環境(Production)上，其不一定會編譯與打包，而是拉取 Image 以及對應的部署配置檔 & 環境配置檔進行部署。

hotfixes:
當 master aka 上線的產品有問題(bug)時，master 會退回上一個版本止血，然而我們顯然無法把這個 bug 加到下一期的 Feature 內修正，再一路合併到 master；面對這種情況，我們會開立 hotfixes 分支來修復 bug，並在完成修復後 merge 回 master & Developer，讓這兩個永久分支的問題能夠同時被修復。
