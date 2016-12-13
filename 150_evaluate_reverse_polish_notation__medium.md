# 150 Evaluate Reverse Polish Notation – Medium

### Problem:



Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each operand may be an integer or another expression.

Some examples:

  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6

### Thoughts:



This is a very straight forward problem using a stack.


### Solutions:


```java
public class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> nums = new Stack<Integer>();
        for (int i = 0; i < tokens.length; i ++) {
            String op = tokens[i];
            if (op.equals("+")) {
                nums.push(nums.pop() + nums.pop());
                continue;
            }
            if (op.equals("-")) {
                int num = nums.pop();
                nums.push(nums.pop() - num);
                continue;
            }
            if (op.equals("*")) {
                nums.push(nums.pop() * nums.pop());
                continue;
            }
            if (op.equals("/")) {
                int num = nums.pop();
                nums.push(nums.pop() / num);
                continue;
            }
            nums.push(Integer.parseInt(op));
        }
        return nums.pop();
    }
}
```
