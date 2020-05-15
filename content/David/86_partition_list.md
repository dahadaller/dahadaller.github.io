Title: 86 Partition List (David)
Date: 2020-05-15 23:30
Authors: David Hadaller
Tags: Week 1, LeetCode, Unsolved

This code solves the [Partition List](https://leetcode.com/problems/partition-list/) problem.

>             Given a linked list and a value *x*, partition it such that all nodes less than *x* come before nodes greater than or equal to *x*.
>
>             You should preserve the original relative order of the nodes in each of the two partitions.
>
>             **Example:**
>
>             ```
>             Input: head = 1->4->3->2->5->2, x = 3
>             Output: 1->2->2->4->3->5
>             ```



 The following is an explanation of my implemention of the two-pointer solution given by LeetCode. My initial attempt (at the bottom of this post) only worked for lists of length greater than 3 and didn't pass the submission after multiple revisions, and it relied on 6 pointers, rather than 2.



### LeetCode's Two-Pointer Solution

For a more in depth explanation, check the solution [here](https://leetcode.com/problems/partition-list/solution/).

The trick I learned from this problem is that lists can be grown in the direction they point without loosing the head, if you save it at the beginning as is done on lines 20 and 21 below.

After all is said and done, a list that starts out with the following arrangement:

```
1 -> 2 -> 2 -> 4 -> 3 -> 2 -> None
```

Will have a pointer arrangement that looks like this:

```
ltx_head
|
| gtx_head
|  |
|  |
|  +-----------+    +---------+
v              v    |         v
1 -> 2 -> 2    4 -> 3    2   None
          |              ^
          |              |
          +--------------+
```

After this, `gtx_head` can be stiched to the back of `ltx_head` to return the final answer.



Here's the code:


```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        
        #ltx = "less than x"
        #gtx = "greater than (or equal to) x"
				
        #ltx_head.next and gtx_head.next will still point to 
        # heads of lists afer ltx and gtx have been incremented
        ltx = ltx_head = ListNode(0) 
        gtx = gtx_head = ListNode(0)

        while head:

            if head.val < x:
                ltx.next = head
                ltx = ltx.next
            else:

                gtx.next = head
                gtx = gtx.next

            head = head.next

        gtx.next = None
        ltx.next = gtx_head.next
        return ltx_head.next                 
                
```



### My Original Solution

```python
class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        
        if not head:
            return
        
        if not head.next:
            return head
        
        trail = trail_ltx = head
        mid   = mid_ltx   = head.next
        lead  = lead_ltx  = head.next.next
        
        while mid:
            print(head)
            if mid.val < x:
                
                trail_ltx.next = mid
                mid.next = mid_ltx
                
                trail.next = lead
                
                trail_ltx = mid
                mid_ltx = mid.next
                
            trail = mid
            mid = lead
            lead = None if not lead else lead.next
            

        return head
```