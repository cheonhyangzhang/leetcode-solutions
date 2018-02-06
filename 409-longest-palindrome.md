# 409. Longest Palindrome

### Problem:

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

Note:
Assume the length of given string will not exceed 1,010.

Example:
```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

### Solutions:

```java
public class Solution {
    public int longestPalindrome(String s) {
        int[] chars = new int[52];
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c >= 'a' && c<= 'z') {
                chars[c - 'a'] ++;
            }
            else {
                chars[c - 'A' + 26] ++;
            }
        }
        int count = 0;
        for (int i = 0; i < chars.length; i ++) {
            count += chars[i] / 2;
        }
        count = count * 2;
        return Math.min(s.length(), count + 1);
    }
}
```

```java
class Solution {
    public int longestPalindrome(String s) {
        int count = 0;
        HashSet<Character> data = new HashSet<Character>();
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (data.contains(c)) {
                count += 2;
                data.remove(c);
            }
            else {
                data.add(c);
            }
        }
        if (data.size() > 0) {
            count ++;
        }
        return count;
    }
}
```
