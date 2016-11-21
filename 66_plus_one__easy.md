# 66 Plus One – Easy


### Problem:



Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.


### Thoughts:



This is a little tricky question. The interface requires to return int[], but you are not sure what’s the length for the returning array. Given input array, int[] digits, it could be digits.length or digits.length + 1.


### Solutions:



```java
public class Solution {
    public int[] plusOne(int[] digits) {
        int carry = 1;
        int i = digits.length - 1;
        while (i >=0 && digits[i] == 9) {
            i --;
        }
        if (i == -1) {
            int[] result = new int[digits.length + 1];
            result[0] = 1;
            return result;
        }
        // If it's find to modify int[] digits, then can only modify digit at index i
        // This will save lots of unnecessary operation.
        int[] result = new int[digits.length];
        result[i] = digits[i] + 1;
        for (int j = 0; j < i; j ++) {
            result[j] = digits[j];
        }
        return result;
    }
}
```
This solution will avoid unnecessary calculation in the first solution.
```java
int tmp = digits[i] + toAdd;
result = (tmp % 10) + result;
toAdd = tmp / 10;
```
when the number given has a lot of 9, then there is no need to do these calculation. Because when you initialize an array of integer in Java, it has default value of 0 already.