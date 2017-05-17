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
public class Solution {
    public int shortestWordDistance(String[] words, String word1, String word2) {
        int index1 = -1;
        int index2 = -1;
        int min = Integer.MAX_VALUE;
        boolean same = false;
        if (word1.equals(word2)) {
            same = true;
        }
        for (int i = 0; i < words.length; i ++) {
            if (words[i].equals(word1)) {
                if (index2 != -1) {
                    min = Math.min(i - index2, min);
                }
                index1 = i;
                if (same) {
                    index2 = i;
                }
                continue;
            }
            if (words[i].equals(word2)) {
                if (index1 != -1) {
                    min = Math.min(i - index1, min);
                }
                index2 = i;
                if (same) {
                    index1 = i;
                }
                continue;
            }
        }
        return min;
    }
}
```
