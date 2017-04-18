# 522 Longest Uncommon Subsequence II

### Problem:

Given a list of strings, you need to find the longest uncommon subsequence among them. The longest uncommon subsequence is defined as the longest subsequence of one of these strings and this subsequence should not be any subsequence of the other strings.

A subsequence is a sequence that can be derived from one sequence by deleting some characters without changing the order of the remaining elements. Trivially, any string is a subsequence of itself and an empty string is a subsequence of any string.

The input will be a list of strings, and the output needs to be the length of the longest uncommon subsequence. If the longest uncommon subsequence doesn't exist, return -1.

Example 1:
```
Input: "aba", "cdc", "eae"
Output: 3
```

Note:

1. All the given strings' lengths will not exceed 10.
2. The length of the given list will be in the range of [2, 50].


### Solutions:

```java
public class Solution {
    public int findLUSlength(String[] strs) {
        int max = 0;
        Arrays.sort(strs, new Comparator<String>() {
           public int compare(String s1, String s2) {
                if (s2.length() != s1.length()) {
                    return s2.length() - s1.length();   
                }
                return s1.compareTo(s2);
           } 
        });
        Set<String> pres = new HashSet<String>();
        for (int i = 0; i < strs.length; i ++) {
            if (i == strs.length - 1 || !strs[i].equals(strs[i + 1])) {
                boolean valid = true;
                for (String pre:pres) {
                    if (isSub(strs[i], pre)) {
                        valid = false;
                        break;
                    }
                }
                if (valid == true) {
                    return strs[i].length();
                }
                else {
                    pres.add(strs[i]);
                }
            }
            else {
                String s = strs[i];
                pres.add(s);
                while (i < strs.length && strs[i].equals(s)) {
                    i ++;
                }
                i --;
            }
            
        }
        return -1;
    }
    private boolean isSub(String s, String l) {
        if (s.length() > l.length()) {
            return false;
        }
        if (s.length() == 1) {
            return l.indexOf(s) != -1;
        }
        char c = s.charAt(0);
        int cut = l.indexOf(c);
        if (cut == -1) {
            return false;
        }
        return isSub(s.substring(1), l.substring(cut + 1));
    }
}
```

