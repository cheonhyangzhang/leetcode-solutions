# 480 Sliding Window Median

### Problem:

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

Examples: 
[2,3,4] , the median is 3

[2,3], the median is (2 + 3) / 2 = 2.5

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position. Your job is to output the median array for each window in the original array.

For example,
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.
```
Window position                Median
---------------               -----
[1  3  -1] -3  5  3  6  7       1
 1 [3  -1  -3] 5  3  6  7       -1
 1  3 [-1  -3  5] 3  6  7       -1
 1  3  -1 [-3  5  3] 6  7       3
 1  3  -1  -3 [5  3  6] 7       5
 1  3  -1  -3  5 [3  6  7]      6
```

Therefore, return the median sliding window as [1,-1,-1,3,5,6].

Note: 
You may assume k is always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

### Solutions:

```java
public class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {
        int[] win = new int[k];
        for (int i = 0; i < k; i ++) {
            win[i] = nums[i];
        }
        Arrays.sort(win);
        double med = (double)(win[k/2]) / 2 + (double)win[(k - 1)/2] / 2;
        double[] res = new double[nums.length - k + 1];
        PriorityQueue<Integer> left = new PriorityQueue<Integer>(Collections.reverseOrder());
        PriorityQueue<Integer> right = new PriorityQueue<Integer>();
        for (int i = 0; i < k; i ++) {
            if ((double)nums[i] <= med) {
                left.add(nums[i]);
            }
            else {
                right.add(nums[i]);
            }
        }
        res[0] = med;
        for (int i = k; i < nums.length; i ++) {
            if (nums[i] <= med) {
                left.add(nums[i]);
            }
            else {
                right.add(nums[i]);
            }
            int remove = nums[i - k];
            if (remove <= med) {
                left.remove(remove);
            }
            else {
                right.remove(remove);
            }
            while (left.size() < right.size()) {
                left.add(right.poll());
            } 
            while (left.size() > right.size() + 1) {
                right.add(left.poll());
            }
            if (left.size() == right.size()) {
                med = (double)left.peek() / 2 + (double)right.peek() / 2;
            }
            else {
                med = left.peek();
            }
            res[i - k + 1] = med;
        }
        return res;
    }
}
```