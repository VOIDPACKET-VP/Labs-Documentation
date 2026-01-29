---
platform: Codeforces
difficulty: "1000"
date: 2026-01-28
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int a, b, c;
    scanf("%d", &a);
    scanf("%d", &b);
    scanf("%d", &c);
    
    int array[6], max;
    
    array[0] = a + b + c;
    array[1] = a + b * c;
    array[2] = a * b + c;
    array[3] = a * b * c;
    array[4] = (a + b) * c;
    array[5] = a * (b + c);  
    
    max = array[0];
    
    for (int i = 0; i < 6; i++){
        if (array[i] > max){
            max = array[i];
        }
    }
    printf("%d", max);
    return 0;

}
```
