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

## (3) 