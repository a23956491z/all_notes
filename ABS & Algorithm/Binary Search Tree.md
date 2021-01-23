## 特色
當Key不重複的情況下
* Key(L) < Key(Current) < Key(R)，NULL則忽略
* 是一種[[Binary Tree]]

## 搜尋
* value小於*currentNode* value
	*currentNode*設成*LeftChild*
* 大於
    *currentNode*設成*RightChild*
* 等於
    回傳*currentNode*
	
	當currentNode變NULL就代表搜尋失敗
	
## 新增
新增資料常常需要先Traversal
找到對的位置後才新增

![](https://i.imgur.com/U5mGPhT.png)
**圖一：BST的一個例子，名字是key數字是value**

搜尋的過程中，找到NULL代表搜尋失敗
但是在新增中，找到NULL就將新的點插在這

簡易範例
```cpp 
//C++，implement with double pointer
void insert(struct Node **root, struct Node *node)
{

	if(*root == NULL){
		*root = node;
	}
	else if(node->data > (*root)->data){
		insert(&((*root)->right), node);
	}

	else {
		insert(&((*root)->left), node);
	}
}
```

## 排序
用**Inorder Traversal**即可

## 刪除

1. 遞迴-傳回小孩法
```cpp
int sub_remove(int root[20][4], int n, int index, int *sign){
	if(index == -1) return -1;
	if(!root[index][HAVE_ELEMENT]) return index;

	if(root[index][DATA] == n){
		*sign = 1;

		int have_right = valid_node(root, root[index][RIGHT_CHILD]);
		int have_left =  valid_node(root, root[index][LEFT_CHILD]);

		if(have_right && have_left){

			int right = root[index][RIGHT_CHILD];//right is not 0

			while(valid_node(root, root[right][LEFT_CHILD])){
				right = root[right][LEFT_CHILD];
			}

			root[index][DATA] = root[right][DATA];
			root[index][RIGHT_CHILD] = sub_remove(root, root[index][DATA], root[index][RIGHT_CHILD], sign);


		}else if(have_right){

			if(!index){
				move_node_to(root, index, root[index][RIGHT_CHILD]);
			}else {
				int need_reset = index;
				index = root[index][RIGHT_CHILD];
				reset(root, need_reset);
			}

		}else{

			if(!index){

				int left = root[index][LEFT_CHILD];
				if(valid_node(root, left )) move_node_to(root, index, left);
				else reset(root, index);

			}else{

				int need_reset = index;
				index = root[index][LEFT_CHILD];
				reset(root, need_reset);

			}
		}
	}
	else if(root[index][DATA] < n){
		root[index][RIGHT_CHILD] = sub_remove(root, n, root[index][RIGHT_CHILD], sign);
	}
	else{
		root[index][LEFT_CHILD] = sub_remove(root, n, root[index][LEFT_CHILD], sign);
	}

	return index;
}
```
2. Parent+Successor法
```cpp
int removal(Node **root, int n)
{
	Node *delete_node = search(*root, n);
	if(!delete_node) return 0;

	Node *cur = NULL;
	Node *child = NULL;

	/*
	set which node to delete:
		if it has 0 or 1 child, we can directly delete it
		however when it has 2 child, we would find successor node
			to cover it, deleting the seccessor one.
	*/
	if(!delete_node->left || !delete_node->right) cur = delete_node;
	else cur = InorderSuccessor(delete_node);

	/*
	set which child is not NULL;
	*/
	child = (cur->left) ? cur->left : cur->right;

	/*
	bind child->parent to cur->parent
	*/
	if(child) child->parent = cur->parent;

	/*
	unbind and set new child

	*/
	if(!cur->parent) *root = child;
	else if(cur == cur->parent->left){
		cur->parent->left = child;
	}else{
		cur->parent->right = child;
	}

	/*
	(cur != delete_node) is equivalent to (delete_node->left && delete_node->right)
	cover the data instead of rebind 2 child
	*/
	if(cur != delete_node) delete_node->data = cur->data;

	return removal(root, n)+1;
}
```
3. 左子樹接到右子樹法
```cpp
Node * simpleRemove(Node **root){

	if(!root || !(*root)) return NULL;

	Node * tmp = NULL, *most;
	if((*root)->right){

		tmp = (*root)->right;
		if((most = leftmost(tmp)))most->left = (*root)->left;
	}else{

		tmp = (*root)->left;
		if((most = rightmost(tmp)))most->right = (*root)->right;
	}

	*root = tmp;
	return NULL;
}
int removal(struct Node **root, int n)
{
	if(!root) return 0;
	int counter = 0;

	Node **cur;
	while((cur = search(root,n))){
		simpleRemove(cur);
		counter++;
	}
	return counter;
}
```
5. 雙重指標直接拔