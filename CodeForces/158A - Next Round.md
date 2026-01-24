---
platform: Codeforces
difficulty: Easy
date: 2026-01-23
---
# Solution
- C
```
#include <stdio.h>
int main(){
    int n, k, count = 0;
    scanf("%d %d", &n, &k);
    int scores[n];
    for (int i = 0; i < n; i++){
        scanf("%d", &scores[i]);
    }
    for (int i = 0; i < n; i++){
        if (scores[i] >= scores[k-1] && scores[k-1] > 0){
            count++;
        } 
    }
    printf("%d", count);
    return 0;
}
```

- C++
```
#include <bits/stdc++.h>
using namespace std;
int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    int n, k;
    cin >> n >> k;
    vector<int> A(n);
    for (auto &i : A) cin >> i;
    cout << count_if(begin(A), end(A), [&](int x) {
        return x > 0 && x >= A[k - 1];
    }) << endl;
}
```

