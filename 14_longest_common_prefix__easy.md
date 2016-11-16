# 14 Longest Common Prefix – Easy


### Problem:



Write a function to find the longest common prefix string amongst an array of strings.


### Thoughts:


Get the first string in the array of strings, the longest common prefix is at best this first string.

So iterate over all strings, and find out if there is a common prefix for the current string and current prefix.

If the first string length is m, and there are n strings. This method will be O(mn) running time.

There could be a optimized solution. Instead of always start with the first string in the array, init the prefix to be the shortest string in the array. If k is the shortest string’s length, then running time would be O(kn). This is helpful when k is significantly smaller than m, where m is the first string length.


### Solutions:

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        String prefix = strs[0];
        for (int i = 1; i < strs.length; i ++ ) {
            for (int j = 0; j < prefix.length(); j ++){
                if (j == strs[i].length() || prefix.charAt(j) != strs[i].charAt(j)) {
                    prefix = prefix.substring(0, j);
                    break;
                }
            }
        }
        return prefix;
    }
}
```