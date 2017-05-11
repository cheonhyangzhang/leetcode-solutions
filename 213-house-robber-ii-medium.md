# 213 House Robber II – Medium


### Problem:
After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

### Thoughts:
This is similar to the version I. The difference is that now the houses are in a circle instead of a single line.

There is a little trick to make things easier.

There are two cases without the first element and without the last element.

Actually there are four cases, but with first and last element is invalid, and without both is already covered by either case described above.
which is R R, R N, N R and N N, where R stands for rob and N stands for no rob.
R R is invalid. R N and N N is covered by without last element, and NR and N N is covered by without first element.

Alternative solution is to consider two cases, with first element robbed and with first element not robbed.

### Solutions:

```java
public class Solution {
    public int rob(int[] num) {
        if (num.length == 0)
            return 0;
        else if (num.length == 1)
            return num[0];
        else
            return Math.max(robRange(num, 0, num.length - 2), robRange(num, 1, num.length -1));
    }
    private int robRange(int[] num, int start, int end){
        int with = num[start];
        int without = 0;
        for (int i = start + 1; i <= end; i ++){
            int newWith = without + num[i];
            int newWithout = Math.max(with, without);
            with = newWith;
            without = newWithout;
        }
        return Math.max(with, without);
    }
}
```

```java
public class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        return Math.max(robRange(nums, 1, nums.length - 1), nums[0] + robRange(nums, 2, nums.length - 2));
    }
    public int robRange(int[] nums, int start, int end) {
        if (start > end) {
            return 0;
        }
        int max = 0;
        int noRob = 0;
        int rob = 0;
        for (int i = start; i <= end; i ++) {
            int newNoRob = Math.max(rob, noRob);
            int newRob = noRob + nums[i];
            rob = newRob;
            noRob = newNoRob;
            max = Math.max(max, rob);
            max = Math.max(max, noRob);
        }
        return max;
    }
}
```