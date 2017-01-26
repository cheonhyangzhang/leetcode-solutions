# 365 Water and Jug Problem

### Problem:

You are given two jugs with capacities x and y litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactly z litres using these two jugs.

If z liters of water is measurable, you must have z liters of water contained within one or both buckets by the end.

Operations allowed:

Fill any of the jugs completely with water.
Empty any of the jugs.
Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.
Example 1: (From the famous "Die Hard" example)
```
Input: x = 3, y = 5, z = 4
Output: True
```
Example 2:
```
Input: x = 2, y = 6, z = 5
Output: False
```

### Solutions:

```java
public class Solution {
      public boolean canMeasureWater(int x, int y, int z) {
            HashSet<Integer> valid = new HashSet<Integer>();
            Collections.addAll(valid, 0, x, y, x + y);
            int max = Math.max(x, y);
            int sum = x + y;
            Queue<Integer> sons = new LinkedList<Integer>();
            sons.add(Math.abs(x - y));
            while (!sons.isEmpty()) {
                  int son = sons.poll();
                  process(max, sum, son + x, valid, sons);
                  process(max, sum, son + y, valid, sons);
                  process(max, sum, son - x, valid, sons);
                  process(max, sum, son - y, valid, sons);
                  process(max, sum, x - son, valid, sons);
                  process(max, sum, y - son, valid, sons);
            }
            return valid.contains(z);
      }
      private void process(int max, int sum, int num, HashSet<Integer> valid, Queue<Integer> sons) {
            if (num <= 0) {
                  return;
            }
            if (num > 0 && num < max && !valid.contains(num)) {
                  valid.add(num);
                  sons.add(num);
            }
            else if (num < sum && !valid.contains(num)) {
                  valid.add(num);
            }
      }
}
```

```java
public class Solution {
    public boolean canMeasureWater(int x, int y, int z) {
        return z == 0 || (x + y >= z && z % gcd(x, y) == 0);
    }
    private int gcd(int x, int y) {
        return y == 0 ? x : gcd(y, x % y);
    }
}
```

```java
public class Solution {
    public boolean canMeasureWater(int x, int y, int z) {
        if(x>y)
            return canMeasureWater(y,x,z);
        if(z > x+y)
            return false;
        Set<Integer> failSet = new HashSet<>();

        int resX = 0;
        int resY = 0;

        while(true){
            int res = resX * x + resY * y;
            if(failSet.contains(res))
                return false;
            if(res == z){
                return true;
            }else if(res < z){
                resY++;
            }else{
                resX--;
            }
            failSet.add(res);
        }
    }
}
```