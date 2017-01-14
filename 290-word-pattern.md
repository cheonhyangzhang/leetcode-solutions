# 290 Word Pattern

### Problem:

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

Examples:
pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.
Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

### Solutions:

```java
public class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] strs = str.trim().split(" ");
        if (strs.length != pattern.length()) {
            return false;
        }
        HashMap<Character, String> bijection = new HashMap<Character, String>();
        for (int i = 0; i < pattern.length(); i ++) {
            char c = pattern.charAt(i);
            if (bijection.containsKey(c) && !bijection.get(c).equals(strs[i])) {
                return false;
            }
            if (!bijection.containsKey(c) && bijection.containsValue(strs[i])) {
                return false;
            }
            bijection.put(c, strs[i]);
        }
        return true;
    }
}
```