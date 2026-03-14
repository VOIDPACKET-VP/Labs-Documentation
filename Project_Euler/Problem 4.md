---
platform: Project Euler
difficulty: "0"
date: 2026-03-14
---
# Solution
- Code in C++
```
#include <iostream>

bool isPalindrome(int n) {
	int original = n;
	int reversed = 0;

	while(n > 0) {
		reversed = reversed * 10 + (n % 10);
		n /= 10;
	}

	return original == reversed;
}

int main() {

	int maxPoli = 0;
	int factor1 = 0, factor2 = 0;

	for (int i = 999; i >= 100; i--) {
		if (i * i <= maxPoli) break;

		for (int j = i; j >= 100; j--) {
			int product = i * j;
			if (product <= maxPoli) break;
			if (isPalindrome(product)) {
				maxPoli = product;
			}
		}
	}

	std::cout << maxPoli;

	return 0;
}
```
- Solution :  906609