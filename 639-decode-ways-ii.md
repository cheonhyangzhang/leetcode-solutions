# 639 Decode Ways II

### Problem
A message containing letters from A-Z is being encoded to numbers using the following mapping way:
```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
Beyond that, now the encoded string can also contain the character '*', which can be treated as one of the numbers from 1 to 9.

Given the encoded message containing digits and the character '*', return the total number of ways to decode it.

Also, since the answer may be very large, you should return the output mod 109 + 7.

Example 1:
```
Input: "*"
Output: 9
Explanation: The encoded message can be decoded to the string: "A", "B", "C", "D", "E", "F", "G", "H", "I".
```
Example 2:
```
Input: "1*"
Output: 9 + 9 = 18
```
Note:
The length of the input string will fit in range [1, 105].
The input string will only contain the character '*' and digits '0' - '9'.


### Solutions

```java
class Solution {
    public int numDecodings(String s) {
        long mod = (int)Math.pow(10, 9) + 7;
        long prepre = 1, pre = 1, curr = 0;
        for (int i = 0; i < s.length(); i ++) {
            if (i == 0) {
                if (s.charAt(i) == '0') {
                    return 0;
                }
                else if (s.charAt(i) == '*') {
                    curr = 9;
                }
                else {
                    curr = 1;
                }
            }
            else {
                curr = 0;
                if (s.charAt(i) != '*') {
                    if (s.charAt(i) != '0') {
                        curr += pre;
                    }
                }
                else {
                    curr += pre * 9;
                }
                if (i - 1 >= 0) {
                    if (s.charAt(i) != '*') {
                        if (s.charAt(i - 1) == '1' || (s.charAt(i - 1) == '2' && s.charAt(i) <= '6')) {
                            curr += prepre;
                        }
                        else if (s.charAt(i - 1) == '*') {
                            if (s.charAt(i) <= '6') {
                                curr += prepre * 2;
                            }
                            else {
                                curr += prepre;
                            }
                        }
                    }
                    else {
                        if (s.charAt(i - 1) == '1') {
                            curr += prepre * 9;
                        }
                        else if (s.charAt(i - 1) == '2') {
                            curr += prepre * 6;
                        }
                        else if (s.charAt(i - 1) == '*') {
                            curr += prepre * 15;
                        }
                    }
                }
                
            }
            
            curr = curr % mod;
            prepre = pre;
            pre = curr;
        }
        return (int)curr;
    }
}
```