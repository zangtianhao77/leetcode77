# 238. Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self/description/

```
//method2 time limit:O(n)

class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[]tempLeft = new int[nums.length];
        int[]tempRight = new int[nums.length];
        int[] res = new int[nums.length];

        int product1=1;
        int product2=1;

        for (int i = 0; i<nums.length; i++) {
            product1*=nums[i];
            tempLeft[i] = product1;
        }
        for (int j=nums.length-1; j>=0;j--) {
            product2*=nums[j];
            tempRight[j] = product2;
        }
        res[0] = tempRight[1];
        res[nums.length-1] = tempLeft[nums.length-2];
        for (int k=1; k<nums.length-1; k++) {
            res[k] = tempLeft[k-1] * tempRight[k+1];
        }

        return res;
    }
}
```

key:
1.tempLeft[i] is the product of prefix elements before nums[i]
2.tempRight[i] is the product of postfix elements after nums[i]