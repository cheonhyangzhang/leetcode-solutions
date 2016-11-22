# 80 Remove Duplicates from Sorted Array II – Medium


### Problem:



Follow up for “Remove Duplicates”:
What if duplicates are allowed at most twice?

For example,
Given sorted array nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn’t matter what you leave beyond the new length.


### Thoughts:



The most straight forward way is to modify the version I solution, adding a flag to indicate if an element has appeared once.

There could be a better solution that is a little simpler in code, but it has the same running complicity of O(n).


### Solutions:



Modified version I with flag:

```java
public class Solution {
    public int removeDuplicates(int[] A) {
        if (A == null || A.length == 0)
            return 0;
        int pre = A[0];
        boolean flag = false;
        int count = 0;
        // index for updating
        int o = 1;
        for (int i = 1; i < A.length; i++) {
            int curr = A[i];
            if (curr == pre) {
                if (!flag) {
                    flag = true;
                    A[o++] = curr;
                    continue;
                }  
                else {
                    count++;
                }
            } 
            else {
                pre = curr;
                A[o++] = curr;
                flag = false;
            }
        }
        return A.length - count;
    }
}
```
Simpler version code with two pointer:

```java
public class Solution {
    public int removeDuplicates(int[] A) {
        if (A.length <= 2)
            return A.length;
        int prev = 1; // point to previous
        int curr = 2; // point to current
        while (curr < A.length) {
             if (A[curr] == A[prev] && A[curr] == A[prev - 1]) {
                 curr++;
             } 
             else {
                 prev++;
                 A[prev] = A[curr];
                 curr++;
            }
       }
  
       return prev + 1;
    }
}
```