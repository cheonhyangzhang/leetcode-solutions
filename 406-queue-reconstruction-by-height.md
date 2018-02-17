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

```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        if (people.length == 0 || people[0].length == 0) {
            return people;
        }
        int[][] res = new int[people.length][people[0].length];
        boolean[] filled = new boolean[people.length];
        Arrays.sort(people, new Comparator<int[]>(){
           public int compare(int[] p1, int[] p2) {
               if (p1[0] == p2[0]) {
                   return p2[1] - p1[1];
               }
               else {
                   return p1[0] - p2[0];
               }
           } 
        });
        for (int i = 0; i < people.length; i ++) {
            int[] p = people[i];
            int count = 0;
            for (int j = 0; j < people.length; j ++) {
                if (filled[j] == false) {
                    count ++;
                    if (count == p[1] + 1) {
                        filled[j] = true;
                        res[j][0] = p[0];
                        res[j][1] = p[1];
                        break;
                    }
                }
            }
        }
        return res;
    }
}
```