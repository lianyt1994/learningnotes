求二叉树两个结点的最低共同结点
```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    //找到或者为null就返回
    if (root == null || root == p || root == q) return root;
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    //如果只有一边有就把这边返回，如果两边都有就把它本身返回
    return left == null ? right : right == null ? left : root;
}
```
