-   superblock：記錄此 filesystem 的整體資訊，包括inode/block的總量、使用量、剩餘量， 以及檔案系統的格式與相關資訊等；
-   inode：記錄檔案的屬性，一個檔案佔用一個inode，同時記錄此檔案的資料所在的 block 號碼；
-   block：實際記錄檔案的內容，若檔案太大時，會佔用多個 block 。

indexed allocation:
![](https://i.imgur.com/yEsdmsS.png)


FAT:
![](https://i.imgur.com/dM8T6pU.png)
need 磁碟重組

