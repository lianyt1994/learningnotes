```JAVA
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
    int max = 1;
    
    public int longestConsecutive(TreeNode root) {
        if(root==null) return 0;
        rec(root, 1);
        return max;
    }
    
    private void rec(TreeNode n, int c) {
        if(n.left!=null) {
            if(n.val+1 == n.left.val) {rec(n.left, c+1); max = Math.max(max, c+1);}
            else rec(n.left, 1);
        }
        
        if(n.right!=null) {
            if(n.val+1 == n.right.val) {rec(n.right, c+1); max = Math.max(max, c+1);}
            else rec(n.right, 1);
        }
    }
}

```
