---
platform: LeetCode
difficulty: Medium
date: 2026-08-09
---
# Description
You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can sell and buy the stock multiple times on the **same day**, ensuring you never hold more than one share of the stock.

Find and return _the **maximum** profit you can achieve_.

**Example 1:**
	**Input:** prices = [7,1,5,3,6,4]
	**Output:** 7
	**Explanation:** Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
	Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
	Total profit is 4 + 3 = 7.

**Example 2:**
	**Input:** prices = [1,2,3,4,5]
	**Output:** 4
	**Explanation:** Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
	Total profit is 4.

**Example 3:**
	**Input:** prices = [7,6,4,3,1]
	**Output:** 0
	**Explanation:** There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.

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