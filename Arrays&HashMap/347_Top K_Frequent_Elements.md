# 347. Top K Frequent Elements
https://leetcode.com/problems/top-k-frequent-elements/description/

```
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int x : nums) {
            if (!map.containsKey(x)) {
                map.put(x,1);
            } else {
                map.put(x,map.get(x)+1);
            }
        }
        ArrayList<Integer> list = new ArrayList<>();
        List<Integer> resList = new ArrayList<>(map.keySet());
        int res[] = new int[k];
        resList.sort((a, b) -> map.get(b) - map.get(a));
        for (int i = 0; i<k; ++i) {
            res[i] = resList.get(i);

        }
        return res;
    }
}
```



key:
```
List<Integer> resList = new ArrayList<>(map.keySet());
resList.sort((a, b) -> map.get(b) - map.get(a)); //descending order
```
resList could be a list with the key elements in map. We can sort the list based on the value set in map (ex.frequencies of a element)
