---
platform: Codeforces
difficulty: "800"
date: 2026-03-07
---
# Solution
- C
```
#include <stdio.h>
int min(int a, int b) {
    return (a < b) ? a : b;
}
int main() {
    int n;
    scanf("%d", &n);
    int left_ones = 0, right_ones = 0;
    for (int i = 0; i < n; i++) {
        int l, r;
        scanf("%d %d", &l, &r);
        if (l == 1) left_ones++;
        if (r == 1) right_ones++;
    }
    int left_cost = min(left_ones, n - left_ones);
    int right_cost = min(right_ones, n - right_ones);
    printf("%d\n", left_cost + right_cost);
    return 0;
}
```

- C++
```
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
	ios_base::sync_with_stdio(false);
	cin.tie(NULL);
	int n;
	cin >> n;
	int left_ones = 0;
	int right_ones = 0;
	for (int i = 0; i < n; i++) {
		int l, r;
		cin >> l >> r;
		if (l == 1) left_ones++;
		if (r == 1) right_ones++;
	}
	int seconds = min(left_ones, n - left_ones) + min(right_ones, n - right_ones);
	cout << seconds << endl;
	return 0;
}
```
