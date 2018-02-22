# 44 Wildcard Matching

### Problem:

Implement wildcard pattern matching with support for '?' and '*'.
```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

### Solutions:
DP is the easy way to think. 
match[i][j] means for String s [0, i) using pattern p [0, j) if it's matchable. 
then 
match[i][j] = match[i-1][j-1] if p.charAt(j) == s.charAt(i) || p.charAt(j) == '?'
match[i][j] = match[i-1][j] || match[i][j-1] if p.charAt(j) == '*'

But DP is not fast enough to solve this.

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        int i = 0;
        int j = 0;
        int starti = -1;
        int startj = -1;
        while (i < s.length()) {
            if (j < p.length() && (p.charAt(j) == '?' || p.charAt(j) == s.charAt(i))) {
                i ++;
                j ++;
            }
            else if (j < p.length() && p.charAt(j) == '*') {
                starti = i;
                startj = j;
                j ++;
            }
            else if (startj != -1) {
                j = startj + 1;
                i = starti + 1;
                starti ++;
            }
            else {
                return false;
            }
        }
        while (j < p.length() && p.charAt(j) == '*') {
            j ++;
        }
        return j == p.length();
    }
}
```

```java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] dp = new boolean[s.length() + 1][p.length() + 1];
        dp[0][0] = true;
        for (int j = 1; j <= p.length(); j ++) {
            if (p.charAt(j - 1) == '*') {
                dp[0][j] = dp[0][j - 1];
            }
        }
        for (int i = 1; i < s.length() + 1; i ++) {
            for (int j = 1; j < p.length() + 1; j ++) {
                if (p.charAt(j - 1) == '?' || p.charAt(j - 1) == s.charAt(i - 1)) {
                    dp[i][j] = dp[i][j] || dp[i - 1][j - 1];
                }
                else if (p.charAt(j - 1) == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                }
            }
        }
        
        return dp[s.length()][p.length()];
    }
}
```