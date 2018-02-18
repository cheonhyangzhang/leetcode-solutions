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
            // * as not zero
            if (s1 < s.length() && ((p.charAt(s2) == '.' ||s.charAt(s1) == p.charAt(s2)) && match(s, p, s1 + 1, s2))) {
                return true;
            }
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[0][0] = true;
        for (int j = 1; j < dp[0].length; j ++) {
            if (p.charAt(j - 1) == '*' && j >= 2) {
                dp[0][j] = dp[0][j - 2];
            }
        }
        for (int i = 1; i < dp.length; i ++) {
            for (int j = 1; j < dp[i].length; j ++) {
                if (p.charAt(j - 1) == '*') {
                    if (j >= 2) {
                        dp[i][j] = dp[i][j] || dp[i][j - 2];
                    }
                    if (p.charAt(j - 2) == '.' || p.charAt(j - 2) == s.charAt(i - 1)) {
                        dp[i][j] = dp[i][j] || dp[i - 1][j];
                    }
                    
                }
                else {
                    if (p.charAt(j- 1) == '.' || p.charAt(j - 1) == s.charAt(i - 1)) {
                        dp[i][j] = dp[i - 1][j - 1];
                    }
                }
            }
        }
        return dp[s.length()][p.length()];
    }
}
```