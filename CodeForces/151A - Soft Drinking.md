---
platform: Codeforces
difficulty: "800"
date: 2026-03-02
---
# Solution
- C
```
#include <stdio.h>

int max_drinks(int a, int b, int c){
    if (a <= b && a <= c) {
        return a;
    } else if (b <= a && b <= c) {
        return b;
    } else {
        return c;
    }
}

int main(){

    int n, k, l, c, d, p, nl, np;
    scanf("%d %d %d %d %d %d %d %d", &n, &k, &l, &c, &d, &p, &nl, &np);

    int mill = (k * l) / nl;
    int slices = (d * c);
    int salt = p / np;

    int max = max_drinks(mill, slices, salt);
    
    printf("%d\n", max / n);
    return 0;
}
```
