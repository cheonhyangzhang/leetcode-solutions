# 208 LeetCode Java: Implement Trie (Prefix Tree) – Medium

### Problem:

Implement a trie with insert, search, and startsWith methods.

Note:
You may assume that all inputs are consist of lowercase letters a-z.

### Thoughts:

This problem is just about understanding what is and how to implement Trie (Prefix Tree).

The trick in the solution below is to create a helper method search node which could be leveraged both by startsWith and search.

### Solutions:

```java
class TrieNode {
    public boolean isLeaf;
    HashMap<Character, TrieNode> children;
    // Initialize your data structure here.
    public TrieNode() {
        isLeaf = false;
        children = new HashMap<Character, TrieNode>();
    }
}
 
public class Trie {
    private TrieNode root;
 
    public Trie() {
        root = new TrieNode();
    }
 
    // Inserts a word into the trie.
    public void insert(String word) {
        HashMap<Character, TrieNode> children = root.children;
        for (int i = 0; i < word.length(); i ++) {
            char c = word.charAt(i);
            if (!children.containsKey(c)) {
                TrieNode node = new TrieNode();
                children.put(c, node);
            }
            TrieNode node = children.get(c);
            if (i == word.length() - 1) {
                node.isLeaf = true;
            }
            children = node.children;
        }
    }
    private TrieNode searchNode(String pre) {
        HashMap<Character, TrieNode> children = root.children;
        TrieNode node = root;
        for (int i = 0; i < pre.length(); i ++) {
            if (!children.containsKey(pre.charAt(i))) {
                return null;
            }
            node = children.get(pre.charAt(i));
            children = node.children;
        }
        return node;
    }
    // Returns if the word is in the trie.
    public boolean search(String word) {
        TrieNode node = searchNode(word);
        return node != null && node.isLeaf == true;
    }
 
    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode node = searchNode(prefix);
        return node != null;
    }
}
 
// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```