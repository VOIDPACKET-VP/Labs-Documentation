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
    int n, x,y,z, X = 0,Y = 0,Z = 0;
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        scanf("%d %d %d", &x, &y, &z);
        X += x;
        Y += y;
        Z += z;
    }
    if (X == 0 && Y == 0 && Z == 0){
        printf("YES");
    } else {
        printf("NO");
    }
    return 0;
}
```