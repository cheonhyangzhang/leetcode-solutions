# 340. Longest Substring with At Most K Distinct Characters

### Problem:
Given a string, find the length of the longest substring T that contains at most k distinct characters.

For example, Given s = “eceba” and k = 2,

T is "ece" which its length is 3.

### Solutions:

```java
public class Solution {
    public int lengthOfLongestSubstringKDistinct(String s, int k) {
        HashMap<Character, Integer> count = new HashMap<Character, Integer>();
        int max = 0;
        int start = 0;
        if (k == 0) {
            return 0;
        }
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (count.size() < k) {
                if (!count.containsKey(c)) {
                    count.put(c, 1);
                }        
                else {
                    count.put(c, count.get(c) + 1);
                }
                max = Math.max(max, i - start + 1);
                continue;
            }
            if (count.containsKey(c)) {
                count.put(c, count.get(c) + 1);
            }
            else {
                while (count.size() == k) {
                    char tmp = s.charAt(start);
                    if (count.get(tmp) == 1) {
                        count.remove(tmp);
                    }
                    else {
                        count.put(tmp, count.get(tmp) - 1);
                    }
                    start ++;
                }
                count.put(c, 1);
            }
            max = Math.max(max, i - start + 1);
        }
        return max;
    }
}
```