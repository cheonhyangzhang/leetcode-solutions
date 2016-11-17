# 28 Implement strStr() – Easy


### Problem:



Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.


### Thoughts:



Very straightforward. String manipulation.


### Solutions:

```java
public class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.equals("")) {
            return 0;
        }
        for (int i = 0; i < (haystack.length() - needle.length()) + 1; i ++ ){
            for (int j = 0; j < needle.length(); j ++ ) {
                if (haystack.charAt(i+j) != needle.charAt(j)){
                    break;
                }
                if (j == needle.length() -1) {
                    return i;
                }
            }
        }
        return -1;
    }
}
```
KMP algorithm.
https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm

```java
public class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.length() == 0) {
            return 0;
        }
        int[] kmp = new int[needle.length()];
        computeKMP(needle, kmp);
        int i = 0, j = 0;//i is for haystack and j is for needle
        while (i < haystack.length()) {
            if (j == -1) {
                j = 0;
                i ++;
                continue;
            }
            if (haystack.charAt(i) == needle.charAt(j)) {
                if (j == needle.length() -1) {
                    return i - needle.length() + 1;
                }
                i ++;
                j ++;
            }
            else {
                j = kmp[j];
            }
        }
        return -1;
    }
    private void computeKMP(String s, int[] kmp){
        int prefixEnd = -1;
        int suffixEnd = 0;
        kmp[0] = -1;
        //while loop updates kmp[suffixEnd + 1]
        while (suffixEnd < s.length() - 1) {
            if (prefixEnd == -1 || s.charAt(prefixEnd) == s.charAt(suffixEnd)) {
                kmp[suffixEnd +1] = prefixEnd + 1;
                prefixEnd ++;
                suffixEnd ++;
            }
            else {
                prefixEnd = kmp[prefixEnd];   
            }
        }
    }
}
```