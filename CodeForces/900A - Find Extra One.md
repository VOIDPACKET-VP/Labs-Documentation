---
platform: Codeforces
difficulty: "800"
date: 2026-02-24
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, x, y;
    int left = 0, right = 0;
    scanf("%d", &n);

    for (int i = 0; i < n; i++){
        scanf("%d %d", &x, &y);
        if (x < 0) left++;
        else right++;
    }

    if (left < 2 || right < 2) printf("Yes");
    else printf("No");
}
```