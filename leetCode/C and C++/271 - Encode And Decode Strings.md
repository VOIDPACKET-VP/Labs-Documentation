---
platform: LeetCode
difficulty: Medium
date: 2026-03-16
---
# Solution
- C++
```
class Solution {
public:
    string encode(vector<string>& strs) {
        std::string encoded_string = "";
        for (const std::string& s : strs) encoded_string += to_string(s.size()) + '#' + s;
        return encoded_string;
    }

    vector<string> decode(string s) {
        vector<string> decoded_string;
        int i = 0;
        while (i < s.size()) {
            size_t hashPosition = s.find('#', i);
            int len = stoi(s.substr(i, hashPosition - i));
            i = hashPosition + 1;
            decoded_string.push_back(s.substr(i, len));
            i += len;
        }
        return decoded_string;
    }
};
```
- The `to_string` is to transform an int to a string
- The `.find()` is to find something from a starting position `i`
- The `stoi` is to transform a string to an int
- 