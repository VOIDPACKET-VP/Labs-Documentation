---
platform: Codeforces
difficulty: "800"
date: 2026-02-07
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int t, n;
    scanf("%d", &t);
    for (int x = 0; x < t; x++){
        scanf("%d", &n);
        int array_a[100];
        int count = 0;
        for (int y = 0; y < n; y++){
            scanf("%d", &array_a[y]);
        }
        for (int i = 0; i < n - 1; i++){
            for (int j = i + 1; j < n; j++){
                if (array_a[i] > array_a[j]){
                    count++;
                }
            }
        }
        printf("%d\n", count);
    }
    return 0;
}
```

- This here didn't work for me for some reason, but it does what the challenges wants, so ... ?