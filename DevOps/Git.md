---
tags : Programming
---
{%hackmd theme-dark %}

# Git

[![hackmd-github-sync-badge](https://hackmd.io/tl43EDMuSMuDqem3spNisQ/badge)]


## 建立或取得Git儲存庫(repository)
1. **從本機初始化一個(initialize)**
進入資料夾後 *`$ git init`*
該目錄就變成儲存庫了

2. **下載別人的儲存庫(clone)** 
 
 *`$ git clone git://github.com/schacon/grit.git`*
 
 當前目錄下就會多一個資料夾

## 提交更新

1. **檔案的循環圖**
![](https://git-scm.com/figures/18333fig0201-tn.png)


2. **我們直接檢視檔案狀態好了**
*`git status`*
> On branch master
> nothing to commit, working directory clean
> **這個訊息代表你的資料庫是無更新狀態
> （你沒變更檔案）**
> ...
> On branch master
> Untracked files:
>  (use `it add <file>...` to include in what will > be committed)  
>  ...
>    NYKD-54.avi
>  ...
> nothing added to commit but untracked files present (use "git add" to track)
> **這個訊息代表NYKD-54.avi是新的或已更新的資料**


3. **現在我們有檔案了，可以加入追蹤**
*`git add NYKD-54.avi`*
> 把NYKD-54.avi加入追蹤
> *`git status`* 確認其狀態
> > On branch master
> > Changes to be committed:
> > (use `it reset HEAD <file>...` to unstage)
> >
> > new file:   NYKD-54.avi
> > **代表系統已經開始追蹤這部影片了**
>
> 所以如果你放入了一個檔案或變更了程式碼
> 提交(commit)前請加入追蹤(add)

4. **提交你的檔案**
*`git commit -m "第一次提交"`*
*`git commit`*
> 你有兩種方法保存你的檔案
> 第一種是**快速提交**
> 第二種是很普通提交
> > 1.輸入完指令他會跳出一個編輯器(通常是vim)
> > 2.然後在最上面打上你的提交訊息
> > 3.儲存
> > 
> 
> **這樣你的檔案就在GIT儲存庫中添加了一次快照(儲存點)！**

5. **忽略某檔案**
> 你可以在你的儲存庫里新增`.gitignore`
> 讓你忽略某個副檔名的檔案或是某部檔案
> ```
> HND-379.avi
> *.mp4
> 期末報告/
> ```
> **如果你在.gitignore放入這些東西
> git就會自動跳過HND-379
> 和所有副檔名為mp4的檔案還有期末報告這個目錄**

---

## 檢視提交記錄
*`git log`*
> 檢視記錄

*`git log -p -2`*
> 檢視最後兩筆記錄，順便顯示你到底新增了那些垃圾(程式碼)

## 刪除或復原commit
*`git reset --hard ^HEAD`*
> 刪除上一筆commit


## 復原更動
*`git commit --amend`*
> **以這次提交覆蓋最新一次的提交**
> 你可以用來改變你寥寥可數的提交訊息
> 或是加入某些忘了加入的檔案
 
*`git reset`*
> **把add過的檔案移出暫存區(解除追蹤)**
 
*`git reset HEAD NYKD-55.avi`*
> **取消追蹤NYKD-55.avi**

*`git checkout -- download.cpp`*
> **把最新提交的download.cpp取代現有目錄的**

## 多人協作
*`git remote`*
> **顯示目前已加入協作的資料庫**
> 通常會顯示origin，代表clone自哪個資料庫

*`git remote -v`*
**顯示已加入協作的資料庫及其URL**
如
origin  https://github.com/a23956491z/receipt.git (fetch)
origin  https://github.com/a23956491z/receipt.git (push)
up_receipt  https://github.com/supermariobros374/receipt.git (fetch)
up_receipt  https://github.com/supermariobros374/receipt.git (push)

**其實就是顯示主資料庫，和FORK出去的資料庫**

*`git remote add pb git://github.com/motherbaby/toy.git`*
把該資料庫令為pb并加入資料庫列

*`git fetch origin`*
rigin這個資料庫更新(擷取)到遠端狀態

*`git push origin master`*
把master這個分支上傳到origin這個資料庫

*`git remote show origin`*
顯示origin的詳細資料

*`git remote rename pb paul`*
把pb重名為paul

*`git remote rm pb`*
刪除pb這個資料庫

---
	
## 基本分支圖
我改天再寫
	
## 實用指令

持續更新git log
```bash
$ watch --color git log --color=always
```


## SSH
```shell
ssh-keygen -t ed25519 -C "a23956491z@yahoo.com.tw"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```