---
platform: Codeforces
difficulty: "800"
date: 2026-03-06
---
# Solution
- C
```
#include <stdio.h>
#include <ctype.h>
int main(){
    char s[1000];
    scanf("%s", s);
    s[0] = toupper(s[0]);
    printf("%s\n", s);

    return 0;
}
```
