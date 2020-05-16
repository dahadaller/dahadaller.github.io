Title: 242 Valid Anagram (David)
Date: 2020-05-10 11:30
Authors: David Hadaller
Tags: Bloomberg, LeetCode

The posts in this series (each with the tag `Bloomberg`) contain problems taken from [this list](https://leetcode.com/discuss/interview-question/439548/Bloomberg-Phone-Interview-Questions) of Bloomberg phone interview problems. In this post, we solve LeetCode's [242 Valid Anagram](https://leetcode.com/problems/valid-anagram/). 

> Given two strings s and t , write a function to determine if t is an anagram of s.

First, it's important to know the difference between an anagram and a palindrome. An anagram is a word formed by rearranging the letters of another word. So if string `s` is "tarp" and string `t` is "part", then `s` and `t` are anagrams of one another. On the other hand, A palindrome is a word that reads the same backward or forward (like the word "kayak").

There are a couple of ways to tackle this problem. Each approach involves creating a dictionary where the letters from `s` and `t` are keys and the values are counts of how many times the letters occur in the string. Whenever we create a tally dictionary in Python, we have to be cognizant of avoiding `KeyError`s. The first approach relies on python's `.get()` method to avoid this, while the last two methods rely on the Python's `collections` classes. 

### Solution using Dictionary and `.get()`

In Python, the `get(key, default)` method returns a value for the given key in a dictionary. If `key` is not available, the method then returns `default`. 

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # if strings are not same length, 
        # they can't be anagrams
        if len(s) != len(t):
            return False

        # create default dictionaries for for s and t
        s_dict = {}
        t_dict = {}

        # populate dictionaries for for s and t
        # where the letters are keys and the number of times
        # the letter appears are values
        for s_char in s: 

        	# if s_dict[s_char] doesn't exist yet, 
        	# initialize to 1. Otherwise increment by 1
            if not s_dict.get(s_char):
                s_dict[s_char] = 1
            else:
                s_dict[s_char] += 1

        for t_char in t:
            if not t_dict.get(t_char):
                t_dict[t_char] = 1
            else:
                t_dict[t_char] += 1

        return t_dict == s_dict

```


### Solution using `collections.defaultdict`

The `defaultdict` class is covered in the [Stacks, Queues, Heaps, and Hash Tables in Python]({filename}useful_python_libraries.md) post. Where a Python dictionary normally throws a `KeyError` if you try to retrieve a value with a key that is not in the dictionary, `defaultdict` will just create a new key-value pair with a default value.


```python
from collections import defaultdict 

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        
        # if strings are not same length, 
        # they can't be anagrams
        if len(s) != len(t):
            return False
        
        # this default dict makes values default to 0 (int's default) 
        # when any accessed key doesn't already exist in the dictionary
        s_dict = defaultdict(int)
        t_dict = defaultdict(int)


  		# populate default dictionaries for for s and t
  		# where the letters are keys and the number of times
  		# the letter appears are values
        for s_char in s: 
            s_dict[s_char] = s_dict[s_char] + 1
        
        for t_char in t:
            t_dict[t_char] = t_dict[t_char] + 1 

        return t_dict == s_dict
```

### Solutions using `collections.Counter` 

Like `defaultdict`, the `Counter` class is also a subclass of Python Dictionary. It's a class designed to keep tallies, like we are doing here. 

```python

from collections import Counter 

class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
            
            if len(s) != len(t):
                return False
        
        	# in one step, we instantiate two dictionaries 
        	# that each contain tallies of letters in s and t
        	# and we compare if those tally dictionaries are equal
            return Counter(s) == Counter(t)
```

