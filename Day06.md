# HashSet <2>
## (1) ransom
383.https://leetcode.cn/problems/ransom-note/

Solution: https://www.programmercarl.com/0383.%E8%B5%8E%E9%87%91%E4%BF%A1.html#%E6%80%9D%E8%B7%AF

Key: 
Similar to 242: https://www.programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE

```
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if (ransomNote.length() > magazine.length()) {
            return false;
        }

        int [] hashTable = new int [26];
        //use toCharArray to iterate each char
        for (char x: magazine.toCharArray()) {
            hashTable[x - 'a']++;
        }

        for (char x: ransomNote.toCharArray()) {
            hashTable[x - 'a']--;
        }
        //if there are some chars in ransomNote which are covered by magzine then there are negative numbers in hashTable
        for (int i : hashTable) {
            if (i < 0) {
                return false;
            }
        }

        return true;
    }
}
```
# Two Pointers
## (2) 4 sum
18: https://leetcode.cn/problems/4sum/description/

Solution: https://www.programmercarl.com/0018.%E5%9B%9B%E6%95%B0%E4%B9%8B%E5%92%8C.html

Key: 
1. sort the whole array to make it ordered so that we can use two pointers
2. make sure to remove duplicates

```
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
       
        for (int i = 0; i < nums.length; i++) {
		
            // nums[i] > target 直接返回, 剪枝操作
            if (nums[i] > 0 && nums[i] > target) {
                return result;
            }
		
            if (i > 0 && nums[i - 1] == nums[i]) {    // 对nums[i]去重
                continue;
            }
            
            for (int j = i + 1; j < nums.length; j++) {

                if (j > i + 1 && nums[j - 1] == nums[j]) {  // 对nums[j]去重
                    continue;
                }

                int left = j + 1;
                int right = nums.length - 1;
                while (right > left) {
		    // nums[k] + nums[i] + nums[left] + nums[right] > target int会溢出
                    long sum = (long) nums[i] + nums[j] + nums[left] + nums[right];
                    if (sum > target) {
                        right--;
                    } else if (sum < target) {
                        left++;
                    } else {
                        result.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        // 对nums[left]和nums[right]去重
                        while (right > left && nums[right] == nums[right - 1]) right--;
                        while (right > left && nums[left] == nums[left + 1]) left++;

                        left++;
                        right--;
                    }
                }
            }
        }
        return result;
    }
}
```