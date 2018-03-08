# 76 Minimum Window Substring

### Problem
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".

Note:
If there is no such window in S that covers all characters in T, return the empty string "".

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

### Solutions
```java
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> miss = new HashMap<Character, Integer>();
        HashSet<Character> chars = new HashSet<Character>();
        HashMap<Character, Integer> count = new HashMap<Character, Integer>();
        for (int i = 0; i < t.length(); i ++) {
            char c = t.charAt(i);
            chars.add(c);
            if (!miss.containsKey(c)) {
                miss.put(c, 0);
            }
            if (!count.containsKey(c)) {
                count.put(c, 0);
            }
            miss.put(c, miss.get(c) + 1);
        }
        int left = -1, right = 0;
        int min = Integer.MAX_VALUE;
        String res = "";
        int target = t.length();
        int matched = 0;
        while (right <= s.length()) {
            if (matched == target) {
                String cand = s.substring(left, right);
                if (cand.length() < min) {
                    min = cand.length();
                    res = cand;
                }
                char toremove = s.charAt(left);
                count.put(toremove, count.get(toremove) - 1);
                if (count.get(toremove) < miss.get(toremove)) {
                    matched --;
                }
                left ++;
                while (left < right && !chars.contains(s.charAt(left))) {
                    left ++;
                }
                continue;
            }
            if (right == s.length()) {
                break;
            }
            char c = s.charAt(right);
            if (chars.contains(c)) {
                if (matched == 0) {
                    left = right;
                }
                count.put(c, count.get(c) + 1);
                if (count.get(c) <= miss.get(c)) {
                    matched ++;
                }
            }
            right ++;
        }
        return res;
    }
}
```

```java
class Solution {
    public String minWindow(String s, String t) {
        if (s == null || t == null || s.length() == 0 || t.length() == 0) {
            return "";
        }
        HashMap<Character, Integer> chars = new HashMap<>();
        for (int i = 0; i < t.length(); i ++) {
            char c = t.charAt(i);
            if (!chars.containsKey(c)) {
                chars.put(c, 0);
            }
            chars.put(c, chars.get(c) + 1);
        }
        HashMap<Character, Integer> appr = new HashMap<>();
        String cand = "";
        int start = 0;
        int miss = t.length();
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            sb.append(c);
            if (chars.containsKey(c)) {
                if (!appr.containsKey(c)) {
                    appr.put(c, 0);
                }
                appr.put(c, appr.get(c) + 1);
                if (appr.get(c) <= chars.get(c)) {
                    miss --;
                }
            }   
            while (sb.length() > 0 && !chars.containsKey(sb.charAt(0))) {
                sb.deleteCharAt(0);
            }
            while (miss == 0) {
                if (cand.equals("") || sb.length() < cand.length()) {
                    cand = sb.toString();
                }
                char remove = sb.charAt(0);
                sb.deleteCharAt(0);
                appr.put(remove, appr.get(remove) - 1);
                if (appr.get(remove) < chars.get(remove)) {
                    miss ++;
                }
                while (sb.length() > 0 && !chars.containsKey(sb.charAt(0))) {
                    sb.deleteCharAt(0);
                }
            }
        }
        return cand;
    }
}
```