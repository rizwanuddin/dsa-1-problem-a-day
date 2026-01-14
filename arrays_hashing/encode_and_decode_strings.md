# Encode and Decode Strings

## Problem
Design an algorithm to encode a list of strings into a single string and decode
it back to the original list of strings.

The encoded string must be safely decodable even if the strings contain
special characters like `#`.

---

## Intuition
Using a delimiter alone is unsafe because the delimiter may appear inside
the strings themselves.

To make decoding unambiguous:
- Store the **length** of each string
- Follow it with a delimiter (`#`)
- Then store the string itself

This way, decoding always knows **exactly how many characters to read**.

---

## Encoding Strategy
For each string `s`:
1. Append `length(s)`
2. Append `#`
3. Append `s`

Example: ["leet", "code"] → "4#leet4#code"

---

## Decoding Strategy
1. Read digits until `#` → this gives the string length
2. Convert length to integer
3. Read the next `length` characters
4. Repeat until the end of the encoded string

---

## Java Solution

```java
import java.util.*;

class Solution {

    // Encode list of strings into a single string
    public String encode(List<String> strs) {
        StringBuilder res = new StringBuilder();
        for (String s : strs) {
            res.append(s.length()).append('#').append(s);
        }
        return res.toString();
    }

    // Decode the encoded string back to list of strings
    public List<String> decode(String str) {
        List<String> res = new ArrayList<>();
        int i = 0;

        while (i < str.length()) {
            int j = i;

            // Find the delimiter '#'
            while (str.charAt(j) != '#') {
                j++;
            }

            int length = Integer.parseInt(str.substring(i, j));
            int start = j + 1;
            int end = start + length;

            res.add(str.substring(start, end));
            i = end;
        }

        return res;
    }
}

Time Complexity

Encoding: O(n)

Decoding: O(n)

Where n is the total number of characters across all strings.


Space Complexity

O(n) for the encoded string and decoded output.

Notes

Length-based encoding avoids delimiter collision.

This approach is commonly used in serialization and system design problems.

Java uses StringBuilder because strings are immutable.
