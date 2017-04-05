# 411 Minimum Unique Word Abbreviation

### Problem:

A string such as "word" contains the following abbreviations:
```
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
```
Given a target string and a set of strings in a dictionary, find an abbreviation of this target string with the smallest possible length such that it does not conflict with abbreviations of the strings in the dictionary.

Each number or letter in the abbreviation is considered length = 1. For example, the abbreviation "a32bc" has length = 4.

Note:
In the case of multiple answers as shown in the second example below, you may return any one of them.
Assume length of target string = m, and dictionary size = n. You may assume that m ≤ 21, n ≤ 1000, and log2(n) + m ≤ 20.
Examples:
```
"apple", ["blade"] -> "a4" (because "5" or "4e" conflicts with "blade")

"apple", ["plain", "amber", "blade"] -> "1p3" (other valid answers include "ap3", "a3e", "2p2", "3le", "3l1").
```

### Solutions:

```java
public class Solution {
    public String minAbbreviation(String target, String[] dictionary) {
        if (dictionary.length == 0) {
            return target.length() + "";
        }
        PriorityQueue<String> q = new PriorityQueue<String>(new Comparator<String>(){
           public int compare(String s1, String s2) {
               return getLen(s1) - getLen(s2);
           } 
        });
        dfs(q, "", 0, target);
        while (!q.isEmpty()) {
            String s = q.poll();
            boolean found = false;
            for (int i = 0; i < dictionary.length; i ++) {
                if (isValid(s, dictionary[i])) {
                    found = true;
                    break;
                }
            }
            if (found == false) {
                return s;
            }
        }
        return "";
    }
    private int getLen(String s) {
        int count = 0;
        boolean num = false;
        for (int i = 0; i < s.length(); i ++) {
           char c = s.charAt(i);
           if (c >= '0' && c <= '9') {
               if (num == false) {
                   count ++;
                   num = true;
               }
           }
           else {
               num = false;
               count ++;
           }
        }
        return count;
    }
    private boolean isValid(String abbr, String s) {
        int count = 0;
        int i = 0, j = 0;
        for (; i < abbr.length() && j < s.length(); i ++) {
            char c = abbr.charAt(i);
            if (c >= '0' && c <= '9') {
                count = count * 10 + (c - '0');
            }
            else {
                j = j + count;
                count = 0;
                if (j >= s.length() || c != s.charAt(j)) {
                    return false;
                }
                j ++;
            }
        }
        return i == abbr.length() && j + count == s.length();
    }
    private void dfs(PriorityQueue<String> q, String prefix, int start, String w) {
        q.add(prefix + w.substring(start));
        if (start == w.length()) {
            return;
        }
        int i = 0;
        if (start > 0) {
            i = start + 1;
        }
        while (i < w.length()) {
            String next = prefix + w.substring(start, i);
            for (int j = 1; j + i <= w.length(); j ++) {
                dfs(q, next + j, i + j, w);
            } 
            i ++;
        }
    }
}
```