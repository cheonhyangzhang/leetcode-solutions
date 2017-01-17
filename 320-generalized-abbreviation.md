# 320 Generalized Abbreviation

### Problem:

Write a function to generate the generalized abbreviations of a word.

Example:
Given word = "word", return the following list (order does not matter):
["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]

### Solutions:

```java
public class Solution {
      public List<String> generateAbbreviations(String word) {
            List<String> result = new LinkedList<String>();
            result.add(word);
            for (int i = 1; i <= word.length(); i ++) {
                  for (int j = 0; j + i <= word.length(); j ++) {
                        List<String> following = generateAbbreviations(j + i + 1 <= word.length()?word.substring(j + i + 1):"");
                        for (String f:following) {
                              String s = word.substring(0, j) + i + (j + i < word.length()?word.charAt(j + i):"") + f;
                              result.add(s);
                        }
                  }
            }
            return result;
      }
}
```