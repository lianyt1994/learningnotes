```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    private int count;
    private Integer unival(TreeNode root) {
        boolean unival = true;
        if (root.left != null) {
            Integer left = unival(root.left);
            if (left == null || root.val != left) unival = false;
        }
        if (root.right != null) {
            Integer right = unival(root.right);
            if (right == null || root.val != right) unival = false;
        }
        if (!unival) return null;
        count ++;
        return root.val;
    }
    public int countUnivalSubtrees(TreeNode root) {
        if (root == null) return 0;
        unival(root);
        return count;
    }
}

```
