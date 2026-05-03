---
platform: Codeforces
difficulty: "800"
date: 2026-05-03
---
# Solution
- C++
```cpp
#include <iostream>
#include <string>

int main() {

	std::ios::sync_with_stdio(false);
	std::cin.tie(NULL);

	std::string first;
	std::string second;
	std::string result;

	std::cin >> first;
	std::cin >> second;

	for (int i = 0; i < first.length(); i++) {
		if (first[i] == second[i]) result.push_back('0');
		else result.push_back('1');
	}

	std::cout << result << std::endl;

	return 0;
}
```