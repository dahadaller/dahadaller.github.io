Title: 328 Odd Even Linked List (Kieran)
Date: 2020-05-15
Authors: Kieran Duggan
Tags: LeetCode
>Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

>You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

My idea is to construct a list containing all of the even nodes of the list, while removing these nodes from the original list

After this seconday list is made, it is tacked to the end of the original list which had its even number removed

```python3
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        #head is the odd list
        #build the even list and tack it to the end
        if head is None:
            return head
        if head.next is None:
            return head
        even = True
        l_odd=head
        l_even =  ListNode()
        even_head = l_even
        
        chaser = head
        head = head.next
        while head:
            if even:
                chaser.next = head.next
                even_head.next = head
                even_head = even_head.next
            chaser2= chaser
            chaser = head
            head = head.next
            even = not even
        even_head.next = None
        if not even:
            chaser2.next = l_even.next
        else:
            chaser.next = l_even.next
        
        return l_odd
```
