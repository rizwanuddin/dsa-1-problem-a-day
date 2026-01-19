# Product of Array Except Self

## Problem
Given an integer array `nums`, construct an array `res` such that:
- `res[i]` is the product of all elements in `nums` except `nums[i]`
- Division is not allowed

---

## Intuition
For any index `i`, the product of all elements except `nums[i]` can be split into two independent parts:
- Product of all elements to the **left** of `i`
- Product of all elements to the **right** of `i`

So:

res[i] = (left product) * (right product)


This avoids division and handles zeros correctly.

---

## Approach
1. Create a result array `res` of size `n`.
2. **Prefix pass (left → right)**:
   - Maintain a running product `prefix`.
   - Store the product of all elements before index `i` in `res[i]`.
3. **Postfix pass (right → left)**:
   - Maintain a running product `postfix`.
   - Multiply the product of all elements after index `i` into `res[i]`.
4. Return `res`.

---

## Example
Input:

nums = [10, 3, 5, 6, 2]


Prefix products:

[1, 10, 30, 150, 900]


Postfix multiplication:

[180, 600, 360, 300, 900]


Output:

[180, 600, 360, 300, 900]


---

## Code
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];

        int prefix = 1;
        for (int i = 0; i < n; i++) {
            res[i] = prefix;
            prefix *= nums[i];
        }

        int postfix = 1;
        for (int i = n - 1; i >= 0; i--) {
            res[i] *= postfix;
            postfix *= nums[i];
        }

        return res;
    }
}

Time Complexity

O(n)

Space Complexity

O(1)

(ignoring the output array)
Notes

    Initializing prefix and postfix to 1 is crucial.

    Works correctly with zeros:

        One zero → only one non-zero result.

        Two or more zeros → all results are zero.

    Division-based solutions are incorrect and usually disallowed.
