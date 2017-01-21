# 344. Reverse String `

### Problem:

Write a function that takes a string as input and returns the string reversed.

Example:
Given s = "hello", return "olleh".


### Solutions:

```java
public class Solution {
    public String reverseString(String s) {
        int left = 0, right = s.length() - 1;
        StringBuilder sb = new StringBuilder(s);
        while (left < right) {
            char tmp = s.charAt(left);
            sb.setCharAt(left, s.charAt(right));
            sb.setCharAt(right, tmp);
            left ++;
            right --;
        }
        return sb.toString();
    }
}
```

```java
public class Solution {
    public String reverseString(String s) {
        int left = 0, right = s.length() - 1;
        char[] chars = s.toCharArray();
        while (left < right) {
            char tmp = chars[left];
            chars[left] = chars[right];
            chars[right] = tmp;
            left ++;
            right --;
        }
        return new String(chars);
    }
}
```