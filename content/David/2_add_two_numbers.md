Title: 2 Add Two Numbers (David)
Date: 2020-05-11 23:30
Authors: David Hadaller
Tags: Week 1, LeetCode, Draft



This is the answer to the [Add Two Numbers - LeetCode](https://leetcode.com/problems/add-two-numbers/) problem. Please don't use it; the solution is very very inefficient. Here are some reasons this code sucks:

- Do three separate pass throughs on l1, l2 and creating a linked list from their integer sum
- `digit.val * (radix ** index_a)` is a very expensive operation.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        
        radix = 10
        running_sum = 0
        
        # iteratively sum l1
        digit = l1
        index_a = 0
        while digit:
            running_sum += digit.val * (radix ** index_a)
            digit = digit.next
            index_a += 1
        l1_sum = running_sum
            
        # iteratively sum l2's digits to l1 for running_sum
        digit = l2
        index_b = 0
        while digit:
            running_sum += digit.val * (radix ** index_b)
            digit = digit.next
            index_b += 1
            
        total_sum = running_sum
        
        ret_list = None
        
        if not running_sum >= (radix ** index_a) or not running_sum >= (radix ** index_b):
            index = max(index_a-1, index_b-1)
        else:
            index = max(index_a, index_b)
            
            
        # create the return list    
        while index >= 0:
            
            digit = total_sum // (radix ** index)
            print(total_sum, '//', (radix ** index), '=', digit)
            total_sum = total_sum % (radix ** index)
            index -= 1
            
            ret_list_old = ret_list
            ret_list = ListNode(digit)
            ret_list.next = ret_list_old
            
            
        return ret_list
```

