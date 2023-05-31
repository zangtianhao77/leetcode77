# Day02 Array part2
## (1) Squares of a Sorted Array
Problem (977): https://leetcode.cn/problems/squares-of-a-sorted-array/

Solution: https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html

Key: 
1. Two pointers, i for initial index, j for end index
2. new array to store new order array
3. compare the squires and move pointer

```
class Solution {
    public int[] sortedSquares(int[] nums) {
        //define a new result array
        int [] arr = new int [nums.length];
        //double pointer
        int left = 0;
        int right = nums.length-1;
        //index of new array
        int k = nums.length-1;
        while (left<=right) {
            if (nums[left]*nums[left] < nums[right]*nums[right]) {
                //逆序从大到小排列新数组
                arr[k] = nums[right]*nums[right];
                k--;
                //move right pointer
                right--;
            } else {
                arr[k] = nums[left]*nums[left];
                k--;
                //move left pointer
                left++;
            }
        }
        return arr;
    }
}
```
***
## (2) Minimum Size Subarray Sum
Problem (209): https://leetcode.cn/problems/minimum-size-subarray-sum/

Solution: https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html

Key: slide window to define a new array; sum of new array satisfy needs
* consecutive array--slide window

```
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        //滑动窗口 slide window
        //define left and right for dynamic array
        int l = 0;
        int sum = 0;
        //set result to max because we want it to be smaller
        int result = Integer.MAX_VALUE;
        //r is the right pointer which is the end position
        for (int r = 0; r < nums.length; r++) {
            sum+=nums[r];
            //twice in total (进出各一次)
            while (sum>=target) {
                result = Math.min(result, r-l+1);
                sum-=nums[l];
                l++;
            }
        }
        if (result == Integer.MAX_VALUE) {
            result = 0;
        }
        return result;
    }
}
```

***
## (3) Spiral Matrix II (?)
Problem (59): https://leetcode.cn/problems/spiral-matrix-ii/

Solution: https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html

Key: Intimitate the process by coding

* 模拟顺时针画矩阵的过程:

填充上行从左到右
填充右列从上到下
填充下行从右到左
填充左列从下到上
![](https://code-thinking-1253855093.file.myqcloud.com/pics/20220922102236.png)
```
class Solution {
    public int[][] generateMatrix(int n) {
        int loop = 0;//控制循环次数
        int [][] arr = new int[n][n];
        int start = 0; //每次循环开始位置
        int num = 1; //填充array的数字
        int i,j;

        while (loop++<n/2) { //判断边界后loop从1开始
            //left to right (upper level)
            for (j=start; j< n - loop; j++) {
                arr[start][j] = num;
                num++; 
            }
            //up to down (right level)
            for (i = start; i < n - loop; i++) {
                arr[i][j] = num;
                num++;
            }
            //right to left (bottom level)
            for (; j >= loop; j--) {
                arr[i][j] = num;
                num++;
            }
            //down to up (left level)
            for (; i >= loop; i--) {
                arr[i][j] = num;
                num++;
            }
            start++;
        }

        if (n % 2 == 1) {
            arr[start][start] = num;
        }

        return arr;
    }
}
```