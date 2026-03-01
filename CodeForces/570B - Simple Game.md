---
platform: Codeforces
difficulty: "1300"
date: 2026-02-28
---
# Solution
- C
```
#include <stdio.h>
int main(){
    long long n,m;
    scanf("%lld %lld", &n, &m);
    if (n == 1){
        printf("1\n");
    } else if (m - 1 < n - m){
        printf("%lld\n", m + 1);
    } else {
        printf("%lld\n", m - 1);
    }
    return 0;
}
```
