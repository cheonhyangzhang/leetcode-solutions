# 60 Permutation Sequence – Medium


### Problem:


The set [1,2,3,…,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

"123"
"132"
"213"
"231"
"312"
"321"
Given n and k, return the kth permutation sequence.

Note: Given n will be between 1 and 9 inclusive.


### Thoughts:



In order to make calculation easier, we need to decrease k at the very beginning.

If n = 4, k = 9.

Decrease k to be 8. All index is starting at 0.

For the first number,  is the (8 / 3!)th , which is 2 of the remaining number {1, 2, 3, 4}.

For the second number, is  k1= (8%3!) , and order is k1 / 2!= 1 , which is 3 of the remaining number (1, 3, 4}

For the third number is  k2 = k1 % 2! = 0, and order is k2 / 1! = 0, which is 1 of the remaining number of {1,4}

For the fouth number is k3 = k2 %1! = 0, and order is k3/ 0! = 0, which is 1 of the remaining number {4}

In order to make calculation correct, we assume 0! = 1


### Solutions:


```java
public class Solution {
    public String getPermutation(int n, int k) {
        int[] fact = new int[n];
        fact[0] = 1;
        ArrayList<Integer> nums = new ArrayList<Integer>();
        nums.add(1);
        for (int i = 1; i < n; i++) {
            fact[i] = fact[i-1] * i;
            nums.add(i+1);
        }
        String result = "";
        k = k - 1;
        for (int i = 0; i < n; i++) {
            int index = k / fact[n-1-i];
            result = result + (nums.get(index) + "");
            nums.remove(index);
            k = k % fact[n-1-i];
        }
        return result;
    }
}
```