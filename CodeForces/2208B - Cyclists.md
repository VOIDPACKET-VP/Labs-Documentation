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

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(NULL);

    int t;
    std::cin >> t;
    while (t--) {
        int n, k, p, m;
        std::cin >> n >> k >> p >> m;

        std::vector<int> deck(n);
        for (int i = 0; i < n; i++) {
            std::cin >> deck[i];
        }

        int target_idx = p - 1;
        int played = 0;

        while (true) {
            if (target_idx < k) {
                if (m >= deck[target_idx]) {
                    m -= deck[target_idx];
                    played++;

                    int val = deck[target_idx];
                    deck.erase(deck.begin() + target_idx);
                    deck.push_back(val);

                    target_idx = n - 1;
                } else {
                    break;
                }
            } else {
                int min_idx = 0;
                for (int i = 1; i < k; i++) {
                    if (deck[i] < deck[min_idx]) {
                        min_idx = i;
                    }
                }

                if (m >= deck[min_idx]) {
                    m -= deck[min_idx];
                    int val = deck[min_idx];
                    deck.erase(deck.begin() + min_idx);
                    deck.push_back(val);

                    target_idx--;
                } else {
                    break;
                }
            }
        }
        std::cout << played << "\n";
    }
    return 0;
}
```