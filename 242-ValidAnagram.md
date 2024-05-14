# 242. Valid Anagram

[View on LeetCode](https://leetcode.com/problems/valid-anagram/)

## Problem Description

Given two strings <code>s</code> and <code>t</code>, return <code>true</code> *if* <code>t</code> *is an anagram of* <code>s</code>, *and* <code>false</code> *otherwise*.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Intuition

My first idea was to convert both input strings to sets, then simply compare the sets. This does not work when there are
duplicate letters, however. Instead, I used two hash maps to keep track of the number of occurrences of each
letter in the two strings. I then compared these two hash maps to determine if the strings were anagrams.

## My Approach

I start by checking for length equality between the strings, because if the strings are not the same length, then I already know
they cannot be anagrams. I then build the two hash maps, one for each string. After building them, I then check
that all letters in string <code>s</code> exist in <code>t</code> and that that letter occurs the same number of times
within both strings. If at least one of these conditions is not true, the strings are not anagrams.

## Complexity

The **time complexity** is O(n), where **n** is the length of the two strings (both <code>s</code>
and <code>t</code> are known to have the same length after the initial length check). There are two loops that iterate over every letter in <code>s</code>.

The **space complexity** is O(n). There are two hash maps that contain all letters from each of the input strings.

## Code

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        # Length check
        if len(s) != len(t):
            return False

        # Build hash maps for strings; key:value is letter:count
        s_map = {}
        t_map = {}
        for i in range(len(s)):
            if s_map.get(s[i]) == None:
                s_map[s[i]] = -1
            if t_map.get(t[i]) == None:
                t_map[t[i]] = -1
            s_map[s[i]] += 1
            t_map[t[i]] += 1

        # Compare hash maps
        for letter in s_map.keys():
            if t_map.get(letter) == None:
                return False
            if s_map[letter] != t_map[letter]:
                return False

        return True
```

## Alternative Approach

Instead of using hash maps, we can simply **sort** both input strings, then do an equality check
between the sorted versions of the input strings to determine if they are anagrams. This approach can be
more memory efficient (depending on the sorting algorithm used), but it will come at the cost of
time complexity, which will be O(nlog(n)) or O(n<sup>2</sup>) (again, depending on the sorting algorithm).
