---
platform: Codeforces
difficulty: Easy
date: 2026-01-27
---
# Solution
- C
```
#include <stdio.h>
#include <stdlib.h>
int compare(const void *a, const void *b){
    int int_a = *(int*)a;
    int int_b = *(int*)b;
    if (int_a > int_b) return 1;
    if (int_a < int_b) return -1;
    return 0;
}
int main(){
    char string[101];
    int sorted[101];
    int j = 0;
    scanf("%s", string);
    for (int i = 0; string[i]; i++){
        if (string[i] != '+'){
            sorted[j] = string[i];
            j++;
        }
    }
    qsort(sorted, j, sizeof(int), compare);
    for (int i = 0; i < j; i++){
        printf("%c", sorted[i]);
        if (i < j - 1){
            printf("+");
        }
    }
    return 0;
}
```
