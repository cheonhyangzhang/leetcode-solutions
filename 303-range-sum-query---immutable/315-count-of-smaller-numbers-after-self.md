# 315 Count of Smaller Numbers After Self

### Problem:
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

Example:
```
Given nums = [5, 2, 6, 1]

To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

Return the array [2, 1, 1, 0].

### Solutions:

Binary search insert

```java
public class Solution {
    public List<Integer> countSmaller(int[] nums) {
        List<Integer> result = new LinkedList<Integer>();
        ArrayList<Integer> cand = new ArrayList<Integer>();
        for (int i = nums.length - 1; i >= 0; i --) {
            int left = 0, right = cand.size();
            while(left < right) {
                int mid = (right - left) / 2 + left;
                if (cand.get(mid) < nums[i]) {
                    left = mid + 1;
                }
                else {
                    right = mid;
                }
            }
            result.add(0, right);
            cand.add(right, nums[i]);
        }
        return result;
    }
}
```
Binary Search Tree
```java
public class Solution {
    private class Node {
        public int val;
        public int cnt;
        public int leftSum;
        public Node left;
        public Node right;
        public Node(int val) {
            cnt = 1;
            leftSum = 0;
            this.val = val;
        }
    }
    public List<Integer> countSmaller(int[] nums) {
        List<Integer> res = new LinkedList<>();
        Node root = null;
        for(int i = nums.length - 1; i >= 0; i --) {
            root = helper(res, nums[i], root, 0);
        }
        return res;
    }
    private Node helper(List<Integer> res, int val, Node root, int preNum) {
        if(root == null) {
            res.add(0, preNum);
            return new Node(val);
        }
        if(root.val == val) {
            root.cnt ++;
            res.add(0, preNum + root.leftSum);
        }
        else if(root.val > val) {
            root.leftSum ++;
            root.left = helper(res, val, root.left, preNum);
        }
        else {
            root.right = helper(res, val, root.right, preNum + root.leftSum + root.cnt);
        }    
        return root;
    }
}
```

Binary Indexed tree
```java
public class Solution {
    public List<Integer> countSmaller(int[] nums) {
        int min = Integer.MAX_VALUE;
        int max = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i ++) {
            if (nums[i] < min) {
                min = nums[i];
            }
            if (nums[i] > max) {
                max = nums[i];
            }
        }
        int diff = 1 - min;
        for (int i = 0; i < nums.length; i ++) {
            nums[i] += diff;
        }
        max += diff;
        List<Integer> result = new LinkedList<Integer>();
        int[] sums = new int[max + 1];
        for (int i = nums.length - 1; i >= 0; i --) {
            result.add(0, getSum(sums, nums[i] - 1));
            update(sums, nums[i]);
        }
        return result;
    }
    private int getSum(int[] sums, int index) {
        int sum = 0;
        while (index > 0) {
            sum += sums[index];
            index -= index & (-index);
        }
        return sum;
    }
    private void update(int[] sums, int val) {
        while (val < sums.length) {
            sums[val] += 1;
            val += val&(-val);
        };
    }
}
```
