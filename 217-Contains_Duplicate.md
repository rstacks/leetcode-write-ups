# 217. Contains Duplicate

[View on LeetCode](https://leetcode.com/problems/contains-duplicate/)

## Problem Description

Given an integer array <code>nums</code>, return <code>true</code> if any value appears
**at least twice** in the array, and return <code>false</code> if every element is distinct.

## Intuition

My immediate thought was to use a brute force solution. This would mean iterating over
every element in <code>nums</code>, then, for each element, iterating over the entire array
and checking for a match. There is a more efficient solution, however. I used a hash map where
the keys were the elements of <code>nums</code> and the values were the number of times the
element occurs in the array. This opens the door to a solution that only requires looping
over the array once.

## My Approach

I begin by creating an empty hash map to keep track of the number of occurrences of each
element in the array. Then, for every element in <code>nums</code>, I check if it is
already present in the hash map. If this is true, that means a duplicate was found, and
I can immediately return <code>true</code>. If the entire array is traversed successfully,
then there are no duplicates.

## Complexity

The **time complexity** is O(n). There is a single loop that iterates over the entire array.

The **space complexity** is O(n). In the worst case, the hash map created to track occurrences
will contain every element from <code>nums</code>.

## Code

```
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        # Use hashmap to keep track of element counts
        num_counts = {}
		
        # Loop over the array of nums
        for num in nums:
            if num_counts.get(num) == None:
                num_counts[num] = 1
            else:
                return True
		
        return False
```

## Alternative Approach
