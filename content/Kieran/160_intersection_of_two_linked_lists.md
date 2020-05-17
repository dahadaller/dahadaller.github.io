Title: 328 Odd Even Linked List (Kieran)
Date: 2020-05-15
Authors: Kieran Duggan
Tags: LeetCode

>Write a program to find the node at which the intersection of two singly linked lists begins.

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        visited = set()
        while headA or headB:
            if headA:
                if headA in visited:
                    return headA
                else:
                    visited.add(headA)
                headA=headA.next
            if headB:
                if headB in visited:
                    return headB
                else:
                    visited.add(headB)
                headB=headB.next
            
        return None
```
