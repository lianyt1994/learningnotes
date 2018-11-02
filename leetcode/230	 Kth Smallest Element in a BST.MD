求二叉搜索树第k小的数
```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        int count = countNodes(root.left);
        if (k <= count) {
            return kthSmallest(root.left, k);
        } else if (k > count + 1) {
            return kthSmallest(root.right, k-1-count); // 1 is counted as current node
        }
        
        return root.val;
    }
    
    public int countNodes(TreeNode n) {
        return n == null?0:1 + countNodes(n.left) + countNodes(n.right);
    }
}
```
