# 202 LeetCode Java: Happy Number – Easy

### Problem:

Write an algorithm to determine if a number is “happy”.

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number

12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
### Thoughts:

This is a very straight forward integer problem. Just do the formula addition, and then check if the result is one.

Do this repeatedly until 1 occurs or same appearing number appears twice. Using a HashSet to keep appearing number is helpful.

### Solutions:

```java
public class Solution {
    private HashSet<Integer> visited = new HashSet<Integer>();
    public boolean isHappy(int n) {
        while(true){
            if (visited.contains(n)){
                return false;
            }
            else{
                int val = sum(n);
                if (val == 1){
                    return true;
                }
                else{
                    visited.add(n);
                    n = val;
                }
            }//else
        }//while true
    }
    private int sum(int n){
        int result = 0;
        while (n != 0){
            result += Math.pow(n % 10, 2);
            n = n / 10;
        }
        return result;
    }
}
```
Updated:12/31/2016
Improve logic.

```java
public class Solution {
    public boolean isHappy(int n) {
        HashSet<Integer> data = new HashSet<Integer>();
        while (true) {
            int r = process(n);
            if (r == 1) {
                return true;
            }
            if (data.contains(r)) {
                return false;
            }
            data.add(r);
            n = r;
        }
    }
    private int process(int n) {
        int result = 0;
        while (n != 0) {
            result += (n % 10) * (n % 10);
            n = n / 10;
        }
        return result;
    }
}
```