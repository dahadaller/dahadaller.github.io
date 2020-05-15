Title: 2 Add Two Numbers (Kieran)
Date: 2020-05-11
Authors: Kieran Duggan
Tags: LeetCode

>You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

>You may assume the two numbers do not contain any leading zero, except the number 0 itself.

First, let's outline what's going on here. Two numbers are given in a linked list representation s.t. **each node is a digit**. The list is ordered s.t. the head is the least significant digit, and the tail is the least significant. 

Example:
>Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
#We put the head to the right to follow convention for digits
l1    = (3<-4<-2)
l2    = (4<-6<-5)
l1+l2 = (8<-0<-7)
```
###Solution using 'pen and paper' math
The name comes from how similar this looks to addition on paper.
Lets review addition, we start from the righthand side, adding down, carry over, then repeat.
```
  1
  342
 +465_
  807
 
```
We can use this as inspiration for our solution. 
Our solution breaks down like this then:

 - Add a single digit
 - Carry
 - Repeat
 
 We're going to progressively work towards the solution together, so follow along.
 
 Here's our first attempt:
```python
class Solution:
	def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
		lsum = l1
		while l1 and l2:
			l1.val+=l2.val
			l1=l1.next
			l2=l2.next
		return lsum
```
Isn't that pretty? Just add each node together and store the result into l1. This is severely incomplete, **but this is really the essense of the solution.** In fact, this covers a lot of the test cases. We just need to work out the kinks.

First and most obviously, what if you get a number that overflows, i.e. greater than 9. From the example input we have 6+4 = 0, carry 1. Our first attempt just gets 10. :(

Here's our next attempt:
```python
class Solution:
	def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
		#We start with 0 in the carry
		carry = 0
		lsum = l1
		#Repeat while l1 and l2 aren't empty
		while l1 and l2:
			l1.val+=l2.val
			#Add the carry and reset it to zero
			l1.val+=carry
			carry=0
			if l1.val>=10:
				#cut off the 1 infront of the digit, and set carry
				l1.val%=10
				carry = 1
			l1=l1.next
			l2=l2.next
		return lsum
```
Now we have something of substance. We've accounted for the carry sufficiently, and if we add the constraint "l1 and l2 are the same length" then our attempt works! Sadly, no such constraint exists and we have to add code to allow for lists of differing lengths.

Lets refer back to how this looks on pen and paper
```
  100342         100342
 +   465_  is  + 000465_
  100807         100807
```
If you think about it... The white space can just be a bunch of trailing zeroes. And we know that any number plus zero is itself. More formally,
```
let n be a number
n + 0 = n
```
Zero is also known as the additive identity because of this property, and we can use this.

Basically all we have to do is "add" a bunch of zeroes to the rest of the number, and doing this means doing nothing

```python
class Solution:
	def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
		#We start with 0 in the carry
		carry = 0
		lsum = l1
		#Repeat while l1 and l2 aren't empty
		while l1 and l2:
			l1.val+=l2.val
			#Add the carry and reset it to zero
			l1.val+=carry
			carry=0
			if l1.val>=10:
				#cut off the 1 infront of the digit, and set carry
				l1.val%=10
				carry = 1
			#temp follows l1 so it can be at the tale of l1 at the end of the while loop
			temp = l1
			l1=l1.next
			l2=l2.next
		#Case where there are still digits in l1
		if l1:
			temp=temp
		#Case where l2 still has digits
		if l2:
			temp.next=l2
		l1 = temp.next
		return lsum
```
What's going on here is `temp` actually represents the rest of the digits we have yet to add. Both cases after the while loop just tack these onto the end of `l1`, effectively adding them. Genius, right? Not quite. There's still the annoying case of there being a carry at the last digit that *wasn't* trailing. The worst case example of this is as follows:
```
  9999
+    1
 10000
```
Our code erroneously does this:
```
 9999
+   1
 9990
```
To fix this, we need to add a second while loop that cascade carries down the remainder of `l1`
```python
class Solution:
	def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
		#We start with 0 in the carry
		carry = 0
		lsum = l1
		#Repeat while l1 and l2 aren't empty
		while l1 and l2:
			l1.val+=l2.val
			#Add the carry and reset it to zero
			l1.val+=carry
			carry=0
			if l1.val>=10:
				#cut off the 1 infront of the digit, and set carry
				l1.val%=10
				carry = 1
			#temp follows l1 so it can be at the tale of l1 at the end of the while loop
			temp = l1
			l1=l1.next
			l2=l2.next
		#Case where there are still digits in l1
		if l1:
			temp=temp
		#Case where l2 still has digits
		if l2:
			temp.next=l2
		l1 = temp.next
		#Loop while l1 isn't empty
		while l1:
			#Add the carry
			l1.val+=carry
			carry=0
			#If it overflows, reset the carry
			if l1.val>=10:
				l1.val%=10
				carry=1
			#Same as before, 'chase' l1 with temp
			temp=l1
			l1=l1.next
		#If there's still a carry, tack it to the end
		if carry == 1:
			temp.next = ListNode(val=1)
		return lsum
```
 And with that we finally have an ***accepted solution!***
 Thank you for reading. Please 
