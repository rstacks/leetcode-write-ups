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
