---
platform: LeetCode
difficulty: Medium
date: 2026-03-16
---
# Solution
- C++
```
class NumMatrix {
private:
    std::vector<std::vector<int>> s;
public:
    NumMatrix(vector<vector<int>>& matrix) {
        int rowCount = matrix.size();
        int colCount = matrix[0].size();
        // We Create a new matrix filled with 0s, size (rowCount+1) x (colCount+1)
        std::vector<vector<int>> pref(rowCount + 1, vector<int>(colCount + 1, 0));
  
        for (int r = 0; r < rowCount; r++){
            int prefix = 0;
            for (int c = 0; c < colCount; c++){
                prefix += matrix[r][c];
                int above = pref[r][c + 1];
                pref[r + 1][c + 1] = prefix + above;
            }
        }
        this->s = std::move(pref);
    }

    int sumRegion(int row1, int col1, int row2, int col2) {
        return s[row2 + 1][col2 + 1] - s[row1][col2 + 1] - s[row2 + 1][col1] + s[row1][col1];
    }
};
```
- We used something called `Prefix Sum` :
	- To Remember The Logic we used here, rewatch this video [Range Sum Query 2D - Immutable](https://youtu.be/KE8MQuwE2yA?si=1th2FjUvqbQzrG9D)