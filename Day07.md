# BinaryTree <1>
## (1) preorder traversal using recursion\

144.https://leetcode.cn/problems/binary-tree-preorder-traversal/

Key of Recursion:
1. 确定递归函数的参数和返回值
public void preorder(TreeNode root, List<Integer> result)
1. 确定终止条件
if (root==null)
1. 确定单层递归的逻辑
result.add(root.val);
preorder(root.left, result);
preorder(root.right, result);

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        preorder(root, result);
        return result;
    }

    public void preorder(TreeNode root, List<Integer> result) {
        if (root==null) {
            return;
        }

        result.add(root.val);
        preorder(root.left, result);
        preorder(root.right, result);
    }
}
```

## (2) postorder traversal using recursion
145.https://leetcode.cn/problems/binary-tree-postorder-traversal/
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        postorder(root, result);
        return result;
    }
    void postorder(TreeNode root, List<Integer> result) {
        if (root==null) {
            return;
        }
        
        postorder(root.left, result);
        postorder(root.right, result);
        result.add(root.val);
    }
}
```

## (3) inorder traversal using recursion
94.https://leetcode.cn/problems/binary-tree-inorder-traversal/

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        inorder(root, result);
        return result;
    }
    void inorder(TreeNode root, List<Integer> result) {
        if (root==null) {
            return;
        }
        
        inorder(root.left, result);
        result.add(root.val);
        inorder(root.right, result);

    }
}
```