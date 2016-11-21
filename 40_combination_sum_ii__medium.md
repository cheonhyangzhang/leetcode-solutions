# 40 Combination Sum II – Medium


### Problem:



Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:

All numbers (including target) will be positive integers.
Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
The solution set must not contain duplicate combinations.
For example, given candidate set 10,1,2,7,6,1,5 and target 8,
A solution set is:
[1, 7]
[1, 2, 5]
[2, 6]
[1, 1, 6]


### Thoughts:



This is similar to the I version of the problem. Only difference is that the element in the collection can only be used once.

The index passed in is different and need to check num[i] == num[i-1] .

if (i == j || candidates[i] != candidates[i-1]) then continue to go deeper down.


### Solutions:



```java
public class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(candidates == null || candidates.length == 0) return result;
        ArrayList<Integer> current = new ArrayList<Integer>();
        Arrays.sort(candidates);
        combinationSum(candidates, target, 0, current, result);
        return result;
    }
    public void combinationSum(int[] candidates, int target, int j, ArrayList<Integer> curr, List<List<Integer>> result){
        if(target == 0){
            ArrayList<Integer> temp = new ArrayList<Integer>(curr);
            result.add(temp);
            return;
        }
        for(int i=j; i<candidates.length; i++){
            if (target < candidates[i]){
                return;
            }
            if (i == j || candidates[i] != candidates[i-1]){
                curr.add(candidates[i]);
                combinationSum(candidates, target - candidates[i], i + 1, curr, result);
                curr.remove(curr.size()-1);
            }
        }//for i
    }//combinationSum
}//Solution
```