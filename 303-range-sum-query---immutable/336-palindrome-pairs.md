# 336. Palindrome Pairs

### Problem:

Given a list of unique words, find all pairs of distinct indices (i, j) in the given list, so that the concatenation of the two words, i.e. words[i] + words[j] is a palindrome.

Example 1:
Given words = ["bat", "tab", "cat"]
Return [[0, 1], [1, 0]]
The palindromes are ["battab", "tabbat"]
Example 2:
Given words = ["abcd", "dcba", "lls", "s", "sssll"]
Return [[0, 1], [1, 0], [3, 2], [2, 4]]
The palindromes are ["dcbaabcd", "abcddcba", "slls", "llssssll"]

### Solutions:

```java
public class Solution {
    public List<List<Integer>> palindromePairs(String[] words) {
        HashMap<String, Integer> index = new HashMap<String, Integer>();
        for (int i = 0; i < words.length; i ++) {
            index.put(words[i], i);
        }
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        for (int i = 0; i < words.length; i ++) {
            String reverse = new StringBuilder(words[i]).reverse().toString();
            int start = 0, end = reverse.length();
            if (index.containsKey(reverse) && index.get(reverse) != i) {
                List<Integer> tmp = new LinkedList<Integer>();
                tmp.add(index.get(reverse));
                tmp.add(i);
                res.add(tmp);
                start ++;
                end --;
            }
            
            for (int j = start; j <= end; j ++) {
                String left = reverse.substring(0, j);
                String right = reverse.substring(j);
                if (index.containsKey(left) && index.get(left) != i && isPa(right)) {
                    List<Integer> tmp = new LinkedList<Integer>();
                    tmp.add(index.get(left));
                    tmp.add(i);
                    res.add(tmp);
                }
                if (index.containsKey(right) && index.get(right) != i && isPa(left)) {
                    List<Integer> tmp = new LinkedList<Integer>();
                    tmp.add(i);
                    tmp.add(index.get(right));
                    res.add(tmp);
                }
            }
        }
        return res;
    }
    private boolean isPa(String s) {
        if (s.equals("")) {
            return true;
        }
        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left ++;
            right --;
        }
        return true;
    }
}
```