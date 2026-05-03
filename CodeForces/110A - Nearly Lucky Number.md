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

	long long n;
	int luckyDigitsNumber = 0;
	std::cin >> n;

	while (n) {
		if (n % 10 == 4 || n % 10 == 7) luckyDigitsNumber++;
		n /= 10;
	}

	if (luckyDigitsNumber == 4 || luckyDigitsNumber == 7) std::cout << "YES";
	else std::cout << "NO";

	return 0;
}
```