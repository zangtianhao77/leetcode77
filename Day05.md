# HashSet <1>
## (1) Happy Number
202: https://leetcode.cn/problems/happy-number/description/

Solution: https://www.programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html#%E6%80%9D%E8%B7%AF

Key: 
1. when it comes to check if an element appears repeatedly, we will use hashset to check how many times it appear
2. Set<Integer> x = new HashSet<>()
3. 2methods about set x.contains(n) // x.add(n)
4. x % 10 to get the last digit

```
class Solution {
    //when it comes to check if an element appears repeatedly, we will use hashset
    public boolean isHappy(int n) {
        Set<Integer> record = new HashSet<>();
        while (n!=1 && !record.contains(n)) {
            record.add(n);
            //get the next sum of all digits
            int sum = 0;
            while (n > 0) {
                int digit = n % 10;
                sum += digit*digit;
                n/=10;
            }
            n = sum;

        }
        return n ==1;

    }
}
```

## (2) Sum of Four II
454: https://leetcode.cn/problems/4sum-ii/description/

Solution: https://www.programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html#%E6%80%9D%E8%B7%AF

Key: 
1. double loop to get the sum of the first two array element combinations
2. double loop the third and fourth to check if 4 sum equal 0 exists
3. Map<Integer, Integer> map = new HashMap<Integer, Integer>();
4. map.put(key, value) // n = map.getOrDefault(key, value v) -> if key exists return its original value of key or returns value v

```
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        //res is the times of sum equal to 0 exists
        int res = 0;
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i : nums1) {
            for (int j : nums2) {
                int sum = i+j;
            //if sum exists, then sum++. if sum does not exist, default is 0 and 1+0 =1
                map.put(sum ,map.getOrDefault(sum, 0) + 1);
            }
        }

        for (int i : nums3) {
            for (int j : nums4) {
                res += map.getOrDefault(0-i-j, 0);
            }
        }
        return res;
    }
}
```
   