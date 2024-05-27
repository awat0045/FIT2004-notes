# Binary search
Binary search is an algorithm used for searching sorted lists. It works by starting in the middle of the list, and checking if the item in the middle of the array is larger or smaller than the item we're searching for. If it's larger, we repeat the process on the right half of the list. If it's smaller, we repeat the process on the left half of the list.

## Pseudocode
```
Algorithm 1 Binary Search
1: function BINARY_SEARCH(array[1..n], key)
2:   lo = 1 and hi = n + 1
3:   while lo < hi −1 do
4:     mid = b(lo + hi)/2)c
5:     if key ≥ array[mid] then lo = mid
6:     else hi = mid
7: if array[lo] = key then return lo // key is located at array[lo]
8: else return null
```
## Time and space complexity
- In-place algorithm as all operations are done on the input list
- Time complexity is O(log n), where n is the number of elements in the array
  - The number of elements halves every iteration, therefore the algorithm can complete in logarithmic time
