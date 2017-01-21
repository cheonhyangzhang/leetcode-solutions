# 345. Reverse Vowels of a String

### Problem:

Write a function that takes a string as input and reverse only the vowels of a string.

Example 1:
Given s = "hello", return "holle".

Example 2:
Given s = "leetcode", return "leotcede".

Note:
The vowels does not include the letter "y".

Show Company Tags
Show Tags
Show Similar Problems


### Solutions:

```java
public class Solution {
    public String reverseVowels(String s) {
        HashSet<Character> vowels = new HashSet<Character>();
        Collections.addAll(vowels, 'a','e','i','o','u','A','E','I','O','U');
        int left = 0, right = s.length() - 1;
        char[] chars = s.toCharArray();
        while (left < right) {
            if (!vowels.contains(chars[left])) {
                left ++;
                continue;
            }
            if (!vowels.contains(chars[right])) {
                right --;
                continue;
            }
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