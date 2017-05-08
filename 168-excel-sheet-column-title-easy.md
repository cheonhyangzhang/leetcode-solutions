168 Excel Sheet Column Title – Easy

### Problem:
Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:
```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
```

### Thoughts:

This is like a base of 26 problem. Also remember, the letter starts as A which should be mapping to 0, while Z be mapping to 25. So remember to subtract 1 when doing the division and module.

### Solutions:
```java
public class Solution {
    public String convertToTitle(int n) {
        String result = "";
        while (n != 0) {
            int tmp = (n - 1) % 26;
            result = (char)('A' + tmp) + result;
            n = (n - 1)/ 26;
        }
        return result;
    }
}
```