# Day01 Array part1
## (1) Binary search
Problem (704): https://leetcode.cn/problems/binary-search/

Solution: https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html

Key: [x, y]

```
class Solution {
    public int search(int[] nums, int target) {
        //prevent 
        if (target < nums[0] || target > nums[nums.length - 1]) {
            return -1;
        }
        int left = 0;
        int right = nums.length-1;
        while(left<=right) {
            int mid = (left+right) / 2;
            if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] < target) {
                left = mid + 1;
            } else if (nums[mid] == target) {
                return mid;
            }
        }

        return -1;
    }
}
```
***
## (2) Elements removal
Problem (27):  https://leetcode.cn/problems/remove-element/

Solution: https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html

Key: Double Pointer (fast pointer and slow pointer work together, one loop as two loops)

* Fast Pointer: search for elements of new array (array without target)
* Slow Pointer: point to the new array index

1. fast and slow pointer
```
class Solution {
    public int removeElement(int[] nums, int val) {
        int slowIndex = 0;
        //快指针：寻找新数组的元素 ，新数组就是不含有目标元素的数组
        //慢指针：指向更新 新数组下标的位置
        for (int fastIndex = 0; fastIndex<nums.length; fastIndex++) {
            if (val != nums[fastIndex]) {
                nums[slowIndex] = nums[fastIndex];
                slowIndex++;
            }
        }

        return slowIndex;
    }
}
```

2. 相向指针
```
class Solution {
    public int removeElement(int[] nums, int val) {
        //相向双指针
        int left = 0;
        int right = nums.length -1;
        while (left <= right) {
            while (left<=right && nums[left]!=val) {
                left++;
            }
            while (left<=right && nums[right]==val) {
                right--;
            }
            if (left<right) {
                nums[left]=nums[right];
                left++;
                right--;
            }
        }
        return left;
    }
}
```