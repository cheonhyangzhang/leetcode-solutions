# 88 Merge Sorted Array


### Problem:


Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

### 
Thoughts:


This is a quite straightforward problem. Only one trick is that we need to merge two sorted array from the right to left not the other way around.
Because we need to merge two array in place and cannot overwrite unmerged element.


### Solution:


This version the code is more clear, only one loop.

```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        m --;
        n --;
        for (int i = m + n + 1; i >=0; i --) {
            int a = m >=0 ? nums1[m]:Integer.MIN_VALUE;
            int b = n >=0 ? nums2[n]:Integer.MIN_VALUE;
            if (a > b) {
                nums1[i] = a;
                m --;
            }
            else {
                nums1[i] = b;
                n --;
            }
        }
    }
}
```
Here is an alternative solution.
```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        m --;
        n --;
        int i = m + n + 1;
        while (m >=0 && n >=0) {
            if (nums1[m] > nums2[n]) {
                nums1[i--] = nums1[m--];
            }
            else {
                nums1[i--] = nums2[n--];
            }
        }
        while (m >=0) {
            nums1[i--] = nums1[m--];
        }
        while (n >=0) {
            nums1[i--] = nums2[n--];
        }
    }
}
```