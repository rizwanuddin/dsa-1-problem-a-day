# Top K Frequent Elements

## Problem
Given an integer array `nums` and an integer `k`, return the `k` most frequent elements.
The answer can be returned in any order.

### Example
Input: nums = [1,1,1,2,2,3], k = 2  
Output: [1,2]

---

## Intuition
Instead of sorting elements by frequency, we can use **bucket sort**.
The frequency of an element cannot exceed the length of the array, which makes
bucket indexing efficient.

---

## Approach (Bucket Sort)

1. Count the frequency of each number using a hashmap.
2. Create a bucket array where:
   - index = frequency
   - value = list of numbers with that frequency
3. Traverse the bucket array from highest frequency to lowest.
4. Collect elements until `k` results are gathered.

This avoids sorting and improves performance.

---

## Java Solution

```java
import java.util.*;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        List<Integer>[] bucket = new List[nums.length + 1];
        Map<Integer, Integer> frequencyMap = new HashMap<>();

        for (int n : nums) {
            frequencyMap.put(n, frequencyMap.getOrDefault(n, 0) + 1);
        }

        for (int key : frequencyMap.keySet()) {
            int frequency = frequencyMap.get(key);
            if (bucket[frequency] == null) {
                bucket[frequency] = new ArrayList<>();
            }
            bucket[frequency].add(key);
        }

        int[] res = new int[k];
        int counter = 0;

        for (int pos = bucket.length - 1; pos >= 0 && counter < k; pos--) {
            if (bucket[pos] != null) {
                for (int val : bucket[pos]) {
                    res[counter++] = val;
                    if (counter == k) break;
                }
            }
        }

        return res;
    }
}
Time Complexity

O(n)
Counting frequencies and bucket traversal are linear.

Space Complexity

O(n)
Extra space for hashmap and bucket array.
Notes

Bucket sort is effective when frequency bounds are known.

This approach avoids O(n log n) sorting.
