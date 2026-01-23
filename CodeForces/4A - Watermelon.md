---
platform: Codeforces
difficulty: Easy
date: 2026-01-23
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int w;
    scanf("%d", &w);
    if (1 <= w <= 100){
        if (w > 2 && w % 2 == 0){
            printf("YES");
        } else {
            printf("NO");
        }
    }
    return 0;
}
```
