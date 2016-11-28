# 127 Word Ladder – Medium


### Problem:



Given two words (beginWord and endWord), and a dictionary’s word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

Only one letter can be changed at a time
Each intermediate word must exist in the word list
For example,

Given:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.

Note:

Return 0 if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.

### Thoughts:



This is a little complicated problem. Solution may vary based on different requirements.

Solution below is using a modified BFS version. It is also modifying the wordDict.

If constraint has cannot modify wordDic, this approach might not work sell. But could use an extra hashSet to achieve the same goal.


### Solutions:

```java
public class Solution {
    public int ladderLength(String beginWord, String endWord, Set<String> wordDict) {
        if (beginWord == null || endWord == null || beginWord.length() != endWord.length()) {
            return 0;
        }
        HashSet<String> visited = new HashSet<String>();
        Queue<String> q = new LinkedList<String>();
        q.add(beginWord);
        visited.add(beginWord);
        int count = 0;
        while (q.size() > 0) {
            int n = q.size();
            count ++;
            for (int i = 0; i < n; i ++) {
                String word = q.remove();
                if (word.equals(endWord)) {
                    return count;
                }
                StringBuilder nwsb = new StringBuilder(word);
                for (int j = 0; j < word.length(); j ++) {
                    char origin = word.charAt(j);
                    for (int m = 0; m < 26; m ++) {
                        if ('a' + m == origin) {
                            continue;
                        }
                        nwsb.setCharAt(j, (char)('a' + m));
                        if (wordDict.contains(nwsb.toString()) && !visited.contains(nwsb.toString())){
                            visited.add(nwsb.toString());
                            q.add(nwsb.toString());
                        }
                    }
                    nwsb.setCharAt(j, origin);
                }
            }
        }
        return 0;
    }
}
```