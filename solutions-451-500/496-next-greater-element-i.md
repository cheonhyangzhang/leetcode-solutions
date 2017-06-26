# 496 Next Greater Element I

### Problem:
You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.

Example 1:
```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```

Example 2:
```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```

Note:
All elements in nums1 and nums2 are unique.
The length of both nums1 and nums2 would not exceed 1000.

### Solutions:

```java
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i ++) {
            index.put(nums[i], i);
        }
        int[] result = new int[findNums.length];
        for (int i = 0; i < findNums.length; i ++) {
            result[i] = -1;
            int j = index.get(findNums[i]);
            while (j < nums.length) {
                if (nums[j] > findNums[i]) {
                    result[i] = nums[j];
                    break;
                }
                j ++;
            }
        }
        return result;
    }
}
```

```java
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        HashMap<Integer, Integer> nextgreat = new HashMap<Integer, Integer>();
        Stack<Integer> stack = new Stack<Integer>();
        int[] result = new int[findNums.length];
        for (int i = 0; i < nums.length; i ++) {
            while (!stack.isEmpty() && stack.peek() < nums[i]) {
                nextgreat.put(stack.pop(), nums[i]);
            }
            stack.push(nums[i]);
        }
        for (int i = 0; i < findNums.length; i ++) {
            result[i] = -1;
            if (nextgreat.containsKey(findNums[i])) {
                result[i] = nextgreat.get(findNums[i]);
            }
        }
        return result;
    }
}
```