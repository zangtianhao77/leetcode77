# BinaryTree <3>
## (1) level order search
102.https://leetcode.cn/problems/binary-tree-level-order-traversal/description/

Key: 
1. recursion
2. ensure when to add a new element to the return list

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();

    public List<List<Integer>> levelOrder(TreeNode root) {

        
        checkFunc01(root, 0);

        return resList;
    }

    //DFS
    public void checkFunc01(TreeNode node, Integer deep) {
        if (node == null) {
            return;
        }
        deep++;
        //为了让right node被添加进list时，不会再多加一个list element
        if (resList.size() < deep) {
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);
        checkFunc01(node.left, deep);
        checkFunc01(node.right, deep);
    }
}
```

## (2) level order search II
107.https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/submissions/

key: reverse of 102

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

    public List<List<Integer>> resList = new ArrayList<List<Integer>>();

    public List<List<Integer>> levelOrderBottom(TreeNode root) {

        
        checkFunc01(root, 0);

        Collections.reverse(resList);
        return resList;
    }

    //DFS
    public void checkFunc01(TreeNode node, Integer deep) {
        if (node == null) {
            return;
        }
        deep++;
        //为了让right node被添加进list时，不会再多加一个list element
        if (resList.size() < deep) {
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);
        checkFunc01(node.left, deep);
        checkFunc01(node.right, deep);
    }
}
```

## (3) level order right view
199.https://leetcode.cn/problems/binary-tree-right-side-view/description/


```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();
    public List<Integer> rightSideView(TreeNode root) {
        resFunc01(root, 0);
        List<Integer> result = new ArrayList<>();

        for (int i = 0; i < resList.size(); i++) {
            List<Integer> temp = new ArrayList<>();
            temp = resList.get(i);
            result.add(temp.get(temp.size()-1));
        }
        return result;
    }

    public void resFunc01(TreeNode node, Integer deep) {
        if (node == null) {
            return;
        }
        deep++;

        if (resList.size() < deep) {
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);
        resFunc01(node.left, deep);
        resFunc01(node.right, deep);
    }
}
```

## (4) level order avg

637.https://leetcode.cn/problems/average-of-levels-in-binary-tree/


```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();

    public List<Double> averageOfLevels(TreeNode root) {
        resFunc(root, 0);
        List<Double> result = new ArrayList<>();

        for (int i=0; i < resList.size(); i++) {
            List<Integer> temp = new ArrayList<>();
            temp = resList.get(i);
            Double sum = 0.0;
            for (int j=0; j < temp.size(); j++) {
                sum += temp.get(j);
            }
            sum /= temp.size();
            result.add(sum);
        }
        return result;
    }

    public void resFunc(TreeNode node, Integer deep) {
        if (node == null) {
            return;
        }
        deep++;

        if (resList.size() < deep) {
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);
        resFunc(node.left, deep);
        resFunc(node.right, deep);
    }
}
```

## (5) N-nary tree level order search
429.https://leetcode.cn/problems/n-ary-tree-level-order-traversal/description/



```
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();
    public List<List<Integer>> levelOrder(Node root) {
        checkFunc01(root, 0);

        return resList;
    }

    //DFS
    public void checkFunc01(Node node, Integer deep) {
        if (node == null) {
            return;
        }
        deep++;
        //为了让right node被添加进list时，不会再多加一个list element
        if (resList.size() < deep) {
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);
        for (int i = 0; i < node.children.size(); i++) {
            checkFunc01(node.children.get(i), deep);
        }
    }
}
```

## (6) level order max val

515.https://leetcode.cn/problems/find-largest-value-in-each-tree-row/description/

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> resList = new ArrayList<List<Integer>>();
    public List<Integer> largestValues(TreeNode root) {
        resFunc01(root, 0);
        List<Integer> result = new ArrayList<>();

        for (int i=0; i < resList.size(); i++) {
            List<Integer> temp = new ArrayList<>();
            temp = resList.get(i);
            Integer maxNode = temp.get(0);
            for (int j=0; j < temp.size(); j++) {
                if (temp.get(j) > maxNode) {
                    maxNode = temp.get(j);
                }
            }
            result.add(maxNode);
        }
        return result;
    }

    public void resFunc01(TreeNode node, Integer deep) {
        if (node == null) {
            return;
        }
        deep++;

        if (resList.size() < deep) {
            List<Integer> item = new ArrayList<Integer>();
            resList.add(item);
        }
        resList.get(deep - 1).add(node.val);
        resFunc01(node.left, deep);
        resFunc01(node.right, deep);
    }
}
```