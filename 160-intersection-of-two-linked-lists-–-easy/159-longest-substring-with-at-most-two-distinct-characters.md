# 159 Longest Substring with At Most Two Distinct Characters

### Problem:

Given a string, find the length of the longest substring T that contains at most 2 distinct characters.

For example, Given s = “eceba”,

T is "ece" which its length is 3.

### Solutions:


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
        
            max = Math.max(max, i - start + 1);
          
        }
        return max;
    }
}
```