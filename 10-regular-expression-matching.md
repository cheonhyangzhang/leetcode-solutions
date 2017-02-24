# 10 Regular Expression Matching

### Problem:
Implement regular expression matching with support for '.' and '*'.
```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

### Solutions:
```java
public class Solution {
    public boolean isMatch(String s, String p) {
        return match(s, p, 0, 0);   
    }
    private boolean match(String s, String p, int s1, int s2) {
        if (s1 == s.length() && s2 == p.length()) {
            return true;
        }
        if (s2 == p.length()) {
            return false;
        }
        if (s2 == p.length() - 1 || p.charAt(s2 + 1) != '*') {
            //normal check
            if (s1 < s.length() && (p.charAt(s2) == '.' || s.charAt(s1) == p.charAt(s2))) {
                return match(s, p, s1 + 1, s2 + 1);
            }
            else {
                return false;
            }
        }
        else {
            // * as zero
            if (match(s, p, s1, s2 + 2)) {
                return true;
            }
            // * as one character
            if (s1 < s.length() && ((p.charAt(s2) == '.' ||s.charAt(s1) == p.charAt(s2)) && match(s, p, s1 + 1, s2 + 2))) {
                return true;
            }
            // * as more character
            if (s1 < s.length() && ((p.charAt(s2) == '.' ||s.charAt(s1) == p.charAt(s2)) && match(s, p, s1 + 1, s2))) {
                return true;
            }
        }
        return false;
    }
}
```