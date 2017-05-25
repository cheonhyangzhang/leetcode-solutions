166 Fraction to Recurring Decimal

### Problem:
Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

For example,

* Given numerator = 1, denominator = 2, return “0.5”.
* Given numerator = 2, denominator = 1, return “2”.
* Given numerator = 2, denominator = 3, return “0.(6)”.

### Thoughts:
One annoying point is that integer overflow, so the solution below is using long instead of integer.

Using a HashMap to store remainder so that we could know if a same remainder exists.

### Solutions:

```java
public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        long n = numerator, d = denominator;
        if (n % d == 0) {
            return n / d + "";
        }
        boolean neg = false;
        if ((n < 0 && d > 0) || (n > 0 && d < 0)) {
            neg = true;
        }
        if (n < 0) {
            n = -n;
        }
        if (d < 0) {
            d = -d;
        }
        HashMap<Long, Integer> index = new HashMap<Long, Integer>();
        String result = "";
        result += n / d + ".";
        n = n % d;
        while (n != 0) {
            if (index.containsKey(n)) {
                //recurring
                result = result.substring(0, index.get(n)) + "(" + result.substring(index.get(n)) + ")";
                break;
            }
            index.put(n, result.length());
            result += n*10/d;
            n = n*10 % d;
        }
        if (neg == true) {
            result = '-' + result;
        }
        return result;
    }
}
```