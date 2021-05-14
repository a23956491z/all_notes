* Server：儲存多個Depot
* Depot：儲存庫
* Workspace：只抓自己需要的Depot下來，不用抓所有Depot


Server: 13.229.205.133:1666
User: username
Workspace: 留白

### 更改檔案
0. **Get latest**：抓伺服器上的新資料
1. **New pending changelist**：新開改動清單
2. **Checkout files**：取得更動檔案的權限
3. 更動
4. **Submit**：提交改動

### 新增檔案
0. **Get latest**
1. **New pending changelist**
2. **Mark for add**：把檔案標記為新增
4. **Submit**


## 其他
`p4 set P4IGNORE=C:\somepath\p4ignore.txt`

.p4ignore Example:
```bash
# directories
bin
obj

# files
*.suo
*.user
```