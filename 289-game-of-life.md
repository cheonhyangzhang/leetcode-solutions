# 289 Game of Life

### Problem:

According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

Any live cell with fewer than two live neighbors dies, as if caused by under-population.
Any live cell with two or three live neighbors lives on to the next generation.
Any live cell with more than three live neighbors dies, as if by over-population..
Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
Write a function to compute the next state (after one update) of the board given its current state.

Follow up: 
Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.
In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

### Solutions:

```java
public class Solution {
    public void gameOfLife(int[][] board) {
        // defines 2 to be a 1 -> 0 case, defines -1 to be a 0 -> 1 case
        for (int i = 0; i < board.length; i ++) {
            for (int j = 0; j < board[0].length; j ++) {
                int num = numOfLive(board, i, j);
                if (board[i][j] >= 1){
                    if (num < 2 || num > 3) {
                        board[i][j] = 2;
                    }
                }
                else{
                    if (num == 3) {
                        board[i][j] = -1;
                    }
                }
            }
        }
        
        for (int i = 0; i < board.length; i ++) {
            for (int j = 0; j < board[0].length; j ++) {
                if (board[i][j] == 2) {
                    board[i][j] = 0;
                }
                else if (board[i][j] == -1) {
                    board[i][j] = 1;
                }
            }
        }
    }
    private int numOfLive(int[][] board, int x, int y) {
        int count = 0;
        for (int i = x - 1; i < x + 2; i++) {
            for (int j = y - 1; j < y + 2; j++) {
                if (!(i == x && j == y) && isLive(board, i, j)) {
                    count ++;
                }
            }
        }
        return count;
    }
    private boolean isLive(int[][] board, int i, int j) {
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length) {
            return false;
        }
        if (board[i][j] >= 1) {
            return true;
        }
        return false;
    }
}
```