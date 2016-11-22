# 75 Sort Colors – Medium


### Problem:



Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:
You are not suppose to use the library’s sort function for this problem.

A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0’s, 1’s, and 2’s, then overwrite array with total number of 0’s, then 1’s and followed by 2’s.

Could you come up with an one-pass algorithm using only constant space?


### Thoughts:



Doing in one pass needs two flags pointer, one left one right.


### Solutions:



```java
public class Solution {
    public void sortColors(int[] nums) {
        int redSt=0, bluSt=nums.length-1;
        int i=0;
        while(i<bluSt+1){
            if(nums[i]==0){
                int tmp = nums[i];
                nums[i] = nums[redSt];
                nums[redSt] = tmp;
                redSt++;
                i++;
                continue;
            }
            if(nums[i] ==2){
                int tmp = nums[i];
                nums[i] = nums[bluSt];
                nums[bluSt] = tmp;
                bluSt--;
                continue;
            }
            i++;
        }
    }
}
```