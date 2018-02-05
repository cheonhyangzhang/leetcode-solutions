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
    private class TrieNode {
        public boolean isLeaf;
        HashMap<Character, TrieNode> children;
        public TrieNode() {
            isLeaf = false;
            children = new HashMap<Character, TrieNode>();
        }
    }
    private class Trie {
        private TrieNode root;
        public Trie() {
            root = new TrieNode();
        }
        public void add(String word) {
            HashMap<Character, TrieNode> children = root.children;
            for (int i = 0; i < word.length(); i ++) {
                char c = word.charAt(i);
                if (!children.containsKey(c)) {
                    TrieNode node = new TrieNode();
                    children.put(c, node);
                }
                TrieNode node = children.get(c);
                children = node.children;
                if (i == word.length() - 1) {
                    node.isLeaf = true;
                }
            }
        }
        private TrieNode searchNode(String pre) {
            HashMap<Character, TrieNode> children = root.children;
            TrieNode node = root;
            for (int i = 0; i < pre.length(); i ++) {
                char c = pre.charAt(i);
                if (!children.containsKey(c)) {
                    return null;
                }
                node = children.get(c);
                children = node.children;
            }
            return node;
        }
        public boolean search(String word) {
            TrieNode node = searchNode(word);
            return node != null && node.isLeaf == true;
        }
        public boolean startsWith(String prefix) {
            TrieNode node = searchNode(prefix);
            return node != null;
        }
    }
    public List<String> findWords(char[][] board, String[] words) {
        Set<String> result = new HashSet<String>();
        Trie pt = new Trie();
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
    private void dfs(Trie pt, int i, int j, char[][] board, boolean[][] visited, String s, Set<String> result) {
        if (i < 0 || i >= visited.length || j < 0 || j >= visited[0].length) {
            return;
        }
        if (visited[i][j] == true) {
            return;
        }
        s += board[i][j];
        if (!pt.startsWith(s)) {
            return;
        }
        if (pt.search(s)) {
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