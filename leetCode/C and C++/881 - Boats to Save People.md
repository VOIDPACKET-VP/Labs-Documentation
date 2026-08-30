---
platform: LeetCode
difficulty: Medium
date: 2026-08-29
---
# Description
You are given an array `people` where `people[i]` is the weight of the `ith` person, and an **infinite number of boats** where each boat can carry a maximum weight of `limit`. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most `limit`.

Return _the minimum number of boats to carry every given person_.

**Example 1:**

**Input:** people = [1,2], limit = 3
**Output:** 1
**Explanation:** 1 boat (1, 2)

**Example 2:**

**Input:** people = [3,2,2,1], limit = 3
**Output:** 3
**Explanation:** 3 boats (1, 2), (2) and (3)

**Example 3:**

**Input:** people = [3,5,3,4], limit = 5
**Output:** 4
**Explanation:** 4 boats (3), (3), (4), (5)

# Solution
- C
```c
int cmp(const void* a, const void* b)

{

    return (*(int*)a - *(int*)b);

}

  
  

int numRescueBoats(int* people, int peopleSize, int limit) {

    qsort(people, peopleSize, sizeof(int), cmp);

  

    int boats = 0;

    int left = 0;

    int right = peopleSize - 1;

  

    while (left <= right)

    {

        if (left == right)

        {

            boats++;

            break;

        }

  

        if (people[left] + people[right] <= limit)

        {

            boats++;

            left++;

            right--;

        }

        else

        {

            boats++;

            right--;

        }

  

    }

  

    return boats;

}
```

# Learned
Keep it simple, here i tried to do some weird stuff, and the answer was way simple and very basic _Two Pointer_ challenge :
- Sort the array
- Use Two Pointers

This code is a bit slow due to the compare function i used, to optimize it use the `Counting Sort`

