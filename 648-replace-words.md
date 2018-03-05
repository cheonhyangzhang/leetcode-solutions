# 648 Replace Words

### Problem
In English, we have a concept called root, which can be followed by some other words to form another longer word - let's call this word successor. For example, the root an, followed by other, which can form another word another.

Now, given a dictionary consisting of many roots and a sentence. You need to replace all the successor in the sentence with the root forming it. If a successor has many roots can form it, replace it with the root with the shortest length.

You need to output the sentence after the replacement.

Example 1:
```
Input: dict = ["cat", "bat", "rat"]
sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```
Note:
1. The input will only have lower-case letters.
2. 1 <= dict words number <= 1000
3. 1 <= sentence words number <= 1000
4. 1 <= root length <= 100
5. <= sentence words length <= 1000

### Solutions
```java
class Solution {
    class Node {
        public boolean isLeaf = false;
        public HashMap<Character, Node> children = new HashMap<>();
    }
    class Trie {
        private Node root = new Node();
        public void add(String word) {
            Node node = root;
            for (int i = 0; i < word.length(); i ++) {
                char c = word.charAt(i);
                if (!node.children.containsKey(c)) {
                    node.children.put(c, new Node());
                }
                node = node.children.get(c);
                if (i == word.length() - 1) {
                    node.isLeaf = true;
                }
            }
        }
        private String shortestPrefix(String word) {
            Node node = root;
            for (int i = 0; i < word.length(); i ++) {
                char c = word.charAt(i);
                if (!node.children.containsKey(c)) {
                    return word;
                }
                node = node.children.get(c);
                if (node.isLeaf == true) {
                    return word.substring(0, i + 1);
                }
            }
            return word;
        }
    }
    public String replaceWords(List<String> dict, String sentence) {
        Trie t = new Trie();
        for (String str:dict) {
            t.add(str);
        }
        
        StringBuilder sb = new StringBuilder();
        String[] tokens = sentence.split(" ");
        for (int i = 0; i < tokens.length; i ++) {
            String token = tokens[i];
            // String res = shortestPrefix(t, token);
            String res = t.shortestPrefix(token);
            sb.append(" " + res);
        }
        if (sb.length() > 0) {
            sb.deleteCharAt(0);
        }
        return sb.toString();
    }
}
```