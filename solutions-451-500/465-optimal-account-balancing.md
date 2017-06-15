# 465 Optimal Account Balancing

### Problem:
A group of friends went on holiday and sometimes lent each other money. For example, Alice paid for Bill's lunch for $10. Then later Chris gave Alice $5 for a taxi ride. We can model each transaction as a tuple (x, y, z) which means person x gave person y $z. Assuming Alice, Bill, and Chris are person 0, 1, and 2 respectively (0, 1, 2 are the person's ID), the transactions can be represented as [[0, 1, 10], [2, 0, 5]].

Given a list of transactions between a group of people, return the minimum number of transactions required to settle the debt.

Note:

1. A transaction will be given as a tuple (x, y, z). Note that x ≠ y and z > 0.

2. Person's IDs may not be linear, e.g. we could have the persons 0, 1, 2 or we could also have the persons 0, 2, 6.

Example 1:
```
Input:
[[0,1,10], [2,0,5]]

Output:
2

Explanation:
Person #0 gave person #1 $10.
Person #2 gave person #0 $5.

Two transactions are needed. One way to settle the debt is person #1 pays person #0 and #2 $5 each.
```

Example 2:
```
Input:
[[0,1,10], [1,0,1], [1,2,5], [2,0,5]]

Output:
1

Explanation:
Person #0 gave person #1 $10.
Person #1 gave person #0 $1.
Person #1 gave person #2 $5.
Person #2 gave person #0 $5.

Therefore, person #1 only need to give person #0 $4, and all debt is settled.
```

```java
public class Solution {
    public int minTransfers(int[][] transactions) {
        int[][] trans = transactions;
        HashMap<Integer, Integer> debts = new HashMap<Integer, Integer>();
        for (int i = 0; i < trans.length; i ++) {
            int give = trans[i][0];
            int get = trans[i][1];
            int money = trans[i][2];
            if (!debts.containsKey(give)) {
                debts.put(give, 0);
            }
            if (!debts.containsKey(get)) {
                debts.put(get, 0);
            }
            debts.put(give, debts.get(give) + money);
            debts.put(get, debts.get(get) - money);
        }
        int[] debtsArr = new int[debts.size()];
        int index = 0;
        for (Integer no:debts.keySet()) {
            debtsArr[index ++] = debts.get(no);
        }
        return process(debtsArr, 0, 0);
    }
    private int process(int[] debts, int start, int count) {
        int min = Integer.MAX_VALUE;
        while (start < debts.length && debts[start] == 0) {
            start ++;
        }
        for (int i = start + 1; i < debts.length; i ++) {
            if (debts[i] == 0) {
                continue;
            }
            if ((debts[start] > 0 && debts[i] < 0) || (debts[start] < 0 && debts[i] > 0)) {
                debts[i] += debts[start];
                min = Math.min(min, process(debts, start + 1, count + 1));
                debts[i] -= debts[start];
            }
        }
        if (min == Integer.MAX_VALUE) {
            return count;
        }
        return min;
    }
}
```
