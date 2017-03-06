# 239 Sliding Window Maximum

### Problem:

Given an array nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

For example,
Given nums = [1,3,-1,-3,5,3,6,7], and k = 3.
```
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```
Therefore, return the max sliding window as [3,3,5,5,6,7].

Note: 
You may assume k is always valid, ie: 1 ≤ k ≤ input array's size for non-empty array.

Follow up:
Could you solve it in linear time?

### Solutions:

```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }
        int[] res = new int[nums.length - k + 1];
        PriorityQueue<Integer> q = new PriorityQueue<Integer>(Collections.reverseOrder());
        for (int i = 0; i < k; i ++) {
            q.add(nums[i]);
        }
        res[0] = q.peek();
        for (int j = k; j < nums.length; j ++) {
            int remove = nums[j - k];
            q.add(nums[j]);
            q.remove((Integer)remove);
            res[j - k + 1] = q.peek();
        }
        return res;
    }
}
```

```java
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return new int[0];
        }
        int[] res = new int[nums.length - k + 1];
        LinkedList<Integer> q = new LinkedList<Integer>();
        for (int i = 0; i < nums.length; i ++) {
            if (!q.isEmpty() && q.peek() == i - k) {
                q.removeFirst();
            }
            while (!q.isEmpty() && nums[q.peekLast()] < nums[i]) {
                q.removeLast();
            }
            q.add(i);
            if (i + 1 >= k) {
                res[i + 1 - k] = nums[q.peekFirst()];
            }
        }
        return res;
    }
}
```