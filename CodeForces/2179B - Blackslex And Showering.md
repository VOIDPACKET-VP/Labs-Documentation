---
platform: Codeforces
difficulty: "800"
date: 2026-02-12
---
# Solution
- C
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int a[200005];

void calculate(){
    int n;
    if (scanf("%d", &n) != 1) return;
    for (int i = 0; i < n; i++){
        scanf("%d", &a[i]);
    }
    if (n <= 2) {
        printf("0\n");
        return;
    }
    long long original_sum = 0;
    for (int i = 0; i < n - 1; i++){
        original_sum += abs(a[i] - a[i+1]);
    }
    long long max_saving = abs(a[0] - a[1]);
    long long last_saving = abs(a[n - 2] - a[n - 1]);
    if (last_saving > max_saving) max_saving = last_saving;
    for (int i = 1; i < n - 1; i++){
        long long unskipped = (long long)abs(a[i-1] - a[i]) + abs(a[i] - a[i + 1]);
        long long skipped = abs(a[i - 1] - a[i + 1]);
        long long current_saving = unskipped - skipped;
        if (current_saving > max_saving) max_saving = current_saving;
    }
    printf("%lld\n", (original_sum - max_saving));
}

int main(){
    int t;
    if (scanf("%d", &t) != 1) return 0;
    while(t--){
      calculate();  
    }
    return 0;
}
```