# 79 Word Search – Medium


### Problem:



Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where “adjacent” cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given board =

[
  ["ABCE"],
  ["SFCS"],
  ["ADEE"]
]
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.


### Thoughts:



This is a four direction DFS. Searching inside of a 2D array with a helper array to record visited element.


### Solutions:


```java
public class Solution {
     
    public boolean exist(char[][] board, String word) {
        if (board == null || board.length == 0 || board[0].length == 0 || word == null || word.equals("")) {
            return false;
        }
        for (int i = 0; i < board.length; i ++) {
            for (int j = 0; j < board[0].length; j ++) {
                if (search(board, word, i, j, 0) == true) {
                    return true;
                }
            }
        }
        return false;
    }
    private boolean search(char[][] board, String word, int i, int j, int matched) {
        if (matched == word.length()) {
            return true;
        }
        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length || board[i][j] != word.charAt(matched)) {
            return false;
        }
        board[i][j] = '#';
        boolean result = search(board, word, i - 1, j, matched + 1) || search(board, word, i, j - 1, matched + 1) || search(board, word, i + 1, j, matched + 1) ||  search(board, word, i, j + 1, matched + 1);
        board[i][j] = word.charAt(matched);
        return result;
         
    }
     
}
```