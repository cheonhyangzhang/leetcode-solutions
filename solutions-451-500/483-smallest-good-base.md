# 483. Smallest Good Base

### Problem:

For an integer n, we call k>=2 a good base of n, if all digits of n base k are 1.

Now given a string representing n, you should return the smallest good base of n in string format. 

Example 1:
```
Input: "13"
Output: "3"
Explanation: 13 base 3 is 111.
```

Example 2:
```
Input: "4681"
Output: "8"
Explanation: 4681 base 8 is 11111.
```

Example 3:
```
Input: "1000000000000000000"
Output: "999999999999999999"
Explanation: 1000000000000000000 base 999999999999999999 is 11.
```

Note:
The range of n is [3, 10^18].
The string representing n is always valid and will not have leading zeros.

### Solutions:

```java
public class Solution {
    public String smallestGoodBase(String n) {
        long num = Long.parseLong(n);
        for (long length = (long)(Math.log(num) / Math.log(2)) + 1; length >= 2; length --) {
            // System.out.println(length);
            long left = 2, right = (long)Math.pow(num + 1, 1.0 / (double)(length - 1));
            while (left <= right) {
                long mid = (right - left) / 2 + left;
                long sum = 0;
                for (int i = 0; i < length; i ++) {
                    sum = sum * mid + 1;
                }
                // System.out.println("Sum : " + sum);
                if (sum == num) {
                    return mid + "";
                }
                else if (sum < num) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }
        }
        return (num - 1) + "";
    }
}
```