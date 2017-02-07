# 406 Queue Reconstruction by Height

### Problem:

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers (h, k), where h is the height of the person and k is the number of people in front of this person who have a height greater than or equal to h. Write an algorithm to reconstruct the queue.

Note:
The number of people is less than 1,100.

Example
```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

### Solutions:

```java
public class Solution {
    private class People implements Comparable<People> {
        private int h;
        private int k;
        public People(int h, int k) {
            this.h = h;
            this.k = k;
        }
        public int compareTo(People p) {
            return this.h - p.h;
        }
    }
    public int[][] reconstructQueue(int[][] people) {
        int[][] result = new int[people.length][2];
        PriorityQueue<People> q = new PriorityQueue<People>();
        for (int i = 0; i < people.length; i ++) {
            q.add(new People(people[i][0], people[i][1]));
        }
        boolean[] filled = new boolean[result.length];
        while (!q.isEmpty()) {
            People p = q.poll();
            int i = 0;
            int k = p.k;
            while (i < result.length) {
                if (filled[i] == true) {
                    if (result[i][0] >= p.h) {
                        k --;
                    }
                    i ++;
                    continue;
                }
                else {
                    if (k == 0) {
                        result[i][0] = p.h;
                        result[i][1] = p.k;
                        filled[i] = true;
                        break;
                    }
                    else {
                        k --;
                        i ++;
                        continue;
                    }
                }
            }
        }
        return result;
    }
}
```

```java
public class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                if (o1[0] == o2[0]) {
                    return o1[1] - o2[1];
                } else {
                    return o2[0] - o1[0];
                }
            }
        }));
        List<int[]> resultList = new LinkedList<>();
        for(int[] cur : people){
            resultList.add(cur[1], cur);
        }
        return resultList.toArray(new int[people.length][]);
    }
}
```

```
public class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                if (o1[0] == o2[0]) {
                    return o1[1] - o2[1];
                } else {
                    return o2[0] - o1[0];
                }
            }
        }));
        for (int i = 1; i < people.length; ++i) {
            int cnt = 0;
            for (int j = 0; j < i; ++j) {
                if (cnt == people[i][1]) {
                    int[] t = people[i];
                    for (int k = i - 1; k >= j; --k) {
                        people[k + 1] = people[k];
                    }
                    people[j] = t;
                    break;
                }
                if (people[j][0] >= people[i][0]) 
                    ++cnt;
            }
        }
        return people;
    }
}
```