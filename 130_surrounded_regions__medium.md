# 130 Surrounded Regions – Medium


### Problem:



Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,

X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X

### Thoughts:



This problem is more like a DFS problem. Solution is using the idea of a DFS, but in a “BFS” way.

Here is the steps of the solution.

1 Find loc for all the ‘O’ at the edge of the square, push these loc into a queue.

2 Iterate over the queue, for each loc, go all possible loc it can reach and marked all the loc with “Y” so that unsurrounded ‘O’ becomes “Y” while surrounded ‘O’ stays ‘O’.

3 Flip all the ‘O’ to be ‘X’ and ‘Y’ to be ‘O’ and we are done.

So the whole ideal is to like a DFS, go deeper as possible. But not like a normal DFS that first iteration is on every elements, this one is on all edged ‘O’ in a queue. Only because it’s using a queue so I called it a “BFS” way.


### Solutions:



```java
public class Solution {
    public void solve(char[][] board) {
        if (board == null || board.length == 0){
            return;
        }
        LinkedList<Integer> xs = new LinkedList<Integer>();
        LinkedList<Integer> ys = new LinkedList<Integer>();
        initStarter(xs, ys, board);
        markO(xs, ys, board);
        flipBoard(board);
    }
    //add all loc of edge 'O' to queue
    private void initStarter(LinkedList<Integer> xs, LinkedList<Integer> ys, char[][] board){
        int height = board.length;
        int width = board[0].length;
        for (int i = 0; i < height; i ++){
            if (board[i][0] == 'O'){
                xs.add(i);
                ys.add(0);
            }
            if (board[i][width-1] == 'O'){
                xs.add(i);
                ys.add(width-1);
            }
        }//for i
        for (int j = 0; j < width; j ++ ){
            if (board[0][j] == 'O'){
                xs.add(0);
                ys.add(j);
            }
            if (board[height - 1][j] == 'O'){
                xs.add(height - 1);
                ys.add(j);
            }
        }//for j
    }
    //mark all unsurronded O with Y
    private void markO(LinkedList<Integer> xs, LinkedList<Integer> ys, char[][] board){
        int height = board.length;
        int width = board[0].length;
        //use Y stands for unsurronded O
        while (xs.size() > 0){
            int x = xs.pop();
            int y = ys.pop();
            board[x][y] = 'Y';
            if (x - 1 >= 0 && board[x-1][y] == 'O'){
                xs.add(x-1);
                ys.add(y);
            }
            if (x + 1 < height && board[x+1][y] == 'O'){ 
                xs.add(x+1); 
                ys.add(y); 
            } 
            if (y - 1 >= 0 && board[x][y-1] == 'O'){
                xs.add(x);
                ys.add(y-1);
            }
            if (y + 1 < width && board[x][y+1] == 'O'){
                xs.add(x);
                ys.add(y+1);
            }
        }//while
    }
    private void flipBoard(char[][] board){
        int height = board.length;
        int width = board[0].length;
        for (int i = 0; i < height; i ++){
            for (int j = 0; j < width; j ++){
                if (board[i][j] == 'Y')
                    board[i][j] = 'O';
                else
                    board[i][j] = 'X';
            }
        }
    }//flipBoard
}
```
Alternative solution:

```java
public class Solution {
    public void solve(char[][] board) {
        for (int i = 0; i < board.length; i ++) {
            mark(board, i, 0);
            mark(board, i, board[i].length - 1);
        }
        for (int j = 0; j < board[0].length; j ++) {
            mark(board, 0, j);
            mark(board, board.length - 1, j);
        }
        for (int i = 0; i < board.length; i ++) {
            for (int j = 0; j < board[0].length; j ++) {
                if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                    continue;
                }
                if (board[i][j] == 'Y') {
                    board[i][j] = 'O';
                    continue;
                }
            }
        }
    }
    private void mark(char[][] board, int i, int j) {
        Queue<Integer> xs = new LinkedList<Integer>();
        Queue<Integer> ys = new LinkedList<Integer>();
        xs.add(i);
        ys.add(j);
        if (board[i][j] != 'O') {
            return;
        }
        while(xs.size() > 0) {
            int x = xs.poll();
            int y = ys.poll();
            board[x][y] = 'Y';
            if (x - 1 >= 0 && board[x-1][y] == 'O') {
                xs.add(x - 1);
                ys.add(y);
            }
            if (x + 1 < board.length && board[x+1][y] == 'O') {
                xs.add(x + 1);
                ys.add(y);
            }
            if (y - 1 >= 0 && board[x][y-1] == 'O') {
                xs.add(x);
                ys.add(y - 1);
            }
            if (y + 1 < board[0].length && board[x][y+1] == 'O') {
                xs.add(x);
                ys.add(y + 1);
            }
        }
 
    }
}
```