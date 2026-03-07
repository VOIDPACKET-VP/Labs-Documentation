---
platform: Codeforces
difficulty: "1000"
date: 2026-03-06
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n;
    int fingers;
    int total_f = 0;
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        scanf("%d", &fingers);
        total_f += fingers;
    }
    int total_p = n + 1;
    int fingers_combintion = 0;
    for (int m = 1; m <= 5; m++){
        if ((total_f + m) % total_p != 1) fingers_combintion++;
    }
    printf("%d\n", fingers_combintion);
    return 0;
}
```

