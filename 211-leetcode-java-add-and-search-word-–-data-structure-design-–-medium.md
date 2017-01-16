# 211 LeetCode Java: Add and Search Word – Data structure design – Medium

### Problem:

Design a data structure that supports the following two operations:

void addWord(word)
bool search(word)
search(word) can search a literal word or a regular expression string containing only letters a-z or .. A . means it can represent any one letter.

For example:

addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
Note:
You may assume that all words are consist of lowercase letters a-z.

### Thoughts:

This problem is very like implement trie problem. Actually we do need a trie here for “Add and Search Word” feature.

Given a trie (prefix tree), the problem is already straight forward enough.

### Solutions:

```java
public class WordDictionary {
    class TrieNode {
        public HashMap<Character, TrieNode> children;
        public boolean isLeaf;
        public TrieNode() {
            children = new HashMap<Character, TrieNode>();
            isLeaf = false;
        }
    }
    TrieNode root = new TrieNode();
    // Adds a word into the data structure.
    public void addWord(String word) {
        HashMap<Character, TrieNode> children = root.children;
        for (int i = 0; i < word.length(); i ++) {
            char c = word.charAt(i);
            if (!children.containsKey(c)) {
                children.put(c, new TrieNode());
            }
            if (i == word.length() - 1) {
                children.get(c).isLeaf = true;
            }
            children = children.get(c).children;
        }
    }
     
    private boolean searchRange(String word, int start, HashMap<Character, TrieNode> children) {
        if (start >= word.length()) {
            return false;
        }
        char c = word.charAt(start);
        if (children.containsKey(c)) {
            if (start == word.length() - 1) {
                return children.get(c).isLeaf;
            }
            return searchRange(word, start + 1, children.get(c).children);
        }
        else {
            if (c == '.') {
                for (Character cha:children.keySet()) {
                    if (start == word.length() - 1 && children.get(cha).isLeaf) {
                        return true;
                    }
                    if (searchRange(word, start + 1, children.get(cha).children)) {
                        return true;
                    }
                }
                return false;
            }
            else {
                return false;
            }
        }
         
    }
    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return searchRange(word, 0, root.children);
    }
}
 
// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```