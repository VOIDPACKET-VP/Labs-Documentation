---
platform: Codeforces
difficulty: "800"
date: 2026-05-05
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

	if (n % 2 != 0) {
		std::cout << -1;
	} else {
		
		for (int i = 1; i <= n; i++) {
			if (i % 2 != 0) std::cout << i + 1 << " ";
			else std::cout << i - 1 << " ";
		}
	}

	return 0;
}
```