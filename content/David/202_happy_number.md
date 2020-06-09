Title: 202 Happy Number (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 2, LeetCode



Here we solve the [Happy Number Problem](https://leetcode.com/problems/happy-number/) from LeetCode.

> Write an algorithm to determine if a number `n` is "happy".
>
> A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where  it will stay), or it **loops endlessly in a cycle** which does not include 1. Those numbers for which this process **ends in 1** are happy numbers.
>
> Return True if `n` is a happy number, and False if not.
>
> **Example:** 
>
> ```
> Input: 19
> Output: true
> Explanation: 
> 12 + 92 = 82
> 82 + 22 = 68
> 62 + 82 = 100
> 12 + 02 + 02 = 1
> ```



The trick to this problem is you have to keep a record of the happy numbers already encountered, and you have to be able to iterate through the individual digits of a number. In this approach, I used a set `previous_numbers` to keep track of the happy numbers that have already been calculated. I also converted the numbers to strings, since strings are iterable by character in Python (each character being a digit in this case) , instead of using `//` and `%`. 

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        
        current_number = str(n)
        previous_numbers = set()
        
        while current_number != '1':
            
            square_sum = 0
            
            for digit in map(int,list(str(current_number))):
                square_sum += digit * digit
                
            current_number = str(square_sum)
            
            if current_number not in previous_numbers:
                previous_numbers.add(current_number)
            else:
                return False
            
        return True
                    
```






