# 249 LeetCode Java: Group Shifted Strings

### Problem:

Given a string, we can “shift” each of its letter to its successive letter, for example: "abc" -> "bcd". We can keep “shifting” which forms the sequence:

"abc" -> "bcd" -> ... -> "xyz"
Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

For example, given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"],
A solution is:

[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
### Thoughts:

The idea is to find what’s in common for those strings that belongs to the same shifting sequence.
In order to shift one string, we increase each of the letter by 1, which means the difference between each letter keeps the same. Say for acef, the different is 2, 1, 1, when you shift, it becomes bdfg 2, 1, 1. So we just need to calculate this sequence.
The original idea is to store that in a string because it’s easy to compare string to be equal. I tried with this solution and it passed. But I think it’s better to avoid this because 121 can be interpreted into 12, 1 or 1, 21. So we still use string but each char we store the difference, because the different is at most 25.

### Solutions:

```java
public class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        HashMap<String, List<String>> data = new HashMap<String, List<String>>();
        for (int i = 0; i < strings.length; i ++) {
            String c = code(strings[i]);
            if (!data.containsKey(c)) {
                data.put(c, new LinkedList<String>());
            }
            data.get(c).add(strings[i]);
        }
        List<List<String>> result = new LinkedList<List<String>>();
        for (String s:data.keySet()) {
            result.add(data.get(s));
        }
        return result;
    }
    private String code(String s) {
        String result = "";
        for (int i = 1; i < s.length(); i ++) {
            int tmp = (s.charAt(i) - s.charAt(i-1) + 26 ) % 26;
            result += (char)tmp;
        }
        return result;
    }
}
```