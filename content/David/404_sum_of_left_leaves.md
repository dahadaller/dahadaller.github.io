Title: 404 Sum of Left Leaves (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 3, LeetCode



Here we solve the [Sum of Left Leaves - LeetCode](https://leetcode.com/problems/sum-of-left-leaves/) problem from LeetCode:

> Find the sum of all left leaves in a given binary tree.
>
> **Example:**
>
> ```
>     3
>    / \
>   9  20
>     /  \
>    15   7
> 
> There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
> ```





This is an interesting problem in that the solution requires some labeling (the comments below) to recognize the base case, and the recursive postorder traversal.


```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
    
    		# base case for stopping traversal
        if  not root:
            return 0
          
        # base case for adding the left leaf value 
        # (notice that this base case also has a recursive call onto the 
        # right sub tree)
        elif root.left and not root.left.left and not root.left.right:
            return root.left.val + self.sumOfLeftLeaves(root.right)
          
        # this is the recursive step and it is a postorder traversal of the 
        # binary tree compressed into a single line
        else:
            return self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
            # the code could also be written as follows to demonstrate that it is postorder:
            # left_sum = self.sumOfLeftLeaves(root.left)
            # right_sum = self.sumOfLeftLeaves(root.right)
            # root_sum = left_sum + right_sum
            # return root_sum
```

