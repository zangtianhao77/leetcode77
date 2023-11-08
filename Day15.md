# BackTracking (3)
## combination sum
39.https://leetcode.cn/problems/combination-sum/

key: no sum-=element after backtracking
如果是一个集合来求组合的话，就需要startIndex，例如：77.组合 (opens new window)，216.组合总和III (opens new window)。

如果是多个集合取组合，各个集合之间相互不影响，那么就不用startIndex，例如：17.电话号码的字母组合

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


## (2) combination sum 3

40.https://leetcode.cn/problems/combination-sum-ii/

key: 去重->为什么 used[i - 1] == false 就是同一树层呢，因为同一树层，used[i - 1] == false 才能表示，当前取的 candidates[i] 是从 candidates[i - 1] 回溯而来的

```
class Solution {
    LinkedList<Integer> path = new LinkedList<>();
    List<List<Integer>> ans = new ArrayList<>();
    boolean[] used;
    int sum = 0;
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {

        used = new boolean[candidates.length];
        Arrays.fill(used, false);
        //方便去重
        Arrays.sort(candidates);
        backTracking(candidates, target, 0);
        return ans;
    }

    public void backTracking(int[]candidates, int target, int startIndex) {
        if (sum == target) {
            ans.add(new ArrayList(path));
        }
        for (int i = startIndex; i < candidates.length; i++) {
            if (sum + candidates[i] > target) {
                break;
            }
            //方便去重
            //可能有的录友想，为什么 used[i - 1] == false 就是同一树层呢，因为同一树层，used[i - 1] == false 才能表示，当前取的 candidates[i] 是从 candidates[i - 1] 回溯而来的。
            if (i > 0 && candidates[i] == candidates[i-1] && !used[i-1]) {
                continue;
            }
            used[i] = true;
            sum+=candidates[i];
            path.add(candidates[i]);
            backTracking(candidates, target, i+1);
            used[i] = false;
            sum-=candidates[i];
            path.removeLast();
        }
    }
}
```

