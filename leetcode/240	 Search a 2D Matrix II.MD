不一定要从左上角开始遍历，可以从右上角开始
```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length < 1 || matrix[0].length <1) {
            return false;
        }
        int col = matrix[0].length-1;
        int row = 0;
        while(col >= 0 && row <= matrix.length-1) {
            if(target == matrix[row][col]) {
                return true;
            } else if(target < matrix[row][col]) {
                col--;
            } else if(target > matrix[row][col]) {
                row++;
            }
        }
        return false;
    }
}
```
左下角开始递归的方法，但是超时了
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length < 1 || matrix[0].length <1) {
            return false;
        }
         return help(matrix,target,0,0) ;
    }
    boolean help(int[][] matrix, int target,int x,int y){
        if(matrix[x][y]==target){return true;}
        else if(matrix[x][y]>target){return false;}
        else {
            return (x<matrix.length-1 && help(matrix,target,x+1,y) )|| (y<matrix[0].length-1 &&help(matrix,target,x,y+1));
        }
        
    }
}
```
