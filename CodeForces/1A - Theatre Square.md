---
platform: Codeforces
difficulty: "1000"
date: 2026-01-24
---
# Solution
- C
```
#include <stdio.h>
int main(){
	unsigned long long n, m, a = 1;
    unsigned long long na, ma, res = 0;
    scanf("%llu %llu %llu", &n, &m, &a);
    na = n/a;
    if (n%a != 0)
        na++;
    ma = m/a;
    if (m%a != 0)
        ma++;
    res = na * ma;
    printf("%llu", res);
    return 0;
}
```