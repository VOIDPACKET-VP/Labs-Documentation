---
platform: Codeforces
difficulty: "1300"
date: 2026-02-28
---
# Solution
- C
```
#include <stdio.h>
#define MAX_S 1000005
int main(){
    int n;
    int count[MAX_S] = {0};
    int first[MAX_S] = {0};
    int last[MAX_S] = {0};
    scanf("%d", &n);
    int l = 1, r = n;
    int max_freq = 0;
    int min_len = n + 1;
    for (int i = 1; i <= n; i++){
        int x;
        scanf("%d", &x);
        if (first[x] == 0){
            first[x] = i;
        }
        last[x] = i;
        count[x]++;
        int currentBeauty = last[x] - first[x] + 1;
        if (count[x] > max_freq){
            max_freq = count[x];
            min_len = currentBeauty;
            l = first[x];
            r = last[x];
        } else if (count[x] == max_freq && currentBeauty < min_len){
            min_len = currentBeauty;
            l = first[x];
            r = last[x];
        }
    }
    printf("%d %d", l, r);
    return 0;
}
```
