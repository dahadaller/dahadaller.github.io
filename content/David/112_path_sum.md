Title: 112 Path Sum (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 3, LeetCode



Here I solve the [Path Sum - LeetCode](https://leetcode.com/problems/path-sum/) problem from LeetCode:

> Given a binary tree and a sum, determine if the tree has a root-to-leaf path  such that adding up all the values along the path equals the given sum.
>
> **Note:** A leaf is a node with no children.
>
> **Example:**
>
> Given the below binary tree and `sum = 22`,
>
> ```
>       5
>      / \
>     4   8
>    /   / \
>   11  13  4
>  /  \      \
> 7    2      1
> ```
>
> return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.



The approach taken here is that we do a postorder traversal (because we're looking for paths that end in leaves)  As we go, we subtract the current node value from the path sum as we encounter new nodes. If the current node is a leaf node, and the `path_sum` is 0, then we know that all the nodes on the way to the current add up to the orignial `path_sum` before subtraction began.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def hasPathSum(self, root: TreeNode, path_sum: int) -> bool:
        
        # base case for stop traversal
        if not root:
            return False
        
        # base case for search: it has to be a path to a leaf. 
        # omitting the leaf restriction means you look for paths of length k
        # ending at any arbitrary node.
        elif not root.left and not root.right and path_sum - root.val == 0:
            return True        
        
        # postorder traversal inductive step
        else: 
            left_path_has_sum = self.hasPathSum(root.left, path_sum - root.val)
            right_path_has_sum = self.hasPathSum(root.right, path_sum - root.val)
            root_path_hast_sum = left_path_has_sum or right_path_has_sum
            
            return root_path_hast_sum
```

