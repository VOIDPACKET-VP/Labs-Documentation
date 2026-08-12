---
platform: LeetCode
difficulty: Hard
date: 2026-08-11
---
# Description
Given an unsorted integer array `nums`. Return the _smallest positive integer_ that is _not present_ in `nums`.

You must implement an algorithm that runs in `O(n)` time and uses `O(1)` auxiliary space.

**Example 1:**
	**Input:** nums = [1,2,0]
	**Output:** 3
	**Explanation:** The numbers in the range [1,2] are all in the array.

**Example 2:**
	**Input:** nums = [3,4,-1,1]
	**Output:** 2
	**Explanation:** 1 is in the array but 2 is missing.

**Example 3:**
	**Input:** nums = [7,8,9,11,12]
	**Output:** 1
	**Explanation:** The smallest positive integer 1 is missing.

# Solution
- C++
```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        int i = 0;

        while (i < nums.size()) {
            if (nums[i] <= 0 || nums[i] > nums.size()) {
                i++;
                continue;
            }  
            int idx = nums[i] - 1;
            if (nums[i] != nums[idx]) std::swap(nums[i], nums[idx]);
            else i++;
        }

        for (int i = 0; i < nums.size(); i++) {
            if (nums[i] != i + 1) return i + 1;
        }

        return nums.size() + 1;
    }
};
```

# Learned 
- I really couldn't find the solution without reading [NeetCode's algorithm Solutions](https://neetcode.io/solutions/first-missing-positive), and i ended up using the ==Cycle Sort== Algorithm

## Cycle Sort
- We basically use the array as its own hasp map. The goal is to place each number at its "correct" index: value `1` at index `0`, value `2` at index `1`, and so on

## Algorithm
1. Iterate through the array with index `i`:
    - While `nums[i]` is in range `[1, n]` and `nums[i] != nums[nums[i] - 1]`:
        - Swap `nums[i]` with `nums[nums[i] - 1]`.
2. Scan the array:
    - Return `i + 1` for the first index where `nums[i] != i + 1`.
3. If all positions are correct, return `n + 1`.

## std::swap
- The most efficient and standard way to exchange two values in C++
- So instead of using manual swapping :
	- Temporary Variable
	- Arithmetic
	- Bitwise XOR
- We use `std::swap()` 

> it's defined in the `<utility>` header (or `<algorithm>` in older standards)