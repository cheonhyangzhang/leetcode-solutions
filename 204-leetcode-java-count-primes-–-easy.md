# 204 LeetCode Java: Count Primes – Easy

### Problem:
Count the number of prime numbers less than a non-negative number, n.

### Thoughts:

Because for this problem, it is not simple check if one number is prime or not, we could not use the trivial way to check. Otherwise it would be too slow.

The solution below is using Sieve of Eratosthenes way to calculate composite.

All numbers under n that is not a composite, it is a prime. Of course 1 is not a prime.

### Solutions:

```java
public class Solution {
    public int countPrimes(int n) {
        boolean[] iscomp = new boolean[n];
        for (int i = 2; i*i < n; i ++){
            for (int j = 2; i*j < n; j ++){
                iscomp[i*j] = true;
            }
        }
        //count prime
        int count = 0;
        for (int i = 2; i < n; i ++){
            if (iscomp[i] == false)
                count ++;
        }
        return count;
    }
}
```