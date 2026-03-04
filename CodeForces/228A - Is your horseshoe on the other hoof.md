---
platform: Codeforces
difficulty: "800"
date: 2026-03-04
---
# Solution
- C
```
#include <stdio.h>

int main(){
    int s[4];
    int unique = 0;
    for (int i = 0; i < 4; i++){
        scanf("%d", &s[i]);
    }

    for (int i = 0; i < 4; i++){
        int is_new = 1;
        for (int y = 0; y < i; y++){
            if (s[i] == s[y]) {
                is_new = 0;
                break;
            }
        }
        if (is_new) unique++;
    }
    printf("%d\n", 4 - unique);
  
    return 0;
}
```
