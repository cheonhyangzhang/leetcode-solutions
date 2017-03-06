# 224. Basic Calculator

### Problem:
Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open ( and closing parentheses ), the plus + or minus sign -, non-negative integers and empty spaces .

You may assume that the given expression is always valid.

Some examples:
```
"1 + 1" = 2
" 2-1 + 2 " = 3
"(1+(4+5+2)-3)+(6+8)" = 23
```

### Solutions:

```java
public class Solution {
    public int calculate(String s) {
        Stack<Integer> nums = new Stack<Integer>();
        Stack<Character> ops = new Stack<Character>();
        for (int i = 0; i < s.length(); i ++) {
            char c = s.charAt(i);
            if (c == ' ') {
                continue;
            }
            if (c == '(') {
                nums.push(null);
                continue;
            }
            if (c == ')') {
                int count = nums.pop();
                nums.pop();
                nums.push(count);
                cal(nums, ops);
                continue;
            }
            if (c == '+' || c == '-') {
                ops.push(c);
                continue;
            }
            int j = i;
            int count = 0;
            while (j < s.length() && s.charAt(j) >= '0' && s.charAt(j) <= '9') {
                count = count * 10 + (s.charAt(j) - '0');
                j ++;
            }
            i = j - 1;
            nums.push(count);
            cal(nums, ops);
        }
        if (nums.isEmpty()) {
            return 0;
        }
        return nums.pop();
    }
    private void cal(Stack<Integer> nums, Stack<Character> ops) {
        if (nums.size() < 2 || ops.isEmpty()) {
            return;
        }
        Integer num2 = nums.pop();
        Integer num1 = nums.pop();
        if (num1 == null) {
            nums.push(num1);
            nums.push(num2);
            return;
        }
        char op = ops.pop();
        if (op == '+') {
            nums.push(num1 + num2);
            cal(nums, ops);
            return;
        }
        if (op == '-') {
            nums.push(num1 - num2);
            cal(nums, ops);
            return;
        }
    }
}
```

```java

```