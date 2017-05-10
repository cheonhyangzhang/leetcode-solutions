# 186 Reverse Words in a String II – Medium


### Problem:
Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

For example,
Given s = “the sky is blue”,
return “blue is sky the”.

Could you do it in-place without allocating extra space?

### Thoughts:
The original problem Reverse Words in a String is quite straightforward, however the solution there might not be used in this problem.

The trick part is that this problem requires do it in-place. In place doesn’t mean that you cannot use O(1) space. It means you cannot have another array.

The solution is a little tricky, the idea is to reverse the whole string first, so “the sky is blue” becomes “eulb si yks eht”.
This will make all the space in this string to be in the expected position.
Next we need to reverse each word, so that it becomes “blue is sky the”.

### Solutions:

```java
public class Solution {
    public void reverseWords(char[] s) {
        if (s.length == 0) {
            return;
        }
        reverse(s, 0, s.length - 1);
        int left = 0;
        for (int i = 0; i <= s.length; i ++) {
            if (i == s.length || s[i] == ' ') {
                reverse(s, left, i - 1);
                left = i + 1;
            }
        }
    }
    private void reverse(char[] s, int l, int r) {
        while (l < r) {
            char tmp = s[l];
            s[l] = s[r];
            s[r] = tmp;
            l ++;
            r --;
        }
    }
}
```