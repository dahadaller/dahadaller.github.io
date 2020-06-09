Title: 373 Find K Pairs with Smallest Sums (David)
Date: 2020-06-09 17:00
Authors: David Hadaller
Tags: Week 2, LeetCode, Draft



Here we solve the [Find K Pairs with Smallest Sums](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/) problem from LeetCode:



> You are given two integer arrays **nums1** and **nums2** sorted in ascending order and an integer **k**.
>
> Define a pair **(u,v)** which consists of one element from the first array and one element from the second array.
>
> Find the k pairs **(u1,v1),(u2,v2) ...(uk,vk)** with the smallest sums.
>
> **Example 1:**
>
> ```
> Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
> Output: [[1,2],[1,4],[1,6]] 
> Explanation: The first 3 pairs are returned from the sequence: 
>              [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
> ```
>
> **Example 2:**
>
> ```
> Input: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
> Output: [1,1],[1,1]
> Explanation: The first 2 pairs are returned from the sequence: 
>              [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
> ```
>
> **Example 3:**
>
> ```
> Input: nums1 = [1,2], nums2 = [3], k = 3
> Output: [1,3],[2,3]
> Explanation: All possible pairs are returned from the sequence: [1,3],[2,3]
> ```



I'm not sure if there's a more efficient solution to this problem. What I have done hear is produce a list of all possible `n1`, `n2` combinations and their sums, and heapified the list by the sum. Then I pop `k` elements off the heap. This runs in O(n^2), but I couldn't think of a way to do it quicker.

```python
import heapq

class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:

        if not nums1 or not nums2:
            return []

        heap = [(n1 + n2, n1, n2) for n1 in nums1 for n2 in nums2]
        heapq.heapify(heap)
        l = len(heap) if k > len(heap) else k
        return [heapq.heappop(heap)[1:] for _ in range(l)]
        
```

