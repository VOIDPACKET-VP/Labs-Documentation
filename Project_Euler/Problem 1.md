---
platform: Project Euler
difficulty: "0"
date: 2026-03-14
---
# Solution
- Code in C++
```
#include <iostream>

int main() {

	int max = 1000;
	int sum = 0;

	for (int i = 0; i < max; i++) {
		if (i % 3 == 0 || i % 5 == 0) sum += i;
	}

	std::cout << sum;
	return 0;
}
```
- Solution : 233168