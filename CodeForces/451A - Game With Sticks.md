---
platform: Codeforces
difficulty: "900"
date: 2026-02-09
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, m, a;
    scanf("%d %d", &n, &m);
    if (m > n) a = n; else a = m;
    if (a % 2 == 0){
        printf("Malvika");
    } else {
        printf("Akshat");
    }
    return 0;
}
```
