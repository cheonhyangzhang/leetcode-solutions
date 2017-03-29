# 330 Patching Array

### Problem:

Given a sorted positive integer array nums and an integer n, add/patch elements to the array such that any number in range [1, n] inclusive can be formed by the sum of some elements in the array. Return the minimum number of patches required.

Example 1:
nums = [1, 3], n = 6
Return 1.

Combinations of nums are [1], [3], [1,3], which form possible sums of: 1, 3, 4.
Now if we add/patch 2 to nums, the combinations are: [1], [2], [3], [1,3], [2,3], [1,2,3].
Possible sums are 1, 2, 3, 4, 5, 6, which now covers the range [1, 6].
So we only need 1 patch.

Example 2:
nums = [1, 5, 10], n = 20
Return 2.
The two patches can be [2, 4].

Example 3:
nums = [1, 2, 2], n = 5
Return 0.

### Solutions:

Memory exceeded solution

```java
public class Solution {
    public int minPatches(int[] nums, int n) {
        boolean[] has = new boolean[n];
        int[] toFill = new int[1];
        toFill[0] = n;
        for (int i = 0; i < nums.length; i ++) {
            if (nums[i] <= n) {
                addElement(nums[i], has, nums, toFill, n);
            }
        }
        int start = 0;
        int count = 0;
        while (toFill[0] != 0) {
            while (has[start] == true) {
                start ++;
            }
            addElement(start + 1, has, nums, toFill, n);
            count ++;
        }
        return count;
    }
    private void addElement(int add, boolean[] has, int[] nums, int[] toFill, int n) {
        Queue<Integer> added = new LinkedList<Integer>();
        for (int j = 0; j < n; j ++) {
            if (has[j] == true && j + add < n && has[j + add] == false) {
                added.add(j + add);
            }
        }
        while (!added.isEmpty()) {
            has[added.poll()] = true;
            toFill[0] --;
        }
        if (has[add - 1] == false) {
            has[add - 1] = true;
            toFill[0] --;
        }
    }
}
```

Greedy working solution

```java
public class Solution {
    public int minPatches(int[] nums, int n) {
        long miss = 1;
        int count = 0;
        int i = 0;
        while (miss <= n) {
            if (i < nums.length && nums[i] <= miss) {
                miss += nums[i];
                i ++;
            }
            else {
                miss += miss;
                count ++;
            }
        }
        return count;
    }
}
```