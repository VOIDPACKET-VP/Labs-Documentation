---
platform: Codeforces
difficulty: "1200"
date: 2026-02-09
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, m, a, b, sum;
    scanf("%d %d %d %d", &n, &m, &a, &b);

    int option1 = a * n;
    int remaining = ((n % m) * a < b) ? (n % m) * a : b;
    int option2 = (n / m) * b + remaining;
    
    if (option1 < option2){
        printf("%d", option1);
    } else {
        printf("%d", option2);
    }
    return 0;
}
```
