Title: 543 Diameter of Binary Tree (Kieran)
Date: 2020-05-18
Authors: Kieran Duggan
Tags: LeetCode, Bloomberg

>Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def height(self, root: TreeNode) -> int:
        if root is None:
            return 0
        else:
            return 1+max(self.height(root.left),self.height(root.right))
    
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        if root is None:
            return 0
        else:
            lheight = self.height(root.left)
            rheight = self.height(root.right)
            
            ldiam = self.diameterOfBinaryTree(root.left)
            rdiam = self.diameterOfBinaryTree(root.right)
            
            return max(lheight+rheight,ldiam,rdiam)
```
