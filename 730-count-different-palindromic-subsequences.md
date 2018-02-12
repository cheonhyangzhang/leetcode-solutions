# 730 Count Different Palindromic Subsequences

### Problem
Given a string S, find the number of different non-empty palindromic subsequences in S, and return that number modulo 10^9 + 7.

A subsequence of a string S is obtained by deleting 0 or more characters from S.

A sequence is palindromic if it is equal to the sequence reversed.

Two sequences A_1, A_2, ... and B_1, B_2, ... are different if there is some i for which A_i != B_i.

Example 1:
```
Input: 
S = 'bccb'
Output: 6
Explanation: 
The 6 different non-empty palindromic subsequences are 'b', 'c', 'bb', 'cc', 'bcb', 'bccb'.
Note that 'bcb' is counted only once, even though it occurs twice.
```
Example 2:
```
Input: 
S = 'abcdabcdabcdabcdabcdabcdabcdabcddcbadcbadcbadcbadcbadcbadcbadcba'
Output: 104860361
Explanation: 
There are 3104860382 different non-empty palindromic subsequences, which is 104860361 modulo 10^9 + 7.
```
Note:

The length of S will be in the range [1, 1000].
Each character S[i] will be in the set {'a', 'b', 'c', 'd'}.

### Solutions

```java
class Solution {
    public int countPalindromicSubsequences(String S) {
        int base = 1000000007;
        long[][] dp = new long[S.length()][S.length()];
        for (int l = 1; l <= S.length(); l ++) {
            for (int i = 0; i + l - 1 < S.length(); i ++) {
                int j = i + l - 1;
                if (l == 1) {
                    dp[i][j] = 1;
                    continue;
                }
                if (l == 2) {
                    dp[i][j] = 2;
                    continue;
                }
                if (S.charAt(i) == S.charAt(j)) {
                    int left = i + 1, right = j - 1;
                    while (left <= right && S.charAt(left) != S.charAt(i)) {
                        left ++;
                    }
                    while (left <= right && S.charAt(right) != S.charAt(i)) {
                        right --;
                    }
                    if (left > right) {
                        dp[i][j] = dp[i + 1][j - 1] * 2 + 2;
                    }
                    else if (left == right) {
                        dp[i][j] = dp[i + 1][j - 1] * 2 + 1;
                    }
                    else {
                        dp[i][j] = dp[i + 1][j - 1] * 2 - dp[left + 1][right - 1];
                    }
                }
                else {
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j] - dp[i + 1][j - 1] ;
                }
                // dp[i][j] = dp[i][j] % base;
                dp[i][j] = dp[i][j] < 0? dp[i][j] + base:dp[i][j]% base;
            }
        }
        return (int)dp[0][S.length() - 1];
    }
}
```