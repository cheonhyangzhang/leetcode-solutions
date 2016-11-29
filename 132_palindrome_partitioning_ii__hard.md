# 132 Palindrome Partitioning II – Hard


### Problem:


Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

For example, given s = “aab”,
Return 1 since the palindrome partitioning [“aa”,”b”] could be produced using 1 cut.

### Thoughts:


This is very similar with the first version of the problem. Palindrome Partitioning. The difference is that instead of generating all the partition, we need the minimum cut now.
It’s fine to still generate all the partition and then count the cut of each partition.
But there could be better way to solve this in DP.
We still needs a helper matrix isP[i][j] to indicate if substring i…j (including) is a palindrome.
Then another one dimension array is min[i] indicate the minimum cut for substring 0…i (including).

min[i] = 0 when i = 1
min[i] = 0 when i > 1 and 0…i is a palindrome
min[i] = minimum of min[j] + 1 where j is 1..i(including) when i > 1 and 0…i is not a palindrome


### Solutions:



```
public class Solution {
    public int minCut(String s) {
        if (s == null || s.length() <= 1) {
            return 0;
        }
        boolean[][] isP = new boolean[s.length()][s.length()];
        calIsP(isP, s);
        int[] min = new int[s.length()];
        min[0] = 0;
        for (int i = 1; i < s.length(); i ++) {
            if (isP[0][i] == true) {
                min[i] = 0;
                continue;
            }
            int minC = Integer.MAX_VALUE;
            for (int j = 1; j <=i; j ++) {
                if (isP[j][i] == true) {
                    minC = Math.min(minC, min[j-1] + 1);
                }    
            }
            min[i] = minC;
        }
        return min[s.length() -1];
    }
    private void calIsP(boolean[][] isP, String s) {
        for (int i = 0; i < s.length(); i ++) {
            isP[i][i] = true;
        }
        for (int i = 0; i < s.length() - 1; i ++) {
            isP[i][i + 1] = s.charAt(i) == s.charAt(i + 1);
        }
        for (int k = 2; k < s.length(); k ++) {
            for (int i = 0; i + k < s.length(); i ++) {
                isP[i][i + k] = s.charAt(i) == s.charAt(i + k) && isP[i + 1][i + k - 1] == true;
            }
        }
    }
}
```