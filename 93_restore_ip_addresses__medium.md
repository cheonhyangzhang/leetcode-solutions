# 93 Restore IP Addresses – Medium


### Problem:



Given a string containing only digits, restore it by returning all possible valid IP address combinations.

For example:
Given "25525511135",

return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)


### Thoughts:



Modified DFS. Keep a variable to keep current potential solution – String.

Keep how many parts to go.

For each visit, there are three possibilities to go deep level. x, xx, xxx.

Only go deep when the possibility is valid.


### Solutions:

```java
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
public class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> result = new LinkedList<String>();
        dfs(s, result, "", 0, 12, 4);
        return result;
    }
    private void dfs(String s, List<String> result, String curr, int start, int max, int min) {
        if (s.length() - start > max || s.length() - start < min) {
            return;
        }
        if (max == 0 && start == s.length()) {
            result.add(curr.substring(1));
            return;
        }
        if (s.charAt(start) == '0') {
            dfs(s, result, curr + ".0", start + 1, max - 3, min - 1);
            return;
        }
        for (int i = 0; i < 3; i ++) {
            if (start + i + 1 <= s.length()) {
                int tmp = Integer.parseInt(s.substring(start, start + i + 1));
                if (tmp >=0 && tmp <= 255) {
                    dfs(s, result, curr + "." + tmp, start + i + 1, max - 3, min - 1);
                }
            }
        }
         
    }
}
```