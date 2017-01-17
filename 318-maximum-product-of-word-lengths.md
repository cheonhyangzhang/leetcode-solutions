# 318 Maximum Product of Word Lengths

### Problem:

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

Example 1:
Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]
Return 16
The two words can be "abcw", "xtfn".

Example 2:
Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]
Return 4
The two words can be "ab", "cd".

Example 3:
Given ["a", "aa", "aaa", "aaaa"]
Return 0
No such pair of words.

### Solutions:

```java
public class Solution {
    public int maxProduct(String[] words) {
        int[] codes = new int[words.length];
        for (int i = 0; i < words.length;i ++) {
            codes[i] = encode(words[i]);
        }
        int max = 0;
        for (int i = 0; i < words.length;i ++) {
            for (int j = i + 1; j < words.length; j ++) {
                if ((codes[i]&codes[j]) == 0) {
                    max = Math.max(max, words[i].length() * words[j].length());
                }
            }
        }
        return max;
    }
    private int encode(String s) {
        int result = 0;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            int mask = 1 << (c - 'a');
            result = result | mask;
        }
        return result;
    }
}
```