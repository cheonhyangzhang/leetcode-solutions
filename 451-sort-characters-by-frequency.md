# 451 Sort Characters By Frequency

### Problem:

Given a string, sort it in decreasing order based on the frequency of characters.

Example 1:
```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

Example 2:

```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```

Example 3:

```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

### Solutions:

```java
public class Solution {
    public String frequencySort(String s) {
        HashMap<Character, Integer> appr = new HashMap<Character, Integer>();
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (!appr.containsKey(c)) {
                appr.put(c, 0);
            }
            appr.put(c, appr.get(c) + 1);
            max = Math.max(max, appr.get(c));
        }
        HashMap<Integer, Queue<Character>> index = new HashMap<Integer, Queue<Character>>();
        for (Character c:appr.keySet()) {
            int count = appr.get(c);
            if (!index.containsKey(count)) {
                index.put(count, new LinkedList<Character>());
            }
            index.get(count).add(c);
        }
        StringBuilder sb = new StringBuilder();
        for (int i = max; i > 0; i --) {
            if (index.containsKey(i)) {
                while (!index.get(i).isEmpty()) {
                    char c = index.get(i).poll();
                    for (int j = 0; j < i; j ++) {
                        sb.append(c);
                    }    
                }
            }
            
        }
        return sb.toString();
    }
}
```