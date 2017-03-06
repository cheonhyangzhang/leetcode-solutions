# 269 Alien Dictionary

### Problem:

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

Example 1:
Given the following words in dictionary,
```
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]
```
The correct order is: "wertf".

Example 2:
Given the following words in dictionary,
```
[
  "z",
  "x"
]
```
The correct order is: "zx".

Example 3:
Given the following words in dictionary,
```
[
  "z",
  "x",
  "z"
]
```

The order is invalid, so return "".

Note:
1. You may assume all letters are in lowercase.
2. You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
3. If the order is invalid, return an empty string.
4. There may be multiple valid order of letters, return any one of them is fine.

### Solutions:

```java
public class Solution {
    public String alienOrder(String[] words) {
        HashSet<Character> cand = new HashSet<Character>();
        int n = 0;
        HashMap<Character, HashSet<Character>> less = new HashMap<Character, HashSet<Character>>();
        HashMap<Character, HashSet<Character>> greater = new HashMap<Character, HashSet<Character>>();
        for (int i = 0; i < words.length; i ++) {
            String word = words[i];
            for (int j = 0; j < word.length(); j ++) {
                cand.add(word.charAt(j));
            }
            if (i > 0) {
                String s1 = words[i - 1];
                String s2 = words[i];
                int i1 = 0;
                int i2 = 0;
                while (i1 < s1.length() && i2 < s2.length()) {
                    char c1 = s1.charAt(i1);
                    char c2 = s2.charAt(i2);
                    if (c1 != c2) {
                        update(c1, c2, less, greater);
                        break;
                    }
                    i1 ++;
                    i2 ++;
                }
            }
        }
        String result = "";
        n = cand.size();
        while (true) {
            Character c = min(cand, less, greater);
            if (c == null) {
                break;
            }
            result += c;
            cand.remove(c);
        }
        if (result.length() != n) {
            return "";
        }
        return result;
    }
    private Character min(HashSet<Character> cand, HashMap<Character, HashSet<Character>> less, HashMap<Character, HashSet<Character>> greater) {
        for (Character c:cand) {
            if (!greater.containsKey(c)) {
                if (less.containsKey(c)) {
                    for (Character cc:less.get(c)) {
                        greater.get(cc).remove(c);
                        if (greater.get(cc).isEmpty()) {
                            greater.remove(cc);
                        }
                    }
                    
                    less.remove(c);
                }
                return c;
            }
        }
        return null;
    }
    private void update(char c1, char c2, HashMap<Character, HashSet<Character>> less, HashMap<Character, HashSet<Character>> greater) {
        if (!less.containsKey(c1)) {
            less.put(c1, new HashSet<Character>());
        }            
        less.get(c1).add(c2);
        if (!greater.containsKey(c2)) {
            greater.put(c2, new HashSet<Character>());
        }
        greater.get(c2).add(c1);
    }
}
```