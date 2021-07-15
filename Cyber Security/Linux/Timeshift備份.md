`apt intall timeshift`

Rsync的timeshift只能備份到partition中

VM備份方案1：
1. 新增另一個新的虛擬硬碟，並attach到虛擬機器中
2. 新增磁碟區並格式化成linux filesystem format
3. 在timeshift中選擇