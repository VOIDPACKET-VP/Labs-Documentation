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
	int current = 2, previous = 1;
	int sum = 2;

	while(current <= 4000000){
		current += previous;
		previous = current - previous;
		if (current % 2 == 0) sum += current;
	}

	std::cout << sum;
	
	return 0;
}
```
- Solution : 4613732