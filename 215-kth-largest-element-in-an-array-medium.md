# 215 Kth Largest Element in an Array – Medium


### Problem:
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,
Given [3,2,1,5,6,4] and k = 2, return 5.

Note: 
You may assume k is always valid, 1 ≤ k ≤ array’s length.

### Thoughts:
The trivial solution would be using a sort, either quicksort or mergesort.

Since sorting is O(nlogn), and additional step is to turn the nums.length – k element, so this trivial approach is O(nlogn).

Better approach is to use a quickSelect way. Average running time for quickSelect is O(n), so this is a faster approach comparing the sorting approach.

In the solution below, quickSelect it to select the (k+1)th smallest element instead.

### Solutions:

```java
public class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, 0, nums.length - 1, k);
    }
    private int quickSelect(int[] nums, int start, int end, int k) {
        int index = partition(nums, start, end, k);
        int right = end - index + 1;
        if (right == k) {
            return nums[index];
        }
        if (right > k) {
            return quickSelect(nums, index + 1, end, k);
        }
        else {
            return quickSelect(nums, start, index - 1, k - right);
        }
    }
    private int partition(int[] nums, int start, int end, int k) {
        int pivot = nums[end];
        int index = end - 1;
        while (start <= index) {
            if (nums[start] > pivot) {
                while (index > start && nums[index] > pivot) {
                    index --;
                }
                int tmp = nums[start];
                nums[start] = nums[index];
                nums[index] = tmp;
                index --;
            }
            start ++;
        }
        nums[end] = nums[index + 1];
        nums[index + 1] = pivot;
        return index + 1;
    }
     
}
```