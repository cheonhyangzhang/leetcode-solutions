# 324. Wiggle Sort II

### Problem:

Given an unsorted array nums, reorder it such that nums[0] < nums[1] > nums[2] < nums[3]....

Example:
(1) Given nums = [1, 5, 1, 1, 6, 4], one possible answer is [1, 4, 1, 5, 1, 6]. 
(2) Given nums = [1, 3, 2, 2, 3, 1], one possible answer is [2, 3, 1, 3, 1, 2].

Note:
You may assume all input has valid answer.

Follow Up:
Can you do it in O(n) time and/or in-place with O(1) extra space?

### Solutions:

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        int[] tmp = new int[nums.length];
        Arrays.sort(nums);
        int left = (nums.length - 1) / 2, right = nums.length - 1;
        for (int i = 0; i < tmp.length; i ++) {
            if (i % 2 == 0) {
                tmp[i] = nums[left--];
            }
            else {
                tmp[i] = nums[right--];
            }
        }
        for (int i = 0; i < tmp.length; i ++) {
            nums[i] = tmp[i];
        }
    }
}
```

```java
public class Solution {
    public void wiggleSort(int[] nums) {
        int median = quickSelect(nums, 0, nums.length - 1, (nums.length + 1)/ 2);
        int i = 0, j = 0, k = nums.length - 1;
        while (i <= k) {
            int it = index(i, nums.length), jt = index(j, nums.length), kt = index(k, nums.length);
            if (nums[it] > median) {
                int tmp = nums[it];
                nums[it] = nums[jt];
                nums[jt] = tmp;
                i ++;
                j ++;
            }
            else if (nums[it] < median) {
                int tmp = nums[it];
                nums[it] = nums[kt];
                nums[kt] = tmp;
                k --;
            }
            else {
                i ++;
            }
        }
    }
    private int index(int i, int n) {
        if (i < n /2) {
            return i * 2 + 1;
        }
        else {
            return (i - n / 2) * 2;
        }
    }
    private int partition(int[] nums, int left, int right) {
        int x = nums[right];
        int i = left;
        int j = right - 1;
        while (i <= j) {
            if (nums[i] <= x) {
                i ++;
            }
            else {
                if (nums[j] > x) {
                    j --;
                }
                else {
                    int tmp = nums[i];
                    nums[i] = nums[j];
                    nums[j] = tmp;
                    i ++;
                    j --;
                }
            }
        }
        nums[right] = nums[i];
        nums[i] = x;
        return i;
    }
    private int quickSelect(int[] nums, int left, int right, int i) {
        if (left == right) {
            return nums[left];
        }
        int q = partition(nums, left, right);
        int k = q - left + 1;
        if (i == k){
            return nums[q];
        }
        else if (i < k) {
            return quickSelect(nums, left, q - 1, i);
        }
        else {
            return quickSelect(nums, q + 1, right, i - k);
        }
    }
}
```