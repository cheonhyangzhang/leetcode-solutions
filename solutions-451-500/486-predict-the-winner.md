# 486 Predict the Winner

### Problem:
Given an array of scores that are non-negative integers. Player 1 picks one of the numbers from either end of the array followed by the player 2 and then player 1 and so on. Each time a player picks a number, that number will not be available for the next player. This continues until all the scores have been chosen. The player with the maximum score wins.

Given an array of scores, predict whether player 1 is the winner. You can assume each player plays to maximize his score.

Example 1:
```
Input: [1, 5, 2]
Output: False
Explanation: Initially, player 1 can choose between 1 and 2. 
If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5. If player 2 chooses 5, then player 1 will be left with 1 (or 2). 
So, final score of player 1 is 1 + 2 = 3, and player 2 is 5. 
Hence, player 1 will never be the winner and you need to return False.
```

### Solutions:

```java
public class Solution {
    public boolean PredictTheWinner(int[] nums) {
        int[][] gain = new int[nums.length][nums.length];
        for (int k = 0; k < nums.length; k ++) {
            for (int i = 0; i + k < nums.length; i ++) {
                if (k == 0) {
                    gain[i][i + k] = nums[i];
                }
                else if (k == 1) {
                    gain[i][i + k] = Math.abs(nums[i] - nums[i + k]);
                }
                else {
                    gain[i][i + k] = Math.max(gain[i][i] - gain[i + 1][i + k], gain[i + k][i + k] - gain[i][i + k - 1]);
                }
            }
        }
        return gain[0][nums.length - 1] >= 0;
    }
}
```