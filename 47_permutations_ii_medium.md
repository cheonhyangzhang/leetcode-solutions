# 47  Permutations II – Medium


### Problem:



Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
[1,1,2] have the following unique permutations:
[1,1,2], [1,2,1], and [2,1,1].


### Thoughts:



This is similar to Permutations, the only difference is that the collection might contain duplicates.

So the modification is to avoid duplicate solution.

So the add condition is that for any duplicate elements, you only want to add it if the previous one ( duplicate) is added.

Say for 0 1 1, for the second 1, only insert it if the previous 1 is inserted so that we could avoid have two 0 1 1 permutation and 0 1 1 permutation.


### Solutions:



```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] num) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        Arrays.sort(num);
        Boolean[] visited = new Boolean[num.length];
        for (int i = 0; i < visited.length; i ++){
            visited[i] = false;
        }
        DFS(num, 0, result, new LinkedList<Integer>(), visited);
        return result;
     }
    private void DFS(int[] num, int togo, List<List<Integer>> result, List<Integer> current, Boolean[] visited ){
        if (togo == visited.length){
            result.add(new LinkedList(current));
        }
        else{
            for (int i = 0; i < num.length; i ++){ 
                if (visited[i] == false){ 
                    if (i > 0 && num[i] == num[i-1] && visited[i-1] == false){
                        continue;//only insert duplicate element when the previous duplicate element has been inserted
                    }
                    current.add(num[i]);
                    visited[i] = true;
                    DFS(num, togo + 1, result, current, visited);
                    current.remove(current.size() - 1);
                    visited[i] = false;
                }
            }//for i
        }//else
    }//
}
```
Alternative version:

```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        boolean[] visited = new boolean[nums.length];
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        List<Integer> tmp = new LinkedList<Integer>();
        process(nums, visited, result, tmp);
        return result;
    }
    private void process(int[] nums, boolean[] visited, List<List<Integer>> result, List<Integer> curr) {
        if (curr.size() == nums.length) {
            result.add(new LinkedList<Integer>(curr));
            return;
        }
        for (int i = 0; i < nums.length; i ++) {
            if (visited[i] == false) {
                visited[i] = true;
                curr.add(nums[i]);
                process(nums, visited, result, curr);
                visited[i] = false;
                curr.remove(curr.size() -1);
                int tmp = nums[i];
                i ++;
                while (i < nums.length && nums[i] == tmp) {
                    i ++;
                }
                i --;
            }
        }
    }
}
```

```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        boolean[] visited = new boolean[nums.length];
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        List<Integer> tmp = new LinkedList<Integer>();
        process(nums, visited, result, tmp);
        return result;
    }
    private void process(int[] nums, boolean[] visited, List<List<Integer>> result, List<Integer> curr) {
        if (curr.size() == nums.length) {
            result.add(new LinkedList<Integer>(curr));
            return;
        }
        for (int i = 0; i < nums.length; i ++) {
            if (visited[i] == true || ( i > 0 && nums[i] == nums[i - 1] && visited[i - 1] == false)) {
                continue;
            }
            visited[i] = true;
            curr.add(nums[i]);
            process(nums, visited, result, curr);
            visited[i] = false;
            curr.remove(curr.size() -1); 
        }
    }
}
```