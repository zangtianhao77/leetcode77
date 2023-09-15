# BinaryTree <6>
## (1) N-nary preorder search
589.https://leetcode.cn/problems/n-ary-tree-preorder-traversal/

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
    
    public List<Integer> preorder(Node root) {
        List<Integer> result = new ArrayList<>();
        //recursion
        func(root, result);

        return result;
    }

    public void func(Node root, List<Integer> resList) {
        if (root == null) return;
        resList.add(root.val);
        for (int i = 0; i < root.children.size(); i++) {
            func(root.children.get(i), resList);
        }
    }
}
```

## (2) N-nary postorder search
590.https://leetcode.cn/problems/n-ary-tree-postorder-traversal/

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
    public List<Integer> postorder(Node root) {
        List<Integer> result = new ArrayList<>();
        //recursion
        func(root, result);

        return result;
    }

    public void func(Node root, List<Integer> resList) {
        if (root == null) return;
        
        for (int i = 0; i < root.children.size(); i++) {
            func(root.children.get(i), resList);
        }
        resList.add(root.val);
    }
}
```

## (3) symmertic binary tree
101.https://leetcode.cn/problems/symmetric-tree/

key:
1.recursion param (1) root.left (2) root.right
2.recursion end conditions -> 4 related null nodes
3.single level -> inside && outside
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
    public boolean isSymmetric(TreeNode root) {
        return compare (root.left, root.right);
    }

    public boolean compare (TreeNode left, TreeNode right) {
        if (left == null && right == null) return true;
        if (left == null && right != null) return false;
        if (left != null && right == null) return false;
        if (left.val != right.val) {
            return false;
        }
        boolean compareOutside = compare(left.left, right.right);
        boolean compareInside = compare(left.right, right.left);

        return compareOutside && compareInside;
    }
}
```