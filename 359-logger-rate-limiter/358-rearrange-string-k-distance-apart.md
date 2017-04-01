# 358 Rearrange String k Distance Apart

### Problem:

Given a non-empty string s and an integer k, rearrange the string such that the same characters are at least distance k from each other.

All input strings are given in lowercase letters. If it is not possible to rearrange the string, return an empty string "".

Example 1:
```
s = "aabbcc", k = 3

Result: "abcabc"

The same letters are at least distance 3 from each other.
```
Example 2:
```
s = "aaabc", k = 3 

Answer: ""

It is not possible to rearrange the string.
```
Example 3:
```
s = "aaadbbcc", k = 2

Answer: "abacabcd"

Another possible answer is: "abcabcda"

The same letters are at least distance 2 from each other.
```

### Solutions:

```java
public class Solution {
    private class Node implements Comparable<Node>{
        public char c;
        public int count;
        public Node(char c, int count) {
            this.c = c;
            this.count = count;
        }
        public int compareTo(Node n) {
            return n.count - this.count;
        }
    }
    public String rearrangeString(String s, int k) {
        PriorityQueue<Node> q = new PriorityQueue<Node>();
        int[] valid = new int[26];
        int[] count = new int[26];
        for (int i = 0; i < s.length() ; i ++) {
            count[s.charAt(i) - 'a'] ++;
        }
        for (int i = 0; i < 26; i ++) {
            if (count[i] != 0) {
                q.add(new Node((char)(i + 'a'), count[i]));
            }
        }
        StringBuilder sb = new StringBuilder();
        int index = 0;
        while (!q.isEmpty()) {
            Stack<Node> tmp = new Stack<Node>();
            while (!q.isEmpty() && index < valid[q.peek().c - 'a']) {
                tmp.push(q.poll());
            }
            if (q.isEmpty()) {
                return "";
            }
            Node n = q.poll();
            char c = n.c;
            if (n.count > 1) {
                q.add(new Node(n.c, n.count - 1));
            }
            while (!tmp.isEmpty()) {
                q.add(tmp.pop());
            }
            valid[c - 'a'] = index + k;
            sb.append(c);
            index ++;
        }
        return sb.toString();
    }
}
```