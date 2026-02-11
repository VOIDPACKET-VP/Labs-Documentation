---
platform: Codeforces
difficulty: "900"
date: 2026-02-11
---
# Solution
- C
```
#include <stdio.h>
int digit_sum(long long n) {
    int sum = 0;
    while (n > 0) {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}

int main() {
    int t;
    scanf("%d", &t);
    while (t--) {
        long long x;
        scanf("%lld", &x);
        if (x % 9 != 0) {
            printf("0\n");
            continue;
        }
        int cnt = 0;
        for (int d = 1; d <= 90; d++) {
            long long y = x + d;
            if (digit_sum(y) == d) cnt++;
        }
        printf("%d\n", cnt);
    }
    return 0;
}
```
