
```java
public static BinaryTreeNode baseconvert(BinaryTreeNode root, BinaryTreeNode lastNode) {
    if (root == null)
        return lastNode;
    BinaryTreeNode current = root;
    lastNode=baseconvert(current.leftNode, lastNode);
        
    current.leftNode = lastNode;
    if (lastNode != null)
       lastNode.rightNode = current;
    lastNode = current;
    lastNode=baseconvert(current.rightNode, lastNode);
    //每次递归把最后一个值返回回去
    return lastNode;
}
```
