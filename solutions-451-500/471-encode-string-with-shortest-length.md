# 471. Encode String with Shortest Length

### Problem:
Given a non-empty string, encode the string such that its encoded length is the shortest.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times.
Note:
1. k will be a positive integer and encoded string will not be empty or have extra space.
2. You may assume that the input string contains only lowercase English letters. The string's length is at most 160.
3. If an encoding process does not make the string shorter, then do not encode it. If there are several solutions, return any of them is fine.

Example 1:
```
Input: "aaa"
Output: "aaa"
Explanation: There is no way to encode it such that it is shorter than the input string, so we do not encode it.
```
Example 2:
```
Input: "aaaaa"
Output: "5[a]"
Explanation: "5[a]" is shorter than "aaaaa" by 1 character.
```

Example 3:
```
Input: "aaaaaaaaaa"
Output: "10[a]"
Explanation: "a9[a]" or "9[a]a" are also valid solutions, both of them have the same length = 5, which is the same as "10[a]".
```

Example 4:
```
Input: "aabcaabcd"
Output: "2[aabc]d"
Explanation: "aabc" occurs twice, so one answer can be "2[aabc]d".
```

Example 5:
```
Input: "abbbabbbcabbbabbbc"
Output: "2[2[abbb]c]"
Explanation: "abbbabbbc" occurs twice, but "abbbabbbc" can also be encoded to "2[abbb]c", so one answer can be "2[2[abbb]c]".
```

### Solutions:

```java
public class Solution {
    public String encode(String s) {
        String[][] dp = new String[s.length()][s.length()];
        for (int l = 1; l <= s.length(); l ++) {
            for (int i = 0; i + l <= s.length(); i ++) {
                int j = i + l - 1;
                dp[i][j] = s.substring(i, j + 1);
                for (int k = i; k < j ; k ++) {
                    String cand = dp[i][k] + dp[k + 1][j];
                    if (cand.length() < dp[i][j].length()) {
                        dp[i][j] = cand;
                    }
                }
                String range = s.substring(i, j + 1);
                String drange = range + range;
                int cut = drange.indexOf(range, 1);
                if (cut != -1 && cut < range.length()) {
                    String cand = range.length() / cut + "[" + dp[i][i + cut - 1] +"]"; 
                    if (cand.length() < dp[i][j].length()) {
                        dp[i][j] = cand;
                    }
                }
            }
        }
        String res = dp[0][dp.length - 1];
        return res;
    }
}
```