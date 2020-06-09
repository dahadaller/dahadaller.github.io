Title: 232 Implement Queue using Stacks (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 2, LeetCode



This post solves the [Implement Queue using Stacks - LeetCode](https://leetcode.com/problems/implement-queue-using-stacks/) problem. 

> Implement the following operations of a queue using stacks.
>
> - push(x) -- Push element x to the back of queue.
> - pop() -- Removes the element from in front of queue.
> - peek() -- Get the front element.
> - empty() -- Return whether the queue is empty.
>
> **Example:**
>
> ```
> MyQueue queue = new MyQueue();
> 
> queue.push(1);
> queue.push(2);  
> queue.peek();  // returns 1
> queue.pop();   // returns 1
> queue.empty(); // returns false
> ```
>
> **Notes:**
>
> - You must use *only* standard operations of a stack -- which means only `push to top`, `peek/pop from top`, `size`, and `is empty` operations are valid.
> - Depending on your language, stack may not be supported natively.  You may simulate a stack by using a list or deque (double-ended queue),  as long as you use only standard operations of a stack.
> - You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).



While in a queue there are two points of ingress and egress, stacks only have one. You can leave from the front of the queue, and enter from the back, but you can only enter and exit from the top of the stack. This solution is optimized for multiple pushes/pops in a row. 

Whenever we want to push to the queue, all data is placed in the `push_stack`, where the front of the queue corresponds to the bottom of the `push_stack` and the back of the queue corresponds to the top of the stack. Then, each subsequent push operation after the first one only takes O(1), since we're just pushing to the end of the stack. 

Whenever we want to pop from the front of the queue, we migrate all the data to the `pop_stack` where it will be in reverse order compared to the `push_stack`. The top of the `pop_stack` corresponds to the front of the queue, so popping off the front takes O(1) just like a normal stack pop.



So, the runtime complexity of pushing/popping to the queue are O(n) in the worst case and O(1) in the average case.



```python
class MyQueue:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        # holds data for queue pushing is O(1) but popping is O(N) because
        # beginning of queue is at bottom of stack in this implementation
        self.push_stack = [] 
        self.pop_stack = []
        

    def push(self, x: int) -> None:
        """
        Push element x to the back of queue.
        """
        
        if not self.push_stack:
            while self.pop_stack:
                self.push_stack.append(self.pop_stack.pop())
         
        self.push_stack.append(x)
            

    def pop(self) -> int:
        """
        Removes the element from in front of queue and returns that element.
        """
        if not self.pop_stack:
            while self.push_stack:
                self.pop_stack.append(self.push_stack.pop())
            
        return self.pop_stack.pop()

    def peek(self) -> int:
        """
        Get the front element.
        """
        if not self.pop_stack:
            while self.push_stack:
                self.pop_stack.append(self.push_stack.pop())
            
        return self.pop_stack[-1]
            

    def empty(self) -> bool:
        """
        Returns whether the queue is empty.
        """
        q_len = max(len(self.push_stack),
                    len(self.pop_stack)
                   )
        return q_len==0
        


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```

