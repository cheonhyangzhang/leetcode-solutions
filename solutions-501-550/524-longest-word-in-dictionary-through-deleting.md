# 524 Longest Word in Dictionary through Deleting

### Problem:

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

Example 1:
```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"
```

Example 2:
```
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"
```

Note:
1. All the strings in the input will only contain lower-case letters.
2. The size of the dictionary won't exceed 1,000.
3. The length of all the strings in the input won't exceed 1,000.

### Solutions:

```java
public class Solution {
    public String findLongestWord(String s, List<String> d) {
        Collections.sort(d, new Comparator<String>() {
           public int compare(String s1, String s2) {
               if (s1.length() != s2.length()) {
                   return s2.length() - s1.length();
               }
               return s1.compareTo(s2);
           } 
        });
        for (String str:d) {
            if (str.length() > s.length()) {
                continue;
            }
            if (isSub(str, s)) {
                return str;
            }
        }
        return "";
    }
    private boolean isSub(String s, String l) {
        int j = 0;
        for (int i = 0; i < l.length(); i ++) {
            char c = l.charAt(i);
            if (j == s.length()) {
                break;
            }
            if (s.charAt(j) == c) {
                j ++;
            }
        }
        return j == s.length();
    }
}
```