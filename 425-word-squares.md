# 425. Word Squares

### Problem:
Given a set of words (without duplicates), find all word squares you can build from them.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

For example, the word sequence ["ball","area","lead","lady"] forms a word square because each word reads the same both horizontally and vertically.

```
b a l l
a r e a
l e a d
l a d y
```

Note:
1. There are at least 1 and at most 1000 words.
2. All words will have the exact same length.
3. Word length is at least 1 and at most 5.
4. Each word contains only lowercase English alphabet a-z.
Example 1:
```
Input:
["area","lead","wall","lady","ball"]

Output:
[
  [ "wall",
    "area",
    "lead",
    "lady"
  ],
  [ "ball",
    "area",
    "lead",
    "lady"
  ]
]

Explanation:
The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
```
Example 2:
```
Input:
["abat","baba","atan","atal"]

Output:
[
  [ "baba",
    "abat",
    "baba",
    "atan"
  ],
  [ "baba",
    "abat",
    "baba",
    "atal"
  ]
]

Explanation:
The output consists of two word squares. The order of output does not matter (just the order of words in each word square matters).
```

### Solutions:

```java
public class Solution {
    private class Node {
        public boolean isLeaf;
        public HashMap<Character, Node> children;
        public List<String> cands;
        public Node() {
            isLeaf = false;
            children = new HashMap<Character, Node>();
            cands = new LinkedList<String>();
        }
    }
    private class Trie {
        public Node root;
        public Trie() {
            root = new Node();
        }
        public void add(String s) {
            Node node = root;
            for (int i = 0; i < s.length(); i ++) {
                char c = s.charAt(i);
                if (!node.children.containsKey(c)) {
                    node.children.put(c, new Node());
                }
                node = node.children.get(c);
                node.cands.add(s);
                if (i == s.length() - 1) {
                    node.isLeaf = true;
                }
            }
        }
        public Node search(String prefix) {
            Node node = root;
            for (int i = 0; i < prefix.length(); i ++) {
                char c = prefix.charAt(i);
                if (!node.children.containsKey(c)) {
                    return null;
                }
                node = node.children.get(c);
            }
            return node;
        }
        public List<String> getCands(String prefix) {
            Node node = search(prefix);
            if (node == null) {
                return null;
            }
            return node.cands;
        }
    }
    public List<List<String>> wordSquares(String[] words) {
        List<List<String>> result = new LinkedList<List<String>>();
        Trie trie = new Trie();
        for (int i = 0; i < words.length; i ++) {
            trie.add(words[i]);
        }
        List<String> tmp = new LinkedList<String>();
        for (int i = 0; i < words.length; i ++) {
            tmp.add(words[i]);
            process(words[0].length(), tmp, 1, trie, result);
            tmp.clear();
        }
        return result;
    }
    private void process(int n, List<String> tmp, int level, Trie trie, List<List<String>> result) {
        if (level == n) {
            result.add(new LinkedList<String>(tmp));
            return;
        }
        StringBuilder prefix = new StringBuilder();
        for (int i = 0; i < tmp.size(); i ++) {
            prefix.append(tmp.get(i).charAt(level));
        }
        
        List<String> cds = trie.getCands(prefix.toString());
        if (cds == null) {
            return;
        }
        for (String s:cds) {
            tmp.add(s);
            process(n, tmp, level + 1, trie, result);
            tmp.remove(tmp.size() - 1);
        }
    }
}
```