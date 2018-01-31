# 291 Word Pattern II

### Problem
Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty substring in str.

Examples:
pattern = "abab", str = "redblueredblue" should return true.
pattern = "aaaa", str = "asdasdasdasd" should return true.
pattern = "aabb", str = "xyzabcxzyabc" should return false.
Notes:
You may assume both pattern and str contains only lowercase letters.

### Solutions
```java
class Solution {
    public boolean wordPatternMatch(String pattern, String str) {
        HashMap<Character, String> ctostr = new HashMap<Character, String>();
        HashMap<String, Character> strtoc = new HashMap<String, Character>();
        return process(pattern, 0, str, 0, ctostr, strtoc);
    }
    private boolean process(String pattern, int pi, String str, int si, HashMap<Character, String> ctostr, HashMap<String, Character> strtoc) {
        // System.out.println(pi + ", " + si);
        if (pi == pattern.length() && si == str.length()) {
            return true;
        }
        if (pi == pattern.length() || si == str.length()) {
            return false;
        }
        char c = pattern.charAt(pi);
        for (int i = si + 1; i <= str.length(); i ++) {
            String tostr = str.substring(si, i);
            if (ctostr.containsKey(c)) {
                if (!ctostr.get(c).equals(tostr)) {
                    continue;
                }
                else {
                    if (process(pattern, pi + 1, str, i, ctostr, strtoc)){
                        return true;
                    }   
                }
            }
            else {
                if (strtoc.containsKey(tostr)) {
                    continue;
                }
                else {
                    ctostr.put(c, tostr);
                    strtoc.put(tostr, c);
                    if (process(pattern, pi + 1, str, i, ctostr, strtoc)) {
                        return true;
                    }
                    ctostr.remove(c);
                    strtoc.remove(tostr);
                }
            }
        }
        return false;
    }
    
}
```