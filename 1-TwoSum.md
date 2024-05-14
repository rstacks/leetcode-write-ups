# 1. Two Sum

[View on LeetCode](https://leetcode.com/problems/two-sum/)

## Problem Description

Given an array of integers <code>nums</code> and an integer <code>target</code>, return *indices of the two numbers such that they add up to <code>target</code>*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

## Intuition

This problem can be solved easily through brute force, but to get a solution with a time complexity of O(n), I once again used a hash map. The hash map stores the elements of the input array as keys and those elements' indices as values. With this setup, I only need to loop over the input array once in order to find a pair of numbers that sum to <code>target</code>. 

## My Approach

There is a single loop that accesses every element in <code>nums</code>. On each iteration, I subtract the current element from <code>target</code> to determine what other value is _needed_. I then check if this other value is already in the hash map. If it is, then I have all the information I need, so I can return. Otherwise, I add the current element and its index to the hash map.

## Complexity

The **time complexity** is O(n). There is a single loop that traverses the input array.

The **space complexity** is O(n). My solution uses a hash map that, in the worst case, stores almost every element in the input array.

## Code

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        ret = []

        # Use hash map to track encountered nums and their indices
        addend_map = {}

        # Loop once over input array
        for i in range(len(nums)):
            other_num = target - nums[i]
            # Return if we've already encountered the other num
            if addend_map.get(other_num) != None:
                ret.append(addend_map[other_num])
                ret.append(i)
                return ret
            # Otherwise, add this num to hash map
            addend_map[nums[i]] = i
        
        return ret
```
