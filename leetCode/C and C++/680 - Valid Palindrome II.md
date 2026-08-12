---
platform: LeetCode
difficulty: Easy
date: 2026-08-12
---
# Description
Given a string `s`, return `true` _if the_ `s` _can be palindrome after deleting **at most one** character from it_.

**Example 1:**
	**Input:** s = "aba"
	**Output:** true

**Example 2:**
	**Input:** s = "abca"
	**Output:** true
	**Explanation:** You could delete the character 'c'.

**Example 3:**
	**Input:** s = "abc"
	**Output:** false

# Solution
- C++
```cpp
class Solution {
public:
    bool validPalindrome(string s) {
        int l = 0, r = s.length() - 1;
        while (l < r) {
            if (s[l] != s[r]) {
                return isPalindrome(s.substr(0, l) + s.substr(l + 1)) ||
                      isPalindrome(s.substr(0, r) + s.substr(r + 1));
            }
            r--;
            l++;
        }
        return true;
    }
private:
    bool isPalindrome(string s) {
        int l = 0, r = s.length() - 1;
        while (l < r) {
            if (s[l] != s[r]) {
                return false;
            }
            l++;
            r--;
        }
        return true;
    }
};
```

# Learned 
- Used the solution from [NeetCode](https://neetcode.io/solutions/valid-palindrome-ii) :
## 2. Two Pointers
### Intuition
Instead of blindly trying every removal, we can be smarter. Use two pointers starting from both ends of the string and move them inward. As long as characters match, keep going. When we find a mismatch, we know exactly where the problem is. At this point, we have only two choices: remove the left character or remove the right character. We check if either choice results in a palindrome for the remaining substring.

### Algorithm
1. Initialize two pointers: `l` at the start and `r` at the end of the string.
2. While `l < r`:
    - If `s[l] == s[r]`, move both pointers inward (`l++`, `r--`).
    - If they differ, we found the mismatch. Check two possibilities:
        - Skip the left character and check if `s[l+1...r]` is a palindrome.
        - Skip the right character and check if `s[l...r-1]` is a palindrome.
    - Return `true` if either substring is a palindrome.
3. If the loop completes without mismatches, the string is already a palindrome. Return `true`.

