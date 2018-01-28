# 245 Shortest Word Distance III – Medium

### Problem:
This is a follow up of Shortest Word Distance. The only difference is now word1 could be the same as word2.

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

word1 and word2 may be the same and they represent two individual words in the list.

For example,
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

Given word1 = “makes”, word2 = “coding”, return 1.
Given word1 = "makes", word2 = "makes", return 3.

Note:
You may assume word1 and word2 are both in the list.


### Solutions:

```java
class Solution {
    public int shortestWordDistance(String[] words, String word1, String word2) {
        int idx = -1, res = Integer.MAX_VALUE;
        for (int i = 0; i < words.length; ++i) {
            if (words[i].equals(word1) || words[i].equals(word2)) {
                if (idx != -1 && (word1.equals(word2) || !words[i].equals(words[idx]))) {
                    res = Math.min(res, i - idx);
                }
                idx = i;
            }
        }
        return res;
    }
}
```
