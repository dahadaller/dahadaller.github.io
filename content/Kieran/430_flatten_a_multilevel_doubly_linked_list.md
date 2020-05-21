Title: 430. Flatten a Multilevel Doubly Linked List (Kieran)
Date: 2020-05-15
Authors: Kieran Duggan
Tags: LeetCode

>You are given a doubly linked list which in addition to the next and previous pointers, it could have a child pointer, which may or may not point to a separate doubly linked list. These child lists may have one or more children of their own, and so on, to produce a multilevel data structure, as shown in the example below.

Iterate down the list. If there's a child then put head.next on the stack, and make head.next = head.child, then continue iterating

When you reach the end of the list, if there is still a node in the stack, make that node next and continue iterating.

```python3
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
        
    def flatten(self, head: 'Node') -> 'Node':
        nodes = []
        ret = head
        
        while head:
            if head.child:
                if head.next:#Only put another node in the stack if next exists
                    nodes.append(head.next)
                head.next = head.child #Make the next node the child
                head.child = None
                head.next.prev = head #Connect backwards for doubly linked list
            elif head.next is None and nodes:
                #print(nodes)
                head.next = nodes.pop() #Pop the top of the stack into next
                head.next.prev = head #Connect backwards for doubly linked list
            head = head.next
                
        return ret
```
