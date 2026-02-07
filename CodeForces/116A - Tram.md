---
platform: Codeforces
difficulty: "800"
date: 2026-02-04
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n;
    scanf("%d", &n);
    int a, b;
    int current = 0;
    int max = 0;
    for (int i = 0; i < n; i++){
        scanf("%d %d", &a, &b);
        current += b;
        current -= a;
        if (current > max){
            max = current;
        }
    }
    printf("%d", max);
    return 0;
}
```
