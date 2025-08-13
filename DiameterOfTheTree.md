# Binary Tree Diameter Solution

## Problem Description
The diameter of a binary tree is the length of the longest path between any two nodes in the tree. This path may or may not pass through the root. The length of a path is measured by the number of edges between nodes.

## Solution Approach

```java
class Solution {
    
    // Calculate right height of a subtree
    public int RH(TreeNode root, int count) {
        if(root == null) return count;
        int left = RH(root.left, count+1);
        int right = RH(root.right, count+1);
        return Math.max(left, right);
    }
    
    // Calculate left height of a subtree
    public int LH(TreeNode root, int count) {
        if(root == null) return count;
        int left = LH(root.left, count+1);
        int right = LH(root.right, count+1);
        return Math.max(left, right);
    }
    
    public int max = 0;
    
    // Pre-order traversal to check all nodes
    public void preOrder(TreeNode root) {
        if(root == null) return;
        
        // Calculate diameter passing through current node
        int val = LH(root.left, 0) + RH(root.right, 0);
        max = Math.max(max, val);
        
        preOrder(root.left);
        preOrder(root.right);
    }
    
    public int diameterOfBinaryTree(TreeNode root) {
        preOrder(root);
        return max;
    }
}
