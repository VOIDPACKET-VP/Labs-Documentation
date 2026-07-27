---
platform: Codingame
difficulty: Easy
date: 2026-07-27
---
- Link is [here](https://www.codingame.com/ide/puzzle/mime-type)

# Solution
- C++
```cpp
#include <iostream>
#include <ostream>
#include <string>
#include <vector>
#include <algorithm>
#include <unordered_map>
#include <cctype>
using namespace std;

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    int n; // Number of elements which make up the association table.
    cin >> n; cin.ignore();
    int q; // Number Q of file names to be analyzed.
    cin >> q; cin.ignore();
    std::unordered_map<std::string, std::string> mimeType;

    for (int i = 0; i < n; i++) {
        string ext; // file extension
        string mt; // MIME type.
        cin >> ext >> mt; cin.ignore();

        for (char &c : ext) {
            c = std::tolower(c);
        }
        mimeType[ext] = mt;
    }

    for (int i = 0; i < q; i++) {
        string fname;
        getline(cin, fname); // One file name per line.
        size_t dotPos = fname.find_last_of('.');
        if (dotPos != std::string::npos) {
            std::string extension = fname.substr(dotPos + 1);
            for (char &c : extension) {
                c = std::tolower(c);
            }

            auto it = mimeType.find(extension);
            if (it != mimeType.end()) {
                std::cout << it->second << "\n";
            } else {
                std::cout << "UNKNOWN" << "\n";
            }
        } else {
            std::cout << "UNKNOWN" << "\n";
        }
    }
}
```

# What I've learned
- It's better to use `unordered_map` than regular `map` cause it uses a `hash table` and it's faster when you look things up inside that map