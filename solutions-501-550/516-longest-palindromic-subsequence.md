# 516 Longest Palindromic Subsequence

### Problem
Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

Example 1:
Input:
```
"bbbab"
```
Output:
```
4
```
One possible longest palindromic subsequence is "bbbb".
Example 2:
Input:
```
"cbbd"
```
Output:
```
2
```
One possible longest palindromic subsequence is "bb".

### Solutions
```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int[][] dp = new int[s.length()][s.length()];
        for (int l = 1; l <= s.length(); l ++) {
            for (int i = 0; i + l - 1 < s.length(); i ++) {
                int j = i + l - 1;
                if (l == 1) {
                    dp[i][j] = 1;
                    continue;
                }
                if (l == 2) {
                    dp[i][j] = s.charAt(i) == s.charAt(j)?2:1;
                    continue;
                }
                dp[i][j] = Math.max(dp[i][j - 1], dp[i + 1][j]);
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = Math.max(dp[i][j], dp[i + 1][j - 1] + 2);
                }
            }
        }
        return dp[0][s.length() - 1];
    }
}
```