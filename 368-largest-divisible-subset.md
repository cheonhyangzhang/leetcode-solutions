# 368 Largest Divisible Subset

### Problem:

Given a set of distinct positive integers, find the largest subset such that every pair (Si, Sj) of elements in this subset satisfies: Si % Sj = 0 or Sj % Si = 0.

If there are multiple solutions, return any subset is fine.

Example 1:

```
nums: [1,2,3]

Result: [1,2] (of course, [1,3] will also be ok)
```
Example 2:

```
nums: [1,2,4,8]

Result: [1,2,4,8]
```

### Solutions:

```java
public class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new LinkedList<Integer>();
        }
        int[] dp = new int[nums.length];
        int[] index = new int[nums.length];
        dp[0] = 1;
        index[0] = -1;
        Arrays.sort(nums);
        int max = 0;
        int start = 0;
        for (int i = 1; i < nums.length; i ++) {
            index[i] = -1;
            dp[i] = 1;
            for (int j = 0; j < i; j ++) {
                if (nums[i] % nums[j] == 0 && dp[j] + 1 > dp[i]) {
                    dp[i] = dp[j] + 1;
                    index[i] = j;
                }
            }
            if (dp[i] > max) {
                max = dp[i];
                start = i;
            }
        }
        int i = start;
        List<Integer> result = new LinkedList<Integer>();
        while (i != -1) {
            result.add(0, nums[i]);
            i = index[i];
        }
        return result;
    }
}
```

Can be resolved in DFS as well

```java
public class Solution {
    List<Integer> answer;
    public List<Integer> largestDivisibleSubset(int[] nums) {
        if(nums==null || nums.length==0)
            return new ArrayList<Integer>();
 
        Arrays.sort(nums);
 
        int[] max = new int[1];
        List<Integer> result = new ArrayList<Integer>();
        helper(nums, 0, result, max);
        return answer;
    }
 
    public void helper(int[] nums, int start, List<Integer> result, int[] max){
        if(result.size()>max[0]){
            max[0]=result.size();
            answer=new ArrayList<Integer>(result);
        }
 
        if(start==nums.length)
            return;
 
        for(int i=start; i<nums.length; i++){
            if(result.size()==0){
                result.add(nums[i]);
                helper(nums, i+1, result, max);
                result.remove(result.size()-1);
 
            }else{
 
                int top = result.get(result.size()-1);
                if(nums[i]%top==0){
                    result.add(nums[i]);
                    helper(nums, i+1, result, max);
                    result.remove(result.size()-1);
                }
            }
        }
    }
}
```