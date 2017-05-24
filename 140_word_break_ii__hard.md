# 140 Word Break II – Hard


### Problem:


Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

For example, given
s = “catsanddog”,
dict = [“cat”, “cats”, “and”, “sand”, “dog”].

A solution is [“cats and dog”, “cat sand dog”].

### Thoughts:


A easily modified version from Word Break I shown below is having Time Limit Exceeded issue when you submit.
Probably this is because string manipulation is taking more time comparing just only keep a record of index.


### Solutions:

easier to understand version

```java
public class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        List<String> result = new LinkedList<String>();
        if (s == null || s.length() == 0 || wordDict == null) {
            return result;
        }
        HashMap<Integer, List<Integer>> pointers = new HashMap<Integer, List<Integer>>();
        List<Integer> tmp = new LinkedList<Integer>();
        tmp.add(-1);
        pointers.put(-1, tmp);
        for (int j = 0; j < s.length(); j ++) {
            pointers.put(j, new LinkedList<Integer>());
            for (int i = 0; i <= j; i ++) {
                if (pointers.get(i - 1).size() > 0 && wordDict.contains(s.substring(i, j + 1))) {
                    pointers.get(j).add(i);
                }
            }
        }
        generate(s, result, s.length() - 1, pointers, "");
        return result;
    }
    private void generate(String s, List<String> result, int index, HashMap<Integer, List<Integer>> pointers, String suffix) {
        List<Integer> nexts = pointers.get(index);
        if (pointers.size() == 0) {
            return;
        }
        if (index == -1) {
            result.add(suffix.substring(0, suffix.length() - 1));
            return;
        }
        for (Integer next:nexts) {
            generate(s, result, next - 1, pointers, s.substring(next, index + 1) + " " + suffix);
        }
    }
}
```

First verision:

```java
public class Solution {
    private void search(int index, String s, List<Integer> path,
                   boolean[][] isWord, boolean[] possible,
                   List<String> result) {
        if (!possible[index]) {
            return;
        }
         
        if (index == s.length()) {
            StringBuilder sb = new StringBuilder();
            int lastIndex = 0;
            for (int i = 0; i < path.size(); i++) {
                sb.append(s.substring(lastIndex, path.get(i)));
                if (i != path.size() - 1) sb.append(" ");
                lastIndex = path.get(i);
            }
            result.add(sb.toString());
            return;
        }
         
        for (int i = index; i < s.length(); i++) {
            if (!isWord[index][i]) {
                continue;
            }
            path.add(i + 1);
            search(i + 1, s, path, isWord, possible, result);
            path.remove(path.size() - 1);
        }
    }
     
    public List<String> wordBreak(String s, Set<String> wordDict) {
        ArrayList<String> result = new ArrayList<String>();
        if (s.length() == 0) {
            return result;
        }
         
        boolean[][] isWord = new boolean[s.length()][s.length()];
        for (int i = 0; i < s.length(); i++) {
            for (int j = i; j < s.length(); j++) {
                String word = s.substring(i, j + 1);
                isWord[i][j] = wordDict.contains(word);
            }
        }
         
        boolean[] possible = new boolean[s.length() + 1];
        possible[s.length()] = true;
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i; j < s.length(); j++) {
                if (isWord[i][j] && possible[j + 1]) {
                    possible[i] = true;
                    break;
                }
            }
        }
         
        List<Integer> path = new ArrayList<Integer>();
        search(0, s, path, isWord, possible, result);
        return result;
    }
}
```