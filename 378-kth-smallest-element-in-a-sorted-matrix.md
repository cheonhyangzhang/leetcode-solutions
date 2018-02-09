# 378 Kth Smallest Element in a Sorted Matrix

Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

Example:
```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

Note: 
You may assume k is always valid, 1 ≤ k ≤ n^2.

### Solutions:

```java
public class Solution {
    private class Entry implements Comparable<Entry> {
        private int val;
        private int i;
        private int j;
        public Entry(int val, int i, int j) {
            this.val = val;
            this.i = i;
            this.j = j;
        }
        public int compareTo(Entry e) {
            return this.val - e.val;
        }
    }
    public int kthSmallest(int[][] matrix, int k) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        HashSet<String> visited = new HashSet<String>();
        int m = matrix.length, n = matrix[0].length;
        PriorityQueue<Entry> q = new PriorityQueue<Entry>();
        q.add(new Entry(matrix[0][0], 0, 0));
        visited.add("0,0");
        while (k > 1) {
            Entry cand = q.poll();
            if (cand.i + 1 < m && !visited.contains((cand.i + 1) + "," + cand.j)) {
                q.add(new Entry(matrix[cand.i + 1][cand.j], cand.i + 1, cand.j));
                visited.add((cand.i + 1) + "," + cand.j);
            }
            if (cand.j + 1 < n && !visited.contains(cand.i + "," + (cand.j + 1))) {
                q.add(new Entry(matrix[cand.i][cand.j + 1], cand.i, cand.j + 1));
                visited.add(cand.i + "," + (cand.j + 1));
            }
            k --;
        }
        return q.poll().val;
    }
}
```

```java
public class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n=matrix.length;
        int lower = matrix[0][0];
        int upper = matrix[n-1][n-1];
        while(lower < upper){
            int mid = lower + (upper-lower) / 2;
            int count = count(matrix, mid);
            if(count<k){
                lower = mid+1;
            }else{
                upper = mid;
            }
        }
     
        return upper;
    }
     
    private int count(int[][] matrix, int target){
        int n = matrix.length;
        int i = m-1;
        int j = 0;
        int count = 0;
     
        while(i >= 0 && j < n){
            if(matrix[i][j] <= target){
                count += i+1;
                j++;
            }else{
                i--;
            }
        }
        return count;
    }
}
```