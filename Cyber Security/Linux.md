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
