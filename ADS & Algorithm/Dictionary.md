將資料**對應(Mapping)**到特定編號or給與權重，依照其編號/權重做排序或搜尋
這就是Dictionary，稱編號為**Key(鍵值)**，資料為**Element(元素)**
並將其視為一組(Key-Element pair)


![](https://i.imgur.com/EJNtRza.png)
圖一：Key-Element pair的範例

以[[Binary Search Tree]]為基礎的Dictionay
```cpp
// C++ code
class TreeNode{
private:
    TreeNode *leftchild;
    TreeNode *rightchild;
    TreeNode *parent;
    std::string data;       // Element
    int Key;                // Key, used for comparison 
     ...
};
```