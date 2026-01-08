# Group Anagrams

## Problem
Given an array of strings, group the anagrams together.
You can return the answer in any order.

## Intuition
Anagrams contain the same characters with the same frequency.
If two strings have identical character counts, they belong to the same group.

## Approach
- Use a hash map where the key represents character frequency
- For each string, compute its frequency count
- Use the frequency representation as the key
- Append the string to the corresponding group

## Example
Input: ["eat","tea","tan","ate","nat","bat"]  
Output: [["eat","tea","ate"],["tan","nat"],["bat"]]

## Time Complexity
O(n * k), where k is the length of the string

## Space Complexity
O(n * k)

## Notes
Sorting each string is another possible approach but increases time complexity.
