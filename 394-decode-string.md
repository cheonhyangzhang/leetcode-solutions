# 394. Decode String

### Problem:

Given an encoded string, return it's decoded string.

The encoding rule is: k[encoded_string], where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

Examples:
```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

### Solutions:

```java
public class Solution {
    public String decodeString(String s) {
        Stack<Integer> nums = new Stack<Integer>();
        Stack<Character> chars = new Stack<Character>();
        int count = 0;
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c >= '0' && c <= '9') {
                count = count * 10 + (c - '0');
            }
            else if (c == ']') {
                int repeat = nums.pop();
                String tmp = "";
                while (chars.peek() != '[') {
                   tmp = chars.pop() + tmp;     
                }
                chars.pop();
                for (int j = 0; j < repeat; j ++) {
                    for (int k = 0; k < tmp.length(); k ++) {
                        chars.push(tmp.charAt(k));
                    }
                }
            }
            else {
                if (count != 0) {
                    nums.push(count);
                }   
                count = 0;
                chars.push(c);
            }
        }
        String result = "";
        while (!chars.isEmpty()) {
            result = chars.pop() + result;
        }
        return result;
    }
}
```

```java
public class Solution {
    public String decodeString(String s) {
        String res = "";
        Stack<Integer> nums = new Stack<Integer>();
        Stack<String> strs = new Stack<String>();
        int cnt = 0;
        for (int i = 0; i < s.length(); ++i) {
            if (s.charAt(i) >= '0' && s.charAt(i) <= '9') {
                cnt = 10 * cnt + s.charAt(i) - '0';
            } else if (s.charAt(i) == '[') {
                nums.push(cnt);
                strs.push(res);
                cnt = 0; res = "";
            } else if (s.charAt(i) == ']') {
                int k = nums.pop();
                String next = strs.pop();
                for (int j = 0; j < k; ++j) 
                    next += res;
                res = next; 
            } else {
                res += s.charAt(i);
            }
        }
        return res;
    }
}
```