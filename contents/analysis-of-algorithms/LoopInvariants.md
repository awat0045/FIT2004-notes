# Loop invariants
- All algorithms hinge on two main principles: correctness, and termination
- Loop invariants are invariants (things that remain true) in every iteration of a loop
- They help us to establish correctness in many simple algorithms

# Loop invariant example: Binary Search
- Here is some pseudocode for a binary search algorithm:
```
Algorithm 1 Binary Search
1: function BINARY_SEARCH(array[1..n], key)
2:   lo = 1 and hi = n + 1
3:   while lo < hi −1 do
4:     mid = b(lo + hi)/2)c
5:     if key ≥ array[mid] then lo = mid
6:     else hi = mid
7:   if array[lo] = key then return lo // key is located at array[lo]
8:   else return null // key not found
```
- Below is an invariant that can be used to prove the correctness of the above algorithm
```
If key ∈ array, then at each iteration:
  1. array[lo] ≤ key,
  2. if hi != n + 1, then array[hi] > key.
Combined with the sortedness of array, this implies that key (if it exists) lies within the
range [lo..hi).
```
## Proving correctness
We first prove the invariant is true at initialisation, then that it is true in every iteration
- When initialised, lo = 1 and h = n+1, so both invariants we determined earlier will hold
- In every iteration, we compute mid = (lo+hi)/2, and compare array[mid] to key. The conditional statement in the loop enforces the invariant
  1. If key ≥ array[mid], then after setting lo = mid, we will still have array[lo] ≤ key.
  2. If key < array[mid], then after setting hi = mid, we will still have array[hi] > key.

## Proving termination
We have determined that the algorithm is correct *if* it terminates, now we need to ensure that it actually terminates
```
Since mid is the floor of (lo + hi)/2, it is true that

(lo + hi)/2 − 1 < mid ≤ (lo + hi)2

Multiplying by two, we find
lo + hi − 2 < 2 × mid ≤ lo + hi.

Since lo < hi-1, we have lo ≤ hi-2. We replace hi-2 with lo on the left most term in the inequality.
2 × lo < 2 ×mid ≤ lo + hi.

Next, we add 1 to the right most term.
2 × lo < 2 ×mid < lo + hi + 1.

Since lo < hi-1, we have lo+1 < hi. We replace lo+1 with hi on the right most term.
2 × lo < 2 ×mid < 2 × hi.

and hence
lo < mid < hi

as desired
```
