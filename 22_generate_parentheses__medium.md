# 22 Generate Parentheses – Medium


### Problem:



Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

"((()))", "(()())", "(())()", "()(())", "()()()"


### Thoughts:



Key idea is that, if you still have left parantheses left, you have two choice : insert a parantheses or a right parenthesis. But the condition for inserting right parenthesis is that used left ones is more than used right ones.

### Solutions:


```java
public class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new LinkedList<String>();
        process("", n, n, result);
        return result;
    }
    private void process(String prefix, int left, int right, List<String> result) {
        if (left == 0 && right == 0) {
            result.add(prefix);
            return;
        }
        if (left > 0) {
            process(prefix + '(', left - 1, right, result);
        }
        if (left < right) {
            process(prefix + ')', left, right - 1, result);
        }
    }
}
```