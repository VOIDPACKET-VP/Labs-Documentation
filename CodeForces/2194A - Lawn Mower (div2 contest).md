---
platform: Codeforces
difficulty: "800"
date: 2026-02-08
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int t;
    scanf("%d", &t);
    long long n, w;
    for (int i = 0; i < t; i++){
        scanf("%lld %lld", &n, &w);
        printf("%lld\n", n - n/w);
    }
    return 0;
}
```
