---
platform: Codeforces
difficulty: "1100"
date: 2026-03-05
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, m, value;
    int position[100005] = {0};
    long long vasya_comp = 0;
    long long petya_comp = 0;
  
    scanf("%d", &n);
    for (int i = 1; i <= n; i++){
        scanf("%d", &value);
        position[value] = i;
    }
    scanf("%d", &m);
    for (int i = 0; i < m; i++){
        scanf("%d", &value);
        vasya_comp += position[value];
        petya_comp += (n - position[value] + 1);
    }
    printf("%lld %lld\n", vasya_comp, petya_comp);
    return 0;
}
```
