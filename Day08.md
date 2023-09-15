# BinaryTree <2> no recursion for pre,in,post order search
## (1) preorder traversal without recursion


Solution: https://www.programmercarl.com/%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%BF%AD%E4%BB%A3%E9%81%8D%E5%8E%86.html#%E5%85%B6%E4%BB%96%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC


Key: preorder->mid, left, right ==  order to enter stack->mid, right, left 
1. create new result list
2. if root is null, return
3. create stack to store nodes
4. push the root node ready for pop to list
5. while stack is not empty, (1) pop the first node in stack (root) (2) add node val to list (3) if right is not null, push right to stack (4) if left is not null, push left to stack -> this makes it pop the left first then right
6. return list

![preorder using stack image](https://code-thinking.cdn.bcebos.com/gifs/%E4%BA%8C%E5%8F%89%E6%A0%91%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%EF%BC%88%E8%BF%AD%E4%BB%A3%E6%B3%95%EF%BC%89.gif)
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

//preorder->mid, left, right ==  order to enter stack->mid, right, left 
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if (root == null) {
            return result;
        }
        Stack<TreeNode> treeStack = new Stack ();
        treeStack.push(root);
        while (!treeStack.isEmpty()) {
            TreeNode node = treeStack.pop();
            result.add(node.val);
            if (node.right!=null) {
                treeStack.push(node.right);
            }
            if (node.left!=null) {
                treeStack.push(node.left);
            }
        }
        return result;
    }
}
```

## (2) inorder traversal without recursion (need to review)


Key: inorder-> left, mid, right == order to enter stack-> left, right

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

//inorder-> left, mid, right == order to enter stack-> left, right
//so amazing!
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if (root==null) {
            return result;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode cur = root;
        while (cur!=null || !stack.isEmpty()) {
            if (cur!=null) {
                stack.push(cur);
                cur = cur.left;
            } else {
                cur = stack.pop();
                result.add(cur.val);
                cur = cur.right;
            }
        }
        return result;
    }
}
```

## (3) postorder traversal without recursion

Key:  调整preorder代码结果的mid, left, right to mid, right, left. Then reverse result, 因此改变if left和right的顺序即可

```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        if (root == null) {
            return result;
        }
        Stack<TreeNode> treeStack = new Stack ();
        treeStack.push(root);
        while (!treeStack.isEmpty()) {
            TreeNode node = treeStack.pop();
            result.add(node.val);
            if (node.left!=null) {
                treeStack.push(node.left);
            }
            if (node.right!=null) {
                treeStack.push(node.right);
            }
        }
        Collections.reverse(result);
        return result;
    }
}
```