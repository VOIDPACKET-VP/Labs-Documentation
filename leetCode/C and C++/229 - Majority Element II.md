---
platform: LeetCode
difficulty: Medium
date: 2026-08-09
---
# Description
Given an integer array of size `n`, find all elements that appear more than `⌊n / 3⌋` times.

**Example 1:**
	**Input:** nums = [3,2,3]
	**Output:** [3]

**Example 2:**
	**Input:** nums = [1]
	**Output:** [1]

**Example 3:**
	**Input:** nums = [1,2]
	**Output:** [1,2]

# Solution
- C++
```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        size_t appearanceCount = nums.size() / 3; // because nums.size() returns a size_t type (unsigned int)
        std::unordered_map<int, int> resultMap;
        std::vector<int> resultArr;
        for (auto& num : nums) {
            if (!resultMap.contains(num)) resultMap[num] = 1;
            else resultMap[num]++;  
            bool exist = false;
            if (resultMap.at(num) > appearanceCount) {
                for (int i = 0; i < resultArr.size(); i++) {
                    if (resultArr[i] == num){
                        exist = true;
                        break;
                    }
                }
                if (!exist) {
                    resultArr.push_back(num);
                    exist = false;
                }
            }
        }
        return resultArr;
    }
};
```

# Learned 
## size_t
- In C++, declaring `size_t appearanceCount = nums.size() / 3;` is highly recommended because `nums.size()` returns an unsigned `size_t` type, and matching this type prevents dangerous signed-to-unsigned mismatches. Forcing this value into a standard signed `int` introduces two critical risks: first, it can trigger an integer overflow if the container holds more than 2 billion elements, which silently flips the count into a negative number; second, it can cause severe logic bugs during downstream comparisons, as C++ will implicitly convert negative signed integers into massive unsigned values, causing conditional checks to fail unexpectedly.

## Notes on my solution
- This code uses an intuitive ==**Frequency Map algorithm**==, but it runs slowly at **O(N²) time complexity** due to a nested loop that constantly scans the result array for duplicates. We can easily optimize this to **O(N) time** by simplifying the map counting syntax (`resultMap[num]++`) and waiting until the end of the program to run a single, separate loop to filter out the qualifying elements. While this hash map fix is highly efficient, the ultimate interview solution for this specific LeetCode problem uses the ==**Boyer-Moore Voting Algorithm**==, which tracks only two candidate variables to drop your memory usage down to **O(1) constant space**.