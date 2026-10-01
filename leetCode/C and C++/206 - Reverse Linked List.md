---
platform: LeetCode
difficulty: Easy
date: 2026-09-09
---
# Description
Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [5,4,3,2,1]

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

**Input:** head = [1,2]
**Output:** [2,1]

**Example 3:**

**Input:** head = []
**Output:** []

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

# Solution
- C++
```cpp
class Solution {

public:

    ListNode* reverseList(ListNode* head) {

        ListNode* prev = nullptr;

        ListNode* current = head;

        ListNode* nextNode = nullptr;

  

        while (current != nullptr) {

            nextNode = current->next;

            current->next = prev;      

            prev = current;            

            current = nextNode;        

        }

        return prev;

    }

};
```

# Learned 
Nothing.