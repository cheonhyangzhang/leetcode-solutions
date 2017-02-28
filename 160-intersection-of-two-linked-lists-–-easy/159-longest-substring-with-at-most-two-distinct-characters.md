# 159 Longest Substring with At Most Two Distinct Characters

### Problem:

Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

For example, Given s = “eceba”,

T is "ece" which its length is 3.

### Solutions:

```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int max = 0;
        Character c1 = null;
        Character c2 = null;
        Character curr = null;
        int i1 = -1;
        int i2 = -1;
        int count = 0;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c1 == null) {
                c1 = c;
                curr = c;
                i1 = i;
                count ++;
                max = Math.max(max, count);
                continue;
            }
            if (c1 == c) {
                count ++;
                max = Math.max(max, count);
                if (curr != c) {
                    curr = c;
                    i1 = i;
                }
                continue;
            }
            if (c2 == null) {
                c2 = c;
                curr = c;
                i2 = i;
                count ++;
                max = Math.max(max, count);
                continue;
            }
            if (c2 == c) {
                count ++;
                max = Math.max(max, count);
                if (curr != c) {
                    curr = c;
                    i2 = i;
                }
                continue;
            }
            if (curr == c1) {
                count = i - i1 + 1;
                c2 = c;
                i2 = i;
                curr = c;
            }
            else {
                count = i - i2 + 1;
                c1 = c;
                i1 = i;
                curr = c;
            }
        }
        return max;
    }
}
```

```java
public class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        HashMap<Character, Integer> chars = new HashMap<Character, Integer>();
        int k = 2;
        int max = 0;
        int start = 0;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            int count = 1;
            if (chars.containsKey(c)) {
                count = chars.get(c) + 1;
            }
            chars.put(c, count);
            if (chars.size() > k) {
                while (chars.size() > k) {
                    char tmp = s.charAt(start);
                    if (chars.get(s.charAt(start)) == 1) {
                        chars.remove(tmp);
                    }
                    else {
                        chars.put(tmp, chars.get(tmp) - 1);
                    }
                    start ++;                    
                }
            }
            else {
                max = Math.max(max, i - start + 1);
            }
        }
        return max;
    }
}
```