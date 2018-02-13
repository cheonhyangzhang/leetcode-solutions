# 493 Reverse Pairs

### Problem:
Given an array nums, we call (i, j) an important reverse pair if i < j and nums[i] > 2*nums[j].

You need to return the number of important reverse pairs in the given array.

Example1:
```
Input: [1,3,2,3,1]
Output: 2
```
Example2:
```
Input: [2,4,3,5,1]
Output: 3
```

Note:
The length of the given array will not exceed 50,000.
All the numbers in the input array are in the range of 32-bit integer.

### Solutions:

```java
public class Solution {
    public int reversePairs(int[] nums) {
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        int[] sorted = new int[nums.length];
        int[] bit = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i ++) {
            sorted[i] = nums[i];
        }
        Arrays.sort(sorted);
        for (int i = 0; i < sorted.length; i ++) {
            index.put(sorted[i], i + 1);
        }
        int res = 0;
        for (int i = nums.length - 1; i >= 0; i --) {
            int j = index(sorted, (double) nums[i]/2.0);
            int tmp = getSum(bit, j);
            res += tmp;
            update(bit, index.get(nums[i]));
        }
        return res;
    }
    private int index(int[] sorted, double val) {
        int left = 0, right = sorted.length - 1;
        while (left <= right) {
            int mid = (right - left) / 2 + left;
            if (sorted[mid] >= val) {
                right = mid - 1;
            }
            else {
                left = mid + 1;
            }
        }
        return right + 1;
    }
    private int getSum(int[] bit, int i) {
        int res = 0;
        while (i > 0) {
            res += bit[i];
            i -= (i&(-i));
        }
        return res;
    }
    private void update(int[] bit, int i) {
        while (i < bit.length) {
            bit[i] ++;
            i += (i&(-i));
        }
    }
}
```

```java
public class Solution {
    public int reversePairs(int[] nums) {
        int res = mergesort(nums, 0, nums.length - 1);
        return res;
    }
    private int mergesort(int[] nums, int start, int end) {
        if (start >= end) {
            return 0;
        }
        int mid = (end - start) / 2 + start;
        int res = mergesort(nums, start, mid) + mergesort(nums, mid + 1, end);
        for (int i = start, j = mid + 1; i <= mid; i ++) {
            while (j <= end && (double)nums[i] / 2.0 > nums[j]) {
                j ++;
            }
            res += j - mid - 1;
        }
        merge(nums, start, mid, mid + 1, end);
        return res;
    }
    private void merge(int[] nums, int s1, int e1, int s2, int e2) {
        int[] result = new int[e2 - s1 + 1];
        int i = s1, j = s2, k = 0;
        while (i <= e1 || j <= e2) {
            long a = Long.MAX_VALUE;
            long b = Long.MAX_VALUE;
            if (i <= e1) {
                a = nums[i];
            }
            if (j <= e2) {
                b = nums[j];
            }
            if (a < b) {
                result[k++] = (int)a;
                i ++;
            }
            else {
                result[k++] = (int)b;
                j ++;
            }
        }
        for (k = 0; k < result.length; k ++) {
            nums[s1 + k] = result[k];
        }
    }
}
```

```java
public class Solution {
    public int reversePairs(int[] nums) {
        int res = mergesort(nums, 0, nums.length - 1);
        return res;
    }
    private int mergesort(int[] nums, int start, int end) {
        if (start >= end) {
            return 0;
        }
        int mid = (end - start) / 2 + start;
        int res = mergesort(nums, start, mid) + mergesort(nums, mid + 1, end);
        for (int i = start, j = mid + 1; i <= mid; i ++) {
            while (j <= end && (double)nums[i] / 2.0 > nums[j]) {
                j ++;
            }
            res += j - mid - 1;
        }
        merge(nums, start, mid, mid + 1, end);
        return res;
    }
    private void merge(int[] nums, int s1, int e1, int s2, int e2) {
        int[] result = new int[e2 - s1 + 1];
        int i = s1, j = s2, k = 0;
        while (i <= e1 || j <= e2) {
            int a = Integer.MAX_VALUE;
            int b = Integer.MAX_VALUE;
            if (i <= e1) {
                a = nums[i];
            }
            if (j <= e2) {
                b = nums[j];
            }
            if (a < b) {
                result[k++] = a;
                i ++;
            }
            else if (a > b){
                result[k++] = b;
                j ++;
            }
            else {
                if (j == e2 + 1) {
                    result[k++] = a;
                    i ++;
                }
                else {
                    result[k++] = b;
                    j ++;
                }
            }
        }
        for (k = 0; k < result.length; k ++) {
            nums[s1 + k] = result[k];
        }
    }
}
```