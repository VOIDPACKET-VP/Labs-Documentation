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

	int k, l, m, n, d;
	int harmed = 0;
	std::cin >> k >> l >> m >> n >> d;

	for (int i = 1; i <= d; i++) {
		if (i % k == 0 || i % l == 0 || i % m == 0 || i % n == 0) harmed++;
	}

	std::cout << harmed;

	return 0;
}
```

- Basically all we had to do is check is every dragon is a multiple of one of the conditions