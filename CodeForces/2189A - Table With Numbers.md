---
platform: Codeforces
difficulty: "800"
date: 2026-02-12
---
# Solution
- C
```
#include <stdio.h>
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
  
void solve() {
    int n, h, l;
    scanf("%d %d %d", &n, &h, &l);
    if (h > l) swap(&h, &l);
    int cntH = 0;
    int cntL = 0;
    for (int i = 0; i < n; i++) {
        int a;
        scanf("%d", &a);
        if (a <= h) cntH++;
        if (a <= l) cntL++;
    }
    int ans1 = cntH;
    int ans2 = cntL / 2;
    printf("%d\n", (ans1 < ans2) ? ans1 : ans2);
}
  
int main() {
    int t;
    scanf("%d", &t);
    while (t--) solve();
    return 0;
}
```

- This is just a translation in code of the Challenge's author's solution : 
```
Link > https://codeforces.com/blog/entry/150452

Note that maximizing the sum of numbers in the table is equivalent to maximizing the number of chosen pairs that specify a valid cell.

Without loss of generality, we assume that h≤l. For any cell of the table (x,y), 1≤x≤h, 1≤y≤l. Let cnth be the number of elements in the array not exceeding h, and cntl be the number of elements in the array not exceeding l. Then, firstly, the answer does not exceed cnth, since each pair must contain a number not exceeding h. Conversely, the answer does not exceed ⌊cntl2⌋, since both numbers in each pair must not exceed l. It remains to be seen that min(cnth,⌊cntl2⌋) pairs can be obtained. To do this, let's consider two cases.

- if cnth≤⌊cntl2⌋, then it is sufficient to pair each number x≤h with its own number h<y≤l, and there will be cnth pairs. This can be done since there are at least as many suitable numbers y as there are suitable x.
    
- if cnth>⌊cntl2⌋, then we need to pair each number h<y≤l with its own number x≤h. After this, split the remaining numbers x≤h into pairs (there may be one extra number left over). We'll get exactly ⌊cntl2⌋ pairs.
```
