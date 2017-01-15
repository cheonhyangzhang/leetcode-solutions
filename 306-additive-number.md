# 306 Additive Number

### Problem:

<pre>
Additive number is a string whose digits can form additive sequence.

A valid additive sequence should contain at least three numbers. Except for the first two numbers, each subsequent number in the sequence must be the sum of the preceding two.

For example:
"112358" is an additive number because the digits can form an additive sequence: 1, 1, 2, 3, 5, 8.

1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8
"199100199" is also an additive number, the additive sequence is: 1, 99, 100, 199.
1 + 99 = 100, 99 + 100 = 199
Note: Numbers in the additive sequence cannot have leading zeros, so sequence 1, 2, 03 or 1, 02, 3 is invalid.

Given a string containing only digits '0'-'9', write a function to determine if it's an additive number.

Follow up:
How would you handle overflow for very large input integers?
</pre>

### Solutions:

```java
import java.math.BigInteger;

public class Solution {
    public boolean isAdditiveNumber(String num) {
        for (int i = 1; i < num.length(); i ++) {
            for (int j = i + 1; j < num.length() - i + 1; j ++) {
                String first = num.substring(0, i);
                String second = num.substring(i, j);
                if (isValid(j, first, second, num)) {
                    return true;
                }
            }
        }
        return false;
    }
    private boolean isValid(int start, String first, String second, String num) {
        if (start == num.length()) {
            return true;
        }
        if ((first.charAt(0) == '0' && first.length() > 1) || (second.charAt(0) == '0' && second.length() > 1)) {
            return false;
        }
        BigInteger f = new BigInteger(first);
        BigInteger s = new BigInteger(second);
        BigInteger sum = f.add(s);
        String sumStr = sum.toString();
        if (sumStr.length() + start > num.length()) {
            return false;
        }
        System.out.println("has following:" + first + " : " + second + " : " + start);
        if (!num.substring(start, start + sumStr.length()).equals(sumStr)) {
            return false;
        }
        return isValid(start + sumStr.length(), second, sumStr, num);
        
    }
}
```