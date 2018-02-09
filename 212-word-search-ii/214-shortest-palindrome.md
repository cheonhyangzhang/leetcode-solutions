# 214. Shortest Palindrome

### Problem
Given a string S, you are allowed to convert it to a palindrome by adding characters in front of it. Find and return the shortest palindrome you can find by performing this transformation.

For example:

Given "aacecaaa", return "aaacecaaa".

Given "abcd", return "dcbabcd".

### Solutions
```java
public class Solution {
    public String shortestPalindrome(String s) {
        char[] arr = s.toCharArray();
        for (int i = 1; i <= s.length(); i ++) {
            if (isPa(arr, 0, s.length() - i) == true) {
                return new StringBuilder(s.substring(s.length() - i + 1)).reverse().toString() + s;
            }    
        }
        return "";
    }
    private boolean isPa(char[] arr, int start, int end) {
        while (start < end) {
            if (arr[start] != arr[end]) {
                return false;
            }
            start ++;
            end --;
        }
        return true;
    }
}
```

