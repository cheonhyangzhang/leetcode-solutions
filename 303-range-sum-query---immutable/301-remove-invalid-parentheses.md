# 301 Remove Invalid Parentheses

### Problem
Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

Note: The input string may contain letters other than the parentheses ( and ).

Examples:
```
"()())()" -> ["()()()", "(())()"]
"(a)())()" -> ["(a)()()", "(a())()"]
")(" -> [""]
```

### Solutions
BFS
```java
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        List<String> res = new LinkedList<String>();    
        HashSet<String> visited = new HashSet<String>();
        Queue<String> q = new LinkedList<String>();
        q.add(s);
        Queue<Integer> levels = new LinkedList<Integer>();
        visited.add(s);
        levels.add(0);
        int found = -1;
        while (!q.isEmpty()) {
            String cand = q.poll();
            int level = levels.poll();
            if (found != -1 && level > found) {
                break;
            }
            if (isValid(cand)) {
                found = level;
                res.add(cand);
                continue;
            }
            for (int i = 0; i < cand.length(); i ++) {
                String newcand = cand.substring(0, i) + cand.substring(i + 1);
                if (!visited.contains(newcand)) {
                    q.add(newcand);
                    visited.add(newcand);
                    levels.add(level + 1);
                }
            }
            
        }
        return res;
    }
    private boolean isValid(String s) {
        int count = 0;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c == '(') {
                count ++;
            }
            else if (c == ')'){
                if (count <= 0) {
                    return false;
                }
                count --;
            }
        }
        return count == 0;
    }
}
```

DFS
```java
public class Solution {
    ArrayList<String> res = new ArrayList<String>();
    int max = 0; 
    public List<String> removeInvalidParentheses(String s) {
        if(s == null) {
            return res;
        }
        dfs(s, "", 0);
        if(res.size() == 0) {
            res.add("");
        }
        return res;
    }
    public void dfs(String s, String cand, int left) {
        if(s.length() == 0){
            if(left == 0 && cand.length() != 0) {
                if (cand.length() > max) {
                    max = cand.length();
                    res.clear();
                }
                if(cand.length() == max && !res.contains(cand)) {
                    res.add(cand);
                }
            }
            return;
        }
        
        if (s.charAt(0) == '(') {
            dfs(s.substring(1), cand + "(", left + 1);
            dfs(s.substring(1), cand, left);
        }
        else if (s.charAt(0) == ')') {
            if (left > 0) {
                dfs(s.substring(1), cand + ")", left - 1);
            }
            dfs(s.substring(1), cand, left);
        }else{
            dfs(s.substring(1), cand + s.charAt(0), left);
        }
    }
}
```