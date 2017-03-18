# 312 Burst Balloons

### Problem:

Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

Note: 
(1) You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.
(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

Example:

Given [3, 1, 5, 8]

Return 167
```
    nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
   coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

### Solutions:

Not working solution:
```java
public class Solution {
    public int maxCoins(int[] nums) {
        HashMap<String, Integer> solutions = new HashMap<String, Integer>();
        int[] left = new int[nums.length];
        int[] right = new int[nums.length];
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < nums.length; i ++) {
            sb.append("0");
            left[i] = i - 1;
            right[i] = i + 1;
        }
        return findMax(nums, sb, solutions, left, right);
    }
    private int findMax(int[] nums, StringBuilder sb, HashMap<String, Integer> solutions, int[] left, int[] right) {
        String s = sb.toString();
        if (solutions.containsKey(s)) {
            return solutions.get(s);
        }
        int max = 0;
        for (int i = 0; i < sb.length(); i ++) {
            if (sb.charAt(i) == '0') {
                sb.setCharAt(i, '1');
                int leftIndex = left[i];
                int rightIndex = right[i];
                int leftValue = leftIndex >= 0 ? nums[leftIndex] : 1;
                int rightValue = rightIndex < nums.length ? nums[rightIndex] : 1;
                if (leftIndex >= 0) {
                    right[leftIndex] = rightIndex;
                }
                if (rightIndex < nums.length) {
                    left[rightIndex] = leftIndex;
                }
                
                int tmp = findMax(nums, sb, solutions, left, right);
                tmp += leftValue * nums[i] * rightValue;
                max = Math.max(max, tmp);
                if (leftIndex >= 0) {
                    right[leftIndex] = i;
                }
                if (rightIndex < nums.length) {
                    left[rightIndex] = i;
                }
                sb.setCharAt(i, '0');
            }
        }
        
        
        solutions.put(s, max);
        return max;
    }
}
```

```
public class Solution {
    public int maxCoins(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int[][] maxs = new int[nums.length][nums.length];
        for (int k = 1; k <= nums.length; k ++) {
            for (int i = 0; i + k - 1 < nums.length; i ++) {
                int max = Integer.MIN_VALUE;
                int left = i - 1 >= 0 ? nums[i - 1] : 1;
                int right = i + k < nums.length ? nums[i + k] : 1;
                for (int j = i; j <= i + k - 1; j ++) {
                    int tmp = 0;
                    if (j - 1 >= i) {
                        tmp += maxs[i][j - 1];
                    }
                    if (j + 1 <= i + k - 1) {
                        tmp += maxs[j + 1][i + k - 1];
                    }
                    tmp += left * nums[j] * right;
                    max = Math.max(max, tmp);
                }
                maxs[i][i + k - 1] = max;
            }
        }    
        
        return maxs[0][nums.length - 1];
    }
    
}
```