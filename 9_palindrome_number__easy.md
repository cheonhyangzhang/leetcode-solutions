# 9 Palindrome Number – Easy


### Problem:



Determine whether an integer is a palindrome. Do this without extra space.

Some hints:

Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem “Reverse Integer”, you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.


### Thoughts:



This question is not very interesting. The requirement “without extra space” is kind of tricky to understand. Maybe it’s trying to say if the number is n digit long, solve it with O(1) space instead of O(n) space.


### Solutions:



```java
public class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        int left = 1;
        while (x / left >= 10) {
            left = left * 10;
        }
        int right = 1;
        while (left > right) {
            if ((x / left) % 10 != (x / right) % 10 ) {
                return false;
            }
            left = left / 10;
            right = right * 10;
        }
        return true;
    }
}
```