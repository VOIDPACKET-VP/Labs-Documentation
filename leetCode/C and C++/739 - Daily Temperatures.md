---
layout: layouts/entry-detail.njk
title: LeetCode - 739
date: 2026-08-22
category: Programming
platform: LeetCode
difficulty: Medium
tags:
  - stack
  - conditionals
  - Loops
summary: Record Temp rises
backLink: /writeups/
backLabel: Writeups
---
# Description 
Given an array of integers `temperatures` represents the daily temperatures, return _an array_ `answer` _such that_ `answer[i]` _is the number of days you have to wait after the_ `ith` _day to get a warmer temperature_. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**
	**Input:** temperatures = [73,74,75,71,69,72,76,73]
	**Output:** [1,1,4,2,1,1,0,0]

**Example 2:**
	**Input:** temperatures = [30,40,50,60]
	**Output:** [1,1,1,0]

**Example 3:**
	**Input:** temperatures = [30,60,90]
	**Output:** [1,1,0]


# Solution
- C++
```cpp
class Solution {

public:

    vector<int> dailyTemperatures(vector<int>& temperatures) {

        std::vector<int> tillRise(temperatures.size(), 0);

        stack<pair<int, int>> stack; // pair: {temp, index}

  

        for (int i = 0; i < temperatures.size(); i++) {

            int t = temperatures[i];

            while (!stack.empty() && t > stack.top().first) {

                auto pair = stack.top(); // store it

                stack.pop(); // get rid of it from the stack

                tillRise[pair.second] = i - pair.second;

            }

            stack.push({t, i});

        }

  

        return tillRise;

    }

};
```

# Learned
I really don't know what i learned