---
platform: Codeforces
difficulty: "800"
date: 2026-03-01
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
int main(){
    char borze[201];
    scanf("%s", borze);
    for (int i = 0; i < strlen(borze);){
        if (borze[i] == '-' && borze[i + 1] == '-'){
            printf("2");
            i += 2;
        } else if (borze[i] == '-' && borze[i + 1] =='.'){
            printf("1");
            i += 2;
        } else {
            printf("0");
            i++;
        }
    }
    printf("\n");
    return 0;
}
```
