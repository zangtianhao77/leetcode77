# BackTracking <1>
## (1) combine problems

77.https://leetcode.cn/problems/combinations/

Key of backtracking:
```
void backtracking(参数) {
    if (终止条件) {
        存放结果;
        return;
    }

    for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
        处理节点;
        backtracking(路径，选择列表); // 递归
        回溯，撤销处理结果
    }
}
```

```
//backtracking
class Solution {
    List<List<Integer>> result= new ArrayList<>(); // result of k-element lists combination
    LinkedList<Integer> path = new LinkedList<>(); // one list containing k elements    
    public List<List<Integer>> combine(int n, int k) {
        backtracking(n , k, 1); //1 is start idx
        return result;

    }

    public void backtracking(int n, int k, int startIdx) {
        //end condition
        if (path.size()==k) {
            result.add(new ArrayList<>(path));
            return;
        }
        //start back track by looping
        for (int i = startIdx; i <=n; i++) {
            path.add(i); //add to path to combine result
            backtracking(n, k, i+1); //start recursion
            path.removeLast(); //cancel this operation to restore, backtracking
        }

    }
}
```

## (2) backtracking with pruning

key: i <=n - (k - path.size()) + 1

```
//backtracking
class Solution {
    List<List<Integer>> result= new ArrayList<>(); // result of k-element lists combination
    LinkedList<Integer> path = new LinkedList<>(); // one list containing k elements    
    public List<List<Integer>> combine(int n, int k) {
        backtracking(n , k, 1); //1 is start idx
        return result;

    }

    public void backtracking(int n, int k, int startIdx) {
        //end condition
        if (path.size()==k) {
            result.add(new ArrayList<>(path));
            return;
        }
        //start back track by looping
        for (int i = startIdx; i <=n - (k - path.size()) + 1; i++) {
            path.add(i); //add to path to combine result
            backtracking(n, k, i+1); //start recursion for backtracking
            path.removeLast(); //cancel this operation to restore
        }

    }
}
```
