# 527. Word Abbreviation

### Problem:

Given an array of n distinct non-empty strings, you need to generate minimal possible abbreviations for every word following rules below.

1. Begin with the first character and then the number of characters abbreviated, which followed by the last character.
2. If there are any conflict, that is more than one words share the same abbreviation, a longer prefix is used instead of only the first character until making the map from word to abbreviation become unique. In other words, a final abbreviation cannot map to more than one original words.
3. If the abbreviation doesn't make the word shorter, then keep it as original.

Example:
```
Input: ["like", "god", "internal", "me", "internet", "interval", "intension", "face", "intrusion"]
Output: ["l2e","god","internal","me","i6t","interval","inte4n","f2e","intr4n"]
```
Note:
1. Both n and the length of each word will not exceed 400.
2. The length of each word is greater than 1.
3. The words consist of lowercase English letters only.
4. The return answers should be in the same order as the original array.

### Solutions:

```java
public class Solution {
    public List<String> wordsAbbreviation(List<String> dict) {
        List<String> res = new ArrayList<String>();
        HashMap<String, List<Integer>> map = new HashMap<String, List<Integer>>();
        int i = 0;
        for (String s:dict) {
            if (s.length() <= 3) {
                res.add(s);
                i ++;
                continue;
            }            
            String tmp = s.charAt(0) + ((s.length() - 2) + "") + s.charAt(s.length() - 1);
            if (!map.containsKey(tmp)) {
                map.put(tmp, new LinkedList<Integer>());
            }
            map.get(tmp).add(i);
            res.add(tmp);
            i ++;
        }
        while (map.size() > 0) {
            HashMap<String, List<Integer>> newMap = new HashMap<String, List<Integer>>();
            List<String> toRemove = new LinkedList<String>();
            for (String key:map.keySet()) {
                List<Integer> indexes = map.get(key);
                if (indexes.size() == 1) {
                    toRemove.add(key);
                }
            }
            for (String key:toRemove) {
                map.remove(key);
            }
            for (String key:map.keySet()) {
                List<Integer> indexes = map.get(key);
                String prefix = findCommonPrefix(indexes, dict);
                for (Integer j:indexes) {
                    String original = dict.get(j);
                    if (original.length() - prefix.length() <=3) {
                        res.set(j, original);
                    }
                    else {
                        String replace = prefix + original.charAt(prefix.length()) + (original.length() - prefix.length() - 2) + original.charAt(original.length() - 1);
                        res.set(j, replace);
                        if (!newMap.containsKey(replace)) {
                            newMap.put(replace, new LinkedList<Integer>());
                        }
                        newMap.get(replace).add(j);
                    }
                }
            }
            map = newMap;
        }
        return res;
    }
    private String findCommonPrefix(List<Integer> indexes, List<String> dict) {
        String prefix = dict.get(indexes.get(0));
        for (int i = 1; i < indexes.size(); i ++) {
            int index = indexes.get(i);
            String compare = dict.get(index);
            for (int j = prefix.length(); j >= 0; j --) {
                if (prefix.substring(0, j).equals(compare.substring(0, j))) {
                    prefix = prefix.substring(0, j);
                    break;
                }
            }
        }
        return prefix;
    }
}
```