定義：每個node的 ** child僅只有兩個 ** (每個node的dgree為2)
![](https://i.imgur.com/iPDpaMo.png)
Data struct implement:
```C
typedef struct Node
{
	int data, level;
	struct Node *left, *right;
}node_t;

```
```Cpp
class Tree;
class TreeNode{
    TreeNode *leftchild;         
    TreeNode *rightchild;       
    TreeNode *parent;//雙向鏈結
    int data1;                  
    double data2;
    ...
    friend class Tree;
};
class Tree{
    TreeNode *root;             // 以root作為存取整棵樹的起點
};
```  

---

## Full & Complete
* Complete Binary Tree :
>若Root node 的 index 為 1
>第 $i$ 個node 必滿足:
>* 其 left child是 $2i$
>* 其 right child 是 $2i + 1$
>* 其parent是 $\lfloor\frac{i}{2}\rfloor$ (無條件捨去)，除了Root之外
>
![](https://i.imgur.com/h9lpypo.png)
 ^cf7ae4
* Full (Perfect BT)：填滿的Complete BT
若 level 為 $n$，整顆樹有 $2^n-1$個node

![](https://i.imgur.com/tR56wQH.png)

---
## [Traversal（尋訪）](http://alrightchiu.github.io/SecondRound/binary-tree-traversalxun-fang.html)：

![](https://i.imgur.com/Y3FSBWm.png)


- 以順序之分： V代表Visit本node， 不分Left Right探訪順序
- - LVR *(inorder)*：
		無法得知樹根
		![](https://i.imgur.com/iOvXTLc.png)
- - VLR *(preorder)* 
		可得知樹根，會在最前面
![](https://i.imgur.com/ZYl9G0Q.png)
- - LRV *(postorder)*
		可得知樹根，會在最後面
![](https://i.imgur.com/bjklBvd.png)
* 以階層之分：
	* Level order：Level由小到大，同一層由左至右
![](https://i.imgur.com/z67oz9K.png)

Implement:
```cpp
/* C & Recusive*/
void inorder(struct Node *root)
{
	if(root == NULL) return;
	inorder(root->left);
	printf("data : %d, lv : %d\n", root->data,root->level);
	inorder(root->right);
}

void preorder(struct Node *root)
{
	if(root == NULL) return;
	printf("data : %d, lv : %d\n", root->data,root->level);
	preorder(root->right);
	preorder(root->left);
}
void levelorder(struct Node *root)
{
	Queue* queue = queue_init();

	Node *node;
	enqueue(queue, root);
	while((node = dequeue(queue))){

		printf("data : %d, lv : %d\n", node->data,node->level);

		if(node->left != NULL) enqueue(queue, node->left);
		if(node->right != NULL) enqueue(queue, node->right);
	}
}
```

### 基於inorder的 Successor(下一個) & Preccessor(前一個)
- Succesor：
	- **有Right child**： Right subtree的leftmost()
	- **無Right child**：以Left Child指向自己的**Ancestor**
	![](https://i.imgur.com/6utGHFS.png)
- Preccessor：與Succesor Right Left相反
![](https://i.imgur.com/AMVRqe3.png)
 
 implement:
 ```Cpp
 // C++ code
TreeNode* BinaryTree::InorderSuccessor(TreeNode *current){
    if (current->rightchild != NULL){
        return leftmost(current->rightchild);
    }

    // 利用兩個pointer: successor與current做traversal 

    TreeNode *successor = current->parent;   
    while (successor != NULL && current == successor->rightchild) {
        current = successor;
        successor = successor->parent;
    }
    return successor;
}

// Inorder travelsal based on Successor
void BinaryTree::Inorder_by_parent(TreeNode *root){
    TreeNode *current = new TreeNode;
    current = leftmost(root);

    while(current){
        std::cout << current->str << " ";
        current = InorderSuccessor(current);
    }
}
// Reverse Inorder
void BinaryTree::Inorder_Reverse(TreeNode *root){
    TreeNode *current = new TreeNode;
    current = rightmost(root);

    while(current){
        std::cout << current->str << " ";
        current = InorderPredecessor(current);
    }
}
 ```
 

---

## Binary Tree之建立

TreeNode與Binary Tree參考
```cpp
// C++ code
class BinaryTree;
class TreeNode{
private:
    TreeNode *leftchild;
    TreeNode *rightchild;
    TreeNode *parent;
    char data;
public:
    TreeNode():leftchild(0),rightchild(0),parent(0),data('x'){};
    TreeNode(char s):leftchild(0),rightchild(0),parent(0),data(s){};

    friend class BinaryTree;
};

class BinaryTree{
private:
    TreeNode *root;
public:
    BinaryTree():root(0){};
    BinaryTree(const char* str);

    void LevelorderConstruct(std::stringstream &ss);
    void InsertLevelorder(char data);

    TreeNode* leftmost(TreeNode *current);
    TreeNode* InorderSuccessor(TreeNode *current);
    void Inorder_by_parent();
};
```