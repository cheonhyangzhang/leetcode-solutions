# 7 Reverse Integer – Easy


### Problem:


Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

Things not provided by the problem itself:
If the integer’s last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.


### Thoughts:


The tricky part is how to handle overflow case. How to determine overflow.
There is no one perfect way to determine overflow during integer calculation. It varies depending on what the specific calculation is.

Say int a = 964632435. a * 10 overflows. but the result is 1056389759 still a positive not a negative. So cannot use result < 0 to determine overflow. The formula to calculate next Integer is b = a * 10 + 1. Because is always a valid integer. So could use ( b – 1) / 10 == a to determine overflow. Also remember Java Integer Range is from -2xxxxxx8 to 2xxxxxx7. Not balanced. Condition result != (newresult – digit) / 10 is not safe enough, say if x * 10 + digit = Integer.MAX + 1. It overflows but reverse is still right. But this problem is never facing this special case because if reverse if Integer.MAX + 1 then the original number is not a valid Integer.


### Solutions:



```java
public class Solution {
    // -8 ~  7
    public int reverse(int x) {
        if (x == Integer.MIN_VALUE){
            // will overflow
            return 0;
        }
        else{
            int flag = 1;
            if (x < 0){
                flag = -1;
                x = -x;
            }
            int result = 0;
            while(x > 0){
                int digit = x % 10;
                int newresult = result * 10 + digit; 
                if (result != (newresult - digit) / 10){
                    result = 0;
                    break;
                }
                result = newresult;
                x = x / 10;
            }
            result = result * flag;
            return result;
        }//else
         
    }//public int 
}
```