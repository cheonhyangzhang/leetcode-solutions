# 33 LeetCode Java: Search in Rotated Sorted Array – Hard

### Problem:

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.



---



### Thoughts

If the sorted array is not rotated, then this is a question of standard binary search. However, when the array is rotated, we will need some modification of standard binary search.
But before that let’s look at one simple and straightforward way to leverage standard binary tree.

Solution 1:
For [4,5,6,7,0,1,2], we noticed that the the problem can be broken into two sub problems, find the target in [4,5,6,7] and in [0,1,2]. Then All we need to do is to find the cutting point. It will be the first element that is larger then the next element, which is 7 in this case. Also need to remember that we need to handle the case the array is not rotated at all. So we need to set the initial cut point index to be the last element of the array.

Solution 2:
Modify the checking condition when moving start and end pivot in standard binary search. We get the mid element of given start and end. If the element equals the target, then good, we can return the index.

After we calculate the mid index, let’s see where the mid is at. In the picture above, there are two cases for the mid point. Either at A or at B.
When mid is at A, we need to find a way to determine if we want to go to the left half or right half. We can see that the easier way is to check the left half, which is nums[start] <=target < nums[mid]. Otherwise, it's falling into the right half.
Similar strategy applies for the case when mid is at point B.


---



### Solutions:

Solution 1:
```
public class Solution {
    public int search(int[] nums, int target) {
        int cut = nums.length - 1;
        for (int i = 0; i < nums.length - 1; i ++) {
            if (nums[i] > nums[i+1]) {
                cut = i;
                break;
            }
        }
        int firstHalf = search(nums, target, 0, cut);
        if ( firstHalf != -1) {
            return firstHalf;
        }
        int secondHalf = search(nums, target, cut + 1, nums.length -1);
        return secondHalf;
    }
    private int search(int[] nums, int target, int start, int end) {
        if (start > end) {
            return -1;
        }
        int mid = (start + end) / 2;
        if (nums[mid] > target) {
            return search(nums, target, start, mid -1);
        }
        if (nums[mid] < target) {
            return search(nums, target, mid + 1, end);
        }
        return mid;
    }
}
```
Solution 2:
```
public class Solution {
    public int search(int[] nums, int target) {
        int start = 0, end = nums.length - 1;
        while (start <= end) {
            int mid = ( start + end) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[start] <= nums[mid]) {
                if (nums[start] <= target && target < nums[mid]) {
                    end = mid -1;
                }
                else {
                    start = mid + 1;
                }
            }
            else{
                if (nums[mid] < target && target <= nums[end]) {
                    start = mid + 1;
                }
                else {
                    end = mid -1;
                }
            }
        }
        return -1;
    }
}
```
