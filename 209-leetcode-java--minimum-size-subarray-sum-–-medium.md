# 209 LeetCode Java : Minimum Size Subarray Sum – Medium

### Problem:

Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn’t one, return 0 instead.

For example, given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.

More practice:If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log n).

### Thoughts:

The key idea is to keep a window, move the window from left to right, adjust the window size based on if the sum of the window is greater than given target. This will end up with O(n) running time. Because for each of the two pointer, left, right, they iterate over the array once. 2n -> O(n).

The problem is asking a O(nlogn) when we already have a O(n) solution which is super weird.

First impression is applying a sort, but you cannot sort on this problem because you cannot break the order of array.

To do in a O(nlogn), we could have an array sum[i], indicates sum from 0 to element i.

For all the sum that’s greater or equal to s, use a binary search to find the subarray that has sum >= s and has minimum number of elements.

But still I don’t know why we are seeking for a O(nlogn).

### Solutions:

O(n) version solution:

```java
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        if (nums.length == 0)
            return 0;
        int min = Integer.MAX_VALUE;
        int left = 0;
        int right = 0;
        int sum = nums[left];
        while (right < nums.length){ 
            if (sum >= s){
                if (right - left + 1 < min)
                    min = right - left + 1;
                sum = sum - nums[left];
                left ++;
            }
            else{
                if (right == nums.length - 1)
                    break;
                else{ 
                    right ++;
                    sum = sum + nums[right];
                }
            }
        }//while
        if (min == Integer.MAX_VALUE)
            return 0;
        else
            return min;
    }
}
```