# 67 Add Binary – Easy


### Problem:



Given two binary strings, return their sum (also a binary string).

For example,
a = "11"
b = "1"
Return "100".


### Thoughts:



Very straight forward solution.


### Solutions:


Improve logic. This is a version of solution that is more into clean code. If looking for a more efficient way, need to avoid unnecessary calculation, e.g. when you have a lot of 0 in the end for both number, you don’t want to keep calculate 0 + 0 + 0.

```java
public class Solution {
    public String addBinary(String a, String b) {
        String result = "";
        int i = a.length() - 1, j = b.length() - 1;
        int carry = 0;
        while (i >=0 || j >=0) {
            int tmp = (i >=0?(a.charAt(i)- '0'):0 ) + (j >=0?(b.charAt(j) - '0'):0) + carry;
            carry = tmp / 2;
            int digit = tmp % 2;
            result = digit + result;
            i --;
            j --;
        }
        if (carry > 0) {
            result = carry + result;
        }
        return result;
    }
}
```
An example to avoid unnecessary calculation for special case.

```java
public class Solution {
    public String addBinary(String a, String b) {
        String result = "";
        int i = a.length() - 1, j = b.length() - 1;
        int carry = 0;
        while (i >=0 && j >=0 && a.charAt(i) == '0' && b.charAt(j) == '0') {
            result = '0' + result;
            i --;
            j --;
        }
        while (i >=0 || j >=0) {
            int tmp = (i >=0?(a.charAt(i)- '0'):0 ) + (j >=0?(b.charAt(j) - '0'):0) + carry;
            carry = tmp / 2;
            int digit = tmp % 2;
            result = digit + result;
            i --;
            j --;
        }
        if (carry > 0) {
            result = carry + result;
        }
        return result;
    }
}
```