# 20 Valid Parentheses – Easy


### Problem:



Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.


### Thoughts:



This is a problem that’s good to use a stack.


### Solutions:

```java
public class Solution {
    public boolean isValid(String s) {
        HashMap<Character, Character> match = new HashMap<Character, Character>();
        match.put(')','(');
        match.put('}','{');
        match.put(']','[');
        Stack<Character> stack = new Stack<Character>();
        for (int i = 0; i < s.length(); i ++){
            if (s.charAt(i) == '(' || s.charAt(i) == '{' || s.charAt(i) == '[') {
                stack.push(s.charAt(i));
                continue;
            }
            if (stack.size() == 0 || match.get(s.charAt(i)) != stack.pop()) {
                return false;
            }
        }
        if (stack.size() == 0) {
            return true;
        }
        return false;
    }
}
```