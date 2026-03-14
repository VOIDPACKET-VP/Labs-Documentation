---
platform: Codeforces
difficulty: "-"
date: 2026-03-14
---
# Solution
- C++
```
#include <iostream>
#include <vector>
#include <iomanip>
#include <algorithm>

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(NULL);

    int t;
    std::cin >> t;
    while (t--) {
        int n;
        std::cin >> n;
        std::vector<double> c(n), p(n);
        for (int i = 0; i < n; i++) {
            std::cin >> c[i] >> p[i];
        }

        double max_points = 0.0;

        for (int i = n - 1; i >= 0; i--) {
            double leave_it = max_points;
            double take_it = c[i] + max_points * (1.0 - p[i] / 100.0);

            max_points = std::max(leave_it, take_it);
        }

        std::cout << std::fixed << std::setprecision(10) << max_points << "\n";
    }
    return 0;
}
```