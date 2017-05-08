# 171 Excel Sheet Column Number – Easy


### Problem:
Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:
```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28
```

### Thoughts:
This is like a base of 26 system problem. It’s similar but easier than the reverse.

Because no need to worry about minus one problem.

### Solutions:

```java
public class Solution {
    public int titleToNumber(String s) {
        int result = 0;
        for (int i = 0; i < s.length(); i ++) {
            int digit = s.charAt(i) - 'A' + 1;
            result = result * 26 + digit;
        }
        return result;
    }
}
```