---
layout: post
title: Algorithms Tree 02
categories: Algorithms
description: Algorithms Tree 02
keywords: Algorithms, Tree
---

#### [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)
```java
/*

Time complexity: O(n);
Space complexity: O(logn);
2018-10-31 12:55:09

*/
class Solution {

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null)
            return null;
        if (root.val == p.val || root.val == q.val)
            return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if (left != null && right != null)
            return root;
        if (left == null)
            return right;
        if (right == null)
            return left;
        return null;
    }
}
```
#### [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
```java
/*

Time complexity: O(n2);
Space complexity: O(logn);
2018-10-31 14:11:04

*/
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTree(preorder, inorder, 0, preorder.length - 1, 0, inorder.length - 1);
    }

    public TreeNode buildTree(int[] pre, int[] in, int pres, int pree, int ins, int ine) {
        if (pres > pree || ins > ine || pree > pre.length - 1 || ine > in.length - 1)
            return null;
        int i = ins;
        while (true) {
            if (in[i] == pre[pres])
                break;
            i++;
        }
        TreeNode node = new TreeNode(pre[pres]);
        node.left = buildTree(pre, in, pres + 1, pres + i - ins, ins, i - 1);
        node.right = buildTree(pre, in, pres + i - ins + 1, pree, i + 1, ine);
        return node;
    }
}
```

#### [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)
```java
/*

Solution 1
Time complexity: O(n);
Space complexity: O(n);
2018-11-01 00:50:27 update

*/
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        levelOrder(root, result, 0);
        return result;
    }

    public void levelOrder(TreeNode node, List<List<Integer>> result, int depth) {
        if (node == null)
            return;
        List<Integer> currentList = null;
        if (depth < result.size()) {
            currentList = result.get(depth);
        } else {
            currentList = new ArrayList<Integer>();
            result.add(currentList);
        }
        currentList.add(node.val);
        levelOrder(node.left, result, depth + 1);
        levelOrder(node.right, result, depth + 1);
    }
}


/*

Solution 2
Time complexity: O(n);
Space complexity: O(n);
2018-11-01 01:15:02 update
*/

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {

        List<TreeNode> list = new ArrayList<TreeNode>();
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if (root == null)
            return result;
        list.add(root);
        list.add(null);
        List<Integer> currentList = new ArrayList<Integer>();
        result.add(currentList);
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i) == null) {
                currentList = new ArrayList<Integer>();
                if (i != list.size() - 1) {
                    list.add(null);
                    result.add(currentList);
                }
            } else {
                currentList.add(list.get(i).val);
                if (list.get(i).left != null)
                    list.add(list.get(i).left);
                if (list.get(i).right != null)
                    list.add(list.get(i).right);
            }

        }
        return result;
    }
}
```
