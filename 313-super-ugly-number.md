# 313 Super Ugly Number

### Problem:

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, [1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32] is the sequence of the first 12 super ugly numbers given primes = [2, 7, 13, 19] of size 4.

Note:
(1) 1 is a super ugly number for any given primes.
(2) The given numbers in primes are in ascending order.
(3) 0 < k ≤ 100, 0 < n ≤ 106, 0 < primes[i] < 1000.
(4) The nth super ugly number is guaranteed to fit in a 32-bit signed integer.

### Solutions:

```java
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] result = new int[n];
        result[0] = 1;
        int[] next = new int[primes.length];
        for (int i = 1; i < n; i ++) {
            int min = Integer.MAX_VALUE;
            for (int j = 0; j < primes.length; j ++) {
                min = Math.min(min, primes[j] * result[next[j]]);
            }
            for (int j = 0; j < primes.length; j ++) {
                if (primes[j] * result[next[j]] == min){
                    next[j] ++;
                }
            }
            result[i] = min;
        }
        return result [n - 1];
    }
}
```

```java
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int[] result = new int[n];
        result[0] = 1;
        int[] next = new int[primes.length];
        
        HashMap<Integer, List<Integer>> index = new HashMap<Integer, List<Integer>>();
        PriorityQueue<Integer> q = new PriorityQueue<Integer>();
        for (int i = 0; i < primes.length; i ++) {
            q.add(primes[i]);
            index.put(primes[i], new LinkedList<Integer>());
            index.get(primes[i]).add(i);
        }
        
        for (int i = 1; i < n; i ++) {
            int min = q.poll();
            List<Integer> indexToUpdate = index.get(min);
            result[i] = min;
            for (Integer j:indexToUpdate) {
                next[j] ++;
                int cand = result[next[j]] * primes[j];
                if (index.containsKey(cand)) {
                    index.get(cand).add(j);
                }
                else {
                    index.put(cand, new LinkedList<Integer>());
                    index.get(cand).add(j);
                    q.add(cand);
                }
            }
        }
        
        
        return result [n - 1];
    }
}
```