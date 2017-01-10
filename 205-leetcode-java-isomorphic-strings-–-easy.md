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
public class Solution {
    public boolean isIsomorphic(String s, String t) {
        if (s.length() != t.length())
            return false;
        HashMap<Character, Character> stot = new HashMap<Character, Character>();
        HashMap<Character, Character> ttos = new HashMap<Character, Character>();
        for (int i = 0; i < s.length(); i ++){ 
            if (stot.containsKey(s.charAt(i))){
                if (stot.get(s.charAt(i)) != t.charAt(i)){
                    return false;
                }
            }
            if (ttos.containsKey(t.charAt(i))){
                if (ttos.get(t.charAt(i)) != s.charAt(i)){
                    return false;
                }
            }
            stot.put(s.charAt(i), t.charAt(i));
            ttos.put(t.charAt(i), s.charAt(i));
        }
        return true;
    }
}
```
Updated: 12/31/2016
The solution above can be solved using only one HashMap, using .containsValue() function.