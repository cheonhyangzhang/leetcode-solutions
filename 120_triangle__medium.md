# 120 Triangle – Medium


### Problem:



Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.


### Thoughts:



This is a very typical dynamic programming problem. Each element has two choice at most. Always pick the least one.

About the O(n) space, it’s similar to Pascal’s Triangle II. Use a rolling one-dimension array to achieve. Calculate new row values from right to left.

Now here is another trick. If we do the calculation from top to bottom, checking for boundary might become a headache for us. In order to get ride of that, we could do this reversely, bottom to top.


### Solutions:



```java
public class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        for (int i = triangle.size() - 1; i >= 0; i --){
            List<Integer> row = triangle.get(i);
            for (int j = 0; j < row.size(); j ++){
                if (i == triangle.size() - 1){
                    res.add(row.get(j));
                }
                else{
                    res.set(j, Math.min(res.get(j),res.get(j+1)) + row.get(j));
                }
            }
        }
        return res.get(0);
    }
}
```