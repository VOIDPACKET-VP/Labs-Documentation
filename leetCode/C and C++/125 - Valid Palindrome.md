---
platform: LeetCode
difficulty: Easy
date: 2026-08-12
---
# Description
A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` _if it is a **palindrome**, or_ `false` _otherwise_.

**Example 1:**
	**Input:** s = "A man, a plan, a canal: Panama"
	**Output:** true
	**Explanation:** "amanaplanacanalpanama" is a palindrome.

**Example 2:**
	**Input:** s = "race a car"
	**Output:** false
	**Explanation:** "raceacar" is not a palindrome.

**Example 3:**
	**Input:** s = " "
	**Output:** true
	**Explanation:** s is an empty string "" after removing non-alphanumeric characters.
	Since an empty string reads the same forward and backward, it is a palindrome.

# Solution
- C++
```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int left = 0;
        int right = s.length() - 1;
        while (left < right) {
            while (left < right && !std::isalnum(static_cast<unsigned char>(s[left]))) {
                left++;
            }

            while (left < right && !std::isalnum(static_cast<unsigned char>(s[right]))) {
                right--;
            }
  
            if (std::tolower(static_cast<unsigned char>(s[left])) !=
                std::tolower(static_cast<unsigned char>(s[right]))) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
};
```

# Learned 
- This was my initial solution :
```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        if (s == " ") return true;
        std::erase_if(s, [](unsigned char c) {
            return !std::isalnum(c);
        });
        std::string reversed = s;
        int i = 0;        
        int j = reversed.size() - 1;        
        while (i < reversed.size() / 2) {           
            std::swap(reversed[i], reversed[j]);           
            i++;            
            j--;        
        }
        if (reversed == s) return true;
        else return false;
    }
};
```

- But it fails on edge cases because it is case-sensitive, misses complex blank strings (like `", ."`), and wastes system resources by allocating extra memory to copy and manually reverse the string. 
- The other approach is better because it solves the case-sensitivity issue using `std::tolower`, handles all empty or non-alphanumeric inputs automatically, and runs significantly faster with **zero extra memory (O(1) space)** by using a ==two-pointer technique== to compare the characters from both ends in a single pass.

## Two Pointer
- Check the DSA Folder to learn more about it