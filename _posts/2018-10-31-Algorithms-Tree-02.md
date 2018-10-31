---
layout: post
title: Algorithms Tree 01
categories: Algorithms
description: Algorithms Tree 01
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
