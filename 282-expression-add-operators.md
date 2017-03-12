# 282. Expression Add Operators

### Problem:

Given a string that contains only digits 0-9 and a target value, return all possibilities to add binary operators (not unary) +, -, or * between the digits so they evaluate to the target value.

Examples: 
```
"123", 6 -> ["1+2+3", "1*2*3"] 
"232", 8 -> ["2*3+2", "2+3*2"]
"105", 5 -> ["1*0+5","10-5"]
"00", 0 -> ["0+0", "0-0", "0*0"]
"3456237490", 9191 -> []
```

### Solutions:

```java
public class Solution {
    public List<String> addOperators(String num, int target) {
        List<String> result = new LinkedList<String>();
        process("", 0, 0, result, num, target);
        return result;
    }
    private void process(String curr, long sum, long addToSum, List<String> result, String num, int target) {
        if (num.length() == 0 && target == sum) {
            result.add(curr);
            return;
        }
        for (int i = 1; i <= num.length(); i ++) {
            String first = num.substring(0, i);
            String second = num.substring(i);
            if (first.charAt(0) == '0' && first.length() > 1) {
                return;
            }
            long firstLong = Long.parseLong(first);
            if (curr.equals("")) {
                process(first, firstLong, firstLong, result, second, target);
            }
            else {
                process(curr + "+" + first, sum + firstLong, firstLong, result, second, target);
                process(curr + "-" + first, sum - firstLong, -firstLong, result, second, target);
                process(curr + "*" + first, (sum - addToSum) + addToSum * firstLong, addToSum * firstLong, result, second, target);
            }
        }
    }
}
```