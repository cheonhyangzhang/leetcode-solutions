# 418 Sentence Screen Fitting

### Problem:

Given a rows x cols screen and a sentence represented by a list of non-empty words, find how many times the given sentence can be fitted on the screen.

Note:

A word cannot be split into two lines.
The order of words in the sentence must remain unchanged.
Two consecutive words in a line must be separated by a single space.
Total words in the sentence won't exceed 100.
Length of each word is greater than 0 and won't exceed 10.
1 ≤ rows, cols ≤ 20,000.
Example 1:
```
Input:
rows = 2, cols = 8, sentence = ["hello", "world"]

Output: 
1

Explanation:
hello---
world---

The character '-' signifies an empty space on the screen.
```

Example 2:
```
Input:
rows = 3, cols = 6, sentence = ["a", "bcd", "e"]

Output: 
2

Explanation:
a-bcd- 
e-a---
bcd-e-

The character '-' signifies an empty space on the screen.
```

Example 3:
```
Input:
rows = 4, cols = 5, sentence = ["I", "had", "apple", "pie"]

Output: 
1

Explanation:
I-had
apple
pie-I
had--

The character '-' signifies an empty space on the screen.
```

### Solutions:

```java
public class Solution {
    public int wordsTyping(String[] sentence, int rows, int cols) {
        int count = 0;
        int i = 0, j = 0;
        int k = 0;
        while (i < rows) {
            if (count != 0 && j == 0 && k == 0) {
                count = count * (rows / i);
                i = (rows / i) * i; 
            }
            if (k == sentence.length) {
                count ++;
                k = 0;
                continue;
            }
            if (sentence[k].length() + j > cols) {
                i ++;
                j = 0;
                continue;
            }
            else {
                j = sentence[k].length() + j + 1;
                k ++;
            }
        }
        return count * (rows / i);
    }
}
```