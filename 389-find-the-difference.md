# 389 Find the Difference

### Problem:

Given two strings s and t which consist of only lowercase letters.

String t is generated by random shuffling string s and then add one more letter at a random position.

Find the letter that was added in t.

Example:

```
Input:
s = "abcd"
t = "abcde"

Output:
e

Explanation:
'e' is the letter that was added.
```

### Solutions:

```java
public class Solution {
    public char findTheDifference(String s, String t) {
        HashMap<Character, Integer> chars = new HashMap<Character, Integer>();
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (!chars.containsKey(c)) {
                chars.put(c, 0);
            }
            chars.put(c, chars.get(c) + 1);
        }
        for (int i = 0; i < t.length(); i ++) {
            char c = t.charAt(i);
            if (!chars.containsKey(c)) {
                return c;
            }
            if (chars.get(c) == 0) {
                return c;
            }
            chars.put(c, chars.get(c) - 1);
        }
        return ' ';
    }
}
```

```java
public class Solution {
    public char findTheDifference(String s, String t) {
        char[] sc = s.toCharArray();
        char[] tc = t.toCharArray();
        Arrays.sort(sc);
        Arrays.sort(tc);
        for (int i = 0; i < sc.length; i ++) {
            if (sc[i] != tc[i]) {
                return tc[i];
            }
        }
        return tc[tc.length - 1];
    }
}
```

```java
public class Solution {
    public char findTheDifference(String s, String t) {
        int res = 0;
        for (int i = 0; i < s.length(); i ++) {
            res = res^s.charAt(i);
            res = res^t.charAt(i);
        }
        res = res^t.charAt(t.length() - 1);
        return (char)res;
    }
}
```

```java
public class Solution {
    public char findTheDifference(String s, String t) {
        int res = 0;
        for (int i = 0; i < s.length(); i ++) {
            res = res - s.charAt(i);
            res = res + t.charAt(i);
        }
        res = res + t.charAt(t.length() - 1);
        return (char)res;
    }
}
```
