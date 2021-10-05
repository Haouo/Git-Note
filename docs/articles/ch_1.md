# 基礎 Git 觀念

![](https://i.imgur.com/2UhnIn0.png)

## 1. Working directory（工作目錄）、Staging area（暫存區）和 Local repository（儲存區）

>你可以想像你有一個倉庫，在倉庫門口有個小廣場，這個廣場的概念就像暫存區一樣，你把要存放到倉庫的貨物先放到這邊（`git add`，staging area）  
然後等收集的差不多了就可以打開倉庫門，把在廣場上的貨物送進倉庫裡（`git commit`，local repo），並且記錄下來這批貨是什麼用途的、誰送來的。  
  
__倉庫前的小廣場 -> Staging area__  
__倉庫 -> Local repository__  

而 Remote 則是遠端（不在電腦 local 端）的儲存庫，例如 Github 上面的 Repository 就是一種 Remote repo

## 2. When to commit ?  

>基本上什麼時候 commit 都可以，你要把東西都完成才提交，或是一直不斷地提交都可以，但是有一套好的規則、習慣會比較好。  
常見的 Commit 的時間點有：  
    1. 完成一個「任務」的時候：不管是大到完成一整個電子商務的金流系統，還是小至只加了一個頁面甚至只是改幾個字，都算是「任務」。  
    2. 下班的時候：雖然可能還沒完全搞定任務，但至少先 Commit 今天的進度，除了備份之外，也讓公司知道你今天有在努力工作。（然後帶回家繼續苦命的做？）  
    4. 你想要 Commit 的時候就可以 Commit。  