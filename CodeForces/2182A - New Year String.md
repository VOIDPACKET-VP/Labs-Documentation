---
platform: Codeforces
difficulty: "800"
date: 2026-02-12
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
int main(){
    int t, n;
    char s[21];
    const char *new_year = "2026";
    const char *last_year = "2025";
    int op;
    scanf("%d", &t);
    for (int i = 0; i < t; i++){
        scanf("%d", &n);
        scanf("%s", s);
        if (strstr(s, new_year) != NULL){
            op = 0;
            printf("%d\n", op);
        } else if (strstr(s, last_year) != NULL){
            op = 1;
            printf("%d\n", op);
        } else {
            op = 0;
            printf("%d\n", op);
        }
    }
    return 0;
}
```