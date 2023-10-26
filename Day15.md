# BackTracking (3)
## combination sum
39.https://leetcode.cn/problems/combination-sum/

key: no sum-=element after backtracking

```
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);
        List<Integer> path = new ArrayList<>();
        int startIdx = 0;
        int sum = 0;
        backtrack(result, candidates,path, target, startIdx, sum);

        return result;
    }
    public void backtrack (List<List<Integer>> result, int [] candidates, List<Integer> path, int target, int startIdx, int sum){
        if (sum == target) {
            result.add(new ArrayList<>(path));
            return;
        }
        for (int i = startIdx; i < candidates.length; i++) {
            //pruning
            if (sum + candidates[i] > target) break;
            path.add(candidates[i]);
            
            backtrack(result, candidates, path, target, i, sum+candidates[i]);
            path.remove(path.size()-1);
        }
    }
}
```

