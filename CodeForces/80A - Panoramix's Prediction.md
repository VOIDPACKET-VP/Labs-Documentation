---
platform: Codeforces
difficulty: "800"
date: 2026-05-03
---
# Solution
- C++
```cpp
#include <iostream>
#include <vector>

int main() {

	std::ios::sync_with_stdio(false);
	std::cin.tie(NULL);

	int n, m;
	std::cin >> n >> m;
	std::vector<bool> is_prime(51, true);
	is_prime[0] = is_prime[1] = false;

	for (int i = 2; i * i <= 50; i++) { // i * i : This is an optimization based on a mathematical fact: If a number \(x\) has a factor, at least one of those factors must be less than or equal to sqrt(x)
		if (is_prime[i]) {
			for (int y = i * i; y <= 50; y += i) {
				is_prime[y] = false;
			}
		}
	}

	int next_prime = -1; // dummy value that is clearly impossible as a real answer.
	for (int i = n + 1; i <= 50; i++) {
		if (is_prime[i]) {
			next_prime = i;
			break;
		} 
	}

	if (next_prime == m) std::cout << "YES";
	else std::cout << "NO";

	return 0;
}
```