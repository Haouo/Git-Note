# 常用 Git 指令

## 1. `git init`  
初始化一個資料夾，建立 Local Repository  
如此一來 Git 才可以對這個資料夾進行版本控制
    
## 2. `git add`  
不論去新增、刪除、修改檔案之後，這些新的狀態（status）都不會自動被丟到 staging area 內，所以要透過 `git add` 這個指令來把這些新的狀態加入暫存區  

### 2.1 基礎用法  
- `git add <file name>`  
    加入指定的檔案到 staging area  

- `git add .` &　`git add --all`  
    一次加入所有的檔案到 staging area  
    
    Ps: 在較新版本的 Git 中，這兩個指令基本上沒有差別

### 2.2 常犯錯誤  
想像一下這個情境：  
1. 你新增了一個檔案叫做 abc.txt。  
2. 然後，執行 git add abc.txt 把檔案加至暫存區。  
3. 接著編輯 abc.txt 檔案。  

    __接下來不可以直接 commit！！！__ 因為你第三步驟修改的東西並沒有放進 staging area，所以要再 add 一次才可以  

## 3. `git commit`  
當你確認目前階段任務已經完成，而且 staging area 內的更改內容都是你想要提交到 local repo 的內容時，就可以用 `git commit` 這個指令  

### 3.1 基礎用法
- 單純 `git commit`  
	這種用法會進入 vim 編輯器內，==需要自己打上需要提交的文字內容==之後才送出  
    
- `git commit -m <commit message>`  
	這種用法就==不會進入 vim 編輯器內==，只要把想要一併提交的文字訊息接在 option `-m` 後面即可 3.1
    
- `git commit -a -m <commit message>`  
	當你剛剛編輯完一些文件的時候，並且已經確認更改內容無誤，要直接 commit 時，但又不想先 add 再 commit？  
    直接加上參數 `-a` 就可以==把 add 和 commit 合併在一起==  
    
- `git commit --allow-empty -m <commit message>`  
	參數 `--allow-empty` 可以允許就算沒有任何東西在 staging area 內需要被 commit 的狀況下，也可以 commit  
    
- `git commit -amend`  
    可以修改最近一次 commit 的訊息  
    也可以用 `git commit -amend -m <commit message>` 直接加上要補充的 commit message  
    
- __想要新增一個空資料夾，並且 commit 到 local repo__  
    因為 git 只追蹤檔案 “內容” 的變化，所以單純新建一個資料夾，git status 不會發生變化  
    可以利用一個小技巧：在資料夾下面新增一個檔案 `.keep`，指令：`touch .keep`  
    如此一來 Git 就可以抓到這個新的資料夾  


## 4. `git branch`  

### 4.1 為什麼要使用分支（Branch）？
> 在開發的過程中，一路往前 Commit 也沒什麼問題，但當開始越來越多同伴一起在同一個專案工作的時候，可能就不能這麼隨興的想 Commit 就 Commit，這時候分支就很好用。例如想要增加新功能，或是修正 Bug，或是想實驗看看某些新的做法，都可以另外做一個分支來進行，待做完確認沒問題之後再合併回來，不會影響正在運行的產品線。


Ps：一個 local repo 會預設建立一個 branch，名為 `master`，這個 branch 是個可以被刪除，或是改名的！

### 4.2 基礎用法  
- `git branch <branch name>`  
    會直接建立一個新的 branch
        
- `git branch -m <branch name brfore> <branch name after>`  
    可以把已經存在的 branch 改名  
        
- `git branch -d <branch name>`  
    可以刪除已經存在的 branch，包含預設的 master branch  
        
    __如果 branch 因為一些原因不能直接刪除怎麼辦？__  
    可以用 `git branch -D <branch name>` 強制刪除  
    差別在於 d 是大寫還是小寫，如果是大寫則強制執行

- 切換分支  
    參考 `git checkout`

## 5. `git checkout`  
`git checkout` 這個指令主要有三個功能  
1. __恢復被修改的檔案__  
    git 會把 staging area 內的內容拿來覆蓋目前 working directory 的內容  
    
    - __重要觀念__  
        正常在沒有 add 任何狀態到 staging area 的時候，此時 staging area 的狀態會和最後一次 commit 時的狀態一致  
        
        但是當你已經有 add 一些新的狀態到 staging area 內時，再用 checkout 指令恢復檔案時，Git 就會用 staging area 內的狀態來覆蓋 working directory，而不是最後一次 commit 的狀態  
    
2. __切換分支（branch）__  
    嗯。就是切換分支  
    
3. 切換 __HEAD__ 指向的地方
    > HEAD 是一個指標，指向某一個分支，通常你可以把 HEAD 當做「目前所在分支」看待。在 .git 目錄裡有一個檔名為 HEAD 的檔案，就是記錄著 HEAD 的內容。  

    __通常 HEAD 就是指向某個分支中的某次 commit__  
    __預設情況下，HEAD 會指向 master branch 中最新的一次 commit__  
    ![](https://i.imgur.com/NrOv6e4.png)


### 5.1 基礎用法
- __恢復被修改的檔案__  
    - `git checkout <file name>`  
        這個指令可以指定你要恢復的檔案，用目前 staging area 的狀態覆蓋 working directory  
    
    - `git checkout .`  
        和上一個指令一樣，差別在於可以一次恢復所有檔案  
    
    - `git checkout HEAD~<an integer> <file name>`  
        這個指令可以把指定的檔案用該次 commit 前幾次的 commit（視輸入的整數而定）的狀態來覆蓋目前的 working directory，並且一併更新 staging area，所以接下來只要直接 `git commit` 即可  

    - `git checkout HEAD~<an integer> .`  
        和上一個指令一樣，差別只在於他會做用於全部檔案  
        
- __切換分支__  
    - `git checkout <branch name>`  
        切換到指定的分支下  

    - `git checkout -b <branch name>`  
        加上參數 `-b` 的特別之處在於，如果你輸入的 `<branch name>` 是一個不存在的分支，他會自動幫你建立一個同名的新分支  
        
- __切換 HEAD 所指的的 commit__  
    - `git checkout HEAD~<an integer>`  
        可以發現後面沒有加上 `<file name>` 或是 `.`，如此一來就只是單純的切換 HEAD pointer 所指的 commit  

### 5.2 特殊情境
- __我可以回到過去的某次 commit 再開一個新分支出來嗎？__
    1. 先利用 `git checkout HEAD~<an integer>` 切換到你想要的那次 commit
    2. 利用 `git branch <branch name>` 從該次 commit 直接創立一個新分支
    3. 如此一來，就可以在這個新分支下繼續 commit 了

    ![](https://i.imgur.com/LJ1yd0R.png)
    
    效果大概就是這樣  
    `Develop` 這個分支是利用 `git chechout HEAD~2` 指令先回到第一次 commit，再利用 `git branch develop` 建立新分支，再繼續開發


## 6. `git merge`  

## 7. `git reset`  

### 7.1 重要觀念
> Reset 這個英文單字的翻譯是「重新設定」，但事實上 Git 的 Reset 指令用中文來說比較像是「前往」或「變成」，也就是「go to」或「become」的概念。當執行這個指令的時候：  
> 
> `git reset HEAD~2`  
> 
> 這個指令你原本可能會解讀成「請幫我拆掉最後兩次的 Commit」，但其實用「拆」這個動詞只是我們比較容易理解而已，事實上並沒有真的把這個 Commit「拆掉」（放心，所有的 Commit 都還在）。  
> 
> 正確的說，上面這個指令應該要解讀成「我要前往兩個 Commit 之前的狀態」或是「我要變成兩個 Commit 之前的狀態」，而隨著使用不同的參數模式，原本的這些檔案就會丟去不同的區域。  
>
> 因為實際上 git reset 指令也並不是真的刪除或是重新設定 Commit，只是「前往」到指定的 Commit，那些看起來好像不見的東西只是暫時看不到，但隨時都可以再撿回來。    

__基本上可以不用 reset 就不要用，多數狀況都可以用 checkout 來完成任務，除非真的有一些 commit 是要捨棄的__  
__特別是在多人協作的時候，隨意 reset 可能會造成別人的 branch 全部被你丟掉__  

## 8. `git log`  
這個指令可以顯示目前這個 branch 下的歷史提交（commit）紀錄，是一個非常基礎且常用的指令  

### 8.1 基礎用法
- `git log`  
    顯示最基本的 commit information、commit message  
 
- `git log --graph`  
    附加選項 `--graph` 可以顯示出簡單的分支、合併線圖  

- `git log -p`  
    詳細顯示每筆 commit 的修改內容  
    
- `git log -<an integer>`  
    限制要顯示出最後幾筆 commit  
    
- `git log --stat`  
    和 `-p` 差不多，差別在於顯示的內容比較簡略


## 9. `git status`  
__用來顯示目前 Working directory 和 Staging Area 的狀態__

### 9.1 基礎用法
- `git status`  

- `git status -s`  
    `-s` 等同 `--short`  
    顯示較少內容  

- `git status -v`  
    `-v` 等同 `--verbose`  
    顯示更完整的內容  
    
    詳細介紹可以參考下面的 Git Documentation  
    >In addition to the names of files that have been changed, also show the textual changes that are staged to be committed (i.e., like the output of `git diff --cached`). If `-v` is specified twice, then also show the changes in the working tree that have not yet been staged (i.e., like the output of `git diff`).
    >[name=Git Documentation]


## 10. `git remote`  
用來管理遠端版本庫（Repository）的指令

### 10.1 基礎用法
- `git remote add <remote name> <URL>`  
新增一個遠端 repo

- `git remote`

## 11. `git push`  

## 12. `git reflog`

## 13. `git pull`

## 14. `git fetch`

## 15. `git clone`
### 15.1 基礎用法
- `git clone [URL]`