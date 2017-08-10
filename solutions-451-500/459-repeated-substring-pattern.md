# 459. Repeated Substring Pattern

### Problem:

Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.

Example 1:
```
Input: "abab"

Output: True

Explanation: It's the substring "ab" twice.
```

Example 2:
```
Input: "aba"

Output: False
```

Example 3:
```
Input: "abcabcabcabc"

Output: True

Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
```

### Solutions:

```java
public class Solution {
    public boolean repeatedSubstringPattern(String str) {
        for (int i = 0; i < str.length() / 2; i ++) {
            int count = i + 1;
            if (str.length() % count != 0) {
                continue;
            }
            boolean same = true;
            for (int k = count; k + count <= str.length() && same; k+=count) {
                for (int j = 0; j <= i && same; j ++) {
                    if (str.charAt(j) != str.charAt(j + k)) {
                        same = false;
                    }
                }
            }
            if (same == true) {
                return true;
            }
        }
        return false;
    }
}
```

```java
public class Solution {
    public boolean repeatedSubstringPattern(String str) {
        int n = str.length();
        for (int count = n / 2; count >= 1; count --) {
            if (n % count == 0) {
                int num = n / count;
                StringBuilder sb = new StringBuilder();
                String cand = str.substring(0, count);
                for (int j = 0; j < num; j ++) {
                    sb.append(cand); 
                }
                if (sb.toString().equals(str)) 
                    return true;
            }
        }
        return false;
    }
}
```

```java
public class Solution {
    public boolean repeatedSubstringPattern(String str) {
        for (int i = 1; i <= str.length() / 2; i ++) {
            if (str.length() % i == 0) {
                if (str.substring(0, str.length() - i).equals(str.substring(i))) {
                    return true;
                }
            }
        }
        return false;
    }
}
```

```java
public class Solution {
    public boolean repeatedSubstringPattern(String s) {
        String doubled = s + s;
        int cut = doubled.indexOf(s, 1);
        if (cut >= 1 && cut < s.length()) {
            return true;
        }
        return false;
    }
}
```
