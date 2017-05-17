# 244 Shortest Word Distance II – Medium

### Problem:
This is a follow up of Shortest Word Distance. The only difference is now you are given the list of words and your method will be called repeatedly many times with different parameters. How would you optimize it?

Design a class which receives a list of words in the constructor, and implements a method that takes two words word1 and word2 and return the shortest distance between these two words in the list.

For example,
Assume that words = [“practice”, “makes”, “perfect”, “coding”, “makes”].

Given word1 = “coding”, word2 = “practice”, return 3.
Given word1 = “makes”, word2 = “coding”, return 1.

Note:
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

### Thoughts:
If the function is going to be called multiple times, then we need to store information that can be calculated already.
In this case, we use a HashMap to keep track of all the appearing index for a certain element.
However the first solution is having O(n^2) running time if n is the length for both two given Strings. It’s easy to think of. Say if we have [1, 3, 7] and [2, 6, 10], when you try with 1 and 2, there is no need to try 1 and 6 anymore, because the distance will for sure be bigger than current comparison.

The second solution is the improved solution.

### Solutions:

```java
public class WordDistance {
    HashMap<String, List<Integer>> indexes = new HashMap<String, List<Integer>>();
    public WordDistance(String[] words) {
        for (int i = 0; i < words.length; i ++) {
            if (!indexes.containsKey(words[i])) {
                indexes.put(words[i], new ArrayList<Integer>());
            }
            indexes.get(words[i]).add(i);
        }
    }
 
    public int shortest(String word1, String word2) {
        List<Integer> indexes1 = indexes.get(word1);
        List<Integer> indexes2 = indexes.get(word2);
        int min = Integer.MAX_VALUE;
        int i = 0, j = 0;
        while (i < indexes1.size() && j < indexes2.size()) {
            int i1 = indexes1.get(i);
            int i2 = indexes2.get(j);
            min = Math.min(min, Math.abs(i1 - i2));
            if (i1 < i2) {
                i ++;
            }
            else {
                j ++;
            }
        }
        return min;
    }
}
 
// Your WordDistance object will be instantiated and called as such:
// WordDistance wordDistance = new WordDistance(words);
// wordDistance.shortest("word1", "word2");
// wordDistance.shortest("anotherWord1", "anotherWord2");
```