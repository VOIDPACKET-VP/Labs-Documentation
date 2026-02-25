---
platform: Codeforces
difficulty: "800"
date: 2026-02-25
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, a, b;
    int years[100];
    int years_of_rank = 0;

    scanf("%d", &n);
    for (int i = 0; i < n-1; i++){
        scanf("%d", &years[i]);
    }
    scanf("%d %d", &a, &b);

    for (int i = a - 1; i < b - 1; i++){
        years_of_rank += years[i];
    }
    printf("%d", years_of_rank);
    return 0;
}
```
