Title: 692 Top K Frequent Words (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 2, LeetCode



Here we solve the [Top K Frequent Words](https://leetcode.com/problems/top-k-frequent-words/description/) from LeetCode.

> Given a non-empty list of words, return the *k* most frequent elements.
>
> Your answer should be sorted by frequency from highest to lowest. If  two words have the same frequency, then the word with the lower  alphabetical order comes first.
>
> **Example 1:**
>
> ```
> Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
> Output: ["i", "love"]
> Explanation: "i" and "love" are the two most frequent words.
>     Note that "i" comes before "love" due to a lower alphabetical order.
> ```
>
> 
>
> **Example 2:**
>
> ```
> Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
> Output: ["the", "is", "sunny", "day"]
> Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
>     with the number of occurrence being 4, 3, 2 and 1 respectively.
> ```
>
> 
>
> **Note:**
>
> 1. You may assume *k* is always valid, 1 ≤ *k* ≤ number of unique elements.
> 2. Input words contain only lowercase letters.
>
> 
>
> **Follow up:**
>
> 1. Try to solve it in *O*(*n* log *k*) time and *O*(*n*) extra space.



This is a simple problem if you know that [heaps are built in O(n)](https://stackoverflow.com/questions/9755721/how-can-building-a-heap-be-on-time-complexity) and that the `Counter()` class allows us to easily keep count of frequent elements in python. First we create the `word_freq` counter dictionary for word frequency, after which we create a list of tuples; we heapify this list into a min heap (negating `freq` with `-freq` allows us to sort like a max heap). After this, we return only the first k elements of the heap. The overall runtime complexity is O(k + 3n) where n is the length of the `words` list.

```python
from collections import Counter
import heapq

class Solution:
    def topKFrequent(self, words: List[str], k: int) -> List[str]:
        
        word_freq =  Counter(words)
        heap = [(-freq, word) for word, freq in word_freq.items()]
        heapq.heapify(heap)
        
        return [heapq.heappop(heap)[1] for _ in range(k)]
```

