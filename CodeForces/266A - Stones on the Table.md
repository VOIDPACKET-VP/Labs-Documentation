---
platform: Codeforces
difficulty: "800"
date: 2026-05-03
---
# Solution
- C++
```cpp
#include <iostream>

int main() {

	std::ios::sync_with_stdio(false);
	std::cin.tie(NULL);

	int n;
	std::cin >> n;
	std::string s;
	std::cin >> s;

	int minNumber = 0;

	for (int i = 0; i < s.length() - 1; i++) {
		if (s[i + 1] == s[i]) minNumber++;
	}

	std::cout << minNumber;

	return 0;
}
```