---
layout: layouts/entry-detail.njk
title: LeetCode - 853
date: 2026-08-22
category: Programming
platform: LeetCode
difficulty: Medium
tags:
  - stack
  - Loops
  - Sorting
summary: Calculate car fleets
backLink: /writeups/
backLabel: Writeups
---
# Description 
There are `n` cars at given miles away from the starting mile 0, traveling to reach the mile `target`.

You are given two integer arrays `position` and `speed`, both of length `n`, where `position[i]` is the starting mile of the `ith` car and `speed[i]` is the speed of the `ith` car in miles per hour.

A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car.

A **car fleet** is a single car or a group of cars driving next to each other. The speed of the car fleet is the **minimum** speed of any car in the fleet.

If a car catches up to a car fleet at the mile `target`, it will still be considered as part of the car fleet.

Return the number of car fleets that will arrive at the destination.

**Example 1:**
	**Input:** target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]
	**Output:** 3
	**Explanation:**
	- The cars starting at 10 (speed 2) and 8 (speed 4) become a fleet, meeting each other at 12. The fleet forms at `target`.
	- The car starting at 0 (speed 1) does not catch up to any other car, so it is a fleet by itself.
	- The cars starting at 5 (speed 1) and 3 (speed 3) become a fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches `target`.

**Example 2:**
	**Input:** target = 10, position = [3], speed = [3]
	**Output:** 1
	**Explanation:**
	There is only one car, hence there is only one fleet.

**Example 3:**
	**Input:** target = 100, position = [0,2,4], speed = [4,2,1]
	**Output:** 1
	**Explanation:**
	- The cars starting at 0 (speed 4) and 2 (speed 2) become a fleet, meeting each other at 4. The car starting at 4 (speed 1) travels to 5.
	- Then, the fleet at 4 (speed 2) and the car at position 5 (speed 1) become one fleet, meeting each other at 6. The fleet moves at speed 1 until it reaches `target`.


# Solution
- C++
```cpp
class Solution {

public:

    int carFleet(int target, vector<int>& position, vector<int>& speed) {

        int n = position.size();

        if (n == 0) return 0;

  

        std::vector<std::pair<int, int>> cars;

        cars.reserve(n);

        for (int i = 0; i < n; ++i) {

            cars.emplace_back(position[i], speed[i]);

        }

        std::sort(cars.begin(), cars.end());

        std::stack<float> carStack;

  

        for (int i = n - 1; i >= 0; i--) {

            float duration = static_cast<float>(target - cars[i].first) / cars[i].second;

            if (carStack.empty() || duration > carStack.top()) {

                carStack.push(duration);

            }

        }

  

        return carStack.size();

    }

};
```

# Learned
