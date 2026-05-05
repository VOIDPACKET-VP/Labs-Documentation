---
platform: Codeforces
difficulty: "800"
date: 2026-05-05
---
# Solution
- C++
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>
int main() {

	std::ios::sync_with_stdio(false);
	std::cin.tie(NULL);

	int n;
	std::cin >> n;
	std::vector<int> soldiers(n);

	int minSeconds = 0;

	for (int i = 0; i < n; i++) {
		std::cin >> soldiers[i];
	}

	auto max = std::max_element(soldiers.begin(), soldiers.end());
	int max_idx = std::distance(soldiers.begin(), max);

	minSeconds = max_idx;

	auto min = std::min_element(soldiers.rbegin(), soldiers.rend());
	int min_idx = std::distance(soldiers.begin(), min.base()) - 1;

	minSeconds += (n - 1) - min_idx;

	if (max_idx > min_idx) minSeconds--;

	std::cout << minSeconds;

	return 0;
}
```

- This is quite a good challenge, it got me in contact with new functions :
	- `std::min_element` and `std::max_element` By including `<algorithm>`
		- To find the max and min elements
		- They return pointers, so we used `auto`
	- `std::distance` by including `<iterator>`
		- To find the indexes

- When i used `std::min_element` i needed to find the last occurrence so i used `Reverse iterators` which searches from right to left
	- You can see we added a little `r` before `begin` and `end`
