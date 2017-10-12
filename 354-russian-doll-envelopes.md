# 354 Russian Doll Envelopes

### Problem:
You have a number of envelopes with widths and heights given as a pair of integers (w, h). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? (put one inside other)

Example:
Given envelopes = [[5,4],[6,4],[6,7],[2,3]], the maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).

### Solutions:

```java
public class Solution {
    private class Pair implements Comparable<Pair>{
        public int w;
        public int h;
        public Pair(int w, int h) {
            this.w = w;
            this.h = h;
        }
        public int compareTo(Pair p) {
            if (this.w != p.w) {
                return this.w - p.w;
            }
            return p.h - this.h;
        }
    }
    public int maxEnvelopes(int[][] envelopes) {
        ArrayList<Pair> data = new ArrayList<Pair>();
        for (int i = 0; i < envelopes.length; i ++) {
            Pair p = new Pair(envelopes[i][0], envelopes[i][1]);
            data.add(p);
        }
        Collections.sort(data);
        ArrayList<Integer> sorted = new ArrayList<Integer>();
        for (int i = 0; i < data.size(); i ++) {
            if (sorted.size() == 0 || data.get(i).h > sorted.get(sorted.size() - 1)) {
                sorted.add(data.get(i).h);
                continue;
            }
            int left = 0, right = sorted.size() - 1;
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (sorted.get(mid) < data.get(i).h) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }
            sorted.set(right + 1, data.get(i).h);
        }
        return sorted.size();
    }
}
```