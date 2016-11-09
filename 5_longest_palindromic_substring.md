# 5 Longest Palindromic Substring


### Problem:


Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.


### Thoughts:


Trivial way is to calculate each substring is palindrome, using O(n^2) time and space.
Could be optimized using only O(1) space.
Idea is to return the longest palindromic substring that is center by (i,i) or (i, i + 1).


### Solution:


Trivial way:

```java
public class Solution {
    public String longestPalindrome(String s) {
        boolean[][] isPa = new boolean[s.length()][s.length()];
        calIsPa(isPa, s);
        String longest = "";
        int max = 0;
        for (int i = 0; i < s.length(); i ++){
            for (int j = i; j < s.length(); j ++){
                if (isPa[i][j] == true && (j - i + 1) > max){
                    max = j - i + 1;
                    longest = s.substring(i, j + 1);
                }
            }
        }
        return longest;
    }
    private void calIsPa(boolean[][] isPa, String s){
        for (int i = 0; i < s.length(); i ++){
            isPa[i][i] = true;
        }
        for (int i = 0; i < s.length() - 1; i ++){
            if (s.charAt(i) == s.charAt(i+1)){
                isPa[i][i+1] = true;
            }
        }
        for (int l = 3; l <= s.length(); l ++ ){
            for (int i = 0; i < s.length() - l + 1; i ++){
                if (s.charAt(i) == s.charAt(i + l - 1) && isPa[i+1][i + l -2]){
                    isPa[i][i+ l - 1] = true;
                }
            }
        }
    }
     
}
```
The better way:

```java
public class Solution {
    public String longestPalindrome(String s) {
        String longest = "";
        for (int i = 0; i < s.length(); i ++){
            String tmp = "";
            tmp = paCenterBy(s, i, i);
            if (tmp.length() > longest.length()){
                longest = tmp;
            }
            tmp = paCenterBy(s, i, i + 1);
            if (tmp.length() > longest.length()){
                longest = tmp;
            }
        }  
        return longest;
    }
    private String paCenterBy(String s, int cleft, int cright){
        String result = "";
        while (cleft >=0 && cright < s.length() && s.charAt(cleft) == s.charAt(cright)){
            cleft --;
            cright ++;
        }
        return s.substring(cleft + 1, cright);
    }
}
```