---
platform: LeetCode
difficulty: Medium
date: 2026-08-16
---
# Description
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int value)` pushes the element `value` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

**Example 1:**

**Input**
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

**Output**
[null,null,null,null,-3,null,0,-2]

**Explanation**
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2

# Solution
- C++
```cpp
class MinStack {
    std::vector<int> arrayStack;
    std::vector<int> minStack;

public:
    MinStack() {
    
    }
    
    void push(int value) {
        arrayStack.push_back(value);
        if (minStack.empty() || value <= minStack.back()) {
            minStack.push_back(value);
        } else {
            minStack.push_back(minStack.back());
        }
    }

    void pop() {
        if (!arrayStack.empty()) {
            arrayStack.pop_back();
            minStack.pop_back();
        }
    }
    
    int top() {
        if (!arrayStack.empty()) return arrayStack[arrayStack.size() - 1];
        return -1;
    }

    int getMin() {
        if (!minStack.empty()) {
            return minStack.back();
        }
        return -1;
    }
};
```

# Learned 
Not much really, it's just a bit of logic