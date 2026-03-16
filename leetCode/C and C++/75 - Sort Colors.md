---
platform: LeetCode
difficulty: Medium
date: 2026-03-15
---
# Solution
- C++
```
class Solution {
public:
    void sortColors(vector<int>& nums) {
        mergeSort(nums);
    }
private:
    void mergeSort(vector<int>& array) {
        int length = array.size();
        if (length <= 1) return;
        int middle = length / 2;
        vector<int> rightArray(length - middle);
        vector<int> leftArray(middle);
        int r = 0;
        for (int l = 0; l < length; l++){
            if (l < middle) {
                leftArray[l] = array[l];
            } else {
                rightArray[r] = array[l];
                r++;
            }
        }
        // the craziness starts here : recursion
        mergeSort(leftArray);
        mergeSort(rightArray);
        merge(array, rightArray, leftArray);
    }
    void merge(vector<int>& array, vector<int>& rightArray, vector<int>& leftArray) {
        int leftSize = leftArray.size();
        int rightSize = rightArray.size();
        int i = 0, l = 0, r = 0; // indices
        // the mergin conditions
        while(l < leftSize && r < rightSize) {
            if (leftArray[l] < rightArray[r]) {
                array[i] = leftArray[l];
                i++;
                l++;
            } else {
                array[i] = rightArray[r];
                i++;
                r++;
            }
        }
        // if we have leftovers
        while (l < leftSize) {
            array[i] = leftArray[l];
            i++;
            l++;
        }
        while (r < rightSize) {
            array[i] = rightArray[r];
            i++;
            r++;
        }
    }
};
```
- All i did was use the solution i used in the `912 - Sort an array` challenge which uses the `merge sort` 
- There are better ways to solve this which can be found here : [neetcode's solutions](https://neetcode.io/solutions/sort-colors)