Title: 141 Linked List Cycle (David)
Date: 2020-05-11 23:30
Authors: David Hadaller
Tags: Week 1, LeetCode

This code solves the  [Linked List Cycle ](https://leetcode.com/problems/linked-list-cycle/) problem. If the hare (a pointer)  starts *ahead* of the turtle (also a pointer) and the hare ends up passing the turtle from behind, then we know there must have been a cycle in the race course (the linked list). This is a [Two-Pointer](https://github.com/codepath/compsci_guides/wiki/Linked-List-Two-Pointer)   problem. 

```python
# 141. Linked List Cycle

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        
        if not head or not head.next:
            return False
        
        hare = head.next
        turtle = head
        
        while hare and hare.next:
            
            if hare.next == turtle or turtle == hare:
                return True
            else:
                turtle = turtle.next
                hare = hare.next.next
            
        return False
```

