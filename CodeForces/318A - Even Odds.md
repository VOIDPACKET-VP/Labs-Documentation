---
platform: Codeforces
difficulty: Easy
date: 2026-01-28
---
# Solution
- C
```
#include <stdio.h>
int main(){
    long long n, k;
    scanf("%lld %lld", &n, &k);
    long long odd = (n + 1) / 2;
    if (k <= odd){
        printf("%lld", 2 * k -1);
    } else {
        printf("%lld", 2* (k - odd));
    }
    return 0;
}
```

- We had to use `%lld` since an `int` can't hold huge numbers like `10^12` , but 
