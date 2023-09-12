# BinaryTree <5>
## (1) max depth of binary tree
104. https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/

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

 //recursion
// class Solution {
//     public List<List<Integer>> resultList = new ArrayList<List<Integer>>();

//     public int maxDepth(TreeNode root) {
//       int depth = 0;
//       levelOrder(root, 0);

//       return resultList.size();
//     }

//     public void levelOrder(TreeNode node, Integer deep) {
//       if (node == null) {
//         return;
//       }

//       deep++;

//       if (resultList.size() < deep) {
//         List<Integer> item = new ArrayList<>();
//         resultList.add(item);
//       }

//       resultList.get(deep-1).add(node.val);
//       levelOrder(node.left, deep);
//       levelOrder(node.right, deep);
//     }
// }

class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null)   return 0;
        Queue<TreeNode> que = new LinkedList<>();
        que.offer(root);
        int depth = 0;
        while (!que.isEmpty())
        {
            int len = que.size();
            while (len > 0)
            {
                TreeNode node = que.poll();
                if (node.left != null)  que.offer(node.left);
                if (node.right != null) que.offer(node.right);
                len--;
            }
            depth++;
        }
        return depth;
    }
}
```
## (2) min depth of binary tree
111.https://leetcode.cn/problems/minimum-depth-of-binary-tree/

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
    public int minDepth(TreeNode root) {
      if (root == null) return 0;
      Queue<TreeNode> tempQ = new LinkedList<>();
      tempQ.offer(root);
      int depth = 0;
      while(!tempQ.isEmpty()) {
        int size = tempQ.size();
        depth++;
        // TreeNode node = null;
        while (size > 0) {
          TreeNode node = tempQ.poll();
          if (node.left == null && node.right == null) return depth;
          if (node.left != null) tempQ.offer(node.left);
          if (node.right != null) tempQ.offer(node.right);
          size--;
        }
      }

      return depth;
    }
}
```

## (3) reverse binary tree
226.https://leetcode.cn/problems/invert-binary-tree/

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

 //preorder and postorder both work, but inorder does not because it will reverse redundantly
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) return null;
        swapChildren(root);
        invertTree(root.left);
        invertTree(root.right);
        
        return root;
    }

    public void swapChildren(TreeNode node ) {
        TreeNode tmp = node.left;
        node.left = node.right;
        node.right = tmp;
        
    }

}

// class Solution {
//     public TreeNode invertTree(TreeNode root) {
//         if (root == null) return null;
//         invertTree(root.left);
//         invertTree(root.right);
//         swapChildren(root);
        
//         return root;
//     }

//     public void swapChildren(TreeNode node ) {
//         TreeNode tmp = node.left;
//         node.left = node.right;
//         node.right = tmp;
        
//     }


}
```
