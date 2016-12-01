# 139 Word Break – Medium


### Problem:



Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

For example, given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".


### Thoughts:



We could use a dynamic programing approach for this problem.

A[i] stands for for the substring [0, i], if it is a valid word break string.

A[i] = A[j] && dict.contains(substring(j+1, i))


### Solutions:


```java
public class Solution {
    public boolean wordBreak(String s, Set<String> wordDict){
        if (s == null || s.length() == 0) {
            return false;
        }
        boolean[] canBreak = new boolean[s.length()];
        for (int i = 0; i < s.length(); i ++) {
            if (wordDict.contains(s.substring(0, i + 1))) {
                canBreak[i] = true;
                continue;
            }
            for (int j = 0; j < i; j ++) {
                if (canBreak[j] && wordDict.contains(s.substring(j + 1, i + 1))){
                    canBreak[i] = true;
                    break;
                }
            }
        }
        return canBreak[canBreak.length - 1];
    }
}
```