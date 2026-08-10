---
platform: LeetCode
difficulty: Medium
date: 2026-08-10
---
# Description
Given an array of integers `nums` and an integer `k`, return _the total number of subarrays whose sum equals to_ `k`.

> A subarray is a contiguous **non-empty** sequence of elements within an array.

**Example 1:**
	**Input:** nums = [1,1,1], k = 2
	**Output:** 2

**Example 2:**
	**Input:** nums = [1,2,3], k = 3
	**Output:** 2

# Solution
- C++
```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        std::unordered_map<int, int> prefixMap = {{0, 1}};
        int currentPrefixSum = 0;
        int totalSubArrays = 0;

        for (auto& num : nums) {
            currentPrefixSum += num;
            int oldPrefixSum = currentPrefixSum - k;
            if (prefixMap.contains(oldPrefixSum)) totalSubArrays += prefixMap[oldPrefixSum];
            prefixMap[currentPrefixSum]++;
        }

        return totalSubArrays;
    }
};
```

# Learned 
## 📌 Concept: Prefix Sum + HashMap
Use this pattern to find or count contiguous subarrays that add up to a target value $k$ in $O(n)$ time. It replaces a slow nested loop $O(n^2)$ search with a fast $O(1)$ hash table lookup.
### The Mathematical Core

The sum of any slice between an early index $i$ and current index $j$ is:  
$$\text{Current Prefix Sum} - \text{Old Prefix Sum} = k$$

Rearranging the formula to find the matching historical value:  
$$\text{Old Prefix Sum} = \text{Current Prefix Sum} - k$$

Instead of looping backward to look for that `Old Prefix Sum`, we query our HashMap:  
_"Have we seen a prefix sum equal to `(Current Prefix Sum - k)` before? If so, how many times?"_

### Example
- Input: `nums = [3, 4, 7, 2, -3, 1]`, `k = 7`
- Map Initialization: `{0: 1}` _(Base case: a sum of 0 has occurred 1 time before we start)_

|Step|Num|Current Sum|Target Complement (`Current Sum - k`)|Found?|Subarrays Count|HashMap State|
|---|---|---|---|---|---|---|
|Start|—|0|—|—|0|`{0:1}`|
|1|`3`|3|$3 - 7 = \mathbf{-4}$|❌ No|0|`{0:1, 3:1}`|
|2|`4`|7|$7 - 7 = \mathbf{0}$|Yes|+1 (Total: 1) _`[3, 4]`_|`{0:1, 3:1, 7:1}`|
|3|`7`|14|$14 - 7 = \mathbf{7}$|Yes|+1 (Total: 2) _`[7]`_|`{0:1, 3:1, 7:1, 14:1}`|
|4|`2`|16|$16 - 7 = \mathbf{9}$|❌ No|2|`{0:1, 3:1, 7:1, 14:1, 16:1}`|
|5|`-3`|13|$13 - 7 = \mathbf{6}$|❌ No|2|`{0:1, 3:1, 7:1, 14:1, 16:1, 13:1}`|
|6|`1`|14|$14 - 7 = \mathbf{7}$|Yes|+1 (Total: 3) _`[7, 2, -3, 1]`_|`{0:1, 3:1, 7:2, 14:1, 16:1, 13:1}`|

### Golden Rules & Traps
- Initialize `{0: 1}`: Essential for catching valid subarrays that start from index 0.
- Order Matters: Always calculate the target complement and check the map before adding the `currentPrefixSum` to the map. Otherwise, if $k=0$, an element will match with itself.
- Handle Negatives: This pattern works perfectly with negative numbers where sliding window / two-pointer approaches fail.



## LeetCode Practice List
1. Direct Variations (Subarray Target Search)
	- ==**LeetCode 525== - Contiguous Array:** Find the maximum length of a binary array with an equal number of `0` and `1`. _(Trick: Treat `0` as `-1`, and find the longest subarray that sums to `0`)_.
	- ==**LeetCode 974== - Subarray Sums Divisible by K:** Count subarrays whose sum is divisible by `k`. _(Trick: Use `currentPrefixSum % k` as your HashMap key)_.

2. Traditional Range Query Variations
	- **==LeetCode 303== - Range Sum Query (Immutable):** The pure baseline definition of Prefix Sum. Precompute once, answer range sum queries in \(\mathcal{O}(1)\).
	- **==LeetCode 238== - Product of Array Except Self:** Compute prefix products from the left and suffix products from the right without using the division operator.

## Real-World Applications
1. Game Development (Procedural Gen & Map Loading)
	- **1D/2D Level Generation (Spawn Weighting):** If you want to spawn items with custom weights (e.g., Common: 70%, Rare: 25%, Legendary: 5%), you generate a prefix sum array of these weights `[70, 95, 100]`. You pick a random number from 1 to 100, and use Binary Search on the prefix array to pick the item instantly in \(\mathcal{O}(\log n)\) time.
	- **Camera Tracking / Streaming Limits:** In infinite runners or open-world games, 2D prefix sums are used to instantly check structural properties (like density of colliders or enemy spawns) within the camera's viewport rectangle as it pans across a massive map matrix.

2. Malware Development (Obfuscation & Evasion)
	- **Polymorphic Shellcode Decryption:** Malware often obfuscates its internal payload strings or API names. Instead of standard XOR encryption, a malicious loader might use a rolling cumulative mutation (a cumulative mathematical prefix transformation) across its raw instruction bytes. The loader loops through the encrypted array once to "un-prefix" and decode the shellcode into memory right before execution, hiding structural patterns from static signature scanners.
	- **Process Injection Timing:** To bypass behavioral heuristics that look for sudden spikes in memory mapping, advanced loaders use running metrics over rolling windows to pace out injection steps.

3. Reverse Engineering (RE) & Binary Analysis
	- **Control Flow Graph (CFG) Alignment:** Disassemblers (like IDA Pro or Ghidra) process massive arrays of raw binary offsets and basic blocks. When reconstructing loops, functions, or tracking jumps, the tools use cumulative prefix tables to calculate target memory alignments, section offsets, and relative virtual addresses (RVAs) instantly.
	- **Network Packet Carving:** When rewriting scripts to reconstruct raw binary stream dumps (PCAPs) into structured files, reversers use prefix tracking to check sequential headers and ensure payload checksum slices line up exactly across fragmented packets.
