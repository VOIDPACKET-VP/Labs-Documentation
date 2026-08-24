---
layout: layouts/entry-detail.njk
title: LeetCode - 735
date: 2026-08-21
category: Programming
platform: LeetCode
difficulty: Medium
tags:
  - stack
  - conditionals
  - Loops
summary: Asteroid Collision
backLink: /writeups/
backLabel: Writeups
---
# Description 
We are given an array `asteroids` of integers representing asteroids in a row. The indices of the asteroid in the array represent their relative position in space.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**
	**Input:** asteroids = [5,10,-5]
	**Output:** [5,10]
	**Explanation:** The 10 and -5 collide resulting in 10. The 5 and 10 never collide.

**Example 2:**
	**Input:** asteroids = [8,-8]
	**Output:** []
	**Explanation:** The 8 and -8 collide exploding each other.

**Example 3:**
	**Input:** asteroids = [10,2,-5]
	**Output:** [10]
	**Explanation:** The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.

**Example 4:**
	**Input:** asteroids = [3,5,-6,2,-1,4]​​​​​​​
	**Output:** [-6,2,4]
	**Explanation:** The asteroid -6 makes the asteroid 3 and 5 explode, and then continues going left. On the other side, the asteroid 2 destroys -1. Since 2 and 4 are both moving right, they never collide.


# Solution
- C++
```cpp
class Solution {
public:
    vector<int> asteroidCollision(vector<int>& asteroids) {
        std::vector<int> stack;
        for (int& aster : asteroids) {

            // we check if there will be a battle
            while (aster < 0 && !stack.empty() && stack.back() > 0) {
                // The battle result : the one with smallest size gets destroyed
                // remember : aster < 0 and stack.back() > 0
                int diff = aster + stack.back();
                if (diff < 0) {
                    stack.pop_back();
                } else if (diff > 0) {
                    aster = 0;
                } else {
                    aster = 0;
                    stack.pop_back();
                }
            }
  
            // If it survived all battles, she gets added to the safe zone
            if (aster != 0) stack.push_back(aster);
        }
        return stack;
    }
};
```

# Learned
Make sure to think about edge cases, like in this case :
- If the first rock < 0 and the second > 0 the won't collide, but if it's the opposite they will collide
