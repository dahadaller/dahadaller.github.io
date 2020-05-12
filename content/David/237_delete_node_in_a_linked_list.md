Title: 237 Delete Node in a Linked List (David)
Date: 2020-05-11 23:30
Authors: David Hadaller
Tags: Week 1, LeetCode

 Usually, when deleting nodes in a linked list, we start with the head, and search for the node to delete. Once found, we usually delete the node with some pointer manipulation according to the [dummy head technique](https://github.com/codepath/compsci_guides/wiki/Dummy-Head). 

**However**, the  [Delete Node in a Linked List](https://leetcode.com/problems/delete-node-in-a-linked-list/)  problem is slightly different; it instructs us to start in the middle of the linked list with  `node` , and delete that element. We don't start at the head of the list or use the dummy head technique, as is normally the case. To delete `node` starting from `node` itself, we use the strategy of overwriting the value of `node` and shifting each of the values of the remaining to the right. Here's a worked example for deleting the node with value `2` in linked list `1 -> 2 -> 3 -> 4 -> 5-> None`. 


This is the linked list we start with
```
1 -> 2 -> 3 -> 4 -> 5-> None
     |
    ptr
   (node)
   
```

We then proceed thrugh the while loop, overwriting `ptr.val` with `ptr.next.val`. Here we overwrote `2` with `3`.
```
1 -> 3 -> 3 -> 4 -> 5-> None
     |    |
    ptr   ptr.next
```

Now, we overwrite `3` with `4`.
```
1 -> 3 -> 4 -> 4 -> 5-> None
           |    |
          ptr   ptr.next
```
After that, we exit the while loop, because we're close enough to the tail of the list to put the final elements in place; shift the final element of the link list over to the left by overwriting `4` with `5`, then overwrite the last `5` with `None`.

```
1 -> 3 -> 4 -> 5 -> 5-> None
               |    |
              ptr   ptr.next
              
             
1 -> 3 -> 4 -> 5 -> None
               |    |
              ptr   ptr.next
```



Finally, the code: 

```python
# 237. Delete Node in a Linked List

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        ptr = node
        
        while ptr.next.next:
            ptr.val = ptr.next.val
            ptr = ptr.next
            
        ptr.val = ptr.next.val
        ptr.next = None
```

