# BackTracking <1>
## (1)combinationSum III

216.https://leetcode.cn/problems/combination-sum-iii/


key: 
1.pruning
 if (sum > targetSum) return;

2.终止条件里需要判断sum
3.sum也需要backtracking（即for做过的操作都需要backtracking）


```
class Solution {
    List<List<Integer>> result= new ArrayList<>();
    LinkedList<Integer> path = new LinkedList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        //k is number of elements, n is targetSum, 0 is sum, 1 is startIdx
        backtracking(n, k, 1, 0);
        return result;
    }
    public void backtracking (int targetSum, int k, int startIndex, int sum) {
        //pruning
        if (sum > targetSum) {
            return;
        }

        if (path.size() == k) {
			if (sum == targetSum) result.add(new ArrayList<>(path));
			return;
		}
        for (int i = startIndex; i < 9-(k-path.size())+1; i++) {
            path.add(i);
            sum += i;
            backtracking(targetSum, k, i + 1, sum);
            path.removeLast();//backtracking
            sum-=i;//backtracking
        }
    }
}
```

## (2)letterCombinations

17.https://leetcode.cn/problems/letter-combinations-of-a-phone-number/

```
class Solution {
    List<String> list = new ArrayList<>();
    public List<String> letterCombinations(String digits) {
        if (digits == null || digits.length() == 0) {
            return list;
        }
        String[] numString = ["", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"];
         backTracking(digits, numString, 0);
         return list;
    }

    StringBuilder temp = new StringBuilder();
    public void backTracking(String digits, String[] numString; int num) {
        if (num == digits.length()) {
            list.add(temp.toString());
            return;
        }
        String str = numString[digits.charAt(num) - '0']; //str is string corresponding to the current num
        for (int i = num; i < str.length(); i++) {
            temp.append(str.charAt(i));
            backTracking(digits, numString, num+1);
            temp.deleteCharAt(temp.length()-1);
        }
    }
}
```