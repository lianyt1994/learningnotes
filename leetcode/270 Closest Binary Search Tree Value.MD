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
    public int closestValue(TreeNode root, double target) {
        
        int closest = root.val;
        double min = Double.MAX_VALUE;
        
        while(root!=null) {
            if( Math.abs(root.val - target) < min  ) {
                min = Math.abs(root.val - target);
                closest = root.val;
            }
            
            if(target < root.val) {
                root = root.left;
            } else if(target > root.val) {
                root = root.right;
            } else {
                return root.val;
            }
        }
        
        return closest;
    }
}

```
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
    private int value;
    private void find(TreeNode root, double target) {
        if (Math.abs(root.val-target) < Math.abs(value-target)) value = root.val;
        if (root.val < target && root.right != null) find(root.right, target);
        if (root.val > target && root.left != null) find(root.left, target);
    }
    public int closestValue(TreeNode root, double target) {
        value = root.val;
        find(root, target);
        return value;
    }
}

```
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
    public int closestValue(TreeNode root, double target) {
        if (root.val == target) return root.val;
        if (root.val < target) {
            if (root.right == null) return root.val;
            int right = closestValue(root.right, target);
            if (Math.abs(root.val-target) <= Math.abs(right-target)) return root.val;
            return right;
        } else {
            if (root.left == null) return root.val;
            int left = closestValue(root.left, target);
            if (Math.abs(root.val-target) <= Math.abs(left-target)) return root.val;
            return left;
        }
    }
}

```
