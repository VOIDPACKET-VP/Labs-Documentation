---
platform: Codeforces
difficulty: "1000"
date: 2026-02-11
---
# Solution
- C
```
#include <stdio.h>
#include <stdbool.h>
#define MAX_n 200005

int p[MAX_n];
int a[MAX_n];
int unique_a[MAX_n];

void solve(){
    int n;
    scanf("%d", &n);
    for (int i = 0; i < n; i++){
        scanf("%d", &p[i]);
    }
    for (int i = 0; i < n; i++){
        scanf("%d", &a[i]);
    }
    int m = 0;
    unique_a[m++] = a[0];
    for (int i = 1; i < n; i++){
        if (a[i] != a[i - 1]){
            unique_a[m++] = a[i];
        }
    }
    int p_ptr = 0;
    int a_ptr = 0;
    while (p_ptr < n && a_ptr < m){
        if (p[p_ptr] == unique_a[a_ptr]){
            a_ptr++;
        }
        p_ptr++;
    }
    if (a_ptr == m){
        printf("YES\n");
    } else {
        printf("NO\n");
    }
}

int main(){
    int t;
    scanf("%d", &t);
    while (t--){
        solve();
    }
    return 0;
}
```