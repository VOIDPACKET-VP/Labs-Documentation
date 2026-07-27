---
platform: Codingame
difficulty: Medium
date: 2026-07-22
---
- Link is [here](https://www.codingame.com/training/medium/stock-exchange-losses)

# Solution
- C++
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/
  
int main()
{
    int n;
    std::cin >> n; std::cin.ignore();
    int maxValue = 0;
    int maxLoss = 0;

    for (int i = 0; i < n; i++) {
        int v;
        std::cin >> v;
        if (v >= maxValue) maxValue = v;
        else {
            int difference = maxValue - v;
            if (maxLoss < difference) maxLoss = difference;
        }
    }
    std::cout << -maxLoss << std::endl;
}
```

# What I've learned
- I was trapped Overthinking the problem by trying to track every single fluctuation, sorting the array, or using nested loops.
- Then I Realized that the problem only cares about the global peak and its relationship to subsequent values.
	- Keep a single running record of the highest number seen so far.
    - Compare every new number against that peak to find the drop.
    - Update the maximum loss if a larger drop appears.
