# 12 Integer to Roman – Medium


### Problem:



Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.


### Thoughts:


Key idea is to switch number by different cases.

Instead of having the base character into
{“M”,”CM”,”D”,”CD”,”C”,”XC”,”L”,”XL”,”X”,”IX”, “V”, “IV”, “I”}
its makes us easier to handle the special case for 9 and 4.
By using the new base character, roman numeric can be only the 1 – 3 appearance of the characters above. So there is no special case we need to handle like we do in the above solution.
The key takeaway here is that if a problem is very annoying and has many special case we need to handle. Think about is there a way we can have a helper variable that can help reduce the annoying part. Especially when you have a lot of if else.

### Solutions:
```java
public class Solution {
    public String intToRoman(int num) {
        int[] base = new int[]{1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] chars = new String[]{"M","CM","D","CD","C","XC","L","XL","X","IX", "V", "IV", "I"};
        //expand the "base" char to make sure that the roman numeric can be only the 1 - 3 appearance of the characters above
        String result = "";
        for (int i = 0; i < base.length; i ++) {
            if (num / base[i] > 0) {
                for (int j = 0; j < num/base[i]; j ++) {
                    result = result + chars[i];
                }
                num = num - (num / base[i]) * base[i];
            }
        }
        return result;
    }
}
```
