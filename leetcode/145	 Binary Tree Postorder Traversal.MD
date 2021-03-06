用栈的方法先序后序遍历二叉树
Pre Order Traverse
```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            result.add(p.val);  // Add before going to children
            p = p.left;
        } else {
            TreeNode node = stack.pop();
            p = node.right;   
        }
    }
    return result;
}
```
In Order Traverse
```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            p = p.left;
        } else {
            TreeNode node = stack.pop();
            result.add(node.val);  // Add after all left children
            p = node.right;   
        }
    }
    return result;
}
```
Post Order Traverse
```java
public List<Integer> postorderTraversal(TreeNode root) {
    LinkedList<Integer> result = new LinkedList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            result.addFirst(p.val);  // Reverse the process of preorder
            p = p.right;             // Reverse the process of preorder
        } else {
            TreeNode node = stack.pop();
            p = node.left;           // Reverse the process of preorder
        }
    }
    return result;
}
```
后序遍历求树高
```c++
int BT_high(BiTree T) 
{ 
    BiTree p=T,r=NULL; 
    int max=0;                                     //树高 
    stack<BiTree> s; 
    while(p||!s.empty()) 
    { 
        if(p!=NULL) 
        { 
            s.push(p); 
            p=p->lchild; 
        } 
        else 
        { 
            p=s.top(); 
            if(p->rchild!=NULL && p->rchild!=r) 
                p=p->rchild; 
            else 
            { 
                if(s.size()>max) max=s.size();//最大层次即为高度 
                //如果右边为空或者访问过了，就可以把这个top弹掉，但要记录为上一个结点
                r=p; 
                s.pop(); 
                //指针记为空，让它再去找stack之前的
                p=NULL; 
            } 
        } 
    } 
    return max; 
}
```
