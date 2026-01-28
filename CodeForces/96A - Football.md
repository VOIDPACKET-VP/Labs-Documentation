---
platform: Codeforces
difficulty: Easy
date: 2026-01-28
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
int main(){
    char string[101];
    int lvl = 1;
    scanf("%s", string);
    for (int i = 0; i < strlen(string) - 1; i++){
        if (string[i] == string[i+1]){
            lvl += 1;
            if (lvl >= 7){
                printf("YES");
                break;
            }
        } else {
            lvl = 1;
        }        
    }
    if (lvl < 7) printf("NO");
    return 0;
}
```
