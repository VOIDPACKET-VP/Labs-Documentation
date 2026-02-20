---
platform: Codeforces
difficulty: "1200"
date: 2026-02-12
---
# Solution
- C
```
#include <stdio.h>

long long max(long long a, long long b) {
    return (a > b) ? a : b;
}
  
void niceness_calculator() {
    int n;
    scanf("%d", &n);
    long long a[200005];
    for (int i = 0; i < n; i++) scanf("%lld", &a[i]);

    long long current_suffix_sum = 0;
    for (int i = 0; i < n; i++) {
        current_suffix_sum += a[i];
    }
    long long max_x = -2e18;
    long long prefix_abs_sum = 0;

    for (int i = 0; i < n; i++) {
        current_suffix_sum -= a[i];
        max_x = max(max_x, prefix_abs_sum - current_suffix_sum);
        prefix_abs_sum += (i == 0) ? a[i] : (a[i] > 0 ? a[i] : -a[i]);
    }
    printf("%lld\n", max_x);
}
  
int main() {
    int t;
    scanf("%d", &t);
    while (t--) niceness_calculator();
    return 0;
}
```

- Here is a video explaining [First or Second](https://youtu.be/KvzGrMCAv2s?si=7-z_bqAGjmz4Evi8) just make sure you go to minute `25:58` 