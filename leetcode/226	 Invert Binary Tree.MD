层级
```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        
        if (root == null) {
            return null;
        }

        final Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while(!queue.isEmpty()) {
            final TreeNode node = queue.poll();
            final TreeNode left = node.left;
            node.left = node.right;
            node.right = left;

            if(node.left != null) {
                queue.offer(node.left);
            }
            if(node.right != null) {
                queue.offer(node.right);
            }
        }
        return root;
    }
}
```
栈
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        TreeNode p = root;
        while(!stack.isEmpty() || p != null) {
              if(p != null) {
                  stack.push(p);
                   swap(p);
                  p = p.left;
              } else {
                  TreeNode node = stack.pop(); 
                  p = node.right;   
          }
        } 
        return root;
    }
    
    void swap(TreeNode p){
        TreeNode left = p.left;
        p.left = p.right;
        p.right = left;
    }
}
```
递归
```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        
        if (root == null) {
            return null;
        }

        final TreeNode left = root.left,
                right = root.right;
        root.left = invertTree(right);
        root.right = invertTree(left);
        return root;
    }
}
```
```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        swap(root);
        invertTree(root.right);
        invertTree(root.left);
        return root;
    }
    void swap(TreeNode p){
        TreeNode left = p.left;
        p.left = p.right;
        p.right = left;
    }
}
```
