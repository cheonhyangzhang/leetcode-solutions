# 541. Reverse String II

### Problem:
Given a string and an integer k, you need to reverse the first k characters for every 2k characters counting from the start of the string. If there are less than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original.
Example:
```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

Restrictions:
1. The string consists of lower English letters only.
2. Length of the given string and k will in the range [1, 10000]

### Solutions:

```java
public class Solution {
    public String reverseStr(String s, int k) {
        if (s == null || s.length() == 0 || k == 0) {
            return "";
        }
        int i = 0;
        StringBuilder sb = new StringBuilder(s);
        while (i < s.length()) {
            int left = i;
            int right = Math.min(i + k - 1, s.length() - 1);
            while (left < right) {
                char a = sb.charAt(left);
                char b = sb.charAt(right);
                sb.setCharAt(left, b);
                sb.setCharAt(right, a);
                left ++;
                right --;
            }
            i = i + 2 * k;
        }
        return sb.toString();
    }
}
```