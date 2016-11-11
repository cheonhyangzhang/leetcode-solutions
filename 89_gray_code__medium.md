# 89 Gray Code – Medium


### Problem:



The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:

00 - 0
01 - 1
11 - 3
10 - 2
Note:
For a given n, a gray code sequence is not uniquely defined.

For example, [0,2,3,1] is also a valid gray code sequence according to the above definition.

For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.


### Thoughts:



key idea is that  to generate gray code list for n, add 1<<(n-1) with the reverse order of the list for gray code n-1.

0: {0}

1: {0} + {1}    1<<0 = 1

2: {0,1}  + {11, 10}      1<< 1 = 10

3: {0, 1, 11, 10} + {110, 111, 101, 100}1 << 2 = 100


### Solutions:



```java
public class Solution {
    public List<Integer> grayCode(int n) {
        ArrayList<Integer> result = new ArrayList<Integer>();
        result.add(0);
        ArrayList<Integer> toAddAll = new ArrayList<Integer>();
        for (int i = 0; i < n; i ++){
            toAddAll.clear();
            int offset = 1 << i;
            for (int j = result.size() -1 ; j >= 0; j --){
                int toAdd = result.get(j) + offset;
                toAddAll.add(toAdd);
            }
            result.addAll(toAddAll);
        }
        return result;
    }
}
```
Updated: 11/10/2016 
This is an alternative, is a little bit more straightforward thinking, but this is taking more time than the solution above. Because it’s checking a lot of same element.
But this solution is easier to come up with.

```java
public class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> result = new LinkedList<Integer>();
        result.add(0);
        process(0, n, result);
        return result;
    }
    private void process(int num, int n , List<Integer> result) {
        for (int i = 0; i < n; i ++) {
            int mask = 1 << i;
            int tmp = num ^ mask;
            if (!result.contains(tmp)) {
                result.add(tmp);
                process(tmp, n, result);
            }
        }
    }
}
```