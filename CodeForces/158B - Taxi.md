---
platform: Codeforces
difficulty: "1100"
date: 2026-01-31
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n;
    int one = 0, two = 0, three = 0, four = 0;
    int group, taxi = 0;
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        scanf("%d", &group);
        if (group == 1){
            one++;
        } else if (group == 2){
            two++;
        } else if (group == 3){
            three++;
        } else {
            four++;
        }
    }

    // Groupe of 4
    taxi += four;
  
    // Groupe of 3
    taxi += three;
    if (one > three) one -= three;
    else one = 0;

    // Groupe of 2
    taxi += two / 2;
    two = two % 2;

    // Leftover Group of 2
    if (two == 1){
        taxi++;
        if (one >= 2){
            one -= 2;
        } else if (one == 1){
            one -= 1;
        }
    }
    
    // Leftover Group of 1
    taxi += (one + 3) / 4;
    printf("%d", taxi);
    return 0;
}
```
