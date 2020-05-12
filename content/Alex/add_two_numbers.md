Title: Add Two Numbers
Date: 2020-05-10 22:30
Authors: Alex Matson
Tags: LeetCode, Week 1

This post will cover my solution in Python 3 for LeetCode's [Add Two Numbers](https://leetcode.com/problems/add-two-numbers/) problem. The problem wants us to add two numbers (`l1` and `l2` that are encoded as linked lists, such that each digit is a linked list node. In this scheme, the digits in the linked list are ordered from least significant to most signficant. Thus, the number `254` would be represented as the linked list `4 -> 5 -> 2 -> None`. 

The general approach to the problem that I took was to loop through the lists, pairwise add the digits of `l1` and `l2` and insert them as new nodes into a return list. I'll walk through my solution with some annotated code snippets. 

    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.next = None
    
    class Solution:
        def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
    	# Use dummy head technique as a starting point for the algorithm
    	head = ListNode("dummy")
    	current = head
    
    	# Iterate through the lists until _both_ are None
    	# This means, even if one is shorter than the other, keep looping anyway
    	while l1 or l2:
    	    # Default to "0" if one of the lists is out of digits
    	    val1 = l1.val if l1 else 0
    	    val2 = l2.val if l2 else 0
    
    	    # Compute the sum of the two digits for the result digit
    	    digit = val1 + val2
    
    	    # Move a carry by adding 1 to the next node in l1 or l2 -- depending on which one actually has a "next" node available
    	    # If neither l1 or l2 have a next node available, (for example, you are carrying past the final digit of the longer l1/l2)
    	    # then just create a new node and append it to the end
    	    if digit >= 10:
    		node = l1 if l1 else l2
    		if node.next:
    		    node.next.val += 1
    		else:
    		    node.next = ListNode(1)
    
    	    temp = ListNode(digit % 10)
    
    	    # Put this digit as a node into our result list
    	    # Move the result list forward
    	    current.next = temp
    	    current = current.next
    
    	    # Move l1 and l2 forward, for as long as they have a "next"
    	    l1 = l1.next if l1 else None
    	    l2 = l2.next if l2 else None
    
    	# Return the next to exclude our dummy head from the beginning
    	return head.next
