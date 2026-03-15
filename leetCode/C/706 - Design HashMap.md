---
platform: LeetCode
difficulty: Easy
date: 2026-03-06
---
# Solution
- C++
```
class MyHashMap {
private:
    static const int SIZE = 10007;
    std::vector<std::list<std::pair<int, int>>> buckets;

    int hash(int key) {
        return key % SIZE;
    }

public:
    MyHashMap() {
        buckets.resize(SIZE);    
    }

    void put(int key, int value) {
        int idx = hash(key);
        for (auto& pair : buckets[idx]) {
            if (pair.first == key) {
                pair.second = value;
                return;
            }
        }
        buckets[idx].push_back({key, value});
    }

    int get(int key) {
        int idx = hash(key);
        for (auto const& pair : buckets[idx]) {
            if (pair.first == key) return pair.second;
        }
        return -1;
    }

    void remove(int key) {
        int idx = hash(key);
        auto& bucket = buckets[idx];
        for (auto it = bucket.begin(); it != bucket.end(); it++){
            if (it->first == key) {
                bucket.erase(it);
                return;
            }
        }
    }
};
```