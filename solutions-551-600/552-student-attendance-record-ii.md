# 552. Student Attendance Record II

### Problem:

Given a positive integer n, return the number of all possible attendance records with length n, which will be regarded as rewardable. The answer may be very large, return it after mod 109 + 7.

A student attendance record is a string that only contains the following three characters:

'A' : Absent.
'L' : Late.
'P' : Present.
A record is regarded as rewardable if it doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).

Example 1:
```
Input: n = 2
Output: 8 
Explanation:
There are 8 records with length 2 will be regarded as rewardable:
"PP" , "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" won't be regarded as rewardable owing to more than one absent times. 
```
Note: The value of n won't exceed 100,000.

### Solutions:
```java
public class Solution {
    public int checkRecord(int n) {
        long dp[][] = {{1, 1, 0}, {1, 0, 0}};
        for (int i = 2; i <= n; i++) {
            long ndp[][] = {{0, 0, 0}, {0, 0, 0}};
            ndp[0][0] = (int)((dp[0][0] + dp[0][1] + dp[0][2]) % 1000000007) ;
            ndp[0][1] = dp[0][0];
            ndp[0][2] = dp[0][1];
            ndp[1][0] = (int)((dp[0][0] + dp[0][1] + dp[0][2] + dp[1][0] + dp[1][1] + dp[1][2]) % 1000000007);
            ndp[1][1] = dp[1][0];
            ndp[1][2] = dp[1][1];
            dp = ndp;
        }
        long res = 0;
        for (int i = 0; i < 2; i ++) {
            for (int j = 0; j < 3; j ++) {
                res = (res + dp[i][j]) % 1000000007;
            }
        }
        return (int)res;
    }

}
```