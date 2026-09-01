---
platform: LeetCode
difficulty: Hard
date: 2026-09-01
---
# Description
Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:** height = [0,1,0,2,1,0,1,3,2,1,2,1]
**Output:** 6
**Explanation:** The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

**Example 2:**

**Input:** height = [4,2,0,3,2,5]
**Output:** 9

**Constraints:**

- `n == height.length`
- `1 <= n <= 2 * 104`
- `0 <= height[i] <= 105`

# Solution
- C
```c
int trap(int* height, int heightSize)

{

    int left = 0;

    int right = heightSize - 1;

    int maxRight = height[right];

    int maxLeft = height[left];

    int trappedWater = 0;

  

    while (left < right)

    {

        if (maxLeft < maxRight)

        {

            left++;

            maxLeft = maxLeft > height[left] ? maxLeft : height[left];

            trappedWater += maxLeft - height[left];

        }

        else

        {

            right--;

            maxRight = maxRight > height[right] ? maxRight : height[right];

            trappedWater += maxRight - height[right];

        }

  

    }

  

    return trappedWater;

}
```

# Learned
Identify all key role factors, lay them down, and think a little 