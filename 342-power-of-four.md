# 342 Power of Four

### Problem:

Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

Example:
Given num = 16, return true. Given num = 5, return false.

Follow up: Could you solve it without loops/recursion?

### Solution:

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        if (num <= 0) {
            return false;
        }
        while (num > 3) {
            if (num % 4 != 0) {
                return false;
            }
            num = num / 4;
        }
        return num == 1;
    }
}
```

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        return num == 1 || num == 4 || num == 16 || num == 64 || num == 256 || num == 1024 || num == 4096 || num == 16384 || num == 65536 || num == 262144 || num == 1048576 || num == 4194304 || num == 16777216 || num == 67108864 || num == 268435456 || num == 1073741824;
    }
}
```

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        int count0=0;
        int count1=0;
     
        while(num>0){
            if((num&1)==1){
                count1++;
            }else{
                count0++;
            }
     
            num>>=1;
        }
     
        return count1==1 && (count0%2==0);
    }
}
```

```java
public class Solution {
    public boolean isPowerOfFour(int num) {
        if (num <= 0) {
            return false;
        }
        double res = Math.log10(num) / Math.log10(4);  
        return Double.compare(res, (int)res) == 0;
    }
}
```

