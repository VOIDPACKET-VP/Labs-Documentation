---
platform: Codeforces
difficulty: "800"
date: 2026-03-07
---
# Solution
- C
```
#include <stdio.h>
int main() {
    int n;
    scanf("%d", &n);
    int points[1001];
    int amazing = 0;
    int worst, best;
    for (int i = 0; i < n; i++) {
        scanf("%d", &points[i]);
    }
    if (n > 0) {
        best = points[0];
        worst = points[0];
    }
    for (int i = 1; i < n; i++) {
        if (points[i] > best) {
            best = points[i];
            amazing++;
        } else if (points[i] < worst) {
            worst = points[i];
            amazing++;
        }
    }
    printf("%d\n", amazing);
    return 0;
}
```
