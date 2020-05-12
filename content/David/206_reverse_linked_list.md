Title: 206 Reverse Linked List (David)
Date: 2020-05-11 23:30
Authors: David Hadaller
Tags: Week 1, LeetCode

This problem is taken from [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/).  Here I present recursive and iterative solutions. 



### Recursive Solution

The intuition for the recursive solution is as follows: Suppose our list looks like this 

```
1 -> [2 -> 3 -> 4 -> 5 -> ...] 
```

where the first element of the linked list is called `head` and the the bracketed portion of the linked list, which I call *the rest*.  

The way we construct a reversed linked list from the `head` and *the rest* by the following process:

First, run the reverse function on *the rest*. `rev_head` will point to the head of the already reversed portion of the list, and `rev_tail` will point to the tail of this portion.

```
1 -> [n -> ... -> 5 -> 4 -> 3 -> 2]
|     |                          |
head rev_head                 rev_tail
```

Then place *the rest* in front of the `head` by assigning `rev_tail.next = head` and `head.next = None `. 

```
[n -> ... -> 5 -> 4 -> 3 -> 2] -> 1 -> None
 |                          |     |    
rev_head               rev_tail  head 
```

The list is now fully reversed.



```python

# 206. Reverse Linked List
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
      
 				# edge case of empty linked list
        if not head:
            return
          
    		# single node is our base case
        if head.next == None: 
            return head
          
        # inductive step  
        else:
          	#this  call to reverseList() does not reverse in-place ...
            rev_head = self.reverseList(head.next) 
  					# ... which means we still have access to head.next here
            rev_tail = head.next 
            head.next = None 
            rev_tail.next = head
            
            return rev_head
```



### Iterative Solution



In the iterative solution, the intuition is to itertively take the head off the original linked list and make it the head of another linked list using the insert function for linked lists. 

```python
def insert(linked_list, node_val):
    n = ListNode(vanode_vall)
    n.next = linked_list
    return n
```

Here's a worked example that lends some intuition to the process, starting with a normal linked list.

```
1 -> 2 -> 3 -> 4 -> 5 -> None 
|
head
```
We then increment `head` and use `ptr` to make the head of the original linked list the head of a new linked list.

```
1 -> 2 -> 3 -> 4 -> 5 -> None 
|    |
ptr  head


None <-1    2 -> 3 -> 4 -> 5 -> None 
       |    |
      ptr  head
```

 And so on, with the remaning nodes

```
None <-1 <- 2     3 -> 4 -> 5 -> None 
            |    |
           ptr  head
           
None <-1 <- 2 <- 3    4 -> 5 -> None 
                 |    |
                ptr  head
           
           
None <-1 <- 2 <- 3 <-  4    5 -> None 
                       |    |
                      ptr  head
                      
                      
None <-1 <- 2 <- 3 <-  4  <- 5   None 
                            |    |
                           ptr  head
```

 Then return `ptr` and you get your reversed linked list.




```python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        
        if not head:
            return
        if not head.next:
            return head
        
        prev_ptr = None
        
        while head:
          
            ptr = head
            head = head.next
            
            ptr.next = prev_ptr
            prev_ptr = ptr
            
        return ptr
```