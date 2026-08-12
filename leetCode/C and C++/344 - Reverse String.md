---
platform: LeetCode
difficulty: Easy
date: 2026-08-11
---
# Description
Write a function that reverses a string. The input string is given as an array of characters `s`.

You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

**Example 1:**
	**Input:** s = ["h","e","l","l","o"]
	**Output:** ["o","l","l","e","h"]

**Example 2:**
	**Input:** s = ["H","a","n","n","a","h"]
	**Output:** ["h","a","n","n","a","H"]

# Solution
- C++
```c++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int i = 0;
        int j = s.size() - 1;
        while (i < s.size() / 2) {
            std::swap(s[i], s[j]);
            i++;
            j--;
        }
    }
};
```

# Learned
- Nothing, it was pretty easy, plus i got to use the `std::swap` which i just learned in the challenge before this one (41)