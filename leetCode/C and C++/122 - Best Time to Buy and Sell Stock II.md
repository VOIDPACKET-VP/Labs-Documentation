---
platform: LeetCode
difficulty: Medium
date: 2026-08-11
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
    int maxProfit(vector<int>& prices) {
        int profit = 0;
        for (int i = 1; i < prices.size(); i++) {
            if (prices[i] > prices[i - 1]) {
                profit += prices[i] - prices[i - 1];
            }
        }
        return profit;
    }
};
```

# Learned 
## Greedy Approach
- The greedy approach works because holding a stock over multiple days of steady growth yields the exact same profit as buying and selling it every single day across that same period.

- Because the problem allows same-day trading with zero transaction fees, you do not need to look ahead to find the absolute peaks and valleys; you simply harvest every immediate, consecutive-day price increase, which mathematically accumulates into the maximum possible global profit while automatically ignoring all downward drops.

> Greedy approaches think about now, and don't worry about tomorrow

