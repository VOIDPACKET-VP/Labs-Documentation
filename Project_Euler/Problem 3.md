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
    long long n = 600851475143LL;
    long long largest_f = 0;

    while (n % 2 == 0) {
        largest_f = 2;
        n /= 2;
    }

    for (long long i = 3; i * i <= n; i += 2) {
        while (n % i == 0) {
            largest_f = i;
            n /= i; 
        }
    }

    if (n > 1) {
        largest_f = n;
    }

    std::cout << largest_f;

    return 0;
}
```
- Solution : 6857 