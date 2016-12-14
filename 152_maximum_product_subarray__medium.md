# 152 Maximum Product Subarray – Medium


### Problem:



Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.


### Thoughts:



The tricky part of this problem is : the array may contain 0 and negative numbers.

To make solution simple, the trick is to use two current max value, one for positive and one for negative. The negative one is actually min value of the product.

When comparing, don’t forget to consider the ith element itself.


### Solutions:



```java
public class Solution {
    public int maxProduct(int[] nums) {
        if(nums==null||nums.length==0)
            return 0;
        int maxProduct = nums[0];
        int max_temp = nums[0];
        int min_temp = nums[0];
        for(int i=1;i<nums.length;i++) {
            int a = nums[i]*max_temp;
            int b = nums[i]*min_temp;
            max_temp = Math.max(Math.max(a,b), nums[i]);
            min_temp = Math.min(Math.min(a,b), nums[i]);
            maxProduct = Math.max(maxProduct, max_temp);
        }
        return maxProduct;
    }
}
```