# 161 One Edit Distance – Medium
### Problem:
Given two strings S and T, determine if they are both one edit distance apart.
### Thoughts:
First of all, one edit distance here means you can change one string to another string by just one operation: add a character, remove a character or replace a character.

If two strings are one edit distance apart, then it must fall into one of these three cases, they have the same length which results in if can modify one character, their length is 1 in difference, which results in if can add one or remove one character.
Actually, for the second case, adding or removing character is the same because you add one character to one string equals remove one character from the other string.

The first solution below is the first solution I come into mind. For the first case, I check if other parts (except one character) is the same. Say for “abbc” and “acbc”, when iterating over the second character, check if first part of both strings, “a” and “a” are the same and check if second part of the string is the same “bc” and “bc”.
For the second case, it’s similar but when checking with the strings, for longer one, exclude one string and for shorter one don’t. E.g. “agbdc” and “agdc”, when iterating over the third character of the longer string, character is “b” and first part is “ag” and “ag” and second part is “dc” and “dc”.
Notice that when two strings are the same, it should return false, because it requires 0 edit to become the same string.

However, the solution is more time consuming, because it requires a lot of substring operation.
So, the better way is to use the second solution which only uses substring function for one time for each case.

### Solutions:
```java
public class Solution {
    public boolean isOneEditDistance(String s, String t) {
        //replace one character  by adding one character by removing one character
        if (s.length() != t.length() && s.length() + 1 != t.length() &&s.length() != t.length() + 1) {
            return false;
        }
        if (s.equals(t)) {
            return false;
        }
        if (s.length() == t.length()) {
            for (int i = 0; i < s.length(); i ++) {
                if (s.charAt(i) != t.charAt(i)) {
                    return s.substring(i + 1).equals(t.substring(i + 1));
                }
            }
            return false;
        }
        else {
            String longer = s;
            String shorter = t;
            if (s.length() < t.length()) {
                longer = t;
                shorter = s;
            }
            for (int i = 0; i < shorter.length(); i ++) {
                if (shorter.charAt(i) != longer.charAt(i)) {
                    return shorter.substring(i).equals(longer.substring(i + 1));
                }
            }
            return true;
        }
    }
}
```