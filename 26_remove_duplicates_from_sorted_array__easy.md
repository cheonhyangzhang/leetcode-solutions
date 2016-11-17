# 26 Remove Duplicates from Sorted Array – Easy


### Problem:



Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn’t matter what you leave beyond the new length.


### Thoughts:


The solution is very straightfoward.


### Solutions:



```java
public class Solution {
    public int removeDuplicates(int[] A) {
        if (A.length == 0){
            return 0;
        }
        int curr = A[0];
        int toFill = 1;
        for (int i = 1; i < A.length; i ++){
            if (A[i] != curr){
                curr = A[i];
                A[toFill] = curr;
                toFill ++;
            }
        }//for i
        return toFill;
    }//removeDuplicates
}//Solution
```