# 238. Product of Array Except Self

[View on LeetCode](https://leetcode.com/problems/product-of-array-except-self/)

## Problem Description

Given an integer array <code>nums</code>, return *an array* <code>answer</code> *such that* <code>answer[i]</code> *is equal to the product of all the elements of* <code>nums</code> *except* <code>nums[i]</code>.

The product of any prefix or suffix of <code>nums</code> is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in <code>O(n)</code> time and without using the division operation.

## Intuition

This was an interesting problem. My first idea was to start by computing the product of every element in the array. I would then loop over the array and divide the computed product by the current element in order to get the value to append to the return array. However, as the problem description states, the division operator is not allowed. To keep my solution's time complexity within O(n), I decided to use two hash maps to store products of subarrays. I would then loop over <code>nums</code> and build the return array using one subarray product from each hash map.

## My Approach

I start by creating *two* hash maps. I then loop forward through the entire input array. As I do so, I fill up the *first* hash map where the keys are the indices of the input array and the values are a running product of every *preceding* element and the current element. I repeat this process a second time, this time looping backwards so that the *second* hash map contains running products of the current element and every *following* element. Finally, I loop forwards once more over the input array in order to build the return array. Every element in the return array is the product of one element from each of the two hash maps: 

1. the product of every element *preceding* the current element (first hash map)
2. the product of every element *following* the current element (second hash map)

## Complexity

The **time complexity** is O(n). There are 3 loops that each loop over the entire input array.

The **space complexity** is O(n). My solution uses 2 hash maps whose size matches that of the input array.

## Code

```
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        # Create return array
        ret = []

        # Create hash maps
        prod_map_forward = {}   # key:value is index:product from beginning through index
        prod_map_backward = {}  # key:value is index:product from end through index

        # Loop over the array to create products of subarrays going forward
        for i in range(len(nums)):
            if i == 0:
                prod_map_forward[i] = nums[i]
            else:
                prod_map_forward[i] = prod_map_forward[i-1] * nums[i]

        # Loop to create products going backwards
        for i in range(len(nums)-1, -1, -1):
            if i == len(nums)-1:
                prod_map_backward[i] = nums[i]
            else:
                prod_map_backward[i] = prod_map_backward[i+1] * nums[i]

        # Build the return array
        for i in range(len(nums)):
            forward_prod_loc = i - 1
            backward_prod_loc = i + 1

            if forward_prod_loc < 0:
                ret.append(prod_map_backward[backward_prod_loc])
            elif backward_prod_loc >= len(nums):
                ret.append(prod_map_forward[forward_prod_loc])
            else:
                ret.append(prod_map_forward[forward_prod_loc] * prod_map_backward[backward_prod_loc])
        
        return ret
```

## Alternative Approach

There is a way to complete this problem with a memory complexity of O(1). That solution would essentially be an "in-place" version of my solution. Instead of building two hash maps of subarray products, we can instead:

1. Loop forward over the input array and compute each of the subarray products, then append each product to the *return* array.
2. Loop backwards over the input array and compute the subarray products, then *multiply* each of them by their corresponding values in the return array.
