---
platform: Codeforces
difficulty: "800"
date: 2026-02-07
---
# Solution
- C
```
#include <stdio.h>
int main() {
    int t, n;
    scanf("%d", &t);
    while (t--) {
        scanf("%d", &n);
        int a[105];
        for (int i = 0; i < n; i++) {
            scanf("%d", &a[i]);
        }
        int total_ops = 0;
        for (int j = 1; j < n; j++) {
            int can_be_removed = 0;
            for (int i = 0; i < j; i++) {
                if (a[i] > a[j]) {
                    can_be_removed = 1;
                    break;
                }
            }
            if (can_be_removed) {
                total_ops++;
            }
        }
        printf("%d\n", total_ops);
    }
    return 0;
}
```