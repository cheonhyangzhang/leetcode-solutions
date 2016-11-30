# 137 Single Number II – Medium


### Problem:



Given an array of integers, every element appears three times except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?


### Thoughts:



This is surely a tricky question. It’s good to know how to solve. But I don’t think this is a good interview question, namely not a good question to measure a programmer’s problem solving skills.

We keep variable for number that appears once, twice and three times. Each iteration updates these three variables and the variable for appearing once will be the returning result.

The key idea is that we need to get rid of the number that appears three times from the variable for once and twice.


### Solutions:



```java
public class Solution {
    public int singleNumber(int[] nums) {
        int one = 0;
        int two = 0;
        int three = 0;
        for (int i = 0; i < nums.length; i ++){
            two = two | ( one & nums[i]);
            one = one ^ nums[i];
            three = one & two;
            one = one & (~three);
            two = two & (~three);
        }//for
        return one;
    }
}
```