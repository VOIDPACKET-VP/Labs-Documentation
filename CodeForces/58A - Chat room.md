---
platform: Codeforces
difficulty: "1000"
date: 2026-01-28
---
# Solution
- C
```
#include <stdio.h>
#include <ctype.h>
int main(){
    char s[101];
    char target[] = "hello";
    int target_i = 0;
    scanf("%s", s);
    for (int i = 0; s[i]; i++) s[i] = tolower(s[i]);
    for (int i = 0; s[i]; i++){
        if (s[i] == target[target_i]){
            target_i++;
        }
        if (target_i == 5){
            break;
        }
    }
    if (target_i == 5){
        printf("YES");
    } else {
        printf("NO");
    }
    return 0;
}
```

