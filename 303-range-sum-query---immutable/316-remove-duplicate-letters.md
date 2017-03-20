# 316. Remove Duplicate Letters

### Problem:
Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

Example:
Given "bcabc"
Return "abc"

Given "cbacdcbc"
Return "acdb"

### Solutions:

```java
public class Solution {
    public String removeDuplicateLetters(String s) {
        StringBuilder sb = new StringBuilder();
        int[] count = new int[26];
        int[] maxs = new int[26];
        for (int i = 0; i < s.length(); i ++) {
            count[s.charAt(i) - 'a'] ++;
            maxs[s.charAt(i) - 'a'] = i;
        }
        int start = 0;
        while (start < s.length()) {
            System.out.println("Current string start at " + start);
            int min = 26;
            int index = -1;
            for (int i = start; i < s.length(); i ++) {
                if (count[s.charAt(i) - 'a'] == 0) {
                    continue;
                }
                if ((s.charAt(i) - 'a') < min) {
                    min = s.charAt(i) - 'a';
                    index = i;
                }
                if (count[s.charAt(i) - 'a'] == 1 || maxs[s.charAt(i) - 'a'] <= i) {
                    break;
                }
            }
            if (index == -1) {
                break;
            }
            for (int i = start; i < index; i ++) {
                count[s.charAt(i) - 'a'] = Math.max(0, count[s.charAt(i) - 'a'] - 1);
            }
            count[min] = 0;
            sb.append((char)(min + 'a'));
            start = index + 1;
        }
        return sb.toString();
    }
}
```

```java
public class Solution {
    public String removeDuplicateLetters(String s) {
        Stack<Character> stack = new Stack<Character>();
        int[] count = new int[26];
        boolean[] visited = new boolean[26];
        for (int i = 0; i < s.length(); i ++) {
            count[s.charAt(i) - 'a'] ++;
        }
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            count[c - 'a'] --;
            if (visited[c - 'a'] == true) {
                continue;
            }
            while (!stack.isEmpty() && c < stack.peek() && count[stack.peek() - 'a'] > 0) {
                visited[stack.peek() - 'a'] = false;
                stack.pop();
            }
            stack.push(c);
            visited[c - 'a'] = true;
        }
        
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.insert(0, stack.pop());
        }
        return sb.toString();
    }
}
```