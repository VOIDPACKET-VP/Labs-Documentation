---
platform: Codeforces
difficulty: Easy
date: 2026-01-28
---
# Solution
- C
```
#include <stdio.h>
#include <ctype.h>
int main(){
    char string[101], sorted[101];
    int j = 0;
    scanf("%s", string);
    for (int i = 0; string[i] != '\0'; i++) string[i] = tolower(string[i]);
    for (int i = 0; string[i]; i++){
        if (string[i] != 'a' && string[i] != 'o' && string[i] != 'y' && string[i] != 'e' && string[i] != 'u' && string[i] != 'i'){
            sorted[j] = string[i];
            j++;
        }
    }
    for (int i = 0; i < j; i++){
        printf(".%c", sorted[i]);
    }
    return 0;
}
```