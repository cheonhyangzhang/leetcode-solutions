# 96Unique Binary Search Trees – Medium


### Problem:



Given n, how many structurally unique BST’s (binary search trees) that store values 1…n?

For example,
Given n = 3, there are a total of 5 unique BST’s.

```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

### Thoughts:



Define nums[i] is the number of unique BST’s for given n = i.

Base case is nums[0] = nums[1] = 1

nums[i] = SUM of (nums[j] + nums[ i – j + 1]) while 0 <= j < i.

j is the number of elements in left subtree.


### Solutions:

```java
public class Solution {
    public int numTrees(int n) {
        int[] ways = new int[n+1];
        ways[0] = 1;
        for (int i = 1; i <=n; i ++) {
            int sum = 0;
            for (int j = 1; j <=i; j ++) {
                //use num[i] as the root of binary tree
                sum += ways[j - 1]* ways[i - j];
            }
            ways[i] = sum;
        }
        return ways[n];
    }
}
```
