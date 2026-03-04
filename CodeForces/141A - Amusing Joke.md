---
platform: Codeforces
difficulty: "800"
date: 2026-03-02
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int compare(const void* a, const void* b){
    char char_1 = *(const char*)a;
    char char_2 = *(const char*)b;
    return (char_1 > char_2) - (char_1 < char_2);
}

int main(){
    char destination[202];
    char source[101];
    char mixedUp[202];
    
    scanf("%s", destination);
    scanf("%s", source);
    scanf("%s", mixedUp);
    
    strcat(destination, source);
    qsort(destination, strlen(destination), sizeof(char), compare);
    qsort(mixedUp, strlen(mixedUp), sizeof(char), compare);
    
    if (strcmp(destination, mixedUp) == 0) printf("YES\n");
    else printf("NO\n");
    
    return 0;
}
```
