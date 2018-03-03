# 205 LeetCode Java: Isomorphic Strings – Easy

### Problem:

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

For example,
Given "egg", "add", return true.

Given "foo", "bar", return false.

Given "paper", "title", return true.

Note:
You may assume both s and t have the same length.

### Thoughts:

Note that there might be some edge cases we need to carefully take care of.

According to the requirement, the mapping has to be two direction. The mapping has to be one to one. That’s why we need two map to store the mapping.

### Solution:

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        HashMap<Character, Character> stot = new HashMap<>();
        HashMap<Character, Character> ttos = new HashMap<>();
        if ((s == null && t != null) || (s != null && t == null)) {
            return false;
        }
        if (s.length() != t.length()) {
            return false;
        }
        for (int i = 0; i < s.length(); i ++) {
            char a = s.charAt(i);
            char b = t.charAt(i);
            if (stot.containsKey(a)) {
                if (!ttos.containsKey(b) || ttos.get(b) != a) {
                    return false;
                }
            }
            else {
                if (ttos.containsKey(b)) {
                    return false;
                }
                stot.put(a, b);
                ttos.put(b, a);
            }
        }
        return true;
    }
}
```
Updated: 12/31/2016
The solution above can be solved using only one HashMap, using .containsValue() function.