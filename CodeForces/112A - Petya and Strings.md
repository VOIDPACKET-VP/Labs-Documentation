---
platform: Codeforces
difficulty: "800"
date: 2026-01-20
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>
int main(){
    char string1[101], string2[101];
    scanf("%s", string1);
    scanf("%s", string2);
    for (int i = 0; string1[i] != '\0'; i++) string1[i] = tolower(string1[i]);
    for (int i = 0; string2[i] != '\0'; i++) string2[i] = tolower(string2[i]);
    int result = strcmp(string1, string2);
    printf("%d", result == 0 ? 0 : result > 0 ? 1 : -1);
    return 0;
}
```