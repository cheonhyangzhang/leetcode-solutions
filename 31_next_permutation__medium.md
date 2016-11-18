# 31 Next Permutation – Medium


### Problem:



Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1


### Thoughts:



A lot of problems are solved by mimic human thinking. So is this one.

Here are the steps we need to follow to solve the problem:

1 From right to left, find the first element that is violating the increase trend, this is called PartitionNumber

2 From right to left, find the first element that is larger than PartitionNumber, this is called ChangeNumber.

3 Switch PartitionNumber and ChangeNumber

4 Reverse all the digit on the right of particionNumber ( Original index)

This problem is not easy to solve even it’s marked as medium.


### Solutions:


```java
public class Solution {
    public void nextPermutation(int[] nums) {
        int paNumIndex = -1;
        for (int i = nums.length - 1; i >0; i --){
            if (nums[i-1] < nums[i]){ 
                paNumIndex = i-1; 
                break; 
            } 
        } 
        if (paNumIndex != -1){ 
            int chNumIndex = -1;
            for (int i = nums.length - 1; i > paNumIndex; i --){
                if (nums[i] > nums[paNumIndex]){
                    chNumIndex = i;
                    break;
                }
            }
            int tmp = nums[paNumIndex];
            nums[paNumIndex] = nums[chNumIndex];
            nums[chNumIndex] = tmp;
        }
        int start = paNumIndex + 1, end = nums.length -1;
        while (start < end) {
            int tmp = nums[start];
            nums[start] = nums[end];
            nums[end] = tmp;
            start ++;
            end --;
        }
  
    }//nextPermutation
}//Solution
```