`apt intall timeshift`

Rsync的timeshift只能備份到partition中


VM備份等級1：
避免軟體更新的Bug
1. 新增另一個新的虛擬硬碟，並attach到虛擬機器中
2. 新增磁碟區並格式化成linux filesystem format
3. 利用timeshift每日將軟體資料備份到另一個虛擬硬碟

VM備份等級2：
避免虛擬硬碟死亡
用VirtualBox snapshot備份重大更新

VM備份等級3：
避免SSD死亡
每個禮拜將VM的所有資料，用增量備份的方式備份到另一顆硬碟(HDD)

VM備份等級4：
避免重大災害
每個月將VM的所有資料，完整備份一份到異地的儲存server