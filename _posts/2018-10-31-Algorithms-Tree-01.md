---
layout: post
title: Algorithms Tree 01
categories: Algorithms
description: Algorithms Tree 01
keywords: Algorithms, Tree
---
#### [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)
```java
/*
2018-10-31 00:50:31

Time complexity: O(n);
Space complexity: O(logn)~O(n);


*/
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null)
            return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```
#### [Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/description/)
```java
/*
Time complexity: O(n);
Space complexity: O(logn);
2018-10-31 01:01:21
*/
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null)
            return null;
        TreeNode node = root.left;
        root.left = root.right;
        root.right = node;
        invertTree(root.left);
        invertTree(root.right);
        return root;
    }
}
```
#### [Same Tree](https://leetcode.com/problems/same-tree/description/)
```java
/*

Time complexity: O(n);
Space complexity: O(logn);
2018-10-31 01:07:25
*/
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null)
            return true;
        if (p == null || q == null)
            return false;
        if (p.val != q.val)
            return false;
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }

}
```

#### [Unique Binary Search Trees](https://leetcode.com/problems/unique-binary-search-trees/description/)
```java

/*

Time complexity: O(n2);
Space complexity: O(n);
2018-10-31 01:30:11

*/

class Solution {
    public Map<Integer, Integer> map = new HashMap<>();

    public int numTrees(int n) {
        if (n == 1)
            return 1;
        if (n == 0)
            return 1;
        if (map.get(n) != null)
            return map.get(n);
        int sum = 0;
        for (int i = 1; i <= n; i++) {
            sum += numTrees(i - 1) * numTrees(n - i);
        }
        map.put(n, sum);
        return sum;
    }
}
```
#### [Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/description/)
```java
/*
Time complexity: O(n);
Space complexity: O(logn);
2018-10-31 10:36:57
*/
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0)
            return null;
        return sortedArrayToBST(nums, 0, nums.length - 1);
    }

    public TreeNode sortedArrayToBST(int[] nums, int begin, int end) {
        if (begin > end)
            return null;
        int mid = begin + (end - begin) / 2;
        TreeNode node = new TreeNode(nums[mid]);
        node.left = sortedArrayToBST(nums, begin, mid - 1);
        node.right = sortedArrayToBST(nums, mid + 1, end);
        return node;
    }
}
```
#### [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)
```java
/*

Time complexity: O(n);
Space complexity: O(logn);
2018-10-31 10:32:43

*/
class Solution {
    public boolean isBalanced(TreeNode root) {
        if (isBalancedToo(root) != -1)
            return true;
        else
            return false;
    }

    public int isBalancedToo(TreeNode node) {
        if (node == null)
            return 0;
        int leftheight = isBalancedToo(node.left);
        int rightheight = isBalancedToo(node.right);
        if (leftheight == -1 || rightheight == -1)
            return -1;
        if (Math.abs(leftheight - rightheight) <= 1)
            return Math.max(leftheight, rightheight) + 1;
        else
            return -1;
    }
}
```
[Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)
```java
/*

Time complexity: O(logn);
Space complexity: O(logn);
2018-10-31 10:50:44

*/
class Solution {

    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (p.val > root.val && q.val < root.val || p.val < root.val && q.val > root.val)
            return root;
        if (p.val < root.val && q.val < root.val)
            return lowestCommonAncestor(root.left, p, q);
        if (p.val > root.val && q.val > root.val)
            return lowestCommonAncestor(root.right, p, q);
        if (p.val == root.val || q.val == root.val)
            return root;
        return null;
    }

}
```
[Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)
```java
/*

Time complexity: O(n);
Space complexity: O(logn);
2018-10-31 11:03:08

*/
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null)
            return true;
        return isSymmetric(root.left, root.right);
    }

    public boolean isSymmetric(TreeNode node1, TreeNode node2) {
        if (node1 == null && node2 == null)
            return true;
        if (node1 == null || node2 == null)
            return false;
        if (node1.val == node2.val)
            return isSymmetric(node1.left, node2.right) && isSymmetric(node2.left, node1.right);
        else
            return false;
    }
}
```
