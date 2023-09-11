# BinaryTree <4>
## (1) level order search no recursion (BFS)

102.https://leetcode.cn/problems/binary-tree-level-order-traversal/description/

key:
1. using queue (fifo) to build the list in the order of bfs

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

        checkFunc02(root);

        return resList;
    }

    //BFS
    public void checkFunc02 (TreeNode node) {
        if (node == null) return;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.offer(node);

        while (!q.isEmpty()) {
            List<Integer> itemList = new ArrayList<>();
            int len = q.size();

            //this len is the len of the original queue without enqueue the left and right children nodes
            while (len > 0) {
                TreeNode tmpNode = q.poll();
                itemList.add(tmpNode.val);

                if(tmpNode.left != null) q.offer(tmpNode.left);
                if(tmpNode.right != null) q.offer(tmpNode.right);
                len--;
            }

            resList.add(itemList);
        }
    }
}
```

## (2)

116.https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/submissions/

key: idx=1 because the last node for each level should point to null which means it lacks one level of loop

```
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        Queue<Node> tmpQueue = new LinkedList<Node>();
        if (root != null) tmpQueue.add(root);

        while (tmpQueue.size() != 0) {
            int size = tmpQueue.size();

            Node cur = tmpQueue.poll();
            if (cur.left != null) {
                tmpQueue.add(cur.left);
            }
            if (cur.right != null) {
                tmpQueue.add(cur.right);
            }
            // idx=1 because the last node for each level should point to null which means it lacks one level of loop
            for (int idx = 1; idx< size; idx++) {
                Node next = tmpQueue.poll();
                if (next.left!=null) tmpQueue.add(next.left);
                if (next.right!=null) tmpQueue.add(next.right);

                cur.next = next;
                cur = next;
            }
        }

        return root;
    }
}
```