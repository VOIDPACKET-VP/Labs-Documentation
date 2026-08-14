---
platform: LeetCode
difficulty: Easy
date: 2026-08-14
---
# Description
You are given two strings `word1` and `word2`. Merge the strings by adding letters in alternating order, starting with `word1`. If a string is longer than the other, append the additional letters onto the end of the merged string.

Return _the merged string._

**Example 1:**
	**Input:** word1 = "abc", word2 = "pqr"
	**Output:** "apbqcr"
	**Explanation:** The merged string will be merged as so:
	word1:  a   b   c
	word2:    p   q   r
	merged: a p b q c r

**Example 2:**
	**Input:** word1 = "ab", word2 = "pqrs"
	**Output:** "apbqrs"
	**Explanation:** Notice that as word2 is longer, "rs" is appended to the end.
	word1:  a   b 
	word2:    p   q   r   s
	merged: a p b q   r   s

**Example 3:**
	**Input:** word1 = "abcd", word2 = "pq"
	**Output:** "apbqcd"
	**Explanation:** Notice that as word1 is longer, "cd" is appended to the end.
	word1:  a   b   c   d
	word2:    p   q 
	merged: a p b q c   d

# Solution
- C++
```cpp
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        std::string result;
        result += word1[0];
        int i1 = 1, i2 = 0;

        while (i1 < word1.size() && i2 < word2.size()) {
            result += word2[i2];
            i2++;
            result += word1[i1];
            i1++;
        }

        if (i1 < word1.size()) result += word1.substr(i1);
        if (i2 < word2.size()) result += word2.substr(i2);
        return result;
    }
};
```

# Learned 
- Nothing, it was pretty easy

