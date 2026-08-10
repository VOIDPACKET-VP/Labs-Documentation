---
platform: LeetCode
difficulty: Medium
date: 2026-03-16
---
# Description
Design an algorithm to encode **a list of strings** to **a string**. The **encoded string** is then sent over the network and is **decoded** back to the **original list** of strings.

**Machine 1 (sender)** has the function:
```java
String encode(List<String> strs) {
    // ... your code
    return encoded_string;
}
```

**Machine 2 (receiver)** has the function:
```java
List<String> decode(String encoded_string) {
    // ... your code
    return decoded_strs;
}
```

So **Machine 1** does:
```java
String encoded_string = encode(strs);
```

and **Machine 2** does:
```java
List<String> decoded_strs = decode(encoded_string);
```

`decoded_strs` in Machine 2 should be the **same** as the input `strs` in Machine 1.

Implement the `encode` and `decode` methods.

**Example 1:**
```java
Input: strs = ["Hello","World"]

Output: ["Hello","World"]
```

**Explanation:**
```java
Solution solution = new Solution();
String encoded_string = solution.encode(strs);

// Machine 1 ---encoded_string---> Machine 2

List<String> decoded_strs = solution.decode(encoded_string);
```

**Example 2:**
```java
Input: strs = [""]

Output: [""]
```

- This challenge is for premium users on LeetCode, but you can solve it on [NeetCode's platform](https://neetcode.io/problems/string-encode-and-decode/question)

# Solution
- C++
```cpp
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
