---
platform: Codeforces
difficulty: "800"
date: 2026-01-20
---
# Solution
- C
```
#include <stdio.h>
#include <math.h>
int main(){
    int x;
    scanf("%d", &x);
    float num = (float)x/5;  
    float steps = ceil(num);
    printf("%d", (int)steps);    
    return 0;
}
```
