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

```java
public class Solution {
    public String rearrangeString(String s, int k) {
        if (k == 0) {
            return s;
        }
        int[] count = new int[26];
        for(int i=0; i < s.length(); i++){
            count[s.charAt(i) - 'a'] ++;
        }
        PriorityQueue<Character> q = new PriorityQueue<Character>(new Comparator<Character>(){
            public int compare(Character c1, Character c2){
                if (count[c1 - 'a'] != count[c2 - 'a']) {
                    return count[c2 - 'a'] - count[c1 - 'a'];
                }
                else {
                    return c1 - c2;
                }
            }
        });
     
        for (int i = 0; i < 26; i ++) {
            if (count[i] != 0) {
                q.add((char) (i + 'a'));
            }
        }
        StringBuilder sb = new StringBuilder();
        int len = s.length();
        while(!q.isEmpty()){
            int cnt = Math.min(k, len);
            ArrayList<Character> tmp = new ArrayList<Character>();
            for(int i=0; i < cnt; i++){
                if(q.isEmpty())
                    return "";
                char c = q.poll();
                sb.append(c);
                count[c - 'a'] --;
                if(count[c - 'a'] > 0){
                    tmp.add(c);
                }
                len--;
            }
     
            for(char c: tmp)
                q.add(c);
        }
     
        return sb.toString();
    }
}
```