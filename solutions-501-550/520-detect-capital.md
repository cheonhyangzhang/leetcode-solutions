# 520 Detect Capital

### Problem:

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

1. All letters in this word are capitals, like "USA".
2. All letters in this word are not capitals, like "leetcode".
3. Only the first letter in this word is capital if it has more than one letter, like "Google".

Otherwise, we define that this word doesn't use capitals in a right way.

Example 1:
```
Input: "USA"
Output: True
```

Example 2:
```
Input: "FlaG"
Output: False
```

Note: The input will be a non-empty word consisting of uppercase and lowercase latin letters.

### Solutions:

```java
public class Solution {
    public boolean detectCapitalUse(String word) {
        int count = 0;
        for (int i = 0; i < word.length(); i ++) {
            char c = word.charAt(i);
            if (c >= 'A' && c <= 'Z') {
                count ++;
            }
            if (!(count == 0 || (count == 1 && word.charAt(0) >= 'A' && word.charAt(0) <= 'Z') || count == i + 1)) {
               return false; 
            }
        }
        return true;
    }
}
```

```java
public class Solution {
    public boolean detectCapitalUse(String word) {
        return word.matches("[A-Z]*|[A-Z][a-z]+|[a-z]+");
    }
}
```