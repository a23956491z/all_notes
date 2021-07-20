## Console
最初的Terminal 直接與System溝通(on console port)，使用所有資源

Physical Console： Terminal 直接用cable直連Linux
Virtual consle：模擬Physical Console

Virtual console 通常僅用一個 terminal
而這兩個詞之間也混用，但不完全相同


TTY是teletypewriter的簡稱
後來基本上都指terminal
常用的TTY1~6是Virtual console的典型實例


### 切換X windows與文字模式
TTY1 開機後的預設操作界面，通常是X window
**Ctrl + Alt + F2～F6** 可以切換不同的 tty終端機

root 提示字元是`#`
user則是`$`

### 語系支援
`$ locale`

`$ LANG=en_US.utf8` 這次登錄**輸出訊息**的語系改英文
`$ export LC_ALL=en_US.utf8` 其他的資訊也改英文

`date` 測試後，正確顯示英文日期

可以藉由修改`/etc/locale.conf`，來改變預設語系
### 簡單指令
`$ date` 日期+時間：
* ```bash
	[dmtsai@study ~]$ date +%Y/%m/%d
	2015/05/29
	```



`$ cal` 日曆
`$ bc` 計算機


### 熱鍵
Tab 命令補全 
Ctrl + C 中斷程式
Ctrl + D EOF 或 Exit
Shift + PageUp/Down 翻頁

## 求助

`--help` 取得說明

### Man
`man COMMAND` 查詢使用手冊(man page)
如：`man date`
man page代號：
* 1 ：shell中的指令
* 5 ：設定檔或格式
* 8 ：管理員可用的指令

導覽：
* 按`/` 向下搜尋
* 按`?` 向上搜尋
* 按`n` 搜尋下一個，`N`上一個

參數：
- `man -f [...]` 消歧義，查詢同名文件
```bash
[dmtsai@study ~]$ man -f man
man (1)              - an interface to the on-line reference manuals
man (1p)             - display system documentation
man (7)              - macros to format man pages
```
- `man [number] [...]` 用代號查特定同名文件
```bash
[dmtsai@study ~]$ man 1 man  <==這裡是用 man(1) 的文件資料
[dmtsai@study ~]$ man 7 man  <==這裡是用 man(7) 的文件資料
```
* `man -k [...]` 文件內有提到關鍵字就列出
```bash
[dmtsai@study ~]$ man -k man
fallocate (2)        - manipulate file space
zshall (1)           - the Z shell meta-man page
....(中間省略)....
yum-config-manager (1) - manage yum configuration options and yum repositories
yum-groups-manager (1) - create and edit yum's group metadata
yum-utils (1)        - tools for manipulating repositories and extended package management
```

### info page
`info [...]` 一樣是查詢指令用法
不過文件可讀性更高，也包含超鏈接和索引

導覽：
* node：子頁面
* tab 移動游標到下一個node
* `N` 到下一個node
* `P` 到上一個node
* `U` 到上一**層**node
* `H` 簡介如何導覽
* `B` 移動游標到第一個可用node
* `E` 移動游標到最後一個node

### Doc
/usr/share/doc 會放軟體的Doc

## 文字編輯器
### Nano
`nano [...]` 用nano開啟`[...]`

請愛用 Ctrl + G 求助

## 關機
由於多人多工，隨意關機會影響到其他人

`who` 看誰在線上

### sync：資料同步寫入
`sync`可以把記憶體的資料立刻寫入硬碟。

一般使用者執行`sync`，只會寫入其相關資料
root執行才會寫入所有資料

### Shutdown
以TTY登錄時，有些OS不需root權限也可關機
否則只有root可以關機


* `# shutdown -h now`
立刻關機
* `# shutdown -h 20:25`
20:25 ，若在21:25才下達此指令，則隔天才關機
* `# shutdown -h +10`
十分鐘後關機
* `# shutdown -r now`
立刻重新開機
* `# shutdown -r +30 'The system will reboot' `
30分鐘後，重新開機，並警告
* `# shutdown -k now 'This system will reboot' `
僅發出警告，不真的關機

其他相關指令：
* reboot
* halt ： 終止所有程式，並關閉CPU
* poweroff：halt + 送出ACPI指令到PSU，關閉電源

多層系統中，shutdown通常是讓guest os關機
poweroff則是讓整個系統關機

---

## 檔案權限
所有的使用者資訊都在 /etc/passwd 內
密碼記錄在 /etc/shadow內

使用`ls -al` 看目錄內，所有檔案的詳細權限
`-a`表示顯示隱藏檔案
linux系統內，以`.`開頭檔案就是隱藏檔

![](https://i.imgur.com/NtrOoHJ.png)

### 表示檔案的權限

![](https://i.imgur.com/TX7J28V.png)


檔案類型：
* `d` 是目錄
* `-` 是檔案
* `l` 是連結檔
* `b` 是可儲存資料的設備
* `c` 周邊設備

`rwx` 的順序不會改變
如果沒有權限則用`-`表示，如`--x`
* `r` 可讀
* `w` 可寫
* `x` 可執行

`ls -l`，如果檔案修改時間太久遠，會省略
`ls -l --full-time` 可以顯示完整時間

目錄的權限如果沒有 `x`可執行，**則不可進入該目錄**


### 區分權限的目的
1. 系統保護：保護一些必要檔案，例如賬號管理的檔案(/etc/shadow)
2. 軟體開發：區分不同團隊

### 改變檔案權限
**1. 改變檔案所屬群組：`chgrp`**
```bash
chgrp [-R] GROUP DIR/FILE
```
* -R：遞迴變更，把目錄下所有檔案都更改
* 群組需要存在於`/etc/group`內
例如：
```bash
$ chgrp test_users init.cfg
```

**2. 改變檔案擁有者：`chown`**
```bash
chown [-R] OWNER DIR/FILE
chown [-R] OWNER:GROUP DIR/FILE
```
* -R：遞迴變更，把目錄下所有檔案都更改
* 使用者需要存在於`/etc/passwd`內
* 分隔owner和group可以用`.`跟`:`
* `chown`也可以只改變群組
例如：
```bash
# change group to ssh
$ chown .sshd init.cfg
```

常用的更改擁有者場景：複製檔案
複製檔案給別人，檔案擁有者仍然是自己
如果我們要把 `.bashrc` copy成 `.bashrc_copy`，並轉給`josh`：
```bash
$ cp .bashrc .bashrc_copy
$ chown josh:josh .bashrc
```

**3. 改變權限：`chmod`**
```bash
chmod [-R] xyz DIR/FILE
```
用數字改變權限：
* `r`: 4
* `w`: 2
* `x`: 1
* `-`: 0

把權限累加即可得到一個數字
例如：
owner = rwx = 4+2+1 = 7
group = r-x = 4+1 = 5
others = --- = 0+0+0 = 0
權限代碼就是775
```bash
$ chmod 750 .bashrc
```

利用vim新增 .sh的shell script後，權限常常是 -rw-rw-r--(664)
如果我們要讓這個.sh可以執行，就需要更改權限成 -rwxrwxr-x(775 )
```bash
$ vim a.sh
$ chmod 775 a.sh
```


用符號改變權限：
```bash
chmod [-R] {u/g/o/a}{+/-/=}{rwx} 
```
* {u/g/o/a}
	* `u` 代表owner
	* `g` 代表group
	* `o` 代表others
	* `a` 代表all
* {+/-/=}
	* +代表新增
	* -代表移除
	* =代表設定


如果要設定成 -rwxr-xr-x
owner：可讀 可寫 可執行
group：可讀 可執行
others：可讀 可執行
```bash
$ chmod u=rwx,go=rx .bashrc
```
**注意，中間不能有空格**

如果是讓所有人都**額外**有可執行權限：
```bash
$ chmod a+x .bashrc
```
在不知道原本權限的情境下特別好用

### 權限意義

檔案：
* r(read)：可以讀取檔案的內容
* w(write)：可以修改檔案內容，但不可刪除
* x(execute)：可以執行

目錄：
* r：可以讀取目錄結構，也就是可以用 ls顯示內容
* w：可以變更目錄結構，也就是可以新增/刪除檔案，改名或移動
* x：可以進入該目錄

如果只有`r`卻沒有`x`，雖然可以看到有哪些檔案，卻不能看到更進階的資訊
![](https://i.imgur.com/hldJJGj.png)
所以通常給`r`權限也會給`x`權限，不然就沒有意義了

---


## 目錄與檔案指令

### PWD
print working directory,列出目前工作目錄
```bash
pwd [-P]
```
* -P 列出真實路徑，而非連接路徑(連接檔)

### MKDIR
make directory
```bash
mkdir [-mp] DIR
$ mkdir -m 771 test_dir
```
* -m 設定檔案權限
* -p 遞迴建立目錄(自動建立不存在的父目錄)，同時也可以忽略已存在目錄

### RMDIR
remove directory, 只能移除空目錄
```bash
rmdir [-p] DIR
```
* -p 遞迴移除空目錄

### PATH

執行指令時，會到PATH的路徑中尋找有沒有可執行檔案
（若有多個同名可執行檔，會使用先找到的）
查看PATH：
```bash
[root@archlinux ~]echo $PATH
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
```

新增PATH：
```bash
PATH="${PATH}=:/root"
```

目前的工作目錄不在$PATH內
所以執行指令時需要加上目錄
```bash=
./test.sh
# 而不是test.sh
```

### LS
```bash
ls [-aAdfFhilnrRSt] DIR/FILE
ls [--color={never, auto, always}] DIR/FILE
ls [--full-time] DIR/FILE
```

Options：
* -a 包含隱藏檔
* -A 包含隱藏檔，除了 `.` `..` 
* -d 只列出`.`目錄
* -f 印出的結果不排序
* -F 附加檔案類型的資訊，如目錄會加上`/`
* -h 容量用GB MB表示
* -i incode號碼
* -l 詳細資料
* -n 列出UID GUD取代使用者與群組
* -r 印出反向排序的結果
* -R 遞迴印出
* -S 照檔案容量排序
* -t 照時間排序
* --color
    * never 取消顏色提示
    * always 顯示顏色
    * auto 自動判定
* --full-time 顯示完整時間
* -time
    * atime 上次訪問時間
    * ctime 狀態更新時間
    * birth 創造時間
    * mtime 內容變更時間

```bash=
$ ls -l --time=ctime
$ ls -l --color=always
$ ls -l --full-time
$ ls -al ~
$ ls -alF 
```

### CP 複製
```bash=
cp [-adfilprsu] SOURCE DESTINATION
cp [options] SOURCE1 SOURCE2... DIRECTORY
```

參數：
* -a 即-dr --preserve=all
* -d 若來源為連接檔則複製連接檔
* -f 強制複製，例如Des已存在
* -i 若目標存在，覆蓋時會先詢問
* -l 建立hard link的連接檔
* -p 連同權限與時間複製(常用於備份)
* -r 遞迴持續複製
* -s 複製成為 symbolic link，也就是捷徑
* -u 目標比來源舊才會複製，類似更新複製
* --preserve=all 複製檔案的所有屬性

```bash=
$ cp -i ~/.bashrc /tmp/bashrc
# 已存在的話會詢問
$ cp -a /var/log/wtmp wtmp_2
# 完全複製，包含所有屬性
$ cp -r /etc/ /tmp
# 遞迴複製
```

### RM 刪除
```bash=
rm [-fir] DIR/FILE
```
參數：
* -f 強制
* -i 詢問
* -r 遞迴

```bash=
$ rm -i bashrc
# 刪除前會詢問
$ rm -i bashrc*
# 刪除bashrc開頭的，並詢問
$ rm -r /tmp/etc
# 刪除整個/tmp/etc 目錄
```
*root的rm 會alias成 rm -r
可以用`\rm` 反斜線來忽略alias*

### MV 更名或移動
```bash=
mv [-fiu] SOURCE DES
mv [options] SRC1 SRC2 ... DIR
```
參數：
* -f 強制
* -i 詢問
* -r 遞迴

```bash=
$ mv bashrc1 bashrc2 mvtest2
# 把前兩個檔案移動到 mvtest2資料夾
```

### Basename / Dirname

* basename 取得路徑中的檔案名
* dirname 取得路徑中的目錄名

### CAT 檢視檔案內容
```bash=
cat [-AbEnTv] FILE
```
參數：
* -A 即-vET
* -b 加上行號
* -E 加上斷行字元
* -n 加上行號(含空白行)
* -T 顯示出tab
* -v 顯示出特殊字元

**`tac`** 是cat的reverse版本
從尾巴印回來

### NL 對行號優化的檢視
```bash=
nl [-bnw] FILE
```
參數：
* -b
    * a 空行也印出行號
    * t 空行跳過
* -n
    * ln 行號在熒幕左方
    * rn 行號在熒幕右方
    * rz 行號在熒幕且補0
* -w
    * NUMBER 行號變幾位數

```bash=
$ nl -b a /etc/issue
# 空白行加上行號
$ nl -b a -n rz /etc/issue
# 行號補零
$ nl -b a -n rz -w 3 /etc/issue
# 指定行號變3位數
```

### less/more 可翻頁檢視

```bash=
more FILE
```
操作：
* 空白 向下翻一頁
* Enter 向下翻一行
* /STR 搜尋STR這個關鍵字
* :f 顯示檔名與已顯示行數
* q 離開


```bash=
less FILE
```
操作：
* 空白|PGDN  向下翻一頁
* PGUP 向上翻一頁
* /STR 向下搜尋STR
* ?STR 向上搜尋STR
* n 再搜尋
* N 反向的再搜尋
* g 第一行
* G 最後一行
* q 離開

### head/tail 部分檢視
```bash=
head [-n number] FILE
tail [-nf number] FILE
```

參數：
* -n 印出幾行，可以用負數表示除了那幾行外，都印
* -f 持續更新

```bash=
$ head -n -10 /etc/man_df.conf
# 印出 除了最後十行外的所有內容
$ tail -f /var/log/messages
# 如果有新的內容也會繼續印出
$ tail -n 10 /var/log/messages
# 最後10行
$ tail -n +10 /var/log/messages
# 10行之後的內容都印出來
$ head -n 20 /var/log/messages | tail -n 10
# 先用head抓前20行，再抓後10行，也就是(11~20行)
$ cat -n /var/log/messages | head -n 20 | tail -n 10
# 11~20行外，再加上行號
```

### od 檢視binary

```bash=
$ od -t xCc /etc/issue
# 同時輸出：十六進制 + ASCII
```
![](https://i.imgur.com/Rs6a35M.png)

利用od的特性，輸出特定字串的ASCII
```bash=
$ echo "print my ASCII" | od -t oCc
# 輸出ASCII，並附帶八進位碼
```

### touch 建立檔案
[[Linux#LS]] 中有提到不同的檔案時間
預設情況是顯示 mtime，也就是內容更動時間
```bash
$ date; ls -l /etc/man_db.conf ; ls -l --time=atime /etc/man_db.conf ; \
> ls -l --time=ctime /etc/man_db.conf
# 顯示三種不同的檔案更改時間
```

```bash
touch [-acdmt] FILE
```
參數：
* -a 只修改 access time
* -c 只修改檔案時間，檔案不存在也不建立
* -d, --date 指定修改日期
* -m 只修改mtime
* -t 指定修改時間，格式 `[YYYYMMDDhhmm]`


可以使用touch來讓檔案的mtime變成「現在」

## Unzip
tar.xz
`tar Jxcf OOO`