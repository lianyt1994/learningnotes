回溯的方法
```java
public List<String> binaryTreePaths(TreeNode root) {
        
    List<String> paths = new LinkedList<>();

    if(root == null) return paths;

    if(root.left == null && root.right == null){
        paths.add(root.val+"");
        return paths;
    }

     for (String path : binaryTreePaths(root.left)) {
         paths.add(root.val + "->" + path);
     }

     for (String path : binaryTreePaths(root.right)) {
         paths.add(root.val + "->" + path);
     }

     return paths;

}
```
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        return help(root);
    }
    
    List<String> help(TreeNode root){
        List<String> list = new ArrayList<>();
        if(root==null)return list;
        if(root.left == null && root.right==null){
            list.add(root.val+"");
            return list;
        }
        
        List<String> list1 =help(root.left);
        List<String> list2 =help(root.right);
        for(String s: list1){
            list.add(root.val+"->"+s);
        }
        for(String s: list2){
            list.add(root.val+"->"+s);
        }
        return list;
    }
}
```
或者在递归的时候把参数传过去
```java
public List<String> binaryTreePaths(TreeNode root) {
    List<String> answer = new ArrayList<String>();
    if (root != null) searchBT(root, "", answer);
    return answer;
}
private void searchBT(TreeNode root, String path, List<String> answer) {
    if (root.left == null && root.right == null) answer.add(path + root.val);
    if (root.left != null) searchBT(root.left, path + root.val + "->", answer);
    if (root.right != null) searchBT(root.right, path + root.val + "->", answer);
}
```
