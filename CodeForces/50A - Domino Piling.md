---
platform: Codeforces
difficulty: "800"
date: 2026-01-24
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int m, n;
    scanf("%d %d", &m, &n);
    int max = (m * n) / 2;
    printf("%d", max);
    return 0;
}
```