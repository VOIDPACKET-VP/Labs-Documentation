---
platform: Codeforces
difficulty: "900"
date: 2026-01-29
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
int main() {
    char dub[201];  
    scanf("%s", dub);
    char nonDub[201];
    int nonDub_i = 0;
    int len = strlen(dub);
    for (int i = 0; i < len; i++) {
        if (i + 2 < len && dub[i] == 'W' && dub[i+1] == 'U' && dub[i+2] == 'B') {
            i += 2;
            if (nonDub_i > 0 && nonDub[nonDub_i-1] != ' ') {
                nonDub[nonDub_i] = ' ';
                nonDub_i++;
            }
        } else {
            nonDub[nonDub_i] = dub[i];
            nonDub_i++;
        }
    }
    nonDub[nonDub_i] = '\0';
    if (nonDub_i > 0 && nonDub[nonDub_i-1] == ' ') {
        nonDub[nonDub_i-1] = '\0';
    }
    printf("%s\n", nonDub);
    return 0;
}
```