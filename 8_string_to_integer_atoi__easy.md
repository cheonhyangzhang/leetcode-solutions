# 8 String to Integer (atoi) – Easy


### Problem:


Implement atoi to convert a string to an integer.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

### Thoughts:


The tricky part for this problem is how to handle overflow.
The annoying thing here is the special cases. “010” -> 10 “+-2″ -> 0 ” 010″ -> 10 “-012ab1234” -> -12 “2147483648” -> “2147483647” “-2147483648” -> – 2147483648 Although I would think for some of these special cases we should throw Exceptions instead of returning things.

### Solutions:



```java
public class Solution {
    public int myAtoi(String str) {
        str = str.trim();
        int result = 0;
        int flag = 1;
        int start = 0;
        if (str == null || str.length() == 0){
            return 0;
        }
        if (str.charAt(0) == '-'){
            flag = -1;
            start = 1;
        }
        else if (str.charAt(0) == '+'){
            start = 1;
        }
        for (int i = start; i < str.length(); i ++){
            if (str.charAt(i) != '0'){
                start = i;
                break;
            }
        }
        for (int i = start; i < str.length(); i ++){
            char c = str.charAt(i);
            if (c < 48 || c > 57){
                break;
            }
            int digit = c - 48;
            int tmp = result * 10 + digit;
            if (tmp == Integer.MIN_VALUE && i == (str.length() -1) && str.charAt(0) == '-'){
                return Integer.MIN_VALUE;
            }
            else if ((tmp - digit) / 10 != result || (result > 0 && tmp < 0)){
                //overflow
                if (str.charAt(0) == '-'){
                    return Integer.MIN_VALUE;
                }
                else{
                    return Integer.MAX_VALUE;
                }
            }
            else{
                result = tmp;
            }
        }
        return result * flag;
    }
}
```
Updated: 10/17/2016

```java
public class Solution {
    public int myAtoi(String str) {
        str = str.trim();
        if (str.length() == 0){
            return 0;
        }
        int i = 0, flag = 1, plus = 0, minus = 0;
        long result = 0;
        if (str.charAt(0) == '-') {
            flag = -1;
            i = 1;
        }
        else if (str.charAt(0) == '+') {
            i = 1;
        }
        while (i < str.length()) {
            if (str.charAt(i) >= '0' && str.charAt(i) <= '9') {
                int digit = str.charAt(i) - '0';
                result = result * 10 + digit;
                if (result > Integer.MAX_VALUE) {
                    break;
                }
            }
            else {
                break;
            }
            i ++;
        }
        if (result*flag > Integer.MAX_VALUE) {
            return Integer.MAX_VALUE;
        }
        if (result*flag < Integer.MIN_VALUE) {
            return Integer.MIN_VALUE;
        }
        return (int) result*flag;
    }
}
```