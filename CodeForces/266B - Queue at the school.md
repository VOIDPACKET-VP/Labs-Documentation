---
platform: Codeforces
difficulty: "800"
date: 2026-03-01
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, t;
    char line[51];
    scanf("%d %d", &n, &t);
    scanf("%s", line);
    for (int i = 0; i < t; i++){
        for (int j = 0; j < n - 1;){
            if (line[j] == 'B' && line[j + 1] == 'G'){
                line[j] = 'G';
                line[j + 1] = 'B';
                j += 2;
            } else {
                j++;
            }
        }
    }
    printf("%s", line);
    return 0;
}
```
