# 692 Top K Frequent Words

### Problem
Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

Example 1:
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```
Example 2:
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```
Note:
1. You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
2. Input words contain only lowercase letters.
Follow up:
1. Try to solve it in O(n log k) time and O(n) extra space.

### Solutions
```java
class Solution {
    private class Node implements Comparable<Node>{
        public String str;
        public int freq;
        public Node(String str, int freq) {
            this.str = str;
            this.freq = freq;
        }
        @Override
        public int compareTo(Node n) {
            if (this.freq != n.freq) {
                return n.freq - this.freq;
            }
            else {
                return this.str.compareTo(n.str);
            }
        }
    }
    public List<String> topKFrequent(String[] words, int k) {
        HashMap<String, Integer> count = new HashMap<>();
        for (int i = 0; i < words.length; i ++) {
            String word = words[i];
            if (!count.containsKey(word)) {
                count.put(word, 0);
            }
            count.put(word, count.get(word) + 1);
        }
        List<Node> list = new LinkedList<>();
        for (String str:count.keySet()) {
            list.add(new Node(str, count.get(str)));
        }
        Collections.sort(list);
        List<String> res = new LinkedList<>();
        for (int i = 0; i < k; i ++) {
            if (i < list.size()) {
                res.add(list.get(i).str);
            }
        }
        return res;
    }
}
```