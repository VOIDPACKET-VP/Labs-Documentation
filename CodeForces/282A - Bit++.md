---
platform: Codeforces
difficulty: "800"
date: 2026-01-23
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n;
    int x = 0;
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        char stat[4];
        scanf("%s", stat);
        if (stat[1] == '+'){
            x++;
        } else {
            x--;
        }
    }
    printf("%d", x);
    return 0;
}
```

- I just learned that we should use `'` to compare instead of `"` as the latter denotes a string literal and `stat[1]` is a `pointer` .