---
platform: Codeforces
difficulty: "900"
date: 2026-03-05
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int lights[3][3];
    int pressed[3][3];
    for (int i = 0; i < 3; i++){
        for (int j = 0; j < 3; j++){
            scanf("%d", &lights[i][j]);
        }
    }

    for (int i = 0; i < 3; i++){
        for (int j = 0; j < 3; j++){
            int sum = lights[i][j];
            if (i > 0) sum += lights[i-1][j];
            if (i < 2) sum += lights[i+1][j];
            if (j > 0) sum += lights[i][j-1];
            if (j < 2) sum += lights[i][j+1];
            if (sum % 2 == 0) printf("1");
            else printf("0");
        }
        printf("\n");
    }
    return 0;
}
```
