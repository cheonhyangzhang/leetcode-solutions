# 348. Design Tic-Tac-Toe

### Problem:

<pre>
Design a Tic-tac-toe game that is played between two players on a n x n grid.

You may assume the following rules:

A move is guaranteed to be valid and is placed on an empty block.
Once a winning condition is reached, no more moves is allowed.
A player who succeeds in placing n of their marks in a horizontal, vertical, or diagonal row wins the game.
Example:
Given n = 3, assume that player 1 is "X" and player 2 is "O" in the board.

TicTacToe toe = new TicTacToe(3);

toe.move(0, 0, 1); -> Returns 0 (no one wins)
|X| | |
| | | |    // Player 1 makes a move at (0, 0).
| | | |

toe.move(0, 2, 2); -> Returns 0 (no one wins)
|X| |O|
| | | |    // Player 2 makes a move at (0, 2).
| | | |

toe.move(2, 2, 1); -> Returns 0 (no one wins)
|X| |O|
| | | |    // Player 1 makes a move at (2, 2).
| | |X|

toe.move(1, 1, 2); -> Returns 0 (no one wins)
|X| |O|
| |O| |    // Player 2 makes a move at (1, 1).
| | |X|

toe.move(2, 0, 1); -> Returns 0 (no one wins)
|X| |O|
| |O| |    // Player 1 makes a move at (2, 0).
|X| |X|

toe.move(1, 0, 2); -> Returns 0 (no one wins)
|X| |O|
|O|O| |    // Player 2 makes a move at (1, 0).
|X| |X|

toe.move(2, 1, 1); -> Returns 1 (player 1 wins)
|X| |O|
|O|O| |    // Player 1 makes a move at (2, 1).
|X|X|X|
Follow up:
Could you do better than O(n2) per move() operation?

Hint:

Could you trade extra space such that move() operation can be done in O(1)?
You need two arrays: int rows[n], int cols[n], plus two variables: diagonal, anti_diagonal.
</pre>

### Solutions:

```java
public class TicTacToe {
    private int[][] board;
    private int n;
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        board = new int[n][n];
        this.n = n;
    }
    
    /** Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins. */
    public int move(int row, int col, int player) {
        board[row][col] = player;
        for (int i = 0; i < n; i ++) {
            int sum = 0;
            boolean allone = true;
            boolean alltwo = true;
            for (int j = 0; j < n; j ++) {
                if (board[i][j] != 1) {
                    allone = false;
                }
                if (board[i][j] != 2) {
                    alltwo = false;
                }
                if (!allone && !alltwo) {
                    break;
                }
            }
            if (allone) {
                return 1;
            }
            if (alltwo) {
                return 2;
            }
        }
        for (int j = 0; j < n; j ++) {
            boolean allone = true, alltwo = true;
            for (int i = 0; i < n; i ++) {
                if (board[i][j] != 1) {
                    allone = false;
                }
                if (board[i][j] != 2) {
                    alltwo = false;
                }
                if (!allone && !alltwo) {
                    break;
                }
            }
            if (allone) {
                return 1;
            }
            if (alltwo) {
                return 2;
            }
        }
        boolean allone = true, alltwo = true;
        for (int i = 0; i < n; i ++) {
            if (board[i][i] != 1) {
                    allone = false;
            }
            if (board[i][i] != 2) {
                alltwo = false;
            }
            if (!allone && !alltwo) {
                break;
            }
        }
        if (allone) {
            return 1;
        }
        if (alltwo) {
            return 2;
        }
        allone = true; alltwo = true;
        int i = 0, j = n - 1;
        for (; i < n; i ++, j --) {
            if (board[i][j] != 1) {
                    allone = false;
            }
            if (board[i][j] != 2) {
                alltwo = false;
            }
            if (!allone && !alltwo) {
                break;
            }
        }
        if (allone) {
            return 1;
        }
        if (alltwo) {
            return 2;
        }
        return 0;
    }
}

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
```
```java
public class TicTacToe {
    private int[][] board;
    private int n;
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        board = new int[n][n];
        this.n = n;
    }
    
    /** Player {player} makes a move at ({row}, {col}).
        @param row The row of the board.
        @param col The column of the board.
        @param player The player, can be either 1 or 2.
        @return The current winning condition, can be either:
                0: No one wins.
                1: Player 1 wins.
                2: Player 2 wins. */
    public int move(int row, int col, int player) {
        board[row][col] = player;
        boolean allsame = true;
        for (int j = 0; j < n; j ++) {
            if (board[row][j] != player) {
                allsame = false;
                break;
            }
        }
        if (allsame) {
            return player;
        }
        allsame = true;
        for (int i = 0; i < n; i ++) {
            if (board[i][col] != player) {
                allsame = false;
                break;
            }
        }
        if (allsame) {
            return player;
        }
        if (row == col) {
            allsame = true;
            for (int i = 0; i < n; i ++) {
                if (board[i][i] != player) {
                    allsame = false;
                    break;
                }
            }
            if (allsame) {
                return player;
            }
        }
        if (row + col == n - 1) {
            allsame = true;
            int i = 0, j = n - 1;
            for (;i < n; i ++, j--) {
                if (board[i][j] != player) {
                    allsame = false;
                    break;
                }
            }
            if (allsame) {
                return player;
            }
        }
        
        return 0;
    }
}

/**
 * Your TicTacToe object will be instantiated and called as such:
 * TicTacToe obj = new TicTacToe(n);
 * int param_1 = obj.move(row,col,player);
 */
 ```
