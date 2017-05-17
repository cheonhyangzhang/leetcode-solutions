# 241 Different Ways to Add Parentheses – Medium

### Problem:
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.
Example 1

Input: "2-1-1".
```
((2-1)-1) = 0
(2-(1-1)) = 2
```
Output: [0, 2]
Example 2

Input: "2*3-4*5"
```
(2*(3-(4*5))) = -34
((2*3)-(4*5)) = -14
((2*(3-4))*5) = -10
(2*((3-4)*5)) = -10
(((2*3)-4)*5) = 10
```
Output: [-34, -14, -10, -10, 10]

### Thoughts:
The problem doesn’t say if each original number is positive. But based on the solution below can pass the test, so this is one of the assumption. If the original number can be negative, we just need some more operation to extract number.

The key here is that we each continuous two elements can be calculated first.
For the e.g above, 23 can be calculated first, or 3 – 4 can be calculated first, then for these two cases the problem becomes 6-45 and 2(-1)5.
So it will become two sub problem.
It is very promising to use a divide and conquer.
If we use [23-45] to represent a problem of such, it can be broken into 2[3-45], [23]-[45] and [23-4]5 sub problems.

In the first solution below, it shows an idea of such. It uses a regular expression to help extract nums and operators. While is not necessary to use though.

In the second solution, it is not using regular expression and the code is less.

If performance is a concern, then we can use memorization to improve performance. E.g use a HashMap data to keep the return value for a given string. So that we avoid redo a problem that’s already been processed.

### Solutions:

```java
public class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> result = new LinkedList<Integer>();
        for (int i = 0; i < input.length(); i ++) {
            char c = input.charAt(i);
            if (c == '+' || c == '-' || c == '*') {
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1));
                for (Integer l:left) {
                    for (Integer r:right) {
                        result.add(cal(l, r, c));
                    }
                }
            }
        }
        if (result.size() == 0) {
            result.add(Integer.parseInt(input));
        }
        return result;
    }
    private int cal(int num1, int num2, char c) {
        if (c == '+') {
            return num1 + num2;
        }
        if (c == '-') {
            return num1 - num2;
        }
        if (c == '*') {
            return num1 * num2;
        }
        return 0;
    }
}
```