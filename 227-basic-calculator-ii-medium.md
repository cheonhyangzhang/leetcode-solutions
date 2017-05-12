# 227 Basic Calculator II – Medium


### Problem:
Implement a basic calculator to evaluate a simple expression string.

The expression string contains only non-negative integers, +, -, *, / operators and empty spaces . The integer division should truncate toward zero.

You may assume that the given expression is always valid.

Some examples:

“3+2*2″ = 7
” 3/2 ” = 1
” 3+5 / 2 ” = 5

Note: Do not use the eval built-in library function.

### Thoughts:
The idea is to always calculate * and / first, I am using regular expression to extract numbers and operators.
Notice that when you have String s= ".ab.", then call s.split("\\.") will end up with a String[] which is {“”,”ab”}.

When iterating over the operators, when meet a ‘+’ or ‘-‘, then we can pass the next number into stack, notice that if we meet ‘-‘, we push the negative value of that number.
When meet a ‘*’ or ‘/’ it means we need to calculate this first, pop one element from the stack and use it to calculate with the next number. Then push the result back to the stack. If the popped element is <0, then the result of * or / is still negative which keeps everything correct.

Extracting numbers and ops can be done by iterating instead of using regex as well.

### Solutions:

```java
public class Solution {
    public int calculate(String s) {
        s = s.trim().replaceAll(" ","");
        String[] nums = s.split("[\\+\\-\\*/]+");
        String[] ops = s.split("[\\d]+");
        Stack<Integer> numsStack = new Stack<Integer>();
        numsStack.push(Integer.parseInt(nums[0]));
        for (int i = 1; i < ops.length; i ++) {
            int curr = Integer.parseInt(nums[i]);
            if (ops[i].equals("*")) {
                curr = numsStack.pop() * curr;
            }
            if (ops[i].equals("/")) {
                curr = numsStack.pop() / curr;
            }
            if (ops[i].equals("-")){
                curr = -curr;
            }
            numsStack.push(curr);
        }
        int result = 0;
        while (numsStack.size() > 0) {
            result += numsStack.pop();
        }
        return result;
    }
}
```