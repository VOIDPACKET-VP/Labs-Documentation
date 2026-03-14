---
platform: Codeforces
difficulty: "-"
date: 2026-03-14
---
# Solution
- C++
```
#include <iostream>

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(NULL);

    int t;
    std::cin >> t;

    while (t--) {
        int n;
        std::cin >> n;
        int board[10001] = { 0 };
        bool arrange = true;

        for (int i = 0; i < n * n; i++) {
            int color;
            std::cin >> color;
            board[color]++;
            if (board[color] > n * (n - 1)) arrange = false;
        }
        if (arrange) std::cout << "Yes\n";
        else std::cout << "No\n";
    }
    return 0;
}
```