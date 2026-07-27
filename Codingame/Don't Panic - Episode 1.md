---
platform: Codingame
difficulty: Medium
date: 2026-07-22
---
- Link is [here](https://www.codingame.com/training/medium/don't-panic-episode-1)

# Solution
- C++
```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/

int main()
{
    int nb_floors; // number of floors
    int width; // width of the area
    int nb_rounds; // maximum number of rounds
    int exit_floor; // floor on which the exit is found
    int exit_pos; // position of the exit on its floor
    int nb_total_clones; // number of generated clones
    int nb_additional_elevators; // ignore (always zero)
    int nb_elevators; // number of elevators
    cin >> nb_floors >> width >> nb_rounds >> exit_floor >> exit_pos >> nb_total_clones >> nb_additional_elevators >> nb_elevators; cin.ignore();

    std::vector<int> elevators(nb_elevators);
    for (int i = 0; i < nb_elevators; i++) {
        int elevator_floor; // floor on which this elevator is found
        int elevator_pos; // position of the elevator on its floor
        cin >> elevator_floor >> elevator_pos; cin.ignore();
        elevators[elevator_floor] = elevator_pos;
    }

    // game loop
    while (1) {
        int clone_floor; // floor of the leading clone
        int clone_pos; // position of the leading clone on its floor
        string direction; // direction of the leading clone: LEFT or RIGHT
        cin >> clone_floor >> clone_pos >> direction; cin.ignore();

        if (clone_floor == -1){
            std::cout << "WAIT" <<std::endl;
            continue;
        }

        int target_pos = 0;
        if (exit_floor == clone_floor) target_pos = exit_pos;
        else target_pos = elevators[clone_floor];

        bool wrong_dir = false;
        if (clone_pos < target_pos && direction == "LEFT") {
            wrong_dir = true;
        } else if (clone_pos > target_pos && direction == "RIGHT") {
            wrong_dir = true;
        }
        if (wrong_dir) std::cout << "BLOCK" << std::endl;
        else std::cout << "WAIT" << std::endl;
    }
}
```

# What I've learned
- I again was overthinking it, i was trying to solve each test case alone using some complex conditions.
- Unfortunately i couldn't solve it on my own, but i learned a lot alhamdulillah