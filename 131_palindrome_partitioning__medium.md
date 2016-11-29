# 131 Palindrome Partitioning – Medium


### Problem:



Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given s = "aab",
Return

[

[“aa”,”b”],

["a","a","b"]
]

### Thoughts:



What is a Palindrome? A palindrome is like a string “aba” where it’s the same no matter if you read from left to right or right to left.

This problem has a optimal structure. If we cut a string s into s1 and s2. Now we need to find out a palindrome partitioning both for s1 and s2. These are new subproblems.

The first idea would be divide and conquer. However, we need to check all the partitioning which means that we cannot simply cut at a point in the string and divide the problem.

So dynamic programming might be a good try.

The idea is like the Rod Cut Problem in book . Suppose string s has length n. We have i from 1 to n, check if substring 0 to i in string s is a palindrome. If not we don’t need to do more, if yes we add this substring into the solution space of partitioning problem for substring i+1 to n. After checking all the possible position, we will get the answer.

One more thing is that we need to quickly check if a certain substring in string s is a palindrome. In order to do so, we build a auxiliary array isPa to keep in mind if that certain substring is palindrome. To calculate this array, we do another dynamic programming.


### Solutions:


```java
public class Solution {
    public List<List<String>> partition(String s) {
        boolean[][] isP = new boolean[s.length()][s.length()];
        List<List<String>> result = new LinkedList<List<String>>();
        List<String> curr = new LinkedList<String>();
        calIsP(isP, s);
        process(result, isP, s, curr, 0);
        return result;
    }
    private void process(List<List<String>> result, boolean[][] isP, String s, List<String> curr, int start) {
        if (start == s.length()) {
            result.add(new LinkedList<String>(curr));
        }
        for (int i = start; i < s.length(); i ++) {
            if (isP[start][i] == true) {
                curr.add(s.substring(start, i + 1));
                process(result, isP, s, curr, i + 1);
                curr.remove(curr.size() - 1);
            }
        }
    }
    private void calIsP(boolean[][] isP, String s) {
        for (int i = 0; i < s.length(); i ++) {
            isP[i][i] = true;
        }
        for (int i = 0; i < s.length() - 1; i ++) {
            isP[i][i + 1] = s.charAt(i) == s.charAt(i + 1);
        }
        for (int k = 2; k < s.length(); k ++) {
            for (int i = 0; i + k < s.length(); i ++) {
                isP[i][i + k] = s.charAt(i) == s.charAt(i + k) && isP[i + 1][i + k - 1] == true;
            }
        }
    }
}
```