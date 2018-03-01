# 243 Shortest Word Distance – Easy

### Problem:
Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

For example,
Assume that words = [“practice”, “makes”, “perfect”, “coding”, “makes”].

Given word1 = “coding”, word2 = “practice”, return 3.
Given word1 = “makes”, word2 = “coding”, return 1.

Note:
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

### Thoughts:
The solution is very easy. Keep two index to remember the last appear index for each word. Also have a variable to keep the current shortest distance.

### Solutions:

```java
class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
        Integer i1 = null;
        Integer i2 = null;
        int max = Integer.MAX_VALUE;
        for (int i = 0; i < words.length; i ++) {
            if (words[i].equals(word1)) {
                i1 = i;
            }
            if (words[i].equals(word2)) {
                i2 = i;
            }
            if (i1 != null && i2 != null) {
                max = Math.min(max, Math.abs(i1 - i2));
            }
        }
        return max;
    }
}
```