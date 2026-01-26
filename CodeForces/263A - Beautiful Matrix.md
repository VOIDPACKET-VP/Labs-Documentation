---
platform: Codeforces
difficulty: Easy
date: 2026-01-26
---
# Solution
- C
```
// Without an array
#include <stdio.h>
#include <stdlib.h>
int main() {
    for (int i = 0; i < 5; i++) {
        for (int j = 0; j < 5; j++) {
            int x;
            scanf("%d", &x);
            if (x == 1) {
                printf("%d", abs(i-2) + abs(j-2));  
                return 0;
            }
        }
    }
    return 0;
}
```

```
// With an array
#include <stdio.h>
#include <math.h>
int main(){
    int arr[5][5];
    int isStopped = 0;
    for (int i = 0; i < 5; i++){
        for (int j = 0; j < 5; j++){
            scanf("%d", &arr[i][j]);
            if (arr[i][j] == 1){
                printf("%d", abs(i-3) + abs(j-3));
                isStopped = 1;
                break;
            }
        }
        if (isStopped){
            break;
        }
    }
    return 0;
}
```
