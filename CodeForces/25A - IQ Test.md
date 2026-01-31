---
platform: Codeforces
difficulty: "1300"
date: 2026-01-31
---
# Solution
- C
```
#include <stdio.h>
#include <stdlib.h>
int main(){
    int n, even = 0, odd = 0;
    int e = 0, o = 0;
    int *numbers;
    scanf("%d", &n);
    numbers = (int *)malloc(n * sizeof(int));
    if (numbers == NULL){
        return 1;
    }
    for (int i = 0; i < n; i++){
        scanf("%d", &numbers[i]);
        if (numbers[i] % 2 == 0){
            even++;
            e = i + 1;
        } else {
            odd++;
            o = i + 1;
        }
    }
    if (odd == 1){
        printf("%d", o);
    } else {
        printf("%d", e);
    }
    free(numbers);
    numbers = NULL;
    return 0;
}
```
