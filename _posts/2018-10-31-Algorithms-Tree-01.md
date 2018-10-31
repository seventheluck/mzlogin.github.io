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
        if(root==null)
            return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right))+1;
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
        if(root == null)
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
        if(p == null&&q == null)
            return true;
        if(p == null||q == null)
            return false;
        if(p.val!=q.val)
            return false;
        return isSameTree(p.left, q.left)&&isSameTree(p.right, q.right);
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
    public Map <Integer, Integer> map = new HashMap<>();
    public int numTrees(int n) {
        if(n==1)
            return 1;
        if(n==0)
            return 1;
        if(map.get(n)!=null)
            return map.get(n);
        int sum = 0;
        for(int i = 1; i <= n; i++){
            sum += numTrees(i-1) * numTrees(n-i);
        }
        map.put(n, sum);
        return sum;
    }
}
```
