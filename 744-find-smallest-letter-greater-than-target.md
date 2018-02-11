# 744 Find Smallest Letter Greater Than Target

### Problem
Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'.

Examples:
```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```
Note:
1. letters has a length in range [2, 10000].
2. letters consists of lowercase letters, and contains at least 2 unique letters.
3. target is a lowercase letter.

### Solutions
```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        Character minInGreater = null;
        Character min = null;
        for (int i = 0; i < letters.length; i ++) {
            char c = letters[i];
            if (min == null || c < min) {
                min = c;
            }
            if (c > target && (minInGreater == null || c < minInGreater)) {
                minInGreater = c;
            }
        }
        return minInGreater == null? min:minInGreater;
    }
}
```

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int left = 0, right = letters.length - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (letters[mid] <= target) {
                left ++;
            }
            else {
                right --;
            }
        }
        if (left == letters.length) {
            return letters[0];
        }
        return letters[left];
    }
}
```