# 267. Palindrome Permutation II

### Problem:

Given a string s, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

For example:

Given s = "aabb", return ["abba", "baab"].

Given s = "abc", return [].

Hint:

If a palindromic permutation exists, we just need to generate the first half of the string.

### Thoughts:

```java
public class Solution {
    public List<String> generatePalindromes(String s) {
        int[] cha = new int [256]; 
        for (int i = 0; i < s.length(); i ++) {
            cha[s.charAt(i)] += 1;
        }
        List<String> result = new LinkedList<String>();
        boolean odd = false;
        int oddIndex = 0;
        for (int i = 0; i < 256; i ++) {
            if (cha[i] % 2 == 1) {
                if (odd == true) {
                    return result;
                }
                oddIndex = i;
                odd = true;
            }
        }
        
        String base = "";
        if (odd == true) {
            base = (char)oddIndex + "";
            cha[oddIndex] -= 1;
        }
        process(base, cha, s.length(), result);
        return result;
    }
    private void process(String base, int[] cha, int n, List<String> result) {
        if (base.length() == n) {
            result.add(base);
            return;
        }
        for (int i = 0; i < cha.length; i ++) {
            if (cha[i] > 0) {
                cha[i] -= 2;
                process((char)i + base + (char)i, cha, n, result);
                cha[i] += 2;
            }
        }
    }
}
```