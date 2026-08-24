---
platform: LeetCode
difficulty: Easy
date: 2026-08-20
---
# Description
Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

**Example 1:**
**Input:** s = "()"
**Output:** true

**Example 2:**
**Input:** s = "()[]{}"
**Output:** true

**Example 3:**
**Input:** s = "(]"
**Output:** false

**Example 4:**
**Input:** s = "([])"
**Output:** true

**Example 5:**
**Input:** s = "([)]"
**Output:** false

# Solution
- C++
This solution takes 3ms to run because it uses unordered_map
```cpp
class Solution {
public:
    bool isValid(string s) {
        std::stack<char> brackets;
        std::unordered_map<char, char> closersAndOpeners = {
            {')', '('},
            {']', '['},
            {'}', '{'}
        };

        for (char ch : s) {
            if (ch == '(' || ch == '[' || ch == '{') brackets.push(ch);
            else {
                if (!brackets.empty() && closersAndOpeners[ch] == brackets.top())
                    brackets.pop();
                else return false;
            }
        }

        if (brackets.empty()) return true;
        else return false;
    }
};
```

This one doesn't use unordered_map, and it uses basic && || logic
```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for(char c : s){
            if(c=='('|| c=='['||c=='{'){
                st.push(c);
            }else{
                if(st.empty()){
                    return false;
                }
                char top = st.top();
                if((c == ')' && top != '(') ||
                (c == ']' && top != '[') ||
                (c == '}' && top != '{')){
                    return false;
                }
                st.pop();
            }
        }
        return st.empty();
    }
};
```

# Learned 
Nothing.