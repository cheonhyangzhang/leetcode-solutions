# 444. Sequence Reconstruction

### Problem:

Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 104. Reconstruction means building a shortest common supersequence of the sequences in seqs (i.e., a shortest sequence so that all sequences in seqs are subsequences of it). Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

Example 1:
```
Input:
org: [1,2,3], seqs: [[1,2],[1,3]]

Output:
false

Explanation:
[1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.
```

Example 2:
```
Input:
org: [1,2,3], seqs: [[1,2]]

Output:
false

Explanation:
The reconstructed sequence can only be [1,2].
```

Example 3:
```
Input:
org: [1,2,3], seqs: [[1,2],[1,3],[2,3]]

Output:
true

Explanation:
The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
```

Example 4:
```
Input:
org: [4,1,5,2,6,3], seqs: [[5,2,6,3],[4,1,5,2]]

Output:
true
```

### Solutions:

```java
public class Solution {
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        int[] min = new int[org.length];
        int[] max = new int[org.length];
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        index.put(Integer.MAX_VALUE, org.length);
        for (int i = 0; i < org.length; i ++) {
            min[i] = 0;
            max[i] = org.length - 1;
            index.put(org[i], i);
        }
        boolean checked = false;
        for (List<Integer> seq:seqs) {
            for (int i = 0; i < seq.size(); i ++) {
                checked = true;
                int first = seq.get(i);
                int second = Integer.MAX_VALUE;
                if (i + 1 < seq.size()) {
                    second = seq.get(i + 1);
                }
                if (!index.containsKey(first) || !index.containsKey(second)) {
                    return false;
                }
                int firstIndex = index.get(first);
                int secondIndex = index.get(second);
                max[firstIndex] = Math.min(max[firstIndex], secondIndex - 1);
                if (secondIndex < org.length) {
                    min[secondIndex] = Math.max(min[secondIndex], firstIndex + 1);
                }
            }
        }
        if (org.length == 1 && !checked) {
            return false;
        }
        for (int i = 0; i < org.length; i ++) {
            if (max[i] != min[i]) {
                return false;
            }
        }
        return true;
    }
}
```

```java
public class Solution {
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        HashMap<Integer, Integer> pre = new HashMap<Integer, Integer>();
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        for (int i = 0; i < org.length; i ++) {
            index.put(org[i], i);
        }
        for (List<Integer> seq:seqs) {
            for (int i = 0; i < seq.size(); i ++) {
                if (!index.containsKey(seq.get(i))) {
                    return false;
                }
                if (!pre.containsKey(seq.get(i))) {
                    pre.put(seq.get(i), i > 0? index.get(seq.get(i - 1)): -1);
                }
                else {
                    pre.put(seq.get(i), Math.max(pre.get(seq.get(i)), i > 0? index.get(seq.get(i - 1)): -1));
                }
            }
        }
        for (int i = 0; i < org.length; i ++) {
            if (!pre.containsKey(org[i]) || pre.get(org[i]) != i - 1) {
                return false;
            }
        }
        return true;
    }
}
```

```java
public class Solution {
    public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
        HashMap<Integer, Integer> index = new HashMap<Integer, Integer>();
        boolean[] checked = new boolean[org.length];
        for (int i = 0; i < org.length; i ++) {
            index.put(org[i], i);
        }
        boolean hasChecked = false;
        int toCheck = org.length - 1;
        for (List<Integer> seq:seqs) {
            for (int i = 0; i < seq.size(); i ++) {
                hasChecked = true;
                int curr = seq.get(i);
                if (curr <= 0 || curr > org.length) {
                    return false;
                }
                if (i == 0) {
                    continue;
                }
                int pre = seq.get(i - 1);
                if (index.get(pre) >= index.get(curr)) {
                    return false;
                }
                if (checked[index.get(curr)] == false && index.get(pre) == index.get(curr) - 1) {
                    checked[index.get(curr)] = true;
                    toCheck --;
                }
            }
        }
        return toCheck == 0 && hasChecked;
    }
}
```