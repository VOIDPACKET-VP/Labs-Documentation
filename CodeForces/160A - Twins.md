---
platform: Codeforces
difficulty: Easy
date: 2026-01-28
---
# Solution
- C
```
#include <stdio.h>
#include <stdlib.h>
int compare(const int* a, const int* b){
    return *(int*)b -*(int*)a;
}
int main(){
    int n;
    int coins[100], total = 0;
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        scanf("%d", &coins[i]);
        total += coins[i];
    }
    qsort(coins, n, sizeof(int), compare);
    int mySum = 0, count = 0;
    for (int i = 0; i < n; i++){
        mySum += coins[i];
        count++;
        if (mySum > total - mySum){
            printf("%d", count);
            break;
        }
    }
    return 0;
}
```
