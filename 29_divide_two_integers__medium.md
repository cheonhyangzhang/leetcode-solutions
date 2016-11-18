# 29 Divide Two Integers – Medium


### Problem:



Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.


### Thoughts:



Integer problem is always kind of tricky. In Java, Integer range is 2,147,483,648 to 2,147,483,647. The first impression to implement is to imitate human’s calculation process. But this one is different because it does not allow using multiplication, division and mod operator. So the only left choice is to use shift operation.

The solution below is still trying to mimic human calculation using shift operation.

The reason to use long instead of integer is to avoid possible stack overflow when doing the shifting operation.


### Solutions:



```java
public class Solution {
    public int divide(int dividend, int divisor) {
        int dd = dividend;
        int dr = divisor;
        if(dr == 0){
            return Integer.MAX_VALUE;
        }
        if(dr == -1 && dd == Integer.MIN_VALUE){
            return Integer.MAX_VALUE;
        }
        int flag = 1;
        if((dd < 0 && dr > 0) || (dd > 0 && dr < 0)){ 
            flag = -1; 
        } 
        long ldd = Math.abs((long)dd); 
        long ldr = Math.abs((long)dr); 
        int result = 0; 
        while(ldd >= ldr){
            int shift = 0;
            while(ldd >= (ldr << shift)){
                shift++;
            }
            shift --;
            result += 1 << shift;
            ldd -= ldr << shift;
        }
        return result*flag;
    }
}
```