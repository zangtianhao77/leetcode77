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