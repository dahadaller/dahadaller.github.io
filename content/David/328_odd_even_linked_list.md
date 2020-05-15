Title: 328 Odd Even Linked List (David)
Date: 2020-05-15 23:30
Authors: David Hadaller
Tags: Week 1, LeetCode



This code solves the [Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/) problem from LeetCode.

>Given a singly linked list, group all odd nodes together followed by the even nodes.  Please note here we are talking about the node number and not the value  in the nodes.
>
>You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.
>
>**Example 1:**
>
>```
>Input: 1->2->3->4->5->NULL
>Output: 1->3->5->2->4->NULL
>```
>
>**Example 2:**
>
>```
>Input: 2->1->3->5->6->4->7->NULL
>Output: 2->3->6->7->1->5->4->NULL
>```
>
>**Note:**
>
>- The relative order inside both the even and odd groups should remain as it was in the input.
>- The first node is considered odd, the second node even and so on ...



```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next


class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        
        if not head:
            return
        
        odds_list = head
        evens_list = head.next
        
        trail_ptr = head
        lead_ptr = head.next
        
        
        trail_ptr_index = 1
        
        while lead_ptr:
            
            # for each list element, make it point
            # to the next element over
            
            # +-----+
            # |     |
            # |     v
            # 1  2->3->4->5->NULL
            # |  |
            # tr lead_ptr 
            trail_ptr.next = lead_ptr.next
            
            old_trail_ptr = trail_ptr
            trail_ptr = lead_ptr
            lead_ptr = lead_ptr.next
            
            trail_ptr_index += 1
        
            
        # the following if statements are needed because the 
        # trail_ptr (abbreviated tr in diagrams) falls on odd/even
        # list element at the end of the while loop depending on whether the total
        # number of elements (list index) is odd or even
          
        # 1->2->3->4->5->NULL  (tr falls on odd)
        #          |  |   |
        #     old_tr  tr  lead_ptr
        
        # 1->2->3->4->5->6->NULL (tr falls on even)
        #             |  |   |
        #         old_tr tr  lead_ptr
        
        if trail_ptr_index % 2 == 0:
            old_trail_ptr.next = evens_list # stitch lists together
            return odds_list # return head of stiched lists
   
        else:
            trail_ptr.next = evens_list # stitch lists together
            return odds_list # return head of stiched lists       
```

