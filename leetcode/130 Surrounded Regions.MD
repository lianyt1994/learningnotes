
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example:

X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
Explanation:

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
<br>BFS一般通过队列来实现，遍历过的可以用visited来表示，也可以直接改成别的图案<br>
把不被包围的用另一个符号表示，DFS，把原来的O变成X，最后再把O换回来
```JAVA
class Solution {
    public void solve(char[][] board) {
	if (board.length == 0 || board[0].length == 0)
		return;
	if (board.length < 2 || board[0].length < 2)
		return;
	int m = board.length, n = board[0].length;
	//Any 'O' connected to a boundary can't be turned to 'X', so ...
	//Start from first and last column, turn 'O' to '*'.
	for (int i = 0; i < m; i++) {
		if (board[i][0] == 'O')
			boundaryDFS(board, i, 0);
		if (board[i][n-1] == 'O')
			boundaryDFS(board, i, n-1);	
	}
	//Start from first and last row, turn '0' to '*'
	for (int j = 0; j < n; j++) {
		if (board[0][j] == 'O')
			boundaryDFS(board, 0, j);
		if (board[m-1][j] == 'O')
			boundaryDFS(board, m-1, j);	
	}
	//post-prcessing, turn 'O' to 'X', '*' back to 'O', keep 'X' intact.
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < n; j++) {
			if (board[i][j] == 'O')
				board[i][j] = 'X';
			else if (board[i][j] == '*')
				board[i][j] = 'O';
		}
	}
}
//Use DFS algo to turn internal however boundary-connected 'O' to '*';
private void boundaryDFS(char[][] board, int i, int j) {
	if (i < 0 || i > board.length - 1 || j <0 || j > board[0].length - 1)
		return;
	if (board[i][j] == 'O')
		board[i][j] = '*';
	if (i > 1 && board[i-1][j] == 'O')
		boundaryDFS(board, i-1, j);
	if (i < board.length - 2 && board[i+1][j] == 'O')
		boundaryDFS(board, i+1, j);
	if (j > 1 && board[i][j-1] == 'O')
		boundaryDFS(board, i, j-1);
	if (j < board[i].length - 2 && board[i][j+1] == 'O' )
		boundaryDFS(board, i, j+1);
}
}
```
 BFS
```JAVA
public class Solution {
    class Node{
        int row;
        int col;
        Node(int x,int y){
            row = x;col = y;
        }
    }
    public void solve(char[][] board) {
        int rowLen = board.length;
        if(rowLen<=0)
            return;
        int colLen = board[0].length;
        if(colLen<=0)
            return;


        int[][] visited = new int[rowLen][colLen];
        Queue<Node> queue = new LinkedList<>();

        for(int row = 0;row<rowLen;row++)
            for(int col = 0;col<colLen;col++)
                visited[row][col] = 0;

        for(int row = 0;row<rowLen;row++)
        {
            if(board[row][0]=='O')
                queue.offer(new Node(row,0));
            if(board[row][colLen-1] == 'O')
                queue.offer(new Node(row,colLen-1));
        }
        for(int col = 0;col<colLen;col++){
            if(board[0][col]=='O')
                queue.offer(new Node(0,col));
            if(board[rowLen-1][col]=='O')
                queue.offer(new Node(rowLen-1,col));
        }
         while(!queue.isEmpty()){
                Node top = queue.poll();
                int rowrow = top.row;
                int colcol = top.col;
                if(visited[rowrow][colcol] == 1)
                    continue;

                visited[rowrow][colcol] = 1;

                if(rowrow+1<rowLen && board[rowrow+1][colcol] == 'O' && visited[rowrow+1][colcol] == 0)
                    queue.offer(new Node(rowrow+1,colcol));
                if(rowrow-1>=0 && board[rowrow-1][colcol] == 'O' && visited[rowrow-1][colcol] == 0)
                    queue.offer(new Node(rowrow-1,colcol));
                if(colcol+1<colLen && board[rowrow][colcol+1] == 'O' && visited[rowrow][colcol+1] == 0)
                    queue.offer(new Node(rowrow,colcol+1));
                if(colcol-1>=0 && board[rowrow][colcol-1] == 'O' && visited[rowrow][colcol-1] == 0)
                    queue.offer(new Node(rowrow,colcol-1));
            }
        for(int row = 0;row<rowLen;row++){
            for(int col = 0;col<colLen;col++){
                if(board[row][col] == 'O' && visited[row][col] == 0)
                    board[row][col] = 'X';
            }
        }
    }
}

```
