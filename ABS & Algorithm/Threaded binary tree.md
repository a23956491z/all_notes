
為了妥善利用[[binary tree]]的NULL pointer：
* Thread(引線)：把樹葉接到其他node(依inorder trversal)
* 需要兩個bool flag，左邊是否為thread & 右邊是否為thread：
    > 以免無法得知是否visit到樹葉  
  

避免dangling pointer：
* 新增virtual root  

優點：
* 可以循inorder進行traversal而不需要使用stack or recursive
缺點：
* 需要消耗多餘的空間(left_thread, right_thread)

implement:
```cpp=
treeNode *inorder_successor(treeNode* node){

	if (!node->right_thread){
        
        treeNode *tmp = node;
		while(!tmp->left_thread){
            tmp = tmp->left_child
        }
        return tmp;
    }
    return node->right_child;
}

void *t_inorder(treeNode* node){
    
    treeNode *tmp = node;
    
    while((tmp = inorder_successor(tmp)) != tree){
        printf("%3c", tmp->data);
    }
}

void insert_right(treeNode *parent, treeNode *child){


    parent->right_child = parent;
    parent->right_thread = false;

    child->left_child = parent;
    child->left_thread = true;
    child->right_child = parent->right_child;
    child->right_thread = parent->right_thread;    

    if(!child->right_thread){
        inorder_successor(child)->left_child = child;
    }
}

```