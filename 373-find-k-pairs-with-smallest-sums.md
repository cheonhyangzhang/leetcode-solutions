# 373 Find K Pairs with Smallest Sums

### Problem:

You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.

Define a pair (u,v) which consists of one element from the first array and one element from the second array.

Find the k pairs (u1,v1),(u2,v2) ...(uk,vk) with the smallest sums.

Example 1:
```
Given nums1 = [1,7,11], nums2 = [2,4,6],  k = 3

Return: [1,2],[1,4],[1,6]

The first 3 pairs are returned from the sequence:
[1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```
Example 2:
```
Given nums1 = [1,1,2], nums2 = [1,2,3],  k = 2

Return: [1,1],[1,1]

The first 2 pairs are returned from the sequence:
[1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

Example 3:
```
Given nums1 = [1,2], nums2 = [3],  k = 3 

Return: [1,3],[2,3]

All possible pairs are returned from the sequence:
[1,3],[2,3]
```

### Solutions:

```java
public class Solution {
    public List<int[]> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        int[] index = new int[nums1.length];
        List<int[]> result = new LinkedList<int[]>();
        for (int i = 0; i < k; i ++) {
            int min = Integer.MAX_VALUE;
            int chosen = -1;
            for (int j = 0; j < nums1.length; j ++) {
                if (index[j] >= nums2.length) {
                    continue;
                }
                int tmp = nums1[j] + nums2[index[j]];
                if (tmp < min) {
                    min = tmp;
                    chosen = j;
                }
            }
            if (chosen != -1) {
                result.add(new int[]{nums1[chosen], nums2[index[chosen]]});
                index[chosen] ++;
            }
        }
        return result;
    }
}
```

```java
public class Solution {
    private class Pair implements Comparable<Pair>{
        private int i1;
        private int i2;
        private int sum;
        public Pair(int i1, int i2, int sum) {
            this.i1 = i1;
            this.i2 = i2;
            this.sum = sum;
        }
        public int compareTo(Pair p) {
            return this.sum - p.sum;
        }
    }
    public List<int[]> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        int[] index = new int[nums1.length];
        List<int[]> result = new LinkedList<int[]>();
        if (nums1.length == 0 || nums2.length == 0) {
            return result;
        }
        PriorityQueue<Pair> q = new PriorityQueue<Pair>();
        for (int i = 0; i < nums1.length; i ++) {
            q.add(new Pair(i, 0, nums1[i] + nums2[0]));
            index[i] ++;
        }
        while (k > 0 && !q.isEmpty()) {
            Pair p = q.poll();
            result.add(new int[]{nums1[p.i1], nums2[p.i2]});
            k --;
            if (index[p.i1] < nums2.length) {
                q.add(new Pair(p.i1, index[p.i1], nums1[p.i1] + nums2[index[p.i1]]));
                index[p.i1] ++;
            }
        }
        return result;
    }
}
```
