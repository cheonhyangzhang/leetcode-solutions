# 198 House Robber – Easy


### Problem:
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### Thoughts:
For each house, there are two choices, either rob or not rob. And this decision is affecting later choice.

So we need two variables to keep the current max for with current value and without current value.

This is a little bit like DP, but no need to have an array because all previous optimal value doesn’t matter.

### Solutions:

```java
public class Solution {
    public int rob(int[] num) {
        if (num.length == 0){
            return 0;
        }
        else{
            int with = num[0];
            int without = 0;
            for (int i = 1; i < num.length; i ++){
                int newWith = without + num[i];
                int newWithout = Math.max(with, without);
                with = newWith;
                without = newWithout;
            }
            return Math.max(with, without);
        }
    }
}
```