# 680 Valid Palindrome II

### Problem

Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.

Example 1:
```
Input: "aba"
Output: True
```
Example 2:
```
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```

### Solutions

```java
class Solution {
    public boolean validPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        while (left < right - 1) {
            if (s.charAt(left) != s.charAt(right)) {
                if (valid(s, left, right - 1)) {
                    return true;
                }
                if (valid(s, left + 1, right)) {
                    return true;
                }
                return false;
            }
            else {
                left ++;
                right --;
            }
        }
        return true;
    }
    private boolean valid(String s, int start, int end) {
        while (start < end) {
            if (s.charAt(start) != s.charAt(end)) {
                return false;
            }
            start ++;
            end --;
        }
        return true;
    }
}
```
