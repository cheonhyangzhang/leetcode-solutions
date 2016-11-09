# 1 Leetcode Java: Two Sum – Medium


### Problem


Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

**UPDATE (2016/2/13):**
The return format had been changed to zero-based indices. Please read the above updated description carefully.

 


### Thoughts:



The most straight forward solution would be a nested loop. This would end up with running complicity of O(n2).

With the help of a hash-table, we could improve running complicity to O(n), but this requires space O(n). This is very common in coding problem. Sometimes, in order to improve the running time, you have to trade off on space.

 


### O(n2) solution:


```
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for (int i = 0; i < nums.length; i ++){
            for (int j = i + 1; j < nums.length; j++){
                if (nums[i] + nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
         }
         return result;
    }
}
```

### O(n) solution:
```
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        HashMap<Integer, Integer> appear = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i ++){
            appear.put(nums[i], i);
        }
        for (int i = 0; i < nums.length; i ++){
            if (appear.containsKey(target - nums[i])){
                int j = appear.get(target - nums[i]);
                if ( i != j){
                    result[0] = Math.min(i, j);
                    result[1] = Math.max(i, j);
                    return result;
                }
 
            }
        }
        return result;
    }
}
```
Note: line 11, i != j is to make sure that for case [3, 2, 4] and target 6, don’t return [1,1].

Also, using line 11 i != j, is going to solve this case [3, 1, 4, 3]. Because for element with value 3, it’s put into hash map twice and the value will be <3, 3> , index 3 is stored. so that when iterating over the array, when i = 0, value is 3, then the index get back from hash map for value 3 is index 3, where j = 3, so that [0, 3] is returned which is the expected output.

This solution will work because of the assumption:

You may assume that each input would have exactly one solution.

This makes sure that there will be at most 2 elements that has the same value. ( Actually it can have more than 2, but the element will never be part of the output. )