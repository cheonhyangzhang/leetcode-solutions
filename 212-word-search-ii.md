# 212 Word Search II

### Problem:

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

For example,
Given words = ["oath","pea","eat","rain"] and board =
```
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
```
Return ["eat","oath"].
Note:
You may assume that all inputs are consist of lowercase letters a-z.

### Solutions:

```java
public class Solution {
    private class Node {
        public char c;
        public boolean isLeaf;
        public List<Node> children;
        public Node (char c, boolean isLeaf) {
            this.c = c;
            this.isLeaf = isLeaf;
            this.children = new LinkedList<Node>();
        }
    }
    private class PrefixTree {
        public Node root;
        public PrefixTree() {
            root = new Node('0', false);
        }
        public void add(String s) {
            Node node = root;
            for (int i = 0; i < s.length(); i ++) {
                char c = s.charAt(i);
                boolean found = false;
                for (Node n:node.children) {
                    if (n.c == c) {
                        node = n;
                        found = true;
                        break;
                    }
                }
                if (found == false) {
                    Node tmp = new Node(c, false);
                    node.children.add(tmp);
                    node = tmp;
                }
                if (i == s.length() - 1) {
                    node.isLeaf = true;
                }
            }
        }
        public Node findNode(String s) {
            Node node = null;
            for (int i = 0; i < s.length(); i ++) {
                if (node == null) {
                    node = root;
                }
                char c = s.charAt(i);
                boolean found = false;
                for (Node n:node.children) {
                    if (n.c == c) {
                        node = n;
                        found = true;
                        break;
                    }
                }
                if (found == false) {
                    return null;
                }
            }
            return node;
        }
        public boolean hasPrefix(String s) {
            Node n = findNode(s);
            return n != null;
        }
        public boolean hasWord(String s) {
            Node n = findNode(s);
            return n != null && n.isLeaf == true;
        }
    }
    public List<String> findWords(char[][] board, String[] words) {
        Set<String> result = new HashSet<String>();
        PrefixTree pt = new PrefixTree();
        for (int i = 0; i < words.length; i ++) {
            pt.add(words[i]);
        }
        if (board == null || board.length == 0 || board[0].length == 0) {
            return new LinkedList<String>(result);
        }
        boolean[][] visited = new boolean[board.length][board[0].length];
        for (int i = 0; i < board.length; i ++) {
            for (int j = 0; j < board[0].length; j ++) {
                dfs(pt, i, j, board, visited, "", result);
            }
        }
        return new LinkedList<String>(result);
    }
    private void dfs(PrefixTree pt, int i, int j, char[][] board, boolean[][] visited, String s, Set<String> result) {
        if (i < 0 || i >= visited.length || j < 0 || j >= visited[0].length) {
            return;
        }
        if (visited[i][j] == true) {
            return;
        }
        s += board[i][j];
        if (!pt.hasPrefix(s)) {
            return;
        }
        if (pt.hasWord(s)) {
            result.add(s);
        }
        visited[i][j] = true;
        dfs(pt, i - 1, j, board, visited, s, result);
        dfs(pt, i, j - 1, board, visited, s, result);
        dfs(pt, i + 1, j, board, visited, s, result);
        dfs(pt, i, j + 1, board, visited, s, result);
        visited[i][j] = false;
    }
}
```

