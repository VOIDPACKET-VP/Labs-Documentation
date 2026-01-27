---
platform: Codeforces
difficulty: Easy
date: 2026-01-27
---
# Solution
- C
```
#include <stdio.h>
#include <string.h>
int hasRepeatedChars(const char* str) {
    int seen[26] = {0};
    int count = 0;
    for (int i = 0; str[i]; i++) {
        int currentChar = str[i] - 'a';
        if (seen[currentChar] == 0) {
            seen[currentChar] = 1;
            count ++;
        }
    }
    return count;
}
int main(){
    char string[101];
    scanf("%s", string);
    int newResult = hasRepeatedChars(string);
    printf("%s", newResult % 2 == 0 ? "CHAT WITH HER!" : "IGNORE HIM!");
    return 0;
}
```

